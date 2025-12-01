--[[ Painel "LEST" para spam de comandos diretamente -- NÃO USA LOADSTRING ]]
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local ChatEvents = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents")
local ChatEvent = ChatEvents and ChatEvents:FindFirstChild("SayMessageRequest")

local gui = Instance.new("ScreenGui")
gui.Name = "LestSpamPanel"
gui.Parent = LocalPlayer:FindFirstChildOfClass("PlayerGui") or game.CoreGui

local panel = Instance.new("Frame")
panel.Size = UDim2.new(0, 390, 0, 245)
panel.Position = UDim2.new(0.5, -195, 0.5, -122)
panel.BackgroundColor3 = Color3.fromRGB(18,17,28)
panel.Active = true
panel.Draggable = true
panel.Visible = false
panel.Parent = gui

local title = Instance.new("TextLabel")
title.Text = "LEST"
title.Size = UDim2.new(1,0,0,45)
title.Position = UDim2.new(0,0,0,0)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBlack
title.TextSize = 26
title.TextColor3 = Color3.fromRGB(255,255,255)
title.Parent = panel

local toggle = Instance.new("TextButton")
toggle.Size = UDim2.new(0,110,0,34)
toggle.Position = UDim2.new(1,-118,0,8)
toggle.BackgroundColor3 = Color3.fromRGB(36,150,215)
toggle.Text = "Entrar no Painel"
toggle.TextSize = 18
toggle.Font = Enum.Font.GothamBold
toggle.Parent = gui

local actions = {
    {nome="MAT", cor=Color3.fromRGB(255,174,0), comando="/mat", flag="mat"},
    {nome="RENDER", cor=Color3.fromRGB(47,123,180), comando="/render", flag="render"},
    {nome="FURAR PNEU", cor=Color3.fromRGB(224,49,49), comando="/furarpneu", flag="furar"},
}

local running = {mat=false, render=false, furar=false}

local function spamComando(flag, command, reps, delay)
    running[flag] = true
    for i=1, reps do
        if not running[flag] then break end
        if ChatEvent then
            ChatEvent:FireServer(command, "All")
        end
        task.wait(delay)
    end
    running[flag] = false
end

local function criarBloco(act, posY)
    local bloco = Instance.new("Frame")
    bloco.Parent = panel
    bloco.Size = UDim2.new(0.92,0,0,56)
    bloco.Position = UDim2.new(0.04,0,0,posY)
    bloco.BackgroundColor3 = act.cor
    bloco.BorderSizePixel = 0

    local nomeLabel = Instance.new("TextLabel")
    nomeLabel.Parent = bloco
    nomeLabel.Text = act.nome
    nomeLabel.Font = Enum.Font.GothamBlack
    nomeLabel.TextSize = 17
    nomeLabel.TextColor3 = Color3.fromRGB(255,255,255)
    nomeLabel.BackgroundTransparency = 1
    nomeLabel.Position = UDim2.new(0,10,0,7)
    nomeLabel.Size = UDim2.new(0,110,0,21)

    local delayBox = Instance.new("TextBox")
    delayBox.Parent = bloco
    delayBox.PlaceholderText = "Delay (s)"
    delayBox.Text = "0.01"
    delayBox.Size = UDim2.new(0,53,0,22)
    delayBox.Position = UDim2.new(0,140,0,10)
    delayBox.Font = Enum.Font.Gotham
    delayBox.TextSize = 15
    delayBox.BackgroundColor3 = Color3.fromRGB(36,36,36)
    delayBox.TextColor3 = Color3.fromRGB(255,255,255)
    delayBox.Name = "Delay"

    local repsBox = Instance.new("TextBox")
    repsBox.Parent = bloco
    repsBox.PlaceholderText = "Repetições"
    repsBox.Text = "10"
    repsBox.Size = UDim2.new(0,56,0,22)
    repsBox.Position = UDim2.new(0,201,0,10)
    repsBox.Font = Enum.Font.Gotham
    repsBox.TextSize = 15
    repsBox.BackgroundColor3 = Color3.fromRGB(36,36,36)
    repsBox.TextColor3 = Color3.fromRGB(255,255,255)
    repsBox.Name = "Reps"

    local startBtn = Instance.new("TextButton")
    startBtn.Parent = bloco
    startBtn.Size = UDim2.new(0,43,0,43)
    startBtn.Position = UDim2.new(1,-70,0,7)
    startBtn.Text = "▶️"
    startBtn.BackgroundColor3 = Color3.fromRGB(36,150,215)
    startBtn.TextSize = 24
    startBtn.Font = Enum.Font.GothamBlack

    local stopBtn = Instance.new("TextButton")
    stopBtn.Parent = bloco
    stopBtn.Size = UDim2.new(0,37,0,23)
    stopBtn.Position = UDim2.new(1,-116,0,11)
    stopBtn.Text = "⏹"
    stopBtn.BackgroundColor3 = Color3.fromRGB(90,50,50)
    stopBtn.TextSize = 18
    stopBtn.Font = Enum.Font.GothamBlack

    startBtn.MouseButton1Click:Connect(function()
        local delay = tonumber(delayBox.Text) or 0.01
        local reps = tonumber(repsBox.Text) or 10
        if not running[act.flag] then
            spawn(function()
                spamComando(act.flag, act.comando, reps, delay)
            end)
        end
    end)

    stopBtn.MouseButton1Click:Connect(function()
        running[act.flag] = false
    end)
end

for i, act in ipairs(actions) do
    criarBloco(act, 45 + (i-1)*65)
end

local painelAberto = false
toggle.MouseButton1Click:Connect(function()
    painelAberto = not painelAberto
    panel.Visible = painelAberto
    toggle.Text = painelAberto and "Sair do Painel" or "Entrar no Painel"
end)

-- CÓDIGO COMPLETO "LEST" (copiado, sem loadstring):

-- Início do código do arquivo https://raw.githubusercontent.com/hackandenso/Lest/refs/heads/main/Lest
--[[
Faça aqui o paste do conteúdo do arquivo Lest
--]]

-- Exemplo fictício do conteúdo que seria colado aqui.
-- Se você quiser o código real que está nesse arquivo, peça: "Cole o código do arquivo https://raw.githubusercontent.com/hackandenso/Lest/refs/heads/main/Lest"  
-- ou me envie o conteúdo desse arquivo!
