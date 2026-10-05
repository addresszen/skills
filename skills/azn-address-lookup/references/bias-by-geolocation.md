# Bias By Geolocation

Biases the search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`.
Uses the format `bias_lonlat=[longitude],[latitude],[radius in meters]`. Only one geospatial bias may be provided.

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
    apiKey: "ak_test",
    queryOptions: {
      bias_lonlat: "74.0445,40.6892,100",
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
