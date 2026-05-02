-- Vinom Hub UI Only (Silver Glossy)

local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")

pcall(function()
    CoreGui:FindFirstChild("VinomHub_UI"):Destroy()
end)

-- ألوان فضية لامعة
local C_BG = Color3.fromRGB(30, 30, 35)
local C_SILVER = Color3.fromRGB(220, 220, 230)
local C_SILVER_DARK = Color3.fromRGB(120, 120, 140)
local C_TEXT = Color3.fromRGB(255,255,255)

-- GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "VinomHub_UI"
ScreenGui.Parent = CoreGui
ScreenGui.ResetOnSpawn = false

-- فريم رئيسي
local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.new(0, 320, 0, 400)
Main.Position = UDim2.new(0.5, -160, 0.5, -200)
Main.BackgroundColor3 = C_BG
Main.BorderSizePixel = 0
Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 12)

-- تأثير لمعان (Gradient)
local UIGradient = Instance.new("UIGradient", Main)
UIGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, C_SILVER),
    ColorSequenceKeypoint.new(0.5, C_SILVER_DARK),
    ColorSequenceKeypoint.new(1, C_SILVER)
})
UIGradient.Rotation = 45

-- عنوان
local Title = Instance.new("TextLabel", Main)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "VINOM HUB"
Title.TextColor3 = C_SILVER
Title.Font = Enum.Font.Bangers
Title.TextSize = 22
Title.TextStrokeTransparency = 0.3
Title.TextStrokeColor3 = Color3.fromRGB(255,255,255)

-- أزرار Auto (فضي لامع)

local C_SILVER = Color3.fromRGB(220, 220, 230)
local C_SILVER_DARK = Color3.fromRGB(120, 120, 140)

-- Auto Left
local AutoLeft = Instance.new("TextButton", Main)
AutoLeft.Size = UDim2.new(0.45, 0, 0, 40)
AutoLeft.Position = UDim2.new(0.05, 0, 0, 60)
AutoLeft.Text = "AUTO LEFT"
AutoLeft.TextColor3 = Color3.new(0,0,0)
AutoLeft.Font = Enum.Font.Bangers
AutoLeft.TextSize = 14
AutoLeft.BorderSizePixel = 0
Instance.new("UICorner", AutoLeft)

-- لمعان
local grad1 = Instance.new("UIGradient", AutoLeft)
grad1.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, C_SILVER),
    ColorSequenceKeypoint.new(0.5, C_SILVER_DARK),
    ColorSequenceKeypoint.new(1, C_SILVER)
})
grad1.Rotation = 45

-- Auto Right
local AutoRight = Instance.new("TextButton", Main)
AutoRight.Size = UDim2.new(0.45, 0, 0, 40)
AutoRight.Position = UDim2.new(0.5, 0, 0, 60)
AutoRight.Text = "AUTO RIGHT"
AutoRight.TextColor3 = Color3.new(0,0,0)
AutoRight.Font = Enum.Font.Bangers
AutoRight.TextSize = 14
AutoRight.BorderSizePixel = 0
Instance.new("UICorner", AutoRight)

-- لمعان
local grad2 = Instance.new("UIGradient", AutoRight)
grad2.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, C_SILVER),
    ColorSequenceKeypoint.new(0.5, C_SILVER_DARK),
    ColorSequenceKeypoint.new(1, C_SILVER)
})
grad2.Rotation = 45

-- زر اغلاق
local Close = Instance.new("TextButton", Main)
Close.Size = UDim2.new(0, 30, 0, 30)
Close.Position = UDim2.new(1, -35, 0, 5)
Close.Text = "X"
Close.TextColor3 = Color3.fromRGB(255,120,120)
Close.BackgroundTransparency = 1
Close.Font = Enum.Font.Bangers

Close.MouseButton1Click:Connect(function()
    Main.Visible = false
end)

-- زر فتح
local Open = Instance.new("TextButton", ScreenGui)
Open.Size = UDim2.new(0, 45, 0, 45)
Open.Position = UDim2.new(0.05, 0, 0.3, 0)
Open.Text = "V"
Open.BackgroundColor3 = C_SILVER
Open.TextColor3 = Color3.fromRGB(20,20,20)
Open.Font = Enum.Font.Bangers
Instance.new("UICorner", Open)

Open.MouseButton1Click:Connect(function()
    Main.Visible = not Main.Visible
end)

-- سحب الواجهة
local dragging, dragInput, dragStart, startPos

Main.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = Main.Position
    end
end)

Main.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        Main.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

Main.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)
