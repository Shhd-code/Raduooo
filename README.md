local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local LP = Players.LocalPlayer

----------------------------------------------------------------
-- ✦ شاشة الباسورد
----------------------------------------------------------------
local PASS = "MZA"

local _passGui = Instance.new("ScreenGui")
_passGui.Name = "SHPassScreen"
_passGui.IgnoreGuiInset = true
_passGui.ResetOnSpawn = false
_passGui.DisplayOrder = 99999
_passGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
pcall(function() _passGui.Parent = game.CoreGui end)
if not _passGui.Parent then _passGui.Parent = LP:WaitForChild("PlayerGui") end

-- خلفية معتمة
local _overlay = Instance.new("Frame", _passGui)
_overlay.Size = UDim2.new(1, 0, 1, 0)
_overlay.BackgroundColor3 = Color3.fromRGB(5, 3, 12)
_overlay.BackgroundTransparency = 0.15
_overlay.BorderSizePixel = 0

-- البطاقة الرئيسية
local _card = Instance.new("Frame", _passGui)
_card.Size = UDim2.new(0, 340, 0, 210)
_card.AnchorPoint = Vector2.new(0.5, 0.5)
_card.Position = UDim2.new(0.5, 0, 0.5, 0)
_card.BackgroundColor3 = Color3.fromRGB(18, 14, 30)
_card.BackgroundTransparency = 0.05
_card.BorderSizePixel = 0
Instance.new("UICorner", _card).CornerRadius = UDim.new(0, 16)
local _cStroke = Instance.new("UIStroke", _card)
_cStroke.Color = Color3.fromRGB(170, 80, 255)
_cStroke.Thickness = 2
_cStroke.Transparency = 0.2

local _cGrad = Instance.new("UIGradient", _card)
_cGrad.Color = ColorSequence.new(Color3.fromRGB(22, 16, 40), Color3.fromRGB(12, 8, 22))
_cGrad.Rotation = 135

-- العنوان
local _titleLbl = Instance.new("TextLabel", _card)
_titleLbl.Size = UDim2.new(1, 0, 0, 54)
_titleLbl.BackgroundTransparency = 1
_titleLbl.Font = Enum.Font.GothamBlack
_titleLbl.TextSize = 20
_titleLbl.TextColor3 = Color3.fromRGB(255, 255, 255)
_titleLbl.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
_titleLbl.TextStrokeTransparency = 0.5
_titleLbl.Text = "🔐  SH Sound Hub"

local _subLbl = Instance.new("TextLabel", _card)
_subLbl.Size = UDim2.new(1, -20, 0, 22)
_subLbl.Position = UDim2.new(0, 10, 0, 54)
_subLbl.BackgroundTransparency = 1
_subLbl.Font = Enum.Font.GothamBold
_subLbl.TextSize = 14
_subLbl.TextColor3 = Color3.fromRGB(200, 160, 255)
_subLbl.Text = "أدخل الباسورد للمتابعة"

-- صندوق الإدخال
local _box = Instance.new("TextBox", _card)
_box.Size = UDim2.new(1, -32, 0, 40)
_box.Position = UDim2.new(0, 16, 0, 86)
_box.BackgroundColor3 = Color3.fromRGB(28, 22, 45)
_box.BackgroundTransparency = 0.1
_box.BorderSizePixel = 0
_box.Font = Enum.Font.GothamBold
_box.TextSize = 15
_box.TextColor3 = Color3.fromRGB(255, 255, 255)
_box.PlaceholderText = "الباسورد..."
_box.PlaceholderColor3 = Color3.fromRGB(140, 100, 200)
_box.ClearTextOnFocus = false
_box.Text = ""
Instance.new("UICorner", _box).CornerRadius = UDim.new(0, 10)
local _bStroke = Instance.new("UIStroke", _box)
_bStroke.Color = Color3.fromRGB(170, 80, 255)
_bStroke.Transparency = 0.4
_bStroke.Thickness = 1.5

-- رسالة الخطأ
local _errLbl = Instance.new("TextLabel", _card)
_errLbl.Size = UDim2.new(1, -20, 0, 18)
_errLbl.Position = UDim2.new(0, 10, 0, 132)
_errLbl.BackgroundTransparency = 1
_errLbl.Font = Enum.Font.GothamBold
_errLbl.TextSize = 13
_errLbl.TextColor3 = Color3.fromRGB(255, 80, 80)
_errLbl.TextTransparency = 1
_errLbl.Text = "❌ باسورد خاطئ، حاول مرة ثانية"

