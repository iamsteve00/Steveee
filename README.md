local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Sidebar = Instance.new("Frame")
local ContentFrame = Instance.new("ScrollingFrame")
local UICorner = Instance.new("UICorner")
local UIListLayout = Instance.new("UIListLayout")
local CloseButton = Instance.new("TextButton")
local MinimizeButton = Instance.new("TextButton")

-- Configurar ScreenGui
ScreenGui.Name = "EmilliHub"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Frame Principal
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Size = UDim2.new(0, 600, 0, 400)
MainFrame.Position = UDim2.new(0.2, 0, 0.2, 0)

-- Sidebar
Sidebar.Name = "Sidebar"
Sidebar.Parent = MainFrame
Sidebar.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
Sidebar.Size = UDim2.new(0, 120, 1, 0)

-- Botões da Sidebar (exemplo)
local sidebarOptions = {"Info", "Scripts Trolls", "Troll Player", "Avatar", "Casa", "Audio All", "Lag Server FE", "Nomes"}
for _, name in pairs(sidebarOptions) do
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(1, 0, 0, 30)
	btn.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
	btn.Text = name
	btn.Font = Enum.Font.SourceSans
	btn.TextColor3 = Color3.fromRGB(255, 255, 255)
	btn.TextSize = 14
	btn.Parent = Sidebar
end

-- Área de Conteúdo
ContentFrame.Name = "ContentFrame"
ContentFrame.Parent = MainFrame
ContentFrame.Position = UDim2.new(0, 130, 0, 40)
ContentFrame.Size = UDim2.new(1, -140, 1, -50)
ContentFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
ContentFrame.CanvasSize = UDim2.new(0, 0, 2, 0)
ContentFrame.ScrollBarThickness = 6

-- Layout dos botões
UIListLayout.Parent = ContentFrame
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 5)

-- Botões de exemplo com ícone
local buttons = {"Fling Boat", "Disable Fling Boat", "Kill All Bus", "House Ban Kill All", "Fling Boat All", "Bring All [melhor]"}
for _, text in pairs(buttons) do
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(1, -10, 0, 40)
	btn.Text = text
	btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	btn.Font = Enum.Font.SourceSansBold
	btn.TextColor3 = Color3.fromRGB(255, 255, 255)
	btn.TextSize = 18
	btn.Parent = ContentFrame

	local icon = Instance.new("ImageLabel")
	icon.Size = UDim2.new(0, 24, 0, 24)
	icon.Position = UDim2.new(1, -30, 0.5, -12)
	icon.BackgroundTransparency = 1
	icon.Image = "rbxassetid://3926305904" -- ícone fingerprint (se quiser outro, posso trocar)
	icon.ImageRectOffset = Vector2.new(324, 4)
	icon.ImageRectSize = Vector2.new(36, 36)
	icon.Parent = btn
end

-- Botões de fechar e minimizar
CloseButton.Name = "CloseButton"
CloseButton.Parent = MainFrame
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Text = "X"
CloseButton.BackgroundColor3 = Color3.fromRGB(60, 0, 0)
CloseButton.TextColor3 = Color3.new(1, 1, 1)
CloseButton.MouseButton1Click:Connect(function()
	ScreenGui:Destroy()
end)

MinimizeButton.Name = "MinimizeButton"
MinimizeButton.Parent = MainFrame
MinimizeButton.Position = UDim2.new(1, -70, 0, 5)
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Text = "-"
MinimizeButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
MinimizeButton.TextColor3 = Color3.new(1, 1, 1)
MinimizeButton.MouseButton1Click:Connect(function()
	MainFrame.Visible = false
end)
