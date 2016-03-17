# Adblock detection code

## Guardian
app.js tries to create an element with id ad_unit dynamically and then checks if the display is getting set to "none" (Adblockers do this automatically)

```html
<div class="ad_unit" style="position: absolute; height: 10px; top: 0; left: 0; z-index: -1;">&nbsp;</div>
```

In case of Firefox, they check an additional css attribute -moz-binding for the presence of elemhidehit. Adblock plus creates such an attribute of the form about:abp-elemhidehit?(Math.Random)#

### Thoughts
Easy and simple implementation. Cannot detect cases where the adblock is a bit slow or executes after the detection call is finished. Cannot detect hosts based adblock.

## Wired
Tries to create an element with id "ob_ad" and classes "Ads_4 AD_area ADBox AdsRec"

```html
("div", "ob_ad", "width: 1px !important; height: 1px !important; position: absolute !important; left: -10000px !important; top: -1000px !important; border:none; padding: 0 0 0 0;");
className = "Ads_4 AD_area ADBox AdsRec";
```

### Thoughts
Spray the word "ad" multiple times in class names and hope it will get blocked somehow. They use a timer so that they can detect even adblockers that are slow or hide elements after a small delay (Learn from these guys Guardian!). They also store the result in localStorage so even if you turn off or whitelist adblock you will still get that annoying popup (Why?). There are some unused code which tries to detect if an ad failed to load properly in a particular iframe. Don't think the logic used is correct anyways :)
