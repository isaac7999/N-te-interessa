local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local backpack = player.Backpack
local UserInputService = game:GetService("UserInputService")

-- Função para simular o pressionamento da tecla F
local function pressF()
    print("Simulando o pressionamento da tecla F...")
    
    -- Simula o clique de F para abrir o inventário
    UserInputService.InputBegan:Fire({
        UserInputType = Enum.UserInputType.Keyboard,
        KeyCode = Enum.KeyCode.F
    })
    
    -- Aguardar o inventário abrir
    wait(1)
    print("Inventário aberto com sucesso.")
end

-- Função para procurar pela tool Uzi ou algo relacionado nas pastas "Tools" ou "Tool"
local function findUziAndEquip()
    print("Procurando por 'Uzi' ou itens relacionados nas pastas 'Tools' ou 'Tool'...")

    local foundTool = nil
    
    -- Procurar na pasta "Tools" ou "Tool" dentro do workspace
    local toolsFolder = workspace:FindFirstChild("Tools") or workspace:FindFirstChild("Tool")
    
    if toolsFolder then
        -- Procurar por ferramentas na pasta "Tools" ou "Tool"
        for _, item in pairs(toolsFolder:GetChildren()) do
            if item:IsA("Tool") and (string.match(item.Name, "Uzi") or string.match(item.Name, "uzi")) then
                foundTool = item
                print("Encontrado item: " .. item.Name)
                break
            end
        end
    else
        print("Não foi encontrada a pasta 'Tools' ou 'Tool' no Workspace.")
    end
    
    -- Caso não tenha encontrado na pasta, procurar no ReplicatedStorage
    if not foundTool then
        print("Procurando em ReplicatedStorage...")
        
        for _, item in pairs(ReplicatedStorage:GetDescendants()) do
            if item:IsA("Tool") and (string.match(item.Name, "Uzi") or string.match(item.Name, "uzi")) then
                foundTool = item
                print("Encontrado item no ReplicatedStorage: " .. item.Name)
                break
            end
        end
    end
    
    if foundTool then
        -- Simula a equipagem da ferramenta (adiciona na Backpack do jogador)
        print("Equipando a ferramenta: " .. foundTool.Name)
        foundTool.Parent = backpack
        print(foundTool.Name .. " equipada com sucesso!")
    else
        print("Nenhuma ferramenta 'Uzi' encontrada no jogo.")
    end
end

-- Executa o processo
pressF()  -- Simula o pressionamento de F
findUziAndEquip()  -- Procura a Uzi e tenta equipá-la
