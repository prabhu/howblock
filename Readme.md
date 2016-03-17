# Adblock detection code

## Guardian

app.js tries to create an element with id ad_unit dynamically and then checks if the display is getting set to "none" (Adblockers do this automatically)

```html
<div class="ad_unit" style="position: absolute; height: 10px; top: 0; left: 0; z-index: -1;">&nbsp;</div>
```

In case of Firefox, they check an additional css attribute -moz-binding for the presence of elemhidehit. Adblock plus creates such an attribute of the form about:abp-elemhidehit?(Math.Random)#

