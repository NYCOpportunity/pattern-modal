The **Modal Pattern** is an accessible modal dialog that focuses user attention on a specific task. It follows the same usage guidelines of the <a href="https://designsystem.digital.gov/components/breadcrumb/" target="_blank" rel="noopener">Modal Component in the U.S. Web Design System (USWDS)</a>. It uses the <a href="https://github.com/CityOfNewYork/patterns-scripts/tree/main/src/dialog" target="_blank" rel="noopener nofollow">Patterns Scripts dialog utility</a> to achieve the showing, hiding, and attribute toggling. The animation uses CSS and will be disabled by devices using the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion" target="_blank" rel="noopener nofollow">prefers-reduced-motion</a> `@media` query.

---

The element will be hidden from screen readers using the `aria-hidden` attribute and potentially focusable children will have their tabindex set to `-1` when the modal is hidden. When the modal is opened, focus will shift from the `data-dialog="open"` element to the `data-dialog="close"` element inside the modal. The focus will be trapped, meaning tabbing focus will cycle through elements within the dialog.

---

Additionally, scrolling can be disabled with the `data-dialog-lock="true"` attribute on the opening element trigger. This will toggle `overflow-hidden` on the body element until the dialog is dismissed. `overflow-hidden` is a Tailwindcss utility that will need to be set in your stylesheet if it doesn't exist (for example `.overflow-hidden { overflow: hidden }`).
