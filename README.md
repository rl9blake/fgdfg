-- Desenvolvido para testes de IA no Roblox Studio - Uso privado
-- Feito por ChatGPT - 100% Lua (Luau) - Aimbot + ESP + GUI

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local localPlayer = Players.LocalPlayer
local camera = workspace.CurrentCamera

-- CONFIGURAÇÕES
local AimbotTecla = Enum.KeyCode.E
local AimbotAlcance = 30

-- ESTADOS
local aimbotAtivo = false
local espAtivo = false
local desenhosESP = {}

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "AimbotESP_GUI"
gui.ResetOnSpawn = false
gui.Parent = localPlayer:WaitForChild("PlayerGui")

-- Botão ESP
local espButton = Instance.new("TextButton")
espButton.Size = UDim2.new(0, 100, 0, 40)
espButton.Position = UDim2.new(0, 10, 0, 10)
espButton.Text = "ESP: OFF"
espButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
espButton.TextColor3 = Color3.new(1, 1, 1)
espButton.Parent = gui

-- Botão Aimbot
local aimbotButton = Instance.new("TextButton")
aimbotButton.Size = UDim2.new(0, 100, 0, 40)
aimbotButton.Position = UDim2.new(0, 10, 0, 60)
aimbotButton.Text = "Aimbot: OFF"
aimbotButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
aimbotButton.TextColor3 = Color3.new(1, 1, 1)
aimbotButton.Parent = gui

-- Toggle ESP
espButton.MouseButton1Click:Connect(function()
	espAtivo = not espAtivo
	espButton.Text = espAtivo and "ESP: ON" or "ESP: OFF"
end)

-- Toggle Aimbot via botão
aimbotButton.MouseButton1Click:Connect(function()
	aimbotAtivo = not aimbotAtivo
	aimbotButton.Text = aimbotAtivo and "Aimbot: ON" or "Aimbot: OFF"
end)

-- Toggle Aimbot via tecla
UserInputService.InputBegan:Connect(function(input, processed)
	if not processed and input.KeyCode == AimbotTecla then
		aimbotAtivo = not aimbotAtivo
		aimbotButton.Text = aimbotAtivo and "Aimbot: ON" or "Aimbot: OFF"
	end
end)

-- Criar ESP para jogadores
local function criarDesenhos(player)
	if player == localPlayer then return end
	if player.Team == localPlayer.Team then return end

	local t = {
		caixa = Drawing.new("Square"),
		vida = Drawing.new("Line"),
		nome = Drawing.new("Text")
	}

	t.caixa.Thickness = 1
	t.caixa.Color = Color3.fromRGB(255, 0, 0)
	t.caixa.Transparency = 1
	t.caixa.Visible = false

	t.vida.Thickness = 2
	t.vida.Transparency = 1
	t.vida.Visible = false

	t.nome.Size = 16
	t.nome.Center = true
	t.nome.Outline = true
	t.nome.Color = Color3.fromRGB(255, 255, 255)
	t.nome.Visible = false

	desenhosESP[player] = t
end

-- Remover ESP
local function removerDesenhos(player)
	if desenhosESP[player] then
		for _, d in pairs(desenhosESP[player]) do
			d:Remove()
		end
		desenhosESP[player] = nil
	end
end

-- Criar e remover quando players entram/saem
for _, p in ipairs(Players:GetPlayers()) do criarDesenhos(p) end
Players.PlayerAdded:Connect(criarDesenhos)
Players.PlayerRemoving:Connect(removerDesenhos)

-- Achar alvo para Aimbot
local function encontrarAlvo()
	local alvoMaisProximo = nil
	local menorDist = AimbotAlcance

	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= localPlayer and player.Team ~= localPlayer.Team then
			local char = player.Character
			if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
				local hrp = char.HumanoidRootPart
				local humanoid = char.Humanoid
				if humanoid.Health > 0 then
					local distancia = (camera.CFrame.Position - hrp.Position).Magnitude
					local pos, visivel = camera:WorldToViewportPoint(hrp.Position)
					if visivel and distancia < menorDist then
						alvoMaisProximo = hrp
						menorDist = distancia
					end
				end
			end
		end
	end

	return alvoMaisProximo
end

-- Acompanhar e aplicar a mira
local function mirar(alvo)
	if not alvo then return end
	local pos = alvo.Position
	camera.CFrame = CFrame.new(camera.CFrame.Position, pos)
end

-- Loop principal
RunService.RenderStepped:Connect(function()
	-- Aimbot
	if aimbotAtivo then
		local alvo = encontrarAlvo()
		if alvo then
			mirar(alvo)
		end
	end

	-- ESP
	for player, desenho in pairs(desenhosESP) do
		local char = player.Character
		if espAtivo and char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
			local hrp = char.HumanoidRootPart
			local humanoid = char.Humanoid
			local pos, visivel = camera:WorldToViewportPoint(hrp.Position)

			if visivel then
				local dist = (camera.CFrame.Position - hrp.Position).Magnitude
				local scale = math.clamp(1 / dist * 100, 0.5, 2)
				local tamanho = Vector2.new(60 * scale, 100 * scale)

				-- Caixa
				desenho.caixa.Size = tamanho
				desenho.caixa.Position = Vector2.new(pos.X - tamanho.X/2, pos.Y - tamanho.Y/2)
				desenho.caixa.Visible = true

				-- Vida
				local vidaRatio = humanoid.Health / humanoid.MaxHealth
				desenho.vida.From = Vector2.new(pos.X - tamanho.X/2 - 6, pos.Y + tamanho.Y/2)
				desenho.vida.To = Vector2.new(desenho.vida.From.X, desenho.vida.From.Y - tamanho.Y * vidaRatio)
				desenho.vida.Color = Color3.fromRGB(255 * (1 - vidaRatio), 255 * vidaRatio, 0)
				desenho.vida.Visible = true

				-- Nome
				desenho.nome.Position = Vector2.new(pos.X, pos.Y - tamanho.Y/2 - 14)
				desenho.nome.Text = player.Name
				desenho.nome.Visible = true
			else
				desenho.caixa.Visible = false
				desenho.vida.Visible = false
				desenho.nome.Visible = false
			end
		else
			desenho.caixa.Visible = false
			desenho.vida.Visible = false
			desenho.nome.Visible = false
		end
	end
end)
