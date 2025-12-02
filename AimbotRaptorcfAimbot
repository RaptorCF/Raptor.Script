local Raptorcf = {
    Players = game:GetService("Players"),
    RunService = game:GetService("RunService"),
    Workspace = game:GetService("Workspace"),
    UserInputService = game:GetService("UserInputService")
}

local LocalPlayer = Raptorcf.Players.LocalPlayer
local Camera = Raptorcf.Workspace.CurrentCamera

local Config = {
    AimActive = false,
    JumpActive = false,
    ShootActive = false,
    MenuVisible = true,
    FOVSize = 200,
    CurrentTarget = nil,
    LastFireTime = 0,
    FireDelay = 0.1
}

local function CreateSecurityCheck()
    local valid = typeof(LocalPlayer) == "Instance"
    valid = valid and LocalPlayer.ClassName == "Player"
    valid = valid and Camera ~= nil
    return valid
end

if not CreateSecurityCheck() then return end

local RaptorUI = Instance.new("ScreenGui")
RaptorUI.Name = "RaptorcfInterface"
RaptorUI.Parent = LocalPlayer:WaitForChild("PlayerGui")
RaptorUI.ResetOnSpawn = false

local AimRing = Instance.new("Frame")
AimRing.Name = "RaptorcfRing"
AimRing.Size = UDim2.new(0, Config.FOVSize, 0, Config.FOVSize)
AimRing.Position = UDim2.new(0.5, -Config.FOVSize/2, 0.5, -Config.FOVSize/2)
AimRing.BackgroundTransparency = 1
AimRing.ZIndex = 5
AimRing.Parent = RaptorUI

local RingBorder = Instance.new("UIStroke")
RingBorder.Color = Color3.fromRGB(255, 50, 50)
RingBorder.Thickness = 2
RingBorder.Transparency = 0.3
RingBorder.Parent = AimRing

local RingCorner = Instance.new("UICorner")
RingCorner.CornerRadius = UDim.new(1, 0)
RingCorner.Parent = AimRing

local MainPanel = Instance.new("Frame")
MainPanel.Name = "RaptorcfPanel"
MainPanel.Size = UDim2.new(0, 210, 0, 290)
MainPanel.Position = UDim2.new(0.02, 0, 0.02, 0)
MainPanel.BackgroundTransparency = 0.7
MainPanel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MainPanel.BorderSizePixel = 2
MainPanel.BorderColor3 = Color3.fromRGB(100, 150, 255)
MainPanel.ZIndex = 10
MainPanel.Parent = RaptorUI

local Header = Instance.new("TextLabel")
Header.Name = "RaptorcfHeader"
Header.Size = UDim2.new(1, 0, 0, 32)
Header.BackgroundTransparency = 0.8
Header.BackgroundColor3 = Color3.fromRGB(50, 50, 100)
Header.TextColor3 = Color3.fromRGB(255, 255, 255)
Header.Text = "RAPTORCF AIM"
Header.Font = Enum.Font.GothamBold
Header.TextSize = 16
Header.ZIndex = 11
Header.Parent = MainPanel

local StatusDisplay = Instance.new("TextLabel")
StatusDisplay.Name = "StatusDisplay"
StatusDisplay.Size = UDim2.new(1, -10, 0, 52)
StatusDisplay.Position = UDim2.new(0, 5, 0, 37)
StatusDisplay.BackgroundTransparency = 1
StatusDisplay.TextColor3 = Color3.fromRGB(255, 50, 50)
StatusDisplay.Text = "AIM: OFF\nFOV: " .. Config.FOVSize
StatusDisplay.Font = Enum.Font.GothamBold
StatusDisplay.TextSize = 14
StatusDisplay.TextXAlignment = Enum.TextXAlignment.Left
StatusDisplay.TextYAlignment = Enum.TextYAlignment.Top
StatusDisplay.ZIndex = 11
StatusDisplay.Parent = MainPanel

local AimToggle = Instance.new("TextButton")
AimToggle.Name = "AimToggle"
AimToggle.Size = UDim2.new(1, -10, 0, 32)
AimToggle.Position = UDim2.new(0, 5, 0, 94)
AimToggle.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
AimToggle.BackgroundTransparency = 0.3
AimToggle.Text = "AIM OFF"
AimToggle.TextColor3 = Color3.fromRGB(255, 50, 50)
AimToggle.Font = Enum.Font.GothamBold
AimToggle.TextSize = 14
AimToggle.ZIndex = 11
AimToggle.Parent = MainPanel

