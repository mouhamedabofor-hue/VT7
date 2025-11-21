-- FE GUI: Decal Spam + Skybox Set
-- Asset ID: 137936542992848

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "DecalSkyboxGUI"
gui.ResetOnSpawn = false

-- Main draggable frame
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 250, 0, 150)
frame.Position = UDim2.new(0.5, -125, 0.8, 0)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
frame.BorderSizePixel = 2
frame.Active = true
frame.Draggable = true

local corner = Instance.new("UICorner", frame)
corner.CornerRadius = UDim.new(0, 8)

-- Utility function
local function makeButton(name, posY, text)
	local button = Instance.new("TextButton", frame)
	button.Size = UDim2.new(0, 200, 0, 40)
	button.Position = UDim2.new(0.5, -100, 0, posY)
	button.Text = text
	button.TextScaled = true
	button.Font = Enum.Font.GothamBold
	button.TextColor3 = Color3.new(1, 1, 1)
	button.BackgroundColor3 = Color3.fromRGB(60, 120, 200)
	local btnCorner = Instance.new("UICorner", button)
	btnCorner.CornerRadius = UDim.new(0, 6)
	return button
end

-- Decal Spam Button
local decalButton = makeButton("DecalSpam", 20, "Decal Spam")

decalButton.MouseButton1Click:Connect(function()
	local id = "rbxassetid://137936542992848"
	for _, part in ipairs(workspace:GetDescendants()) do
		if part:IsA("BasePart") and not part:IsA("Terrain") then
			local decal = Instance.new("Decal")
			decal.Texture = id
			decal.Face = Enum.NormalId.Front
			decal.Parent = part
		end
	end
	decalButton.Text = "Spammed!"
end)

-- Set Skybox Button
local skyboxButton = makeButton("SetSkybox", 70, "Set Skybox")

skyboxButton.MouseButton1Click:Connect(function()
	local id = "rbxassetid://137936542992848"
	local lighting = game:GetService("Lighting")
	for _, v in ipairs(lighting:GetChildren()) do
		if v:IsA("Sky") then v:Destroy() end
	end
	local sky = Instance.new("Sky", lighting)
	sky.SkyboxBk = id
	sky.SkyboxDn = id
	sky.SkyboxFt = id
	sky.SkyboxLf = id
	sky.SkyboxRt = id
	sky.SkyboxUp = id
	skyboxButton.Text = "Skybox Set!"
end)
