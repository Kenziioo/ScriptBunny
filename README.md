local Players = game:GetService("Players")
local InsertService = game:GetService("InsertService")

Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        -- Aguarda o carregamento completo do personagem
        task.wait(1)
        
        -- IDs dos acessórios (substitua por IDs válidos da Toolbox)
        local earsId = 6682339691  -- ID das orelhas de gato
        local tailId = 16884733740  -- ID da cauda de coelho
        local hairId = 105728701340497 -- ID do cabelo
        local shirtId = 17487482975  -- ID da Camisa Branca
        local pantsId = 129459077 -- ID da calça social preta

        -- Função para adicionar acessórios
        local function addAccessory(assetId)
            local success, model = pcall(function()
                return InsertService:LoadAsset(assetId)
            end)
            
            if success and model then
                local accessory = model:GetChildren()[1]
                if accessory and accessory:IsA("Accessory") then
                    accessory.Parent = character
                end
                model:Destroy()
            else
                warn("Falha ao carregar acessório: " .. tostring(assetId))
            end
        end

        -- Função para adicionar roupas
        local function addShirt(assetId)
            local shirt = Instance.new("Shirt")
            shirt.ShirtTemplate = "rbxassetid://" .. assetId
            shirt.Parent = character
        end

        local function addPants(assetId)
            local pants = Instance.new("Pants")
            pants.PantsTemplate = "rbxassetid://" .. assetId
            pants.Parent = character
        end

        local function addHair(assetId)
            local hair = Instance.new("Accessory")
            local hairModel = InsertService:LoadAsset(assetId):GetChildren()[1]
            if hairModel and hairModel:IsA("Accessory") then
                hairModel.Parent = character
            end
        end

        -- Adiciona os acessórios ao personagem
        addAccessory(earsId)
        addAccessory(tailId)
        addHair(hairId)
        addShirt(shirtId)
        addPants(pantsId)
    end)
end)
