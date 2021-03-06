---
layout: gettingStarted
title:  "Device test"
link: "devicetest"
tags: 
 - name: Prerequisites
   link: deviceTestPreresuisites
 - name: Apply appium's desiredCapabilities
   link: appiumDesiredcapabilities
 - name: Manage appium's life cycle
   link: manageAppiumLifecycle
 - name: Test in local environment
   link: testInLocalEnvironment
 - name: Test in remote environment
   link: testInRemoteEnvironment
category: Getting Started
---


{:name="link-content"}
## Device Test
---

{:.description}
_Testarmada_ supports mobile browser test as well as native app test via _[appium](http://appium.io/)_. By using the _[nightwatch-extra](https://github.com/TestArmada/nightwatch-extra)_ addon, _Testarmada_ can even manage the life cycle of appium and simulator for you.


{:id="deviceTestPreresuisites"}
{:name="link-content"}
### Prerequisites

{:.description}
Appium is required for device test. You must include it in your project's `package.json`.

<code data-gist-id="ffe008d062530ea8e444496a03f08c37" data-gist-line="1,20,21,38-39"></code>

{:id="appiumDesiredcapabilities"}
{:name="link-content"}
### Apply appium's desiredCapabilities

{:.description}
For device test, appium requires a different set of desiredCapabilities from what is needed by desktop browser test, for example _deviceName_ or _avd_ for android are desiredCapabilities for device test only. _Testarmada_ allows to add these desiredCapabilities directly in your configurations. The following example shows how to add those appium specific desiredCapabilities in your configuration.

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32,92,94,96-102,110,177-178"></code>

{:id="manageAppiumLifecycle"}
{:name="link-content"}
### Manage appium's life cycle

{:.description}
_Testarmada_ can manage appium's life cycle automatically for you during your test run. To use this feature you need to 

{:.list}
{:.description}
1). Disable selenium server and enable appium in your test entry of `nightwatch.json`, such as.

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32,92,103-110,177-178"></code>

{:.list}
{:.description}
2) .Copy [global.js](https://github.com/TestArmada/boilerplate-nightwatch/blob/master/lib/globals.js) and put it somewhere in your repo.

{:.list}
{:.description}
3). Put path of `global.js` in your `nightwatch.json`.

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,19,178"></code>

{:.description}
You can also choose to launch appium manually and plug your _Testarmada_'s test with it. To do so, appium port and host need to be specified as selenium_port and selenium_host in `nightwatch.json`.

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32-33,35-36,51,177-178"></code>

{:.description}
Then in your test entry in `nightwatch.json`, diable both selenium and appium:

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32,92,156-159,177-178"></code>

{:.description}
> _Pleaes note_:

{:.description}
> By default if not being explicitly specified, appium server will be disabled.

{:id="testInLocalEnvironment"}
{:name="link-content"}
### Test in local environment

{:.description}
_Testarmada_ can manage the life cycle of your local test environment (iOS simulator or Android emulator) automatically for you as well. To fully utilize this feature, your local test environment should be properly configured. Please refer to [here](https://github.com/TestArmada/nightwatch-extra/blob/master/docs/android.md#pre-requisites) for environment setup for android, and [here](https://github.com/TestArmada/nightwatch-extra/blob/master/docs/ios.md#pre-requisites) for your iOS environment.

{:.description}
For Android emulator, the _platformName_, _platformVersion_ and _deviceName_ in your appium desireCapabilities should match what your local environment has. For example

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32,111,113,115-119,127,177-178"></code>

{:.description}
For iOS simulator, the values of following keys should reflect what your local environment has.

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32,92,94,98-100,102,110,177-178"></code>

{:.description}
If you want to run test against a native application, please add key app into your appium desiredCapabilities. This desiredCapabilities tells appium to install and use Walmart.apk in the ./app folder for test.

<code data-gist-id="557c10f8cf51e41c3f73293e98ee9044" data-gist-line="1,32,111,113-114,119,127,177-178"></code>

{:id="testInRemoteEnvironment"}
{:name="link-content"}
### Test in remote environment

{:.description}
Similar to what is described in [Remote browser test](#enableAnExecutor) section, _Testarmada_ uses executor to drive device test remotely. Currently you can choose from _Testarmada_'s _[magellan-saucelabs-executor](https://github.com/TestArmada/magellan-saucelabs-executor)_ or _[magellan-browserstack-executor](https://github.com/TestArmada/magellan-browserstack-executor)_ for testing in simulator/emulator and _[magellan-testobject-executor](https://github.com/TestArmada/magellan-testobject-executor)_ for real device test. Please refer to the README.md in each executor for configuration detail.