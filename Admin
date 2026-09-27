local Libary = loadstring(game:HttpGet("https://raw.githubusercontent.com/trakishub/V-rtex-library-/refs/heads/main/Vortex"))()
workspace.FallenPartsDestroyHeight = -math.huge

local Window = Libary:MakeWindow({
    Title = "   Vortex Hub",
    SubTitle = "   By: Vitinwz22",
    LoadText = "Carregando Vortex Hub",
    Flags = "VortexHub"
})

Window:AddMinimizeButton({
    Button = {
        Image = 'rbxassetid://73920359467024',
        BackgroundTransparency = 0,
        Size = UDim2.new(0, 35, 0, 35),
    },
    Corner = {
        CornerRadius = UDim.new(0, 100),
    },
})

--// LED ANIMADO NO BOTÃO ORIGINAL DA ZYRO

local TweenService = game:GetService("TweenService")
local CoreGui = game:GetService("CoreGui")

task.spawn(function()

    -- Espera a interface da Zyro carregar
    local Nexus

    for i = 1, 50 do
        Nexus = CoreGui:FindFirstChild("Nexus Library V1")

        if Nexus then
            break
        end

        task.wait(0.1)
    end

    if not Nexus then
        warn("[Vortex Hub] Nexus Library V1 não encontrado.")
        return
    end

    -- Pega o botão original
    local Button

    for i = 1, 50 do
        Button = Nexus:FindFirstChild("ImageButton")

        if Button then
            break
        end

        task.wait(0.1)
    end

    if not Button then
        warn("[Vortex Hub] Botão da Zyro não encontrado.")
        return
    end

    -- Remove LED antigo caso o script seja executado novamente
    local OldLED = Button:FindFirstChild("TrakisLED")

    if OldLED then
        OldLED:Destroy()
    end

    -- Cria a borda LED
    local LED = Instance.new("UIStroke")
    LED.Name = "VortexLED"
    LED.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    LED.Color = Color3.fromRGB(138, 43, 226) -- Roxo (Purple/BlueViolet)
    LED.Thickness = 2
    LED.Transparency = 0
    LED.Parent = Button

    -- Animação
    task.spawn(function()
        while Button.Parent and LED.Parent do

            local Dim = TweenService:Create(
                LED,
                TweenInfo.new(
                    0.8,
                    Enum.EasingStyle.Sine,
                    Enum.EasingDirection.InOut
                ),
                {
                    Transparency = 0.65,
                    Thickness = 1.5
                }
            )

            Dim:Play()
            Dim.Completed:Wait()

            if not Button.Parent or not LED.Parent then
                break
            end

            local Bright = TweenService:Create(
                LED,
                TweenInfo.new(
                    0.8,
                    Enum.EasingStyle.Sine,
                    Enum.EasingDirection.InOut
                ),
                {
                    Transparency = 0,
                    Thickness = 3
                }
            )

            Bright:Play()
            Bright.Completed:Wait()
        end
    end)
end)

--// RESTO DO SEU SCRIPT CONTINUA AQUI


local InfoTab = Window:MakeTab({ Title = "Info", Icon = "rbxassetid://15309138473" })

InfoTab:AddSection({ "Informações do Script" })
InfoTab:AddParagraph({ "Owner / Developer:", "Zyronis" })
InfoTab:AddParagraph({ "Collaboration:", "Lolytadev, Rick/Shadow and Bazuka" })
InfoTab:AddParagraph({ "Leaked by:", "Bazuka (eu recriei tudo) se for vazar, deixe meus creditos." })
InfoTab:AddParagraph({ "You are using:", "Zyronis Hub Brookhaven " })
InfoTab:AddParagraph({"Your executor:", executor})

InfoTab:AddSection({ "Rejoin" })
InfoTab:AddButton({
    Name = "Rejoin",
    Callback = function()
        local TeleportService = game:GetService("TeleportService")
        TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, game.Players.LocalPlayer)
    end
})

--painel admin

