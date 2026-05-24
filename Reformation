if (getgenv().REFO_LOADED) then
	return
end
getgenv().REFO_LOADED = true

local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Loader = {}

local DAHOOD_BLOCKED = {2788229376, 16033173781, 7213786345}

local function handleGame(gameName)
	local placeId = game.PlaceId

	if gameName == "Prison Life" then
		LocalPlayer:Kick("[Reformation.gg] This script does not officially support Prison Life (for now). Please use the Universal option instead. Join our Discord for more information.")
		return
	end

	if gameName == "Hood Games" then
		for _, blockedId in ipairs(DAHOOD_BLOCKED) do
			if placeId == blockedId then
				LocalPlayer:Kick("[Reformation.gg] This script does not support the official Da Hood game. Only Da Hood copies are currently supported. Join our Discord for more information.")
				return
			end
		end
		loadstring(game:HttpGet("https://raw.githubusercontent.com/Pixeluted/adoniscries/main/Source.lua", true))()
		loadstring(game:HttpGet("https://api.getpolsec.com/scripts/hosted/d396426fcee16f4051596ebf43e645a98c4c3b99d0f23ef548bb422228fff775.lua"))()
		return
	end

	if gameName == "Universal" then
		loadstring(game:HttpGet("https://api.getpolsec.com/scripts/hosted/a6ca7910af84d86a8268df087542a8908fbbd4fff3850473f8841f38f066198b.lua"))()
		return
	end
end

local function dragify(Frame)
	local dragToggle, dragInput, dragStart, startPos

	local function updateInput(input)
		local Delta = input.Position - dragStart
		local Position = UDim2.new(
			startPos.X.Scale, startPos.X.Offset + Delta.X,
			startPos.Y.Scale, startPos.Y.Offset + Delta.Y
		)
		TweenService:Create(Frame, TweenInfo.new(0.2), {Position = Position}):Play()
	end

	Frame.InputBegan:Connect(function(input)
		if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch)
			and UIS:GetFocusedTextBox() == nil then
			dragToggle = true
			dragStart = input.Position
			startPos = Frame.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragToggle = false
				end
			end)
		end
	end)

	Frame.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)

	UIS.InputChanged:Connect(function(input)
		if input == dragInput and dragToggle then
			updateInput(input)
		end
	end)
end

