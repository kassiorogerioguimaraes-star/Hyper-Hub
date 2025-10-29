-- // 🌌 Futuristic Floating GUI System by Kássio

local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

-- // GUI Principal
local gui = Instance.new("ScreenGui")
gui.Name = "FuturisticGUI"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = playerGui

-- // Botão flutuante (com efeito espacial)
local toggleBtn = Instance.new("ImageButton")
toggleBtn.Size = UDim2.new(0, 60, 0, 60)
toggleBtn.Position = UDim2.new(0, 15, 0, 70) -- 🔽 abaixado um pouco mais
toggleBtn.BackgroundTransparency = 0.3
toggleBtn.BackgroundColor3 = Color3.fromRGB(10, 10, 25)
toggleBtn.Image = "rbxassetid://807232418494"
toggleBtn.ImageTransparency = 0
toggleBtn.ScaleType = Enum.ScaleType.Fit
toggleBtn.AutoButtonColor = false
toggleBtn.Parent = gui

-- Glow em volta do botão
local glow = Instance.new("UIStroke")
glow.Thickness = 2
glow.Color = Color3.fromRGB(0, 200, 255)
glow.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
glow.Parent = toggleBtn

-- Bordas arredondadas
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(1, 0)
corner.Parent = toggleBtn

-- Brilho animado no botão
task.spawn(function()
while task.wait(0.05) do
local t = tick() * 2
glow.Color = Color3.fromRGB(0, 150 + math.sin(t) * 100, 255)
end
end)

-- // Função de arrastar
local dragging, dragInput, dragStart, startPos
local function update(input)
local delta = input.Position - dragStart
toggleBtn.Position = UDim2.new(
startPos.X.Scale, startPos.X.Offset + delta.X,
startPos.Y.Scale, startPos.Y.Offset + delta.Y
)
end

toggleBtn.InputBegan:Connect(function(input)
if input.UserInputType == Enum.UserInputType.MouseButton1 then
dragging = true
dragStart = input.Position
startPos = toggleBtn.Position
input.Changed:Connect(function()
if input.UserInputState == Enum.UserInputState.End then
dragging = false
end
end)
end
end)

toggleBtn.InputChanged:Connect(function(input)
if input.UserInputType == Enum.UserInputType.MouseMovement then
dragInput = input
end
end)

UserInputService.InputChanged:Connect(function(input)
if input == dragInput and dragging then
update(input)
end
end)

-- // Painel principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 320, 0, 230)
mainFrame.Position = UDim2.new(0.5, -160, 0.5, -115)
mainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 35)
mainFrame.BackgroundTransparency = 0.2
mainFrame.Visible = false
mainFrame.Parent = gui

Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0, 12)
local frameGlow = Instance.new("UIStroke", mainFrame)
frameGlow.Color = Color3.fromRGB(0, 255, 255)
frameGlow.Thickness = 1.8

-- Fade futurista
local function toggleFrame(show)
local goal = {BackgroundTransparency = show and 0.2 or 1}
TweenService:Create(mainFrame, TweenInfo.new(0.4, Enum.EasingStyle.Sine), goal):Play()
mainFrame.Visible = true
task.wait(show and 0 or 0.4)
mainFrame.Visible = show
end

-- Botões principais
local stealsBtn = Instance.new("TextButton")
stealsBtn.Size = UDim2.new(0, 140, 0, 30)
stealsBtn.Position = UDim2.new(0, 10, 0, 10)
stealsBtn.Text = "🛰 Steals"
stealsBtn.BackgroundColor3 = Color3.fromRGB(25, 25, 55)
stealsBtn.TextColor3 = Color3.fromRGB(180, 255, 255)
stealsBtn.Parent = mainFrame
Instance.new("UICorner", stealsBtn).CornerRadius = UDim.new(0, 6)

