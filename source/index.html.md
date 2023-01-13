---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - lua

toc_footers:

includes:

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Lua variant of the Roblox Game, Gmod.
---

# Introduction

Welcome to the official documentation on the "Lua variant" called GLua which is for my game called, Gmod on Roblox which is similar to Garry's Mod. GLua is made to act as a scripting source for addons created in my Roblox game.

# New built-in-functions

> a list of the few new built-in-functions

```lua
 local table = {1, 2, 3}
 
 foreach(table, function(i, v) -- loops through the table
  print(v)
 end)
 
```

```lua
 local ModuleService = GetModuleService() -- loads the ModuleService which can be used to act as module scripts
```

GLua has only a couple of built-in-functions such as `foreach`, `GetModuleService`, `LoadScriptsEnv`, `LoadCmdLineService`, and `LoadConsoleService`

# removed keywords, Services, and globals

## require
removed for obvious reasons which could be used to destroy the game

## getfenv
removed for obvious reasons which could be used to destroy the game

## setfenv
removed for obvious reasons which could be used to destroy the game

## ReplicatedStorage
removed because it should only be accessed by the core and mostly it is used by `require`

## ServerScriptStorage
removed to protect core scripts

## \_G
removed instead use the ModuleService to share info globally
also it is advised not to use \_G in Lua

## loadstring
removed for obvious reasons which could be used to destroy the game

# Functions, globals, and Services

## Hook

Hook is basically an easy way of doing events and it supports a few custom events
Hook is a global with only one function which is `Add`

```lua
local HookClass = Hook.Add("OnSpawn", function(player) -- when player is added to the game and returns a hook object class
     print(player.Name)
end)

print(HookClass.value, HookClass.eventtype) -- SUCCESSFUL, OnSpawn
```

## ModuleService

The ModuleService is a roundabout for module scripts because modulescripts arent supported in my game it currently has a few functions.
It can be used to communicate through different scripts it can be accessed by using the function `GetModuleService()`

### ModuleService:Add(modulename)
Returns false if the modulename is already taken

Parameter | Description
--------- | -----------
modulename | Creates a new module which can have functions added to it make sure the name is unique or else it wont be created

### ModuleService:Get(modulename)
Returns nil if the module was not found

Parameter | Description
--------- | -----------
modulename | Similar to requiring an actual module and it is used to get the module

### ModuleService:AddFunction(modulename, functionName, func)

Parameter | Description
--------- | -----------
modulename | The module in which the function will be put inside of
function | The name of the function which will go inside the module
FunctionName | The function that is put inside the module

```lua
local ModuleService = GetModuleService() -- Loads the ModuleService

ModuleService:Add("print_hi") -- Creates the module

ModuleService:AddFunction("print_hi", function() -- Adds the function
     print("hi")
end, "PrintHi")

local module = ModuleService:Get("print_hi")

module.PrintHi() -- outputs to hi
```

## LoadScriptEnv
It allows you to use the global `script` which is where the script is located although advise this instance doesn't inherit anything from script so you cant disable it.

## ConsoleService
The Service responsible for logging output in the console which can be accessed by pressing \ (back slash)

### ConsoleService:Add(text)

Parameter | Description
--------- | -----------
text | Adds white text to the console

### ConsoleService:Warn(text)

Parameter | Description
--------- | -----------
text | Adds a warning to the console which is orange

### ConsoleService:Error(text)

Parameter | Description
--------- | -----------
text | Adds an error to the console which is red that begins with "Error: "

### ConsoleService:Error2(text)

Parameter | Description
--------- | -----------
text | Adds an error to the console which is red that doesn't begin with "Error: " but instead begins with nothing and is only your text

### ConsoleService:ColorFromRGB(r, g, b)

Adds text to the console with the color depending on the rgb

### ConsoleService:ColorFromHex(hex)

Parameter | Description
--------- | -----------
hex | Adds text to the console with the corrosponding hex color code (string)

## CmdLineService (Client Only)
The CmdLineService is a RemoteEvent responsible for the command line in the console.

### CmdLineService:FireServer()
Fires the CmdLineService RemoteEvent.

Parameter | Description
--------- | -----------
message | "{Command} {Parameter1} {Parameter2} ect." acts like an admin script

Current Commands are:
  - kill {parameter : user} - kills the selected user(s)
  - warn {parameter : string} - makes a warning in the console
  - error {parameter : string} - makes an error in the console
  - time {parameter : number} - changes the time of day in lighting
  - clearaddons - clears all spawned addons
  - clearprops - clears all spawned props
  - clearnpcs - clears all spawned npcs
  - clearentities - clears all spawned entities
  - clear - clears addons, props, npcs, and entities
  - adminize {parameter : user} - gives a user admin (host only)
