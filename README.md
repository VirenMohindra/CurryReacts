# [CurryReact](https://chrome.google.com/webstore/detail/curryreacts-for-facebook/doomjeblpidgihaceihmjcnapmhokjbo)
Google Chrome Extension which swaps out Facebook's emoji reactions and displays Steph Curry's face

## Preface
After watching Stephen Curry's insane [performance](https://youtu.be/YkaqIujpcbw) against OKC on 02/27/16, I knew I had to make something ~for~ him.

In the same weekend, Facebook released its emoji's. After inspecting the code a little, with a little bit of help from [Francois Grante](https://francoisgrante.com/)

I've never made an extension before and I thought this would be a great opportunity to hone in those skills.

## Screenshot
![CurryReacts Extension Screenshot](https://raw.githubusercontent.com/VirenMohindra/CurryReacts/master/screenshot.png)

## Interesting problems and solutions

I really wanted to display a static html site as soon as someone installed the extension. It would also make my job easier in knowing how many people opened up the extension to view it, and how many people __actually__ downloaded it.

I could use this data to know the conversion rate, and how many of my friends actually downloaded the extension.

JavaScript code which needs to be added to `popup.js`. Found at [StackOverflow](http://stackoverflow.com/a/24429523/5673665)

```javascript
chrome.runtime.onInstalled.addListener(function (object) {
	chrome.tabs.create({
	url: "popup.html"
	}, 
		function (tab) {
			console.log("New tab launched with popup.html");
	});
});
```
Code which needs to be added to the `manifest.json` for it to 'popup'. Same source ^

```json
	"background": {
		"scripts": [ "js/popup.js" ],
		"persistent": false
		},
	"options_page": "popup.html",
```

## Google Analytics (for your extension)

If you want to track your users in your extension you'll need a modified analytics tracking code which I got from the [Chrome Developer documentation](https://developer.chrome.com/extensions/tut_analytics). Add this to your `javascript` files.

```javascript
(function() {
  var ga = document.createElement('script');
  ga.type = 'text/javascript';
  ga.async = true;
  ga.src = 'https://ssl.google-analytics.com/ga.js';
  var s = document.getElementsByTagName('script')[0];
  s.parentNode.insertBefore(ga, s);
})();

This should be added to your `manifest.json` too! Source: [StackOverflow](http://stackoverflow.com/a/12986150/5673665)

```json
"content_security_policy": "script-src 'self' https://ssl.google-analytics.com; object-src 'self'"
```

## Make Your Own Emoji's

1. You'll need to swap out all the images in the provided psd's and output it as a png
2. Done!
3. Actually, the Google analytics will also needed to be swapped out - currently XXXXXXX in `js/popup.js`