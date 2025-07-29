local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

local airForce = 5
local airHelper = false
local hitboxSize = Vector3.new(20, 5, 20)

local gui = Instance.new("ScreenGui")
gui.Name = "FetlessGui"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local function addShadow(instance)
	local stroke = Instance.new("UIStroke")
	stroke.Color = Color3.fromRGB(0, 0, 0)
	stroke.Thickness = 1.2
	stroke.Transparency = 0.4
	stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	stroke.Parent = instance
end

local function styleButton(button)
	button.AutoButtonColor = false
	addShadow(button)
	local stroke = Instance.new("UIStroke", button)
	stroke.Color = Color3.fromRGB(255, 255, 255)
	stroke.Thickness = 1
	stroke.Transparency = 0.6
	stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	button.MouseEnter:Connect(function()
		TweenService:Create(button, TweenInfo.new(0.2), {BackgroundTransparency = 0.1}):Play()
	end)
	button.MouseLeave:Connect(function()
		TweenService:Create(button, TweenInfo.new(0.2), {BackgroundTransparency = 0}):Play()
	end)
end

local openBtn = Instance.new("ImageButton", gui)
openBtn.Size = UDim2.new(0, 50, 0, 50)
openBtn.Position = UDim2.new(0, 20, 0.5, -25)
openBtn.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
openBtn.Image = "rbxthumb://type=Asset&id=72543982349733&w=420&h=420"
openBtn.Name = "OpenButton"
openBtn.Draggable = true
openBtn.Active = true
Instance.new("UICorner", openBtn)
addShadow(openBtn)

local panel = Instance.new("Frame", gui)
panel.Size = UDim2.new(0, 300, 0, 350)
panel.Position = UDim2.new(0.5, -150, 0.5, -175)
panel.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
panel.BackgroundTransparency = 0.2
panel.Visible = false
panel.ZIndex = 1
Instance.new("UICorner", panel)
addShadow(panel)

local bg = Instance.new("ImageLabel", panel)
bg.Size = UDim2.new(1, 0, 1, 0)
bg.Position = UDim2.new(0, 0, 0, 0)
bg.Image = "rbxthumb://type=Asset&id=138209408586401&w=420&h=420"
bg.BackgroundTransparency = 1
bg.ZIndex = 0

local icon = Instance.new("ImageLabel", panel)
icon.Size = UDim2.new(0, 40, 0, 40)
icon.Position = UDim2.new(0, 5, 0, 5)
icon.Image = "rbxthumb://type=Asset&id=119604369257338&w=420&h=420"
icon.BackgroundTransparency = 1
icon.ZIndex = 2

local title = Instance.new("TextLabel", panel)
title.Size = UDim2.new(1, -50, 0, 40)
title.Position = UDim2.new(0, 50, 0, 0)
title.Text = "Fetless"
title.TextColor3 = Color3.new(1, 1, 1)
title.TextStrokeTransparency = 0.8
title.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
title.TextScaled = true
title.Font = Enum.Font.GothamBold
title.BackgroundTransparency = 1
title.ZIndex = 2

local subTitle = Instance.new("TextLabel", panel)
subTitle.Size = UDim2.new(1, 0, 0, 20)
subTitle.Position = UDim2.new(0, 0, 0, 40)
subTitle.Text = ".Hub SOCCER League"
subTitle.TextColor3 = Color3.fromRGB(0, 255, 0)
subTitle.TextStrokeTransparency = 0.8
subTitle.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
subTitle.TextScaled = true
subTitle.Font = Enum.Font.GothamBold
subTitle.BackgroundTransparency = 1
subTitle.ZIndex = 2

local closeBtn = Instance.new("TextButton", panel)
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -35, 0, 5)
closeBtn.Text = "X"
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
closeBtn.TextColor3 = Color3.new(1, 1, 1)
closeBtn.TextScaled = true
closeBtn.Font = Enum.Font.GothamBold
closeBtn.ZIndex = 2
Instance.new("UICorner", closeBtn)
styleButton(closeBtn)

closeBtn.MouseButton1Click:Connect(function()
	TweenService:Create(panel, TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
	wait(0.3)
	panel.Visible = false
end)

local function createBar(yPos, color)
	local bg = Instance.new("Frame", panel)
	bg.Size = UDim2.new(0, 270, 0, 20)
	bg.Position = UDim2.new(0, 15, 0, yPos)
	bg.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	bg.ZIndex = 2
	local corner = Instance.new("UICorner", bg)
	corner.CornerRadius = UDim.new(0, 10)
	addShadow(bg)

	local bar = Instance.new("Frame", bg)
	bar.Size = UDim2.new(0, 0, 1, 0)
	bar.BackgroundColor3 = color
	bar.ZIndex = 3
	local barCorner = Instance.new("UICorner", bar)
	barCorner.CornerRadius = UDim.new(0, 10)
	bar.Parent = bg

	return bar
end

local hitboxBar = createBar(220, Color3.fromRGB(255, 100, 0))
local airBar = createBar(270, Color3.fromRGB(0, 200, 255))

local hitboxBtn = Instance.new("TextButton", panel)
hitboxBtn.Size = UDim2.new(0, 130, 0, 40)
hitboxBtn.Position = UDim2.new(0, 15, 0, 70)
hitboxBtn.Text = "Aumentar Hitbox"
hitboxBtn.BackgroundColor3 = Color3.fromRGB(255, 100, 0)
hitboxBtn.TextColor3 = Color3.new(1, 1, 1)
hitboxBtn.TextScaled = true
hitboxBtn.Font = Enum.Font.GothamBold
hitboxBtn.ZIndex = 2
Instance.new("UICorner", hitboxBtn)
styleButton(hitboxBtn)

local decreaseHitboxBtn = hitboxBtn:Clone()
decreaseHitboxBtn.Text = "Diminuir Hitbox"
decreaseHitboxBtn.Position = UDim2.new(0, 155, 0, 70)
styleButton(decreaseHitboxBtn)

local airBtn = Instance.new("TextButton", panel)
airBtn.Size = UDim2.new(0, 130, 0, 40)
airBtn.Position = UDim2.new(0, 15, 0, 120)
airBtn.Text = "Aumentar Air Helper"
airBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 255)
airBtn.TextColor3 = Color3.new(1, 1, 1)
airBtn.TextScaled = true
airBtn.Font = Enum.Font.GothamBold
airBtn.ZIndex = 2
Instance.new("UICorner", airBtn)
styleButton(airBtn)

