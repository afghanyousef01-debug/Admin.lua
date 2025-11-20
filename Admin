-- Admin Panel Example
-- Educational / Safe
local Admins = {
    "YourUsernameHere" -- Replace with your Roblox username
}

-- Check if player is admin
local function isAdmin(player)
    for _, name in pairs(Admins) do
        if player.Name == name then
            return true
        end
    end
    return false
end

-- Spawn objects
local function spawnObject(objectName, position)
    local obj
    if objectName == "StrawberryElephant" then
        -- Example custom model
        obj = Instance.new("Part")
        obj.Size = Vector3.new(6,6,6)
        obj.BrickColor = BrickColor.new("Bright red")
        obj.Shape = Enum.PartType.Ball
        local label = Instance.new("BillboardGui", obj)
        label.Size = UDim2.new(0,200,0,50)
        local text = Instance.new("TextLabel", label)
        text.Text = "🍓 Elephant 🍓"
        text.Size = UDim2.new(1,0,1,0)
        text.BackgroundTransparency = 1
        obj.Anchored = true
    else
        obj = Instance.new("Part")
        obj.Size = Vector3.new(4,1,4)
        obj.BrickColor = BrickColor.Random()
        obj.Anchored = true
    end
    obj.Position = position or Vector3.new(0,5,0)
    obj.Parent = workspace
end

-- Admin commands
local function runCommand(player, command, args)
    if not isAdmin(player) then return end
    
    if command == "kick" then
        local target = game.Players:FindFirstChild(args[1])
        if target then
            target:Kick("Kicked by admin")
        end
    elseif command == "teleport" then
        local target = game.Players:FindFirstChild(args[1])
        if target and player.Character and target.Character then
            player.Character:SetPrimaryPartCFrame(target.Character.PrimaryPart.CFrame + Vector3.new(0,3,0))
        end
    elseif command == "spawn" then
        local objectName = args[1] or "Part"
        spawnObject(objectName)
    elseif command == "speed" then
        local speed = tonumber(args[1]) or 16
        if player.Character and player.Character:FindFirstChild("Humanoid") then
            player.Character.Humanoid.WalkSpeed = speed
        end
    end
end

-- Listen to chat for commands
game.Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(msg)
        if msg:sub(1,1) == "!" then
            local args = msg:split(" ")
            local command = args[1]:sub(2)
            table.remove(args,1)
            runCommand(player, command, args)
        end
    end)
end)
