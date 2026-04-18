local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "HUBS",
   Icon = 0,
   LoadingTitle = "Loading HUBS",
   LoadingSubtitle = "by mittenteee",
   ShowText = "Rayfield",
   Theme = "Default",
   ToggleUIKeybind = "K",

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false,

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil,
      FileName = "Big Hub"
   },

   Discord = {
      Enabled = false,
      Invite = "noinvitelink",
      RememberJoins = true
   },

   KeySystem = true,
   KeySettings = {
      Title = "HUBS",
      Subtitle = "Key System",
      Note = "...",
      FileName = "Key",
      SaveKey = true,
      GrabKeyFromSite = false,
      Key = {"dordefemboy"}
   }
})

local Tab = Window:CreateTab("My Own", 4483362458)

Tab:CreateButton({
   Name = "Extra",
   Callback = function()
      loadstring(game:HttpGet("https://raw.githubusercontent.com/mittenteee/sigma/refs/heads/main/Extra.md"))()
   end,
})

Tab:CreateDivider()

Tab:CreateButton({
   Name = "TSB",
   Callback = function()
      loadstring(game:HttpGet("https://raw.githubusercontent.com/mittenteee/sigma/refs/heads/main/TSB.md"))()
   end,
})

local Tab = Window:CreateTab("Others", 4483362458)

Tab:CreateButton({
   Name = "TSB",
   Callback = function()
      pcall(function()
         loadstring(game:HttpGet("https://raw.githubusercontent.com/DiosDi/VexonHub/main/Loader-VexonHub"))()
      end)
   end,
})

Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "FTAP",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Fling-Things-and-People-FTAP-Hub-79081"))()
   end,
})

Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "MM2",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-a-170306"))()
   end,
})


Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "BALB",
   Callback = function()
   repeat wait() until game:IsLoaded() and game.Players.LocalPlayer
loadstring(game:HttpGet("https://raw.githubusercontent.com/domiusexecutores/block/refs/heads/main/luau"))()
   end,
})


Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "Spelling Bee",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Spelling-bee-auto-type-OP-no-key-114502"))()
   end,
})


Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "Bloxstrike",
   Callback = function()
   loadstring(game:HttpGet('https://raw.githubusercontent.com/Zylang104/BloxStrike/refs/heads/main/main.lua'))()
   end,
})

Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "Rivals (Broken)",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/RIVALS-Kurby-Hub-ANTI-CHEAT-BYPASS-AND-INSANE-AIMBOT-202671"))()
   end,
})


Tab:CreateDivider()
local Section = Tab:CreateSection("Emergency Hamburg")


local Button = Tab:CreateButton({
   Name = "Car Fly Legit",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Emergency-Hamburg-Script-55826"))()
   end,
})

local Button = Tab:CreateButton({
   Name = "Car Fly Unlegit",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Emergency-Hamburg-Fly-Car-Open-Source-134890"))()
   end,
})

local Button = Tab:CreateButton({
   Name = "Vortex",
   Callback = function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Emergency-Hamburg-Vortex-Main-Script-68747"))()
   end,
})


local Tab = Window:CreateTab("Universal", 4483362458)


local Button = Tab:CreateButton({
   Name = "Infinite Yield",
   Callback = function()
   loadstring(game:HttpGet(('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'),true))()
   end,
})

Tab:CreateDivider()

local Button = Tab:CreateButton({
   Name = "Auto Piano",
   Callback = function()
   loadstring(game:HttpGet("https://hellohellohell0.com/talentless-raw/TALENTLESS.lua", true))()
   end,
})


local Tab = Window:CreateTab("Aimbot", 4483362458)


local Button = Tab:CreateButton({
   Name = "Z3US",
   Callback = function()
   loadstring(game:HttpGet("https://raw.githubusercontent.com/blackowl1231/Z3US/refs/heads/main/main.lua"))()
   end,
})
