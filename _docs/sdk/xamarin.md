---
title: “Xamarin”
subtitle: "SDK for screen recording and analytics for Xamarin Android/iOS multi-platform apps.”
description: "This SDK offers several options to developers and/or companies."
---

## What you can do

* Replay session recordings in our web player
* Capture all of the user interactions and find ones you can about in the Events manager
* Set your own custom analytics event and do complex funnels/queries in the dashboard

## Reporting issues

For more information on how to report issues please check our [Smartlook SDK Support section](https://smartlook.github.io/docs/sdk/support/#how-to-submit-an-issue).

## WiFi / mobile connection / offline

Currently we are uploading sessions **only on WiFi** connection. If application is on mobile connection or offline we are storing sessions locally and will upload them as soon as application has WiFi connection.
*Note: we are working on a change so you could enable mobile uploads on per project basis in the dashboard in near future.*

## Installation

TBD

Install from the standard NuGet repository nuget.org.

You need to provide your **SDK Key** which can be found in [Smartlook Dashboard](https://www.smartlook.com/app/dashboard/settings/projects){:target="_blank"}.
{: .alert .alert-warning }


## API Reference

Applications can interact with the SDK using public SDK methods. To get access to Smartlook API, declare

```cs
using Smartlook;
```

in your C# files.

### Run Smartlook

You need to provide your **SDK Key** which can be found in [Smartlook Dashboard](https://www.smartlook.com/app/dashboard/settings/projects){:target="_blank"}.
{: .alert .alert-warning }

To access Smartlook API, use static methods exposed by `Smartlook.Analytics` class. The methods are the same for multi-platform, Android or iOS projects.

The most straightforward way to run Smartlook is by calling the following method at the very begin of the app life-cycle (e.g., iOS: `AppDelegates`’s `FinishedLaunching`, Android: `Application` class `OnCreate`):

```cs
Smartlook.Analytics.SetupAndStart("your-app-sdk-key");
```

That is all. This initialises Smartlook and starts recording events and screen recording.

Even if you do not want starting the recording right away, setup the Smartlook as soon as possible in your app life-cycle by calling:

```cs
Smartlook.Analytics.Setup("your-app-sdk-key");
```

You can then start and stop the recording and checking its recording status any time by 

```cs
Smartlook.Analytics.StartRecording();
Smartlook.Analytics.StopRecording();
bool isRecording = Smartlook.Analytics.IsRecording;
```

It is not necessary to stop recording when the app is suspended, or start when it wakes from its suspended state, this happens automatically.

### Fine-tune Smartlook

Setup methods have an optional parameter with `SetupOptions` type to set running options. At present, it can be used to set the preferred video recording framerate in frames-per-seconds
```cs
Smartlook.Analytics.Setup("your-app-sdk-key", new Analytics.SetupOptions(framerate: 4));

Smartlook.Analytics.SetupAndStart("your-app-sdk-key", new Analytics.SetupOptions(framerate: 4));
```
#### Framerate Option

From our experience, the default 1~2fps framerate is quite sufficient for capturing user behaviour for analytics purposes. Increase the framerate if you need *smoother* recordings. Plese note that custom framerate must not be lesser than 2fps.

Higher framerate do not necessarily lead to bigger video data, but more frequent screen capture increases the device CPU/GPU load and energy consumption. Compromise strategy could be e.g., enabling higher framerate during beta-testing, and decrease it to the default value in production builds.

### Add User ID

You can specify your app's user identifier together with optional setting of other custom parameters by 
```cs
static void SetUserIdentifier(string identifier, Dictionary<string, string> userProperies = null);
```

### Session properties [iOS only]

Additional custom properties can be added or removed to each recording session by these methods:

```cs
static void SetSessionProperty(string name, string value, PropertyOptions options = PropertyOptions.Defaults);

static void RemoveSessionProperty(string name);

static void ClearSessionProperties();
```

If you do want _locking_ a session property value to protect it against accidental further changes, set its options to `Immutable`. Immutable property value cannot be changed once it is set (it can be removed and set again, though).

### Working with sensitive data

#### Blacklisted views

In order to protect potentially sensitive or personal data of your users, SDK contains list of blacklisted views. These views won't be recorded (there will be only black rectangle instead of the view in the recording). 

To add/remove an instance of View/UIView to the blacklist, use these methods
```cs
static void RegisterBlacklistedObject(object @object);
static void UnregisterBlacklistedObject(object @object);
```

#### Whitelisted views
Views of some classes are included in the blacklist by default (Android: `EditText` and `WebView`, iOS: `UITextView`, `UITextField`, `UIWebView` and `WKWebView`).
To whitelist an instance of blacklisted class View/UIView, use
```cs
static void RegisterWhitelistedObject(object @object);
```
and to return a view back to its default blacklisted state
```cs
static void UnregisterWhitelistedObject(object @object);
```

#### Sensitive mode

In the case you don't want SDK to record video at all, but still want to get analytics events, use fullscreen sensitive mode:

```cs
static void BeginFullscreenSensitiveMode();

static void EndFullscreenSensitiveMode();

static bool IsFullscreenSensitiveModeActive;
```

### Analytics

SDK records several analytics events by default:

- Navigation events (controller transitions)
- Focus events
- Orientation events
- Tap events

You can also add your own custom events.

#### Custom events

Custom events are identified by a name, and can also have optional additional properties. These properties can be used in **funnels** and by any other **filtering**.

```cs
static void TrackCustomEvent(string name, Dictionary<string, string> eventProperties = null);
```

#### Timed event

In the case you want to measure the duration of any time-sensitive or long-running actions in the app, you can first call

```cs
static void StartTimedCustomEvent(string name, Dictionary<string, string> eventProperties = null);
```

This will not send out any event, but once the `TrackCustomEvent(...)` with the corresponding event gets called it will have extra **duration** property with the time interval between the `Start...` and `Track...` calls.

Properties set in the `StartTimedCustomEvent` will be merged with properties set in `TrackCustomEvent`. Properties from the  `TrackCustomEvent` will have higher priority and will override conflicting properties from `StartTimedCustomEvent` call.

#### Global event properties

Global event properties are sent with every event. To manage global event properties, use the following set of methods:

```cs
static void SetGlobalEventProperty(string name, string value, PropertyOptions options = PropertyOptions.Defaults);

static void RemoveGlobalEventProperty(string name);

static void ClearGlobalEventProperties();
```

Global event properties can be set `Immutable` the same way session properties. Immutable property value cannot be changes once it is set (it can be removes and set again, though).

### Shareable session URL

You can obtain URL leading to the Dashboard player for the current Smartlook session by reading this property:

```cs
static Uri Smartlook.Analytics.dashboardSessionURL;
```

This URL can be access by everyone with the access rights to the dashboard.


