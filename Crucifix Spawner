local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
local MainUI = PlayerGui:WaitForChild("MainUI")
local MainGame = require(MainUI:WaitForChild("Initiator"):WaitForChild("Main_Game"))
local CurrentCamera = workspace.CurrentCamera

local function GetEntityColor(entityName)
    if entityName == "Silence" then
        return Color3.fromRGB(255, 255, 255)
    elseif entityName == "WH1T3" then
        return Color3.fromRGB(0, 0, 255)
    elseif entityName == "Smiler" then
        return Color3.fromRGB(255, 0, 0)
    elseif entityName == "HungerMoving" then
        return Color3.fromRGB(59, 6, 6)
    elseif entityName == "Common Sense" then
        return Color3.fromRGB(117, 117, 117)
    elseif entityName == "Dimensional Eye" then
        return Color3.fromRGB(31, 29, 43)
    elseif entityName == "Blink" then
        return Color3.fromRGB(216, 0, 240)
    else
        return Color3.fromRGB(255, 255, 255)
    end
end

local u1 = ''
local u2 = _G.OnAnything or false

local customSoundFile = "custom_crucifix_sound.mp3"
if not isfile(customSoundFile) then
    writefile(customSoundFile, game:HttpGet("https://github.com/reboundplayz/Doors-Fixed-Modes/raw/refs/heads/main/0527.mp3"))
end
local CUSTOM_SOUND_ASSET = getcustomasset(customSoundFile)

local function ColorRepentanceModel(model, color)
    if not model then return end
    for _, desc in ipairs(model:GetDescendants()) do
        if desc:IsA("BasePart") then
            desc.Color = color
        elseif desc:IsA("Light") then
            desc.Color = color
        elseif desc:IsA("ParticleEmitter") then
            desc.Color = ColorSequence.new({
                ColorSequenceKeypoint.new(0, color),
                ColorSequenceKeypoint.new(1, color)
            })
        elseif desc:IsA("Beam") then
            desc.Color = ColorSequence.new({
                ColorSequenceKeypoint.new(0, color),
                ColorSequenceKeypoint.new(1, color)
            })
        end
    end
end

local originalRightC1 = CFrame.new(0, 0.5, 0) * CFrame.Angles(0, 0, 0)
local originalLeftC1 = CFrame.new(0, 0.5, 0) * CFrame.Angles(0, 0, 0)
local jointsSaved = false

local function ResetCharacterArms(character)
    if not character then return end
    local rArm = character:FindFirstChild('R_Arm') or character:FindFirstChild('RightUpperArm')
    local lArm = character:FindFirstChild('L_Arm') or character:FindFirstChild('LeftUpperArm')
    
    if rArm and rArm:FindFirstChild("RightShoulder") and jointsSaved then
        rArm.RightShoulder.C1 = originalRightC1
    end
    if lArm and lArm:FindFirstChild("LeftShoulder") and jointsSaved then
        lArm.LeftShoulder.C1 = originalLeftC1
    end
    if rArm then rArm.Name = 'RightUpperArm' end
    if lArm then lArm.Name = 'LeftUpperArm' end
end

local v8 = require(game.ReplicatedStorage.CameraShaker)
local u11 = v8.new(Enum.RenderPriority.Camera.Value, function(p10)
    CurrentCamera.CFrame = CurrentCamera.CFrame * p10
end)

