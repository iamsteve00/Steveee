local ChaosHub = loadstring(game:HttpGet("https://pastebin.com/raw/6ZeQgsmw"))()

-- Funções aprimoradas do SanderX
local function SanderXFeatures()
    -- Teleporte para locais específicos
    local locations = {
        Bank = Vector3.new(0, 10, 0),
        Hospital = Vector3.new(50, 10, 100),
        PoliceStation = Vector3.new(-100, 10, 200),
    }
    local function TeleportTo(place)
        if locations[place] then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(locations[place])
        end
    end

    -- Veículos turbo
    for _,v in pairs(game.Workspace:GetChildren()) do
        if v:IsA("VehicleSeat") then
            v.MaxSpeed = 500
        end
    end

    -- Invisibilidade temporária
    game.Players.LocalPlayer.Character.Head.Transparency = 1
    game.Players.LocalPlayer.Character.HumanoidRootPart.Transparency = 1

    -- Super pulo
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = 100
end

-- Funções aprimoradas do Rael Hub
local function RaelHubFeatures()
    -- ESP para visualizar jogadores e veículos
    for _,v in pairs(game.Players:GetPlayers()) do
        if v.Character then
            local highlight = Instance.new("Highlight")
            highlight.Parent = v.Character
            highlight.FillColor = Color3.fromRGB(255, 0, 0)
            highlight.FillTransparency = 0.5
        end
    end

    -- Fly Mode
    local function EnableFly()
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid:SetStateEnabled(Enum.HumanoidStateType.Flying, true)
        end
    end

    -- God Mode
    local function EnableGodMode()
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
                part.Anchored = true
            end
        end
    end

    -- Speed Boost
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100

    -- Unban Feature (tentativa de reentrada)
    local function Unban()
        game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)
    end

    -- Executando funções
    task.spawn(EnableFly)
    task.spawn(EnableGodMode)
    task.spawn(Unban)
end

-- Funções aprimoradas do Chaos Hub
local function ChaosHubFeatures()
    -- Admin Menu (exemplo básico)
    local function OpenAdminMenu()
        print("Admin Menu Ativado!") -- Aqui pode ser expandido para abrir um GUI real
    end

    -- Kill All (exemplo de função ofensiva)
    local function KillAll()
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player ~= game.Players.LocalPlayer then
                player.Character:BreakJoints()
            end
        end
    end

    -- Gamepass Grátis
    local function FreeGamepass()
        local player = game.Players.LocalPlayer
        local backpack = player:FindFirstChild("Backpack")
        if backpack then
            local gamepassItem = Instance.new("Tool")
            gamepassItem.Parent = backpack
            gamepassItem.Name = "Gamepass Exclusivo"
        end
    end

    -- Executando funções
    task.spawn(OpenAdminMenu)
    task.spawn(KillAll)
    task.spawn(FreeGamepass)
end

-- Inicializando Chaos Hub e adicionando funções únicas dos outros scripts
ChaosHub()
task.spawn(SanderXFeatures)
task.spawn(RaelHubFeatures)
task.spawn(ChaosHubFeatures)local ChaosHub =

-- Funções específicas para Brookhaven
local function CustomFeatures()
    -- No Clip (atravessar paredes)
    local function EnableNoClip()
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid:ChangeState(Enum.HumanoidStateType.Physics)
        end
    end

    -- Super Speed (corrida ultra rápida)
    local function SuperSpeed()
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 200
    end

    -- Infinite Jump (pular infinitamente)
    local function InfiniteJump()
        local UserInputService = game:GetService("UserInputService")
        UserInputService.JumpRequest:Connect(function()
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end)
    end

    -- Executando funções
    task.spawn(EnableNoClip)
    task.spawn(SuperSpeed)
    task.spawn(InfiniteJump)
end

-- Inicializando Chaos Hub e adicionando funcionalidades extras
ChaosHub()
task.spawn(CustomFeatures)
