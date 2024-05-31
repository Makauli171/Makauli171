-- 1. Rastrear ovos raros
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local EggFolder = ReplicatedStorage:WaitForChild("Eggs")

local function trackRareEggs()
    while true do
        for _, egg in pairs(EggFolder:GetChildren()) do
            if egg:IsA("Model") and egg:FindFirstChild("Rare") then
                print("Ovo raro encontrado:", egg.Name)
            end
        end
        wait(1)
    end
end

-- 2. Caminhar até moedas
local PathfindingService = game:GetService("PathfindingService")
local Player = game.Players.LocalPlayer
local Character = Player.Character

local function walkToCoin(coinPosition)
    local path = PathfindingService:CreatePath({
        AgentRadius = 2,
        AgentHeight = 5,
        AgentCanJump = true,
        AgentJumpHeight = 10,
        AgentMaxSlope = 45,
        AgentMaxStepHeight = 5,
    })
    path:ComputeAsync(Character.HumanoidRootPart.Position, coinPosition)
    path:MoveTo(Character.HumanoidRootPart)
end

-- Exemplo de uso:
local coinPosition = Vector3.new(10, 0, 20) -- Posição da moeda
walkToCoin(coinPosition)

-- 3. Mostrar o time de cada jogador
local Players = game:GetService("Players")

local function showPlayerRoles()
    for _, player in pairs(Players:GetPlayers()) do
        local role = player.Team.Name
        print(player.Name, "é", role)
    end
end

showPlayerRoles()

-- 4. Ficar invisível para outros jogadores
local Humanoid = Character:WaitForChild("Humanoid")
Humanoid:SetAttribute("Invisibility", 0.5) -- Valor entre 0 (totalmente visível) e 1 (totalmente invisível)
