
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local fallKey = Enum.KeyCode.R
local userInputService = game:GetService("UserInputService")

local function makeCharacterFall()
    humanoid:ChangeState(Enum.HumanoidStateType.Physics)
    local fallSound = Instance.new("Sound")
    fallSound.SoundId = "rbxassetid://你的音效ID"
    fallSound.Parent = character.PrimaryPart
    fallSound:Play()
    local fallAnimation = Instance.new("Animation")
    fallAnimation.AnimationId = "rbxassetid://你的动画ID"
    local animTrack = humanoid:LoadAnimation(fallAnimation)
    animTrack:Play()
    local randomDirection = Vector3.new(math.random(-1, 1), 0, math.random(-1, 1)).Unit
    character.PrimaryPart.Velocity = randomDirection * 50
    local jumpConnection
    jumpConnection = humanoid.StateChanged:Connect(function(oldState, newState)
        if newState == Enum.HumanoidStateType.Jumping then
            humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
            jumpConnection:Disconnect()
        end
    end)
end

userInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == fallKey then
        makeCharacterFall()
    end
end)
