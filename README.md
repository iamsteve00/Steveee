
-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local MinimizedFrame = Instance.new("Frame") -- Small movable square when minimized

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)

-- Close button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 1, -35)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Minimized Square
MinimizedFrame.Name = "MinimizedFrame"
MinimizedFrame.Parent = ScreenGui
MinimizedFrame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
MinimizedFrame.Size = UDim2.new(0, 50, 0, 50)
MinimizedFrame.Position = UDim2.new(0.5, -25, 0.5, -25)
MinimizedFrame.Visible = false

-- Function to minimize and restore the interface
local minimized = false

MinimizedFrame.MouseButton1Click:Connect(function()
    minimized = false
    MinimizedFrame.Visible = false
    Frame.Visible = true
end)

local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Frame
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 1, -35)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

MinimizeButton.MouseButton1Click:Connect(function()
    minimized = true
    Frame.Visible = false
    MinimizedFrame.Visible = true
end)

-- Making the minimized frame draggable
local UserInputService = game:GetService("UserInputService")
local dragging = false
local dragInput
local dragStart
local startPos

MinimizedFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = MinimizedFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

MinimizedFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        MinimizedFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

-- Creating tabs
local function createTabButton(name, text, position)
    local tabButton = Instance.new("TextButton")
    tabButton.Name = name
    tabButton.Parent = Frame
    tabButton.Text = text
    tabButton.Size = UDim2.new(0, 80, 0, 30)
    tabButton.Position = position
    return tabButton
end

local TrollTab = createTabButton("TrollTab", "Troll", UDim2.new(0, 10, 0, 10))
local PlayerTab = createTabButton("PlayerTab", "Player", UDim2.new(0, 100, 0, 10))
local OthersTab = createTabButton("OthersTab", "Others", UDim2.new(0, 190, 0, 10))

local function createTabFrame()
    local tabFrame = Instance.new("Frame")
    tabFrame.Parent = ScreenGui
    tabFrame.Size = UDim2.new(0, 300, 0, 250)
    tabFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
    tabFrame.Visible = false
    return tabFrame
end

local TrollFrame = createTabFrame()
local PlayerFrame = createTabFrame()
local OthersFrame = createTabFrame()

createTabButton("Back", "Back", UDim2.new(0, 10, 0, 10)).MouseButton1Click:Connect(function()
    TrollFrame.Visible = false
    PlayerFrame.Visible = false
    OthersFrame.Visible = false
    Frame.Visible = true
end)

-- Functions to open tabs
TrollTab.MouseButton1Click:Connect(function()
    TrollFrame.Visible = true
    PlayerFrame.Visible = false
    OthersFrame.Visible = false
    Frame.Visible = false
end)

PlayerTab.MouseButton1Click:Connect(function()
    TrollFrame.Visible = false
    PlayerFrame.Visible = true
    OthersFrame.Visible = false
    Frame.Visible = false
end)

OthersTab.MouseButton1Click:Connect(function()
    TrollFrame.Visible = false
    PlayerFrame.Visible = false
    OthersFrame.Visible = true
    Frame.Visible = false
end)

-- Troll functionalities (Void & View Player)
local PlayerNameBox = Instance.new("TextBox")
PlayerNameBox.Parent = TrollFrame
PlayerNameBox.PlaceholderText = "Enter Player Name"
PlayerNameBox.Size = UDim2.new(0, 150, 0, 30)
PlayerNameBox.Position = UDim2.new(0, 10, 0, 10)

local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollFrame
VoidButton.Text = "Void Player (ON/OFF)"
VoidButton.Size = UDim2.new(0, 150, 0, 30)
VoidButton.Position = UDim2.new(0, 10, 0, 50)

VoidButton.MouseButton1Click:Connect(function()
    -- Void logic
end)

local ViewButton = Instance.new("TextButton")
ViewButton.Parent = TrollFrame
ViewButton.Text = "View Player (ON/OFF)"
ViewButton.Size = UDim2.new(0, 150, 0, 30)
ViewButton.Position = UDim2.new(0, 10, 0, 90)

ViewButton.MouseButton1Click:Connect(function()
    -- View logic
end)
