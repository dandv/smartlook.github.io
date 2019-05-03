---
title: "Custom events"
subtitle: "Create your own specific events for tracking."
description: "Use in case you have on your site our API code which can Identify visitor."
---

## What you can track

**Custom events** information (custom user actions) will be displayed directly in recordings. Create your own events and we will track them for you. Events allow you to track user interactions other than clicks, page views (URL) and text inputs.  With custom events you can get creative and track pretty much everything you want.

Code you need to insert in your site has a following format in **JavaScript**.

```js
<script>
  smartlook('track', eventName, properties);
</script>
```

## Interact with pop-up windows

You can configure an event that will fire when your user sees certain pop-up windows such as promotion alerts or upsell windows. Watch recordings to understand how your users are interacting with those pop-ups and get helpful insights to better engage your users.

```js
<script>
  // full example with your defined variables
  var eventName = 'UserOpenUpsellWindow';
  var properties = {
    "type": "SmallDiscLimit"
  };
  smartlook('track', eventName, properties);
</script>
```

## Custom Properties

In the example above, the parameter `properties` is a variable which can be used in case you need to send a specific information about your users to Smartlook. When `properties` is passed there no need to use any other parameters in your custom event.

In Smartlook, the `properties` variable can be used as a filter (further saved as a Segment) and as a dimension for events breakdown.

Have a look at this example where user reached app preset limit.

```js
<script>
  smartlook('track', 'UserLimitReached');
</script>
```
