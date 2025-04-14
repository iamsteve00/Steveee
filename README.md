local player = game.Players.LocalPlayer
local gui = player:WaitForChild("PlayerGui")
local isAdmin = false -- Defina como verdadeiro para testar os comandos de admin.

-- Função para verificar se o jogador é admin
local function checkAdmin()
    local adminList = {"AdminPlayer1", "AdminPlayer2"} -- Adicione aqui os nomes dos administradores.
    for _, adminName in ipairs(adminList) do
        if player.Name == adminName then
            isAdmin = true
            break
        end
    end
end

-- Criação do hub principal
local hubFrame = Instance.new("Frame", gui)
hubFrame.Size = UDim2.new(0, 600, 0, 500)
hubFrame.Position = UDim2.new(0.5, -300, 0.5, -250)
hubFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
hubFrame.BorderSizePixel = 0
hubFrame.Active = true
hubFrame.Draggable = true

-- Título principal do Hub
local title = Instance.new("TextLabel", hubFrame)
title.Size = UDim2.new(1, 0, 0, 50)
title.Text = "Emilli Hub - Hubs Integrados"
title.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.GothamBold
title.TextSize = 24

-- Aba para alternar entre funcionalidades
local tabs = {"ChaosHub", "SanderXHub", "RaelHub", "Admin", "Exploração", "Visuais"}
local tabButtons = {}
local contentFrames = {}

-- Função para criar botões
local function createButton(parent, name, position, callback)
    local button = Instance.new("TextButton", parent)
    button.Size = UDim2.new(0, 200, 0, 40)
    button.Position = position
    button.Text = name
    button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.GothamBold
    button.TextSize = 16
    button.MouseButton1Click:Connect(callback)

    -- Efeito de hover
    button.MouseEnter:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    end)
    button.MouseLeave:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    end)
end

-- Criar abas e conteúdo de cada hub
for i, tabName in ipairs(tabs) do
    local tab = Instance.new("TextButton", hubFrame)
    tab.Size = UDim2.new(0, 120, 0, 30)
    tab.Position = UDim2.new(0, (i - 1) * 123, 0, 60)
    tab.Text = tabName
    tab.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    tab.TextColor3 = Color3.new(1, 1, 1)
    tab.Font = Enum.Font.GothamSemibold
    tab.TextSize = 16
    table.insert(tabButtons, tab)

    local content = Instance.new("Frame", hubFrame)
    content.Size = UDim2.new(1, -20, 1, -100)
    content.Position = UDim2.new(0, 10, 0, 95)
    content.BackgroundTransparency = 1
    content.Visible = (i == 1)
    table.insert(contentFrames, content)

    tab.MouseButton1Click:Connect(function()
        for j = 1, #tabs do
            contentFrames[j].Visible = (j == i)
        end
    end)
end

-- Funções específicas dos hubs integrados

-- Chaos Hub: Funções como NoClip e Velocidade
local chaosHubFrame = contentFrames[1]
createButton(chaosHubFrame, "NoClip", UDim2.new(0.1, 0, 0.1, 0), function()
    local char = player.Character
    if char then
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = hrp.CFrame + Vector3.new(0, 100, 0) -- NoClip (atravessar paredes)
        end
    end
end)

createButton(chaosHubFrame, "Velocidade 100", UDim2.new(0.1, 0, 0.3, 0), function()
    local humanoid = player.Character:FindFirstChild("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = 100
    end
end)

-- SanderX Hub: Admin e Comandos de Servidor
local sanderXHubFrame = contentFrames[2]
createButton(sanderXHubFrame, "Banir Jogador", UDim2.new(0.1, 0, 0.1, 0), function()
    if isAdmin then
        local playerToBan = "JogadorExemplo"
        -- Código para banir jogador do servidor
        print(playerToBan .. " banido!")
    else
        notify("Você não tem permissão para isso.")
    end
end)

createButton(sanderXHubFrame, "Alterar Hora para Dia", UDim2.new(0.1, 0, 0.3, 0), function()
    game.Lighting.TimeOfDay = "12:00:00"
    notify("Hora alterada para o dia.")
end)

-- Rael Hub: Personalização e Interação com o Mundo
local raelHubFrame = contentFrames[3]
createButton(raelHubFrame, "Criar Carro", UDim2.new(0.1, 0, 0.1, 0), function()
    local car = game.Workspace:FindFirstChild("CarroExemplo") -- Exemplo
    if car then
        car:Clone().Parent = game.Workspace
    end
end)

createButton(raelHubFrame, "Mudar Cor do Personagem", UDim2.new(0.1, 0, 0.3, 0), function()
    local char = player.Character
    if char then
        char:FindFirstChild("BodyColors").HeadColor = BrickColor.new("Bright red")
    end
end)

-- Funções de Admin (Para admins)
local adminHubFrame = contentFrames[4]
createButton(adminHubFrame, "Alterar Hora para Noite", UDim2.new(0.1, 0, 0.1, 0), function()
    game.Lighting.TimeOfDay = "00:00:00"
    notify("Hora alterada para a noite.")
end)

-- Funções de Exploração (Voo, Teleporte)
local exploracaoFrame = contentFrames[5]
createButton(exploracaoFrame, "Voo", UDim2.new(0.1, 0, 0.1, 0), function()
    local bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.MaxForce = Vector3.new(4000, 4000, 4000)
    bodyVelocity.Velocity = Vector3.new(0, 100, 0)
    bodyVelocity.Parent = player.Character:WaitForChild("HumanoidRootPart")
    notify("Você agora pode voar!")
end)

createButton(exploracaoFrame, "Teleporte para a Delegacia", UDim2.new(0.1, 0, 0.3, 0), function()
    local char = player.Character
    if char then
        char.HumanoidRootPart.CFrame = CFrame.new(69, 10, -141) -- Coordenadas da delegacia
        notify("Teleportado para a delegacia!")
    end
end)

-- Funções Visuais
local visuaisFrame = contentFrames[6]
createButton(visuaisFrame, "Mudar Cor do Céu", UDim2.new(0.1, 0, 0.1, 0), function()
    game.Lighting.Ambient = Color3.fromRGB(0, 0, 0)
    notify("Cor do céu alterada.")
end)

-- Função de notificação
local function notify(message)
    local notif = Instance.new("TextLabel", hubFrame)
    notif.Size = UDim2.new(1, 0, 0, 50)
    notif.Position = UDim2.new(0, 0, 0, -50)
    notif.Text = message
    notif.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    notif.TextColor3 = Color3.new(1, 1, 1)
    notif.Font = Enum.Font.GothamBold
    notif.TextSize = 16
    notif.Visible = true
    game:GetService("TweenService"):Create(notif, TweenInfo.new(0.5), {Position = UDim2.new(0, 0, 0, 10)}):Play()
    wait(3)
    game:GetService("TweenService"):Create(notif, TweenInfo.new(0.5), {Position = UDim2.new(0, 0, 0, -50)}):Play()
end