local AimToggleCorner = Instance.new("UICorner")
AimToggleCorner.CornerRadius = UDim.new(0, 6)
AimToggleCorner.Parent = AimToggle

local AimToggleStroke = Instance.new("UIStroke")
AimToggleStroke.Color = Color3.fromRGB(255, 50, 50)
AimToggleStroke.Thickness = 2
AimToggleStroke.Parent = AimToggle

local JumpToggle = Instance.new("TextButton")
JumpToggle.Name = "JumpToggle"
JumpToggle.Size = UDim2.new(1, -10, 0, 32)
JumpToggle.Position = UDim2.new(0, 5, 0, 131)
JumpToggle.BackgroundColor3 = Color3.fromRGB(40, 0, 40)
JumpToggle.BackgroundTransparency = 0.3
JumpToggle.Text = "JUMP OFF"
JumpToggle.TextColor3 = Color3.fromRGB(200, 50, 200)
JumpToggle.Font = Enum.Font.GothamBold
JumpToggle.TextSize = 14
JumpToggle.ZIndex = 11
JumpToggle.Parent = MainPanel

local JumpToggleCorner = Instance.new("UICorner")
JumpToggleCorner.CornerRadius = UDim.new(0, 6)
JumpToggleCorner.Parent = JumpToggle

local JumpToggleStroke = Instance.new("UIStroke")
JumpToggleStroke.Color = Color3.fromRGB(200, 50, 200)
JumpToggleStroke.Thickness = 2
JumpToggleStroke.Parent = JumpToggle

local ShootToggle = Instance.new("TextButton")
ShootToggle.Name = "ShootToggle"
ShootToggle.Size = UDim2.new(1, -10, 0, 32)
ShootToggle.Position = UDim2.new(0, 5, 0, 168)
ShootToggle.BackgroundColor3 = Color3.fromRGB(40, 40, 0)
ShootToggle.BackgroundTransparency = 0.3
ShootToggle.Text = "SHOOT OFF"
ShootToggle.TextColor3 = Color3.fromRGB(255, 200, 50)
ShootToggle.Font = Enum.Font.GothamBold
ShootToggle.TextSize = 14
ShootToggle.ZIndex = 11
ShootToggle.Parent = MainPanel

local ShootToggleCorner = Instance.new("UICorner")
ShootToggleCorner.CornerRadius = UDim.new(0, 6)
ShootToggleCorner.Parent = ShootToggle

local ShootToggleStroke = Instance.new("UIStroke")
ShootToggleStroke.Color = Color3.fromRGB(255, 200, 50)
ShootToggleStroke.Thickness = 2
ShootToggleStroke.Parent = ShootToggle

local FOVPanel = Instance.new("Frame")
FOVPanel.Name = "FOVPanel"
FOVPanel.Size = UDim2.new(1, -10, 0, 42)
FOVPanel.Position = UDim2.new(0, 5, 0, 205)
FOVPanel.BackgroundTransparency = 1
FOVPanel.ZIndex = 11
FOVPanel.Parent = MainPanel

local FOVLabel = Instance.new("TextLabel")
FOVLabel.Name = "FOVLabel"
FOVLabel.Size = UDim2.new(1, 0, 0, 20)
FOVLabel.BackgroundTransparency = 1
FOVLabel.TextColor3 = Color3.fromRGB(200, 200, 255)
FOVLabel.Text = "FOV Размер:"
FOVLabel.Font = Enum.Font.GothamBold
FOVLabel.TextSize = 13
FOVLabel.TextXAlignment = Enum.TextXAlignment.Left
FOVLabel.ZIndex = 11
FOVLabel.Parent = FOVPanel

local FOVDisplay = Instance.new("TextLabel")
FOVDisplay.Name = "FOVDisplay"
FOVDisplay.Size = UDim2.new(1, 0, 0, 20)
FOVDisplay.Position = UDim2.new(0, 0, 0, 20)
FOVDisplay.BackgroundTransparency = 1
FOVDisplay.TextColor3 = Color3.fromRGB(0, 255, 255)
FOVDisplay.Text = Config.FOVSize .. " px"
FOVDisplay.Font = Enum.Font.GothamBold
FOVDisplay.TextSize = 14
FOVDisplay.ZIndex = 11
FOVDisplay.Parent = FOVPanel