-- زر الإغلاق (X)
local _closeBtn = Instance.new("TextButton", _card)
_closeBtn.Size = UDim2.new(0, 30, 0, 30)
_closeBtn.Position = UDim2.new(1, -38, 0, 8)
_closeBtn.BackgroundColor3 = Color3.fromRGB(160, 30, 30)
_closeBtn.BackgroundTransparency = 0.1
_closeBtn.BorderSizePixel = 0
_closeBtn.AutoButtonColor = false
_closeBtn.Font = Enum.Font.GothamBold
_closeBtn.Text = "✕"
_closeBtn.TextSize = 15
_closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", _closeBtn).CornerRadius = UDim.new(0, 8)
_closeBtn.MouseEnter:Connect(function()
    TweenService:Create(_closeBtn, TweenInfo.new(0.12), {BackgroundColor3 = Color3.fromRGB(220, 50, 50)}):Play()
end)
_closeBtn.MouseLeave:Connect(function()
    TweenService:Create(_closeBtn, TweenInfo.new(0.12), {BackgroundColor3 = Color3.fromRGB(160, 30, 30)}):Play()
end)
_closeBtn.MouseButton1Click:Connect(function()
    TweenService:Create(_card, TweenInfo.new(0.25, Enum.EasingStyle.Back, Enum.EasingDirection.In),
        {Size = UDim2.new(0, 0, 0, 0), BackgroundTransparency = 1}):Play()
    task.wait(0.3)
    _passGui:Destroy()
end)

-- زر الدخول
local _enterBtn = Instance.new("TextButton", _card)
_enterBtn.Size = UDim2.new(1, -32, 0, 40)
_enterBtn.Position = UDim2.new(0, 16, 0, 156)
_enterBtn.BackgroundColor3 = Color3.fromRGB(110, 50, 200)
_enterBtn.BackgroundTransparency = 0.05
_enterBtn.BorderSizePixel = 0
_enterBtn.AutoButtonColor = false
_enterBtn.Font = Enum.Font.GothamBold
_enterBtn.Text = "✅  دخول"
_enterBtn.TextSize = 16
_enterBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
_enterBtn.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
_enterBtn.TextStrokeTransparency = 0.5
Instance.new("UICorner", _enterBtn).CornerRadius = UDim.new(0, 10)
local _eBG = Instance.new("UIGradient", _enterBtn)
_eBG.Color = ColorSequence.new(Color3.fromRGB(170, 80, 255), Color3.fromRGB(95, 40, 200))
_eBG.Rotation = 90

-- تأثيرات hover
_enterBtn.MouseEnter:Connect(function()
    TweenService:Create(_enterBtn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(140, 70, 230)}):Play()
end)
_enterBtn.MouseLeave:Connect(function()
    TweenService:Create(_enterBtn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(110, 50, 200)}):Play()
end)
_box:GetPropertyChangedSignal("Text"):Connect(function()
    TweenService:Create(_bStroke, TweenInfo.new(0.15), {Transparency = _box.Text ~= "" and 0.05 or 0.4}):Play()
end)

