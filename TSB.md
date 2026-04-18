local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "TSB",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Loading TSB",
   LoadingSubtitle = "by mittenteee",
   ShowText = "Rayfield", -- for mobile users to unhide Rayfield, change if you'd like
   Theme = "Amethyst", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   ToggleUIKeybind = "K", -- The keybind to toggle the UI visibility (string like "K" or Enum.KeyCode)

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from emitting warnings when the script has a version mismatch with the interface.

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub"
   },

   Discord = {
      Enabled = false, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "noinvitelink", -- The Discord invite code, do not include Discord.gg/. E.g. Discord.gg/ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the Discord every time they load it up
   },

   KeySystem = false, -- Set this to true to use our key system
   KeySettings = {
      Title = "Key",
      Subtitle = "Key System",
      Note = "Secret", -- Use this to tell the user how to get a key
      FileName = "thekey", -- It is recommended to use something unique, as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"sigmakey"} -- List of keys that the system will accept, can be RAW file links (pastebin, github, etc.) or simple strings ("hello", "key22")
   }
})

local Tab = Window:CreateTab("Scripts", nil) -- Title, Image
local Section = Tab:CreateSection("Scripts")

local Button = Tab:CreateButton({
   Name = "Infinite Yield",
   Callback = function()
   loadstring(game:HttpGet(('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'),true))()
   end,
})

local Button = Tab:CreateButton({
   Name = "Vexon Hub (antiban)",
   Callback = function()
   pcall(function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/DiosDi/VexonHub/main/Loader-VexonHub"))()
end)
   end,
})

local Tab = Window:CreateTab("Player", nil) -- Title, Image
local Section = Tab:CreateSection("Player")

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer

local cframeSpeed = 10
local enabled = false

local keysDown = {
   W = false,
   A = false,
   S = false,
   D = false
}

-- Toggle with C
UserInputService.InputBegan:Connect(function(input, gp)
   if gp then return end

   if input.KeyCode == Enum.KeyCode.C then
      enabled = not enabled
      print("CFrame Speed:", enabled and "ON" or "OFF")
   end

   if input.KeyCode == Enum.KeyCode.W then keysDown.W = true end
   if input.KeyCode == Enum.KeyCode.A then keysDown.A = true end
   if input.KeyCode == Enum.KeyCode.S then keysDown.S = true end
   if input.KeyCode == Enum.KeyCode.D then keysDown.D = true end
end)

UserInputService.InputEnded:Connect(function(input)
   if input.KeyCode == Enum.KeyCode.W then keysDown.W = false end
   if input.KeyCode == Enum.KeyCode.A then keysDown.A = false end
   if input.KeyCode == Enum.KeyCode.S then keysDown.S = false end
   if input.KeyCode == Enum.KeyCode.D then keysDown.D = false end
end)

-- Movement loop
RunService.RenderStepped:Connect(function()
   if not enabled then return end

   local direction = Vector3.zero

   if keysDown.W then direction += Vector3.new(0, 0, -1) end
   if keysDown.S then direction += Vector3.new(0, 0, 1) end
   if keysDown.A then direction += Vector3.new(-1, 0, 0) end
   if keysDown.D then direction += Vector3.new(1, 0, 0) end

   if direction.Magnitude > 0 and cframeSpeed > 0 then
      local char = player.Character
      if char and char:FindFirstChild("HumanoidRootPart") then
         local hrp = char.HumanoidRootPart
         local cam = workspace.CurrentCamera

         local moveDir = cam.CFrame:VectorToWorldSpace(direction)
         hrp.CFrame = hrp.CFrame + (moveDir.Unit * (cframeSpeed / 10))
      end
   end
end)

-- Slider
local Slider = Tab:CreateSlider({
   Name = "C-Walkspeed ( C )",
   Range = {0, 100},
   Increment = 10,
   Suffix = "C-Frame Walkspeed",
   CurrentValue = 10,
   Flag = "C_WS",
   Callback = function(Value)
      cframeSpeed = Value
   end,
})

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

local flying = false
local speed = 200

local bodyVelocity
local bodyGyro

local keys = {
   W = false,
   A = false,
   S = false,
   D = false,
   Space = false,
   Shift = false
}

-- Key tracking (movement)
UserInputService.InputBegan:Connect(function(input, gp)
   if gp then return end

   if input.KeyCode == Enum.KeyCode.W then keys.W = true end
   if input.KeyCode == Enum.KeyCode.A then keys.A = true end
   if input.KeyCode == Enum.KeyCode.S then keys.S = true end
   if input.KeyCode == Enum.KeyCode.D then keys.D = true end
   if input.KeyCode == Enum.KeyCode.Space then keys.Space = true end
   if input.KeyCode == Enum.KeyCode.LeftShift then keys.Shift = true end

   -- 🔥 PRESS V TO TOGGLE FLY
   if input.KeyCode == Enum.KeyCode.V then
      flying = not flying

      local char = player.Character or player.CharacterAdded:Wait()
      local hrp = char:WaitForChild("HumanoidRootPart")

      if flying then
         bodyVelocity = Instance.new("BodyVelocity")
         bodyVelocity.MaxForce = Vector3.new(1e5, 1e5, 1e5)
         bodyVelocity.Velocity = Vector3.zero
         bodyVelocity.Parent = hrp

         bodyGyro = Instance.new("BodyGyro")
         bodyGyro.MaxTorque = Vector3.new(1e5, 1e5, 1e5)
         bodyGyro.CFrame = hrp.CFrame
         bodyGyro.Parent = hrp
      else
         if bodyVelocity then bodyVelocity:Destroy() end
         if bodyGyro then bodyGyro:Destroy() end
      end
   end
end)

