# HWPlugin

Here will you see how to build an plugin for Hentai Web  
The plugin path is `/hentai-web/plugins/<PLUGINNAME>/`

## Start

Function should start like this
For this needs to be in `/hentai-web/plugins/<PLUGINNAME>/index.js`

```js
initFile((plugin) => {
  console.log("Hello, world!");
});
```

> The plugin name should always equal to the folder name!

If you want another file name, change the `run` in `plugin.yaml` to your owm

```diff
- run: index.js
+ run: bundle.js
```

## Plugin.yaml

Setup an config file in `/hentai-web/plugins/<PLUGINNAME>/plugin.yaml`. This is required to make the plugin run

```yaml
run: index.js
package:
  author: Der_Googler
  version: 2.3
  language: JavaScript
  description: |-
    # Fancy Event Plugin

    This plugin is for the [HW Project](https://github.com/DerGoogler/Hentai-Web)

    ### Notification

    Making some notifications with this plugin :D

    ### Open by typing <kbd>n</kbd> <kbd>o</kbd> <kbd>t</kbd> <kbd>i</kbd> on the keyboard   

    ![image](https://user-images.githubusercontent.com/54764558/151820875-c18c3478-8ed2-4fd8-8c2d-6f5b346b04b8.png)

    ### And enjoy the useless!

    ![image](https://user-images.githubusercontent.com/54764558/151821078-4ef76687-a53e-4d29-9c79-a812d81d777d.png)
options:
  allowEditor: true
```

> Note: The `run` is required, without will not work  
> Markdown should applied like in the sample, with spaces etc...

## Add to plugin list

You have to control about the plugin list

Don't remove the example plugin (The app will not work anymore)

```yaml
- example # Don't remove this plugin!
- plugin
```

## Translate your plugin

```js
initFile((plugin) => {
  const string = plugin.strings({
    de: {
      enableHCstring: "Aktivire Hohen Kontrast",
      displayDLbutton: "Download button anzeigen",
    },
    en: {
      enableHCstring: "Enable high contrast",
      displayDLbutton: "Display download button",
    },
  });
  // get string
  cosole.log(string.enableHCstring);
});
```

## Add settings

```js
initFile((plugin) => {
  plugin.addSettings([
    {
      title: "My Plugin",
      content: [
        {
          key: "enableStartupDialog",
          type: "switch",
          text: "Dialog on app start",
        },
      ],
    },
  ]);
});
```

## Functional Settings

To make an startup dialog, if the setting is turned on

```js
initFile((plugin) => {
  if (plugin.getPluginPref("enableStartupDialog") === "true") {
    alert("Welcome to the App");
  }
});
```

> Note: Useless if you give an Boolean or Number, it will always converted to an string

## Get plugin information

```js
initFile((plugin) => {
  console.log(plugin.getAuthor);
  console.log(plugin.getVersion);
  console.log(plugin.getLanguage);
});
```

## Platform

You can allow the plugin on different platforms

```js
initFile((plugin) => {
  if (native.isWindows /* native.isAndroid */) {
    plugin.addSettings([
      {
        title: "DLG",
        content: [
          {
            key: "DLG",
            type: "switch",
            text: "Dialog on app start",
          },
        ],
      },
    ]);
  } else {
    plugin.removeSettings();
  }
});
```

## Get plugin preferences

> Note: It returns always an string

```js
initFile((plugin) => {
  // get
  plugin.getPluginPref("enableFireworks");

  // set
  plugin.setPluginPref("enableFireworks", "true");

  // remove
  plugin.removePluginPref("enableFireworks");
});
```

## Others

Here are other functions that can be used

```js
initFile((plugin) => {
  // Will load from C:\hentai-web\plugins\<PLUGINNAME>\styles\index.css
  plugin.loadCSSfromFile("/styles/index.css");

  // Load CSS from an object. Lean more about JSS.
  plugin.loadCSS({
    "@global": {
      ".card": {
        border: "1px solid rgb(74 20 140)",
      },
      ".card-header": {
        borderBottom: "1px solid rgb(74 20 140)",
        backgroundColor: "rgba(74, 20, 140,.03)",
      },
      ".search-input--custom": {
        border: "1px solid rgb(74 20 140)",
      },
    },
  });

  // Will load from C:\hentai-web\plugins\<PLUGINNAME>\core\lib.css
  // Nore: This code will directly executed!
  plugin.require("/core/lib.js");
});
```