-- منطق التحقق
local _verified = false
local function _checkPass()
    if _box.Text == PASS then
        _verified = true
        TweenService:Create(_card, TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.In),
            {Size = UDim2.new(0, 0, 0, 0), BackgroundTransparency = 1}):Play()
        task.wait(0.35)
        _passGui:Destroy()
    else
        _errLbl.TextTransparency = 0
        TweenService:Create(_box, TweenInfo.new(0.07), {Position = UDim2.new(0, 22, 0, 86)}):Play()
        task.wait(0.07)
        TweenService:Create(_box, TweenInfo.new(0.07), {Position = UDim2.new(0, 10, 0, 86)}):Play()
        task.wait(0.07)
        TweenService:Create(_box, TweenInfo.new(0.07), {Position = UDim2.new(0, 16, 0, 86)}):Play()
        task.delay(2, function()
            TweenService:Create(_errLbl, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
        end)
    end
end

_enterBtn.MouseButton1Click:Connect(_checkPass)
_box.FocusLost:Connect(function(enter) if enter then _checkPass() end end)

-- انتظر التحقق قبل تحميل الباقي
repeat task.wait(0.05) until _verified

----------------------------------------------------------------
-- ✦ السكربت الرئيسي (يعمل فقط بعد الباسورد)
----------------------------------------------------------------

local spamming = false
local selectedTarget = "الكل"

----------------------------------------------------------------
-- remote
----------------------------------------------------------------
local function getRemote()
        local gui = LP.PlayerGui:FindFirstChild("MountedGui")
        if gui then
                for _, v in pairs(gui:GetDescendants()) do
                        if v.Name == "Remote" and v:IsA("RemoteEvent") then
                                return v
                        end
                end
        end
end

local function fireRemote(target, code)
        local r = getRemote()
        if not r then return end
        if target == "الكل" then
                for _, p in pairs(Players:GetPlayers()) do
                        r:FireServer(p, code)
                end
        else
                local p = Players:FindFirstChild(target)
                if p then r:FireServer(p, code) end
        end
end

----------------------------------------------------------------
-- cleanup + root
----------------------------------------------------------------
pcall(function() game.CoreGui.ShahadSoundHub:Destroy() end)

local gui = Instance.new("ScreenGui")
gui.Name = "ShahadSoundHub"
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.Parent = game.CoreGui

----------------------------------------------------------------
-- helpers
----------------------------------------------------------------
local PURPLE_A = Color3.fromRGB(170, 80, 255)
local PURPLE_B = Color3.fromRGB(95, 40, 200)
local PINK     = Color3.fromRGB(255, 90, 180)
local DARK     = Color3.fromRGB(18, 14, 30)
local DARK2    = Color3.fromRGB(28, 22, 45)
local WHITE    = Color3.fromRGB(255, 255, 255)

local function corner(p, r)
        local c = Instance.new("UICorner", p)
        c.CornerRadius = UDim.new(0, r or 12)
        return c
end

local function gradient(p, c1, c2, rot)
        local g = Instance.new("UIGradient", p)
        g.Color = ColorSequence.new(c1, c2)
        g.Rotation = rot or 90
        return g
end

local function stroke(p, col, t, trans)
        local s = Instance.new("UIStroke", p)
        s.Color = col
        s.Thickness = t or 1
        s.Transparency = trans or 0
        s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
        return s
end

-- crisp white text with subtle dark outline for legibility
local function whiteText(lbl)
        lbl.TextColor3 = WHITE
        lbl.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
        lbl.TextStrokeTransparency = 0.55
end

local function glow(p, col)
        local s = Instance.new("UIStroke", p)
        s.Color = col
        s.Thickness = 1.5
        s.Transparency = 0.3
        task.spawn(function()
                while s.Parent do
                        TweenService:Create(s, TweenInfo.new(1.4, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Transparency = 0.75, Thickness = 2.5}):Play()
                        task.wait(1.4)
                        TweenService:Create(s, TweenInfo.new(1.4, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Transparency = 0.3, Thickness = 1.5}):Play()
                        task.wait(1.4)
                end
        end)
        return s
end

local function hoverScale(btn)
        local baseSize = btn.Size
        btn.MouseEnter:Connect(function()
                TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
                        {Size = UDim2.new(baseSize.X.Scale, baseSize.X.Offset, baseSize.Y.Scale, baseSize.Y.Offset + 2)}):Play()
        end)
        btn.MouseLeave:Connect(function()
                TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {Size = baseSize}):Play()
        end)
        btn.MouseButton1Down:Connect(function()
                TweenService:Create(btn, TweenInfo.new(0.08), {Size = UDim2.new(baseSize.X.Scale, baseSize.X.Offset - 2, baseSize.Y.Scale, baseSize.Y.Offset - 2)}):Play()
        end)
        btn.MouseButton1Up:Connect(function()
                TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Size = baseSize}):Play()
        end)
end

local function ripple(btn)
        btn.ClipsDescendants = true
        btn.MouseButton1Down:Connect(function()
                local m = UIS:GetMouseLocation()
                local abs = btn.AbsolutePosition
                local rip = Instance.new("Frame", btn)
                rip.BackgroundColor3 = WHITE
                rip.BackgroundTransparency = 0.6
                rip.BorderSizePixel = 0
                rip.AnchorPoint = Vector2.new(0.5, 0.5)
                rip.Position = UDim2.new(0, m.X - abs.X, 0, m.Y - abs.Y)
                rip.Size = UDim2.new(0, 0, 0, 0)
                corner(rip, 999)
                local size = math.max(btn.AbsoluteSize.X, btn.AbsoluteSize.Y) * 2
                TweenService:Create(rip, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                        {Size = UDim2.new(0, size, 0, size), BackgroundTransparency = 1}):Play()
                task.delay(0.5, function() rip:Destroy() end)
        end)
