--[[ 
    MANUAL PIVOT ENTITY: OVERKILL (CRUCIFIX ANIMATION FIXED)
    Targeting specific hierarchy paths inside Model "50" with complete deep lighting removal,
    automatic local-character framework protection, and strict PrimaryPart assignment.
]]--

local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- ====== Configuration ======
local entityspeed = 40 
local killRange = 15 
local entityName = "Common Sense"
local assetId = "rbxassetid://136276859671592"

print("[Overkill] Starting script synced to Room 50 structure...")

-- ====== Setup Model ======
local function LoadEntity()
    local success, objects = pcall(function()
        return game:GetObjects(assetId)
    end)
    
    local model
    if success and objects and objects[1] then
        model = objects[1]
    else
        warn("[Overkill] Model failed to load via GetObjects. Creating fallback red block.")
        model = Instance.new("Model")
        
        local part = Instance.new("Part")
        part.Name = "HumanoidRootPart"
        part.Size = Vector3.new(4, 6, 4)
        part.Color = Color3.fromRGB(255, 0, 0)
        part.Material = Enum.Material.Neon
        part.Parent = model
    end
    
    -- FIX: Manually locate and assign PrimaryPart so the Crucifix Distance Engine doesn't break!
    local hrp = model:FindFirstChild("HumanoidRootPart") or model:FindFirstChildWhichIsA("BasePart")
    if hrp then
        model.PrimaryPart = hrp
        print("[Overkill] Successfully bound PrimaryPart to: " .. hrp.Name)
    else
        warn("[Overkill] Warning: No valid RootPart found to map as PrimaryPart!")
    end
    
    model.Name = entityName
    model.Parent = workspace
    return model
end

local entity = LoadEntity()
if not entity then return end

-- ====== Exact Attribute Formatting ======
entity:SetAttribute('IsCustomEntity', true)
entity:SetAttribute('NoAI', false)

for _, v in ipairs(entity:GetDescendants()) do
    if v:IsA("BasePart") then
        v.Anchored = true
        v.CanCollide = false
    end
end

-- ====== Movement Core ======
function EntityMoveTo(targetCFrame)
    if not entity or not entity.Parent then return end
    local reached = false
    local connection
    
    connection = RunService.Stepped:Connect(function(_, step)
        if not entity or not entity.Parent or entity:GetAttribute("NoAI") == true then 
            if connection then connection:Disconnect() end
            reached = true 
            return 
        end
        
        local pivot = entity:GetPivot()
        local difference = (targetCFrame.Position - pivot.Position)
        
        if difference.Magnitude > 0.5 then
            local unit = difference.Unit
            local moveAmount = math.min(step * entityspeed, difference.Magnitude)
            local newPosition = pivot.Position + (unit * moveAmount)
            
            entity:PivotTo(CFrame.new(newPosition, newPosition + unit))
        else
            if connection then connection:Disconnect() end
            reached = true
        end
    end)
    
    local start = tick()
    repeat RunService.Stepped:Wait() until reached or (tick() - start > 15) or (entity and entity:GetAttribute("NoAI") == true)
    if connection then connection:Disconnect() end
end

-- ====== Helper: Find Room 50 Model ======
local function getRoom50()
    local currentRooms = workspace:FindFirstChild("CurrentRooms")
    if currentRooms and currentRooms:FindFirstChild("50") then
        return currentRooms["50"]
    elseif workspace:FindFirstChild("50") then
        return workspace["50"]
    end
    return nil
end

-- ====== Deep Light Shatter Logic ======
local function shatterRoomLights(room)
    if not room then return end
    print("[Overkill] Deep shattering room lights for: " .. room.Name)
    
    pcall(function()
        local soundCount = 3
        for i = 1, soundCount do
            task.spawn(function()
                if i > 1 then task.wait(math.random(2, 8) / 100) end
                
                local breakSound = Instance.new("Sound")
                breakSound.SoundId = "rbxassetid://8828938165"
                breakSound.Volume = 0.5
                breakSound.Pitch = math.random(90, 110) / 100 
                breakSound.Parent = workspace
                breakSound:Play()
                
                task.delay(2, function()
                    if breakSound then
                        breakSound:Stop()
                        breakSound:Destroy()
                    end
                end)
            end)
        end

        local useEvent = game.ReplicatedStorage:FindFirstChild("EntityInfo") 
            and game.ReplicatedStorage.EntityInfo:FindFirstChild("UseEventModule")
        if useEvent and firesignal then
            firesignal(useEvent.OnClientEvent, 'shatter', room)
        end

        for _, v in ipairs(room:GetDescendants()) do
            if v:IsA("Light") or v:IsA("PointLight") or v:IsA("SpotLight") or v:IsA("SurfaceLight") then
                v.Enabled = false
            end
            if v:IsA("BasePart") then
                if v.Name == "Glow" or v.Name == "Neon" or v.Name == "LightFixture" or v.Material == Enum.Material.Neon then
                    v.Material = Enum.Material.Glass
                    v.Color = Color3.fromRGB(40, 40, 40)
                end
            end
        end
    end)
