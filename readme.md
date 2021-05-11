# Modal Pattern

The Modal Pattern is an accessible modal dialog that uses the [Patterns Scripts dialog utility](https://github.com/CityOfNewYork/patterns-scripts/tree/main/src/dialog) to achieve the showing, hiding, and attribute toggling.

The modal element will be hidden from screen readers using the `aria-hidden` attribute and potentially focusable children will have their tabindex set to `-1` when the modal is hidden. When the modal is opened, focus will shift from the `data-dialog="open"` element to the `data-dialog="close"` element inside the modal. The focus will be trapped, meaning tabbing focus will cycle through elements within the dialog.

Additionally, scrolling can be disabled with the `data-dialog-lock="true"` attribute on the opening element trigger. This will toggle `overflow-hidden` on the body element until the dialog is dismissed. `overflow-hidden` is a Tailwindcss utility that will need to be set in your stylesheet if it doesn't exist (for example `.overflow-hidden { overflow: hidden }`).

## Usage

### ES Module

This method is a wrapper around the [Patterns Scripts dialog utility](https://github.com/CityOfNewYork/patterns-scripts/tree/main/src/dialog) which is included as a dependency of this project. The utility can be imported as an ES module and instantiated.

```javascript
import Modal from '@nycopportunity/pattern-modal/src/modal';

new Modal();
```

### Styles

The Modal Pattern includes two stylesheets. One that sets default design tokens using [CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties) and one that applies the tokens to the modal CSS selectors. The tokens can be used as is or overridden.

```scss
@import '@nycopportunity/pattern-modal/src/tokens';
@import '@nycopportunity/pattern-modal/src/modal';
```

### Markup

Below is the minimum required markup for the Modal Pattern.

```html
<button data-js="dialog" data-dialog-lock="true" data-dialog="open" aria-controls="aria-c-modal" aria-expanded="false">Show Modal</button>

<div id="aria-c-modal" class="o-modal hidden" aria-hidden="true" role="dialog" aria-modal="true" aria-labelledby="aria-lb-modal-header" aria-describedby="aria-db-modal-body">
  <div class="o-modal__layout">
    <div class="o-modal__body animated fadeInUp">
      <button data-js="dialog" aria-controls="aria-c-modal" data-dialog="close" aria-expanded="false" tabindex="-1">
        Dismiss
      </button>

      <h3 id="aria-lb-modal-header">{{ Your custom modal header }}</h3>

      <p id="aria-db-modal-body">{{ Your custom modal body }}</p>

      <button data-js="dialog" aria-controls="aria-c-modal" aria-expanded="false" tabindex="-1">
        Cancel
      </button>

      <button tabindex="-1">
        {{ Your custom modal action button }}
      </button>
    </div>
  </div>
</div>
```

#### Potentially Focusable Elements

The Patterns Scripts dialog utility uses the [toggling utility](https://github.com/CityOfNewYork/patterns-scripts/tree/main/src/toggle#attributes) from the same library. Potentially focusable elements will need to have their `tabindex` set to `-1` before the modal is toggled open. A full list of elements can be found in the documentation for the Toggle Utility.

#### Data Attributes

Attribute                 | Description
--------------------------|-
`data-js="dialog"`        | Triggers the modal event listeners.
`data-dialog="open"`      | Triggers the modal opening event listener.
`data-dialog="close"`     | Triggers the modal closing event listener and designates the target for the focus shift from the open to close button. It must be the first focusable element inside the modal.
`data-dialog-lock="true"` | Configures the modal to lock scrolling on the body by toggling the `overflow-hidden` CSS utility.

#### Aria Attributes

Attribute          | Description
-------------------|-
`aria-controls`    | Should be present on the modal opening and closing buttons. Describes what the button controls.
`aria-expanded`    | Describes when the target of the open or closed button is toggled "on" or "off"
`aria-hidden`      | Describes the visibility state of the modal. This should be set to true before the modal is opened.
`aria-labelledby`  | Should be present on the modal element and set to the `id` of the main heading in the modal. Describes the modal heading, or, the main message inside the modal when it is opened.
`aria-describedby` | Should be present on the modal element and set to the `id` of the body text in the modal. Describes the modal body and supporting text.

