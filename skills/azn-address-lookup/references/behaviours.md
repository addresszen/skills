# Behavior

This guide outlines technical details about how Address Lookup behaves and interacts with the DOM.

## DOM Changes

When the primary input has been identified, for accessibility reasons, Address Lookup will wrap the input field in a `<div>` and insert a hidden Address Lookup UI as sibling elements.

Thus your primary input will likely go from this:

```html
<input type="text" id="line_1" name="line_1">
```

To this:

```html
<div class="idpc_autocomplete" id="idpcaf1" aria-haspopup="listbox">
  <input type="text" id="line_1" name="line_1" autocomplete="none" aria-autocomplete="list" aria-controls="idpcaf2" aria-activedescendant="" autocorrect="off" autocapitalize="off" spellcheck="false" role="combobox" aria-expanded="false" aria-owns="idpcaf2">
  <ul class="idpc_ul" id="idpcaf2" aria-label="Select your address" role="listbox" style="display: none;">
    <li class="idpc_error">Start typing to find address</li>
  </ul>
  <div style="border:0px;padding:0px;clip:rect(0px,0px,0px,0px);height:1px;margin-bottom:-1px;margin-right:-1px;overflow:hidden;position:absolute;white-space:nowrap;width:1px">
    <div id="idpcaf3" role="status" aria-live="polite" aria-atomic="true"></div>
    <div id="idpcaf4" role="status" aria-live="polite" aria-atomic="true"></div>
  </div>
</div>
```

Address suggestions will appear as `<li>` elements in the above `<ul>` like this:

```html
<div class="idpc_autocomplete" id="idpcaf1" aria-haspopup="listbox">
  <input type="text" id="line_1" autocomplete="none" aria-autocomplete="list" aria-controls="idpcaf2" aria-activedescendant="" autocorrect="off" autocapitalize="off" spellcheck="false" role="combobox" aria-expanded="false" aria-owns="idpcaf2">
  <ul class="idpc_ul" id="idpcaf2" aria-label="Select your address" role="listbox" style="display: none;">
    <li aria-selected="false" tabindex="-1" aria-posinset="1" aria-setsize="10" role="option" id="idpcaf2_0">123 Space, 123 Cheltenham Road, Bristol, BS6</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="2" aria-setsize="10" role="option" id="idpcaf2_1">123 News, 123 Morrison Street, Edinburgh, EH3</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="3" aria-setsize="10" role="option" id="idpcaf2_2">Salon 123, 123 High Street, Herne Bay, CT6</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="4" aria-setsize="10" role="option" id="idpcaf2_3">123 Cleaners, 123 Shirland Road, London, W9</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="5" aria-setsize="10" role="option" id="idpcaf2_4">123 Bargates, Christchurch, BH23</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="6" aria-setsize="10" role="option" id="idpcaf2_5">123 Broadway, Cardiff, CF24</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="7" aria-setsize="10" role="option" id="idpcaf2_6">123 Greenways, Gloucester, GL4</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="8" aria-setsize="10" role="option" id="idpcaf2_7">123 Holloway, Birmingham, B31</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="9" aria-setsize="10" role="option" id="idpcaf2_8">123 Hornbeams, Harlow, CM20</li>
    <li aria-selected="false" tabindex="-1" aria-posinset="10" aria-setsize="10" role="option" id="idpcaf2_9">123 Kingsway, Hereford, HR1</li>
  </ul>
  <div style="border:0px;padding:0px;clip:rect(0px,0px,0px,0px);height:1px;margin-bottom:-1px;margin-right:-1px;overflow:hidden;position:absolute;white-space:nowrap;width:1px">
    <div id="idpcaf3" role="status" aria-live="polite" aria-atomic="true">10 addresses available</div>
    <div id="idpcaf4" role="status" aria-live="polite" aria-atomic="true"></div>
  </div>
</div>
```
