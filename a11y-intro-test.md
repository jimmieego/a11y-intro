# Testing Accessibility

## Why accessibility testing

- Accessibility is about the experience of all users
- Users using assistive technologies (keyboard, screen reader) should have functionally equilvalent experience
- Testing is the only way to ensure the experience is accessible
- The goal is to verify how well web content functions as WCAG 2.0/2.1 specified

## Test process

Automated test > Keyboard test > Screen reader test > Color accessibility

## What to test

- Critical workflows
- Important pages
- UI components

## Automated test with aXe

- Tests rendered DOM
- Aims at no false positives
- Accessible
- Helpful documentation
- Automated test is good starting point but cannot detect all accessibility issues
- Run automated test of different page states (modals, accordions, tabs)

### Practice aXe

Use aXe to test an example app, [Park Locator](http://arcg.is/05DzDX)

## Keyboard test

### Keyboard navigation

### Expected outcomes

- [2.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html): Interact with all controls, links, and menus using only keyboard
- [2.4.7](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html): See what item has focus at all times.
- [2.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html): Visual focus order matches intended interaction order.
- [2.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html): No keyboard trap.
- [2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html): Bypass blocks of content that are repeated on multiple pages. 
- Off-screen content (e.g., responsive navigation) should not receive focus when invisible.

References:

- [Nutrition Cards for Accessible Components](https://davatron5000.github.io/a11y-nutrition-cards/): outlines expected behavior for common interactive components.

### Practice keyboard test

- Test app
  - [Park Locator](http://servicesbeta.esri.com/demos/a11y/index.html)
- Tools
  - [Enhanced focus](https://pauljadam.com/demos/focusvisible.html)
  - Live Expression in Chrome DevTools: `document.activeElement` ([source](https://developers.google.com/web/tools/chrome-devtools/accessibility/focus))
  
  ```javascript
  document.body.addEventListener('focusin', (event) => {
    console.log(document.activeElement)
  })
  ```

## Screen reader test

### Screen readers

- Narrator
- VoiceOver
- NVDA
- JAWS

### Screen reader commands

- Turn on
- Stop
- Modifier key
- Read next/previous item
- Interact with links, buttons, and form controls
- Open rotor

References:

- [Basic screen reader commands for accessibility testing](https://developer.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/)

### Screen reader testing coverage

- Navigation
  - Headings
  - Links
  - Landmarks
  - Menus
- Content
  - Alt text
  - Tables
- Interaction
  - Forms
  - Modals
  - Widgets

### Practice screen reader test

Use VoiceOver to test an example app, [Park Locator](http://arcg.is/05DzDX)

## Color accessibility test

### Expected outcomes

- [1.4.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html): Not use presentation that relies solely on color.
- [1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html): Color contrast ratio is at least 4.5:1.
- [1.4.11](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast): UI components and graphics have at laeast 3:1 contrast against adjacent colors.

### Practice color test

- Test app
  - [Park Locator](http://servicesbeta.esri.com/demos/a11y/index.html)
- Tools
  - [Chrome color picker & accessibility pane](https://developers.google.com/web/tools/chrome-devtools/accessibility/reference#pane)
  - [Contrast ratio calculator](https://contrast-ratio.com/)

## Summary

- Start with automated test, then do keyboard, screen reader, and color test.
- Need to understand [WCAG Success Criteria](https://www.w3.org/TR/WCAG21/).
- Get familiar with [ARIA Best Practices](https://www.w3.org/TR/wai-aria-practices-1.1/).
- The ultimate decision-maker about whether or not something is accessible, is whether or not people can use it.