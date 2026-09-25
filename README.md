local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

--==================================================
-- SETTINGS
--==================================================

local Settings = {
	AutoSteal = false,
	TeleportEgg = false,
	AutoTreadmill = false,
	AutoPlaceEgg = false,
	AutoHatch = false,
	AutoUpgradePen = false,
	AutoUpgradeTreadmill = false,
	AutoTrials = false,
	AutoEvent = false,
	AutoDrScrambled = false,
	AutoBuyShop = false,
	AutoFuse = false,
	VisualRarities = false,
	Webhook = false
}

--==================================================
-- REMOTE
--==================================================

local Remote = ReplicatedStorage:FindFirstChild("AutomationEvent")

if not Remote then
	Remote = Instance.new("RemoteEvent")
	Remote.Name = "AutomationEvent"
	Remote.Parent = ReplicatedStorage
end

--==================================================
-- GUI
--==================================================

local gui = Instance.new("ScreenGui")
gui.Name = "EggAutomation"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 300, 0, 560)
main.Position = UDim2.new(0, 20, 0.5, -280)
main.BackgroundColor3 = Color3.fromRGB(25,25,25)
main.BorderSizePixel = 0
main.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0,12)
corner.Parent = main

--==================================================
-- TITLE
--==================================================

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,0,0,45)
title.BackgroundTransparency = 1
title.Text = "🥚 STEAL AN EGG"
title.TextColor3 = Color3.new(1,1,1)
title.TextSize = 21
title.Font = Enum.Font.GothamBold
title.Parent = main

--==================================================
-- SCROLLING FRAME
--==================================================

local scroll = Instance.new("ScrollingFrame")
scroll.Position = UDim2.new(0,5,0,50)
scroll.Size = UDim2.new(1,-10,1,-55)
scroll.BackgroundTransparency = 1
scroll.BorderSizePixel = 0
scroll.ScrollBarThickness = 5
scroll.CanvasSize = UDim2.new(0,0,0,0)
scroll.Parent = main

local layout = Instance.new("UIListLayout")
layout.Padding = UDim.new(0,6)
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
layout.Parent = scroll

--==================================================
-- FEATURES
--==================================================

local Features = {
	{"Auto Steal Egg","AutoSteal"},
	{"Teleport to Egg","TeleportEgg"},
	{"Auto Treadmill","AutoTreadmill"},
	{"Auto Place Egg","AutoPlaceEgg"},
	{"Auto Hatch Egg","AutoHatch"},
	{"Auto Upgrade Pen","AutoUpgradePen"},
	{"Auto Upgrade Treadmill","AutoUpgradeTreadmill"},
	{"Auto Trials","AutoTrials"},
	{"Auto Event","AutoEvent"},
	{"Auto Dr Scrambled","AutoDrScrambled"},
	{"Auto Buy Shop","AutoBuyShop"},
	{"Auto Fuse","AutoFuse"},
	{"Visual Rarities","VisualRarities"},
	{"Webhook","Webhook"}
}

--==================================================
-- BUTTON CREATOR
--==================================================

local Buttons = {}

local function createButton(displayName, settingName)

	local button = Instance.new("TextButton")

	button.Size = UDim2.new(1,-10,0,34)

	button.BackgroundColor3 =
		Color3.fromRGB(55,55,55)

	button.TextColor3 =
		Color3.fromRGB(255,255,255)

	button.TextSize = 14

	button.Font =
		Enum.Font.GothamSemibold

	button.Text =
		"OFF  |  "..displayName

	button.AutoButtonColor = true

	button.Parent = scroll

	local c = Instance.new("UICorner")
	c.CornerRadius = UDim.new(0,7)
	c.Parent = button

	Buttons[settingName] = button

	button.MouseButton1Click:Connect(function()

		Settings[settingName] =
			not Settings[settingName]

		if Settings[settingName] then

			button.Text =
				"ON   |  "..displayName

			button.BackgroundColor3 =
				Color3.fromRGB(35,150,70)

		else

			button.Text =
				"OFF  |  "..displayName

			button.BackgroundColor3 =
				Color3.fromRGB(55,55,55)

		end

		Remote:FireServer(
			settingName,
			Settings[settingName]
		)

	end)
end

for _, feature in ipairs(Features) do
	createButton(feature[1],feature[2])
end

--==================================================
-- UPDATE SCROLL SIZE
--==================================================

layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()

	scroll.CanvasSize =
		UDim2.new(
			0,
			0,
			0,
			layout.AbsoluteContentSize.Y + 10
		)

