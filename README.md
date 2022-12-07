# Linoria Library
This is the written documentation for the Linoria Library


## Booting the Library
```lua
local repo = 'https://raw.githubusercontent.com/wally-rblx/LinoriaLib/main/'

local Library = loadstring(game:HttpGet(repo .. 'Library.lua'))()
local ThemeManager = loadstring(game:HttpGet(repo .. 'addons/ThemeManager.lua'))()
local SaveManager = loadstring(game:HttpGet(repo .. 'addons/SaveManager.lua'))()
```


## Creating a Window
```lua
local Window = Library:CreateWindow({
    Title = 'Window',
    Center = true, 
    AutoShow = true,
})
```

## Creating a Tab
```lua
local Tabs = {
    tab = Window:AddTab('Tab'),
    ['UI Settings'] = Window:AddTab('UI Settings'),
}
```

## Creating a Group
```lua
local mainGroup = Tabs.AutoFarm:AddLeftGroupbox('Main')
```

## GroupBox Positions
```lua
AddLeftGroupbox('') -- left
AddRightGroupbox('') -- right


## Notifying the user
```lua
Library:Notify("Notification")
```

## Creating a Button
```lua
MenuGroup:AddButton('Unload', function() Library:Unload() end)
```

## Creating a Toggle
```lua
local Toggle = Tab:CreateToggle({
	Name = "Toggle Example",
	CurrentValue = false,
	Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		-- The function that takes place when the toggle is pressed
    		-- The variable (Value) is a boolean on whether the toggle is true or false
	end,
})
```
### Updating a Toggle
```lua
Toggle:Set(false)
```

## Creating a Color Picker
Coming Soon


## Creating a Slider
```lua
local Slider = Tab:CreateSlider({
	Name = "Slider Example",
	Range = {0, 100},
	Increment = 10,
	Suffix = "Bananas",
	CurrentValue = 10,
	Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		-- The function that takes place when the slider changes
    		-- The variable (Value) is a number which correlates to the value the slider is currently at
	end,
})
```
### Updating a Slider
```lua
Slider:Set(10) -- The new slider integer value
```

## Creating a Label
```lua
local Label = Tab:CreateLabel("Label Example")
```
### Updating a Label
```lua
Label:Set("Label Example")
```

## Creating a Paragraph
```lua
local Paragraph = Tab:CreateParagraph({Title = "Paragraph Example", Content = "Paragraph Example"})
```
### Updating a Paragraph
```lua
Paragraph:Set({Title = "Paragraph Example", Content = "Paragraph Example"})
```

## Creating an Adaptive Input (TextBox)
```lua
local Input = Tab:CreateInput({
	Name = "Input Example",
	PlaceholderText = "Input Placeholder",
	RemoveTextAfterFocusLost = false,
	Callback = function(Text)
		-- The function that takes place when the input is changed
    		-- The variable (Text) is a string for the value in the text box
	end,
})
```



## Creating a Keybind
```lua
local Keybind = Tab:CreateKeybind({
	Name = "Keybind Example",
	CurrentKeybind = "Q",
	HoldToInteract = false,
	Flag = "Keybind1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Keybind)
		-- The function that takes place when the keybind is pressed
    		-- The variable (Keybind) is a boolean for whether the keybind is being held or not (HoldToInteract needs to be true)
	end,
})
```
### Updating a Keybind
```lua
Keybind:Set("RightCtrl") -- Keybind (string)
```

## Creating a Dropdown menu
```lua
local Dropdown = Tab:CreateDropdown({
	Name = "Dropdown Example",
	Options = {"Option 1","Option 2"},
	CurrentOption = "Option 1",
	Flag = "Dropdown1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Option)
	  	  -- The function that takes place when the selected option is changed
    	  -- The variable (Option) is a string for the value that the dropdown was changed to
	end,
})
```

## Destroying the Interface
```lua
Library:Unload()
```