end

-- ====== Spawn Logic ======
local function spawnAtExit()
    local room50 = getRoom50()
    if room50 then
        local spawnTarget = room50:FindFirstChild("Door") or room50:FindFirstChild("RoomStart") or room50:FindFirstChild("RoomEnd")
        if spawnTarget then
            print("[Overkill] Room 50 structure located. Spawning at: " .. spawnTarget.Name)
            shatterRoomLights(room50)
            
            if spawnTarget:IsA("Model") then
                entity:PivotTo(spawnTarget:GetPivot() + Vector3.new(0, 5, 0))
            else
                entity:PivotTo(spawnTarget.CFrame + Vector3.new(0, 5, 0))
            end
            return
        end
    end
    
    print("[Overkill] Room 50 structure not found. Using absolute position backup.")
    entity:PivotTo(CFrame.new(841.8, 10, -468.3))
end

spawnAtExit()

-- ====== Kill Logic ======
local isDead = false
task.spawn(function()
    while entity and entity.Parent do
        RunService.Heartbeat:Wait()
        
        if entity:GetAttribute("NoAI") == true or entity:GetAttribute("GoingToHell") == true then
            continue
        end
        
        local character = LocalPlayer.Character
        if character and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Humanoid") and not isDead then
            
            -- Tool check safety
            local activeTool = character:FindFirstChildOfClass("Tool")
            if activeTool and string.find(string.lower(activeTool.Name), "crucifix") then
                continue
            end
            
            local root = character.HumanoidRootPart
            local distance = (entity:GetPivot().Position - root.Position).Magnitude
            
            if distance < killRange and character:GetAttribute("Hiding") ~= true then
                isDead = true
                character.Humanoid.Health = 0
                print("[Overkill] Eliminated the player!")
                task.delay(5, function() isDead = false end)
            end
        end
    end
end)

-- ====== Pathing Logic via Room 50 Folder ======
local visitedNodes = {}

local function patrol()
    local room50 = getRoom50()
    local pathFolder = room50 and room50:FindFirstChild("Nodes")
    
    if not pathFolder then
        pathFolder = workspace:FindFirstChild("Nodes", true)
    end
    
    if not pathFolder then
        task.wait(1)
        return
    end
    
    local nodes = {}
    for _, child in ipairs(pathFolder:GetChildren()) do
        if child:IsA("BasePart") then
            table.insert(nodes, child)
        end
    end
    
    if #nodes == 0 then
        task.wait(1)
        return
    end
    
    local entityPos = entity:GetPivot().Position
    local closestNode = nil
    local shortestDistance = math.huge
    
    for _, node in ipairs(nodes) do
        if not visitedNodes[node] then
            local dist = (node.Position - entityPos).Magnitude
            if dist < shortestDistance then
                shortestDistance = dist
                closestNode = node
            end
        end
    end
    
    if not closestNode then
        table.clear(visitedNodes)
        return
    end
    
    visitedNodes[closestNode] = true
    EntityMoveTo(closestNode.CFrame + Vector3.new(0, 4, 0))
end

-- ====== Main Loop ======
task.spawn(function()
    print("[Overkill] Starting proximity patrol loop.")
    while entity and entity.Parent do
        if entity:GetAttribute("NoAI") == true then 
            task.wait(0.5)
            continue 
        end
        patrol()
        task.wait(0.1)
    end
end)

-- ====== Hand-off to Crucifix Clone Engine ======
script.Parent = entity

entity.AncestryChanged:Connect(function(_, parent)
    if parent == nil then
        task.delay(0.02, function()
            local fakeEntity = workspace:FindFirstChild("Fake" .. entityName)
            if fakeEntity and not fakeEntity:FindFirstChild(script.Name) then
                print("[Overkill] Handing script brains over to the Crucifix Fake clone...")
                local scriptClone = script:Clone()
                scriptClone.Parent = fakeEntity
                fakeEntity:SetAttribute("NoAI", true) 
                scriptClone.Disabled = false
            end
        end)
    end
end)

-- Cleanup on Room Change
task.spawn(function()
    local repStorage = game:GetService("ReplicatedStorage")
    local gameData = repStorage:WaitForChild("GameData", 5)
    if gameData then
        local latestRoom = gameData:WaitForChild("LatestRoom", 5)
        if latestRoom then
            latestRoom.Changed:Connect(function()
                if entity then entity:Destroy() end
            end)
        end
    end
end)
