---
title: 'Quickly Open Localhost from Anywhere using Hammerspoon'
date: 2024-10-08T17:07:37+10:00
draft: false
tags: 
    - hammerspoon
category: productivity
---

# Quickly Open Localhost from Anywhere using Hammerspoon

I love to reduce friction in my workflows.

I find it incredibly useful and pleasant.

You might not save hours in your day, but you increase your skills and get a hit of satisfaction every time you use [INSERT THE TOOL YOU BUILT HERE].

It also greatly help you staying in the flow.

As a developer, you have access to some incredible tools that you can leverage improve your workflows.

[Hammerspoon](https://www.hammerspoon.org/) is one of them.

Hammerspoon, or HS, is a scripting framework to interact with macOS.

In this example, I use it to create a script that prompt me for a port number, and then automatically open a browser at `http://localhost:[MY_PORT]`.

Simple, but very effective!

I bind it to HYPER + A, which means I can quickly open a browser at localhost from anywhere.

```lua
local hyper = { "ctrl", "alt", "cmd", "shift" }

-- Function to open browser and navigate to locahost:my_port
function openBrowserAtLocalHost()
	local appName = "Zen Browser"
	local base = "http://localhost:"
	local browser = hs.application.find(appName)
	-- By default, use 9943/admin (work)
	local _, port = hs.dialog.textPrompt("Enter port", "Please enter the localhost port to open:", "9443/admin")

	if browser then
		hs.application.launchOrFocus(appName)
		-- browser is running, open the URL in the existing instance
		hs.urlevent.openURLWithBundle(base .. port, browser:bundleID())
	else
		-- browser is not running, launch it first, then open the URL
		-- Small delay to ensure browser opens before navigating to the URL
		hs.timer.doAfter(1, function()
			hs.urlevent.openURL(base .. port)
		end)
	end
end
```

Enjoy,
Aloys.

