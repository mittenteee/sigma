local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Extra",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Loading Extra",
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

   KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "Extra",
      Subtitle = "Key System",
      Note = "...", -- Use this to tell the user how to get a key
      FileName = "key", -- It is recommended to use something unique, as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"dordefemboy"} -- List of keys that the system will accept, can be RAW file links (pastebin, github, etc.) or simple strings ("hello", "key22")
   }
})


local Tab = Window:CreateTab("Anti-AFK", nil) -- Title, Image
local Section = Tab:CreateSection("Anti-AFK")



local VirtualInputManager = game:GetService("VirtualInputManager")

local interval = 300 -- 5 minutes (300 seconds)
local antiAFK = false

local Toggle = Tab:CreateToggle({
   Name = "Anti AFK",
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


local Tab = Window:CreateTab("Auto", nil) -- Title, Image
local Section = Tab:CreateSection("Auto")


local UIS = game:GetService("UserInputService")
local VIM = game:GetService("VirtualInputManager")

local holdingW = false

local Toggle = Tab:CreateToggle({
   Name = "Hold W",
   CurrentValue = false,
   Flag = "HoldW",
   Callback = function(Value)
      holdingW = Value

      if holdingW then
         task.spawn(function()
            while holdingW do
               -- Press W
               VIM:SendKeyEvent(true, Enum.KeyCode.W, false, game)
               task.wait(0.1)
            end
         end)
      else
         -- Release W when toggle is turned off
         VIM:SendKeyEvent(false, Enum.KeyCode.W, false, game)
      end
   end,
})


local Tab = Window:CreateTab("Desync", nil) -- Title, Image
local Section = Tab:CreateSection("Desync")


local Button = Tab:CreateButton({
   Name = "Desync",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Universal-FE-Desync-196417"))()
   end,
})
