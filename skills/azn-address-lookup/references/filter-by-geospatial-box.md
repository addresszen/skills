# Filter By Geospatial Box

Restricts the search to a geospatial box determined by the `"top-left"` and `"bottom-right"` geolocations.
Only one geospatial box can be provided.

```html
<form>
  <label for="line_1">Address First Line</label>
  <input type="text" id="line_1" />
  <label for="line_2">Address Second Line</label>
  <input type="text" id="line_2" />
  <label for="city">City</label>
  <input type="text" id="city" />
  <label for="state">State</label>
  <input type="text" id="state" />
  <label for="zipcode">Zip Code</label>
  <input type="text" id="zipcode" />
</form>
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "zenkey",
    queryOptions: {
      box: "-73.989801,40.698141,-73.899698,40.652793",
    },
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4: "#zipcode",
    },
  });
```