end

----------------------------------------------------------------
-- 🎧 floating toggle
----------------------------------------------------------------
local toggle = Instance.new("TextButton", gui)
toggle.Size = UDim2.new(0, 52, 0, 52)
toggle.Position = UDim2.new(0.05, 0, 0.4, 0)
toggle.Text = "🎧"
toggle.Font = Enum.Font.GothamBold
toggle.TextSize = 24
toggle.BackgroundColor3 = PURPLE_A
toggle.AutoButtonColor = false
whiteText(toggle)
corner(toggle, 999)
gradient(toggle, PURPLE_A, PINK, 135)
glow(toggle, PURPLE_A)

task.spawn(function()
        while toggle.Parent do
                TweenService:Create(toggle, TweenInfo.new(2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Rotation = 8}):Play()
                task.wait(2)
                TweenService:Create(toggle, TweenInfo.new(2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {Rotation = -8}):Play()
                task.wait(2)
        end
end)

local dragToggle, dragStart, startPos = false, nil, nil
local function update(input)
        local delta = input.Position - dragStart
        local targetPos = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
                startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        TweenService:Create(toggle, TweenInfo.new(0.15, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                {Position = targetPos}):Play()
end

toggle.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                dragToggle = true
                dragStart = input.Position
                startPos = toggle.Position
                input.Changed:Connect(function()
                        if input.UserInputState == Enum.UserInputState.End then
                                dragToggle = false
                        end
                end)
        end
end)

UIS.InputChanged:Connect(function(input)
        if dragToggle and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
                update(input)
        end
end)

----------------------------------------------------------------
-- 🟣 main panel (smaller)
----------------------------------------------------------------
local PANEL_W, PANEL_H = 340, 340

local main = Instance.new("Frame", gui)
main.Size = UDim2.new(0, PANEL_W, 0, PANEL_H)
main.AnchorPoint = Vector2.new(0.5, 0.5)
main.Position = UDim2.new(0.5, 0, 0.5, 0)
main.BackgroundColor3 = DARK
main.BackgroundTransparency = 0.05
main.Active = true
main.Draggable = true
corner(main, 16)
gradient(main, DARK, DARK2, 135)
glow(main, PURPLE_A)

local header = Instance.new("Frame", main)
header.Size = UDim2.new(1, 0, 0, 38)
header.BackgroundColor3 = PURPLE_B
header.BorderSizePixel = 0
corner(header, 16)
gradient(header, PURPLE_A, PINK, 90)

local headerMask = Instance.new("Frame", header)
headerMask.Size = UDim2.new(1, 0, 0.5, 0)
headerMask.Position = UDim2.new(0, 0, 0.5, 0)
headerMask.BackgroundColor3 = PURPLE_B
headerMask.BorderSizePixel = 0
gradient(headerMask, PURPLE_A, PINK, 90)

local title = Instance.new("TextLabel", header)
title.BackgroundTransparency = 1
title.Size = UDim2.new(1, -50, 1, 0)
title.Position = UDim2.new(0, 12, 0, 0)
title.Text = "✦ Shahad Sound Hub 🎵"
title.Font = Enum.Font.GothamBlack
title.TextSize = 15
title.TextXAlignment = Enum.TextXAlignment.Left
whiteText(title)

local closeBtn = Instance.new("TextButton", header)
closeBtn.Size = UDim2.new(0, 26, 0, 26)
closeBtn.Position = UDim2.new(1, -34, 0.5, -13)
closeBtn.Text = "✕"
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 14
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 80, 110)
closeBtn.AutoButtonColor = false
whiteText(closeBtn)
corner(closeBtn, 999)
hoverScale(closeBtn)

local content = Instance.new("Frame", main)
content.Position = UDim2.new(0, 0, 0, 38)
content.Size = UDim2.new(1, 0, 1, -38)
content.BackgroundTransparency = 1