--// Serviços 
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera
local TextChatService = game:GetService("TextChatService")
local TeleportService = game:GetService("TeleportService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local Debris = game:GetService("Debris")

--// Sistema de VerificaÃ§Ã£o
local USUARIOS_AUTORIZADOS = {
    ["silvaa_lenda"] = true,
    ["patodev_lenda"] = true,
    ["Hey_zPUDIM"] = true,
    [""] = true,
    [""] = true,
    [""] = true,
    [""] = true,
    [""] = true
}

local function UsuarioTemAcesso()
    return USUARIOS_AUTORIZADOS[LocalPlayer.Name:lower()] == true
end

local usuarioAutorizado = UsuarioTemAcesso()

if not usuarioAutorizado then
    print("[Swat hub] UsuÃ¡rio nÃ£o autorizado - FunÃ§Ãµes internas ativas, painel oculto")
else
    print("[Swat hub] UsuÃ¡rio autorizado - Painel visÃ­vel")
end

--// Sistema de Tags - Definir tipos de tags
local TAG_TYPES = {
    DONO = {
        Text = "Dono",
        Color = Color3.fromRGB(255, 215, 0),              -- amarelo 
        GlowColor = Color3.fromRGB(200, 140 , 40),       -- amarelo claro
        TextStrokeColor = Color3.fromRGB(255, 255, 255), -- Branco
        Icon = "rbxassetid://99919616573238"
    },
    ADM = {
        Text = "ADM",
        Color = Color3.fromRGB(255, 215, 0),              -- amarelo 
        GlowColor = Color3.fromRGB(255, 215, 0),       -- amarelo 
        TextStrokeColor = Color3.fromRGB(255, 255, 255), -- Branco
        Icon = "rbxassetid://76588208301730"
    }
}

local Donos = {
    ["Hey_zPUDIM"] = TAG_TYPES.DONO,
    ["silvaa_lenda"] = TAG_TYPES.DONO,
    ["darkizinho9910"] = TAG_TYPES.ADM,
    ["novax0548"] = TAG_TYPES.ADM,
    ["ax7_offbatendo"] = TAG_TYPES.ADM,
    ["murilo_12303"] = TAG_TYPES.ADM,
    [""] = TAG_TYPES.ADM,
}

local Autorizados = {
    [""] = true,
}

local function createTag(player, character)
    if not character then return end
    
    local tagType = Donos[player.Name:lower()]
    
    if not tagType then
        local head = character:FindFirstChild("Head")
        if head then
            local existingTag = head:FindFirstChild("ModTag")
            if existingTag then
                existingTag:Destroy()
            end
        end
        return
    end
    
    local head = character:FindFirstChild("Head")
    if not head then return end
    
    local existingTag = head:FindFirstChild("ModTag")
    if existingTag then
        existingTag:Destroy()
    end

    local tag = Instance.new("BillboardGui")
    tag.Name = "ModTag"
    tag.Adornee = head
    tag.Size = UDim2.new(0, 120, 0, 80)
    tag.StudsOffset = Vector3.new(0, 2.5, 0)
    tag.AlwaysOnTop = true
    tag.MaxDistance = 80
    tag.Parent = head

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundTransparency = 1
    frame.Parent = tag

    local backgroundColor = tagType.Color
    local glowColor = tagType.GlowColor
    local textStrokeColor = tagType.TextStrokeColor
    local tagText = tagType.Text
    local iconId = tagType.Icon

    local bg = Instance.new("Frame")
    bg.Size = UDim2.new(0, 80, 0, 25)
    bg.AnchorPoint = Vector2.new(0.5, 0.5)
    bg.Position = UDim2.new(0.5, 0, 0.8, 0)
    bg.BackgroundColor3 = backgroundColor
    bg.BackgroundTransparency = 0.50
    bg.BorderSizePixel = 0
    bg.Parent = frame

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 12)
    corner.Parent = bg

    local glow = Instance.new("UIStroke")
    glow.Thickness = 1.5
    glow.Color = glowColor
    glow.Transparency = 0.3
    glow.Parent = bg

    local text = Instance.new("TextLabel")
    text.Size = UDim2.new(1, 0, 1, 0)
    text.BackgroundTransparency = 1
    text.Text = tagText
    text.Font = Enum.Font.GothamBold
    text.TextScaled = true
    text.TextColor3 = Color3.fromRGB(255, 255, 255)
    text.TextStrokeTransparency = 0.4
    text.TextStrokeColor3 = textStrokeColor
    text.Parent = bg

    local icon = Instance.new("ImageLabel")
    icon.Name = "Icon"
    icon.Size = UDim2.new(0, 25, 0, 25)
    icon.AnchorPoint = Vector2.new(0.5, 0.5)
    icon.Position = UDim2.new(0.5, 0, 0.35, 0)
    icon.BackgroundTransparency = 1
    icon.Image = iconId
    icon.ImageColor3 = Color3.fromRGB(255, 255, 255)
    icon.Parent = frame
end

local function onPlayerAdded(player)
    player.CharacterAdded:Connect(function(char)
        task.wait(0.2)
        createTag(player, char)
    end)
    if player.Character then
        createTag(player, player.Character)
    end
end

Players.PlayerAdded:Connect(onPlayerAdded)
for _, plr in ipairs(Players:GetPlayers()) do
    onPlayerAdded(plr)
end

--// Sistema de Comandos via Chat (SEMPRE ATIVO)
local playerOriginalSpeed = {}
local jaulas = {}
local jailConnections = {}

local function EnviarComando(text, alvo)
    local canal = TextChatService.TextChannels:FindFirstChild("RBXGeneral")
    if canal then
        if alvo then
            canal:SendAsync(text .. " " .. alvo)
        else
            canal:SendAsync(text)
        end
    else
        warn("Canal RBXGeneral nÃ£o encontrado!")
    end
end

