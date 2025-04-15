-- Emilli Hub Interface Script com Abas e Funções

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TopBar = Instance.new("Frame")
local MinimizeButton = Instance.new("TextButton")
local CloseButton = Instance.new("TextButton")
local SideBar = Instance.new("Frame")
local Content = Instance.new("Frame")
local miniBtn = Instance.new("TextButton")

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false

-- MAIN FRAME
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.5, -300, 0.5, -200)
MainFrame.Size = UDim2.new(0, 600, 0, 400)
MainFrame.Active = true
MainFrame.Draggable = true

-- TOP BAR
TopBar.Name = "TopBar"
TopBar.Parent = MainFrame
TopBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
TopBar.Size = UDim2.new(1, 0, 0, 30)

-- MINIMIZE BUTTON
MinimizeButton.Name = "MinimizeButton"
MinimizeButton.Parent = TopBar
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -60, 0, 0)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.BorderSizePixel = 0

-- CLOSE BUTTON
CloseButton.Name = "CloseButton"
CloseButton.Parent = TopBar
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -30, 0, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.BorderSizePixel = 0

-- SIDEBAR
SideBar.Name = "SideBar"
SideBar.Parent = MainFrame
SideBar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
SideBar.Position = UDim2.new(0, 0, 0, 30)
SideBar.Size = UDim2.new(0, 150, 1, -30)

-- CONTENT FRAME
Content.Name = "Content"
Content.Parent = MainFrame
Content.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Content.Position = UDim2.new(0, 150, 0, 30)
Content.Size = UDim2.new(1, -150, 1, -30)

-- MINI BUTTON (para restaurar a interface)
miniBtn.Name = "MiniBtn"
miniBtn.Parent = ScreenGui
miniBtn.Size = UDim2.new(0, 50, 0, 50)
miniBtn.Position = UDim2.new(0.5, -25, 0.5, -25)
miniBtn.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
miniBtn.Visible = false
miniBtn.Text = ""

-- E IMAGE ICON (no mini botão)
local icon = Instance.new("ImageLabel", miniBtn)
icon.Size = UDim2.new(1, 0, 1, 0)
icon.Position = UDim2.new(0, 0, 0, 0)
icon.BackgroundTransparency = 1
icon.Image = "rbxassetid://ID_DA_IMAGEM"  -- Coloque o ID real aqui

-- DRAG MINI BUTTON
miniBtn.Active = true
miniBtn.Draggable = true

-- FUNÇÕES

-- Minimizar a interface
MinimizeButton.MouseButton1Click:Connect(function()
	MainFrame.Visible = false
	miniBtn.Visible = true
end)

-- Restaurar a interface
miniBtn.MouseButton1Click:Connect(function()
	MainFrame.Visible = true
	miniBtn.Visible = false
end)

-- Fechar a interface
CloseButton.MouseButton1Click:Connect(function()
	ScreenGui:Destroy()
end)

-- ABAS

-- Criando as abas na barra lateral
local tab1 = Instance.new("TextButton")
tab1.Parent = SideBar
tab1.Size = UDim2.new(1, 0, 0, 50)
tab1.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
tab1.Text = "Funções de Jogo"
tab1.TextColor3 = Color3.fromRGB(255, 255, 255)
tab1.TextSize = 18
tab1.BorderSizePixel = 0

local tab2 = Instance.new("TextButton")
tab2.Parent = SideBar
tab2.Size = UDim2.new(1, 0, 0, 50)
tab2.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
tab2.Text = "Comandos Admin"
tab2.TextColor3 = Color3.fromRGB(255, 255, 255)
tab2.TextSize = 18
tab2.BorderSizePixel = 0

local tab3 = Instance.new("TextButton")
tab3.Parent = SideBar
tab3.Size = UDim2.new(1, 0, 0, 50)
tab3.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
tab3.Text = "Visual Features"
tab3.TextColor3 = Color3.fromRGB(255, 255, 255)
tab3.TextSize = 18
tab3.BorderSizePixel = 0

local tab4 = Instance.new("TextButton")
tab4.Parent = SideBar
tab4.Size = UDim2.new(1, 0, 0, 50)
tab4.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
tab4.Text = "Avançado"
tab4.TextColor3 = Color3.fromRGB(255, 255, 255)
tab4.TextSize = 18
tab4.BorderSizePixel = 0

-- ABAS INTERATIVAS
local currentTab = nil  -- Para saber qual aba está ativa

-- Função para mudar o conteúdo dependendo da aba selecionada
local function setTabContent(tab)
	if currentTab then
		currentTab.BackgroundColor3 = Color3.fromRGB(35, 35, 35)  -- Cor padrão das abas
	end
	tab.BackgroundColor3 = Color3.fromRGB(50, 50, 50)  -- Cor ativa da aba
	currentTab = tab
	
	-- Limpa o conteúdo atual
	for _, child in pairs(Content:GetChildren()) do
		child:Destroy()
	end
	
	-- Adiciona conteúdo à aba
	if tab == tab1 then
		-- Funções de Jogo
		local btnFly = Instance.new("TextButton")
		btnFly.Parent = Content
		btnFly.Size = UDim2.new(1, 0, 0, 50)
		btnFly.Text = "Fly"
		btnFly.TextColor3 = Color3.fromRGB(255, 255, 255)
		btnFly.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
		btnFly.TextSize = 18
		btnFly.BorderSizePixel = 0
		
		btnFly.MouseButton1Click:Connect(function()
			print("Fly ativado!")
		end)

		local btnSpeed = Instance.new("TextButton")
		btnSpeed.Parent = Content
		btnSpeed.Size = UDim2.new(1, 0, 0, 50)
		btnSpeed.Text = "Speed"
		btnSpeed.TextColor3 = Color3.fromRGB(255, 255, 255)
		btnSpeed.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
		btnSpeed.TextSize = 18
		btnSpeed.BorderSizePixel = 0
		
		btnSpeed.MouseButton1Click:Connect(function()
			print("Speed ativado!")
		end)

		-- Adicione mais funções de jogo aqui

	elseif tab == tab2 then
		-- Comandos Admin
		local btnKick = Instance.new("TextButton")
		btnKick.Parent = Content
		btnKick.Size = UDim2.new(1, 0, 0, 50)
		btnKick.Text = "Kick Player"
		btnKick.TextColor3 = Color3.fromRGB(255, 255, 255)
		btnKick.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
		btnKick.TextSize = 18
		btnKick.BorderSizePixel = 0
		
		btnKick.MouseButton1Click:Connect(function()
			print("Kick Player executado!")
		end)

		local btnBan = Instance.new("TextButton")
		btnBan.Parent = Content
		btnBan.Size = UDim2.new(1, 0, 0, 50)
		btnBan.Text = "Ban Player"
		btnBan.TextColor3 = Color3.fromRGB(255, 255, 255)
		btnBan.BackgroundColor3 = Color