----------------------------------------------------------------
-- open/close
----------------------------------------------------------------
local open = true
local function setOpen(state)
        open = state
        if open then
                main.Visible = true
                main.Size = UDim2.new(0, 0, 0, 0)
                TweenService:Create(main, TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
                        {Size = UDim2.new(0, PANEL_W, 0, PANEL_H)}):Play()
        else
                local t = TweenService:Create(main, TweenInfo.new(0.22, Enum.EasingStyle.Quad, Enum.EasingDirection.In),
                        {Size = UDim2.new(0, 0, 0, 0)})
                t:Play()
                t.Completed:Connect(function() main.Visible = false end)
        end
end

toggle.MouseButton1Click:Connect(function() setOpen(not open) end)
closeBtn.MouseButton1Click:Connect(function() setOpen(false) end)

----------------------------------------------------------------
-- styled button factory (white text, crisp)
----------------------------------------------------------------
local function style(btn, c1, c2)
        c2 = c2 or c1
        btn.BackgroundColor3 = c1
        btn.Font = Enum.Font.GothamBold
        btn.TextSize = 12
        btn.AutoButtonColor = false
        btn.BorderSizePixel = 0
        whiteText(btn)
        corner(btn, 9)
        gradient(btn, c1, c2, 90)
        stroke(btn, WHITE, 1, 0.85)
        hoverScale(btn)
        ripple(btn)
end

----------------------------------------------------------------
-- players list (left column, narrower)
----------------------------------------------------------------
local playerList = Instance.new("ScrollingFrame", content)
playerList.Size = UDim2.new(0, 105, 1, -16)
playerList.Position = UDim2.new(0, 8, 0, 8)
playerList.BackgroundColor3 = Color3.fromRGB(15, 12, 25)
playerList.BackgroundTransparency = 0.15
playerList.ScrollBarThickness = 3
playerList.ScrollBarImageColor3 = PURPLE_A
playerList.BorderSizePixel = 0
playerList.CanvasSize = UDim2.new()
playerList.AutomaticCanvasSize = Enum.AutomaticSize.Y
corner(playerList, 10)
stroke(playerList, PURPLE_A, 1, 0.6)

local pad = Instance.new("UIPadding", playerList)
pad.PaddingTop = UDim.new(0, 5)
pad.PaddingLeft = UDim.new(0, 4)
pad.PaddingRight = UDim.new(0, 4)

local layout = Instance.new("UIListLayout", playerList)
layout.Padding = UDim.new(0, 5)
layout.SortOrder = Enum.SortOrder.LayoutOrder

----------------------------------------------------------------
-- side column
----------------------------------------------------------------
local side = Instance.new("Frame", content)
side.Position = UDim2.new(0, 120, 0, 8)
side.Size = UDim2.new(1, -128, 1, -16)
side.BackgroundTransparency = 1

local label = Instance.new("TextLabel", side)
label.Size = UDim2.new(1, 0, 0, 26)
label.Text = "🎯 المستهدف: الكل"
label.BackgroundColor3 = Color3.fromRGB(40, 30, 65)
label.Font = Enum.Font.GothamBold
label.TextSize = 12
label.BorderSizePixel = 0
whiteText(label)
corner(label, 8)
gradient(label, Color3.fromRGB(50, 35, 80), Color3.fromRGB(30, 22, 50), 90)
stroke(label, PURPLE_A, 1, 0.5)

local box = Instance.new("TextBox", side)
box.Size = UDim2.new(1, 0, 0, 28)
box.Position = UDim2.new(0, 0, 0, 32)
box.Text = "140217738705613"
box.PlaceholderText = "Sound ID..."
box.PlaceholderColor3 = Color3.fromRGB(150, 150, 170)
box.BackgroundColor3 = Color3.fromRGB(25, 20, 40)
box.Font = Enum.Font.GothamMedium
box.TextSize = 12
box.BorderSizePixel = 0
box.ClearTextOnFocus = false
whiteText(box)
corner(box, 8)
stroke(box, PURPLE_A, 1, 0.5)

local boxPad = Instance.new("UIPadding", box)
boxPad.PaddingLeft = UDim.new(0, 8)
boxPad.PaddingRight = UDim.new(0, 8)

box.Focused:Connect(function()
        TweenService:Create(box:FindFirstChildOfClass("UIStroke"), TweenInfo.new(0.2), {Color = PINK, Transparency = 0.1}):Play()
end)
box.FocusLost:Connect(function()
        TweenService:Create(box:FindFirstChildOfClass("UIStroke"), TweenInfo.new(0.2), {Color = PURPLE_A, Transparency = 0.5}):Play()
end)