local function ExecutarComando(msgText, autor)
    if not Donos[autor:lower()] then return end
    local playerName = LocalPlayer.Name:lower()
    local character = LocalPlayer.Character
    local humanoid = character and character:FindFirstChildOfClass("Humanoid")

    if msgText:match(";kick%s+" .. playerName) then
        LocalPlayer:Kick("kickado by anonymus hub ðŸ¤£ðŸ–•")
    end
    
    if msgText:match(";kill%s+" .. playerName) then
        if character then character:BreakJoints() end
    end
    
    if msgText:match(";killplus%s+" .. playerName) then
        if character then
            character:BreakJoints()
            local root = character:FindFirstChild("HumanoidRootPart")
            if root then
                for i = 1, 10 do
                    local part = Instance.new("Part")
                    part.Size = Vector3.new(10,10,10)
                    part.Anchored = false
                    part.CanCollide = false
                    part.Material = Enum.Material.Neon
                    part.BrickColor = BrickColor.Random()
                    part.CFrame = root.CFrame
                    part.Parent = workspace
                    local bv = Instance.new("BodyVelocity")
                    bv.Velocity = Vector3.new(math.random(-50,50), math.random(20,80), math.random(-50,50))
                    bv.MaxForce = Vector3.new(1e5, 1e5, 1e5)
                    bv.Parent = part
                    game.Debris:AddItem(part, 3)
                end
            end
        end
    end

    if msgText:match(";explode%s+" .. playerName) then
        if character then
            local root = character:FindFirstChild("HumanoidRootPart")
            if root then
                local explosion = Instance.new("Explosion")
                explosion.Position = root.Position
                explosion.BlastRadius = 10
                explosion.BlastPressure = 500000
                explosion.DestroyJointRadiusPercent = 1
                explosion.Parent = workspace
            end
        end
    end

    if msgText:match(";fling%s+" .. playerName) then
        pcall(function()
            if character then
                local root = character:FindFirstChild("HumanoidRootPart")
                if root then
                    local targetCFrame = CFrame.new(50000, 5000000, 3972823)
                    TweenService:Create(root, TweenInfo.new(2, Enum.EasingStyle.Linear), {CFrame = targetCFrame}):Play()
                end
            end
        end)
    end

    if msgText:match(";crash%s+" .. playerName) then
        while true do
            Instance.new("Part").Parent = workspace
        end
    end

    if msgText:match(";freeze%s+" .. playerName) then
        if humanoid then
            playerOriginalSpeed[playerName] = humanoid.WalkSpeed
            humanoid.WalkSpeed = 0
        end
    end

    if msgText:match(";unfreeze%s+" .. playerName) then
        if humanoid then
            humanoid.WalkSpeed = playerOriginalSpeed[playerName] or 16
            playerOriginalSpeed[playerName] = nil
        end
    end

    if msgText:match(";verifique") then
        pcall(function()
            local channel = TextChatService.TextChannels:FindFirstChild("RBXGeneral")
            if channel then
                channel:SendAsync("anonymus_####")
            end
        end)
    end

    if msgText:match(";bring%s+" .. playerName) then
        local chatter = Players:FindFirstChild(autor)
        local targetPlayer = LocalPlayer

        if chatter and chatter.Character and chatter.Character:FindFirstChild("HumanoidRootPart") 
        and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
            targetPlayer.Character:SetPrimaryPartCFrame(chatter.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -5))
        end
    end

    if msgText:match(";jail%s+" .. playerName) then
        if character then
            local root = character:FindFirstChild("HumanoidRootPart")
            if root then
                local model = Instance.new("Model", workspace)
                model.Name = LocalPlayer.Name.."_Jail"
                for i = -1,1,2 do
                    local wall = Instance.new("Part")
                    wall.Size = Vector3.new(1,10,10)
                    wall.Anchored = true
                    wall.CFrame = root.CFrame * CFrame.new(i*5,0,0)
                    wall.Parent = model
                end
                for i = -1,1,2 do
                    local wall = Instance.new("Part")
                    wall.Size = Vector3.new(10,10,1)
                    wall.Anchored = true
                    wall.CFrame = root.CFrame * CFrame.new(0,0,i*5)
                    wall.Parent = model
                end
                local roof = Instance.new("Part")
                roof.Size = Vector3.new(10,1,10)
                roof.Anchored = true
                roof.CFrame = root.CFrame * CFrame.new(0,5,0)
                roof.Parent = model
            end
        end
    end

    if msgText:match(";unjail%s+" .. playerName) then
        local jail = workspace:FindFirstChild(LocalPlayer.Name.."_Jail")
        if jail then jail:Destroy() end
    end
end

local function ConectarChat()
    for _, channel in pairs(TextChatService.TextChannels:GetChildren()) do
        if channel:IsA("TextChannel") then
            channel.MessageReceived:Connect(function(message)
                if message.TextSource and message.Text then
                    ExecutarComando(message.Text:lower(), message.TextSource.Name)
                end
            end)
        end
    end
end

ConectarChat()
TextChatService.TextChannels.ChildAdded:Connect(function(channel)
    if channel:IsA("TextChannel") then
        channel.MessageReceived:Connect(function(message)
            if message.TextSource and message.Text then
                ExecutarComando(message.Text:lower(), message.TextSource.Name)
            end
        end)
    end
end)

LocalPlayer.CharacterAdded:Connect(function()
    task.wait(0.5)
    ConectarChat()
end)



-- SISTEMA DO MONSTRO DAS BACKROOMS
local backroomsMonster = nil
local monsterActive = false
local backroomsFolder = nil

