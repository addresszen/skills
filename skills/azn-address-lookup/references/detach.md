# Detach Address Lookup

After instantiation, you can detach Address Lookup with `detach`.

```js
const controller = AddressLookup.setup(config);

// Removes Address Lookup from DOM and clears event listeners
controller.view.detach();
```

The same Address Lookup instance can be reconnected with `attach`.

```js
controller.view.detach();

// Restores Address Lookup to the DOM and starts event listeners
controller.view.attach();
```
