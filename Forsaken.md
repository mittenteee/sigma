local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Forsaken",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "loading Forsaken",
   LoadingSubtitle = "by mittenteee",
   ShowText = "Rayfield", -- for mobile users to unhide Rayfield, change if you'd like
   Theme = "Default", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   ToggleUIKeybind = "K", -- The keybind to toggle the UI visibility (string like "K" or Enum.KeyCode)

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from emitting warnings when the script has a version mismatch with the interface.

   -- ScriptID = "sid_xxxxxxxxxxxx", -- Your Script ID from developer.sirius.menu — enables analytics, managed keys, and script hosting

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

   KeySystem = true,
   KeySettings = {
      Title = "Forsaken",
      Subtitle = "Key System",
      Note = "...",
      FileName = "Key",
      SaveKey = true,
      GrabKeyFromSite = false,
      Key = {"dordefemboy"}
   }
})


local Tab = Window:CreateTab("Player", nil) -- Title, Image
local Section = Tab:CreateSection("Player")

local Button = Tab:CreateButton({
   Name = "Enable Jump",
   Callback = function()
      task.spawn(function()
         while true do
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()
            local hum = character:FindFirstChildOfClass("Humanoid")

            if hum then
               hum.UseJumpPower = true
               hum.JumpPower = 50
            end

            task.wait(1)
         end
      end)
   end,
})


local player = game.Players.LocalPlayer
local RunService = game:GetService("RunService")

local noclip = false

-- Loop that handles noclip
RunService.Stepped:Connect(function()
    if noclip and player.Character then
        for _, part in pairs(player.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)

-- Your toggle
local Toggle = Tab:CreateToggle({
   Name = "Noclip",
   CurrentValue = false,
   Flag = "NoclipToggle",

   Callback = function(Value)
       noclip = Value

       -- Optional: restore collisions when turned off
       if not noclip and player.Character then
           for _, part in pairs(player.Character:GetDescendants()) do
               if part:IsA("BasePart") then
                   part.CanCollide = true
               end
           end
       end
   end,
})


local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local flying = false
local bv, bg, flyConn

local Toggle = Tab:CreateToggle({
   Name = "Fly",
   CurrentValue = false,
   Flag = "Toggle1",
   Callback = function(Value)
      flying = Value

      if flying then
         local character = player.Character or player.CharacterAdded:Wait()
         local hrp = character:WaitForChild("HumanoidRootPart")

         bv = Instance.new("BodyVelocity")
         bv.MaxForce = Vector3.new(1e5, 1e5, 1e5)
         bv.Velocity = Vector3.zero
         bv.Parent = hrp

         bg = Instance.new("BodyGyro")
         bg.MaxTorque = Vector3.new(1e5, 1e5, 1e5)
         bg.CFrame = hrp.CFrame
         bg.Parent = hrp

         flyConn = RunService.RenderStepped:Connect(function()
            local cam = workspace.CurrentCamera
            local moveDir = Vector3.zero

            if UIS:IsKeyDown(Enum.KeyCode.W) then moveDir += cam.CFrame.LookVector end
            if UIS:IsKeyDown(Enum.KeyCode.S) then moveDir -= cam.CFrame.LookVector end
            if UIS:IsKeyDown(Enum.KeyCode.A) then moveDir -= cam.CFrame.RightVector end
            if UIS:IsKeyDown(Enum.KeyCode.D) then moveDir += cam.CFrame.RightVector end
            if UIS:IsKeyDown(Enum.KeyCode.Space) then moveDir += Vector3.new(0,1,0) end
            if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then moveDir -= Vector3.new(0,1,0) end

            bv.Velocity = moveDir.Magnitude > 0 and moveDir.Unit * 60 or Vector3.zero
            bg.CFrame = cam.CFrame
         end)

      else
         if flyConn then flyConn:Disconnect() flyConn = nil end
         if bv then bv:Destroy() bv = nil end
         if bg then bg:Destroy() bg = nil end
      end
   end,
})


local Tab = Window:CreateTab("Teleport", nil)
local Section = Tab:CreateSection("Teleport")

local teleporting = false

local Button = Tab:CreateButton({
   Name = "Spawn (Press Twice For Disable)",
   Callback = function()
      teleporting = not teleporting

      if teleporting then
         task.spawn(function()
            while teleporting do
               local player = game.Players.LocalPlayer
               local character = player.Character or player.CharacterAdded:Wait()
               local hrp = character:WaitForChild("HumanoidRootPart")

               hrp.CFrame = CFrame.new(-3553, 12, 267)

               task.wait(0.1)
            end
         end)
      end
   end,
})
