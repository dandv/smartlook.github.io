---
title: "Unreal"
subtitle: "SDK for screen recording and analytics of Unreal Engine games."
---

## Description

The Smartlook Unreal SDK is currently available only for iOS devices.

If you are not using Unreal, check out our [Android](https://smartlook.github.io/docs/sdk/android/) and [iOS](https://smartlook.github.io/docs/sdk/ios/) builds for normal apps.

## What you can do

* Replay session recordings in our web player
* Capture all of the user interactions and find ones you can about in the Events manager
* Set your own custom analytics event and do complex funnels/queries in the dashboard
* Collect referrer value and source of installation per visitor

## Reporting issues

For more information on how to report issues please check our [Smartlook SDK Support section](https://smartlook.github.io/docs/sdk/support/#how-to-submit-an-issue).

## Installation for iOS

1. Download [Smartlook iOS Unreal SDK v1.2.4](https://sdk.smartlook.com/ios/smartlook-unreal-ios-sdk-1.2.4.zip).
2. Unzip the archive, create `Plugins` directory in your project's directory (if needed), and put `Smartlook` to `Plugins`.
3. Close and reopen your Unreal project to load the Smartlook plugin.
4. Open Plugins settings (Edit - Plugins), make sure Smartlook plugin is enabled. Smartlook plugin can be found in Installed section under Analytics.
5. Set analytics provider to `IOSSmartlook` (Edit - Project Settings - Analytics - Providers)
6. Obtain your SDK Key from [Smartlook Dashboard](https://www.smartlook.com/app/dashboard/settings/projects) and enter it into Smartlook Plugin settings (Edit - Project Settings - Analytics - Smartlook).
7. Enable recording by ticking the `Start Recording` switch in Smartlook Plugin settings, or by using Unreal analytics' `FAnalytics::Get().GetDefaultConfiguredProvider()->StartSession();`, or by using `Start Session` analytics blueprint node.
8. You can record events with `FAnalytics::Get().GetDefaultConfiguredProvider()->StartSession();`, or by using `Record Event` analytics blueprint node.

## Supported Analytics Methods

* Start Session
* End Session
* Record Event
* Record Event With Attribute
* Record Event With Attributes
* Set User ID
* Those Methods are recorded as events: Record Item Purchase, Record Currency Purchase, Record Currency Given, Record Error, Record Progress
