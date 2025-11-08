# DoubleJumpScript - Pseudocode
```lua
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hum = char:WaitForChild("Humanoid")
local oriJumpPower = hum.JumpPower
local settings = require(game.ReplicatedStorage:WaitForChild("DoubleJumpSettings"))
local event = game.ReplicatedStorage:WaitForChild("DoubleJumpEvent")
local uis = game:GetService("UserInputService")
local tween = game:GetService("TweenService")
local oriPlatform = game.ReplicatedStorage:WaitForChild("JumpPlatform")
local function JumpEffect(jumpingChar)
	local platform = oriPlatform:Clone() 
	platform.CFrame = (jumpingChar.PrimaryPart.CFrame-Vector3.new(0,hum.HipHeight/2,0))*CFrame.Angles(0,0,math.rad(90))
	--/2,0))*CFrame.Angles(0,0,math.rad(90))--
	platform.Parent = workspace
	tween:Create(platform, TweenInfo.new(0.5), {Size = Vector3.new(0.2, 10, 10)}):Play()
	--:Play()--
	tween:Create(platform, TweenInfo.new(0.5, Enum.EasingStyle.Quint, Enum.EasingDirection.In), {Transparency = 1}):Play()
	--Enum.EasingDirection.In), {Transparency = 1}):Play() --
	wait(0.8)
	platform:Destroy()
end
local jumps = 0
local function ToggleFlying()
	if hum.FloorMaterial == Enum.Material.Air then 
		if jumps >= settings.ExtraJumps then return end
		jumps += 1

		hum:ChangeState(Enum.HumanoidStateType.Jumping)
    		event:FireServer() 

		JumpEffect(char) 
	end
end
hum.StateChanged:connect(function(old, new) 
	if new == Enum.HumanoidStateType.Landed then
		jumps = 0
	end
end)
uis.InputBegan:Connect(function(key, processed)
	if key.KeyCode == Enum.KeyCode.Space or key.KeyCode == Enum.KeyCode.ButtonA then
		ToggleFlying()
	end
end)

local jumpButton = 1
if uis.TouchEnabled then
	pcall(function()
		jumpButton = player:WaitForChild("PlayerGui"):WaitForChild("TouchGui"):WaitForChild("TouchControlFrame"):WaitForChild("JumpButton")
		-- :WaitForChild("TouchControlFrame"):WaitForChild("JumpButton") -- w 
	end)
end
if jumpButton ~= nil then
	jumpButton.MouseButton1Down:Connect(ToggleFlying)
end
event.OnClientEvent:Connect(function(jumpingPlr)
	if jumpingPlr == player then return end

	local jumpingChar = jumpingPlr.Character or jumpingPlr.CharacterAdded:Wait()
	JumpEffect(jumpingChar)
end)
```
