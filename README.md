
-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local MinimizedFrame = Instance.new("Frame") -- Small movable square when minimized
local FlyGui = Instance.new("ScreenGui") -- Dedicated Fly GUI

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)

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

local function createBackButton(tabFrame)
    local BackButton = Instance.new("TextButton")
    BackButton.Parent = tabFrame
    BackButton.Text = "Back"
    BackButton.Size = UDim2.new(0, 80, 0, 30)
    BackButton.Position = UDim2.new(0, 10, 0, 10)
    BackButton.BackgroundColor3 = Color3.fromRGB(150, 150, 150)

    BackButton.MouseButton1Click:Connect(function()
        tabFrame.Visible = false
        Frame.Visible = true
    end)
end

createBackButton(TrollFrame)
createBackButton(PlayerFrame)
createBackButton(OthersFrame)

-- Void Player functionality with ON/OFF button
local voidActive = false
local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollFrame
VoidButton.Text = "Void Player (ON/OFF)"
VoidButton.Size = UDim2.new(0, 150, 0, 30)
VoidButton.Position = UDim2.new(0, 10, 0, 50)

VoidButton.MouseButton1Click:Connect(function()
    voidActive = not voidActive
    VoidButton.Text = voidActive and "Void Player (ON)" or "Void Player (OFF)"
end)

-- View Player functionality with ON/OFF button
local viewing = false
local ViewButton = Instance.new("TextButton")
ViewButton.Parent = TrollFrame
ViewButton.Text = "View Player (ON/OFF)"
ViewButton.Size = UDim2.new(0, 150, 0, 30)
ViewButton.Position = UDim2.new(0, 10, 0, 90)

ViewButton.MouseButton1Click:Connect(function()
    viewing = not viewing
    ViewButton.Text = viewing and "View Player (ON)" or "View Player (OFF)"

    if viewing then
        local targetPlayer = game.Players:FindFirstChild("TargetName") -- Replace with target selection
        if targetPlayer and targetPlayer.Character then
            game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character:FindFirstChild("Humanoid")
        end
    else
        game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
    end
end)

-- Fly GUI Setup
FlyGui.Parent = game.CoreGui
local FlyFrame = Instance.new("Frame")
local EnableFlyButton = Instance.new("TextButton")
local DisableFlyButton = Instance.new("TextButton")
local SpeedBox = Instance.new("TextBox")

FlyFrame.Parent = FlyGui
FlyFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
FlyFrame.Size = UDim2.new(0, 200, 0, 150)
FlyFrame.Position = UDim2.new(0.8, 0, 0.2, 0)

EnableFlyButton.Parent = FlyFrame
EnableFlyButton.Text = "Enable Fly"
EnableFlyButton.Size = UDim2.new(0, 180, 0, 40)

DisableFlyButton.Parent = FlyFrame
DisableFlyButton.Text = "Disable Fly"
DisableFlyButton.Size = UDim2.new(0, 180, 0, 40)

SpeedBox.Parent = FlyFrame
SpeedBox.Text = "Speed: 50"
SpeedBox.Size = UDim2.new(0, 180, 0, 40)
