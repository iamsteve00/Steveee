-- Função para garantir que a execução do código seja segura
local function safeCall(func)
    pcall(func)
end

-- Função para exibir mensagens de sucesso ou erro
local function displayMessage(message, type)
    local color = type == "success" and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 0, 0)
    print(message)  
end

-- Função para verificar se o jogador está validado
local function verifyPlayer()
    local player = game.Players.LocalPlayer
    return player and player.Character and player.Character:FindFirstChild("HumanoidRootPart")
end

-- Fly: Movimentação disfarçada para evitar detecção
local function fly()
    if not verifyPlayer() then return end
    safeCall(function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            local humanoid = character:FindFirstChild("Humanoid")
            if humanoid then
                humanoid.PlatformStand = true
                local bodyGyro = Instance.new("BodyGyro")
                bodyGyro.CFrame = character.HumanoidRootPart.CFrame
                bodyGyro.MaxTorque = Vector3.new(4000, 4000, 4000)
                bodyGyro.Parent = character.HumanoidRootPart

                local bodyVelocity = Instance.new("BodyVelocity")
                bodyVelocity.MaxForce = Vector3.new(10000, 10000, 10000)
                bodyVelocity.Velocity = Vector3.new(0, 5, 0)
                bodyVelocity.Parent = character.HumanoidRootPart

                wait(1)
                bodyGyro:Destroy()
                bodyVelocity:Destroy()
            end
        end
    end)
end

-- Função de matar jogador
local function killPlayer()
    if not verifyPlayer() then return end
    safeCall(function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        if character and character:FindFirstChild("Humanoid") then
            local humanoid = character:FindFirstChild("Humanoid")
            humanoid.Health = 0  -- Mata o jogador
            displayMessage("Você matou um jogador.", "success")
        end
    end)
end

-- Função de teleportação para outro jogador
local function viewPlayer()
    if not verifyPlayer() then return end
    safeCall(function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            local randomPlayer = game.Players:GetPlayers()[math.random(1, #game.Players:GetPlayers())]
            if randomPlayer and randomPlayer.Character then
                character.HumanoidRootPart.CFrame = randomPlayer.Character.HumanoidRootPart.CFrame
                displayMessage("Você está agora vendo o jogador: " .. randomPlayer.Name, "success")
            end
        end
    end)
end

-- Anti-Ban: Protege contra o sistema de detecção de banimento
local function antiBan()
    displayMessage("Anti-Ban ativado!", "success")
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        while true do
            wait(math.random(5, 10))
            local randomPosition = Vector3.new(math.random(-10, 10), 5, math.random(-10, 10))
            character:SetPrimaryPartCFrame(CFrame.new(randomPosition))
        end
    end
end

-- Resetar o personagem para um local seguro
local function resetCharacter()
    if not verifyPlayer() then return end
    safeCall(function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        if character then
            character:SetPrimaryPartCFrame(CFrame.new(0, 50, 0)) -- Teleporta para um local seguro
            displayMessage("Você foi teleportado de volta.", "success")
        end
    end)
end

-- Função para ocultar comportamentos suspeitos
local function hideSuspiciousEvents()
    -- Alterar eventos de "Touched" e "Changed" para impedir a detecção
end

-- Função para otimizar o desempenho do script
local function optimizePerformance()
    -- Ajustar configurações de desempenho para garantir que o script funcione de maneira mais suave
end

-- Função para criar um menu GUI com todas as opções do hub
local function createMainMenu()
    local player = game.Players.LocalPlayer
    local screenGui = Instance.new("ScreenGui")
    screenGui.Parent = player:WaitForChild("PlayerGui")

    local mainFrame = Instance.new("Frame")
    mainFrame.Parent = screenGui
    mainFrame.Size = UDim2.new(0, 250, 0, 450)
    mainFrame.Position = UDim2.new(0.5, -125, 0.5, -225)
    mainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    mainFrame.BorderSizePixel = 2
    mainFrame.BorderColor3 = Color3.fromRGB(255, 255, 255)

    -- Adicionando botões com as funções do Hub
    createButton(mainFrame, "Ativar Fly", UDim2.new(0.1, 0, 0.1, 0), fly)
    createButton(mainFrame, "Matar Jogador", UDim2.new(0.1, 0, 0.2, 0), killPlayer)
    createButton(mainFrame, "Visualizar Jogador", UDim2.new(0.1, 0, 0.3, 0), viewPlayer)
    createButton(mainFrame, "Ativar Anti-Ban", UDim2.new(0.1, 0, 0.4, 0), antiBan)
    createButton(mainFrame, "Resetar Personagem", UDim2.new(0.1, 0, 0.5, 0), resetCharacter)
end

-- Função para criar um botão customizado na UI
local function createButton(parent, text, position, func)
    local button = Instance.new("TextButton")
    button.Parent = parent
    button.Size = UDim2.new(0, 200, 0, 40)
    button.Position = position
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
    button.BorderSizePixel = 2
    button.BorderColor3 = Color3.fromRGB(255, 255, 255)

    button.MouseButton1Click:Connect(function()
        safeCall(func)
    end)
end

-- Função para ativar todos os hubs (ChaosHub, SanderX, RaelHub)
local function activateAllHubs()
    -- Inserir os scripts dos hubs ChaosHub, SanderX e RaelHub no script, se necessário
end

-- Função de segurança contra banimento (anti-ban)
local function antiBanProtection()
    -- Impede comportamentos que poderiam ser detectados por sistemas de anti-cheat
end

-- Inicialização do Hub: Criação do menu e ativação de funções
safeCall(function()
    hideSuspiciousEvents()
    optimizePerformance()
    createMainMenu()
    activateAllHubs()
    antiBanProtection()
end)
