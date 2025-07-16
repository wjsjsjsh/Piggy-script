--[[
📌 Feito por Werick Scripts
✅ Compatível com Piggy
🔒 Segura e permitida
]]
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- UI Library
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/3xploitGuy/uilib/main/MainUI.lua"))()
local Window = Library:CreateWindow("Werick Hub - Piggy")

-- ESP Table
local ESP = {}

-- Criar ESP
local function createESP(part, text, color)
    local billboard = Instance.new("BillboardGui", part)
    billboard.Name = "ESP"
    billboard.Size = UDim2.new(0, 100, 0, 30)
    billboard.AlwaysOnTop = true
    billboard.StudsOffset = Vector3.new(0, 2, 0)

    local label = Instance.new("TextLabel", billboard)
    label.Size = UDim2.new(1, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = color
    label.TextScaled = true
end

-- Adicionar ESP
local function toggleESP(name, color)
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("BasePart") and obj.Parent:FindFirstChild("Name") and string.find(obj.Parent.Name, name) then
            if not obj:FindFirstChild("ESP") then
                createESP(obj, obj.Parent.Name, color)
            end
        end
    end
end

-- Main Tab
local MainTab = Window:CreateTab("Main")

MainTab:CreateToggle("ESP da Piggy", function(state)
    if state then
        toggleESP("Piggy", Color3.fromRGB(255, 0, 0))
    else
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("BillboardGui") and v.Name == "ESP" then
                v:Destroy()
            end
        end
    end
end)

MainTab:CreateToggle("ESP dos Jogadores", function(state)
    if state then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= LocalPlayer and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                toggleESP(p.Name, Color3.fromRGB(0, 255, 0))
            end
        end
    else
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("BillboardGui") and v.Name == "ESP" then
                v:Destroy()
            end
        end
    end
end)

MainTab:CreateToggle("ESP das Chaves", function(state)
    if state then
        toggleESP("Key", Color3.fromRGB(255, 255, 0))
    else
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("BillboardGui") and v.Name == "ESP" then
                v:Destroy()
            end
        end
    end
end)

MainTab:CreateButton("Speed Hack (Velocidade 100)", function()
    LocalPlayer.Character.Humanoid.WalkSpeed = 100
end)

MainTab:CreateButton("Fly (Segure ESPAÇO)", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/InfinityHubScript/roblox-scripts/main/fly.lua"))()
end)

MainTab:CreateButton("NoClip (Tecla N para ativar)", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/0zvY3SgS"))()
end)
