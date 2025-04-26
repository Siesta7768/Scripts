local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Dig to Earth's Core Wins GUI",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Rayfield Interface Suite",
   LoadingSubtitle = "by Siesta",
   Theme = "Amethyst", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub"
   },

   Discord = {
      Enabled = false, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

   KeySystem = false, -- Set this to true to use our key system
   KeySettings = {
      Title = "Untitled",
      Subtitle = "Key System",
      Note = "No method of obtaining the key is provided", -- Use this to tell the user how to get a key
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"Hello"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})

local Tab = Window:CreateTab("Teleport Wins", 4483362458) -- Title, Image
local Section = Tab:CreateSection("GUI World Selections")

local Button = Tab:CreateButton({
   Name = "Destroy GUI",
   Callback = function()
   -- The function that takes place when the button is pressed
   Rayfield:Destroy()
   end,
})
local Button = Tab:CreateButton({
   Name = "World 9",
   Callback = function()
   -- The function that takes place when the button is pressed
   local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer

local teleporting = false
local targetPosition = Vector3.new(5.5, -400, -9006.2)

-- Create ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleportUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Frame with glowing edge
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 280, 0, 220)
frame.Position = UDim2.new(0, 20, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.BackgroundTransparency = 0.05
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui

local corner = Instance.new("UICorner", frame)
corner.CornerRadius = UDim.new(0, 12)

-- UIStroke for neon border
local neonBorder = Instance.new("UIStroke")
neonBorder.Thickness = 6
neonBorder.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
neonBorder.Parent = frame

-- Function to cycle through rainbow colors (slowed down)
local function cycleColors()
    while true do
        for i = 0, 1, 0.05 do  -- Reduced the increment to slow down the color change
            neonBorder.Color = Color3.fromHSV(i, 1, 1)  -- Smooth transition through rainbow colors
            wait(0.2)  -- Increased the wait time for slower animation
        end
    end
end

-- Start the neon animation loop
spawn(cycleColors)

-- Title
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -40, 0, 30)
title.Position = UDim2.new(0, 10, 0, 5)
title.Text = "🌟 TELEPORT PANEL 🌟"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamSemibold
title.TextScaled = true
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = frame

-- Status Label
local status = Instance.new("TextLabel")
status.Size = UDim2.new(1, -20, 0, 20)
status.Position = UDim2.new(0, 10, 0, 35)
status.Text = "⏸️ Status: Idle"
status.TextColor3 = Color3.fromRGB(200, 200, 200)
status.Font = Enum.Font.Gotham
status.TextScaled = true
status.BackgroundTransparency = 1
status.TextXAlignment = Enum.TextXAlignment.Left
status.Parent = frame

-- Button Creator Function
local function createButton(text, yPos, bgColor, emoji)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -40, 0, 40)
    button.Position = UDim2.new(0, 20, 0, yPos)
    button.Text = emoji .. " " .. text
    button.Font = Enum.Font.Gotham
    button.TextScaled = true
    button.TextColor3 = Color3.new(1, 1, 1)
    button.BackgroundColor3 = bgColor

    local uic = Instance.new("UICorner")
    uic.CornerRadius = UDim.new(0, 8)
    uic.Parent = button

    -- Hover effect
    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {
            BackgroundColor3 = bgColor:lerp(Color3.new(1,1,1), 0.1)
        }):Play()
    end)
    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {
            BackgroundColor3 = bgColor
        }):Play()
    end)

    button.Parent = frame
    return button
end

-- Buttons with Emojis
local startButton = createButton("Start Teleport", 60, Color3.fromRGB(0, 170, 0), "🚀")
local stopButton = createButton("Stop Teleport", 110, Color3.fromRGB(170, 0, 0), "❌")

-- Close Button
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -35, 0, 5)
closeButton.Text = "❌"
closeButton.Font = Enum.Font.GothamBold
closeButton.TextScaled = true
closeButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.Parent = frame

local closeCorner = Instance.new("UICorner", closeButton)
closeCorner.CornerRadius = UDim.new(0, 8)

-- Logic
closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

startButton.MouseButton1Click:Connect(function()
    teleporting = true
    status.Text = "⏳ Status: Teleporting..."
    status.TextColor3 = Color3.fromRGB(0, 255, 0)
end)

stopButton.MouseButton1Click:Connect(function()
    teleporting = false
    status.Text = "⛔ Status: Stopped"
    status.TextColor3 = Color3.fromRGB(255, 0, 0)
end)

-- Fixed the issue here
RunService.RenderStepped:Connect(function()
    if teleporting and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character:MoveTo(targetPosition)
    end
end)
   end,
})


local Divider = Tab:CreateDivider()

local Toggle = Tab:CreateToggle({
   Name = "Toggle Example",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
   local terrain = workspace.Terrain
terrain:Clear()

   -- The function that takes place when the toggle is pressed
   -- The variable (Value) is a boolean on whether the toggle is true or false
   end,
})