-- FUNÃ‡ÃƒO PARA CRIAR O MONSTRO COM IMAGEM
local function CreateBackroomsMonster(position)
    local monsterFolder = Instance.new("Folder")
    monsterFolder.Name = "BackroomsMonster"
    
    -- Criar parte principal do monstro
    local monsterPart = Instance.new("Part")
    monsterPart.Name = "MonsterBody"
    monsterPart.Size = Vector3.new(8, 12, 8)
    monsterPart.Position = position
    monsterPart.Anchored = true
    monsterPart.CanCollide = true
    monsterPart.Material = Enum.Material.SmoothPlastic
    monsterPart.BrickColor = BrickColor.new("Dark green")
    monsterPart.Parent = monsterFolder
    
    -- Criar decal/textura com a imagem do monstro (NOVA IMAGEM)
    local monsterDecal = Instance.new("Decal")
    monsterDecal.Name = "MonsterFace"
    monsterDecal.Texture = "rbxassetid://136213845438136"
    monsterDecal.Face = Enum.NormalId.Front
    monsterDecal.Parent = monsterPart
    
    -- Adicionar decal nas outras faces tambÃ©m
    local decalBack = Instance.new("Decal")
    decalBack.Texture = "rbxassetid://136213845438136"
    decalBack.Face = Enum.NormalId.Back
    decalBack.Parent = monsterPart
    
    local decalLeft = Instance.new("Decal")
    decalLeft.Texture = "rbxassetid://136213845438136"
    decalLeft.Face = Enum.NormalId.Left
    decalLeft.Parent = monsterPart
    
    local decalRight = Instance.new("Decal")
    decalRight.Texture = "rbxassetid://136213845438136"
    decalRight.Face = Enum.NormalId.Right
    decalRight.Parent = monsterPart
    
    -- Luz verde assustadora (COR ALTERADA)
    local monsterLight = Instance.new("PointLight")
    monsterLight.Brightness = 5
    monsterLight.Range = 20
    monsterLight.Color = Color3.fromRGB(0, 255, 0)
    monsterLight.Parent = monsterPart
    
    -- PartÃ­culas de fumaÃ§a verde (COR ALTERADA)
    local smokeParticles = Instance.new("ParticleEmitter")
    smokeParticles.Texture = "rbxassetid://243664672"
    smokeParticles.Lifetime = NumberRange.new(1, 3)
    smokeParticles.Rate = 25
    smokeParticles.SpreadAngle = Vector2.new(45, 45)
    smokeParticles.Speed = NumberRange.new(2, 4)
    smokeParticles.Color = ColorSequence.new(Color3.fromRGB(0, 255, 0))
    smokeParticles.Transparency = NumberSequence.new(0.3, 0.8)
    smokeParticles.Size = NumberSequence.new(1, 3)
    smokeParticles.Parent = monsterPart
    
    -- Som do monstro
    local monsterSound = Instance.new("Sound")
    monsterSound.SoundId = "rbxassetid://138873214826309"
    monsterSound.Volume = 1.5
    monsterSound.Looped = true
    monsterSound.Parent = monsterPart
    monsterSound:Play()
    
    -- Efeito de pulsaÃ§Ã£o na luz (COR ALTERADA)
    coroutine.wrap(function()
        while monsterPart.Parent do
            monsterLight.Brightness = 8
            wait(0.5)
            monsterLight.Brightness = 3
            wait(0.5)
        end
    end)()
    
    return monsterFolder
end