local function InitializeCrucifixLogic(_Crucifix, _Repentance)
    local u3 = _G.Uses or 1
    local u4 = _G.Range or 30
    local u5 = _G.Fail or false
    local u6 = false
    local u7 = nil
    local _Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()

    local function u25()
        local _huge = math.huge
        local v17, v18, v19 = ipairs(workspace:GetDescendants())
        local v20 = nil
        local v21 = nil

        while true do
            local v22
            v19, v22 = v17(v18, v19)
            if v19 == nil then break end
            if v22:IsA('Model') then
                local _IsCustomEntity = v22:GetAttribute('IsCustomEntity')
                local v24

                if u2 ~= true or v22.Name ~= u1 then
                    v24 = _huge
                else
                    v24 = LocalPlayer:DistanceFromCharacter(v22.PrimaryPart.Position)
                    if v24 < _huge then
                        v20 = v22
                        v21 = true
                    else
                        v24 = _huge
                    end
                end
                if _IsCustomEntity then
                    _huge = LocalPlayer:DistanceFromCharacter(v22.PrimaryPart.Position)
                    if _huge < v24 then
                        v20 = v22
                        v21 = false
                    else
                        _huge = v24
                    end
                end
            end
        end
        return v20, _huge, v21
    end

    local function HellModel(p31, _)
        local CUSTOM_REPENTANCE_COLOR = GetEntityColor(p31.Name)
        local u32

        if u5 then
            u32 = p31
        else
            u32 = p31:Clone()
            u32.Name = 'Fake' .. p31.Name
            u32.Parent = workspace
            p31:Destroy()
        end

        for _, obj in ipairs(u32:GetDescendants()) do
            if obj:IsA("Sound") then
                obj:Stop()
                obj.Volume = 0
            end
        end

        local v33 = u32.PrimaryPart or u32:FindFirstChildOfClass('Part')
        local v34 = RaycastParams.new()
        v34.FilterType = Enum.RaycastFilterType.Blacklist
        v34.FilterDescendantsInstances = {_Character, u32}

        local v35 = workspace:Raycast(v33.Position, Vector3.new(0, -1, 0) * 20, v34)
        local u36 = _Repentance:Clone()

        ColorRepentanceModel(u36, CUSTOM_REPENTANCE_COLOR)
        u36.Parent = workspace
        local _Pentagram = u36.Pentagram

        if v35 then
            local _Part = Instance.new('Part')
            _Part.Anchored = true
            _Part.Position = v35.Position + Vector3.new(0, 1, 0)
            u36:PivotTo(_Part.CFrame * CFrame.new(0, -0.5, 0) * CFrame.Angles(0, 0, 0))
            _Part:Destroy()
        end

        local v39, v40, v41 = pairs(u32:GetDescendants())
        while true do
            local v42
            v41, v42 = v39(v40, v41)
            if v41 == nil then break end
            if v42:IsA('BasePart') then v42.Anchored = true end
        end

        local hellCrucifixGlow = u36.Crucifix:FindFirstChild("Glow") or u36.Crucifix:FindFirstChild("Handle") or u36.Crucifix:FindFirstChildOfClass("BasePart")

        if hellCrucifixGlow then
            hellCrucifixGlow.Anchored = false
            if hellCrucifixGlow:FindFirstChild("BodyAngularVelocity") then
                hellCrucifixGlow.BodyAngularVelocity.AngularVelocity = Vector3.new(0, 0, 0)
            end
            if hellCrucifixGlow:FindFirstChild("BodyPosition") then
                local v43 = _Character.HumanoidRootPart.CFrame * CFrame.new(0, 3.5, -6)
                hellCrucifixGlow.BodyPosition.Position = v43.Position
            end
        end

        u36.Crucifix:PivotTo(LastCFrame)

        local customCrucifixSound = Instance.new("Sound")
        customCrucifixSound.Name = "GlobalCustomCrucifixSound"
        customCrucifixSound.SoundId = CUSTOM_SOUND_ASSET
        customCrucifixSound.Volume = 7 
        customCrucifixSound.Parent = game:GetService("CoreGui") or LocalPlayer:FindFirstChildOfClass("PlayerGui")
        customCrucifixSound:Play()
        
        customCrucifixSound.Ended:Connect(function()
            customCrucifixSound:Destroy()
        end)

        u11:Start()
        u11:ShakeOnce(10, 15, 4, 5)

        local function u67(p44)
            task.wait(1.5)
            if u5 then
                TweenService:Create(u36.Entity, TweenInfo.new(1.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Position = u36.Entity.Position + Vector3.new(0, 3.5, 0)}):Play()
                task.spawn(function()
                    task.wait(1.25)
                    if _Pentagram.Base.LightAttach:FindFirstChild("LightBright") then
                        TweenService:Create(_Pentagram.Base.LightAttach.LightBright, TweenInfo.new(1.25, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {Range = 10, Brightness = 2.5}):Play()
                        task.wait(1.25)
                        TweenService:Create(_Pentagram.Base.LightAttach.LightBright, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Range = 1, Brightness = 0}):Play()
                    end
                end)
                task.wait(2.1)
                task.spawn(function()
                    if hellCrucifixGlow and hellCrucifixGlow:FindFirstChild("ExplodeParticle") then
                        hellCrucifixGlow.ExplodeParticle.Color = ColorSequence.new({ColorSequenceKeypoint.new(0, CUSTOM_REPENTANCE_COLOR), ColorSequenceKeypoint.new(1, CUSTOM_REPENTANCE_COLOR)})
                    end
                    if _Pentagram.Base.LightAttach:FindFirstChild("LightBright") then
                        TweenService:Create(_Pentagram.Base.LightAttach.LightBright, TweenInfo.new(0.25, Enum.EasingStyle.Sine, Enum.EasingDirection.In), {Color = CUSTOM_REPENTANCE_COLOR}):Play()
                    end
                    if hellCrucifixGlow then
                        TweenService:Create(hellCrucifixGlow, TweenInfo.new(0.25, Enum.EasingStyle.Sine, Enum.EasingDirection.In), {Color = CUSTOM_REPENTANCE_COLOR}):Play()
                        if hellCrucifixGlow:FindFirstChild("Light") then
                            TweenService:Create(hellCrucifixGlow.Light, TweenInfo.new(0.25, Enum.EasingStyle.Sine, Enum.EasingDirection.In), {Color = CUSTOM_REPENTANCE_COLOR}):Play()
                        end
                    end
                end)

                local v45 = _Pentagram
                local v46, v47, v48 = pairs(v45:GetChildren())
                while true do
                    local u49
                    v48, u49 = v46(v47, v48)
                    if v48 == nil then break end
                    if u49:IsA('Beam') then
                        task.spawn(function()
                            u49.Color = ColorSequence.new({ColorSequenceKeypoint.new(0, CUSTOM_REPENTANCE_COLOR), ColorSequenceKeypoint.new(1, CUSTOM_REPENTANCE_COLOR)})
                        end)
                    end
                end

                task.wait(3.4)
                local v50 = _Pentagram
                local v51, v52, v53 = pairs(v50:GetChildren())
                while true do
                    local u54
                    v53, u54 = v51(v52, v53)
                    if v53 == nil then break end
                    if u54:IsA('Beam') then
                        task.spawn(function()
                            if u54:GetAttribute('Delay') ~= 0 then task.wait(u54:GetAttribute('Delay')) end
                            TweenService:Create(u54, TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Brightness = 0}):Play()
                        end)
                    end
                end
            else
                TweenService:Create(u36.Entity, TweenInfo.new(1.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Position = u36.Entity.Position + Vector3.new(0, 3.5, 0)}):Play()
                TweenService:Create(p44, TweenInfo.new(1.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Position = p44.Position + Vector3.new(0, 3.5, 0)}):Play()
                task.spawn(function()
                    task.wait(0.5)
                    if _Pentagram.Base.LightAttach:FindFirstChild("LightBright") then
                        TweenService:Create(_Pentagram.Base.LightAttach.LightBright, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {Range = 30, Brightness = 5}):Play()
                        task.wait(1.75)
                        TweenService:Create(_Pentagram.Base.LightAttach.LightBright, TweenInfo.new(4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Range = 1, Brightness = 0}):Play()
                    end
                end)
                task.wait(1.5)
                TweenService:Create(p44, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Position = p44.Position - Vector3.new(0, 50, 0)}):Play()
                TweenService:Create(u36.Entity, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Position = u36.Entity.Position - Vector3.new(0, 50, 0)}):Play()
                task.spawn(function()
                    task.wait(0.5)
                    if hellCrucifixGlow and hellCrucifixGlow:FindFirstChild("Light") then
                        TweenService:Create(hellCrucifixGlow.Light, TweenInfo.new(1.25, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Range = 30, Brightness = 5}):Play()
                    end
                end)
                task.wait(1)

                local v56 = u32
                local v57, v58, v59 = pairs(v56:GetDescendants())
                while true do
                    local v60
                    v59, v60 = v57(v58, v59)
                    if v59 == nil then break end
                    if v60:IsA('Sound') and v60.Name ~= "GlobalCustomCrucifixSound" then
                        TweenService:Create(v60, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Volume = 0}):Play()
                    elseif v60:IsA('Light') then
                        TweenService:Create(v60, TweenInfo.new(3, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Range = 0}):Play()
                    end
                end

                local v61 = _Pentagram
                local v62, v63, v64 = pairs(v61:GetChildren())
                while true do
                    local u65
                    v64, u65 = v62(v63, v64)
                    if v64 == nil then break end
                    if u65.Name == 'BeamFlat' then
                        task.spawn(function()
                            if u65:GetAttribute('Delay') ~= 0 then task.wait(u65:GetAttribute('Delay')) end
                            TweenService:Create(u65, TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Brightness = 0}):Play()
                        end)
                    end
                end
            end
        end

        task.spawn(function()
            TweenService:Create(_Pentagram.Circle, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Position = _Pentagram.Circle.Position - Vector3.new(0, 7.5, 0)}):Play()
            task.wait(1)
            _Pentagram.Circle.Anchored = false
            if hellCrucifixGlow and hellCrucifixGlow:FindFirstChild("BodyAngularVelocity") then
                TweenService:Create(hellCrucifixGlow.BodyAngularVelocity, TweenInfo.new(2.5, Enum.EasingStyle.Sine, Enum.EasingDirection.In), {AngularVelocity = Vector3.new(0, 30, 0)}):Play()
            end
            task.wait(4)
            if hellCrucifixGlow and hellCrucifixGlow:FindFirstChild("BodyAngularVelocity") then
                TweenService:Create(hellCrucifixGlow.BodyAngularVelocity, TweenInfo.new(1.5, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {AngularVelocity = Vector3.new(0, 0, 0)}):Play()
            end
        end)

        local v68, v69, v70 = pairs(u32:GetDescendants())
        while true do
            local u71
            v70, u71 = v68(v69, v70)
            if v70 == nil then break end
            if u71:IsA('BasePart') then
                task.spawn(function() u67(u71) end)
            end
        end

        task.spawn(function()
            task.wait(6.5)
            if hellCrucifixGlow then
                if hellCrucifixGlow:FindFirstChild("Light") then
                    hellCrucifixGlow.Light.Enabled = false
                    TweenService:Create(hellCrucifixGlow.Light, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Brightness = 0, Range = 1}):Play()
                end
                task.wait(3)
                TweenService:Create(hellCrucifixGlow, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Size = hellCrucifixGlow.Size * 3.5}):Play()
                TweenService:Create(hellCrucifixGlow, TweenInfo.new(1.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Transparency = 1}):Play()
                if hellCrucifixGlow:FindFirstChild("ExplodeParticle") then
                    hellCrucifixGlow.ExplodeParticle:Emit(50)
                end
            end
            u11:ShakeOnce(3, 10, 0.7, 0.5)
        end)

        task.wait(u5 and 11.5 or 9)
        task.spawn(function()
            u36:Destroy()
            if not u5 or p31:GetAttribute('IsCustomEntity') == true then
                u32:Destroy()
            end
            ResetCharacterArms(_Character)
        end)
    end

    _Crucifix.Equipped:Connect(function()
        local v71 = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
        local _Humanoid = v71:WaitForChild('Humanoid')
        local _RightUpperArm = v71:WaitForChild('RightUpperArm', 3)
        local _LeftUpperArm = v71:WaitForChild('LeftUpperArm', 3)

        if _RightUpperArm and _LeftUpperArm then
            if not jointsSaved and _RightUpperArm:FindFirstChild("RightShoulder") and _LeftUpperArm:FindFirstChild("LeftShoulder") then
                originalRightC1 = _RightUpperArm.RightShoulder.C1
                originalLeftC1 = _LeftUpperArm.LeftShoulder.C1
                jointsSaved = true
            end

            _RightUpperArm.Name = 'R_Arm'
            _LeftUpperArm.Name = 'L_Arm'
            if _RightUpperArm:FindFirstChild("RightShoulder") and _LeftUpperArm:FindFirstChild("LeftShoulder") then
                _RightUpperArm.RightShoulder.C1 = _RightUpperArm.RightShoulder.C1 * CFrame.Angles(math.rad(-90), math.rad(-15), 0)
                _LeftUpperArm.LeftShoulder.C1 = _LeftUpperArm.LeftShoulder.C1 * CFrame.new(-0.2, -0.3, -0.5) * CFrame.Angles(math.rad(-125), math.rad(25), math.rad(25))
            end
        end

        for _, track in ipairs(_Humanoid:GetPlayingAnimationTracks()) do
            track:Stop()
        end

        LocalPlayer:SetAttribute('Hidden', true)
        u6 = true

        u7 = RunService.Stepped:Connect(function()
            if u6 == true then
                local v29, _, v30 = u25()
                if v29 ~= nil and v29:GetAttribute('GoingToHell') ~= true and LocalPlayer:DistanceFromCharacter(v29.PrimaryPart.Position) <= u4 then
                    LastCFrame = v71.RightHand.CFrame * CFrame.Angles(math.rad(-90), 0, 0)
                    u11:Start()
                    u11:ShakeOnce(10, 30, 0.7, 0.5)

                    if u3 ~= 1 then
                        _Crucifix.Parent = LocalPlayer.Backpack
                        u6 = false
                        u3 = u3 - 1
                    else
                        u6 = false
                        _Crucifix:Destroy()
                    end

                    u1 = ''
                    v29:SetAttribute('GoingToHell', true)
                    HellModel(v29, v30)
                end
            end
        end)
    end)

    _Crucifix.Unequipped:Connect(function()
        LocalPlayer:SetAttribute('Hidden', false)
        u6 = false
        if u7 then u7:Disconnect() u7 = nil end
        ResetCharacterArms(LocalPlayer.Character)
    end)
