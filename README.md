[![npm version](https://badge.fury.io/js/capacitor-android-shortcuts.svg)](https://badge.fury.io/js/capacitor-android-shortcuts)
[![capacitor support](https://img.shields.io/badge/capacitor%20support-v3-brightgreen?logo=capacitor)](https://capacitorjs.com/)

# capacitor-android-shortcuts

This plugin provides the feature to add dynamic and pinned shortcuts in Android apps. See more [in the Android docs](https://developer.android.com/guide/topics/ui/shortcuts). Its possible to listen to a shortcut tap action with an event listener (see `Usage`).

**Dynamic shortcut**<br/>
Tap and hold on the app icon and you will see the dynamic shortcuts in the dropdown<br/>
=> Usage: Call the `addDynamic` method one time to add the array of dynamic shortcuts

**Pinned shortcut**<br/>
You can add a pinned shortcut programmatically inside your app, i.e. let a customer add a favorite of an article/product/... to the home screen<br/>
=> Usage: Call the `addPinned` method where the user wants to pin something. An alert will be shown to add the pinned shortcut to the home screen.

## Supported platforms

| Platform | Supported |
| -------- | --------: |
| Android  |         ✔ |
| iOS      |         ✖ |
| Web      |         ✖ |

## Install

```bash
npm install capacitor-android-shortcuts
npx cap sync android
```

## Usage

```javascript
import { AndroidShortcuts } from 'capacitor-android-shortcuts';

...

// Add dynamic shortcuts
AndroidShortcuts.isDynamicSupported().then(({ result }) => {
    if (result) {
        AndroidShortcuts.addDynamic({
            items: [
                {
                    id: "myfirstid",
                    shortLabel: "My first short label",
                    longLabel: "My first long label",
                    icon: {
                        type: "Bitmap",
                        name: "<base64-string>"
                    },
                    data: "I am a simple string",
                },
                {
                    id: "mysecondid",
                    shortLabel: "My first short label",
                    longLabel: "My first long label",
                    icon: {
                        type: "Resource",
                        name: "<vector-asset-name>"
                    },
                    data: JSON.stringify({
                        myProperty: "Pass a stringified JSON object",
                    }),
                },
            ],
        });
    }
});
...

// Add pinned shortcuts
AndroidShortcuts.isPinnedSupported().then(({ result }) => {
    if (result) {
        AndroidShortcuts.addPinned({
            id: "mypinnedid",
            shortLabel: "My pinned short label",
            longLabel: "My pinned long label",
            icon: {
                type: "Bitmap",
                name: "<base64-string>"
            },
            data: "I am a simple string",
        });
    }
});

// Triggered when app is launched by a shortcut
AndroidShortcuts.addListener('shortcut', (response: any) => {
  // response.data contains the content of the 'data' property of the created shortcut
});
```

See also [Wiki: Icon examples](https://github.com/NePheus/capacitor-android-shortcuts/wiki/Icon-examples)

## API

<docgen-index>

<docgen-api>
<!--Update the source file JSDoc comments and rerun docgen to update the docs below-->

### isDynamicSupported()

```typescript
isDynamicSupported() => any
```

Checks if dynamic shortcuts are supported on the device

**Returns:** <code>any</code>

--------------------


### isPinnedSupported()

```typescript
isPinnedSupported() => any
```

Checks if pinned shortcuts are supported on the device

**Returns:** <code>any</code>

--------------------


### addDynamic(...)

```typescript
addDynamic(options: { items: ShortcutItem[]; }) => any
```

Created dynamic shortcuts

| Param         | Type                        | Description                                      |
| ------------- | --------------------------- | ------------------------------------------------ |
| **`options`** | <code>{ items: {}; }</code> | An items array with the options of each shortcut |

**Returns:** <code>any</code>

--------------------


### addPinned(...)

```typescript
addPinned(options: ShortcutItem) => any
```

Created a pinned shortcut

| Param         | Type                                                                                                                                  | Description                              |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| **`options`** | <code>{ id: string; shortLabel: string; longLabel: string; icon?: { type: AvailableIconTypes; name: string; }; data: string; }</code> | An option object for the pinned shortcut |

**Returns:** <code>any</code>

--------------------


### addListener(...)

```typescript
addListener(eventName: 'shortcut', listenerFunc: MessageListener) => Promise<PluginListenerHandle> & PluginListenerHandle
```

Add a listener to a shortcut tap event

| Param              | Type                                                  |
| ------------------ | ----------------------------------------------------- |
| **`eventName`**    | <code>"shortcut"</code>                               |
| **`listenerFunc`** | <code>(response: { data: string; }) =&gt; void</code> |

**Returns:** <code>any</code>

--------------------


### Interfaces


#### PluginListenerHandle

| Prop         | Type                      |
| ------------ | ------------------------- |
| **`remove`** | <code>() =&gt; any</code> |

</docgen-api>