-- FUNÃ‡ÃƒO PARA ATIVAR O MONSTRO
local function ActivateMonster(player)
    -- VERIFICAR SE Ã‰ DONO OU ADM
    if not Donos[player.Name:lower()] then
        warn("Acesso negado: Apenas donos e ADMs podem usar este comando")
        return
    end
    
    if not player or not player.Character then return end
    
    local humanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then return end
    
    -- Criar monstro se nÃ£o existir
    if not backroomsMonster then
        local monsterPosition = humanoidRootPart.Position + Vector3.new(25, 0, 0)
        backroomsMonster = CreateBackroomsMonster(monsterPosition)
        backroomsMonster.Parent = workspace
    end
    
    monsterActive = true
    
    -- Sistema de perseguiÃ§Ã£o do monstro
    local monsterBody = backroomsMonster:FindFirstChild("MonsterBody")
    if not monsterBody then return end
    
    -- Jumpscare inicial apÃ³s 2 segundos
    task.wait(2)
    
    -- Criar jumpscare assustador (NOVA IMAGEM)
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "MonsterJumpscare"
    screenGui.IgnoreGuiInset = true
    screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    screenGui.Parent = game:GetService("CoreGui") or LocalPlayer:WaitForChild("PlayerGui")
    
    local imageLabel = Instance.new("ImageLabel")
    imageLabel.Size = UDim2.new(1, 0, 1, 0)
    imageLabel.Position = UDim2.new(0, 0, 0, 0)
    imageLabel.BackgroundColor3 = Color3.new(0, 0, 0)
    imageLabel.BackgroundTransparency = 0
    imageLabel.Image = "rbxassetid://136213845438136"
    imageLabel.ScaleType = Enum.ScaleType.Fit
    imageLabel.ImageTransparency = 1
    imageLabel.Parent = screenGui
    
    -- Som do jumpscare
    local scareSound = Instance.new("Sound")
    scareSound.SoundId = "rbxassetid://138873214826309"
    scareSound.Volume = 2.5
    scareSound.Looped = false
    scareSound.Parent = screenGui
    
    -- AnimaÃ§Ã£o do jumpscare
    coroutine.wrap(function()
        imageLabel.ImageTransparency = 0
        scareSound:Play()
        
        -- Efeito de pulsaÃ§Ã£o
        for i = 1, 6 do
            imageLabel.Size = UDim2.new(1.1, 0, 1.1, 0)
            wait(0.1)
            imageLabel.Size = UDim2.new(1, 0, 1, 0)
            wait(0.1)
        end
        
        -- Fade out
        for i = 1, 10 do
            imageLabel.ImageTransparency = i / 10
            wait(0.05)
        end
        
        scareSound:Stop()
        screenGui:Destroy()
    end)()
    
    -- Mensagem de alerta (COR ALTERADA)
    game:GetService("StarterGui"):SetCore("ChatMakeSystemMessage", {
        Text = " O MONSTRO DAS BACKROOMS TE VIU! FUJA!",
        Color = Color3.fromRGB(0, 255, 0),
        Font = Enum.Font.GothamBold
    })

    -- Sistema de perseguiÃ§Ã£o
    while monsterActive and player.Character and player.Character:FindFirstChild("HumanoidRootPart") do
        local playerPos = player.Character.HumanoidRootPart.Position
        local monsterPos = monsterBody.Position
        
        -- Calcular direÃ§Ã£o para o jogador
        local direction = (playerPos - monsterPos).Unit
        local newPosition = monsterPos + (direction * 2.5)
        
        -- Atualizar posiÃ§Ã£o do monstro
        monsterBody.Position = newPosition
        
        -- Fazer o monstro sempre olhar para o jogador
        monsterBody.CFrame = CFrame.new(newPosition, playerPos)
        
        -- Verificar se o monstro alcanÃ§ou o jogador
        if (playerPos - newPosition).Magnitude < 8 then
            -- Efeito visual antes de matar (COR ALTERADA)
            local killEffect = Instance.new("Part")
            killEffect.Size = Vector3.new(10, 10, 10)
            killEffect.Position = playerPos
            killEffect.Anchored = true
            killEffect.CanCollide = false
            killEffect.Material = Enum.Material.Neon
            killEffect.BrickColor = BrickColor.new("Lime green")
            killEffect.Transparency = 0.7
            killEffect.Parent = workspace
            
            local killLight = Instance.new("PointLight")
            killLight.Brightness = 15
            killLight.Range = 15
            killLight.Color = Color3.fromRGB(0, 255, 0)
            killLight.Parent = killEffect
            
            -- Matar o jogador
            if player.Character then
                player.Character:BreakJoints()
                
                -- Som de morte
                local deathSound = Instance.new("Sound")
                deathSound.SoundId = "rbxassetid://143942090"
                deathSound.Volume = 1.5
                deathSound.Parent = workspace
                deathSound:Play()
                
                game:GetService("Debris"):AddItem(deathSound, 3)
                game:GetService("Debris"):AddItem(killEffect, 2)
                
                -- Mensagem de morte (COR ALTERADA)
                game:GetService("StarterGui"):SetCore("ChatMakeSystemMessage", {
                    Text = " O MONSTRO DAS BACKROOMS TE PEGOU! VOCÃŠ MORREU!",
                    Color = Color3.fromRGB(0, 255, 0),
                    Font = Enum.Font.GothamBold
                })
                
                break
            end
        end
        
        wait(0.1)
    end
end

-- FUNÃ‡ÃƒO PARA DESATIVAR O MONSTRO
local function DeactivateMonster()
    -- VERIFICAR SE Ã‰ DONO OU ADM
    if not Donos[LocalPlayer.Name:lower()] then
        warn("Acesso negado: Apenas donos e ADMs podem usar este comando")
        return
    end
    
    monsterActive = false
    if backroomsMonster then
        backroomsMonster:Destroy()
        backroomsMonster = nil
    end
end