UserInputService.InputEnded:Connect(function(input)
   if input.KeyCode == Enum.KeyCode.W then keys.W = false end
   if input.KeyCode == Enum.KeyCode.A then keys.A = false end
   if input.KeyCode == Enum.KeyCode.S then keys.S = false end
   if input.KeyCode == Enum.KeyCode.D then keys.D = false end
   if input.KeyCode == Enum.KeyCode.Space then keys.Space = false end
   if input.KeyCode == Enum.KeyCode.LeftShift then keys.Shift = false end
end)

-- Fly loop
RunService.RenderStepped:Connect(function()
   if not flying then return end

   local char = player.Character
   if not char or not char:FindFirstChild("HumanoidRootPart") then return end

   local hrp = char.HumanoidRootPart
   local cam = workspace.CurrentCamera

   local direction = Vector3.zero

   if keys.W then direction += Vector3.new(0, 0, -1) end
   if keys.S then direction += Vector3.new(0, 0, 1) end
   if keys.A then direction += Vector3.new(-1, 0, 0) end
   if keys.D then direction += Vector3.new(1, 0, 0) end
   if keys.Space then direction += Vector3.new(0, 1, 0) end
   if keys.Shift then direction += Vector3.new(0, -1, 0) end

   if direction.Magnitude > 0 then
      direction = cam.CFrame:VectorToWorldSpace(direction)
      bodyVelocity.Velocity = direction.Unit * speed
   else
      bodyVelocity.Velocity = Vector3.zero
   end

   bodyGyro.CFrame = cam.CFrame
end)

-- Optional: Keep your slider
local FlySpeedSlider = Tab:CreateSlider({
    Name = "Fly ( V )",
    Range = {10, 200},
    Increment = 10,
    Suffix = "Studs/s",
    CurrentValue = 120,
    Flag = "FlySpeedSlider",
    Callback = function(Value)
        speed = Value
    end,
})


local Tab = Window:CreateTab("Autofarm", nil) -- Title, Image
local Section = Tab:CreateSection("Autofarm")

local targetPosition = Vector3.new(559, 440, -370)
local interval = 0.1
local teleporting = false

local Toggle = Tab:CreateToggle({
   Name = "Loop Teleport",
   CurrentValue = false,
   Flag = "LoopTeleport",
   Callback = function(Value)
      teleporting = Value

      if teleporting then
         task.spawn(function()
            while teleporting do
               local player = game.Players.LocalPlayer
               local character = player.Character or player.CharacterAdded:Wait()

               local hrp = character:FindFirstChild("HumanoidRootPart")
               if hrp then
                  hrp.CFrame = CFrame.new(targetPosition)
               end

               task.wait(interval)
            end
         end)
      end
   end,
})

local interval = 0.2
local killing = false

local Toggle = Tab:CreateToggle({
   Name = "Loop Kill",
   CurrentValue = false,
   Flag = "LoopKill",
   Callback = function(Value)
      killing = Value

      if killing then
         task.spawn(function()
            while killing do
               local player = game.Players.LocalPlayer
               local character = player.Character or player.CharacterAdded:Wait()
               local humanoid = character:FindFirstChildOfClass("Humanoid")

               if humanoid then
                  humanoid.Health = 0
               end

               task.wait(interval)
            end
         end)
      end
   end,
})


local interval = 0.2
local damage = false

local Toggle = Tab:CreateToggle({
   Name = "Loop Damage",
   CurrentValue = false,
   Flag = "LoopDamage",
   Callback = function(Value)
      damage = Value

      if damage then
         task.spawn(function()
            while damage do
               local player = game.Players.LocalPlayer
               local character = player.Character or player.CharacterAdded:Wait()
               local humanoid = character:FindFirstChildOfClass("Humanoid")

               if humanoid then
                  humanoid.Health = 2
               end

               task.wait(interval)
            end
         end)
      end
   end,
})


local Tab = Window:CreateTab("Anti-AFK", nil) -- Title, Image
local Section = Tab:CreateSection("Anti-AFK")


local VirtualInputManager = game:GetService("VirtualInputManager")

local interval = 300 -- 5 minutes (300 seconds)
local antiAFK = false

local Toggle = Tab:CreateToggle({
   Name = "Anti-AFK",
   CurrentValue = false,
   Flag = "AntiAFK",
   Callback = function(Value)
      antiAFK = Value

      if antiAFK then
         task.spawn(function()
            while antiAFK do
               -- Simulate W key press
               VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.W, false, game)
               task.wait(0.1)
               VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.W, false, game)

               print("Anti-AFK triggered")

               task.wait(interval)
            end
         end)
      end
   end,
})