end

local function FindTableInCurrentRoom()
    local currentRooms = workspace:FindFirstChild("CurrentRooms")
    if not currentRooms then return nil end

    local currentRoomValue = LocalPlayer:GetAttribute("CurrentRoom")
    if not currentRoomValue then return nil end

    local roomModel = currentRooms:FindFirstChild(tostring(currentRoomValue))
    if not roomModel then return nil end

    for _, instance in ipairs(roomModel:GetDescendants()) do
        if instance:IsA("BasePart") then
            local nameLower = string.lower(instance.Name)
            if string.find(nameLower, "table") or string.find(nameLower, "desk") or string.find(nameLower, "counter") then
                local topY = instance.Position.Y + (instance.Size.Y / 2)
                return Vector3.new(instance.Position.X, topY, instance.Position.Z)
            end
        end
    end

    return nil
end

local function spawncruxy()
    local char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    local hrp = char:WaitForChild("HumanoidRootPart")
    
    local targetPos = FindTableInCurrentRoom()
    local spawnedOnTable = true
    
    if not targetPos then
        targetPos = hrp.Position + Vector3.new(0, -1, -4)
        spawnedOnTable = false
    end

    local masterObjects = game:GetObjects('rbxassetid://12849323184')[1]
    local baseCrucifix = masterObjects.Crucifix
    local baseRepentance = masterObjects.Repentance

    local targetGlowPart = baseCrucifix:FindFirstChild("Glow") or baseCrucifix:FindFirstChild("Handle") or baseCrucifix:FindFirstChildOfClass("BasePart")
    if not targetGlowPart then return end

    local pickupWorldModel = targetGlowPart:Clone()
    pickupWorldModel.Parent = game.Workspace
    pickupWorldModel.Name = 'Cruxy'
    pickupWorldModel.Position = targetPos
    pickupWorldModel.Anchored = true

    local randomRotationAngle = math.random(-180, 180)
    pickupWorldModel.CFrame = CFrame.new(pickupWorldModel.Position) * CFrame.Angles(math.rad(0), math.rad(randomRotationAngle), math.rad(90))

    local _PointLight = Instance.new('PointLight')
    _PointLight.Brightness = 10000
    _PointLight.Parent = pickupWorldModel
    _PointLight.Enabled = true
    _PointLight.Color = Color3.fromRGB(255, 0, 0)
    _PointLight.Range = 1

    local _PointLight2 = Instance.new('PointLight')
    _PointLight2.Brightness = 3
    _PointLight2.Parent = pickupWorldModel
    _PointLight2.Enabled = true
    _PointLight2.Color = Color3.fromRGB(0, 255, 255)
    _PointLight2.Range = 10

    local _ProximityPrompt = pickupWorldModel:FindFirstChildOfClass('ProximityPrompt') or baseCrucifix:FindFirstChildOfClass('ProximityPrompt')
    if not _ProximityPrompt then
        _ProximityPrompt = Instance.new('ProximityPrompt')
        _ProximityPrompt.Parent = pickupWorldModel
    else
        _ProximityPrompt = _ProximityPrompt:Clone()
        _ProximityPrompt.Parent = pickupWorldModel
    end
    
    _ProximityPrompt.Name = 'prompty'
    _ProximityPrompt.MaxActivationDistance = 5
    _ProximityPrompt.ObjectText = 'Custom'
    _ProximityPrompt.RequiresLineOfSight = true

    _ProximityPrompt.Triggered:Connect(function()
        pickupWorldModel:Destroy()

        local activeTool = baseCrucifix:Clone()
        activeTool.Parent = LocalPlayer.Backpack

        InitializeCrucifixLogic(activeTool, baseRepentance)
        
        MainGame.caption('You grab the crucifix.', true)
        task.wait(3)
        MainGame.caption('It has a text on the back: "Made in China"', true)
        task.wait(3)
        MainGame.caption('It only works with custom entities.', true)
    end)

    if spawnedOnTable then
        print("Crucifix spawned onto a table within your current room!")
    else
        print("No table found inside the current room model. Spawned in front of character fallback.")
    end
end

spawncruxy()
