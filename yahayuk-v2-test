--// Load Rayfield UI
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
    Name = "Script Yahahahahahayuk",
    LoadingTitle = "Script Yahahahahahayuk",
    LoadingSubtitle = "By Jamet",
    ConfigurationSaving = {
       Enabled = false,
    },
    KeySystem = false,
})

--// Buat Tab
local Tab = Window:CreateTab("Coba", 4483362458)

--// Checkpoint List
local checkpoints = {
    Vector3.new(-417.717041, 250.125443, 768.976562),   -- cp1
    Vector3.new(-347.273407, 389.755432, 523.254944),   -- cp2
    Vector3.new(287.095459, 430.755371, 504.069824),    -- cp3
    Vector3.new(334.016785, 491.755432, 347.104889),    -- cp4
    Vector3.new(211.191711, 315.755432, -146.613632),   -- cp5
    Vector3.new(-611.723022, 906.495422, -529.531555),  -- summit
}

local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Fungsi untuk ambil HRP & Humanoid
local function getHRP()
    local char = player.Character or player.CharacterAdded:Wait()
    return char:WaitForChild("HumanoidRootPart"), char:WaitForChild("Humanoid")
end

--// Manual Teleport Buttons (CP1 - CP5)
for i = 1, 5 do
    Tab:CreateButton({
        Name = "Teleport CP" .. i,
        Callback = function()
            local hrp = getHRP()
            hrp.CFrame = CFrame.new(checkpoints[i])
        end,
    })
end

--// Manual Teleport Button untuk Summit (dibawah CP5)
Tab:CreateButton({
    Name = "Teleport Summit",
    Callback = function()
        local hrp = getHRP()
        hrp.CFrame = CFrame.new(checkpoints[6])
    end,
})

--// Looping Auto Summit
local running = false

Tab:CreateButton({
    Name = "Auto Summit",
    Callback = function()
        if running then return end
        running = true
        print("Auto Summit mulai...")
        
        task.spawn(function()
            while running do
                local hrp, humanoid = getHRP()

                -- teleport semua cp sampai summit
                for i = 1, #checkpoints do
                    if not running then break end
                    hrp.CFrame = CFrame.new(checkpoints[i])
                    print("Teleport ke CP " .. i)
                    task.wait(2) -- jeda 2 detik

                    -- kalau udah summit → respawn
                    if i == #checkpoints and running then
                        print("Sudah sampai Summit, respawn...")
                        humanoid.Health = 0
                        player.CharacterAdded:Wait()
                        task.wait(2) -- jeda respawn
                    end
                end
            end
        end)
    end,
})

--// Stop Looping
Tab:CreateButton({
    Name = "Stop Looping",
    Callback = function()
        running = false
        print("Looping dihentikan!")
    end,
})
