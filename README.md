local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("oceann", "Ocean")
local Combat = Window:NewTab("Combat")
local Movement = Window:NewTab("Movement")
local Other = Window:NewTab("Other")

local MovementSection = Movement:NewSection("Speed")
local CombatSection = Combat:NewSection("Lock")
local OtherSection = Other:NewSection("Trashtalk")
local ServerSection = Other:NewSection("Server")
local MiscSection = Other:NewSection("Misc")
local AntiLockSection = Combat:NewSection("AntiLock")

MovementSection:NewButton("CFrame Speed", "Gives you cframe speed. Zoooooom!", function()
    --SHORTCUTS
local Players = game:GetService("Players")
local Client = Players.LocalPlayer
local RService = game:GetService("RunService")

--SETTINGS
local CFrameSpeedToggeled = true
local CFrameSpeed = 1

RService.Heartbeat:Connect(function()
    if CFrameSpeedToggeled then
        Client.Character.HumanoidRootPart.CFrame = Client.Character.HumanoidRootPart.CFrame + Vector3.new(Client.Character.Humanoid.MoveDirection.X * CFrameSpeed, Client.Character.Humanoid.MoveDirection.Y * CFrameSpeed, Client.Character.Humanoid.MoveDirection.Z * CFrameSpeed)
    end
end)
end)

CombatSection:NewButton("Trace Lock", "Enable Trace Lock", function()
    local Settings = { AimLock = { Enabled = true, Aimlockkey = "q", Prediction = 0.130340, Aimpart = 'HumanoidRootPart', Notifications = true }, Settings = { Thickness = 3.5, Transparency = 1, Color = Color3.fromRGB(106, 13, 173), FOV = true } } local CurrentCamera = game:GetService("Workspace").CurrentCamera local Inset = game:GetService("GuiService"):GetGuiInset().Y local RunService = game:GetService("RunService") local Mouse = game.Players.LocalPlayer:GetMouse() local LocalPlayer = game.Players.LocalPlayer local Line = Drawing.new("Line") local Circle = Drawing.new("Circle") local Plr = game.Players.LocalPlayer Mouse.KeyDown:Connect(function(KeyPressed) if KeyPressed == (Settings.AimLock.Aimlockkey) then if Settings.AimLock.Enabled == true then Settings.AimLock.Enabled = false if Settings.AimLock.Notifications == true then Plr = FindClosestPlayer() game.StarterGui:SetCore("SendNotification", { Title = "p", Text = "Unlocked" }) end else Plr = FindClosestPlayer() Settings.AimLock.Enabled = true if Settings.AimLock.Notifications == true then game.StarterGui:SetCore("SendNotification", { Title = "p", Text = "Locked On : " .. tostring(Plr.Character.Humanoid.DisplayName) }) end end end end) function FindClosestPlayer() local ClosestDistance, ClosestPlayer = math.huge, nil; for _, Player in next, game:GetService("Players"):GetPlayers() do if Player ~= LocalPlayer then local Character = Player.Character if Character and Character.Humanoid.Health > 1 then local Position, IsVisibleOnViewPort = CurrentCamera:WorldToViewportPoint(Character.HumanoidRootPart .Position) if IsVisibleOnViewPort then local Distance = (Vector2.new(Mouse.X, Mouse.Y) - Vector2.new(Position.X, Position.Y)).Magnitude if Distance < ClosestDistance then ClosestPlayer = Player ClosestDistance = Distance end end end end end return ClosestPlayer, ClosestDistance end RunService.Heartbeat:connect(function() if Settings.AimLock.Enabled == true then local Vector = CurrentCamera:WorldToViewportPoint(Plr.Character[Settings.AimLock.Aimpart].Position + (Plr.Character[Settings.AimLock.Aimpart].Velocity * Settings.AimLock.Prediction)) Line.Color = Settings.Settings.Color Line.Transparency = Settings.Settings .Transparency Line.Thickness = Settings.Settings .Thickness Line.From = Vector2.new(Mouse.X, Mouse.Y + Inset) Line.To = Vector2.new(Vector.X, Vector.Y) Line.Visible = true Circle.Position = Vector2.new(Mouse.X, Mouse.Y + Inset) Circle.Visible = Settings.Settings.FOV Circle.Thickness = 1.5 Circle.Thickness = 2 Circle.Radius = 60 Circle.Color = Settings.Settings.Color elseif Settings.AimLock.FOV == true then Circle.Visible = true else Circle.Visible = false Line.Visible = false end end) local mt = getrawmetatable(game) local old = mt.__namecall setreadonly(mt, false) mt.__namecall = newcclosure(function(...) local args = {...} if Settings.AimLock.Enabled and getnamecallmethod() == "FireServer" and args[2] == "MousePos" then args[3] = Plr.Character[Settings.AimLock.Aimpart].Position + (Plr.Character[Settings.AimLock.Aimpart].Velocity * Settings.AimLock.Prediction) return old(unpack(args)) end return old(...) end)
end)


OtherSection:NewKeybind("Trashtalk", "annoy kids", Enum.KeyCode.T, function()
    game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("Get good, Get oceann!", "All")
    game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("Are you sniffing the ground?", "All")
    game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("Start aiming at me, not the sky.", "All")
end)

MovementSection:NewButton("Speed - C", "Press C to go zoooooom!!", function()
	local Player = game:GetService'Players'.LocalPlayer;
	local UIS = game:GetService'UserInputService';
	UIS.InputBegan:connect(function(UserInput)
		if UserInput.UserInputType == Enum.UserInputType.Keyboard and UserInput.KeyCode == Enum.KeyCode.C then
			_G.Running = true
			while wait(0.00001) and _G.Running == true do
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.5
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.5
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.5
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.5
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.5
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.5
			end
		end
	end)
	UIS.InputEnded:connect(function(UserInput)
		if UserInput.UserInputType == Enum.UserInputType.Keyboard and UserInput.KeyCode == Enum.KeyCode.C then
			_G.Running = false
		end
	end)
end)

ServerSection:NewButton("Copy JobId", "Copy servers JobId", function()
    setclipboard(game.JobId)
end)

ServerSection:NewButton("Rejoin", "Rejoins the same server!", function()
    local TPService = game:GetService('TeleportService')
local Client = game.Players.LocalPlayer

Client:Kick("Rejoining")
wait(0.2)
TPService:TeleportToPlaceInstance(game.PlaceId, game.JobId)
end)

MiscSection:NewKeybind("Toggle UI", "Toggles UI", Enum.KeyCode.V, function()
	Library:ToggleUI()
end)

AntiLockSection:NewButton("AntiLock", "Prevent Lockers from hitting you!", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/chrsschrs/antilocks/main/aa"))()
end)
