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
local mainGroup = Tabs.tab:AddLeftGroupbox('Main')
```

## GroupBox Positions
```lua
:AddLeftGroupbox('') -- left
:AddRightGroupbox('') -- right
```

## Notifying the user
```lua
Library:Notify("Notification")
```

## Creating a Button
```lua
mainGroup:AddButton('Unload', function() end)
```

## Creating a Toggle
```lua
mainGroup:AddToggle('Toggle1', {
    Text = 'Toggle',
    Default = false,
    Tooltip = 'hover text',
})
```
### Toggle Function
```lua
Toggles.Toggle1:OnChanged(function()
    print('Toggle changed to:', Toggles.MyToggle.Value)
end)
```

## Creating a Color Picker
```lua
mainGroup:AddLabel('Color'):AddColorPicker('ColorPicker', {
    Default = Color3.new(0, 1, 0),
    Title = 'Some color',
})

Options.ColorPicker:OnChanged(function()
    print('Color changed!', Options.ColorPicker.Value)
end)

Options.ColorPicker:SetValueRGB(Color3.fromRGB(0, 255, 140))
```


## Creating a Slider
```lua
mainGroup:AddSlider('MySlider', {
    Text = 'Slider!',
    Default = 0,
    Min = 0,
    Max = 5,
    Rounding = 1,

    Compact = false, -- If set to true, then it will hide the label
})
```
### Slider Function
```lua
Options.MySlider:OnChanged(function()
    print('MySlider was changed! New value:', Options.MySlider.Value)
end)
```

## Creating a Label
```lua
mainGroup:AddLabel('This is a label')
```

## Creating a Divider
```lua
mainGroup:AddDivider()
```

## Creating an Adaptive Input (TextBox)
```lua
mainGroup:AddInput('MyTextbox', {
    Default = 'My textbox!',
    Numeric = false, -- true / false, only allows numbers
    Finished = false, -- true / false, only calls callback when you press enter

    Text = 'Textbox',
    Tooltip = 'Hover text', -- Information shown when you hover over the textbox

    Placeholder = 'Placeholder text', -- placeholder text when the box is empty
    -- MaxLength is also an option which is the max length of the text
})
```

## Input Function
```lua
Options.MyTextbox:OnChanged(function()
    print('Text updated. New text:', Options.MyTextbox.Value)
end)
```

## Creating a Keybind
```lua
mainGroup:AddLabel('Keybind'):AddKeyPicker('KeyPicker', {
    -- SyncToggleState only works with toggles. 
    -- It allows you to make a keybind which has its state synced with its parent toggle

    -- Example: Keybind which you use to toggle flyhack, etc.
    -- Changing the toggle disables the keybind state and toggling the keybind switches the toggle state

    Default = 'MB2', -- String as the name of the keybind (MB1, MB2 for mouse buttons)  
    SyncToggleState = false, 


    -- You can define custom Modes but I have never had a use for it.
    Mode = 'Toggle', -- Modes: Always, Toggle, Hold

    Text = 'Auto lockpick safes', -- Text to display in the keybind menu
    NoUI = false, -- Set to true if you want to hide from the Keybind menu,
})

-- OnClick is only fired when you press the keybind and the mode is Toggle
-- Otherwise, you will have to use Keybind:GetState()
Options.KeyPicker:OnClick(function()
    print('Keybind clicked!', Options.KeyPicker.Value)
end)

task.spawn(function()
    while true do
        wait(1)

        -- example for checking if a keybind is being pressed
        local state = Options.KeyPicker:GetState()
        if state then
            print('KeyPicker is being held down')
        end

        if Library.Unloaded then break end
    end
end)

Options.KeyPicker:SetValue({ 'MB2', 'Toggle' }) -- Sets keybind to MB2, mode to Hold
```
-- i have no idea how to use keybinds or anything obt them lol, i just copied this from the original thing

## Creating a Dropdown menu
```lua
mainGroup:AddDropdown('MyDropdown', {
    Values = { 'This', 'is', 'a', 'dropdown' },
    Default = 1, -- number index of the value / string

    Text = 'A dropdown',
    Tooltip = 'Hover text', -- Information shown when you hover over the textbox
})

```

## Dropdown menu Fucntion
```lua
Options.MyDropdown:OnChanged(function()
    print('Dropdown got changed. New value:', Options.MyDropdown.Value)
end)

Options.MyDropdown:SetValue('This')
```

## Creating a Multi Dropdown menu
```lua
mainGroup:AddDropdown('MyMultiDropdown', {
    -- Default is the numeric index (e.g. "This" would be 1 since it if first in the values list)
    -- Default also accepts a string as well

    -- Currently you can not set multiple values with a dropdown

    Values = { 'This', 'is', 'a', 'dropdown' },
    Default = 1, 
    Multi = true, -- true / false, allows multiple choices to be selected

    Text = 'A dropdown',
    Tooltip = 'Hover Text', -- Information shown when you hover over the textbox
})
```

## Multi Dropdown menu Fucntion
```lua
Options.MyMultiDropdown:OnChanged(function()
    print('Multi dropdown got changed:')
    for key, value in next, Options.MyMultiDropdown.Value do
        print(key, value) -- should print something like This, true
    end
end)

Options.MyMultiDropdown:SetValue({
    This = true,
    is = true,
})
```

## Destroying the Interface
```lua
Library:Unload()
```

## Put this at the end cuz it will break if u dont, i think
```lua
Library.KeybindFrame.Visible = true;

Library:OnUnload(function()
    print('Unloaded!')
    Library.Unloaded = true
end)


local MenuGroup = Tabs['UI Settings']:AddLeftGroupbox('Menu')

MenuGroup:AddToggle("Keybinds", { Text = "Show Keybinds Menu", Default = false }):OnChanged(function()
    Library.KeybindFrame.Visible = Toggles.Keybinds.Value
end)
MenuGroup:AddToggle("Watermark", { Text = "Show Watermark", Default = false }):OnChanged(function()
    Library:SetWatermarkVisibility(Toggles.Watermark.Value)
end)
MenuGroup:AddButton('Unload', function() Library:Unload() end)
MenuGroup:AddLabel('Menu bind'):AddKeyPicker('MenuKeybind', { Default = 'RShift', NoUI = true, Text = 'Menu keybind' }) 

Library.ToggleKeybind = Options.MenuKeybind

ThemeManager:SetLibrary(Library)
SaveManager:SetLibrary(Library)
SaveManager:IgnoreThemeSettings() 
SaveManager:SetIgnoreIndexes({ 'MenuKeybind' }) 
ThemeManager:SetFolder('MyScriptHub')
SaveManager:SetFolder('MyScriptHub/specific-game')
SaveManager:BuildConfigSection(Tabs['UI Settings']) 
ThemeManager:ApplyToTab(Tabs['UI Settings'])
```
