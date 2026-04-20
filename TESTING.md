# End-to-End Testing Strategy — InterviewPrep App

## How to Run

1. Start the preview server (uses `.claude/launch.json`)
2. Open browser at `http://localhost:8001`
3. Run each section below using the browser console or Claude's `preview_eval` tool

---

## 1. Data Layer Validation

```js
// Verify all topics and questions loaded with valid IDs
(function() {
  var allHaveIds = ALL_TOPICS.every(t => t.qs.every(q => q.id !== undefined && q.id !== null));
  var missingIds = ALL_TOPICS.filter(t => t.qs.some(q => !q.id)).map(t => t.id);
  var totalQs = ALL_TOPICS.reduce((sum, t) => sum + t.qs.length, 0);
  console.log('Topics:', ALL_TOPICS.length);
  console.log('Total questions:', totalQs);
  console.log('All have IDs:', allHaveIds);
  console.log('Missing IDs in:', missingIds);
})();
```

**Expected:** 28 topics, 1169+ questions, `allHaveIds: true`, `missingIds: []`

---

## 2. Landing Page

- [ ] Page loads without blank screen
- [ ] Frontend/Backend toggle buttons visible
- [ ] Stats (question count, topic count) display correctly
- [ ] Topic cards render in grid

```js
// Check active view
['landingView','homeView','topicView','bookmarkView']
  .map(id => ({id, visible: !document.getElementById(id)?.classList.contains('off')}));
```

---

## 3. Frontend / Backend Section Switch

```js
showSection('frontend');
// Verify frontend topics shown
showSection('backend');
// Verify backend topics shown
```

- [ ] Frontend shows 3 topics (React, JavaScript, Next.js)
- [ ] Backend shows 25 topics

---

## 4. Topic Navigation

```js
showTopic('java');   // navigate to Core Java
```

- [ ] Topic header shows correct title, icon, description
- [ ] Difficulty breakdown stats (Easy / Medium / Hard) are correct
- [ ] Question list renders with numbered rows
- [ ] ⭐ bookmark button visible on each question row
- [ ] Back button returns to home

```js
// Verify question count and IDs
var java = ALL_TOPICS.find(t => t.id === 'java');
console.log('Questions:', java.qs.length);
console.log('First ID:', java.qs[0].id);  // should be 1
console.log('Last ID:', java.qs[java.qs.length-1].id);  // should equal qs.length
```

---

## 5. Question Expand / Collapse

```js
showTopic('java');
toggleQ(0);  // expand first question
var el = document.getElementById('qi-0');
console.log('Open:', el.classList.contains('open'));        // true
console.log('Has answer:', el.querySelector('.qans-in').innerHTML.length > 0); // true
toggleQ(0);  // collapse
console.log('Closed:', !el.classList.contains('open'));     // true
```

- [ ] Answer HTML renders (code blocks, lists, tables)
- [ ] Clicking again collapses

---

## 6. Bookmark Toggle — Core Functionality

```js
// Clear bookmarks for clean test
saveBookmarks(new Set());

showTopic('java');
var java = ALL_TOPICS.find(t => t.id === 'java');
var key = makeBookmarkKey('java', java.qs[0]);
console.log('Key format:', key);  // expected: "java:1"

toggleBookmark(key, null);

// Check only 1 button is active (not mass-select bug)
var activeCount = document.querySelectorAll('.bm-btn.bm-active').length;
console.log('Active buttons:', activeCount);  // must be 1, not all

// Check storage
console.log('Stored:', Array.from(getBookmarks()));  // ["java:1"]
```

**Critical check:** `activeCount` must be **1**. If it equals total questions, the mass-select bug has regressed (cause: `q.id` is undefined on question objects).

---

## 7. Bookmarks View

```js
// Add bookmarks across multiple topics
saveBookmarks(new Set());
var java = ALL_TOPICS.find(t => t.id === 'java');
var react = ALL_TOPICS.find(t => t.id === 'react');
toggleBookmark(makeBookmarkKey('java', java.qs[0]), null);
toggleBookmark(makeBookmarkKey('java', java.qs[4]), null);
toggleBookmark(makeBookmarkKey('react', react.qs[0]), null);

showBookmarks();
```

- [ ] Bookmarks view opens (not blank)
- [ ] Questions grouped by topic with topic label
- [ ] Badge count in nav matches bookmark count
- [ ] Removing a bookmark (⭐ click) removes it from list immediately
- [ ] "Clear" per-topic button removes only that topic's bookmarks
- [ ] "Clear All" removes everything

```js
// Validate all stored bookmarks resolve to real questions (no orphans)
(function() {
  var bms = Array.from(getBookmarks());
  var valid = bms.filter(key => {
    var colonIdx = key.indexOf(':');
    var topicId = key.substring(0, colonIdx);
    var qId = key.substring(colonIdx + 1);
    var topic = ALL_TOPICS.find(t => t.id === topicId);
    return topic && topic.qs.some(q => String(q.id) === qId);
  });
  console.log('Valid bookmarks:', valid.length + '/' + bms.length);
})();
```

---

## 8. Search

```js
// From home view
goHome();
var input = document.getElementById('gSearch');
input.value = 'java';
input.dispatchEvent(new Event('input', {bubbles: true}));
// Topic grid should filter to ~9 matching topics

input.value = '';
input.dispatchEvent(new Event('input', {bubbles: true}));
// All topics should reappear
```

- [ ] Search filters topic cards in real time
- [ ] Clearing search restores all topics
- [ ] No results state shows appropriate message

---

## 9. Dark / Light Theme Toggle

```js
toggleTheme();  // switch to light
toggleTheme();  // switch back to dark
```

- [ ] Theme switches visually (background color changes)
- [ ] Preference persists on reload (stored in localStorage)

---

## 10. Cache & Script Version Check

After any data file changes, verify the browser is loading the latest versions:

```js
// Check script src versions currently loaded
Array.from(document.querySelectorAll('script[src*="data/"]'))
  .map(s => s.src.split('/').pop());
```

- [ ] All data scripts have `?v=N` params matching `index.html`
- [ ] If IDs are showing as `undefined`, bump `?v=` in `index.html` and hard-reload

**Force reload without cache:**
```js
location.href = 'http://localhost:8001/?bust=' + Date.now();
```

---

## 11. Console Error Check

```js
// Run in browser DevTools console — should return nothing critical
// Or use Claude's preview_logs tool with level: "error"
```

- [ ] No `ReferenceError` or `TypeError` in console
- [ ] No `undefined` IDs on question objects
- [ ] No broken `data-key` attributes on bookmark buttons

---

## Common Bugs & Root Causes

| Symptom | Root Cause | Fix |
|---------|-----------|-----|
| All bookmarks activate on one click | `q.id` is `undefined` → all buttons get `data-key="topic:undefined"` | Bump `?v=` on data scripts in `index.html`; ensure all questions have `id:` field |
| Bookmarks view shows empty despite badge count | `q.id` is a `number` but key stores a `string`; strict `===` fails | Use `String(q.id)` in `makeBookmarkKey` and `renderBookmarks` |
| Topic view overlays landing page | `_activateTopic()` not hiding `landingView` | Add `document.getElementById('landingView').classList.add('off')` |
| Old cached files served | Browser caches `index.html` and data scripts | Navigate to `/?bust=<timestamp>` or bump `?v=` params |
| Questions missing IDs | Data file added without `id:` field | Run ID-assignment script; use `d:"easy|medium|hard"` pattern match |