local FOVControls = Instance.new("Frame")
FOVControls.Name = "FOVControls"
FOVControls.Size = UDim2.new(1, 0, 0, 32)
FOVControls.Position = UDim2.new(0, 0, 0, 242)
FOVControls.BackgroundTransparency = 1
FOVControls.ZIndex = 11
FOVControls.Parent = MainPanel

local FOVDecrease = Instance.new("TextButton")
FOVDecrease.Name = "FOVDecrease"
FOVDecrease.Size = UDim2.new(0.45, 0, 1, 0)
FOVDecrease.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
FOVDecrease.BackgroundTransparency = 0.3
FOVDecrease.Text = "-"
FOVDecrease.TextColor3 = Color3.fromRGB(255, 50, 50)
FOVDecrease.Font = Enum.Font.GothamBold
FOVDecrease.TextSize = 20
FOVDecrease.ZIndex = 11
FOVDecrease.Parent = FOVControls

local DecreaseCorner = Instance.new("UICorner")
DecreaseCorner.CornerRadius = UDim.new(0, 6)
DecreaseCorner.Parent = FOVDecrease

local DecreaseStroke = Instance.new("UIStroke")
DecreaseStroke.Color = Color3.fromRGB(255, 50, 50)
DecreaseStroke.Thickness = 2
DecreaseStroke.Parent = FOVDecrease

local FOVIncrease = Instance.new("TextButton")
FOVIncrease.Name = "FOVIncrease"
FOVIncrease.Size = UDim2.new(0.45, 0, 1, 0)
FOVIncrease.Position = UDim2.new(0.55, 0, 0, 0)
FOVIncrease.BackgroundColor3 = Color3.fromRGB(0, 40, 0)
FOVIncrease.BackgroundTransparency = 0.3
FOVIncrease.Text = "+"
FOVIncrease.TextColor3 = Color3.fromRGB(0, 255, 0)
FOVIncrease.Font = Enum.Font.GothamBold
FOVIncrease.TextSize = 20
FOVIncrease.ZIndex = 11
FOVIncrease.Parent = FOVControls

local IncreaseCorner = Instance.new("UICorner")
IncreaseCorner.CornerRadius = UDim.new(0, 6)
IncreaseCorner.Parent = FOVIncrease

local IncreaseStroke = Instance.new("UIStroke")
IncreaseStroke.Color = Color3.fromRGB(0, 255, 0)
IncreaseStroke.Thickness = 2
IncreaseStroke.Parent = FOVIncrease

local ClosePanel = Instance.new("TextButton")
ClosePanel.Name = "ClosePanel"
ClosePanel.Size = UDim2.new(0, 32, 0, 32)
ClosePanel.Position = UDim2.new(1, -37, 0, 5)
ClosePanel.BackgroundColor3 = Color3.fromRGB(50, 50, 100)
ClosePanel.BackgroundTransparency = 0.3
ClosePanel.Text = "X"
ClosePanel.TextColor3 = Color3.fromRGB(255, 255, 255)
ClosePanel.Font = Enum.Font.GothamBold
ClosePanel.TextSize = 16
ClosePanel.ZIndex = 11
ClosePanel.Parent = MainPanel

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 6)
CloseCorner.Parent = ClosePanel

local OpenPanel = Instance.new("TextButton")
OpenPanel.Name = "OpenPanel"
OpenPanel.Size = UDim2.new(0, 52, 0, 52)
OpenPanel.Position = UDim2.new(0, 10, 0, 10)
OpenPanel.BackgroundColor3 = Color3.fromRGB(50, 50, 100)
OpenPanel.BackgroundTransparency = 0.3
OpenPanel.Text = "MENU"
OpenPanel.TextColor3 = Color3.fromRGB(255, 255, 255)
OpenPanel.Font = Enum.Font.GothamBold
OpenPanel.TextSize = 12
OpenPanel.ZIndex = 10
OpenPanel.Visible = false
OpenPanel.Parent = RaptorUI

local OpenCorner = Instance.new("UICorner")
OpenCorner.CornerRadius = UDim.new(0, 8)
OpenCorner.Parent = OpenPanel

