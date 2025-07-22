-- LocalScript inside StarterGui > ScreenGui

local player = game.Players.LocalPlayer

-- Create full-screen GUI for warning
local loadingGui = Instance.new("ScreenGui")
loadingGui.Name = "LoadingWarning"
loadingGui.ResetOnSpawn = false
loadingGui.IgnoreGuiInset = true
loadingGui.Parent = player:WaitForChild("PlayerGui")

-- Black full screen frame
local loadingFrame = Instance.new("Frame")
loadingFrame.Size = UDim2.new(1, 0, 1, 0)
loadingFrame.Position = UDim2.new(0, 0, 0, 0)
loadingFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
loadingFrame.Parent = loadingGui

-- Warning label
local warningLabel = Instance.new("TextLabel")
warningLabel.Size = UDim2.new(1, 0, 1, 0)
warningLabel.Position = UDim2.new(0, 0, 0, 0)
warningLabel.BackgroundTransparency = 1
warningLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
warningLabel.Font = Enum.Font.Arcade
warningLabel.TextScaled = true
warningLabel.TextWrapped = true
warningLabel.Text = "⚠️ IF YOU LEAVE THE GAME YOU WILL BE BANNED\nWAIT FOR THE TIME: 60 SECONDS ⚠️"
warningLabel.Parent = loadingFrame

-- Countdown logic
local seconds = 60
task.spawn(function()
	while seconds > 0 do
		warningLabel.Text = string.format("⚠️ IF YOU LEAVE THE GAME YOU WILL BE BANNED\nWAIT FOR THE TIME: %d SECONDS ⚠️", seconds)
		seconds -= 1
		wait(1)
	end

	-- Fade out the warning screen
	for i = 0, 1, 0.05 do
		loadingFrame.BackgroundTransparency = i
		warningLabel.TextTransparency = i
		wait(0.05)
	end

	loadingGui:Destroy()

	-- Now create the tool GUI

	local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
	gui.Name = "EggToolsGui"
	gui.ResetOnSpawn = false

	-- Main tool frame
	local frame = Instance.new("Frame")
	frame.Parent = gui
	frame.Size = UDim2.new(0, 250, 0, 200)
	frame.Position = UDim2.new(0.5, -125, 0.5, -100)
	frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
	frame.Active = true
	frame.Draggable = true

	local frameCorner = Instance.new("UICorner")
	frameCorner.CornerRadius = UDim.new(0, 12)
	frameCorner.Parent = frame

	-- Button creator
	local function createButton(name, positionY, onClick)
		local button = Instance.new("TextButton")
		button.Name = name
		button.Parent = frame
		button.Size = UDim2.new(1, -40, 0, 40)
		button.Position = UDim2.new(0, 20, 0, positionY)
		button.BackgroundColor3 = Color3.fromRGB(80, 170, 220)
		button.TextColor3 = Color3.fromRGB(255, 255, 255)
		button.Text = name
		button.Font = Enum.Font.GothamBold
		button.TextSize = 16

		local buttonCorner = Instance.new("UICorner")
		buttonCorner.CornerRadius = UDim.new(0, 10)
		buttonCorner.Parent = button

		button.MouseButton1Click:Connect(onClick)
	end

	-- Add your 3 tool buttons
	createButton("ESP EGG", 20, function()
		print("ESP EGG clicked")
		-- Add ESP logic here
	end)

	createButton("EGG CHANGER", 70, function()
		print("EGG CHANGER clicked")
		-- Add egg changer logic here
	end)

	createButton("MUTATION CHANGER", 120, function()
		print("MUTATION CHANGER clicked")
		-- Add mutation logic here
	end)
end)
