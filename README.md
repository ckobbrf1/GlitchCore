# GlitchCore

A lightweight foundation addon for Garry's Mod that provides seamless inter-addon communication through a centralized Event System.

## Overview

GlitchCore eliminates the need for direct dependencies between addons. Instead of hardcoding connections, addons communicate via events — any addon can fire an event, and any other addon can subscribe to it.

**Example:**

Addon A fires "PlayerOpenedShop" → all subscribed addons receive the notification and respond accordingly.

## Features

- Centralized event bus for inter-addon communication
- Lightweight with minimal performance overhead
- Fully customizable via configuration files
- Well-documented API for third-party developers

## Installation

### Steam Workshop
Subscribe on [Steam Workshop](https://steamcommunity.com/workshop/filedetails/?id=3674746875)

### Manual
1. Download or clone this repository
2. Place the folder into `garrysmod/addons/`
3. Restart the server or change the map

## API Reference

### Subscribing to an Event

```lua
local gl = GlitchLab
if not gl then return end
local events = gl.Core.Events

local handle = events.On("EventName", function(data)
    print("Event received:", data)
end)

One-Time Subscription

local handle = events.Once("EventName", function(data)
    print("Event received:", data)
end)

Firing an Event

local gl = GlitchLab
if not gl then return end
local events = gl.Core.Events

hook.Add("PlayerSpawnedNPC", "UMS_PlayerSpawnedNPC", function(ply, npc)
    npc:SetNWFloat("Morale", UMaBS.Config.Morale.DefaultMorale) --Current morale value
    npc:SetNWFloat("TargetMorale", UMaBS.Config.Morale.DefaultMorale) --Current morale value
    npc:SetNWString("State", "Steady") --Current morale state (e.g., "Eager", "Steady", "Wavering", "Routed"). Check config for defined states and thresholds
    npc.MoraleModifiers = {}

    events.Fire("UMS_PlayerSpawnedNPC", ply, npc)
end)

Clearing Event Listeners

local gl = GlitchLab
if not gl then return end
local events = gl.Core.Events

-- Clear all listeners for a specific event
events.Clear("EventName")

-- Clear all listeners for all events
events.Clear()
```

Documentation

Official Addons Using GlitchCore

    Source Legions — Total War-inspired Morale System for NPCs

Contributing

Contributions are welcome. Please open an issue first to discuss proposed changes.
License

MIT License
Contact

Discord: v0idkr31