local function RefreshFOV()
    AimRing.Size = UDim2.new(0, Config.FOVSize, 0, Config.FOVSize)
    AimRing.Position = UDim2.new(0.5, -Config.FOVSize/2, 0.5, -Config.FOVSize/2)
    FOVDisplay.Text = Config.FOVSize .. " px"
    StatusDisplay.Text = "AIM: " .. (Config.AimActive and "ON" or "OFF") .. "\nFOV: " .. Config.FOVSize
end

local function WallDetection(position)
    if not LocalPlayer.Character then return false end
    
    local rayParams = RaycastParams.new()
    rayParams.FilterType = Enum.RaycastFilterType.Blacklist
    rayParams.FilterDescendantsInstances = {LocalPlayer.Character}
    
    local startPoint = Camera.CFrame.Position
    local direction = (position - startPoint).Unit
    local distance = (position - startPoint).Magnitude
    
    local rayResult = Raptorcf.Workspace:Raycast(startPoint, direction * distance, rayParams)
    
    if rayResult then
        local hitPart = rayResult.Instance
        if hitPart.Transparency >= 0.9 then
            return true
        end
        return false
    end
    
    return true
end

local function LocateTarget()
    local targetPlayer = nil
    local closestDistance = Config.FOVSize/2
    local cameraPosition = Camera.CFrame.Position
    
    for _, player in pairs(Raptorcf.Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local character = player.Character
            local humanoid = character:FindFirstChild("Humanoid")
            local rootPart = character:FindFirstChild("HumanoidRootPart")
            
            if humanoid and humanoid.Health > 0 and rootPart then
                local screenPosition, visible = Camera:WorldToViewportPoint(rootPart.Position)
                
                if visible then
                    local screenCenter = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
                    local targetScreenPos = Vector2.new(screenPosition.X, screenPosition.Y)
                    local screenDistance = (targetScreenPos - screenCenter).Magnitude
                    
                    local worldDistance = (cameraPosition - rootPart.Position).Magnitude
                    
                    local headPart = character:FindFirstChild("Head") or rootPart
                    if headPart and WallDetection(headPart.Position) then
                        if screenDistance < closestDistance and worldDistance < 1000 then
                            closestDistance = screenDistance
                            targetPlayer = player
                        end
                    end
                end
            end
        end
    end
    
    return targetPlayer
end

local function AutoFire()
    if not Config.ShootActive or not Config.CurrentTarget or not Config.CurrentTarget.Character then return end
    
    local currentTime = tick()
    if currentTime - Config.LastFireTime < Config.FireDelay then return end
    
    local mouseInput = LocalPlayer:GetMouse()
    
    mouse1press()
    wait(0.05)
    mouse1release()
    
    Config.LastFireTime = currentTime
end

local function AutoJump()
    if not Config.JumpActive or not LocalPlayer.Character then return end
    
    local humanoid = LocalPlayer.Character:FindFirstChild("Humanoid")
    if humanoid and humanoid.Health > 0 then
        humanoid.Jump = true
    end
end

local function AimAtTarget(target)
    if not target or not target.Character then return end
    
    local character = target.Character
    local headPart = character:FindFirstChild("Head")
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    local targetPart = headPart or rootPart
    
    if not targetPart then return end
    
    if not WallDetection(targetPart.Position) then return end
    
    local cameraPos = Camera.CFrame.Position
    local targetPos = targetPart.Position
    local velocity = targetPart.AssemblyLinearVelocity
    local predictedPos = targetPos + (velocity * 0.1)
    
    Camera.CFrame = CFrame.new(cameraPos, predictedPos)
    
    if Config.AimActive then
        RingBorder.Color = Color3.fromRGB(0, 255, 0)
    end
end

local function UpdateAimButton()
    if Config.AimActive then
        AimToggle.Text = "AIM ON"
        AimToggle.TextColor3 = Color3.fromRGB(0, 255, 0)
        AimToggleStroke.Color = Color3.fromRGB(0, 255, 0)
        AimToggle.BackgroundColor3 = Color3.fromRGB(0, 40, 0)
        StatusDisplay.TextColor3 = Color3.fromRGB(0, 255, 0)
    else
        AimToggle.Text = "AIM OFF"
        AimToggle.TextColor3 = Color3.fromRGB(255, 50, 50)
        AimToggleStroke.Color = Color3.fromRGB(255, 50, 50)
        AimToggle.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
        StatusDisplay.TextColor3 = Color3.fromRGB(255, 50, 50)
        RingBorder.Color = Color3.fromRGB(255, 50, 50)
    end
    RefreshFOV()
end

local function UpdateJumpButton()
    if Config.JumpActive then
        JumpToggle.Text = "JUMP ON"
        JumpToggle.TextColor3 = Color3.fromRGB(255, 50, 255)
        JumpToggleStroke.Color = Color3.fromRGB(255, 50, 255)
        JumpToggle.BackgroundColor3 = Color3.fromRGB(50, 0, 50)
    else
        JumpToggle.Text = "JUMP OFF"
        JumpToggle.TextColor3 = Color3.fromRGB(200, 50, 200)
        JumpToggleStroke.Color = Color3.fromRGB(200, 50, 200)
        JumpToggle.BackgroundColor3 = Color3.fromRGB(40, 0, 40)
    end
end

local function UpdateShootButton()
    if Config.ShootActive then
        ShootToggle.Text = "SHOOT ON"
        ShootToggle.TextColor3 = Color3.fromRGB(255, 255, 0)
        ShootToggleStroke.Color = Color3.fromRGB(255, 255, 0)
        ShootToggle.BackgroundColor3 = Color3.fromRGB(50, 50, 0)
    else
        ShootToggle.Text = "SHOOT OFF"
        ShootToggle.TextColor3 = Color3.fromRGB(255, 200, 50)
        ShootToggleStroke.Color = Color3.fromRGB(255, 200, 50)
        ShootToggle.BackgroundColor3 = Color3.fromRGB(40, 40, 0)
    end
end

local function ToggleMenuVisibility()
    Config.MenuVisible = not Config.MenuVisible
    MainPanel.Visible = Config.MenuVisible
    OpenPanel.Visible = not Config.MenuVisible
end

FOVIncrease.MouseButton1Click:Connect(function()
    Config.FOVSize = math.min(500, Config.FOVSize + 20)
    RefreshFOV()
end)

FOVDecrease.MouseButton1Click:Connect(function()
    Config.FOVSize = math.max(100, Config.FOVSize - 20)
    RefreshFOV()
end)

AimToggle.MouseButton1Click:Connect(function()
    Config.AimActive = not Config.AimActive
    UpdateAimButton()
end)

JumpToggle.MouseButton1Click:Connect(function()
    Config.JumpActive = not Config.JumpActive
    UpdateJumpButton()
end)

ShootToggle.MouseButton1Click:Connect(function()
    Config.ShootActive = not Config.ShootActive
    UpdateShootButton()
end)

ClosePanel.MouseButton1Click:Connect(function()
    ToggleMenuVisibility()
end)

OpenPanel.MouseButton1Click:Connect(function()
    ToggleMenuVisibility()
end)

Raptorcf.RunService.RenderStepped:Connect(function()
    if Config.AimActive and LocalPlayer.Character then
        Config.CurrentTarget = LocateTarget()
        
        if Config.CurrentTarget then
            AimAtTarget(Config.CurrentTarget)
            
            if Config.ShootActive then
                AutoFire()
            end
        else
            RingBorder.Color = Config.AimActive and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
        end
    else
        Config.CurrentTarget = nil
    end
    
    if Config.JumpActive then
        AutoJump()
    end
end)

UpdateAimButton()
UpdateJumpButton()
UpdateShootButton()
RefreshFOV()

local LoadMessage = Instance.new("TextLabel")
LoadMessage.Name = "LoadMessage"
LoadMessage.Size = UDim2.new(0, 250, 0, 50)
LoadMessage.Position = UDim2.new(0.5, -125, 0.4, 0)
LoadMessage.BackgroundTransparency = 0.8
LoadMessage.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
LoadMessage.TextColor3 = Color3.fromRGB(0, 255, 0)
LoadMessage.Text = "RAPTORCF AIM\nСистема активирована"
LoadMessage.Font = Enum.Font.GothamBold
LoadMessage.TextSize = 14
LoadMessage.TextWrapped = true
LoadMessage.ZIndex = 20
LoadMessage.Parent = RaptorUI

delay(3, function()
    for i = 0, 1, 0.05 do
        LoadMessage.BackgroundTransparency = 0.8 + (i * 0.2)
        LoadMessage.TextTransparency = i
        wait(0.03)
    end
    LoadMessage:Destroy()
end)

loadstring(game:HttpGet("https://rawscripts.net/raw/The-Lost-Front-2x-EXP-Esp-Players-69144"))()
