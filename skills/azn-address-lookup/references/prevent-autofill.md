# Prevent Autofill

Sets the `autocomplete=` attribute of the input element. Setting this attribute aims to prevent some browsers (particularly Chrome) from providing a clashing autofill overlay.

The best practice for this attribute breaks over time (see [https://stackoverflow.com/questions/15738259/disabling-chrome-autofill](https://stackoverflow.com/questions/15738259/disabling-chrome-autofill)) and is specific to different forms. If you are observing Chrome's autofill clashing on your form, update this attribute to the best practice du jour.

Defaults to `"none"`.