end)

--==================================================
-- AUTOMATION LOOP
--==================================================

task.spawn(function()

	while task.wait(0.5) do

		------------------------------------------------
		-- AUTO STEAL
		------------------------------------------------

		if Settings.AutoSteal then

			Remote:FireServer(
				"AutoStealEgg"
			)

		end

		------------------------------------------------
		-- TELEPORT
		------------------------------------------------

		if Settings.TeleportEgg then

			Remote:FireServer(
				"TeleportToEgg"
			)

		end

		------------------------------------------------
		-- TREADMILL
		------------------------------------------------

		if Settings.AutoTreadmill then

			Remote:FireServer(
				"UseTreadmill"
			)

		end

		------------------------------------------------
		-- PLACE EGG
		------------------------------------------------

		if Settings.AutoPlaceEgg then

			Remote:FireServer(
				"PlaceEgg"
			)

		end

		------------------------------------------------
		-- HATCH
		------------------------------------------------

		if Settings.AutoHatch then

			Remote:FireServer(
				"HatchEgg"
			)

		end

		------------------------------------------------
		-- PEN UPGRADE
		------------------------------------------------

		if Settings.AutoUpgradePen then

			Remote:FireServer(
				"UpgradePen"
			)

		end

		------------------------------------------------
		-- TREADMILL UPGRADE
		------------------------------------------------

		if Settings.AutoUpgradeTreadmill then

			Remote:FireServer(
				"UpgradeTreadmill"
			)

		end

		------------------------------------------------
		-- TRIALS
		------------------------------------------------

		if Settings.AutoTrials then

			Remote:FireServer(
				"Trials"
			)

		end

		------------------------------------------------
		-- EVENT
		------------------------------------------------

		if Settings.AutoEvent then

			Remote:FireServer(
				"Event"
			)

		end

		------------------------------------------------
		-- DR SCRAMBLED
		------------------------------------------------

		if Settings.AutoDrScrambled then

			Remote:FireServer(
				"DrScrambled"
			)

		end

		------------------------------------------------
		-- SHOP
		------------------------------------------------

		if Settings.AutoBuyShop then

			Remote:FireServer(
				"BuyShop"
			)

		end

		------------------------------------------------
		-- FUSE
		------------------------------------------------

		if Settings.AutoFuse then

			Remote:FireServer(
				"Fuse"
			)

		end

		------------------------------------------------
		-- WEBHOOK
		------------------------------------------------

		if Settings.Webhook then

			Remote:FireServer(
				"Webhook"
			)

		end

	end

end)

--==================================================
-- VISUAL RARITY SYSTEM
--==================================================

local function addRarityVisual(object)

	if not Settings.VisualRarities then
		return
	end

	if not object:IsA("Model") then
		return
	end

	local rarity =
		object:GetAttribute("Rarity")

	if not rarity then
		return
	end

	if object:FindFirstChild("RarityDisplay") then
		return
	end

	local part =
		object.PrimaryPart
		or object:FindFirstChildWhichIsA("BasePart")

	if not part then
		return
	end

	local billboard =
		Instance.new("BillboardGui")

	billboard.Name =
		"RarityDisplay"

	billboard.Size =
		UDim2.new(0,120,0,30)

	billboard.StudsOffset =
		Vector3.new(0,3,0)

	billboard.AlwaysOnTop =
		true

	billboard.Parent =
		part

	local text =
		Instance.new("TextLabel")

	text.Size =
		UDim2.new(1,0,1,0)

	text.BackgroundTransparency =
		1

	text.Text =
		tostring(rarity)

	text.TextColor3 =
		Color3.new(1,1,1)

	text.TextStrokeTransparency =
		0

	text.TextScaled =
		true

	text.Font =
		Enum.Font.GothamBold

	text.Parent =
		billboard
end

--==================================================
-- WATCH WORKSPACE
--==================================================

workspace.DescendantAdded:Connect(function(object)

	if Settings.VisualRarities then
		task.wait()
		addRarityVisual(object)
	end

end)

--==================================================
-- CLOSE / OPEN WITH RIGHT SHIFT
--==================================================

local UIS = game:GetService("UserInputService")

UIS.InputBegan:Connect(function(input, processed)

	if processed then
		return
	end

	if input.KeyCode == Enum.KeyCode.RightShift then

		main.Visible =
			not main.Visible

	end

end)

print("🥚 Egg Automation GUI loaded!")
