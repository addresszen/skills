# Retrieve Additional Data

You may insert more address attributes into your form by expanding `outputFields`.

The key value should map to an address field described in the address schema.

In this example, we also populate organization name, county, congressional district and USPS carrier route.

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
  <label for="state_abbr">State Abbreviation</label>
  <input type="text" id="state_abbr" />
  <label for="zipcode">Zip Code</label>
  <input type="text" id="zipcode" />
  <!-- Additional fields -->
  <label for="organisation_name">Organization Name</label>
  <input type="text" id="organisation_name" />
  <label for="county">County</label>
  <input type="text" id="county" />
  <label for="congressional_district">Congressional District</label>
  <input type="text" id="congressional_district" />
  <label for="carrier_route">USPS Carrier Route</label>
  <input type="text" id="carrier_route" />
</form>
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "ak_test",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      state_abbreviation: "#state_abbr",
      zip_plus_4_code: "#zipcode",
      // Additional data
      building_or_firm_name: "#organisation_name",
      county: "#county",
      congressional_district_number: "#congressional_district",
      carrier_route_id: "#carrier_route",
    },
  });
```
