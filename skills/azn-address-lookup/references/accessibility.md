# Accessibility

Address Lookup is developed to meet [WCAG 2.1 Level AA](https://www.w3.org/TR/WCAG21/). It implements the WAI-ARIA combobox pattern, works with screen readers and is fully operable by keyboard.

## Screen Reader Support

The suggestion list is exposed as an ARIA combobox: the input carries `role="combobox"`, `aria-expanded` and `aria-controls`, and the suggestion list is a `listbox` of `option` elements. DOM focus stays on the input at all times - the highlighted suggestion is conveyed via `aria-activedescendant`, so screen reader users hear each suggestion as they arrow through it, along with its position in the list.

By default Address Lookup uses ARIA 1.0 authoring, which has the widest screen reader support (notably VoiceOver and NVDA). The [`aria` option](https://docs.addresszen.com/docs/address-lookup/configuration-reference) switches to ARIA 1.1 authoring if preferred.

A visually hidden live region announces events as they happen:

- The number of addresses found, e.g. `"10 addresses available"`
- With the first results only: the active search country and how to change it, e.g. `"Searching United States. Press Tab to change country"`
- The number of countries listed when selecting a country
- `"Country switched to United States"` after a change of country
- Confirmation that a selected address has been applied to the form
- Notices, e.g. `"No matches found"`

The `aria-label` on the suggestion list can be customized with the `msgList` option - see [Messages](https://docs.addresszen.com/docs/address-lookup/messages).

## Keyboard Support

| Key | Action |
| --- | --- |
| <kbd>↓</kbd> / <kbd>↑</kbd> | Move through suggestions, wrapping at either end |
| <kbd>Enter</kbd> | Select the highlighted suggestion and populate the form |
| <kbd>Escape</kbd> | Close the suggestion list and clear the input |
| <kbd>Home</kbd> / <kbd>End</kbd> | Return to the input |
| <kbd>Tab</kbd> | Move to the country toggle; press again to leave the widget |
| <kbd>Enter</kbd> / <kbd>Space</kbd> on the country toggle | Open the country list |

Clickable elements rendered by Address Lookup (the country toggle, the [no-match action](https://docs.addresszen.com/docs/address-lookup/no-match-action), the [unhide link](https://docs.addresszen.com/docs/address-lookup/hide)) are focusable buttons and respond to <kbd>Enter</kbd> and <kbd>Space</kbd>.

## Testing

Every release is gated by automated axe-core WCAG A/AA scans and keyboard regression tests covering the interactions above.

If you find an accessibility issue, please [report it](https://github.com/addresszen/feedback/issues) - accessibility defects are treated as bugs.