local protectionBtn = Instance.new("TextButton")
protectionBtn.Size = UDim2.new(0, 140, 0, 30)
protectionBtn.Position = UDim2.new(0, 160, 0, 10)
protectionBtn.Text = "🛡 Protection"
protectionBtn.BackgroundColor3 = Color3.fromRGB(25, 25, 55)
protectionBtn.TextColor3 = Color3.fromRGB(180, 255, 255)
protectionBtn.Parent = mainFrame
Instance.new("UICorner", protectionBtn).CornerRadius = UDim.new(0, 6)

-- Painel Steals
local stealsPanel = Instance.new("Frame")
stealsPanel.Size = UDim2.new(0, 300, 0, 170)
stealsPanel.Position = UDim2.new(0, 10, 0, 50)
stealsPanel.Visible = false
stealsPanel.BackgroundColor3 = Color3.fromRGB(20, 20, 40)
stealsPanel.BackgroundTransparency = 0.2
stealsPanel.Parent = mainFrame
Instance.new("UICorner", stealsPanel).CornerRadius = UDim.new(0, 10)

-- Painel Protection
local protectionPanel = Instance.new("Frame")
protectionPanel.Size = UDim2.new(0, 300, 0, 170)
protectionPanel.Position = UDim2.new(0, 10, 0, 50)
protectionPanel.Visible = false
protectionPanel.BackgroundColor3 = Color3.fromRGB(20, 20, 40)
protectionPanel.BackgroundTransparency = 0.2
protectionPanel.Parent = mainFrame
Instance.new("UICorner", protectionPanel).CornerRadius = UDim.new(0, 10)

-- Criador de botões
local function createBtn(name, y, parent)
local btn = Instance.new("TextButton")
btn.Name = name
btn.Size = UDim2.new(0, 280, 0, 30)
btn.Position = UDim2.new(0, 10, 0, y)
btn.Text = "⚙ " .. name
btn.BackgroundColor3 = Color3.fromRGB(30, 30, 60)
btn.TextColor3 = Color3.fromRGB(200, 255, 255)
btn.Parent = parent
Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
return btn
end

local infiniteJumpBtn = createBtn("Infinite Jump", 0, stealsPanel)
local floatBtn = createBtn("Float", 35, stealsPanel)
local xrayBtn = createBtn("Xray", 70, stealsPanel)
local desyncBtn = createBtn("Desync", 105, stealsPanel)
local godModeBtn = createBtn("God Mode", 140, stealsPanel)

-- 🔰 Botão Anti Hit (Protection)
local antiHitBtn = createBtn("Anti Hit", 0, protectionPanel)

-- Alternar painel principal
local visible = false
toggleBtn.MouseButton1Click:Connect(function()
visible = not visible
toggleFrame(visible)
end)

-- Alternar Steals e Protection
stealsBtn.MouseButton1Click:Connect(function()
stealsPanel.Visible = true
protectionPanel.Visible = false
end)
protectionBtn.MouseButton1Click:Connect(function()
stealsPanel.Visible = false
protectionPanel.Visible = true
end)


---

-- 🌠 Infinite Jump

local infiniteJumpEnabled = false
local infiniteJumpConnection
local smoothPower = 35

local function toggleInfiniteJump()
infiniteJumpEnabled = not infiniteJumpEnabled
infiniteJumpBtn.Text = infiniteJumpEnabled and "⚙ Infinite Jump ✅" or "⚙ Infinite Jump ❌"

if infiniteJumpEnabled then  
	infiniteJumpConnection = UserInputService.JumpRequest:Connect(function()  
		local char = player.Character  
		if char and char:FindFirstChild("HumanoidRootPart") then  
			local root = char.HumanoidRootPart  
			root.Velocity = Vector3.new(root.Velocity.X, smoothPower, root.Velocity.Z)  
		end  
	end)  
else  
	if infiniteJumpConnection then  
		infiniteJumpConnection:Disconnect()  
		infiniteJumpConnection = nil  
	end  
end

end
infiniteJumpBtn.MouseButton1Click:Connect(toggleInfiniteJump)


---

-- 🚀 God Mode

local godModeEnabled = false
local godConnection

