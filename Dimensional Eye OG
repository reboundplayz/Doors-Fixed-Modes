--// Services
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")

local player = Players.LocalPlayer

--// Custom Audio Downloader (Using writefile / getcustomasset)
local fileName = "NewDamageNoise.mp3"
local customSoundUrl = "https://github.com/reboundplayz/Doors-Fixed-Modes/raw/refs/heads/main/NewDamageNoise.mp3.mpeg"

if writefile and getcustomasset and not isfile(fileName) then
    local success, result = pcall(function()
        return game:HttpGet(customSoundUrl)
    end)
    if success and result then
        writefile(fileName, result)
    end
end

local customDamageSound = Instance.new("Sound")
customDamageSound.Name = "CustomDamageSound"
customDamageSound.Volume = 2
customDamageSound.Parent = game:GetService("SoundService")

if isfile(fileName) and getcustomasset then
    customDamageSound.SoundId = getcustomasset(fileName)
end

--// Check current room
local entityModel = true
local latestRoom = game.ReplicatedStorage.GameData.LatestRoom.Value

if game.Workspace:FindFirstChild("SeekMovingNewClone")
or latestRoom == 50
or latestRoom == 100
or (latestRoom >= 90 and latestRoom <= 100) then
    entityModel = false
end

--// Load asset safely
local assets = game:GetObjects("rbxassetid://112033845584439")
if not assets or #assets == 0 then
    warn("Greed asset failed to load")
    return
end

local root = assets[1]

-- Find Model inside asset (IMPORTANT FIX)
local model = nil

if root:IsA("Model") then
    model = root
else
    for _, v in ipairs(root:GetDescendants()) do
        if v:IsA("Model") then
            model = v
            break
        end
    end
end

if not model then
    warn("No model found inside Greed asset")
    return
end

model.Parent = workspace
model.Name = "Greed"

local greed = workspace:WaitForChild("Greed")

--// Safely disable lights
local effects = greed:FindFirstChild("Effects")
if effects then
    local p2 = effects:FindFirstChild("PointLight2")
    if p2 then p2:Destroy() end

    local p1 = effects:FindFirstChild("PointLight")
    if p1 then
        p1.Range = 0
    end

    -- tween light safely
    if p1 then
        TweenService:Create(p1, TweenInfo.new(3), {Range = 20}):Play()
    end
end

--// Find a valid part (safe)
local part
for _, v in ipairs(greed:GetDescendants()) do
    if v:IsA("BasePart") then
        part = v
        break
    end
end

if not part then
    warn("Greed has no BasePart")
    return
end

--// Position in room safely
task.wait(1)

local rooms = workspace:WaitForChild("CurrentRooms"):GetChildren()
local lastRoom = rooms[#rooms - 1]

if lastRoom and lastRoom:FindFirstChild("Parts") and lastRoom.Parts:FindFirstChild("Floor") then
    part.CFrame = lastRoom.Parts.Floor.CFrame + Vector3.new(0, 6, 0)
end

--// Main logic
local Greed = true

task.spawn(function()
    while Greed do
        task.wait(0.05)

        local char = player.Character
        local hum = char and char:FindFirstChild("Humanoid")
        local cam = workspace.CurrentCamera

        if hum and cam and part then
            -- PROPER look check (fixes viewport bug)
            local direction = (part.Position - cam.CFrame.Position).Unit
            local look = cam.CFrame.LookVector

            local dot = look:Dot(direction)

            -- if looking at it
            if dot > 0.5 then
                hum:TakeDamage(0.2)
                
                -- Play custom audio whenever look check inflicts damage
                if customDamageSound.SoundId ~= "" then
                    customDamageSound:Play()
                end
            end

            if hum.Health <= 0 then
                firesignal(
                    game.ReplicatedStorage.RemotesFolder.DeathHint.OnClientEvent,
                    {
                        "You died to who you call Dimensional Eye...",
                        "He spawns in the center and damages you if you look at him"
                    },
                    "Blue"
                )

                game:GetService("ReplicatedStorage")
                    .GameStats["Player_" .. player.Name]
                    .Total.DeathCause.Value = "Dimensional Eye"
            end
        end
    end
end)

--// Cleanup on room change
game.ReplicatedStorage.GameData.LatestRoom.Changed:Connect(function()
    Greed = false

    local g = workspace:FindFirstChild("Greed")
    if g then
        g:Destroy()
    end
end)
