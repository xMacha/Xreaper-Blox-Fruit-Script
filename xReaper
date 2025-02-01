local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/xMacha/Xreaper-for-bloxfruit/refs/heads/main/Rayfield.lua'))()

local Window = Rayfield:CreateWindow({
   Name = "Xreaper for blox fruit",
   Icon = "skull",
   LoadingTitle = "loading Xreaper for blox fruit....",
   LoadingSubtitle = "by Macha",
   Theme = "",

   DisableRayfieldPrompts = true,
   DisableBuildWarnings = true, 

   ConfigurationSaving = {
      Enabled = true,
      FolderName = Xreaper, 
      FileName = "cfg"
   },

   Discord = {
      Enabled = true, 
      Invite = "EtjXnWjt",
      RememberJoins = true 
   },

   KeySystem = false, 
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

Rayfield:Notify({
   Title = "Welcome",
   Content = "Use K to hide/unhide menu",
   Duration = 6.5,
   Image = "skull",
})

local PlayerTab = Window:CreateTab("Player", "user")

local Section = PlayerTab:CreateSection("Movement")

local Speed = PlayerTab:CreateSlider({
   Name = "Player speed multiplier",
   Range = {1, 30},
   Increment = 1,
   Suffix = "x Speed",
   CurrentValue = 1,
   Flag = "Speed", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
local player = game.Players.LocalPlayer

local function applySpeedMultiplier()
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")

    -- Ustawienie SpeedMultiplier (zmień `Value` na rzeczywistą wartość, np. 12)
    character:SetAttribute("SpeedMultiplier", Value)
	local speed = Value
end

-- Wywołanie funkcji przy pierwszym uruchomieniu
applySpeedMultiplier()

-- Ponowne ustawianie po respawnie gracza
player.CharacterAdded:Connect(function()
    applySpeedMultiplier()
end)
   end,
})

local Slider = PlayerTab:CreateSlider({
   Name = "Dash length",
   Range = {1, 800},
   Increment = 1,
   Suffix = "Length",
   CurrentValue = 1,
   Flag = "DashLenght", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
local player = game.Players.LocalPlayer

local function applySpeedMultiplier()
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")

    -- Ustawienie SpeedMultiplier (zmień `Value` na rzeczywistą wartość, np. 12)
    character:SetAttribute("DashLength", Value)
end

-- Wywołanie funkcji przy pierwszym uruchomieniu
applySpeedMultiplier()

-- Ponowne ustawianie po respawnie gracza
player.CharacterAdded:Connect(function()
    applySpeedMultiplier()
end)

   end,
})

 local Slider = PlayerTab:CreateSlider({
    Name = "Jump Height",
    Range = {50, 500},
    Increment = 1,
    Suffix = "Height",
    CurrentValue = 50,
    Flag = "Height", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
    local player = game.Players.LocalPlayer

	local function applySpeedMultiplier()
 	   local character = player.Character or player.CharacterAdded:Wait()
 	   local humanoid = character:WaitForChild("Humanoid")

 	   -- Ustawienie SpeedMultiplier (zmień `Value` na rzeczywistą wartość, np. 12)
  	   game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
	end

	-- Wywołanie funkcji przy pierwszym uruchomieniu
	applySpeedMultiplier()

	-- Ponowne ustawianie po respawnie gracza
	player.CharacterAdded:Connect(function()
    applySpeedMultiplier()
	end)

  	  end,
})

local Section = PlayerTab:CreateSection("Teleport")

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local selectedPlayerName = nil

-- Pobierz listę aktualnych graczy i utwórz tablicę z ich nazwami
local players = Players:GetPlayers()
local options = {}
for _, plr in ipairs(players) do
    table.insert(options, plr.Name)
end
local SelectPlayer = PlayerTab:CreateDropdown({
    Name = "Select Player",
    Options = options,
    CurrentOption = { options[1] or "No player" },
    MultipleOptions = false,
    Flag = "TeleportToPlayer",
    Callback = function(Options)
		targetPlayer = Options[1]
		Rayfield:Notify({
            Title = "Player Selected",
            Content = "Selected player: " .. targetPlayer,
            Duration = 6.5,
            Image = "rewind",
        })
	end,
})

local Button = PlayerTab:CreateButton({
   Name = "Refresh",
   Callback = function()
	local players = Players:GetPlayers()
	local options = {}
	for _, plr in ipairs(players) do
    table.insert(options, plr.Name)
	end
  	 end,
})

local selectedPlaceName = "second sea"

-- Tworzenie dropdowna (mimo że jest tylko jedna opcja, pozwala na ewentualne przyszłe rozszerzenie)
local DropdownPlaces = PlayerTab:CreateDropdown({
    Name = "Select Place",
    Options = {selectedPlaceName},
    CurrentOption = {selectedPlaceName},
    MultipleOptions = false,
    Flag = "DropdownPlace",
    Callback = function(selected)
        selectedPlaceName = selected[1]
        print("Selected place: " .. selectedPlaceName)
    end,
})

-- Tworzenie przycisku do teleportacji
local ButtonPlace = PlayerTab:CreateButton({
    Name = "Teleport to Coordinates",
    Callback = function()
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character and character:FindFirstChild("HumanoidRootPart")

        if not humanoidRootPart then
            warn("No HumanoidRootPart found!")
            Rayfield:Notify({
                Title = "Teleport Error",
                Content = "Your character is not loaded!",
                Duration = 6.5,
                Image = "rewind",
            })
            return
        end

        -- Docelowa pozycja teleportacji
        local targetPosition = Vector3.new(-558.41, 7.2, 1486.88)

        -- Teleportacja
        humanoidRootPart.CFrame = CFrame.new(targetPosition)

        Rayfield:Notify({
            Title = "Teleport",
            Content = "Teleported to target location!",
            Duration = 6.5,
            Image = "rewind",
        })
    end,
})


