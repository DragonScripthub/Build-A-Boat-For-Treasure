local Flux = loadstring(game:HttpGet"https://raw.githubusercontent.com/dawid-scripts/UI-Libs/main/fluxlib.txt")()

local win = Flux:Window("Dragon Hub", "Build A Boat For Treasure", Color3.fromRGB(255, 110, 48), Enum.KeyCode.RightControl)
local tab = win:Tab("Player", "http://www.roblox.com/asset/?id=6023426915")

tab:Slider("Player Speed", " SpeedPlayer.", 0, 1000,16,function(s)
game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
end)
tab:Slider("Player Jump", " JumpPlayer.", 0, 1000,16,function(j)
game.Players.LocalPlayer.Character.Humanoid.JumpPower = j
end)
tab:Toggle("Player Fly", " FlyPlayer.", function(fl)
repeat wait()
   until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:findFirstChild("Torso") and game.Players.LocalPlayer.Character:findFirstChild("Humanoid")
local mouse = game.Players.LocalPlayer:GetMouse()
repeat wait() until mouse
local plr = game.Players.LocalPlayer
local torso = plr.Character.Torso
local flying = true
local deb = true
local ctrl = {f = 0, b = 0, l = 0, r = 0}
local lastctrl = {f = 0, b = 0, l = 0, r = 0}
local maxspeed = 50
local speed = 0

function Fly()
local bg = Instance.new("BodyGyro", torso)
bg.P = 9e4
bg.maxTorque = Vector3.new(9e9, 9e9, 9e9)
bg.cframe = torso.CFrame
local bv = Instance.new("BodyVelocity", torso)
bv.velocity = Vector3.new(0,0.1,0)
bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
repeat wait()
plr.Character.Humanoid.PlatformStand = true
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then
speed = speed+.5+(speed/maxspeed)
if speed > maxspeed then
speed = maxspeed
end
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then
speed = speed-1
if speed < 0 then
speed = 0
end
end
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r}
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
else
bv.velocity = Vector3.new(0,0.1,0)
end
bg.cframe = game.Workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad((ctrl.f+ctrl.b)*50*speed/maxspeed),0,0)
until not flying
ctrl = {f = 0, b = 0, l = 0, r = 0}
lastctrl = {f = 0, b = 0, l = 0, r = 0}
speed = 0
bg:Destroy()
bv:Destroy()
plr.Character.Humanoid.PlatformStand = false
end
mouse.KeyDown:connect(function(key)
if key:lower() == "e" then
if flying then flying = false
else
flying = true
Fly()
end
elseif key:lower() == "w" then
ctrl.f = 1
elseif key:lower() == "s" then
ctrl.b = -1
elseif key:lower() == "a" then
ctrl.l = -1
elseif key:lower() == "d" then
ctrl.r = 1
end
end)
mouse.KeyUp:connect(function(key)
if key:lower() == "w" then
ctrl.f = 0
elseif key:lower() == "s" then
ctrl.b = 0
elseif key:lower() == "a" then
ctrl.l = 0
elseif key:lower() == "d" then
ctrl.r = 0
end
end)
Fly()
end)
tab:Label("Power Player.")
tab:Line()
local tab = win:Tab("Game", "http://www.roblox.com/asset/?id=6023426915")
tab:Button("Auto Fram", "Fram-Auto Coins. ถ้าเปิดฟังชั้นนี้แล้วจะไม่สามารถปิดได้.", function()
spawn(function()
    while true do wait(0.0001)
        pcall(function()
            game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
        end)
    end
end)
while true do wait()
    pcall(function()
        for i,v in pairs(game:GetService("Workspace").BoatStages:GetDescendants()) do
            if v.Name == "DarknessPart" then
                for i = 1,10 do
                    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame * CFrame.new(math.random(1,3),1,math.random(1,3))
                    wait()
                end
                wait()
            end
        end
        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").BoatStages.NormalStages.TheEnd.GoldenChest.Trigger.CFrame
        wait(20) --do not change this value | อย่าหาเปลี่ยนค่า
    end)
end
end)
tab:Label("Auto-Fram.")
tab:Line()
tab:Textbox("Spam Messate", "Spam ้อความต่อไปนี้.", true, function(spames)
print ("spamess")
game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(unpack(args))
end)
tab:Toggle("Auto-Spame Messate", "Auto Spame Messate จากข้อความด้านบน!", function(spamess)
_G.ff = false
while _G.ff do wait(1)
local args = {
    [1] = "Spamess",
    [2] = "All"
}

game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(unpack(args))
end
end)
tab:Label("Spame Messate.")
tab:Line()
tab:Button("Common Spin", "สุ่มหล่องระดับ Common.", function()
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Common Chest",
    [2] = 1
}

workspace.ItemBoughtFromShop:InvokeServer(unpack(args))
end)
tab:Button("UnCommon Spin", "สุ่มหล่องระดับ UnCommon.", function()
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Uncommon Chest",
    [2] = 1
}

workspace.ItemBoughtFromShop:InvokeServer(unpack(args))
end)
tab:Button("Rare Spin", "สุ่มหล่องระดับ Rare.", function()
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Rare Chest",
    [2] = 1
}

workspace.ItemBoughtFromShop:InvokeServer(unpack(args))
end)
tab:Button("Epic Spin", "สุ่มหล่องระดับ Epic.", function()
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Epic Chest",
    [2] = 1
}

workspace.ItemBoughtFromShop:InvokeServer(unpack(args))
end)
tab:Button("Legendary Spin", "สุ่มหล่องระดับ Legendary.", function()
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Legendary Chest",
    [2] = 1
}

workspace.ItemBoughtFromShop:InvokeServer(unpack(args))
end)
tab:Label("Spin Chest.")
tab:Line()
