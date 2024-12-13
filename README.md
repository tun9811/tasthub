LocalPlayer = game:GetService("Players").LocalPlayer
Char = LocalPlayer.Character

_G.AutoFarm = true
local GetQuests = function(N,NB)
    local args = {
        [1] = "StartQuest",
        [2] = N or "BanditQuest1",
        [3] = NB or 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("CommF_"):InvokeServer(unpack(args))    
end;local ChackQ = function()
    local Lv = LocalPlayer.Data.Level
    if Lv.Value >= 1 and Lv.Value <= 10 then
        return {
            ["Mon"] = 'Bandit',
            ["NumQ"] = 'BanditQuest1',
            ["NameQ"] = 1,
            ["CFrameQ"] = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544),
            ["CFrameMon"] = CFrame.new(1196.172, 11.8689699, 1616.95923, -0.309060812, 0, 0.951042235, 0, 1, 0, -0.951042235, 0, -0.309060812)
        }
    elseif Lv.Value >= 11 and Lv.Value <= 14 then
        return {
            ["Mon"] = 'Monkey',
            ["NumQ"] = 'JungleQuest',
            ["NameQ"] = 1,
            ["CFrameQ"] = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0),
            ["CFrameMon"] = CFrame.new(-1619.10632, 21.7005882, 142.148117, 0.342042625, -0.000311157171, 0.939684391, 0.000113111477, 0.99999994, 0.000289957155, -0.939684391, 7.11137545e-06, 0.342042685)
        }
        elseif Lv.Value >= 15 and Lv.Value <= 29 then
        return {
            ["Mon"] = 'Gorilla',
            ["NumQ"] = 'JungleQuest',
            ["NameQ"] = 2,
            ["CFrameQ"] = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0),
            ["CFrameMon"] = CFrame.new(-1249.19006, 4.97732592, -456.189667, 0, 0, -1, 0, 1, 0, 1, 0, 0)
        }
        elseif Lv.Value >= 30 and Lv.Value <= 39 then
        return {
            ["Mon"] = 'Pirate',
            ["NumQ"] = 'PirateQuest',
            ["NameQ"] = 1,
            ["CFrameQ"] = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627),
            ["CFrameMon"] = CFrame.new(-1136.18848, 3.45001364, 3888.21265, 0.956416667, 3.34192727e-08, -0.29200545, 2.64960787e-09, 1, 1.23125787e-07, 0.29200545, -1.18533258e-07, 0.956416667)
        }
        elseif Lv.Value >= 40 and Lv.Value <= 59 then
        return {
            ["Mon"] = 'Brute',
            ["NumQ"] = 'PirateQuest',
            ["NameQ"] = 2,
            ["CFrameQ"] = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627),
            ["CFrameMon"] = CFrame.new(-1397.73499, 13.7513227, 4185.58398, 0.5592103, 0, -0.829025805, 0, 1, 0, 0.829025805, 0, 0.5592103)
        }
        elseif Lv.Value >= 60 and Lv.Value <= 74 then
        return {
            ["Mon"] = 'Desert Bandit',
            ["NumQ"] = 'DesertQuest',
            ["NameQ"] = 1,
            ["CFrameQ"] = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0, 0.573571265, 0, 0.819155693),
            ["CFrameMon"] = CFrame.new(886.707886, 5.58019638, 4462.00635, -0.988810837, 0, 0.149175406, 0, 1, 0, -0.149175406, 0, -0.988810837)
        }
        elseif Lv.Value >= 60 and Lv.Value <= 74 then
        return {
            ["Mon"] = 'Desert Officer',
            ["NumQ"] = 'DesertQuest',
            ["NameQ"] = 2,
            ["CFrameQ"] = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0, 0.573571265, 0, 0.819155693),
            ["CFrameMon"] = CFrame.new(1578.36646, 0.308917493, 4299.2334, -0.707134247, 0, 0.707079291, 0, 1, 0, -0.707079291, 0, -0.707134247)
        }        
    end