local play = Instance.new("TextButton", side)
play.Size = UDim2.new(1, 0, 0, 28)
play.Position = UDim2.new(0, 0, 0, 66)
play.Text = "▶  تشغيل"
play.TextSize = 13
style(play, Color3.fromRGB(0, 200, 130), Color3.fromRGB(0, 140, 90))

local spamBtn = Instance.new("TextButton", side)
spamBtn.Size = UDim2.new(1, 0, 0, 28)
spamBtn.Position = UDim2.new(0, 0, 0, 100)
spamBtn.Text = "🚀  سبام"
spamBtn.TextSize = 13
style(spamBtn, Color3.fromRGB(110, 80, 140), Color3.fromRGB(70, 50, 100))

----------------------------------------------------------------
-- library title
----------------------------------------------------------------
local libraryTitle = Instance.new("TextLabel", side)
libraryTitle.Size = UDim2.new(1, 0, 0, 18)
libraryTitle.Position = UDim2.new(0, 4, 0, 134)
libraryTitle.BackgroundTransparency = 1
libraryTitle.Text = "🎶 مكتبة شهد"
libraryTitle.Font = Enum.Font.GothamBlack
libraryTitle.TextSize = 13
libraryTitle.TextXAlignment = Enum.TextXAlignment.Left
whiteText(libraryTitle)

----------------------------------------------------------------
-- songs list (smaller)
----------------------------------------------------------------
local songsFrame = Instance.new("ScrollingFrame", side)
songsFrame.Size = UDim2.new(1, 0, 1, -158)
songsFrame.Position = UDim2.new(0, 0, 0, 156)
songsFrame.BackgroundColor3 = Color3.fromRGB(15, 12, 25)
songsFrame.BackgroundTransparency = 0.15
songsFrame.ScrollBarThickness = 3
songsFrame.ScrollBarImageColor3 = PINK
songsFrame.BorderSizePixel = 0
songsFrame.CanvasSize = UDim2.new()
songsFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
corner(songsFrame, 10)
stroke(songsFrame, PINK, 1, 0.6)

local songsPad = Instance.new("UIPadding", songsFrame)
songsPad.PaddingTop = UDim.new(0, 5)
songsPad.PaddingLeft = UDim.new(0, 5)
songsPad.PaddingRight = UDim.new(0, 5)