-- FUNÃ‡ÃƒO PARA CRIAR BACKROOMS COM MAPA
local function CreateBackrooms()
    local existingFolder = workspace:FindFirstChild("LightClient_Backrooms")
    if existingFolder then
        existingFolder:Destroy()
    end
    
    backroomsFolder = Instance.new("Folder")
    backroomsFolder.Name = "LightClient_Backrooms"
    backroomsFolder.Parent = workspace
    
    -- Carregar mapa das Backrooms (ID: 10581711055)
    local mapID = 10581711055
    local distantPosition = Vector3.new(0, 10000, 0)
    local teleportPosition = Vector3.new(59.06, 9996.70, 19.42)
    
    local success, mapa = pcall(function()
        return game:GetObjects("rbxassetid://"..mapID)[1]
    end)
    
    if success and mapa then
        mapa.Parent = backroomsFolder
        mapa.Name = "BackroomsMap"
        
        -- Configurar posiÃ§Ã£o do mapa
        if not mapa.PrimaryPart then
            local part = mapa:FindFirstChildWhichIsA("BasePart")
            if part then 
                mapa.PrimaryPart = part 
            end
        end
        
        if mapa.PrimaryPart then
            mapa:SetPrimaryPartCFrame(CFrame.new(distantPosition))
        else
            -- Se nÃ£o tiver PrimaryPart, mover todas as partes
            for _, part in ipairs(mapa:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.Position = part.Position + distantPosition
                end
            end
        end
        
        -- Aplicar iluminaÃ§Ã£o das backrooms (CORES ALTERADAS)
        local lighting = game:GetService("Lighting")
        lighting.Brightness = 0.6
        lighting.Ambient = Color3.fromRGB(100, 255, 100)
        lighting.OutdoorAmbient = Color3.fromRGB(100, 255, 100)
        lighting.FogColor = Color3.fromRGB(100, 255, 100)
        lighting.FogEnd = 250
        lighting.FogStart = 50
        
        -- Adicionar efeitos sonoros
        local humSound = Instance.new("Sound")
        humSound.SoundId = "rbxassetid://9114825996"
        humSound.Volume = 0.6
        humSound.Looped = true
        humSound.Parent = backroomsFolder
        humSound:Play()
        
        return backroomsFolder, teleportPosition
    else
        -- Fallback: criar backrooms manualmente se o mapa nÃ£o carregar
        local basePosition = Vector3.new(0, -500, 0)
        local roomSize = 100
        local wallHeight = 20
        
        local function createRoom(roomPosition, roomName)
            local roomFolder = Instance.new("Folder")
            roomFolder.Name = roomName
            roomFolder.Parent = backroomsFolder
            
            local function createWall(position, size, name)
                local wall = Instance.new("Part")
                wall.Name = name
                wall.Size = size
                wall.Position = roomPosition + position
                wall.Anchored = true
                wall.CanCollide = true
                wall.Material = Enum.Material.Plastic
                wall.BrickColor = BrickColor.new("Br. yellowish green")
                wall.Parent = roomFolder
                return wall
            end
            
            -- Piso
            local floor = createWall(Vector3.new(0, 0, 0), Vector3.new(roomSize, 1, roomSize), "Floor")
            
            -- Teto
            local ceiling = createWall(Vector3.new(0, wallHeight, 0), Vector3.new(roomSize, 1, roomSize), "Ceiling")
            ceiling.BrickColor = BrickColor.new("Medium green")
            
            -- Paredes
            createWall(Vector3.new(-roomSize/2, wallHeight/2, 0), Vector3.new(2, wallHeight, roomSize), "WestWall")
            createWall(Vector3.new(roomSize/2, wallHeight/2, 0), Vector3.new(2, wallHeight, roomSize), "EastWall")
            createWall(Vector3.new(0, wallHeight/2, -roomSize/2), Vector3.new(roomSize, wallHeight, 2), "NorthWall")
            createWall(Vector3.new(0, wallHeight/2, roomSize/2), Vector3.new(roomSize, wallHeight, 2), "SouthWall")
            
            return roomFolder
        end
        
        -- Criar sala central
        local centralRoom = createRoom(basePosition, "CentralRoom")
        teleportPosition = basePosition + Vector3.new(0, 5, 0)
        
        return backroomsFolder, teleportPosition
    end
end

-- FUNÃ‡ÃƒO PARA TEletransportar PARA BACKROOMS
local function TeleportToBackrooms(player)
    if not Donos[player.Name:lower()] then
        warn("Acesso negado: Apenas donos e ADMs podem usar este comando")
        return false
    end
    
    if not player or not player.Character then
        return false
    end
    
    local humanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then
        return false
    end
    
    -- Criar backrooms
    local backroomsFolder, spawnPosition = CreateBackrooms()
    
    -- Efeito visual de transiÃ§Ã£o (COR ALTERADA)
    local transitionEffect = Instance.new("Part")
    transitionEffect.Name = "BackroomsTransition"
    transitionEffect.Size = Vector3.new(8, 8, 8)
    transitionEffect.Position = humanoidRootPart.Position
    transitionEffect.Anchored = true
    transitionEffect.CanCollide = false
    transitionEffect.Material = Enum.Material.Neon
    transitionEffect.BrickColor = BrickColor.new("Bright green")
    transitionEffect.Transparency = 0.3
    transitionEffect.Parent = workspace
    
    local transitionLight = Instance.new("PointLight")
    transitionLight.Brightness = 8
    transitionLight.Range = 12
    transitionLight.Color = Color3.fromRGB(150, 255, 150)
    transitionLight.Parent = transitionEffect
    
    -- AnimaÃ§Ã£o de teletransporte
    local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(transitionEffect, tweenInfo, {Size = Vector3.new(15, 15, 15), Transparency = 0.8})
    tween:Play()
    
    -- Teletransportar jogador para as backrooms
    humanoidRootPart.CFrame = CFrame.new(spawnPosition)
    
    -- Remover efeito apÃ³s 1 segundo
    game:GetService("Debris"):AddItem(transitionEffect, 1)
    
    -- Ativar o monstro apÃ³s 3 segundos
    task.wait(3)
    ActivateMonster(player)
    
    return true
end

-- ===== FUNÃ‡ÃƒO PARA RESTAURAR MUNDO NORMAL =====
local function RestoreNormalWorld()
    -- VERIFICAR SE Ã‰ DONO OU ADM
    if not Donos[LocalPlayer.Name:lower()] then
        warn("Acesso negado: Apenas donos e ADMs podem usar este comando")
        return
    end
    
    -- Desativar monstro
    DeactivateMonster()
    
    -- Remover backrooms
    local backroomsFolder = workspace:FindFirstChild("LightClient_Backrooms")
    if backroomsFolder then
        backroomsFolder:Destroy()
    end
    
    -- Restaurar configuraÃ§Ãµes de iluminaÃ§Ã£o originais
    local lighting = game:GetService("Lighting")
    lighting.Brightness = 2
    lighting.Ambient = Color3.fromRGB(128, 128, 128)
    lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
    lighting.FogColor = Color3.fromRGB(191, 191, 191)
    lighting.FogEnd = 100000
    lighting.FogStart = 0
end
    

local function ExecutarComandoBackrooms(msgText, autor)
    if not Donos[autor:lower()] then return end
    
        local playerName = LocalPlayer.Name:lower()
    
    -- Comando para enviar para backrooms
    if msgText:match(";backrooms%s+" .. playerName) then
        TeleportToBackrooms(targetPlayer)
    end
    
    -- Comando para ativar monstro
    if msgText:match(";monstro%s+" .. playerName) then
        ActivateMonster(targetPlayer)
    end
    
    -- Comando para restaurar mundo normal
    if msgText:match(";normal%s+" .. playerName) then
        RestoreNormalWorld(targetPlayer)
    end
end


--// PAINEL VISUAL (APENAS PARA AUTORIZADOS)
if usuarioAutorizado then
    
    -- WindUI Loader
    local WindUI = loadstring(game:HttpGet("https://github.com/Footagesus/WindUI/releases/latest/download/main.lua"))()

    WindUI:AddTheme({
    Name = "Black & White Theme",
    
    Background = Color3.fromRGB(0, 0, 0),
    WindowBackground = Color3.fromRGB(10, 10, 10),
    DialogBackground = Color3.fromRGB(15, 15, 15),
    TabBackground = Color3.fromRGB(400, 400, 400),
    ElementBackground = Color3.fromRGB(400, 400, 400),
    PopupBackground = Color3.fromRGB(15, 15, 15),
    
    Accent = Color3.fromRGB(255, 255, 255),
    Outline = Color3.fromRGB(50, 50, 50),
    Text = Color3.fromRGB(255, 255, 255),
    Placeholder = Color3.fromRGB(150, 150, 150),
    Button = Color3.fromRGB(30, 30, 30),
    Icon = Color3.fromRGB(255, 255, 255),
    
    BackgroundTransparency = 0.08,
    Hover = Color3.fromRGB(40, 40, 40),
    WindowShadow = Color3.fromRGB(0, 0, 0),
    
    DialogBackgroundTransparency = 0.08,
    DialogTitle = Color3.fromRGB(255, 255, 255),
    DialogContent = Color3.fromRGB(255, 255, 255),
    DialogIcon = Color3.fromRGB(255, 255, 255),
    
    WindowTopbarButtonIcon = Color3.fromRGB(255, 255, 255),
    WindowTopbarTitle = Color3.fromRGB(255, 255, 255),
    WindowTopbarAuthor = Color3.fromRGB(255, 255, 255),
    WindowTopbarIcon = Color3.fromRGB(255, 255, 255),
    
    TabTitle = Color3.fromRGB(255, 255, 255),
    TabIcon = Color3.fromRGB(255, 255, 255),
    
    ElementTitle = Color3.fromRGB(255, 255, 255),
    ElementDesc = Color3.fromRGB(220, 220, 220),
    ElementIcon = Color3.fromRGB(255, 255, 255),
    
    PopupBackgroundTransparency = 0.08,
    PopupTitle = Color3.fromRGB(255, 255, 255),
    PopupContent = Color3.fromRGB(255, 255, 255),
    PopupIcon = Color3.fromRGB(255, 255, 255),
    
    DialogButton = Color3.fromRGB(40, 40, 40),
    DialogButtonText = Color3.fromRGB(255, 255, 255),
    DialogButtonHover = Color3.fromRGB(60, 60, 60),
    
    PopupButton = Color3.fromRGB(40, 40, 40),
    PopupButtonText = Color3.fromRGB(255, 255, 255),
    PopupButtonHover = Color3.fromRGB(60, 60, 60)
})

local Window = WindUI:CreateWindow({
    Title = "<font color='rgb(255, 215, 0)'> ANONYMUS HUB ADMIN</font>",
    Icon = "rbxassetid://76588208301730",
    Author = "<font color='rgb(255, 255, 255)'>By: silvadev</font>",
    Folder = "ANONYMUS HUB",
    Size = UDim2.fromOffset(580, 480),
    Transparent = true,
    BackgroundImageTransparency = 0.42,
    Theme = "Dark",
    User = {
        Enabled = true
    },
    SideBarWidth = 200,
    HideSearchBar = false,
    ScrollBarEnabled = true,
    HasOutline = true,
    Background = "rbxassetid://99919616573238"
})

Window:EditOpenButton({
    Title = "ANONYMUS HUB",
    Icon = "cloud",
    CornerRadius = UDim.new(0, 16),
    StrokeThickness = 2,
    Color = ColorSequence.new(
        Color3.fromRGB(255, 215, 0),
        Color3.fromRGB(255, 255, 255)
    ),
    OnlyMobile = false,
    Enabled = true,
    Draggable = true,
})

    -- Aba Comandos
    local TabComandos = Window:Tab({ Title = "Comandos", Icon = "terminal", Locked = false })
    local SectionComandos = TabComandos:Section({ Title = "Admin", Icon = "user-cog", Opened = true })

    local TargetName
    local function getPlayersList()
        local t = {}
        for _, p in ipairs(Players:GetPlayers()) do
            table.insert(t, p.Name)
        end
        return t
    end

    local Dropdown = SectionComandos:Dropdown({
        Title = "Selecionar Jogador",
        Values = getPlayersList(),
        Value = "",
        Callback = function(option)
            TargetName = option
        end
    })

    Players.PlayerAdded:Connect(function()
        Dropdown:SetValues(getPlayersList())
    end)
    Players.PlayerRemoving:Connect(function()
        Dropdown:SetValues(getPlayersList())
    end)

    local comandosAlvo = {"kick","kill","killplus","explode","fling","crash","freeze","unfreeze","bring","jail","unjail"}

    for _, cmd in ipairs(comandosAlvo) do
        SectionComandos:Button({
            Title = cmd:upper(),
            Desc = "Envia ;"..cmd.." no chat para o jogador selecionado",
            Callback = function()
                if TargetName then
                    EnviarComando(";"..cmd, TargetName)
                else
                    warn("Nenhum jogador selecionado!")
                end
            end
        })
    end

    -- Aba Verify
    local TabVerify = Window:Tab({ Title = "Verify", Icon = "check", Locked = false })
    local SectionVerify = TabVerify:Section({ Title = "Verificar", Icon = "search", Opened = true })
    SectionVerify:Button({
        Title = "Enviar VerificaÃ§Ã£o",
        Desc = "Envia ;verifique no chat",
        Callback = function()
            EnviarComando(";verifique")
        end
    })

    -- Aba Backrooms
    local TabBackrooms = Window:Tab({ Title = "Backrooms", Icon = "skull", Locked = false })
    local SectionBackrooms = TabBackrooms:Section({ Title = "Sistema Backrooms", Icon = "door-open", Opened = true })

SectionBackrooms:Button({
    Title = "Enviar Jogador para Backrooms",
    Desc = "Teletransporta o jogador selecionado para as backrooms com monstro",
    Callback = function()
        -- VERIFICAR SE Ã‰ DONO OU ADM
        if not Donos[LocalPlayer.Name:lower()] then
            warn("Acesso negado: Apenas donos e ADMs podem usar este comando")
            return
        end
        
        if TargetName then
            local targetPlayer = Players:FindFirstChild(TargetName)
            if targetPlayer then
                TeleportToBackrooms(targetPlayer)
            else
                warn("Jogador nÃ£o encontrado!")
            end
        else
            warn("Nenhum jogador selecionado!")
        end
    end
})

    SectionBackrooms:Button({
        Title = "Ativar Monstro nas Backrooms",
        Desc = "Ativa o monstro para perseguir o jogador selecionado",
        Callback = function()
            if not Donos[LocalPlayer.Name:lower()] then
                warn("Acesso negado: Apenas donos e ADMs podem usar este comando")
                return
            end
            
            if TargetName then
                local targetPlayer = Players:FindFirstChild(TargetName)
                if targetPlayer then
                    ActivateMonster(targetPlayer)
                else
                    warn("Jogador nÃ£o encontrado!")
                end
            else
                warn("Nenhum jogador selecionado!")
            end
        end
    })

    SectionBackrooms:Button({
    Title = "Restaurar Mundo Normal",
    Desc = "Remove backrooms e monstro, restaurando o mundo normal",
    Callback = function()  
        RestoreNormalWorld()
    end
})




    -- Aba Aviso
    local TabInfo = Window:Tab({ Title = "Aviso", Icon = "shield", Locked = false })
    local SectionInfo = TabInfo:Section({ Title = "Aviso do painel admin", Icon = "shield", Opened = true })
    SectionInfo:Button({
        Title = "Nosso painel nÃ£o funciona para users",
        Desc = "Se quiser o acesso ao nosso painel admin compre no nosso servidor do discord",
        Callback = function()
        end
    })

    -- Som final
    local sound = Instance.new("Sound", workspace)
    sound.SoundId = "rbxassetid://8486683243"
    sound.Volume = 0.5
    sound:Play()
    Debris:AddItem(sound, 3)
    
else
    -- UsuÃ¡rio nÃ£o autorizado - apenas carrega funÃ§Ãµes internas
    warn("[Swat hub] Painel oculto - Comandos internos ativos")
end
    
