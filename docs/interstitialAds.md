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

## Example

### Tag

```html
<div id="adspot-2000"></div>

<script>
  var rdntag = rdntag || {};
  rdntag.cmd = rdntag.cmd || [];

  rdntag.cmd.push(function () {
    // Define the ad spot
    rdntag.defineAd(2000, "adspot-2000");

    // Load the interstitial ad
    rdntag.loadInterstitialAd("adspot-2000").then(() => {
      // do something after loading interstitial ad

      rdntag.showInterstitialAd();
    });

    document
      .getElementById("adspot-2000")
      .addEventListener("slotResponseReceived", function (e) {
        if (e && e.detail && e.detail.adReturned) {
          // do something after rendering ad contents
        }
      });
  });
</script>
<script src="https://s-cdn.rmp.rakuten.co.jp/js/aa.js" async></script>
```

### Creative

```html
<html>
  <head>
    <style>
      body {
        background-color: rgba(0, 0, 0, 0.7);
        width: 100%;
        height: 100%;
      }
      #wrapper {
        width: 300px;
        height: 250px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
      }
      #close_wrapper {
        width: 100%;
        height: 32px;
        display: flex;
        justify-content: flex-end;
      }
      #close_btn {
        width: 32px;
        height: 32px;
        border: 2px solid #333;
        border-radius: 50%;
        background: none;
        font-size: 18px;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 4px 4px 0 0;
      }
      #content_wrapper {
        height: 218px;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    </style>
  </head>
  <body>
    <div id="wrapper">
      <div id="close_wrapper">
        <div id="close_btn">&times;</div>
      </div>
      <div id="content_wrapper">AD</div>
    </div>
    <script>
      document.getElementById("close_btn").addEventListener("click", (e) => {
        e.stopPropagation();
        // Close an intersitial ad by sending the message to JS SDK from a creative
        window.parent.postMessage({ vendor: "rdn", type: "close" }, "*");
      });
    </script>
  </body>
</html>
```
