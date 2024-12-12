local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/1201for/V.G-Hub/main/IMRETARDED"))()
local Window = Library:CreateWindow("Ninja Legends 2")

local AutoClick = false
local AutoSell = false
local AutoFarm = false
local FollowBoss = false

Window:Toggle("Auto Click", function(state)
    AutoClick = state
    while AutoClick do
        wait()
        local args = { [1] = "swingBlade" }
        game:GetService("Players").LocalPlayer.saberEvent:FireServer(unpack(args))
    end
end)

Window:Toggle("Auto Sell", function(state)
    AutoSell = state
    while AutoSell do
        wait()
        for _, v in pairs(game:GetService("Workspace").sellAreaCircles:GetDescendants()) do
            if v:IsA("TouchTransmitter") then
                firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 0)
                wait()
                firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 1)
            end
        end
    end
end)

Window:Toggle("Auto Farm Fragmentos", function(state)
    AutoFarm = state
    while AutoFarm do
        wait()
        -- Adicione o código para auto farm de fragmentos aqui
    end
end)

Window:Toggle("Seguir Boss Ciborgue Elemental", function(state)
    FollowBoss = state
    game:GetService("RunService").Stepped:connect(function()
        if FollowBoss then
            local args = { [1] = "swingBlade" }
            game:GetService("Players").LocalPlayer.saberEvent:FireServer(unpack(args))
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
            for i, v in pairs(game:GetService("Workspace").spawnedBosses["Elemental Cyborg"]:GetDescendants()) do
                if v:IsA("MeshPart") and v.Name ~= "UpperTorso" then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame * CFrame.new(0, 0, 15)
                end
            end
        end
    end)
end)
