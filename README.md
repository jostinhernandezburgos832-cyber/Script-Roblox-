# Script-Roblox-
Auto farmeo 
-- Escape Waves For Lucky Blocks - Auto Farm Admin Tokens (Auto Claim Mejorado)
-- Modificado por Grok - Con Auto Server Hop al finalizar el recorrido

local player = game.Players.LocalPlayer
local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")

local character = player.Character or player.CharacterAdded:Wait()
local root = character:WaitForChild("HumanoidRootPart")

-- ✅ NUEVAS COORDENADAS
local positions = {
    CFrame.new(643, 3, -83),
    CFrame.new(931, 3, -70),
    CFrame.new(721, -3, 134),
    CFrame.new(737, -3, 1137),
    CFrame.new(858, -3, 1707),
    CFrame.new(721, -3, 2479),
    CFrame.new(859, 3, 2790),
    CFrame.new(730, -3, 3389),
    CFrame.new(859, -3, 4791),
    CFrame.new(721, 3, 5762),
    CFrame.new(790, 3, -88)
}

-- Función para simular presionar E
local function claimItem()
    game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.E, false, game)
    wait(0.05)
    game:GetService("VirtualInputManager"):SendKeyEvent(false, Enum.KeyCode.E, false, game)
end

-- Función para cambiar a un servidor diferente (Server Hop)
local function serverHop()
    print("🔄 Completando ciclo... Cambiando a un nuevo servidor en 3 segundos...")
    wait(3)
    
    local success, err = pcall(function()
        -- Método simple y efectivo para ir a un servidor público diferente
        TeleportService:Teleport(game.PlaceId, player)
    end)
    
    if not success then
        print("❌ Error al cambiar de servidor: " .. tostring(err))
        print("Intentando de nuevo en 5 segundos...")
        wait(5)
        TeleportService:Teleport(game.PlaceId, player)
    end
end

print("🚀 Auto Farm Admin Tokens iniciado")
print("📍 Usando " .. #positions .. " posiciones | Auto Server Hop activado al final de cada ciclo")

while true do
    for _, pos in ipairs(positions) do
        if root and root.Parent then
            root.CFrame = pos
            wait(1.3)
            
            for i = 1, 7 do
                claimItem()
                wait(0.32)
            end
        else
            character = player.Character or player.CharacterAdded:Wait()
            root = character:WaitForChild("HumanoidRootPart")
        end
    end
    
    print("✅ Ciclo completo finalizado (" .. #positions .. " posiciones visitadas)")
    serverHop()  -- Cambia de servidor automáticamente
    
    -- El script se detendrá aquí porque el teleport reinicia el juego
    wait(10) -- Por si falla el teleport, reintenta el ciclo
end