local decreaseAirBtn = airBtn:Clone()
decreaseAirBtn.Text = "Diminuir Air Helper"
decreaseAirBtn.Position = UDim2.new(0, 155, 0, 120)
styleButton(decreaseAirBtn)

hitboxBtn.Parent = panel
decreaseHitboxBtn.Parent = panel
airBtn.Parent = panel
decreaseAirBtn.Parent = panel

hitboxBtn.MouseButton1Click:Connect(function()
	hitboxSize += Vector3.new(5, 0, 5)
	hitboxBar.Size = UDim2.new(math.clamp(hitboxSize.X / 50, 0, 1), 0, 1, 0)
end)

decreaseHitboxBtn.MouseButton1Click:Connect(function()
	hitboxSize -= Vector3.new(5, 0, 5)
	hitboxSize = Vector3.new(math.max(5, hitboxSize.X), hitboxSize.Y, math.max(5, hitboxSize.Z))
	hitboxBar.Size = UDim2.new(math.clamp(hitboxSize.X / 50, 0, 1), 0, 1, 0)
end)

airBtn.MouseButton1Click:Connect(function()
	airForce += 1
	airHelper = true
	airBar.Size = UDim2.new(math.clamp(airForce / 50, 0, 1), 0, 1, 0)
end)

decreaseAirBtn.MouseButton1Click:Connect(function()
	airForce = math.max(1, airForce - 1)
	airBar.Size = UDim2.new(math.clamp(airForce / 50, 0, 1), 0, 1, 0)
end)

openBtn.MouseButton1Click:Connect(function()
	if not panel.Visible then
		panel.BackgroundTransparency = 1
		panel.Visible = true
		TweenService:Create(panel, TweenInfo.new(0.3), {BackgroundTransparency = 0.2}):Play()
	else
		TweenService:Create(panel, TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
		wait(0.3)
		panel.Visible = false
	end
end)

local BodyVelocity = nil

RunService.Heartbeat:Connect(function()
	character = player.Character or player.CharacterAdded:Wait()
	local hrp = character:FindFirstChild("HumanoidRootPart")
	local leg = character:FindFirstChild("Right Leg") or character:FindFirstChild("RightLowerLeg")

	for _, ball in ipairs(workspace:GetDescendants()) do
		if ball:IsA("Part") and ball.Name == "Ball" then
			local model = ball.Parent
			if model and model:IsA("Model") then
				local hitbox = model:FindFirstChild("BallHitbox")
				if not hitbox then
					hitbox = Instance.new("Part")
					hitbox.Name = "BallHitbox"
					hitbox.Anchored = true
					hitbox.CanCollide = false
					hitbox.Massless = true
					hitbox.Shape = Enum.PartType.Block -- Retângulo
					hitbox.Size = hitboxSize
					hitbox.Transparency = 0.6
					hitbox.Material = Enum.Material.ForceField
					hitbox.Color = Color3.fromRGB(0, 0, 255)
					hitbox.Parent = model
				end

				hitbox.Size = hitboxSize
				hitbox.CFrame = CFrame.new(ball.Position) -- sem rotação

				if leg and (leg.Position - hitbox.Position).Magnitude < (hitbox.Size.X / 2 + leg.Size.X / 2) then
					local dir = (ball.Position - hrp.Position).Unit
					ball.Velocity = dir * 50 + Vector3.new(0, 30, 0)
					ball.AssemblyLinearVelocity = Vector3.new(
						ball.AssemblyLinearVelocity.X * 0.5,
						math.max(ball.AssemblyLinearVelocity.Y, 30),
						ball.AssemblyLinearVelocity.Z * 0.5
					)
				end

				if airHelper and hrp and ball.Position.Y > hrp.Position.Y and (ball.Position - hrp.Position).Magnitude < 20 then
					if not BodyVelocity or not BodyVelocity.Parent then
						BodyVelocity = Instance.new("BodyVelocity")
						BodyVelocity.MaxForce = Vector3.new(4000, 4000, 4000)
						BodyVelocity.P = 1000
						BodyVelocity.Parent = hrp
					end

					local targetPos = ball.Position + Vector3.new(0, 2, 0)
					local moveDir = (targetPos - hrp.Position) * (airForce * 0.2)
					BodyVelocity.Velocity = moveDir
				else
					if BodyVelocity and BodyVelocity.Parent then
						BodyVelocity:Destroy()
						BodyVelocity = nil
					end
				end
			end
		end
	end
end)
