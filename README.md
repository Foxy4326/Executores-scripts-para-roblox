-- 🎃 99 Noite na Floresta Hub V5 - Menu + Kill Aura + Auto Diamante + Auto Baú
-- Autor: Vitor / GPT-5

local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")

-- ================= CONFIG =================
local config = {
    killAura = true,
    killAuraRange = 20,
    autoDiamonds = true,
    autoChests = true,
    speedEnabled = true,
}

-- ================= ENTIDADES =================
local entidades = {
    "Bunny","Horse","Kiwi","Polar Bear","Arctic Fox","Frogs","Mammoth","Scorpion",
    "Cultist","Crossbow Cultist","Juggernaut Cultist","Cultist King","Wolf","Alpha Wolf",
    "Bear","Polar Bear","Aliens","Arctic Fox","Frogs","Scorpion","Hellephant","Meteor Crab",
    "Mammoth","The Deer","The Owl","The Ram"
}

-- ================= FUNÇÃO DE NOTIFICAÇÃO SIMPLES =================
local function safeNotify(title,msg)
    print(title..": "..msg)
end

-- ================= KILL AURA =================
task.spawn(function()
    while task.wait(0.1) do
        if config.killAura then
            for _, obj in pairs(Workspace:GetDescendants()) do
                if table.find(entidades,obj.Name) and obj:IsA("Model") then
                    local hrp = obj:FindFirstChild("HumanoidRootPart")
                    local hum = obj:FindFirstChildOfClass("Humanoid")
                    if hrp and hum and (HumanoidRootPart.Position - hrp.Position).Magnitude <= config.killAuraRange then
                        hum.Health = 0
                        HumanoidRootPart.CFrame = hrp.CFrame + Vector3.new(0,3,0)
                    end
                end
            end
        end
    end
end)

-- ================= AUTO DIAMANTE E BAÚ =================
task.spawn(function()
    while task.wait(0.5) do
        for _, obj in pairs(Workspace:GetDescendants()) do
            -- Auto Diamond
            if config.autoDiamonds and obj.Name == "Diamond" then
                local part = obj:IsA("BasePart") and obj or obj:FindFirstChildWhichIsA("BasePart")
                if part and (HumanoidRootPart.Position - part.Position).Magnitude < 10 then
                    HumanoidRootPart.CFrame = part.CFrame + Vector3.new(0,3,0)
                end
            end
            -- Auto Chest
            if config.autoChests and obj.Name == "Chest" then
                local part = obj:IsA("BasePart") and obj or obj:FindFirstChildWhichIsA("BasePart")
                if part and (HumanoidRootPart.Position - part.Position).Magnitude < 10 then
                    HumanoidRootPart.CFrame = part.CFrame + Vector3.new(0,3,0)
                    if obj:FindFirstChild("ClickDetector") then
                        fireclickdetector(obj.ClickDetector)
                    end
                end
            end
        end
    end
end)

-- ================= LOOP SPEED =================
RunService.RenderStepped:Connect(function()
    if config.speedEnabled then
        local hum = Character:FindFirstChildOfClass("Humanoid")
        if hum then hum.WalkSpeed = 21 end
    end
end)

-- ================= MENU FLUTUANTE =================
local gui = Instance.new("ScreenGui", game.CoreGui)
gui.Name = "NoiteFlorestaHub"

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0,200,0,250)
mainFrame.Position = UDim2.new(0.5,-100,0.5,-125)
mainFrame.BackgroundColor3 = Color3.fromRGB(30,30,35)
mainFrame.Visible = false
mainFrame.Parent = gui
Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0,12)

-- Scrolling
local scroll = Instance.new("ScrollingFrame", mainFrame)
scroll.Size = UDim2.new(1,-10,1,-10)
scroll.Position = UDim2.new(0,5,0,5)
scroll.BackgroundTransparency = 1
scroll.ScrollBarThickness = 6
scroll.CanvasSize = UDim2.new(0,0,0,0)

local layout = Instance.new("UIListLayout", scroll)
layout.Padding = UDim.new(0,5)
layout.SortOrder = Enum.SortOrder.LayoutOrder

local function newButton(text,callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1,0,0,35)
    btn.BackgroundColor3 = Color3.fromRGB(50,50,55)
    btn.Text = text
    btn.Font = Enum.Font.SourceSansBold
    btn.TextColor3 = Color3.new(1,1,1)
    btn.TextSize = 14
    btn.Parent = scroll
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0,8)
    btn.MouseButton1Click:Connect(callback)
    task.wait()
    scroll.CanvasSize = UDim2.new(0,0,0,layout.AbsoluteContentSize.Y + 10)
end

-- Botões do menu
newButton("⚔️ Kill Aura", function()
    config.killAura = not config.killAura
    safeNotify("Kill Aura",tostring(config.killAura))
end)

newButton("💎 Auto Diamond", function()
    config.autoDiamonds = not config.autoDiamonds
    safeNotify("Auto Diamond",tostring(config.autoDiamonds))
end)

newButton("📦 Auto Chest", function()
    config.autoChests = not config.autoChests
    safeNotify("Auto Chest",tostring(config.autoChests))
end)

newButton("⚡ Speed Boost", function()
    config.speedEnabled = not config.speedEnabled
    safeNotify("Speed Boost",tostring(config.speedEnabled))
end)

-- Botão flutuante
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0,50,0,50)
toggleButton.Position = UDim2.new(0,10,1,-70)
toggleButton.Text = "📱"
toggleButton.TextSize = 24
toggleButton.BackgroundColor3 = Color3.fromRGB(0,170,255)
toggleButton.TextColor3 = Color3.new(1,1,1)
toggleButton.Font = Enum.Font.SourceSansBold
toggleButton.Parent = gui
Instance.new("UICorner", toggleButton).CornerRadius = UDim.new(1,0)

toggleButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
    safeNotify("Menu",""..(mainFrame.Visible and "Aberto" or "Fechado"))
end)

print("✅ 99 Noite na Floresta Hub carregado! Menu funcional, Kill Aura + Auto Diamond + Auto Chest ativos.")