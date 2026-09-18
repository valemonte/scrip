if not game:IsLoaded() then
    game.Loaded:Wait()
end
do
    local str

    do
        local Players = game:GetService("Players")
        local LocalPlayer = Players.LocalPlayer

        if not LocalPlayer then
            pcall(function()
                Players:GetPropertyChangedSignal("LocalPlayer"):Wait()
            end)
            LocalPlayer = Players.LocalPlayer
        end

        str = tostring(LocalPlayer and LocalPlayer.UserId or 0)
    end

    local v4 = getgenv and getgenv() or _G
    local KiraHub = v4.KiraHub

    if type(KiraHub) ~= "table" then
        KiraHub = {
			slots = {}
		}
        v4.KiraHub = KiraHub
    end

    if type(KiraHub.slots) ~= "table" then
        KiraHub.slots = {}
    end

    local unload

    do
        local v6 = KiraHub.slots[str]

        if type(v6) ~= "table" then
            v6 = {}
            KiraHub.slots[str] = v6
        end

        v6.gen = (tonumber(v6.gen) or 0) + 1

        local v7 = false

        for k, v in pairs(KiraHub.slots) do
            if str ~= tostring(k) and type(v) == "table" and v.alive == true then
                v7 = true

                break
            end
        end

        if not v7 then
            v4.KiraCfgGen = (tonumber(v4.KiraCfgGen) or 0) + 1
        end

        unload = v6.unload
        v6.unload = nil
        v6.alive = false
    end

    if type(unload) == "function" then
        pcall(unload)
    elseif type(v4.KiraUnload) == "function" then
        local KiraUnloadUid = v4.KiraUnloadUid
        local v12 = KiraUnloadUid == nil or str == tostring(KiraUnloadUid)

        if KiraUnloadUid == nil then
            for k, v in pairs(KiraHub.slots) do
                if str ~= tostring(k) and type(v) == "table" and type(v.unload) == "function" then
                    v12 = false

                    break
                end
            end
        end

        if v12 then
            local KiraUnload = v4.KiraUnload

            if str == tostring(KiraUnloadUid or str) then
                v4.KiraUnload = nil
                v4.KiraUnloadUid = nil
            end

            pcall(KiraUnload)
        end
    end
end
do
    local Players = game:GetService("Players")
    local LocalPlayer = Players.LocalPlayer

    if not LocalPlayer then
        pcall(function()
            Players:GetPropertyChangedSignal("LocalPlayer"):Wait()
        end)
        LocalPlayer = Players.LocalPlayer
    end

    local v18 = os.clock() + 60

    while LocalPlayer and v18 > os.clock() do
        local v20, v21

        do
            local Character = LocalPlayer.Character

            v20 = Character and Character:FindFirstChildOfClass("Humanoid")
            v21 = Character and Character:FindFirstChild("HumanoidRootPart")
        end

        if v20 and v21 and v20.Health > 0 then
            task.wait(0.45)

            local Character = LocalPlayer.Character
            local v23 = Character and Character:FindFirstChildOfClass("Humanoid")
            local v24 = Character and Character:FindFirstChild("HumanoidRootPart")

            if not v23 or not v24 or not (v23.Health > 0) then
                continue
            end

            break
        end

        task.wait(0.1)
    end
end
local t1 = {
	Title = "Kira Hub",
	Version = "0.1",
	Product = "Steal an Egg",
	OpenBind = Enum.KeyCode.RightShift,
	FlightBind = Enum.KeyCode.F,
	Tagline = "",
	Status = "preview",
	Game = "Steal an Egg",
	Discord = "https://discord.gg/ZNwS8csX3j",
	Website = "",
	Changelog = "",
	Author = "Kira (@kira_scripts.gg)",
	Credits = "Thanks to all my dicord members",
	Support = "Thank You for your support !"
}
local function v26(p1)
    local v328 = tostring(p1 or "Game"):gsub("[<>:\"/\\|?*]", "_"):gsub("%s+", "_"):gsub("_+", "_"):match("^%s*(.-)%s*$")

    if not v328 or v328 == "" or v328 == "_" then
        v328 = "Game"
    end

    return v328
