---
name: browser-extension
description: Build Chrome/Chromium browser extensions for browser automation, content manipulation, or page interaction. Use this skill whenever the user wants to create a Chrome extension, browser extension, auto-clicker, page scraper, content script, browser automation tool, or anything that injects JavaScript into web pages. Also trigger when the user mentions manifest.json, content scripts, popup.html, chrome.scripting, chrome.storage, or describes wanting to "click through" or "automate" something in their browser. Covers Manifest V3 extensions for Chrome, Arc, Brave, Edge, and other Chromium browsers.
---

# Browser Extension Development

## When to Use This Skill

Use this when the user wants to build, debug, or modify a Chrome/Chromium browser extension. This includes auto-clickers, page scrapers, content injectors, UI overlays, or any tool that interacts with web page content programmatically.

## Extension Architecture (The Mental Model)

A Chrome extension has three layers. Understand these before writing any code.

**1. manifest.json**: The ID card. Tells Chrome what the extension is called, what permissions it needs, and what files to load. Every extension must have one.

**2. popup.html + popup.js**: The remote control. The little panel that appears when the user clicks the extension icon. Use it for settings, start/stop buttons, and status display.

**3. Content scripts (injected JS)**: The worker. Code that runs inside the actual web page. This is where DOM manipulation, element clicking, and page interaction happen.

## Manifest V3 Template

Always use Manifest V3 (V2 is deprecated). Here is the minimal starting template:

```json
{
  "manifest_version": 3,
  "name": "Extension Name",
  "version": "1.0",
  "description": "What it does.",
  "permissions": ["activeTab", "scripting", "storage"],
  "host_permissions": ["<all_urls>"],
  "action": {
    "default_popup": "popup.html",
    "default_icon": { "48": "icon.png" }
  },
  "icons": { "48": "icon.png", "128": "icon.png" }
}
```

### Permission Notes

- `activeTab`: Access to the current tab when the user clicks the extension icon.
- `scripting`: Required to inject JavaScript into pages via `chrome.scripting.executeScript`.
- `storage`: Persist settings across sessions with `chrome.storage.local`.
- `notifications`: System-level notifications (OS toast popups).
- `host_permissions: ["<all_urls>"]`: Required to inject into cross-origin iframes. Without this, the extension can only access same-origin content.

Only request permissions you actually need. Users see a permissions prompt on install.

## Injecting Scripts into Pages

Use `chrome.scripting.executeScript` from popup.js to inject code into the active tab:

```javascript
await chrome.scripting.executeScript({
  target: { tabId: tab.id, allFrames: true },
  func: myFunction,
  args: [arg1, arg2]
});
```

### Critical: The `allFrames` Flag

`allFrames: true` injects into every frame on the page, including iframes. This is essential when the target content lives inside an iframe (very common with embedded training platforms, SCORM wrappers, and third-party widgets).

However, `allFrames: true` means the script runs in EVERY frame. This causes duplicate instances if you are not careful. Always gate your script logic based on which frame it is running in. See the Iframe Problem section below.

## The Iframe Problem (Most Common Issue)

**Symptom:** The script clicks things, but nothing happens on screen. Or the click counter goes up but the page does not respond.

**Cause:** The content the user cares about is inside a cross-origin iframe. The script is running on the parent page and clicking the wrong elements.

**How to diagnose:** Ask the user to right-click on the actual content, click Inspect, and look at the bottom of the Elements panel for an iframe breadcrumb. If the URL domain in the iframe differs from the parent page, you have a cross-origin iframe situation.

**How to fix:** Check `window.location.href` inside the injected script. Assign different roles based on domain:

```javascript
const loc = window.location.href.toLowerCase();
const isTargetSite = loc.includes('targetdomain.com');
const isTop = (window === window.top);

if (isTop && !isTargetSite) {
  // Parent page: show UI only, no clicking
}
if (isTargetSite) {
  // Target frame: do the actual work
}
```

### Nested Iframe Deduplication

When there are nested iframes on the same domain (e.g., a SCORM wrapper and a content frame both on the same training-platform domain), the script runs in both. Fix this by checking for child iframes:

```javascript
const childIframes = document.querySelectorAll('iframe');
let hasTargetChild = false;
for (const f of childIframes) {
  if ((f.src || '').includes('targetdomain.com')) {
    hasTargetChild = true;
    break;
  }
}
if (hasTargetChild) {
  // This is a wrapper frame. Defer to the inner frame.
  // Only relay messages, do not click anything.
  return;
}
```

### Cross-Frame Communication

Use `postMessage` for communication between frames:

```javascript
// Child frame sends status to parent
window.top.postMessage({ type: 'status', msg: 'Clicked button' }, '*');

// Parent frame listens
window.addEventListener('message', (e) => {
  if (e.data && e.data.type === 'status') {
    updateBadge(e.data.msg);
  }
});

// Parent sends commands to child frames
const iframes = document.querySelectorAll('iframe');
for (const f of iframes) {
  try { f.contentWindow.postMessage({ type: 'resume' }, '*'); } catch(e) {}
}
```

## Element Targeting Strategy

This is the core challenge of any browser automation extension. The page has many elements. You only want to interact with some of them.

### Priority: Ask the User for outerHTML

The single most effective thing is to get the actual HTML of target elements. Ask the user to:

1. Right-click the element they want to interact with.
2. Click **Inspect**.
3. Right-click the highlighted element in the Elements panel.
4. Choose **Copy > Copy outerHTML**.
5. Paste it into the conversation.

This gives you exact class names, data attributes, aria-labels, SVG viewBox values, and DOM structure. It eliminates guessing.

### Selector Priority (Most Reliable to Least)

1. **Unique IDs**: `#submitBtn`: most stable, but rare on dynamic sites.
2. **Data attributes**: `[data-testid="next-button"]`: developers put these in deliberately, they tend to stick around.
3. **Aria labels**: `[aria-label="Play the audio"]`: accessibility attributes, fairly stable.
4. **Specific class names**: `.progressSvg`: stable if intentionally named.
5. **Generated class names**: `.sc-bXCLTC`: styled-components/CSS-in-JS hashes. UNSTABLE. These change between builds. Never rely on these alone.
6. **Tag + attribute combos**: `svg[viewBox="0 0 77 68"]`: good for identifying specific icons by their dimensions.
7. **Text content matching**: Searching for buttons with text "Next" or "Continue": works but is fragile across languages.
8. **Color/position heuristics**: Checking computed styles for orange backgrounds, or filtering by pixel position: last resort, very fragile.

### Building an Allow-List and Block-List

For automation that clicks buttons, define two lists:

**Allow-list (click these):**
```javascript
const NAV_PATTERNS = [
  /^next$/i, /^continue$/i, /^proceed$/i,
  /^start$/i, /^ok$/i, /^agree$/i,
];
```

**Block-list (never click these):**
```javascript
const AVOID_PATTERNS = [
  /^(settings|help|menu|back|close|exit)/i,
  /^(download|print|share|save)/i,
];
```

Also block by selector for known UI chrome:
```javascript
const NEVER_CLICK = [
  '[class*="vjs-"]',       // Video.js player
  '[class*="toolbar" i]',  // Toolbars
  '[class*="settings" i]', // Settings buttons
  '[class*="menu" i]',     // Menus
];
```

### Position-Based Filtering

When toolbar buttons are in predictable locations (e.g., top corners), add a position check:

```javascript
function isInToolbar(el) {
  const rect = el.getBoundingClientRect();
  if (rect.top < 70) return true;  // Top strip
  return false;
}
```

### Two-State Elements

Elements change state. The same DOM node can show different content depending on its state. Always ask the user about both states.

Example: An audio button shows a speaker icon when unplayed and a checkmark when completed. Both use the same `<button>` element. Differentiate by checking what is inside:

```javascript
const speakerSvg = btn.querySelector('svg[viewBox="0 0 77 68"]');
const checkSvg = btn.querySelector('svg[viewBox="0 0 13 10"]');
if (speakerSvg) { /* unplayed, click it */ }
if (checkSvg) { /* completed, skip it */ }
```

## Click Priority Systems

When a page has multiple interactive elements that must be completed in order, implement a priority system in the main loop:

```javascript
function tick() {
  // Priority 1: Wait for media to finish
  if (isMediaPlaying()) return;

  // Priority 2: Interactive elements (audio buttons, hotspots)
  const interactive = findInteractiveElements();
  if (interactive.length > 0) { interactive[0].click(); return; }

  // Priority 3: Step cards / flip cards
  const cards = findStepCards();
  if (cards.length > 0) { cards[0].click(); return; }

  // Priority 4: Navigation (Next/Continue)
  const nav = findNavButton();
  if (nav) { nav.click(); return; }
}
```

The key rule: never advance to a lower priority until the higher priority is fully resolved.

## Media Playback Detection

When the page has audio or video that must complete before advancing:

```javascript
function isMediaPlaying() {
  for (const a of document.querySelectorAll('audio')) {
    if (!a.paused && !a.ended) return true;
  }
  for (const v of document.querySelectorAll('video')) {
    if (!v.paused && !v.ended) return true;
  }
  return false;
}
```

Only check HTML5 `<audio>` and `<video>` elements. Avoid checking CSS animations or class names for playback state as these produce false positives.

## Third-Party Player Avoidance

Embedded players (Video.js, YouTube, Vimeo) create real button elements in the DOM. An auto-clicker will find and click these unless explicitly blocked.

Common patterns to block:
- Video.js: `[class*="vjs-"]`
- YouTube: `[class*="ytp-"]`
- Vimeo: `[class*="vp-"]`

Add these to the never-click selector list.

## User Notification Strategies

When the extension needs to alert the user (e.g., quiz detected), choose based on context:

| Method | When to Use |
|--------|-------------|
| In-page overlay | User is looking at the tab |
| Tab title flashing | User is on another tab in the same browser |
| System notification (Notification API) | User is in a different app entirely |

For system notifications, request permission early:
```javascript
if ('Notification' in window && Notification.permission === 'default') {
  Notification.requestPermission();
}
```

Sound-based alerts are unreliable because users often mute tabs. Prefer visual notifications.

## Status Badge Pattern

A floating status badge in the corner of the page helps the user see what the extension is doing:

```javascript
const badge = document.createElement('div');
badge.style.cssText = 'position:fixed;bottom:20px;right:20px;z-index:999999;' +
  'background:#1a1a2e;color:#e0e0e0;padding:14px 20px;border-radius:12px;' +
  'font-family:system-ui;font-size:13px;box-shadow:0 4px 20px rgba(0,0,0,0.3);';
document.body.appendChild(badge);
```

Only create the badge in the top frame. Child frames should send status messages to the parent via postMessage.

## Debugging Workflow

When the extension is not working as expected, follow this sequence:

1. **Check the console.** Press F12, go to Console, and look for log messages from the extension (prefix all logs with a tag like `[AC]`).
2. **Check which frame you are in.** The console has a frame selector dropdown at the top. Switch to the iframe's context to see logs from the injected script.
3. **Check what it is clicking.** Log the element's text content, class name, and tag name on every click.
4. **Check what it is skipping.** When debugging targeting, temporarily log elements that are being filtered out and why.

Always prefix console logs so the user can find them:
```javascript
console.log('[AC] Clicked:', element.textContent.trim().substring(0, 40));
```

## Asking the User the Right Questions

When the user reports a problem, here is what to ask for:

- "What does the console say?": Check for `[AC]` prefixed log lines.
- "Right-click the button it should be clicking, Inspect it, and copy the outerHTML for me.": Gets exact selectors.
- "Right-click the button it should NOT be clicking, Inspect it, and copy the outerHTML.": Identifies what to block.
- "Is the content inside an iframe?": Check the frame breadcrumb in the Elements panel.
- "What does it look like before and after you click it?": Identifies two-state elements.

## Extension File Structure

```
extension-name/
├── manifest.json    # Config and permissions
├── popup.html       # Extension popup UI
├── popup.js         # Popup logic and script injection
└── icon.png         # Extension icon (128x128, transparent PNG)
```

For simple extensions, keep everything in popup.js. The injected function is defined inside popup.js and passed to `chrome.scripting.executeScript`. This avoids needing separate content script files.

## Loading and Updating the Extension

Guide the user through these steps:

1. Open `chrome://extensions` in the browser (works in Chrome, Arc, Brave, Edge).
2. Enable **Developer mode** (toggle in the top right).
3. Click **Load unpacked**.
4. Select the extension folder (the folder itself, not a file inside it).
5. To update: Remove the old version, unzip the new one, Load unpacked again.

Note: Chrome may require the user to type `allow pasting` in the console the first time they paste a script. This is a security measure and is normal.

## Common Pitfalls

1. **Clicking in the wrong frame.** Always check iframe context first.
2. **Duplicate script instances.** Gate logic by URL or frame depth.
3. **Clicking video player buttons.** Blacklist all player UI selectors.
4. **Relying on generated class names.** Use data attributes, aria labels, or element structure instead.
5. **Not waiting for media.** Check `<audio>` and `<video>` element states before advancing.
6. **Blocking on CSS animations.** Only use HTML5 media element `.paused` / `.ended` for playback detection. CSS class checks produce false positives.
7. **Elements that change state.** Always ask what the element looks like in each state and differentiate by inner content, not just the outer wrapper.
8. **Over-eager clicking.** Build allow-lists (what to click) and block-lists (what to never click) from the start.