local songs = {
        -- ✦ إضافات جديدة ✦
        {"عيوني",                         "78744235126876"},
        {"اشكج",                          "116944711355320"},
        {"مز",                            "129026857772427"},
        {"تعليقاتكم",                     "78556094634466"},
        {"ميعرفون",                       "91461705065460"},
        {"تفعلينه",                       "111347389464575"},
        {"رنندو",                         "118454236095685"},
        {"فارغين",                        "93041149202267"},
        {"شعر",                           "114093342444289"},
        {"قيرل",                          "98538049169426"},
        {"ياس",                           "137961100462597"},
        {"عصفور",                         "100494285375861"},
        {"اهزمك",                         "110422993267192"},
        {"قسمبالله",                      "114290844191754"},
        {"طالعة",                         "106751281188916"},
        {"هعهعهعهعهعهه",                  "136851539077852"},
        {"كهرباء",                        "90515631199924"},
        {"من انا",                        "136061944036711"},
        {"جنكوك",                         "107435326928417"},
        {"ارجل",                          "104866661304289"},
        {"يكرهوني",                       "120512708140731"},
        {"موكل شخص",                      "128326074391182"},
        {"بوعلوش",                        "130232085843697"},
        {"بلوك",                          "131246317659921"},
        {"بسم",                           "133545082327166"},
        {"كنافة",                         "109417861448568"},
        {"محد يسالني شمحتاج",             "132207001013729"},
        {"شلون تتحرش بالكيرل؟",           "125158134915546"},
        {"مفاجأة",                        "113795117051799"},
        {"مو اني",                        "135871744262409"},
        {"نو بلس",                        "106975640364898"},
        {"هذا موطفل",                     "139737419680252"},
        {"هههه متت",                      "76756794343055"},
        {"ستحي عشيباتك",                  "71182450669974"},
        {"فلتو",                          "115407116502174"},
        {"عاا",                           "99669254159811"},
        {"ختفوو",                         "81250662075243"},
        {"باربي",                         "113942681281973"},
        {"شقصدك",                         "105050078279608"},
        {"بابعع",                         "79292296077171"},
        {"جمالي",                         "89882139062414"},
        {"بوسو",                          "95471764423035"},
        {"احتراما لبوك",                  "89798786728523"},
        {"فشلتونه",                       "137005220955237"},
        {"kill me 💀",         "136373350899288"},
        {"cant steal 💎",      "91214368916078"},
        {"هعهعهع 😂",          "140669499902711"},
        {"رعب 👻",             "133594398909422"},
        {"omg hack 💻",        "121670695729530"},
        {"طننننن 🔊",          "17070340316"},
        {"ازعاج 📢",           "7713890963"},
        {"اندلس 🏛️",           "132039307762001"},
        {"كداوت 💥",           "139208046340684"},
        {"شاورما 🌯",          "80487723481385"},
        {"امبيه 😮",           "7657178494"},
        {"نشيد",               "127840997774724"},
        {"ماعرفة",             "112355709978731"},
        {"انجب",               "121555401150981"},
        {"مساعدة",             "140536118901554"},
        {"ءيييءوءي",           "109984662623550"},
        {"فلجر",               "106407090357978"},
        {"اف مسوي قوي",        "79409542007462"},
        {"ذوق سز",             "132580130213636"},
        {"زيج سليمة",          "108738009845992"},
        {"مش محترمة",          "106127140036172"},
        {"دعسناهم",            "131526626444645"},
        {"مواححح",             "91105326510831"},
        {"يا يايايايا",        "77086551992217"},
        {"عسيييرر",            "81043822558284"},
        {"شعر 😭",             "117027323424952"},
        {"ما انسحب منا",       "104302181580123"},
        {"شبييج؟؟",            "120762576337726"},
        {"يليل زعل يعيال",     "85716215961368"},
        {"اكعدد",              "130214797273250"},
        {"اطلع برا",           "130220767255992"},
        {"اويي",               "132148967247772"},
        {"الله يخلي الريس",    "137772793850988"},
        {"اسرار",              "71510214799841"},
        -- ✦ إضافات جديدة ✦
        {"نوانيتواني سيكس",    "73817028129753"},
        {"مكيف",               "1330849332"},
        {"هيهو",               "2664580729"},
        {"رومانصي",            "133069275120209"},
        {"أو ماي",             "110671591479123"},
        {"اوماكاود",           "18143191014"},
        {"لوفيو",              "382544569"},
        {"اا اي كالاللو",      "1837457258"},
        {"هندي",               "130429015275433"},
        {"تركي",               "113227937386311"},
        {"فرنسي",              "107398475872570"},
        {"صلاة",               "126599650423226"},
        {"ميكوميوز",           "76819270320985"},
        {"ميكويورشكي",         "98890468237805"},
        {"ااا",                "95314743444924"},
        {"ميكووو",             "72812231495047"},
        {"ميكودايووا",         "84162815595670"},
        {"بابا",               "139618641613879"},
        {"جديد",               "129399324665670"},
        {"نافخ روحه وصاير شيخ","135409156222389"},
        -- ✦ إضافات شهد الجديدة ✦
        {"اشتاگ",              "106271890575602"},
        {"علكيفي",             "139847877346679"},
        {"اغمض",               "99214057064825"},
        {"شكد",                "136775741963432"},
        {"حب",                 "103364437862340"},
        {"ويلة",               "122778815130580"},
        {"ماريدك",             "125465198315715"},
        {"مقهور",              "113313866676949"},
        {"يخون",               "135516904939463"},
        {"دموعي",              "102061344423921"},
        {"اموت",               "71923758173463"},
        {"حنية",               "118259650236773"},
        {"مجروح",              "78720110715179"},
        {"سدريه",              "117238020171431"},
        {"راديو",              "5958513683"},
        {"راديو 2",            "139054544880574"},
        {"صراخ",               "140336243123684"},
        {"عيد",                "133627178430167"},
        {"شويخ",               "105959819409554"},
        {"اعايدكم",            "80457867765884"},
        {"صدفه",               "79216410317106"},
        {"جمالج",              "126078631771334"},
        {"طبار الجماجم",       "79860899344472"},
        {"خسرني",              "100812988870930"},
        {"ليل",                "122957821960545"},
        {"رسمي",               "89189069089618"},
        {"وسفه",               "77951452994771"},
        {"انساك",              "99391269377766"},
        {"حمود",               "5225783799"},
        {"ميلي",               "133682020019480"},
        -- ✦ إضافات جديدة ✦
        {"سبونج",              "96747038140954"},
        {"تنغساهور",           "117121991980809"},
        {"ماشا",               "128160683925215"},
}

