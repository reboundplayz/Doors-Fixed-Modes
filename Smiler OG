local Creator = loadstring(game:HttpGet("https://pastebin.com/raw/0fSnvfGt"))() 
-- Create entity
local entity = Creator.createEntity({
    CustomName = "Smiler", -- Custom name of your entity
    Model = "https://github.com/reboundplayz/Doors-Fixed-Modes/raw/refs/heads/main/Smiler.rbxm", -- Can be GitHub file or rbxassetid
    Speed = 700, -- Percentage, 100 = default Rush speed
    DelayTime = 12, -- Time before starting cycles (seconds)
    HeightOffset = 0,
    CanKill = true,
    KillRange = 50,
    BreakLights = true,
    BackwardsMovement = false,
    FlickerLights = {
        true, -- Enabled/Disabled
        10, -- Time (seconds)
    },
    Cycles = {
        Min = 10,
        Max = 10,
        WaitTime = 0,
    },
    CamShake = {
        true, -- Enabled/Disabled
        {5, 15, 0.1, 1}, -- Shake values (don't change if you don't know)
        100, -- Shake start distance (from Entity to you)
    },
    Jumpscare = {
        false, -- Enabled/Disabled
        {
            Image1 = "rbxassetid://10483855823", -- Image1 url
            Image2 = "rbxassetid://10483999903", -- Image2 url
            Shake = true,
            Sound1 = {
                10483790459, -- SoundId
                { Volume = 0.5 }, -- Sound properties
            },
            Sound2 = {
                10483837590, -- SoundId
                { Volume = 0.5 }, -- Sound properties
            },
            Flashing = {
                true, -- Enabled/Disabled
                Color3.fromRGB(0, 0, 255), -- Color
            },
            Tease = {
                true, -- Enabled/Disabled
                Min = 4,
                Max = 4,
            },
        },
    },
    CustomDialog = {"I REMEMBER THAT SMILE ...", "It seems like u got access to an entity that isn't released yet.", "Please report to LSplash#1234 and Redibles#7070 if this happens again."}, -- Custom death message
})

-----[[ Advanced ]]-----
entity.Debug.OnEntitySpawned = function(entityTable)
    print("Entity has spawned:", entityTable.Model)
end

entity.Debug.OnEntityDespawned = function(entityTable)
    print("Entity has despawned:", entityTable.Model)
end

entity.Debug.OnEntityStartMoving = function(entityTable)
    print("Entity has started moving:", entityTable.Model)
end

entity.Debug.OnEntityFinishedRebound = function(entityTable)
    print("Entity has finished rebound:", entityTable.Model)
end

entity.Debug.OnEntityEnteredRoom = function(entityTable, room)
    print("Entity:", entityTable.Model, "has entered room:", room)
end

entity.Debug.OnLookAtEntity = function(entityTable)
    print("Player has looked at entity:", entityTable.Model)
end

entity.Debug.OnDeath = function(entityTable)
    warn("Player has died.")
	local Players = game:GetService("Players")
	local TweenService = game:GetService("TweenService")

	local player = Players.LocalPlayer
	local playerGui = player:WaitForChild("PlayerGui")

	-- GUI
	local gui = Instance.new("ScreenGui")
	gui.IgnoreGuiInset = true
	gui.DisplayOrder = 999999
	gui.ResetOnSpawn = false
	gui.Parent = playerGui

	-- FLASH
	local flash = Instance.new("Frame")
	flash.Size = UDim2.new(1,0,1,0)
	flash.BorderSizePixel = 0
	flash.BackgroundColor3 = Color3.new(0,0,0)
	flash.ZIndex = 10
	flash.Parent = gui

	-- IMAGE
	local image = Instance.new("ImageLabel")
	image.AnchorPoint = Vector2.new(0.5, 0.5)
	image.Position = UDim2.new(0.5, 0, 0.5, 0)
	image.Size = UDim2.new(0, 300, 0, 420)
	image.BackgroundTransparency = 1
	image.Image = "rbxassetid://11417375410"
	image.ZIndex = 11
	image.Parent = gui

	-- 🔊 GITHUB SOUND (YOUR ORIGINAL SYSTEM, BUT SAFE)
	local url = "https://github.com/reboundplayz/doors-crazy-mode-stuff/raw/refs/heads/main/Project%20Name%204.mp3"
	local file = "smilerjumpscare.mp3"

	if not isfile(file) then
		writefile(file, game:HttpGet(url))
	end

	local sound = Instance.new("Sound")
	sound.SoundId = getcustomasset(file)
	sound.Volume = 10
	sound.Parent = gui
	task.spawn(function()
		sound:Play()
	end)

	-- ZOOM
	TweenService:Create(
		image,
		TweenInfo.new(1.2, Enum.EasingStyle.Exponential, Enum.EasingDirection.Out),
		{Size = UDim2.new(0, 3500, 0, 3500)}
	):Play()

	-- LOOP (mobile stable)
	task.spawn(function()
		local duration = 1.2
		local start = os.clock()

		while true do
			local t = os.clock() - start
			if t >= duration then break end

			-- FLASH
			if math.random(1,2) == 1 then
				flash.BackgroundColor3 = Color3.fromRGB(255,0,0)
			else
				flash.BackgroundColor3 = Color3.fromRGB(0,0,0)
			end

			-- SHAKE
			image.Rotation = math.random(-5,5)

			local offsetX = math.random(-25,25)
			local offsetY = math.random(-25,25)

			image.Position = UDim2.new(0.5, offsetX, 0.5, offsetY)

			task.wait(0.01)
		end

		gui:Destroy()
	end)
end
------------------------

-- Run the created entity
Creator.runEntity(entity)
