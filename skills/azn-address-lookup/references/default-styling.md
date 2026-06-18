# Default Styling

Address Lookup's default styling works by injecting a style tag into the document head.

To prevent this, set `injectStyle` to `false`.

To provide your own CSS stylesheet you can assign a CSS Stylesheet link to `injectStyle`. E.g.

```javascript
const d = `
.idpc_af.hidden {
    display:none
}

div.idpc_autocomplete {
  position:relative;
  margin:0!important;
  padding:0;
  border:0;
  color:#28282b;
  text-rendering:optimizeLegibility;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale
}

div.idpc_autocomplete > input {
  display:block
}

div.idpc_af {
  position:absolute;
  left:0;z-index:2000;
  min-width:100%;
  box-sizing:border-box;
  border-radius:3px;
  background:#fff;
  border:1px solid rgba(0,0,0,.3);
  box-shadow:.05em .2em .6em rgba(0,0,0,.2);
  text-shadow:none;
  padding:0;
  margin-top:2px
}

div.idpc_af > ul {
  list-style:none;
  padding:0;
  max-height:250px;
  overflow-y:scroll;
  margin:0!important
}

div.idpc_af > ul > li { 
  position:relative;
  padding:.2em .5em;
  cursor:pointer;
  margin:0!important
}

div.idpc_toolbar { 
  padding:.3em .5em;
  border-top:1px solid rgba(0,0,0,.3);
  text-align:right
}

div.idpc_af > ul > li:hover {
  background-color:#e5e4e2
}

div.idpc_af > ul > li.idpc_error {
  padding:.5em;
  text-align:center;
  cursor:default!important
}

div.idpc_af > ul > li.idpc_error:hover {
  background:#fff;
  cursor:default!important
}

div.idpc_af > ul > li[aria-selected=true] {
  background-color:#e5e4e2;
  z-index:3000
}

div.idpc_autocomplete >.idpc-unhide {
  font-size:.9em;
  text-decoration:underline;
  cursor:pointer
}

div.idpc_af > div > span {
  padding:.2em .5em;
  border-radius:3px;
  cursor:pointer;
  font-size:110%
}

span.idpc_icon {
  font-size:1.2em;
  line-height:1em;
  vertical-align:middle
}

div.idpc_toolbar > span span.idpc_country {
  margin-right:.3em;
  max-width:0;
  font-size:.9em;
  -webkit-transition:max-width .5s ease-out;
  transition:max-width .5s ease-out;
  display:inline-block;
  vertical-align:middle;
  white-space:nowrap;
  overflow:hidden
}

div.idpc_autocomplete > div > div > span:hover span.idpc_country {
  max-width:7em
}

div.idpc_autocomplete > div > div > span:hover {
  background-color:#e5e4e2;
  -webkit-transition:background-color .5s ease;
  -ms-transition:background-color .5s ease;
  transition:background-color .5s ease
}`;

```
