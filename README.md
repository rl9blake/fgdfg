-- Roblox ESP com GUI - Feito em Lua (Luau)
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local localPlayer = Players.LocalPlayer
local camera = workspace.CurrentCamera

-- Criar GUI com botão
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ESP_GUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = localPlayer:WaitForChild("PlayerGui")

local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 100, 0, 40)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.Text = "ESP: OFF"
toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.Parent = screenGui

local espAtivo = false
toggleButton.MouseButton1Click:Connect(function()
	espAtivo = not espAtivo
	toggleButton.Text = espAtivo and "ESP: ON" or "ESP: OFF"
end)

-- Guardar os desenhos de ESP
local espDesenhos = {}

function criarESP(player)
	if player == localPlayer then return end

	local dados = {
		caixa = Drawing.new("Square"),
		vida = Drawing.new("Line"),
		nome = Drawing.new("Text")
	}

	dados.caixa.Thickness = 1
	dados.caixa.Color = Color3.fromRGB(255, 0, 0)
	dados.caixa.Transparency = 1
	dados.caixa.Visible = false

	dados.vida.Thickness = 2
	dados.vida.Color = Color3.fromRGB(0, 255, 0)
	dados.vida.Transparency = 1
	dados.vida.Visible = false

	dados.nome.Size = 16
	dados.nome.Color = Color3.fromRGB(255, 255, 255)
	dados.nome.Center = true
	dados.nome.Outline = true
	dados.nome.Visible = false

	espDesenhos[player] = dados
end

function removerESP(player)
	if espDesenhos[player] then
		for _, desenho in pairs(espDesenhos[player]) do
			desenho:Remove()
		end
		espDesenhos[player] = nil
	end
end

for _, player in ipairs(Players:GetPlayers()) do
	criarESP(player)
end

Players.PlayerAdded:Connect(criarESP)
Players.PlayerRemoving:Connect(removerESP)

-- Atualizar ESP a cada frame
RunService.RenderStepped:Connect(function()
	if not espAtivo then
		for _, desenho in pairs(espDesenhos) do
			for _, item in pairs(desenho) do
				item.Visible = false
			end
		end
		return
	end

	for player, desenho in pairs(espDesenhos) do
		local char = player.Character
		if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
			local hrp = char.HumanoidRootPart
			local humanoid = char.Humanoid
			local pos, visivel = camera:WorldToViewportPoint(hrp.Position)

			if visivel then
				local distancia = (camera.CFrame.Position - hrp.Position).Magnitude
				local escala = math.clamp(1 / distancia * 100, 0.5, 2)
				local tamanho = Vector2.new(60 * escala, 100 * escala)

				-- Caixa 2D
				desenho.caixa.Size = tamanho
				desenho.caixa.Position = Vector2.new(pos.X - tamanho.X / 2, pos.Y - tamanho.Y / 2)
				desenho.caixa.Visible = true

				-- Barra de vida
				local vidaPorcentagem = humanoid.Health / humanoid.MaxHealth
				desenho.vida.From = Vector2.new(pos.X - tamanho.X / 2 - 6, pos.Y + tamanho.Y / 2)
				desenho.vida.To = Vector2.new(desenho.vida.From.X, desenho.vida.From.Y - (tamanho.Y * vidaPorcentagem))
				desenho.vida.Color = Color3.fromRGB(255 * (1 - vidaPorcentagem), 255 * vidaPorcentagem, 0)
				desenho.vida.Visible = true

				-- Nome
				desenho.nome.Position = Vector2.new(pos.X, pos.Y - tamanho.Y / 2 - 14)
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
