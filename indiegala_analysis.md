# IndieGala DOM Analysis
*Last Updated: 2026-02-07 (v1.59 Planning)*

## 1. Store Page (`/store`)
### Grid Items (Modern Layout)
- **Container**: `.main-list-item` (was `.store-main-page-items-list-item-col`)
- **Structure**:
  - `div.main-list-item.relative`
    - `figure` (Product Image)
    - `a.fit-click` (Overlay Link, z-index: 10)
    - `.store-main-list-item-os-container` or `.main-list-results-item-data-platforms` (Platform Icons: Steam/Windows)
- **Overlay Strategy (v1.58)**:
  - Append to `figure`.
  - Set `figure { position: relative; }`.
  - Inject `a.ssl-steam-overlay` with `z-index: 20` inside `figure`.
  - Position: `bottom: 0; left: 0; width: 100%`.

## 2. Bundle Page (`/bundle/...`)
### Bundle Tiers / Items
- **Container**: `.bundle-item`, `.game-card`
- **Structure**:
  - Similar to Store: `figure` + `a.fit-click`.
- **Overlay Strategy**:
  - Same as Store (Figure Overlay).
  - Solves the "bottom of card" positioning issue.

## 3. Homepage (`/`)
### Top Sellers (Horizontal List)
- **Container**: `.relative` (wrapping `.item-inner`)
- **Key Children**:
  - `.item-inner`
  - `.item-left` (Image)
  - `.item-right` (Details)
    - `.item-title` -> `.item-title-span` (Title)
    - `.item-platforms` (Platform Icons: Steam, Windows, Apple)
- **Goal**:
  - Insert Steam Link/Badge **inside** `.item-platforms`.
  - Place it next to existing icons (`.fa-steam`, etc.).

### Selectors to Add
```javascript
// Homepage Top Sellers
{ 
    container: '.item-inner', // Or parent .relative?
    title: '.item-title-span' 
}
```
**Insertion Logic**:
- If `element.querySelector('.item-platforms')` exists:
  - Append Badge to `.item-platforms`.
  - Ensure styles match the small icon layout.