end
t1.LogoFile = "Kira" .. "/logo.png"
t1.LogoFileLight = "Kira" .. "/logo-light.png"
local n1 = 620
local n2 = 430
local n3 = 152
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local HttpService, Stats, ProximityPromptService, ReplicatedStorage, LocalPlayer, v40, v41, u42, u43, u44, str, v48, v49, v50, v51, t2
local t3, t4, t5, t6, t7, t9, t10, t11, t12, u66, u67, u68, u69, u70, u71, t14
local v73, u75, u76, v79, self, v82, v83, v84, v85, v87, v98, v103, v108, v113, v151, v194
local v199, v217, v228, v229, v245, v250, v259, v261, v262, v263, u265, u266, v268, v270, v272, v274
local v277, v278, v279, v280, v281, v282, u284, v287, v288, v289, v290, v291, v292, v293
do
    local t8, t13, v81, v86

    do
        local t26, v94

        do
            local TweenService = game:GetService("TweenService")

            HttpService = game:GetService("HttpService")
            Stats = game:GetService("Stats")
            ProximityPromptService = game:GetService("ProximityPromptService")
            ReplicatedStorage = game:GetService("ReplicatedStorage")

            local GuiService = game:GetService("GuiService")

            LocalPlayer = Players.LocalPlayer

            if not LocalPlayer then
                pcall(function()
                    Players:GetPropertyChangedSignal("LocalPlayer"):Wait()
                end)
                LocalPlayer = Players.LocalPlayer
            end

            function v40()
                if UserInputService.VREnabled then
                    return false
                end
                local u338 = false
                pcall(function()
                    u338 = GuiService:IsTenFootInterface()
                end)
                if u338 then
                    return false
                end
                if UserInputService.TouchEnabled then
                    return true
                end
                if UserInputService.MouseEnabled == false then
                    return true
                end
                local u339 = false
                local u340 = false
                pcall(function()
                    u339 = UserInputService.GyroscopeEnabled == true
                end)
                pcall(function()
                    u340 = UserInputService.AccelerometerEnabled == true
                end)
                if u339 or u340 then
                    return true
                end
                local PreferredInput
                local LastInputType
                pcall(function()
                    PreferredInput = UserInputService.PreferredInput
                end)
                pcall(function()
                    LastInputType = UserInputService:GetLastInputType()
                end)
                if PreferredInput == Enum.PreferredInput.Touch or LastInputType == Enum.UserInputType.Touch then
                    return true
                end
                local v343 = LocalPlayer and LocalPlayer:FindFirstChild("PlayerGui")
                if v343 and (v343:FindFirstChild("TouchGui", true) or v343:FindFirstChild("TouchControlFrame", true) or v343:FindFirstChild("JumpButton", true) or v343:FindFirstChild("DynamicThumbstickFrame", true)) then
                    return true
                end

                return false
            end
            function v41()
                local CurrentCamera = workspace.CurrentCamera
                local v345 = if not CurrentCamera then Vector2.new(1280, 720) else CurrentCamera.ViewportSize
                local v346 = math.floor(math.clamp(v345.X * 0.7, 440, 560))
                local v347 = math.floor(math.clamp(v345.Y * 0.74, 340, 410))

                if v345.X > 80 then
                    v346 = math.min(v346, v345.X - 36)
                end

                if v345.Y > 80 then
                    v347 = math.min(v347, v345.Y - 36)
                end

                return math.max(400, v346), math.max(320, v347)
            end

            u42 = v40()
            u43 = false
            u44 = nil

            if u42 then
                local v45, v46 = v41()

                n1 = v45
                n2 = v46
                n3 = 128
            end

            str = tostring(LocalPlayer and LocalPlayer.UserId or 0)
            v48 = "PH_UI_" .. str
            v49 = "KiraWorldGui_" .. str

            function v50()
                return getgenv and getgenv() or _G
            end
            function v51()
                local v350 = getgenv and getgenv() or _G
                local KiraHub = v350.KiraHub

                if type(KiraHub) ~= "table" then
                    KiraHub = {
						slots = {}
					}
                    v350.KiraHub = KiraHub
                end

                if type(KiraHub.slots) ~= "table" then
                    KiraHub.slots = {}
                end

                local v352 = KiraHub.slots[str]

                if type(v352) ~= "table" then
                    v352 = {}
                    KiraHub.slots[str] = v352
                end

                return v352
            end

            t1.ConfigFile = (("Kira" .. "/" .. v26(t1.Game)) .. "/cache") .. "/" .. v26(LocalPlayer and LocalPlayer.Name or "Player") .. "-config.json"
            t2 = {
				Dark = {
					bg = Color3.fromRGB(12, 11, 10),
					rail = Color3.fromRGB(16, 15, 14),
					card = Color3.fromRGB(32, 30, 27),
					lift = Color3.fromRGB(42, 39, 35),
					fill = Color3.fromRGB(48, 44, 39),
					line = Color3.fromRGB(58, 53, 46),
					text = Color3.fromRGB(246, 242, 234),
					dim = Color3.fromRGB(168, 158, 144),
					mute = Color3.fromRGB(110, 102, 92),
					accent = Color3.fromRGB(214, 168, 108),
					accentDeep = Color3.fromRGB(92, 68, 36),
					accentHover = Color3.fromRGB(228, 186, 128),
					ink = Color3.fromRGB(22, 18, 14),
					ok = Color3.fromRGB(138, 166, 128),
					Kira = Color3.fromRGB(246, 242, 234)
				},
				Light = {
					bg = Color3.fromRGB(232, 226, 218),
					rail = Color3.fromRGB(232, 226, 218),
					card = Color3.fromRGB(252, 250, 246),
					lift = Color3.fromRGB(242, 236, 228),
					fill = Color3.fromRGB(224, 218, 208),
					line = Color3.fromRGB(204, 196, 184),
					text = Color3.fromRGB(28, 24, 20),
					dim = Color3.fromRGB(92, 84, 74),
					mute = Color3.fromRGB(128, 120, 108),
					accent = Color3.fromRGB(168, 114, 56),
					accentDeep = Color3.fromRGB(120, 80, 38),
					accentHover = Color3.fromRGB(186, 132, 70),
					ink = Color3.fromRGB(252, 250, 246),
					ok = Color3.fromRGB(64, 118, 82),
					Kira = Color3.fromRGB(28, 24, 20)
				}
			}
            t3 = {}

            for k, v in pairs(t2.Dark) do
                t3[k] = v
            end

            t4 = {
				title = Enum.Font.BuilderSansBold,
				mid = Enum.Font.BuilderSansMedium,
				body = Enum.Font.BuilderSans,
				mono = Enum.Font.RobotoMono
			}
            t5 = {
				"Forest",
				"Desert",
				"Lake",
				"Jungle",
				"Snow",
				"Volcano",
				"Prehistoric",
				"Cosmic",
				"Abyss Ocean",
				"Cherry Blossom"
			}
            t6 = {
				"Common",
				"Uncommon",
				"Rare",
				"Epic",
				"Legendary",
				"Mythic",
				"Cosmic",
				"Secret",
				"Eternal",
				"Divine",
				"Titan"
			}
            t7 = {
				"Golden",
				"Rainbow",
				"Galaxy",
				"Crystal",
				"Bloom"
			}
            t8 = {
				About = "info",
				["Auto Steal"] = "egg",
				Plot = "grid",
				Serverhop = "rocket",
				Misc = "layers",
				Webhook = "out",
				Settings = "cog"
			}
            t9 = {}
            t10 = {}
            t11 = {}
            t12 = {}
            t13 = {}
            u66 = nil
            u67 = nil
            u68 = nil
            u69 = nil
            u70 = nil
            u71 = nil
            t14 = {}

            function v73(p2)
                if p2 then
                    t14[#t14 + 1] = p2
                end

                return p2
            end

            local t15 = {}

            u75 = nil
            u76 = nil

            local function v77(p3)
                if type(p3) ~= "string" or p3 == "" then
                    return
                end

                local t16 = {}

                if crypt then
                    t16[#t16 + 1] = crypt.base64decode
                    t16[#t16 + 1] = crypt.base64_decode
                end

                if syn and syn.crypt and syn.crypt.base64 and syn.crypt.base64.decode then
                    t16[#t16 + 1] = syn.crypt.base64.decode
                end

                if base64 and base64.decode then
                    t16[#t16 + 1] = base64.decode
                end

                if base64_decode then
                    t16[#t16 + 1] = base64_decode
                end

                for i = 1, #t16 do
                    local ok, result = pcall(t16[i], p3)

                    if ok and type(result) == "string" and #result > 64 then
                        return result
                    end
                end
            end
            local function v78(p4)
                if p4 then
                    if u76 then
                        return u76
                    end
                elseif u75 then
                    return u75
                end

                local v367 = v77(not p4 and "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# scrip
