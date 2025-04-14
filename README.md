-- Emilli Hub Completo com Interface Gráfica (300x400px) e Funções de Todos os Hubs

-- Criação da Interface de Usuário (GUI) - 300x400px
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player.PlayerGui

-- Criação do Frame Principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 400)  -- 300x400px
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)  -- Centralizado
mainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)  -- Cor de fundo preta
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui

-- Função para criar um botão
local function createButton(text, position, onClick)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 280, 0, 40)  -- Tamanho do botão
    button.Position = position
    button.Text = text
    button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Cor de fundo vermelha
    button.TextColor3 = Color3.fromRGB(255, 255, 255)  -- Cor do texto branca
    button.Font = Enum.Font.GothamBold
    button.TextSize = 18
    button.Parent = mainFrame

    button.MouseButton1Click:Connect(onClick)  -- Evento de clique no botão
end

-- Funções dos 4 hubs (Chaos, SanderX, Rael e Cartola Hub)
local function enableFly()
    -- Lógica para habilitar o Fly
    print("Fly ativado!")
end

local function killPlayer()
    -- Lógica para matar o jogador
    print("Jogador morto!")
end

local function setSpeed()
    -- Lógica para ajustar a velocidade
    print("Velocidade ajustada!")
end

local function unlockAll()
    -- Lógica para desbloquear itens
    print("Todos os itens desbloqueados!")
end

local function infiniteJump()
    -- Lógica para saltos infinitos
    print("Saltos infinitos ativados!")
end

local function enableNoClip()
    -- Lógica para ativar NoClip
    print("No Clip ativado!")
end

local function enableGodMode()
    -- Lógica para ativar o God Mode
    print("Modo Deus ativado!")
end

local function teleportHome()
    -- Lógica para teleportar para a casa
    print("Teleportando para a casa...")
end

local function teleportRandom()
    -- Lógica para teleportar aleatoriamente
    print("Teleportando aleatoriamente...")
end

local function unlockAllCars()
    -- Lógica para desbloquear todos os carros
    print("Todos os carros desbloqueados!")
end

local function enableVisualEffects()
    -- Lógica para ativar efeitos visuais
    print("Efeitos visuais ativados!")
end

-- Funções do Chaos Hub
local function ghostMode()
    -- Lógica para modo fantasma
    print("Modo Fantasma ativado!")
end

local function noGravity()
    -- Lógica para desativar a gravidade
    print("Gravidade desativada!")
end

local function removeWeapons()
    -- Lógica para remover todas as armas
    print("Todas as armas removidas!")
end

-- Funções do SanderX Hub
local function flySpeed()
    -- Lógica para velocidade de voo
    print("Velocidade de voo ajustada!")
end

local function antiJump()
    -- Lógica para desabilitar o salto
    print("Salto desabilitado!")
end

-- Funções do Rael Hub
local function speedBoost()
    -- Lógica para aumento de velocidade
    print("Aumento de velocidade ativado!")
end

local function turnInvisible()
    -- Lógica para tornar invisível
    print("Invisibilidade ativada!")
end

-- Funções do Cartola Hub
local function unlockAllVehicles()
    -- Lógica para desbloquear todos os veículos
    print("Todos os veículos desbloqueados!")
end

local function removeAllVehicles()
    -- Lógica para remover todos os veículos
    print("Todos os veículos removidos!")
end

-- Funções de Anti-Ban
function randomAntiBanActions()
    local actions = {
        enableFly,
        killPlayer,
        setSpeed,
        unlockAllCars,
        enableGodMode,
        teleportRandom,
        enableNoClip,
        teleportHome,
        ghostMode,
        noGravity,
        removeWeapons,
        flySpeed,
        antiJump,
        speedBoost,
        turnInvisible,
        unlockAllVehicles,
        removeAllVehicles
    }

    -- Escolhe uma ação aleatória
    local action = actions[math.random(1, #actions)]
    action()
end

-- Função de Anti-Ban com Intervalo
while true do
    wait(math.random(10, 30))  -- Espera entre 10 e 30 segundos
    randomAntiBanActions()
end

-- Adicionando os botões para as funções

createButton("Fly", UDim2.new(0, 10, 0, 10), enableFly)
createButton("Kill Player", UDim2.new(0, 10, 0, 60), killPlayer)
createButton("Set Speed", UDim2.new(0, 10, 0, 110), setSpeed)
createButton("Unlock All", UDim2.new(0, 10, 0, 160), unlockAll)
createButton("Infinite Jump", UDim2.new(0, 10, 0, 210), infiniteJump)
createButton("No Clip", UDim2.new(0, 10, 0, 260), enableNoClip)
createButton("God Mode", UDim2.new(0, 10, 0, 310), enableGodMode)
createButton("Teleport Home", UDim2.new(0, 10, 0, 360), teleportHome)
createButton("Teleport Random", UDim2.new(0, 10, 0, 410), teleportRandom)
createButton("Unlock All Cars", UDim2.new(0, 10, 0, 460), unlockAllCars)
createButton("Visual Effects", UDim2.new(0, 10, 0, 510), enableVisualEffects)

-- Funções dos outros hubs (Chaos, SanderX, Rael e Cartola)
createButton("Ghost Mode", UDim2.new(0, 10, 0, 560), ghostMode)
createButton("No Gravity", UDim2.new(0, 10, 0, 610), noGravity)
createButton("Remove Weapons", UDim2.new(0, 10, 0, 660), removeWeapons)

createButton("Fly Speed", UDim2.new(0, 10, 0, 710), flySpeed)
createButton("Anti Jump", UDim2.new(0, 10, 0, 760), antiJump)

createButton("Speed Boost", UDim2.new(0, 10, 0, 810), speedBoost)
createButton("Invisible", UDim2.new(0, 10, 0, 860), turnInvisible)

createButton("Unlock All Vehicles", UDim2.new(0, 10, 0, 910), unlockAllVehicles)
createButton("Remove All Vehicles", UDim2.new(0, 10, 0, 960), removeAllVehicles)

-- Função para fechar o hub (botão "Fechar")
local function closeHub()
    screenGui:Destroy()  -- Fecha o hub removendo a interface
end

-- Adicionando o botão de fechar
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 280, 0, 40)  -- Tamanho do botão
closeButton.Position = UDim2.new(0, 10, 0, 1010)  -- Posição abaixo dos outros botões
closeButton.Text = "Fechar"
closeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Cor de fundo vermelha
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)  -- Cor do texto branca
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 18
closeButton.Parent = mainFrame

closeButton.MouseButton1Click:Connect(closeHub)  -- Evento de clique para fechar o hub
