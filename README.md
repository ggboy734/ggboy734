
本地玩家=game.Players.LocalPlayer
本地字符=玩家。字符或玩家。添加的字符：等待()
局部仿人=字符：WaitForChild("Humanoid")
本地fallKey=枚举.KeyCode.R
本地userInputService=game:GetService("UserInputService")

局部函数makeCharacterFall()
humanoid:changeState(枚举。HumanoidStateType。物理学)
本地fallSound=Instance.new("声音")
fallSound.SoundId="rbxassetid://你的音效ID"
fallSound.Parent=character.PrimaryPart
fallSound：播放()
本地fallAnimation=Instance.new(“动画”)
fallAnimation.AnimationId="rbxassetid://你的动画ID"
局部animTrack=仿人：加载动画(fallAnimation)
animTrack：播放()
本地randomDirection=Vector3.new(math.random(-1，1)，0，math.random(-1，1)).Unit
character.primary Part.Velocity=randomDirection*50
本地jumpConnection
jumpConnection=仿人。stateChanged:Connect(函数(oldstate，newState)
如果newState==枚举.HumanoidStateType.Jumping，则
humanoid:changeState(枚举。HumanoidStateType。getingUp)
jumpConnection:Disconnect()
结束
结束)
结束

userInputService.InputBegin:Connect(函数(输入，gameProcessed)
如果gameProcessed，则返回结束
如果input.KeyCode==fallKey，则
makeCharacterFall()
结束
结束)