function Loader:Create(info)
	local name = info.Name or "Reformation"
	local callback = info.Callback

	if game.CoreGui:FindFirstChild(name) then
		game.CoreGui:FindFirstChild(name):Destroy()
	end

	local ScreenGui = Instance.new("ScreenGui")
	ScreenGui.Name = name
	ScreenGui.Parent = game.CoreGui
	ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	ScreenGui.ResetOnSpawn = false

	local Main = Instance.new("Frame")
	Main.Name = "Main"
	Main.Parent = ScreenGui
	Main.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
	Main.BorderSizePixel = 0
	Main.Position = UDim2.new(0.5, -220, 0.5, -85)
	Main.Size = UDim2.new(0, 440, 0, 170)
	Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 8)

	local Gradient = Instance.new("UIGradient")
	Gradient.Color = ColorSequence.new{
		ColorSequenceKeypoint.new(0, Color3.fromRGB(20, 20, 20)),
		ColorSequenceKeypoint.new(1, Color3.fromRGB(35, 35, 35))
	}
	Gradient.Rotation = 135
	Gradient.Parent = Main

	local Accent = Instance.new("Frame")
	Accent.Parent = Main
	Accent.BackgroundColor3 = Color3.fromRGB(100, 60, 220)
	Accent.BorderSizePixel = 0
	Accent.Size = UDim2.new(1, 0, 0, 2)
	Accent.Position = UDim2.new(0, 0, 0, 0)
	Instance.new("UICorner", Accent).CornerRadius = UDim.new(0, 8)

	local Title = Instance.new("TextLabel")
	Title.Parent = Main
	Title.BackgroundTransparency = 1
	Title.Position = UDim2.new(0, 0, 0, 12)
	Title.Size = UDim2.new(1, 0, 0, 30)
	Title.Font = Enum.Font.GothamBold
	Title.Text = "Reformation Loader"
	Title.TextColor3 = Color3.fromRGB(255, 255, 255)
	Title.TextSize = 17
	Title.TextXAlignment = Enum.TextXAlignment.Center

	local Sub = Instance.new("TextLabel")
	Sub.Parent = Main
	Sub.BackgroundTransparency = 1
	Sub.Position = UDim2.new(0, 0, 0, 40)
	Sub.Size = UDim2.new(1, 0, 0, 18)
	Sub.Font = Enum.Font.Gotham
	Sub.Text = "Select a game to inject"
	Sub.TextColor3 = Color3.fromRGB(140, 140, 140)
	Sub.TextSize = 12
	Sub.TextXAlignment = Enum.TextXAlignment.Center

	local Divider = Instance.new("Frame")
	Divider.Parent = Main
	Divider.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	Divider.BorderSizePixel = 0
	Divider.Position = UDim2.new(0.05, 0, 0, 64)
	Divider.Size = UDim2.new(0.9, 0, 0, 1)

	local ButtonContainer = Instance.new("Frame")
	ButtonContainer.Parent = Main
	ButtonContainer.BackgroundTransparency = 1
	ButtonContainer.Position = UDim2.new(0, 16, 0, 78)
	ButtonContainer.Size = UDim2.new(1, -32, 0, 72)

	local UIListLayout = Instance.new("UIListLayout")
	UIListLayout.FillDirection = Enum.FillDirection.Horizontal
	UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout.VerticalAlignment = Enum.VerticalAlignment.Center
	UIListLayout.Padding = UDim.new(0, 10)
	UIListLayout.Parent = ButtonContainer

	local GAMES = {"Hood Games", "Prison Life", "Universal"}
	local ACCENT_COLOR = Color3.fromRGB(100, 60, 220)
	local HOVER_COLOR  = Color3.fromRGB(120, 80, 240)
	local BASE_COLOR   = Color3.fromRGB(30, 30, 30)

	for _, gameName in ipairs(GAMES) do
		local Btn = Instance.new("TextButton")
		Btn.Parent = ButtonContainer
		Btn.BackgroundColor3 = BASE_COLOR
		Btn.BorderSizePixel = 0
		Btn.Size = UDim2.new(0, 126, 0, 44)
		Btn.Font = Enum.Font.GothamSemibold
		Btn.Text = gameName
		Btn.TextColor3 = Color3.fromRGB(220, 220, 220)
		Btn.TextSize = 13
		Btn.AutoButtonColor = false
		Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 6)

		local Stroke = Instance.new("UIStroke")
		Stroke.Color = Color3.fromRGB(60, 60, 60)
		Stroke.Thickness = 1
		Stroke.Parent = Btn

		Btn.MouseEnter:Connect(function()
			TweenService:Create(Btn, TweenInfo.new(0.15), {BackgroundColor3 = HOVER_COLOR}):Play()
			TweenService:Create(Stroke, TweenInfo.new(0.15), {Color = ACCENT_COLOR}):Play()
		end)

		Btn.MouseLeave:Connect(function()
			TweenService:Create(Btn, TweenInfo.new(0.15), {BackgroundColor3 = BASE_COLOR}):Play()
			TweenService:Create(Stroke, TweenInfo.new(0.15), {Color = Color3.fromRGB(60, 60, 60)}):Play()
		end)

		Btn.MouseButton1Click:Connect(function()
			TweenService:Create(Btn, TweenInfo.new(0.08), {BackgroundColor3 = Color3.fromRGB(80, 40, 180)}):Play()
			task.wait(0.1)
			task.spawn(callback, gameName)
		end)
	end

	dragify(Main)
end

function Loader:Delete(name)
	local gui = game.CoreGui:FindFirstChild(name)
	if gui then
		gui:Destroy()
	else
		error("[Reformation Loader]: GUI '" .. tostring(name) .. "' could not be found.")
	end
end

Loader:Create({
	Name = "Reformation",
	Callback = function(SelectedGame)
		Loader:Delete("Reformation")
		handleGame(SelectedGame)
	end,
})
