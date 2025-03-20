local Library = loadstring(game:HttpGet("https://github.com/realredz/RedzLibV5/blob/main/Source.lua?raw=true"))()
              Library.Themes.Darker["Color Hub 1"] = ColorSequence.new({
				ColorSequenceKeypoint.new(0.00, Color3.fromRGB()),
				ColorSequenceKeypoint.new(0.50, Color3.fromRGB(5,5,5)),
				ColorSequenceKeypoint.new(1.00, Color3.fromRGB(2,2,2))
			})
			Library.Themes.Darker["Color Hub 2"] = Color3.fromRGB(20,20,20)
			Library.Themes.Darker["Color Stroke"] = Color3.fromRGB(15,15,15)
			Library.Themes.Darker["Color Theme"] = Color3.fromRGB(0,255,100)
			Library.Themes.Darker["Color Text"] = Color3.fromRGB(255,255,255)
			Library.Themes.Darker["Color Dark Text"] = Color3.fromRGB(0,255)

local LibraryESP = loadstring(game:HttpGet("https://github.com/RGV-devid/Scripts/blob/main/ESP?raw=true"))()

local Window = Library:MakeWindow({"YOUHUB | Dead Rails (Game)", "v0.0.1", "testando-redzLibv5.json"})

local Button = Window:AddMinimizeButton({
Button = { ImageColor3 = Color3.fromRGB(0,150,255), Image = "rbxassetid://95869322194132", BackgroundColor3 = Color3.fromRGB(0,100,255), BackgroundTransparency = 0 },
Corner = { CornerRadius = UDim.new(0, 5) },
})
Instance.new("UIStroke", game:GetService("CoreGui")["redz Library V5"].Hub).Color = Color3.fromRGB(0,255,100)

local Tabs = {
Main = Window:MakeTab({"Main"}),
Exploit = Window:MakeTab({"Exploit"}),
Players = Window:MakeTab({"Players"}),
Visual = Window:MakeTab({"Visual"})
}
Tabs.Main:AddSection({"Money"})
Tabs.Main:AddParagraph({"Attention", "Other players can report you, because you can get money of other players."})
Tabs.Main:AddToggle({
Name = "Auto Money Bag",
Callback = function(v)
_G.AutoMoneyBag = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.AutoMoneyBag then
for i, v in ipairs(workspace:GetDescendants()) do
if v.Name == "MoneyBag" then
fireproximityprompt(v.CollectPrompt)
end
end
end
end)
end})
Tabs.Main:AddSection({"Interact"})
Tabs.Main:AddToggle({
Name = "Auto Snake Oil",
Callback = function(v)
_G.AutoSnakeOil = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.AutoSnakeOil then
local args = {
    [1] = workspace.RuntimeItems:FindFirstChild("Snake Oil")
}

game:GetService("ReplicatedStorage").Remotes.Tool.PickUpTool:FireServer(unpack(args))
end
end)
end})
Tabs.Main:AddToggle({
Name = "Auto Bandage",
Callback = function(v)
_G.AutoBandage = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.AutoBandage then
local args = {
    [1] = workspace.RuntimeItems:FindFirstChild("Bandage")
}

game:GetService("ReplicatedStorage").Remotes.Tool.PickUpTool:FireServer(unpack(args))
end
end)
end})
Tabs.Main:AddSection({"Proximity"})
Tabs.Main:AddToggle({
Name = "Higher Interact",
Callback = function(v)
if v then
for _,v in pairs(workspace:GetDescendants()) do
if v:IsA("ProximityPrompt") then
v.MaxActivationDistance = v.MaxActivationDistance + 5
end
end
IncreasedDistance = workspace.DescendantAdded:Connect(function(v)
if v:IsA("ProximityPrompt") then
v.MaxActivationDistance = v.MaxActivationDistance + 5
end
end)
else
IncreasedDistance:Disconnect()
for _,v in pairs(workspace:GetDescendants()) do
if v:IsA("ProximityPrompt") then
v.MaxActivationDistance = v.MaxActivationDistance - 5
end
end
end
end})
Tabs.Main:AddToggle({
Name = "Instance Interact",
Callback = function(v)
if v then
for _,v in pairs(workspace:GetDescendants()) do
if v:IsA("ProximityPrompt") then
v.HoldDuration = 0
end
end
InstanceInteract = workspace.DescendantAdded:Connect(function(v)
if v:IsA("ProximityPrompt") then
v.HoldDuration = 0
end
end)
else
InstanceInteract:Disconnect()
end
end})
Tabs.Main:AddToggle({
Name = "Througher Interact",
Callback = function(v)
if v then
for _,v in pairs(workspace:GetDescendants()) do
if v:IsA("ProximityPrompt") then
v.RequiresLineOfSight = false
end
end
ThroughInteract = workspace.DescendantAdded:Connect(function(v)
if v:IsA("ProximityPrompt") then
v.RequiresLineOfSight = false
end
end)
else
ThroughInteract:Disconnect()
for _,v in pairs(workspace:GetDescendants()) do
if v:IsA("ProximityPrompt") then
v.RequiresLineOfSight = true
end
end
end
end})
Tabs.Main:AddSection({"Auto Use"})
_G.HealthUseSnakeOil = 50
Tabs.Main:AddSlider({
  Name = "Health Use Snake Oil",
  Min = 1,
  Max = 99,
  Increase = 1,
  Default = 50,
  Callback = function(v)
_G.HealthUseSnakeOil = v
end})
Tabs.Main:AddToggle({
Name = "Auto Use Snake Oil (Must Hold)",
Callback = function(v)
_G.AutoUseSnakeOil = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.AutoUseSnakeOil and game.Players.LocalPlayer.Character.Humanoid.Health < _G.HealthUseSnakeOil then
game:GetService("Players").LocalPlayer.Character:FindFirstChild("Snake Oil").Use:FireServer()
end
end)
end})
_G.HealthUseBandage = 50
Tabs.Main:AddSlider({
  Name = "Health Use Bandage",
  Min = 1,
  Max = 99,
  Increase = 1,
  Default = 50,
  Callback = function(v)
_G.HealthUseBandage = v
end})
Tabs.Main:AddToggle({
Name = "Auto Use Bandage (Must Hold)",
Callback = function(v)
_G.AutoUseBandage = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.AutoUseBandage and game.Players.LocalPlayer.Character.Humanoid.Health < _G.HealthUseBandage then
game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bandage").Use:FireServer()
end
end)
end})
