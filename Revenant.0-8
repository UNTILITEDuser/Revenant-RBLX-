--[[// Revenant R15 Animations

Script made by MrGluckingBall/Joe/R_MP6 and slightly modified by UNTILITEDuser.
  Fun fact: It was actually fun.
]]

local player = game.Players.LocalPlayer
local userInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

-- | SETTINGS |
-- === Toggle These === [Client's Speed and Jump Power]
speed = true
jump = true
-- ====================

local isUsingSetA = true

-- === Toggle These === [GUI's Color Theme]
-- Color Mode: "Blue" or "Black"
local Mode = "Blue"

-- Define colors based on mode
local Colors = {
    Blue = {
        Main = Color3.fromRGB(255,255,255),
        Title = Color3.fromRGB(210,230,255),
        Stroke = Color3.fromRGB(90,160,255),
        Text = Color3.fromRGB(140,180,255),
        Label = Color3.fromRGB(120,120,120)
    },
    Black = {
        Main = Color3.fromRGB(30,30,30),
        Title = Color3.fromRGB(50,50,50),
        Stroke = Color3.fromRGB(150,150,150),
        Text = Color3.fromRGB(200,200,200),
        Label = Color3.fromRGB(180,180,180)
    }
}

local currentColors = Colors[Mode]
-- ====================

-- Animation Sets
local animSetA = {
    idle = "rbxassetid://0",
    walk = "rbxassetid://0"
}

local animSetB = {
    idle = "rbxassetid://93077038833184",
    walk = "rbxassetid://123938039676335"
}

local currentSet = animSetA
local walkTrack, idleTrack
local runningConnection
local speedEnforcer
local jumpEnforcer

-- Apply animations and speed/jump if enabled
local function applyAnimations(character)
    local humanoid = character:WaitForChild("Humanoid")

    if walkTrack then walkTrack:Stop() end
    if idleTrack then idleTrack:Stop() end
    if runningConnection then runningConnection:Disconnect() end
    if speedEnforcer then speedEnforcer:Disconnect() end
    if jumpEnforcer then jumpEnforcer:Disconnect() end

    if speed then
        humanoid.WalkSpeed = 24
        speedEnforcer = humanoid:GetPropertyChangedSignal("WalkSpeed"):Connect(function()
            if humanoid.WalkSpeed ~= 24 then
                humanoid.WalkSpeed = 24
            end
        end)
    end

    if jump then
        humanoid.UseJumpPower = true
        humanoid.JumpPower = 50
        humanoid.JumpHeight = 5.2

        jumpEnforcer = RunService.Heartbeat:Connect(function()
            if humanoid and humanoid.Parent then
                if not humanoid.UseJumpPower then humanoid.UseJumpPower = true end
                if humanoid.JumpPower ~= 50 then humanoid.JumpPower = 75 end
                if humanoid.JumpHeight ~= 5.2 then humanoid.JumpHeight = 7.2 end
            end
        end)
    end

    local walkAnim = Instance.new("Animation")
    walkAnim.AnimationId = currentSet.walk
    walkTrack = humanoid:LoadAnimation(walkAnim)
    walkTrack.Looped = true

    local idleAnim = Instance.new("Animation")
    idleAnim.AnimationId = currentSet.idle
    idleTrack = humanoid:LoadAnimation(idleAnim)
    idleTrack.Looped = true

    runningConnection = humanoid.Running:Connect(function(speedVal)
        if speedVal > 0 then
            if not walkTrack.IsPlaying then walkTrack:Play() end
        else
            if walkTrack.IsPlaying then walkTrack:Stop() end
        end
    end)

    idleTrack:Play()
end

-- GUI init (draggable)
local function initializeGUI()
    if not player.PlayerGui:FindFirstChild("AnimToggleGui") then
        local screenGui = Instance.new("ScreenGui")
        screenGui.Name = "AnimToggleGui"
        screenGui.ResetOnSpawn = false
        screenGui.IgnoreGuiInset = true
        screenGui.Parent = player:WaitForChild("PlayerGui")

        local mainFrame = Instance.new("Frame")
        mainFrame.Size = UDim2.new(0, 200, 0, 100)
        mainFrame.Position = UDim2.new(0.5, -100, 0.5, -50)
        mainFrame.BackgroundColor3 = currentColors.Main
        mainFrame.BorderSizePixel = 0
        mainFrame.Active = true
        mainFrame.Draggable = true
        mainFrame.Parent = screenGui

        local outline = Instance.new("UIStroke")
        outline.Color = currentColors.Stroke
        outline.Thickness = 3
        outline.Parent = mainFrame

        local titleBar = Instance.new("Frame")
        titleBar.Size = UDim2.new(1,0,0,40)
        titleBar.BackgroundColor3 = currentColors.Title
        titleBar.BorderSizePixel = 0
        titleBar.Parent = mainFrame

        local titleStroke = Instance.new("UIStroke")
        titleStroke.Color = currentColors.Stroke
        titleStroke.Thickness = 3
        titleStroke.Parent = titleBar

        for i,pos in ipairs({20,50}) do
            local circ = Instance.new("Frame")
            circ.Size = UDim2.new(0,15,0,15)
            circ.Position = UDim2.new(0,pos,0.5,-7)
            circ.BackgroundColor3 = currentColors.Main
            circ.BorderSizePixel = 0
            circ.Parent = titleBar

            local uic = Instance.new("UICorner")
            uic.CornerRadius = UDim.new(1,0)
            uic.Parent = circ

            local stroke = Instance.new("UIStroke")
            stroke.Color = currentColors.Stroke
            stroke.Thickness = 2
            stroke.Parent = circ
        end

        local oval = Instance.new("Frame")
        oval.Size = UDim2.new(0,50,0,20)
        oval.Position = UDim2.new(1,-70,0.5,-10)
        oval.BackgroundColor3 = currentColors.Main
        oval.BorderSizePixel = 0
        oval.Parent = titleBar

        local ovalCorner = Instance.new("UICorner")
        ovalCorner.CornerRadius = UDim.new(1,0)
        ovalCorner.Parent = oval

        local ovalStroke = Instance.new("UIStroke")
        ovalStroke.Color = currentColors.Stroke
        ovalStroke.Thickness = 2
        ovalStroke.Parent = oval

        local button = Instance.new("TextButton")
        button.Size = UDim2.new(0,100,0,50)
        button.Position = UDim2.new(0.5,-50,0.5,-12.5)
        button.Text = "Toggle Anim"
        button.TextColor3 = currentColors.Text
        button.BackgroundTransparency = 1
        button.Font = Enum.Font.GothamBold
        button.TextSize = 24
        button.Parent = mainFrame

        local bstroke = Instance.new("UIStroke")
        bstroke.Color = currentColors.Stroke
        bstroke.Thickness = 3
        bstroke.Parent = button

        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1,0,0,30)
        label.Position = UDim2.new(0,0,1,-30)
        label.BackgroundTransparency = 1
        label.Text = "Made By R_MP6"
        label.TextColor3 = currentColors.Label
        label.Font = Enum.Font.Gotham
        label.TextSize = 16
        label.Parent = mainFrame

        button.MouseButton1Click:Connect(function()
            isUsingSetA = not isUsingSetA
            currentSet = isUsingSetA and animSetA or animSetB
            if player.Character then
                applyAnimations(player.Character)
            end
        end)
    end
end

-- Main
initializeGUI()
if player.Character then
    isUsingSetA = true
    currentSet = animSetA
    applyAnimations(player.Character)
end

player.CharacterAdded:Connect(function(character)
    isUsingSetA = true
    currentSet = animSetA
    applyAnimations(character)
end)
