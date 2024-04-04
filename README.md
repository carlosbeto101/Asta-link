local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local PlayerTags = script.Parent

-- Supongamos que tienes una función que convierte la posición del jugador en el mundo a la posición en tu mapa o UI.
-- Esta función dependerá de cómo esté diseñado tu mapa/UI y cómo quieras que se relacione con el mundo del juego.
local function WorldToScreenPosition(worldPosition)
    -- Implementa la conversión aquí.
    -- Retorna una UDim2 que representa la posición en la UI.
end

local function UpdateTagPosition(player)
    local Tag = PlayerTags:FindFirstChild(player.Name .. "Tag")
    if Tag then
        local playerPosition = player.Character and player.Character:FindFirstChild("HumanoidRootPart").Position
        if playerPosition then
            Tag.Position = WorldToScreenPosition(playerPosition)
        end
    end
end

local function UpdateAllTags()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            UpdateTagPosition(player)
        end
    end
end

-- Actualiza la posición de las etiquetas en cada frame.
RunService.RenderStepped:Connect(UpdateAllTags)
