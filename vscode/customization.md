# VSCode settings overview

VScode allows to customize most settings. Inspection tools for all available settings
are built in, so it's easy to search for a specific setting.

## Title bar color settings for workspace

For example you can color a workspace's title bar by adding the following to `settings` of 
the `workspacename.code-workspace` file you use to save a workspace:


You can use [colorbrewer](https://colorbrewer2.org) to find colors, but
a code palette is also built in once you create the setting.

```
{
	"folders": [
		{
			"path": "/rel/path/from/config/to/folder"
		},
	],
	"settings": {
		"workbench.colorCustomizations": {
			"titleBar.activeBackground": "#f46d43"
		}
	}
}
```
