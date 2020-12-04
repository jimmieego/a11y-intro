# Accessibility for Developers

## Semantic HTML

### Accessibility tree

- Browser's responsibility to expose accessibility tree to assistive technologies.
- Shows how webpage is interpreted by assistive technologies and how accessible data are provided.
- Assistive technologies simulate and relay user interactions like click and key press to accessibility tree.
- As developers, we need to:
 - Express the semantics of page correctly
 - Specify accessible names and descriptions
 - Make sure important elements have correct accessible roles, states, and properties

### Semantics in native HTML

- Most HTML elements have implicit semantics (role and state).
- Native HTML elements are recognized by browsers and work predictably on a variety of platforms.
- We should take advantage of built-in accessibility by writing HTML that expresses the semantics of page elements.
- Example: `<a href="http://www.esri.com">Esri Homepage</a>`
 - Role="link"
 - Accessible name="Esri Homepage"
 - State="focusable"
- Example: `<label><input type="checkbox" checked>Working at Esri </label>`  
 - Role="checkbox"
 - Accessible name="Working at Esri"
 - State="focusable checked"   

### Neutral semantics

- Some HTML elements do not convey semantics (role or state)
 - `<div>This is a block area</div>`
 - `<span>This is an inline area</span>`
- If the element is interactive, we need to do extra work:
 - Make it focusable: `tabindex="0"`
 - Receive keyboard events: <kbd>Enter</kbd>, <kbd>Space</kbd>
 - Name: explicit label (`label`) or implicit text (`aria-label`, `aria-labelledby`)

### Use cases of common semantic HTML elements

- `ul` and `ol`
- `button`
- `a`
- `<label>`

## Keyboard and focus management

### Keyboard

- Interactive native HTML elements receive keyboard focus
 - `<a href>`
 - `<button>`
 - `<input>`
- Interactive elements have expected interactions:
 - Link: click, tap, or <kbd>Enter</kbd> key
 - Button: click, tap, <kbd>Enter</kbd> key, or <kbd>Space</kbd> key
 - Input: click, tap, or <kbd>Enter</kbd> key   

### Focusable elements

- Native interactive HTML elements are focusable:
 - Text fields
 - Buttons
 - Links
 - Select lists
- Not focusable:
 - Paragraphs
 - Divs and spans
 - Headings

We should only focus elements that keyboard users need to interact with. Screen reader users have ways to read focusable and non-focusable elements (tab mode and browse mode).

### Manage focus

Set `tabindex = "0"` and let DOM structure determine focus order. Sometimes we need to set `tabindex = "-1"` to programmatically move focus. In general, setting `tabindex` to a positive integer is anti-pattern.

### Offscreen elements

- Example: [Calcite drawer pattern](http://esri.github.io/calcite-web/documentation/patterns/#drawers)
- Prevent the panel from gaining focus when it's off screen
- Only allow it to be focused when the user can interact with it
- Set `display:none` or `visibility:hidden` when off screen
- Set `display:block` or `visibility:visible` before showing it to user

## ARIA

### What is ARIA

- Specification for increasing accessibility of custom elements
- Allows developers to modify and augment accessibility tree from standard DOM
- ARIA doesn't augment any of the element's inherent behavior:
 - Focusable
 - Keyboard event listeners
- Custom behaviors still need to be implemented

### Why ARIA

- Native HTML semantics should still be used whenever possible, but ARIA is useful when certain semantics, design patterns, or interactions make it impossible to do so.
 - Example: a pop-up menu, no standard HTML element
 - Example: a semantic characteristic "the user needs to know about this as soon as possible"

### ARIA attributes

- **Roles**
 - Landmarks
 - Widgets
- **Labels**
 - `aria-label`
 - `aria-labelledby`
- **Relationships**
 - `aria-owns`
 - `aria-describedby`
 - `aria-controls`

### Roles

- Landmarks
 - `banner`: The main header of a page; typically assigned to a header element.
 - `contentinfo`: A collection of metadata, copyright information and the like.
 - `main`: the main content of a document.
 - `navigation`: A collection of links for navigation.
- Widgets
 - `alert`
 - `dialog`
 - `data grid`
 - `tab`
 - `tablist`
 - `tabpanel`

### Labels

- `aria-label`
 - Specifies a string as accessible label
 - Overrides native labeling
- `aria-labelledby`
 - Specifies `id` of another element in the DOM as label of current element
 - Overrides all other name sources
 - Could be used on any element, not just labelable elements
 - Could take a list of `id`s
 - Could specify visually hidden elements  

### Relationships

- `aria-owns`
 - Indicates an element should be treated as parent of another separate element in the DOM  
- `aria-describedby`
 - Provides an accessible description for an element
 - References elements in the DOM separated from current element
- `aria-controls`
 - Indicates an element "controls" another element in interaction  


### ARIA use cases

- Label and description
- Relationship
- States
- Hide elements
- Update elements

### ARIA best practices

- Don't change native semantics, unless you really have to.
- All interactive elements must be usable with keyboard.
- Don't use `role="presentation"` or `aria-hidden="true"` on a visible and focusable element.
- All interactive elements must have an accessible label or name.

## A dev checklist

| Requirement   | Description   |
| ------------- | ------------- |
| Focusable     | Can you get to the element via keyboard?  |
| Operable      | Can you use the element with keyboard?    |
| Expected operation  | Does the element match [WAI-ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices/)?    |
| Focus visible      | Can you see when the element has keyboard focus?   |
| Label      | Does the element have accessible text label?    |
| Role      | Does the element have appropriate ARIA role?   |
| States and properties      | Does the element have any ARIA states and properties to show UI changes?    |

### Text alternatives

- Every `<img>` must have an `alt` attribute.
- Images that contain information or perform actions require descriptive `alt` text.
- The `alt` attribute should describe the information conveyed by the image, not the image itself.
- Decorative images should have empty `alt` text.

### Semantic HTML

- Tabular data should be in `<table>`.
- Headings are in `<h1>` - `<h6>` elements.
- Lists have list item (`<li>`) elements wrapped in `<ul>` or `<ol>` elements.
- Inputs (`<input>`) should always have a `<label>`, `aria-label`, or `aria-labelledby`.
- Set up ARIA [landmark roles](https://www.w3.org/TR/wai-aria/roles#landmark_roles).
- [WAI-ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices-1.1/) provides detailed design patterns of accessible web components such as accordion, dialog, tabs, etc.

### Tab order and focus

- Use `tabindex="0"` and let the natural DOM structure determine the keyboard tab order.
- Avoid jumping around keyboard focus
- Show clear focus indicator for interactive elements
- Do not set `outline:none` to focusable elements, unless using customized focus style

### Color

- Provide additional indication that does not rely on color perception
- Minimum color contrast ratio is **4.5** for normal text, 3 for larger text (at least 24 px or 19 px bold)

### Label

- Associate `label` with form control
- Avoid replacing visual label with placeholder text
- Use `aria-label`, `aria-labelledby`, and `aria-describedby` if needed

## Dev Tools

- [axe-core](https://github.com/dequelabs/axe-core)
- [eslint-plugin-jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y)