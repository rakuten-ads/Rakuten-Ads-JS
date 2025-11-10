# Interstitial Ads Documentation

## Overview

Interstitial ads are full-screen advertisements that cover the entire viewport. They are displayed at natural transition points in your application.

## API Reference

### `defineAd(id: number, elementId: string)`

Defines an ad spot.

### `loadInterstitialAd(id: string): Promise<void>`

Loads an interstitial ad. Must be called before showing.

### `showInterstitialAd(): void`

Displays the loaded interstitial ad in full-screen mode.

## Complete Example

```html
<!doctype html>
<html>
  <head>
    <title>Interstitial Ad Example</title>
  </head>
  <body>
    <h1>My App</h1>
    <!-- Ad container (can be empty, as interstitial ads cover the full screen) -->
    <div id="adspot-2000"></div>

    <script>
      var rdntag = rdntag || {};
      rdntag.cmd = rdntag.cmd || [];

      rdntag.cmd.push(function () {
        // Define the ad spot
        rdntag.defineAd(2000, 'adspot-2000');

        // Load the interstitial ad
        rdntag.loadInterstitialAd('adspot-2000');

        document
          .getElementById('adspot-2000')
          .addEventListener('slotResponseReceived', function (e) {
            if (e && e.detail && e.detail.adReturned) {
              rdntag.showInterstitialAd();
            }
          });
      });
    </script>
    <script src="https://s-cdn.rmp.rakuten.co.jp/js/aa.js" async></script>
  </body>
</html>
```
