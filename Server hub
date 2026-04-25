------------------------------------------------
-- VC9 Server (UPDATED + RANDOM + SMART HOP)
------------------------------------------------

local TeleportService = game:GetService("TeleportService")
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")

local player = Players.LocalPlayer
local placeId = game.PlaceId
local currentJobId = game.JobId

------------------------------------------------
-- GUI
------------------------------------------------

local gui = Instance.new("ScreenGui", game.CoreGui)
gui.Name = "VC9_Server"

local main = Instance.new("Frame", gui)
main.Size = UDim2.new(0, 300, 0, 230) -- ⬅️ كبرت شوي عشان الزر الجديد
main.Position = UDim2.new(0.5, -150, 0.5, -115)
main.BackgroundColor3 = Color3.fromRGB(25,25,25)
main.Active = true
main.Draggable = true
Instance.new("UICorner", main)

------------------------------------------------
-- Header
------------------------------------------------

local header = Instance.new("Frame", main)
header.Size = UDim2.new(1, 0, 0, 35)
header.BackgroundColor3 = Color3.fromRGB(40,40,40)
Instance.new("UICorner", header)

local title = Instance.new("TextLabel", header)
title.Size = UDim2.new(1, -40, 1, 0)
title.Text = "VC9 Server"
title.Font = Enum.Font.GothamBold
title.TextSize = 16
title.TextColor3 = Color3.new(1,1,1)
title.BackgroundTransparency = 1

------------------------------------------------
-- X
------------------------------------------------

local close = Instance.new("TextButton", header)
close.Size = UDim2.new(0, 35, 1, 0)
close.Position = UDim2.new(1, -35, 0, 0)
close.Text = "X"
close.Font = Enum.Font.GothamBold
close.BackgroundColor3 = Color3.fromRGB(120,0,0)
close.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", close)

close.MouseButton1Click:Connect(function()
gui:Destroy()
end)

------------------------------------------------
-- Input
------------------------------------------------

local box = Instance.new("TextBox", main)
box.Size = UDim2.new(0.85,0,0,30)
box.Position = UDim2.new(0.075,0,0.25,0)
box.PlaceholderText = "Enter Server Code (JobId)"
box.Font = Enum.Font.Gotham
box.TextSize = 13
box.TextColor3 = Color3.new(1,1,1)
box.BackgroundColor3 = Color3.fromRGB(40,40,40)
Instance.new("UICorner", box)

------------------------------------------------
-- Join by Code
------------------------------------------------

local join = Instance.new("TextButton", main)
join.Size = UDim2.new(0.85,0,0,35)
join.Position = UDim2.new(0.075,0,0.43,0)
join.Text = "Join Server by Code"
join.Font = Enum.Font.GothamSemibold
join.TextSize = 14
join.BackgroundColor3 = Color3.fromRGB(60,60,60)
join.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", join)

join.MouseButton1Click:Connect(function()
local code = box.Text
if code ~= "" then
TeleportService:TeleportToPlaceInstance(placeId, code, player)
else
warn("Enter a valid server code")
end
end)

------------------------------------------------
-- 🎲 RANDOM SERVERS
------------------------------------------------

local function randomServer()

local success, result = pcall(function()
local url = "https://games.roblox.com/v1/games/"..placeId.."/servers/Public?sortOrder=Desc&limit=100"
return HttpService:JSONDecode(game:HttpGet(url))
end)

if not success or not result then
TeleportService:Teleport(placeId, player)
return
end

local servers = {}

for _,v in pairs(result.data) do
table.insert(servers, v.id)
end

if #servers > 0 then
local chosen = servers[math.random(1,#servers)]
TeleportService:TeleportToPlaceInstance(placeId, chosen, player)
else
TeleportService:Teleport(placeId, player)
end

end

------------------------------------------------
-- زر السيرفرات العشوائية (فوق)
------------------------------------------------

local randomBtn = Instance.new("TextButton", main)
randomBtn.Size = UDim2.new(0.85,0,0,30)
randomBtn.Position = UDim2.new(0.075,0,0.61,0) -- 👈 فوق Server Hop
randomBtn.Text = "سيرفرات عشوائية"
randomBtn.Font = Enum.Font.Gotham
randomBtn.TextSize = 13
randomBtn.BackgroundColor3 = Color3.fromRGB(70,70,70)
randomBtn.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", randomBtn)

randomBtn.MouseButton1Click:Connect(randomServer)

------------------------------------------------
-- 🔥 SMART SERVER HOP
------------------------------------------------

local function smartHop()

local success, result = pcall(function()
local url = "https://games.roblox.com/v1/games/"..placeId.."/servers/Public?sortOrder=Desc&limit=100"
return HttpService:JSONDecode(game:HttpGet(url))
end)

if not success or not result then
TeleportService:Teleport(placeId, player)
return
end

local servers = {}

for _,v in pairs(result.data) do
if v.id ~= currentJobId then
if v.playing >= 18 and v.playing <= 26 then
table.insert(servers, v.id)
end
end
end

if #servers > 0 then
TeleportService:TeleportToPlaceInstance(placeId, servers[math.random(1,#servers)], player)
else
TeleportService:Teleport(placeId, player)
end

end

------------------------------------------------
-- Server Hop Button
------------------------------------------------

local hop = Instance.new("TextButton", main)
hop.Size = UDim2.new(0.85,0,0,30)
hop.Position = UDim2.new(0.075,0,0.75,0)
hop.Text = "Server Hop"
hop.Font = Enum.Font.Gotham
hop.TextSize = 13
hop.BackgroundColor3 = Color3.fromRGB(50,50,50)
hop.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", hop)

hop.MouseButton1Click:Connect(smartHop)

------------------------------------------------
-- Copy Code
------------------------------------------------

local copy = Instance.new("TextButton", main)
copy.Size = UDim2.new(0.85,0,0,25)
copy.Position = UDim2.new(0.075,0,0.88,0)
copy.Text = "Copy My Server Code"
copy.Font = Enum.Font.Gotham
copy.TextSize = 12
copy.BackgroundColor3 = Color3.fromRGB(35,35,35)
copy.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", copy)

copy.MouseButton1Click:Connect(function()
if setclipboard then
setclipboard(currentJobId)
copy.Text = "Copied!"
task.wait(1)
copy.Text = "Copy My Server Code"
end
end)