local function toggleGodMode()
godModeEnabled = not godModeEnabled
godModeBtn.Text = godModeEnabled and "⚙ God Mode ✅" or "⚙ God Mode ❌"

if godModeEnabled then  
	godConnection = RunService.Heartbeat:Connect(function()  
		local char = player.Character  
		if char and char:FindFirstChild("Humanoid") then  
			local humanoid = char.Humanoid  
			humanoid:SetStateEnabled(Enum.HumanoidStateType.Dead, false)  
			if humanoid.Health < humanoid.MaxHealth then  
				humanoid.Health = humanoid.MaxHealth  
			end  
		end  
	end)  
else  
	if godConnection then  
		godConnection:Disconnect()  
		godConnection = nil  
	end  
end

end
godModeBtn.MouseButton1Click:Connect(toggleGodMode)


---

-- 🧊 Xray

local xrayEnabled = false
local originalMaterials = {}

local function toggleXray()
xrayEnabled = not xrayEnabled
xrayBtn.Text = xrayEnabled and "⚙ Xray ✅" or "⚙ Xray ❌"

for _, obj in ipairs(workspace:GetDescendants()) do  
	if obj:IsA("BasePart") then  
		if xrayEnabled then  
			originalMaterials[obj] = obj.Transparency  
			obj.Transparency = 0.7  
		elseif originalMaterials[obj] ~= nil then  
			obj.Transparency = originalMaterials[obj]  
		end  
	end  
end

end
xrayBtn.MouseButton1Click:Connect(toggleXray)


---

-- 🛸 Float

local floatEnabled = false
local floatConnection
local flySpeed = 15

local function toggleFloat()
floatEnabled = not floatEnabled
floatBtn.Text = floatEnabled and "⚙ Float ✅" or "⚙ Float ❌"

if floatEnabled then  
	floatConnection = RunService.Heartbeat:Connect(function()  
		local char = player.Character  
		if char and char:FindFirstChild("HumanoidRootPart") then  
			local root = char.HumanoidRootPart  
			local dir = workspace.CurrentCamera.CFrame.LookVector  
			root.Velocity = dir * flySpeed  
		end  
	end)  
else  
	if floatConnection then  
		floatConnection:Disconnect()  
		floatConnection = nil  
	end  
end

end
floatBtn.MouseButton1Click:Connect(toggleFloat)


---

-- ⚠️ Desync (Em Manutenção!)

local function showMaintenance()
local msg = Instance.new("TextLabel")
msg.Size = UDim2.new(1, 0, 0, 40)
msg.Position = UDim2.new(0, 0, 0.4, 0)
msg.BackgroundTransparency = 1
msg.Text = "🚧 Em Manutenção!"
msg.TextColor3 = Color3.fromRGB(255, 200, 0)
msg.TextScaled = true
msg.Font = Enum.Font.GothamBold
msg.Parent = gui
task.wait(2)
msg:Destroy()
end
desyncBtn.MouseButton1Click:Connect(showMaintenance)


---

-- 🧩 Anti Hit (Detecta ragdoll e congela 2.5s)

local antiHitEnabled = false
local ragdollConnection

local function toggleAntiHit()
antiHitEnabled = not antiHitEnabled
antiHitBtn.Text = antiHitEnabled and "⚙ Anti Hit ✅" or "⚙ Anti Hit ❌"

if antiHitEnabled then  
	ragdollConnection = RunService.Heartbeat:Connect(function()  
		local char = player.Character  
		if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then  
			local humanoid = char.Humanoid  
			if humanoid.PlatformStand then -- 🔹 Detecta ragdoll  
				humanoid.PlatformStand = true  
				task.wait(2.5)  
				humanoid.PlatformStand = false  
			end  
		end  
	end)  
else  
	if ragdollConnection then  
		ragdollConnection:Disconnect()  
		ragdollConnection = nil  
	end  
end

end
antiHitBtn.MouseButton1Click:Connect(toggleAntiHit)