local sl = Instance.new("UIListLayout", songsFrame)
sl.Padding = UDim.new(0, 4)
sl.SortOrder = Enum.SortOrder.LayoutOrder

local palette = {
        {Color3.fromRGB(120, 60, 200), Color3.fromRGB(80, 40, 150)},
        {Color3.fromRGB(200, 70, 140), Color3.fromRGB(140, 40, 100)},
        {Color3.fromRGB(60, 130, 220), Color3.fromRGB(40, 90, 170)},
        {Color3.fromRGB(220, 130, 60), Color3.fromRGB(170, 90, 40)},
        {Color3.fromRGB(60, 180, 160), Color3.fromRGB(40, 130, 120)},
}

for i, s in ipairs(songs) do
        local n, id = s[1], s[2]
        local b = Instance.new("TextButton", songsFrame)
        b.Size = UDim2.new(1, -8, 0, 24)
        b.Text = "  " .. n
        b.TextXAlignment = Enum.TextXAlignment.Left
        b.LayoutOrder = i
        local p = palette[((i - 1) % #palette) + 1]
        style(b, p[1], p[2])

        b.MouseButton1Click:Connect(function()
                box.Text = id
                fireRemote(selectedTarget, id)
                local original = label.BackgroundColor3
                TweenService:Create(label, TweenInfo.new(0.15), {BackgroundColor3 = PINK}):Play()
                task.delay(0.25, function()
                        TweenService:Create(label, TweenInfo.new(0.3), {BackgroundColor3 = original}):Play()
                end)
        end)
end

----------------------------------------------------------------
-- actions
----------------------------------------------------------------
play.MouseButton1Click:Connect(function()
        fireRemote(selectedTarget, box.Text)
end)

spamBtn.MouseButton1Click:Connect(function()
        spamming = not spamming
        if spamming then
                spamBtn.Text = "🛑  إيقاف"
                local g = spamBtn:FindFirstChildOfClass("UIGradient")
                if g then g.Color = ColorSequence.new(Color3.fromRGB(255, 80, 110), Color3.fromRGB(180, 40, 70)) end
        else
                spamBtn.Text = "🚀  سبام"
                local g = spamBtn:FindFirstChildOfClass("UIGradient")
                if g then g.Color = ColorSequence.new(Color3.fromRGB(110, 80, 140), Color3.fromRGB(70, 50, 100)) end
        end

        task.spawn(function()
                while spamming do
                        fireRemote(selectedTarget, box.Text)
                        task.wait(0.5)
                end
        end)
end)

----------------------------------------------------------------
-- players refresh
----------------------------------------------------------------
local function refresh()
        for _, v in pairs(playerList:GetChildren()) do
                if v:IsA("TextButton") then v:Destroy() end
        end

        local all = Instance.new("TextButton", playerList)
        all.Size = UDim2.new(1, -8, 0, 24)
        all.Text = "🌐 الكل"
        all.LayoutOrder = 0
        style(all, PURPLE_A, PURPLE_B)

        all.MouseButton1Click:Connect(function()
                selectedTarget = "الكل"
                label.Text = "🎯 المستهدف: الكل"
        end)

        for i, p in ipairs(Players:GetPlayers()) do
                local b = Instance.new("TextButton", playerList)
                b.Size = UDim2.new(1, -8, 0, 24)
                b.Text = "👤 " .. p.Name
                b.LayoutOrder = i
                style(b, Color3.fromRGB(55, 45, 80), Color3.fromRGB(35, 28, 55))

                b.BackgroundTransparency = 1
                b.TextTransparency = 1
                TweenService:Create(b, TweenInfo.new(0.3 + i * 0.04, Enum.EasingStyle.Quad),
                        {BackgroundTransparency = 0, TextTransparency = 0}):Play()

                b.MouseButton1Click:Connect(function()
                        selectedTarget = p.Name
                        label.Text = "🎯 المستهدف: " .. p.Name
                end)
        end
end

refresh()
Players.PlayerAdded:Connect(refresh)
Players.PlayerRemoving:Connect(refresh)