end;
(getgenv()).Config = {
    ["FastAttack"] = true,
    ["ClickAttack"] = true
   } 
   
   coroutine.wrap(function()
   local StopCamera = require(game.ReplicatedStorage.Util.CameraShaker)StopCamera:Stop()
       for v,v in pairs(getreg()) do
           if typeof(v) == "function" and getfenv(v).script == game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework then
                for v,v in pairs(debug.getupvalues(v)) do
                   if typeof(v) == "table" then
                       spawn(function()
                           game:GetService("RunService").RenderStepped:Connect(function()
                               if getgenv().Config['FastAttack'] then
                                    pcall(function()
                                        v.activeController.timeToNextAttack = -(math.huge^math.huge^math.huge)
                                        v.activeController.attacking = false
                                        v.activeController.increment = 4
                                        v.activeController.blocking = false   
                                        v.activeController.hitboxMagnitude = 150
                                        v.activeController.humanoid.AutoRotate = true
                                          v.activeController.focusStart = 0
                                          v.activeController.currentAttackTrack = 0
                                        sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRaxNerous", math.huge)
                                    end)
                                end
                            end)
                       end)
                   end
               end
           end
       end
   end)();
   
   spawn(function()
       game:GetService("RunService").RenderStepped:Connect(function()
           if getgenv().Config['ClickAttack'] then
                pcall(function()
                   game:GetService'VirtualUser':CaptureController()
                   game:GetService'VirtualUser':Button1Down(Vector2.new(0,1,0,1))
               end)
           end
       end)
   end)
---บินฟาร์ม--
local TW = function(...)
    local CFrame = {...}
    pcall(function()
        if not _G.StopTween then
            local Distance = (CFrame[1].Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
            Tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/120, Enum.EasingStyle.Cubic),{CFrame = CFrame[1]})
            if _G.StopTween then Tween:Cancel()
            elseif game.Players.LocalPlayer.Character.Humanoid.Health > 0 then Tween:Play() end
            if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("OMG Hub") then
                local Noclip = Instance.new("BodyVelocity")
                Noclip.Name = "OMG Hub"
                Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
                Noclip.MaxForce = Vector3.new(9e99,9e99,9e99)
                Noclip.Velocity = Vector3.new(0,0,0)
            end
        end
    end)
end;local ClearQ = function()
    if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, tostring(ChackQ()["Mon"])) then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
    end
end

spawn(function()
    while wait() do
        pcall(function()
            if _G.AutoFarm then
                local UIQ = LocalPlayer.PlayerGui.Main.Quest
                ClearQ()
                if not UIQ.Visible or UIQ.Visible == false then
                    TW(ChackQ()["CFrameQ"])
                    if (ChackQ()["CFrameQ"].Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 15 then
                        wait(.2)
                        GetQuests(ChackQ()["NumQ"],ChackQ()["NameQ"])
                    end
                else
                    if game:GetService("Workspace").Enemies:FindFirstChild(ChackQ()["Mon"]) then
                        for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if _v.Name == tostring(ChackQ()["Mon"]) and _v:FindFirstChild("Humanoid") and _v:FindFirstChild("HumanoidRootPart") then
                                if _v.Humanoid.Health > 0 then
                                    repeat wait()
                                        TW(_v:FindFirstChild("HumanoidRootPart").CFrame * CFrame.new(5,28,5))
                                        game:GetService("VirtualUser"):CaptureController()
                                        game:GetService("VirtualUser"):Button1Down(Vector2.new(4000,1272))
                                    until not _G.AutoFarm or _G.AutoFarm == false or not _v.Parent or _v.Humanoid.Health <= 0 or not UIQ.Visible or UIQ.Visible == false
                                end
                            end
                        end
                    else
                        Char.HumanoidRootPart.CFrame = ChackQ()["CFrameMon"]
                    end
                end
            end
        end)
    end
end)
_G.AUTOHAKI = true
spawn(function()
	while wait(.1) do
		if _G.AUTOHAKI then 
			if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
				local args = {
					[1] = "Buso"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
		end
	end
end)
