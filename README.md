
    




if game.PlaceId == 621129760 then
    local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
    local venyx = library.new("Ez W Hub: Kat", 5013109572)

    local section1 = venyx:addPage("Main", 8162117119)
    local section1 = section1:addSection("Main")



    section1:addButton("Silent Aim", function()
        local refreshrate = 0.01
        _G.toggled = true
        loadstring(game:HttpGet("https://raw.githubusercontent.com/venosu/kat/main/head.lua", true))()
        end)







        section1:addButton("Infinite Amo", function()
            local mt = getrawmetatable(game)
setreadonly(mt,false)
local nidx = mt.__newindex

mt.__newindex = newcclosure(function(a,b,c)
    if b == 'Text' and tostring(a.Name) == 'AmmoCounter' then
        return nidx(a,b,math.huge..'/3')
    end
   
    return nidx(a,b,c)
end)

local function Ammo()
    for i, v in next, getgc(true) do
        if type(v) == "table" and rawget(v, "LoadedAmmo") then
            v.LoadedAmmo = math.huge
        end
    end
end

while wait(1) do
    if game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild('Revolver') then
        spawn(function()
            pcall(function()
                game.Players.LocalPlayer.Character.Revolver.ClientEvent:FireServer("SetVisible", {[1] = false})
               
                wait(0.25)
               
                game.Players.LocalPlayer.Character.Revolver.ClientEvent:FireServer("SetVisible", {[1] = true})
                game.Players.LocalPlayer.Character.Revolver.ClientEvent:FireServer("ReloadUpdate", {[1] = "Start"})
               
                wait(0.25)
               
                game.Players.LocalPlayer.Character.Revolver.ClientEvent:FireServer("ReloadUpdate", {[1] = "AmmoAdded"})
               
                Ammo()
            end)
        end)
    end
end
            end)




            section1:addButton("Esp", function()
                --[[
A distribution of https://wearedevs.net/scripts
Created August 17, 2021, Last updated August 17, 2021

Description: Draws boxes around each player.

Credits to "Real Panda" for their ESP library

Instruction: Edit the settings as desired below and execute the script.

Settings: 
Replace "nil" with "true" to enable the setting, or "false" to disable the setting. Without the quotes. 
If you do not change "nil", the defaults will take place.
]]
_G.WRDESPEnabled = nil --Enables the ESP (Defaults to true)
_G.WRDESPBoxes = nil --Draws boxes around other players (Defaults to true)
_G.WRDESPTeamColors = nil --Distinguish different teams by their team color. If the game sets one. (Defaults to true)
_G.WRDESPTracers = nil --Displays lines leading to other players (Defaults to false)
_G.WRDESPNames = nil --Displays the names of the players within the ESP box (Defaults to true)

--Dont edit below

--Only ever load the script once
if not _G.WRDESPLoaded then    
    ----[[ First- Load Kiriot ESP Library ]]----

    --Settings--
    local ESP = {
        Enabled = false,
        Boxes = true,
        BoxShift = CFrame.new(0,-1.5,0),
        BoxSize = Vector3.new(4,6,0),
        Color = Color3.fromRGB(255, 170, 0),
        FaceCamera = false,
        Names = true,
        TeamColor = true,
        Thickness = 2,
        AttachShift = 1,
        TeamMates = true,
        Players = true,
        
        Objects = setmetatable({}, {__mode="kv"}),
        Overrides = {}
    }

    --Declarations--
    local cam = workspace.CurrentCamera
    local plrs = game:GetService("Players")
    local plr = plrs.LocalPlayer
    local mouse = plr:GetMouse()

    local V3new = Vector3.new
    local WorldToViewportPoint = cam.WorldToViewportPoint

    --Functions--
    local function Draw(obj, props)
        local new = Drawing.new(obj)
        
        props = props or {}
        for i,v in pairs(props) do
            new[i] = v
        end
        return new
    end

    function ESP:GetTeam(p)
        local ov = self.Overrides.GetTeam
        if ov then
            return ov(p)
        end
        
        return p and p.Team
    end

    function ESP:IsTeamMate(p)
        local ov = self.Overrides.IsTeamMate
        if ov then
            return ov(p)
        end
        
        return self:GetTeam(p) == self:GetTeam(plr)
    end

    function ESP:GetColor(obj)
        local ov = self.Overrides.GetColor
        if ov then
            return ov(obj)
        end
        local p = self:GetPlrFromChar(obj)
        return p and self.TeamColor and p.Team and p.Team.TeamColor.Color or self.Color
    end

    function ESP:GetPlrFromChar(char)
        local ov = self.Overrides.GetPlrFromChar
        if ov then
            return ov(char)
        end
        
        return plrs:GetPlayerFromCharacter(char)
    end

    function ESP:Toggle(bool)
        self.Enabled = bool
        if not bool then
            for i,v in pairs(self.Objects) do
                if v.Type == "Box" then --fov circle etc
                    if v.Temporary then
                        v:Remove()
                    else
                        for i,v in pairs(v.Components) do
                            v.Visible = false
                        end
                    end
                end
            end
        end
    end

    function ESP:GetBox(obj)
        return self.Objects[obj]
    end

    function ESP:AddObjectListener(parent, options)
        local function NewListener(c)
            if type(options.Type) == "string" and c:IsA(options.Type) or options.Type == nil then
                if type(options.Name) == "string" and c.Name == options.Name or options.Name == nil then
                    if not options.Validator or options.Validator(c) then
                        local box = ESP:Add(c, {
                            PrimaryPart = type(options.PrimaryPart) == "string" and c:WaitForChild(options.PrimaryPart) or type(options.PrimaryPart) == "function" and options.PrimaryPart(c),
                            Color = type(options.Color) == "function" and options.Color(c) or options.Color,
                            ColorDynamic = options.ColorDynamic,
                            Name = type(options.CustomName) == "function" and options.CustomName(c) or options.CustomName,
                            IsEnabled = options.IsEnabled,
                            RenderInNil = options.RenderInNil
                        })
                        --TODO: add a better way of passing options
                        if options.OnAdded then
                            coroutine.wrap(options.OnAdded)(box)
                        end
                    end
                end
            end
        end

        if options.Recursive then
            parent.DescendantAdded:Connect(NewListener)
            for i,v in pairs(parent:GetDescendants()) do
                coroutine.wrap(NewListener)(v)
            end
        else
            parent.ChildAdded:Connect(NewListener)
            for i,v in pairs(parent:GetChildren()) do
                coroutine.wrap(NewListener)(v)
            end
        end
    end

    local boxBase = {}
    boxBase.__index = boxBase

    function boxBase:Remove()
        ESP.Objects[self.Object] = nil
        for i,v in pairs(self.Components) do
            v.Visible = false
            v:Remove()
            self.Components[i] = nil
        end
    end

    function boxBase:Update()
        if not self.PrimaryPart then
            --warn("not supposed to print", self.Object)
            return self:Remove()
        end

        local color
        if ESP.Highlighted == self.Object then
        color = ESP.HighlightColor
        else
            color = self.Color or self.ColorDynamic and self:ColorDynamic() or ESP:GetColor(self.Object) or ESP.Color
        end

        local allow = true
        if ESP.Overrides.UpdateAllow and not ESP.Overrides.UpdateAllow(self) then
            allow = false
        end
        if self.Player and not ESP.TeamMates and ESP:IsTeamMate(self.Player) then
            allow = false
        end
        if self.Player and not ESP.Players then
            allow = false
        end
        if self.IsEnabled and (type(self.IsEnabled) == "string" and not ESP[self.IsEnabled] or type(self.IsEnabled) == "function" and not self:IsEnabled()) then
            allow = false
        end
        if not workspace:IsAncestorOf(self.PrimaryPart) and not self.RenderInNil then
            allow = false
        end

        if not allow then
            for i,v in pairs(self.Components) do
                v.Visible = false
            end
            return
        end

        if ESP.Highlighted == self.Object then
            color = ESP.HighlightColor
        end

        --calculations--
        local cf = self.PrimaryPart.CFrame
        if ESP.FaceCamera then
            cf = CFrame.new(cf.p, cam.CFrame.p)
        end
        local size = self.Size
        local locs = {
            TopLeft = cf * ESP.BoxShift * CFrame.new(size.X/2,size.Y/2,0),
            TopRight = cf * ESP.BoxShift * CFrame.new(-size.X/2,size.Y/2,0),
            BottomLeft = cf * ESP.BoxShift * CFrame.new(size.X/2,-size.Y/2,0),
            BottomRight = cf * ESP.BoxShift * CFrame.new(-size.X/2,-size.Y/2,0),
            TagPos = cf * ESP.BoxShift * CFrame.new(0,size.Y/2,0),
            Torso = cf * ESP.BoxShift
        }

        if ESP.Boxes then
            local TopLeft, Vis1 = WorldToViewportPoint(cam, locs.TopLeft.p)
            local TopRight, Vis2 = WorldToViewportPoint(cam, locs.TopRight.p)
            local BottomLeft, Vis3 = WorldToViewportPoint(cam, locs.BottomLeft.p)
            local BottomRight, Vis4 = WorldToViewportPoint(cam, locs.BottomRight.p)

            if self.Components.Quad then
                if Vis1 or Vis2 or Vis3 or Vis4 then
                    self.Components.Quad.Visible = true
                    self.Components.Quad.PointA = Vector2.new(TopRight.X, TopRight.Y)
                    self.Components.Quad.PointB = Vector2.new(TopLeft.X, TopLeft.Y)
                    self.Components.Quad.PointC = Vector2.new(BottomLeft.X, BottomLeft.Y)
                    self.Components.Quad.PointD = Vector2.new(BottomRight.X, BottomRight.Y)
                    self.Components.Quad.Color = color
                else
                    self.Components.Quad.Visible = false
                end
            end
        else
            self.Components.Quad.Visible = false
        end

        if ESP.Names then
            local TagPos, Vis5 = WorldToViewportPoint(cam, locs.TagPos.p)
            
            if Vis5 then
                self.Components.Name.Visible = true
                self.Components.Name.Position = Vector2.new(TagPos.X, TagPos.Y)
                self.Components.Name.Text = self.Name
                self.Components.Name.Color = color
                
                self.Components.Distance.Visible = true
                self.Components.Distance.Position = Vector2.new(TagPos.X, TagPos.Y + 14)
                self.Components.Distance.Text = math.floor((cam.CFrame.p - cf.p).magnitude) .."m away"
                self.Components.Distance.Color = color
            else
                self.Components.Name.Visible = false
                self.Components.Distance.Visible = false
            end
        else
            self.Components.Name.Visible = false
            self.Components.Distance.Visible = false
        end
        
        if ESP.Tracers then
            local TorsoPos, Vis6 = WorldToViewportPoint(cam, locs.Torso.p)

            if Vis6 then
                self.Components.Tracer.Visible = true
                self.Components.Tracer.From = Vector2.new(TorsoPos.X, TorsoPos.Y)
                self.Components.Tracer.To = Vector2.new(cam.ViewportSize.X/2,cam.ViewportSize.Y/ESP.AttachShift)
                self.Components.Tracer.Color = color
            else
                self.Components.Tracer.Visible = false
            end
        else
            self.Components.Tracer.Visible = false
        end
    end

    function ESP:Add(obj, options)
        if not obj.Parent and not options.RenderInNil then
            return warn(obj, "has no parent")
        end

        local box = setmetatable({
            Name = options.Name or obj.Name,
            Type = "Box",
            Color = options.Color --[[or self:GetColor(obj)]],
            Size = options.Size or self.BoxSize,
            Object = obj,
            Player = options.Player or plrs:GetPlayerFromCharacter(obj),
            PrimaryPart = options.PrimaryPart or obj.ClassName == "Model" and (obj.PrimaryPart or obj:FindFirstChild("HumanoidRootPart") or obj:FindFirstChildWhichIsA("BasePart")) or obj:IsA("BasePart") and obj,
            Components = {},
            IsEnabled = options.IsEnabled,
            Temporary = options.Temporary,
            ColorDynamic = options.ColorDynamic,
            RenderInNil = options.RenderInNil
        }, boxBase)

        if self:GetBox(obj) then
            self:GetBox(obj):Remove()
        end

        box.Components["Quad"] = Draw("Quad", {
            Thickness = self.Thickness,
            Color = color,
            Transparency = 1,
            Filled = false,
            Visible = self.Enabled and self.Boxes
        })
        box.Components["Name"] = Draw("Text", {
            Text = box.Name,
            Color = box.Color,
            Center = true,
            Outline = true,
            Size = 19,
            Visible = self.Enabled and self.Names
        })
        box.Components["Distance"] = Draw("Text", {
            Color = box.Color,
            Center = true,
            Outline = true,
            Size = 19,
            Visible = self.Enabled and self.Names
        })
        
        box.Components["Tracer"] = Draw("Line", {
            Thickness = ESP.Thickness,
            Color = box.Color,
            Transparency = 1,
            Visible = self.Enabled and self.Tracers
        })
        self.Objects[obj] = box
        
        obj.AncestryChanged:Connect(function(_, parent)
            if parent == nil and ESP.AutoRemove ~= false then
                box:Remove()
            end
        end)
        obj:GetPropertyChangedSignal("Parent"):Connect(function()
            if obj.Parent == nil and ESP.AutoRemove ~= false then
                box:Remove()
            end
        end)

        local hum = obj:FindFirstChildOfClass("Humanoid")
        if hum then
            hum.Died:Connect(function()
                if ESP.AutoRemove ~= false then
                    box:Remove()
                end
            end)
        end

        return box
    end

    local function CharAdded(char)
        local p = plrs:GetPlayerFromCharacter(char)
        if not char:FindFirstChild("HumanoidRootPart") then
            local ev
            ev = char.ChildAdded:Connect(function(c)
                if c.Name == "HumanoidRootPart" then
                    ev:Disconnect()
                    ESP:Add(char, {
                        Name = p.Name,
                        Player = p,
                        PrimaryPart = c
                    })
                end
            end)
        else
            ESP:Add(char, {
                Name = p.Name,
                Player = p,
                PrimaryPart = char.HumanoidRootPart
            })
        end
    end
    local function PlayerAdded(p)
        p.CharacterAdded:Connect(CharAdded)
        if p.Character then
            coroutine.wrap(CharAdded)(p.Character)
        end
    end
    plrs.PlayerAdded:Connect(PlayerAdded)
    for i,v in pairs(plrs:GetPlayers()) do
        if v ~= plr then
            PlayerAdded(v)
        end
    end

    game:GetService("RunService").RenderStepped:Connect(function()
        cam = workspace.CurrentCamera
        for i,v in (ESP.Enabled and pairs or ipairs)(ESP.Objects) do
            if v.Update then
                local s,e = pcall(v.Update, v)
                if not s then warn("[EU]", e, v.Object:GetFullName()) end
            end
        end
    end)

    ----[[ Now Begins WRD's modification for implementation ]]----

    --Sets defaults where required
    if _G.WRDESPEnabled == nil then _G.WRDESPEnabled = true end
    if _G.WRDESPBoxes == nil then _G.WRDESPBoxes = true end
    if _G.WRDESPTeamColors == nil then _G.WRDESPTeamColors = true end
    if _G.WRDESPTracers == nil then _G.WRDESPTracers = false end
    if _G.WRDESPNames == nil then _G.WRDESPNames = true end
	
	--Hacky way to keep up with setting changes
    while wait(.1) do
        ESP:Toggle(_G.WRDESPEnabled or false)
        ESP.Boxes = _G.WRDESPBoxes or false
        ESP.TeamColors = _G.WRDESPTeamColors or false
        ESP.Tracers = _G.WRDESPTracers or false
        ESP.Names = _G.WRDESPNames or false
    end

    _G.WRDESPLoaded = true
end
            end)





















            local page2 = venyx:addPage("Local Player", 8097641254)
            local Farm = page2:addSection("Local Player")
    

    
            local Farm = page2:addSection("Infinite Jump")
        local RANKUP
        Farm:addToggle("Inf Jump", nil, function(bool)
            game:GetService("UserInputService").JumpRequest:connect(function()
                game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
            end)
            RANKUP = bool
        end)
    
    
    
    
    
        local Farm = page2:addSection("Anti-Afk")
        local RANKUP
        Farm:addToggle("Anti-Afk", nil, function(bool)
            wait(0.5)local ba=Instance.new("ScreenGui")
            local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
            local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
            ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
            ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
            ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
            ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
            ca.TextSize=22;da.Parent=ca
            da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
            da.Size=UDim2.new(0,304,0,107)_b.Parent=da
            _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
            _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
            _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
            ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
            ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
            ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
            game:service'Players'.LocalPlayer.Idled:connect(function()
            bb:CaptureController()bb:ClickButton2(Vector2.new())
            ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
            RANKUP = bool
        end)
    
    
    
        local Farm = page2:addSection("Fly with (E)")
        local RANKUP
        Farm:addToggle("Fly (E)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/7rXZ9VNc", true))()
            RANKUP = bool
        end)
    
    



        local Title = page2:addSection("Reset Character")
    
    
        Title:addButton("Reset", function()
            game.Players.LocalPlayer.Character.Head:Remove()
        end)
    
    



    
    
        local Farm = page2:addSection("Noclip with (R)")
        local RANKUP
        Farm:addToggle("Noclip (R)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()		
            RANKUP = bool
        end)
    



    
    
    
        local Farm = page2:addSection("Alt Delete")
        local RANKUP
        Farm:addToggle("Alt Delet", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()		
            RANKUP = bool
        end)
    
    
    
    
        local Farm = page2:addSection("Ctrl Teleport")
        local RANKUP
        Farm:addToggle("Ctrl Teleport", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/gp9y2Wht", true))()	
            RANKUP = bool
        end)
    
    
    
        local Farm = page2:addSection("God Mode")
        local RANKUP
        Farm:addToggle("God Mode", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/MSZAznxp", true))()
            RANKUP = bool
        end)
















        local page5 = venyx:addPage("Credits", 5012544693)
        local Discord = page5:addSection("Discord")
        
        
        Discord:addButton("Copy Discord Link", function()
            setclipboard("https://discord.gg/2NyAaSRtJu")
        end)
        local Discord = page5:addSection("Credits")
        local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
        
        
        
        
        
        
        
            -- themes
            local themes = {
                Background = Color3.fromRGB(24, 24, 24),
                Glow = Color3.fromRGB(0, 0, 0),
                Accent = Color3.fromRGB(10, 10, 10),
                LightContrast = Color3.fromRGB(20, 20, 20),
                DarkContrast = Color3.fromRGB(14, 14, 14),
                TextColor = Color3.fromRGB(255, 255, 255)
                }
                
                    
                -- Theme page
                local settings = venyx:addPage("Settings", 8087082683)
                local colors = settings:addSection("Colors")
                local setting = settings:addSection("Settings")
                
                setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                print("Activated Keybind")
                venyx:toggle()
                end, function()
                print("Changed Keybind")
                end)
                
                for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                colors:addColorPicker(theme, color, function(color3)
                venyx:setTheme(theme, color3)
                end)
                
            
            
            end
            
            
            
            
            
            
            
            
            -- load
                venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                end







































                






































































    



    if game.PlaceId == 2788229376 then
        local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
        local venyx = library.new("Vex Hub: Da Hood", 5013109572)

        






        local page1 = venyx:addPage("Local Player", 8162222302)
        local Farm = page1:addSection("ESP")





        local RANKUP
        Farm:addToggle("Esp", nil, function(bool)
            local MainParent = game.workspace.Terrain or nil
local LineFrame = Instance.new("ScreenGui",MainParent)
LineFrame.Name = "Lines"
LineFrame.Enabled = false
ToggleKey = Enum.KeyCode.F1
local Spotted = {};
local CharacterMotors = {}
CharacterMotors.GetMotors = function(char)
    local Motors = {}
        for i,v in pairs(char:GetDescendants()) do
            if v:IsA("Motor6D") then
                if v.Part0 and v.Part1 then--and v.Part0.Name ~= "HumanoidRootPart" and v.Part1.Name ~= "HumanoidRootPart" then
                    table.insert(Motors,{v.Part0,v.Part1})
                end
            end
        end
    table.insert(Motors,{char:FindFirstChild("Head") or char.PrimaryPart,"Camera"})
    CharacterMotors[char] = Motors
    return CharacterMotors[char]
end
        
lerp = function(a, b, t)
    return a + (b - a) * t
end
 
local ESP = {Characters = {}}
ESP.Visible = true
ESP.Init = function(char,plr)
    --if (game:GetService("Players").LocalPlayer.Team == nil or plr.Team ~= game:GetService("Players").LocalPlayer.Team) then
        char.DescendantAdded:Connect(function()
            CharacterMotors.GetMotors(char)
        end)
        
        local BillboardUi = Instance.new("BillboardGui")
        BillboardUi.AlwaysOnTop = true
        BillboardUi.Size = UDim2.new(3,60,1,30)
        BillboardUi.StudsOffsetWorldSpace = Vector3.new(0,-4.5,0)
        BillboardUi.Adornee = char:WaitForChild("HumanoidRootPart")
        
        local PlayerName = Instance.new("TextLabel",BillboardUi)
        PlayerName.BackgroundTransparency = 1
        PlayerName.TextColor3 = (game:GetService("Players"):GetPlayerFromCharacter(char)).TeamColor.Color
        PlayerName.Size = UDim2.new(1,0,.3,0)
        PlayerName.ZIndex = 2
        PlayerName.Text = char.Name
        PlayerName.TextScaled = true
        PlayerName.TextStrokeTransparency = .25
        PlayerName.Font = Enum.Font.GothamBold
        PlayerName.TextStrokeColor3 = Color3.fromRGB(33, 33, 33)
        
        local Distance = PlayerName:Clone()
        Distance.Parent = BillboardUi
        Distance.Font = Enum.Font.Gotham
        Distance.TextColor3 = Color3.new(1,1,1)
        Distance.Position = UDim2.new(0,0,.3,0)
        
        local Health = PlayerName:Clone()
        Health.Parent = BillboardUi
        Health.Font = Enum.Font.Gotham
        Health.Position = UDim2.new(0,0,.6,0)
        
        ESP.Characters[char] = {PlayerName,Distance,Health,BillboardUi}
    --end
end
ESP.Render = function()
    
    for i,v in pairs(ESP.Characters) do
        pcall(function()
            local shrink = ((((game.Workspace.CurrentCamera.CFrame.p) - i.HumanoidRootPart.Position).Magnitude)/1500)+1
            v[2].Text = math.floor(((game.Workspace.CurrentCamera.CFrame.p) - i.HumanoidRootPart.Position).Magnitude+.5)
            v[3].Text = math.floor(i.Humanoid.Health).."/"..i.Humanoid.MaxHealth.." - "..math.floor(((i.Humanoid.Health/i.Humanoid.MaxHealth)*100)+.5).."%"
            v[3].TextColor3 = Color3.fromHSV((i.Humanoid.Health/i.Humanoid.MaxHealth) * (80/255),1,1)
            if not Spotted[i] then
                --v[1].TextTransparency = lerp(v[1].TextTransparency,.6,0.05)
            else
                --v[1].TextTransparency = lerp(v[1].TextTransparency,0,0.1)
            end
            v[1].TextColor3 = (game:GetService("Players"):GetPlayerFromCharacter(i)).TeamColor.Color
            --v[1].TextStrokeTransparency = 1-((1-v[1].TextTransparency)/2)
            --v[2].TextTransparency = v[1].TextTransparency
            --v[2].TextStrokeTransparency = v[1].TextStrokeTransparency
            --v[3].TextTransparency = v[1].TextTransparency
            --v[3].TextStrokeTransparency = v[1].TextStrokeTransparency
            v[4].Size = UDim2.new(3,60/shrink,1,30/shrink)
            v[1].Visible = ESP.Visible
            v[2].Visible = ESP.Visible
            v[3].Visible = ESP.Visible
            v[4].Parent = MainParent
            
        end)
    end
    
end
 
local Perspective = {}
Perspective.CalculatePoint = function(position,cam)
    local vector, onScreen = cam:WorldToScreenPoint(position)
    return Vector2.new(vector.X, vector.Y),vector.Z,onScreen
end
 
local Draw = {UsedLines = {}}
Draw.Line = function(a,b,line,width)
    if a and b then 
        local lerp = a:Lerp(b,.5)
        local Magnitude = (a-b).Magnitude
        line.AnchorPoint = Vector2.new(0.5,.5)
        line.Position = UDim2.new(lerp.X/game.Workspace.CurrentCamera.ViewportSize.X,0,(lerp.Y/(game.Workspace.CurrentCamera.ViewportSize.Y-36)),36/2)
        line.Size = UDim2.new(Magnitude/line.Parent.AbsoluteSize.X,0,0,width)
        line.Rotation = math.deg(math.atan2(a.y - b.y, a.x - b.x))
    else
        line:Destroy()
    end
end
 
 
Draw.Character = function(player,lines,cam)
    local Motors = CharacterMotors[player]
    if not Motors then
        Motors = CharacterMotors.GetMotors(player)
    end
 
    for i,v in pairs(Motors) do
        if v[1] and v[2] then
            local FoundLine = nil
            for i,v in pairs(lines:GetChildren()) do
                if Draw.UsedLines[v] == nil then
                    Draw.UsedLines[v] = true
                    FoundLine = v
                    break
                end
            end
            local a2d,az,screen = Perspective.CalculatePoint(v[1].Position,cam)
            local b2d,bz,screen2
            local v2pos = v[2].Position
            Spotted[player] = false
            if v[2] == "Camera" then
                local ray = Ray.new(v[1].Position, (cam.CFrame.p - v[1].Position).unit * (cam.CFrame.p - v[1].Position).Magnitude)
                local part, position = workspace:FindPartOnRayWithIgnoreList(ray, {game:GetService("Players").LocalPlayer.Character,player}, false, true)
                if part then
                    screen = false
                    screen2 = false
                else
                    Spotted[player] = true
                    b2d,bz,screen2 = Vector2.new(cam.ViewportSize.x/2, cam.ViewportSize.y),0,true   
                    screen = true
                end
                v2pos = v[1].Position
            else
                b2d,bz,screen2 = Perspective.CalculatePoint(v[2].Position,cam)  
            end
            if screen and screen2 and (v[1].Position-v2pos).Magnitude <= 5 then
                if not FoundLine then
                    FoundLine = Instance.new("Frame")
                    FoundLine.BackgroundColor3 = Color3.new(1,1,1)
                    FoundLine.BackgroundTransparency = .25
                    FoundLine.BorderSizePixel = 0
                    FoundLine.Parent = lines    
                    Draw.UsedLines[FoundLine] = true
                end
                if screen then
                    Draw.Line(a2d,b2d,FoundLine,1)
                else
                    Draw.Line(b2d,a2d,FoundLine,1)
                end
            elseif FoundLine then
                FoundLine:Destroy()
            end
        end
    end
end
 
Draw.ResetLines = function(lines)
    for i,v in pairs(lines:GetChildren()) do
        if Draw.UsedLines[v] == nil then
            v:Destroy()
        end
    end
    Draw.UsedLines = {}
end
 
local AddPlayer = function(plr)
    coroutine.resume(coroutine.create(function()
        if plr ~= game:GetService("Players").LocalPlayer  then
            if plr.Character then
                ESP.Init(plr.Character,plr)
            end
            plr.CharacterAdded:Connect(function(cha)
                ESP.Init(cha,plr)
            end)
        end
    end))
end
 
for i,v in pairs(game:GetService("Players"):GetChildren()) do
    AddPlayer(v)
end
game:GetService("Players").PlayerAdded:Connect(function(v)
    AddPlayer(v)
end)
game:GetService("UserInputService").InputBegan:connect(function(inputObject)
    if inputObject.KeyCode == ToggleKey then
        ESP.Visible = not ESP.Visible
    end
end)
game:GetService("RunService").RenderStepped:Connect(function()
    ESP.Render()
    for i,v in pairs(game:GetService("Players"):GetChildren()) do
        if v.Character and v ~= game:GetService("Players").LocalPlayer and (game:GetService("Players").LocalPlayer.Team == nil or v.Team ~= game:GetService("Players").LocalPlayer.Team) then
            if v.Character.PrimaryPart and (v.Character.PrimaryPart.Position - game.Workspace.CurrentCamera.CFrame.Position).Magnitude <= 200 then
                Draw.Character(v.Character,LineFrame,game.Workspace.CurrentCamera)
            end
        end
    end
    Draw.ResetLines(LineFrame)
end)

            RANKUP = bool
        end)
    
    





        local Farm = page1:addSection("Infinite Jump")
        local RANKUP
        Farm:addToggle("Inf Jump", nil, function(bool)
            game:GetService("UserInputService").JumpRequest:connect(function()
                game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
            end)
            RANKUP = bool
        end)
    




       
    

        local Farm = page1:addSection("Noclip with (R)")
        local RANKUP
        Farm:addToggle("Noclip (R)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()
            RANKUP = bool
        end)


        local Farm = page1:addSection("Alt Delet")
        local RANKUP
        Farm:addToggle("Alt Delet", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()	
            RANKUP = bool
        end)


        





        



        local Farm = page1:addSection("Anti-Afk")
        local RANKUP
        Farm:addToggle("Anti-Afk", nil, function(bool)
            wait(0.5)local ba=Instance.new("ScreenGui")
    local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
    local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
    ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
    ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
    ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
    ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
    ca.TextSize=22;da.Parent=ca
    da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
    da.Size=UDim2.new(0,304,0,107)_b.Parent=da
    _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
    _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
    _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
    ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
    ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
    ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
    game:service'Players'.LocalPlayer.Idled:connect(function()
    bb:CaptureController()bb:ClickButton2(Vector2.new())
    ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
            RANKUP = bool
        end)




        local page2 = venyx:addPage("AutoFarm", 8419465385)
        local Farm = page2:addSection("Farming")




        
    
    
    
    





        local RANKUP
        Farm:addToggle("AutoFarm Money", nil, function(bool)
            loadstring(game:HttpGet("https://raw.githubusercontent.com/xaxaxaxaxaxaxaxaxa/Bypasses/main/Da-Hood", true))()

if not getgenv().Settings then 
    getgenv().Settings = {
        Enabled = true, -- Dont mess with this, just rejoin the game to turn the autofarm off
        TeleportSpeed = 5, -- The Lower the Faster, the Higher the Slower
    }
end

local Players, RService, TweenService = game:GetService"Players", game:GetService"RunService", game:GetService"TweenService";
local Client, CF, INew, Vec3 = Players.LocalPlayer, CFrame.new, Instance.new, Vector3.new;

local Path = workspace:WaitForChild"Ignored".Drop

function TweenTo(Part, Speed)
    local ClientPart = Client.Character:FindFirstChild"HumanoidRootPart";
    local TweenInformation = TweenService:Create(ClientPart, TweenInfo.new(
        Speed, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {CFrame = Part}
    )
    
    if ClientPart and Part then 
        TweenInformation:Play()
    end
end

function FarmMoney()
    local SitDetection = Client.Character:WaitForChild"Humanoid".Sit
    
    while RService.RenderStepped:Wait() and getgenv().Settings.Enabled == true do 
        if SitDetection == true then 
            SitDetection = false 
        end
        
        for _, v in next, Path:GetChildren() do 
            if v and v:IsA"Part" and v.Name == "MoneyDrop" then 
                local FoundMoney = v
                local ClickDetector = FoundMoney:FindFirstChild"ClickDetector";
                local ClientPart = Client.Character:WaitForChild"HumanoidRootPart";
                
                if ClickDetector and ClientPart then 
                    TweenTo(CF(FoundMoney.Position), getgenv().Settings.TeleportSpeed)
                    
                    repeat RService.RenderStepped:Wait()
                    until ((ClientPart.Position - FoundMoney.Position).Magnitude <= ClickDetector.MaxActivationDistance)
                    
                    fireclickdetector(ClickDetector)
                end
            end
        end
    end
end
FarmMoney()

do 
    for _, v in next, workspace:GetDescendants() do 
        if v and v:IsA"Seat" then 
            v:Destroy()
        end
    end
end

Client.CharacterAdded:Connect(function()
    Client.Character:WaitForChild"Humanoid"
    
    FarmMoney()
end)

workspace.DescendantAdded:Connect(function(Descendant)
    if Descendant and Descendant:IsA"Seat" then 
        Descendant:Destroy()
    end
end)

Path.ChildAdded:Connect(function()
    FarmMoney()
end)
            RANKUP = bool
        end)

        
        




        Farm:addButton("Auto Rob", function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/rapnz/scripts/master/DaHoodFarm.lua"))()
        end)
    
    





        

        












    local page5 = venyx:addPage("Credits", 5012544693)
    local Discord = page5:addSection("Discord")
    
    
    Discord:addButton("Copy Discord Link", function()
        setclipboard("https://discord.gg/2NyAaSRtJu")
    end)
    local Discord = page5:addSection("Credits")
    local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
    
    -- themes
    local themes = {
    Background = Color3.fromRGB(24, 24, 24),
    Glow = Color3.fromRGB(0, 0, 0),
    Accent = Color3.fromRGB(10, 10, 10),
    LightContrast = Color3.fromRGB(20, 20, 20),
    DarkContrast = Color3.fromRGB(14, 14, 14),
    TextColor = Color3.fromRGB(255, 255, 255)
    }
    
        
    -- Theme page
    local settings = venyx:addPage("Settings", 8419885246)
    local colors = settings:addSection("Colors")
    local setting = settings:addSection("Settings")
    
    setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
    print("Activated Keybind")
    venyx:toggle()
    end, function()
    print("Changed Keybind")
    end)
    
    for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
    colors:addColorPicker(theme, color, function(color3)
    venyx:setTheme(theme, color3)
    end)
    end
    
    -- load
    venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
end








































































    if game.PlaceId == 142823291 then
        local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
        local venyx = library.new("Ez W Hub: Murder Mystery 2", 5013109572)




        local page5 = venyx:addPage("Main", 5012544693)
    local Discord = page5:addSection("Discord")
    
    
    Discord:addButton("Copy Discord Link", function()
        setclipboard("https://discord.gg/JdEK5qN7Yb")
    end)
    local Discord = page5:addSection("Credits")
    local d = page5:addSection("Leon!#0831")
    local d = page5:addSection("Leon!#0831")
    
    
    
    
    
        

local page2 = venyx:addPage("Local Player", 5012544693)
 

        
   

 local Farm = page2:addSection("Infinite Jump")
    local RANKUP
    Farm:addToggle("Inf Jump", nil, function(bool)
        game:GetService("UserInputService").JumpRequest:connect(function()
            game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
        end)
		RANKUP = bool
    end)





    local Farm = page2:addSection("Fly with (E)")
    local RANKUP
    Farm:addToggle("Fly (E)", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/7rXZ9VNc", true))()
		RANKUP = bool
    end)




    local Farm = page2:addSection("Noclip with (R)")
    local RANKUP
    Farm:addToggle("Noclip (R)", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()		
        RANKUP = bool
    end)






    local Farm = page2:addSection("Alt Delet")
    local RANKUP
    Farm:addToggle("Alt Delet", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()		
        RANKUP = bool
    end)




    local Farm = page2:addSection("Ctrl Teleport")
    local RANKUP
    Farm:addToggle("Ctrl Teleport", nil, function(bool)
        --[[local Plr = game:GetService("Players").LocalPlayer
local Mouse = Plr:GetMouse()
 
Mouse.Button1Down:connect(function()
if not game:GetService("UserInputService"):IsKeyDown(Enum.KeyCode.LeftControl) then return end
if not Mouse.Target then return end
Plr.Character:MoveTo(Mouse.Hit.p)
end)
--]]
    game:GetService("StarterGui"):SetCore("SendNotification",{
        Title = "CTRL click tp",
        Text = "Hold Ctrl then press click to a place you want to teleport to.",
        Duration = 6,
            })
        local speed = 100 -- set this lower to make it slower
        local bodyvelocityenabled = true -- set this to false if you are getting kicked
         
        local Imput = game:GetService("UserInputService")
        local Plr = game.Players.LocalPlayer
        local Mouse = Plr:GetMouse()
         
        function To(position)
        local Chr = Plr.Character
        if Chr ~= nil then
        local ts = game:GetService("TweenService")
        local char = game.Players.LocalPlayer.Character
        local hm = char.HumanoidRootPart
        local dist = (hm.Position - Mouse.Hit.p).magnitude
        local tweenspeed = dist/tonumber(speed)
        local ti = TweenInfo.new(tonumber(tweenspeed), Enum.EasingStyle.Linear)
        local tp = {CFrame = CFrame.new(position)}
        ts:Create(hm, ti, tp):Play()
        if bodyvelocityenabled == true then
        local bv = Instance.new("BodyVelocity")
        bv.Parent = hm
        bv.MaxForce = Vector3.new(100000,100000,100000)
        bv.Velocity = Vector3.new(0,0,0)
        wait(tonumber(tweenspeed))
        bv:Destroy()
        end
        end
        end
         
        Imput.InputBegan:Connect(function(input)
           if input.UserInputType == Enum.UserInputType.MouseButton1 and Imput:IsKeyDown(Enum.KeyCode.LeftControl) then
               To(Mouse.Hit.p)
           end
        end)	
        RANKUP = bool
    end)



    local Farm = page2:addSection("God Mode")
    local RANKUP
    Farm:addToggle("God Mode", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/MSZAznxp", true))()
        RANKUP = bool
    end)





    local Farm = page2:addSection("Anti-Afk")
    local RANKUP
    Farm:addToggle("Anti-Afk", nil, function(bool)
        wait(0.5)local ba=Instance.new("ScreenGui")
        local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
        local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
        ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
        ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
        ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
        ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
        ca.TextSize=22;da.Parent=ca
        da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
        da.Size=UDim2.new(0,304,0,107)_b.Parent=da
        _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
        _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
        _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
        ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
        ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
        ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
        game:service'Players'.LocalPlayer.Idled:connect(function()
        bb:CaptureController()bb:ClickButton2(Vector2.new())
        ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
        RANKUP = bool
    end)



local page3 = venyx:addPage("Visual", 5012544693)
local Farm = page3:addSection("Esp")
local Esp
    Farm:addToggle("Esp", nil, function(bool)
        loadstring(game:HttpGet(('https://pastebin.com/raw/ypSsQRK6'),true))()
		Esp = bool
    end)

    local d = page3:addSection("Esp is with Gun Esp")

    

local fd = page3:addSection("Unlock Xbox Item")
                    fd:addButton("Unlock", function()
        game:GetService("ReplicatedStorage").IsXbox:FireServer()

    end)

    
    
    
    
    
  
    
    
    
    
    
    
    
    
    
   
                   
                   
                   
                   
                   
    local page8 = venyx:addPage("Teleports", 5012544693)
    
    
    

       
                    
                    
    local Title = page8:addSection("Lobby")
    Title:addButton("Teleport", function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-108.25495147705, 138.3260345459, 41.639129638672)
    end)

    local Test = page8:addSection("Waiting Room")
    Test:addButton("Teleport", function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-108.14199829102, 140.67608642578, 83.178932189941)
    end)





    local df = page8:addSection("Map")
    df:addButton("Teleport", function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(413.26495361328, 46.076118469238, 36.120166778564)
    end)



    local page5 = venyx:addPage("Credits", 5012544693)
    local Discord = page5:addSection("Discord")
    
    
    Discord:addButton("Copy Discord Link", function()
        setclipboard("https://discord.gg/2NyAaSRtJu")
    end)
    local Discord = page5:addSection("Credits")
    local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")



-- themes
    local themes = {
    Background = Color3.fromRGB(24, 24, 24),
    Glow = Color3.fromRGB(0, 0, 0),
    Accent = Color3.fromRGB(10, 10, 10),
    LightContrast = Color3.fromRGB(20, 20, 20),
    DarkContrast = Color3.fromRGB(14, 14, 14),
    TextColor = Color3.fromRGB(255, 255, 255)
    }
    
        
    -- Theme page
    local settings = venyx:addPage("Settings", 5012544693)
    local colors = settings:addSection("Colors")
    local setting = settings:addSection("Settings")
    
    setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
    print("Activated Keybind")
    venyx:toggle()
    end, function()
    print("Changed Keybind")
    end)
    
    for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
    colors:addColorPicker(theme, color, function(color3)
    venyx:setTheme(theme, color3)
    end)
    end











-- load
    venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
    end























    
    










































    if game.PlaceId == 1240123653 then
        local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
        local venyx = library.new("Vex Hub: Zombie Attack", 5013109572)
        
        
        
        
        
        
        











        
        
        
        
        local page2 = venyx:addPage("Local Player", 5012544693)
        local Farm = page2:addSection("Local Player")

        local Farm = page2:addSection("Infinite Jump")
    local RANKUP
    Farm:addToggle("Inf Jump", nil, function(bool)
        game:GetService("UserInputService").JumpRequest:connect(function()
            game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
        end)
		RANKUP = bool
    end)





    local Farm = page2:addSection("Anti-Afk")
    local RANKUP
    Farm:addToggle("Anti-Afk", nil, function(bool)
        wait(0.5)local ba=Instance.new("ScreenGui")
        local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
        local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
        ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
        ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
        ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
        ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
        ca.TextSize=22;da.Parent=ca
        da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
        da.Size=UDim2.new(0,304,0,107)_b.Parent=da
        _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
        _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
        _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
        ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
        ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
        ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
        game:service'Players'.LocalPlayer.Idled:connect(function()
        bb:CaptureController()bb:ClickButton2(Vector2.new())
        ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
        RANKUP = bool
    end)



    local Farm = page2:addSection("Fly with (E)")
    local RANKUP
    Farm:addToggle("Fly (E)", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/7rXZ9VNc", true))()
		RANKUP = bool
    end)




    local Farm = page2:addSection("Noclip with (R)")
    local RANKUP
    Farm:addToggle("Noclip (R)", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()		
        RANKUP = bool
    end)






    local Farm = page2:addSection("Alt Delet")
    local RANKUP
    Farm:addToggle("Alt Delet", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()		
        RANKUP = bool
    end)




    local Farm = page2:addSection("Ctrl Teleport")
    local RANKUP
    Farm:addToggle("Ctrl Teleport", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/gp9y2Wht", true))()	
        RANKUP = bool
    end)



    local Farm = page2:addSection("God Mode")
    local RANKUP
    Farm:addToggle("God Mode", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/MSZAznxp", true))()
        RANKUP = bool
    end)














local page3 = venyx:addPage("AutoFarm", 5012544693)
        local Farm = page3:addSection("AutoFarm")
        local RANKUP
        Farm:addToggle("AutoFarm", nil, function(bool)
            -- Equilibrium Special Zombie_Attack Auto_Farming Enjoy Heart
local groundDistance = 8
local Player = game:GetService("Players").LocalPlayer
local function getNearest()
local nearest, dist = nil, 99999
for _,v in pairs(game.Workspace.BossFolder:GetChildren()) do
if(v:FindFirstChild("Head")~=nil)then
local m =(Player.Character.Head.Position-v.Head.Position).magnitude
if(m<dist)then
dist = m
nearest = v
end
end
end
for _,v in pairs(game.Workspace.enemies:GetChildren()) do
if(v:FindFirstChild("Head")~=nil)then
local m =(Player.Character.Head.Position-v.Head.Position).magnitude
if(m<dist)then
dist = m
nearest = v
end
end
end
return nearest
end
_G.farm2 = true
Player.Chatted:Connect(function(m)
if(m==";autofarm false")then
_G.farm2 = false
elseif(m==";autofarm true")then
_G.farm2 = true
end
end)
_G.globalTarget = nil
game:GetService("RunService").RenderStepped:Connect(function()
if(_G.farm2==true)then
local target = getNearest()
if(target~=nil)then
game:GetService("Workspace").CurrentCamera.CFrame = CFrame.new(game:GetService("Workspace").CurrentCamera.CFrame.p, target.Head.Position)
Player.Character.HumanoidRootPart.CFrame = (target.HumanoidRootPart.CFrame * CFrame.new(0, groundDistance, 9))
_G.globalTarget = target
end
end
end)
spawn(function()
while wait() do
game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(0,0,0)
game.Players.LocalPlayer.Character.Torso.Velocity = Vector3.new(0,0,0)
end
end)
while wait() do
if(_G.farm2==true and _G.globalTarget~=nil and _G.globalTarget:FindFirstChild("Head") and Player.Character:FindFirstChildOfClass("Tool"))then
local target = _G.globalTarget
game.ReplicatedStorage.Gun:FireServer({["Normal"] = Vector3.new(0, 0, 0), ["Direction"] = target.Head.Position, ["Name"] = Player.Character:FindFirstChildOfClass("Tool").Name, ["Hit"] = target.Head, ["Origin"] = target.Head.Position, ["Pos"] = target.Head.Position,})
wait()
end
end
            RANKUP = bool
        end)
    
    














        local page5 = venyx:addPage("Credits", 5012544693)
        local Discord = page5:addSection("Discord")
        
        
        Discord:addButton("Copy Discord Link", function()
            setclipboard("https://discord.gg/2NyAaSRtJu")
        end)
        local Discord = page5:addSection("Credits")
        local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
    







    -- themes
    local themes = {
        Background = Color3.fromRGB(24, 24, 24),
        Glow = Color3.fromRGB(0, 0, 0),
        Accent = Color3.fromRGB(10, 10, 10),
        LightContrast = Color3.fromRGB(20, 20, 20),
        DarkContrast = Color3.fromRGB(14, 14, 14),
        TextColor = Color3.fromRGB(255, 255, 255)
        }
        
            
        -- Theme page
        local settings = venyx:addPage("Settings", 5012544693)
        local colors = settings:addSection("Colors")
        local setting = settings:addSection("Settings")
        
        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
        print("Activated Keybind")
        venyx:toggle()
        end, function()
        print("Changed Keybind")
        end)
        
        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
        colors:addColorPicker(theme, color, function(color3)
        venyx:setTheme(theme, color3)
        end)
        end
    
    
    
    
    
    
    
    
    
    
    
    -- load
        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
        end


























































        if game.PlaceId == 3956818381 then
            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
            local venyx = library.new("Vex Hub: Ninja Legends", 5013109572)













            local page2 = venyx:addPage("Local Player", 5012544693)
        local Farm = page2:addSection("Local Player")

        local Farm = page2:addSection("Infinite Jump")
    local RANKUP
    Farm:addToggle("Inf Jump", nil, function(bool)
        game:GetService("UserInputService").JumpRequest:connect(function()
            game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
        end)
		RANKUP = bool
    end)





    local Farm = page2:addSection("Anti-Afk")
    local RANKUP
    Farm:addToggle("Anti-Afk", nil, function(bool)
        wait(0.5)local ba=Instance.new("ScreenGui")
        local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
        local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
        ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
        ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
        ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
        ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
        ca.TextSize=22;da.Parent=ca
        da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
        da.Size=UDim2.new(0,304,0,107)_b.Parent=da
        _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
        _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
        _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
        ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
        ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
        ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
        game:service'Players'.LocalPlayer.Idled:connect(function()
        bb:CaptureController()bb:ClickButton2(Vector2.new())
        ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
        RANKUP = bool
    end)



    local Farm = page2:addSection("Fly with (E)")
    local RANKUP
    Farm:addToggle("Fly (E)", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/7rXZ9VNc", true))()
		RANKUP = bool
    end)




    local Farm = page2:addSection("Noclip with (R)")
    local RANKUP
    Farm:addToggle("Noclip (R)", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()		
        RANKUP = bool
    end)






    local Farm = page2:addSection("Alt Delete")
    local RANKUP
    Farm:addToggle("Alt Delet", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()		
        RANKUP = bool
    end)




    local Farm = page2:addSection("Ctrl Teleport")
    local RANKUP
    Farm:addToggle("Ctrl Teleport", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/gp9y2Wht", true))()	
        RANKUP = bool
    end)



    local Farm = page2:addSection("God Mode")
    local RANKUP
    Farm:addToggle("God Mode", nil, function(bool)
        loadstring(game:HttpGet("https://pastebin.com/raw/MSZAznxp", true))()
        RANKUP = bool
    end)



















    local page7 = venyx:addPage("AutoFarm", 5012544693)
    


local Farm = page7:addSection("AutoFarm")
local RANKUP
    Farm:addToggle("Auto Swing", nil, function(bool)
        _G.swing = true
while _G.swing do
wait()
game.Players.LocalPlayer.ninjaEvent:FireServer("swingKatana")
end
		RANKUP = bool
    end)
    
    
    
    local Farm = page7:addSection("Auto Rank")
    local RANKUP
    Farm:addToggle("Auto Rank", nil, function(bool)
        _G.sword = true
while _G.sword do
wait()
--This script was generated by Hydroxide
local oh1 = "buyRank"
local oh2 = game:GetService("ReplicatedStorage").Ranks.Ground:GetChildren()
for i = 1,#oh2 do
game:GetService("Players").LocalPlayer.ninjaEvent:FireServer(oh1, oh2[i].Name)
end
end
		RANKUP = bool
    end)






    local Farm = page7:addSection("Auto buy Skills")
    local RANKUP
    Farm:addToggle("Auto Skills", nil, function(bool)
        _G.sword = true
while _G.sword do
wait()
--This script was generated by Hydroxide
local oh1 = "buyAllSkills"
local oh2 = {"Ground", "Astral Island", "Dragon Legend Island"}
for i = 1, #oh2 do
    game:GetService("Players").LocalPlayer.ninjaEvent:FireServer(oh1, oh2[i])
end
end
		RANKUP = bool
    end)






    local Farm = page7:addSection("Auto buy belt")
    local RANKUP
    Farm:addToggle("Auto buy belt", nil, function(bool)
        _G.sword = true
while _G.sword do
wait()
--This script was generated by Hydroxide
local oh1 = "buyAllBelts"
local oh2 = {"Ground", "Astral Island", "Golden Master Island"}
for i = 1, #oh2 do
    game:GetService("Players").LocalPlayer.ninjaEvent:FireServer(oh1, oh2[i])
end
end
		RANKUP = bool
    end)











    local Farm = page7:addSection("Auto buy Swords")
    local RANKUP
    Farm:addToggle("Auto buy Swords", nil, function(bool)
        _G.sword = true
while _G.sword do
wait()
--This script was generated by Hydroxide
local oh1 = "buyAllSwords"
local oh2 = {"Ground", "Astral Island", "Dragon Legend Island"}
for i = 1, #oh2 do
    game:GetService("Players").LocalPlayer.ninjaEvent:FireServer(oh1, oh2[i])
end
end
		RANKUP = bool
    end)




    
    





local Farm = page7:addSection("Auto Sell")

local RANKUP
    Farm:addToggle("Auto Sell", nil, function(bool)
        _G.Condition = true -- true turns it on, false turns it off
        while _G.Condition == true do
        wait(1)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(84.2945251, 87069.0391, 123.435143)
        wait()
      end
		RANKUP = bool
    end)




local page9 = venyx:addPage("Elements", 5012544693)


local Title = page9:addSection("Unlock Frost Element")
     Title:addButton("Unlock Frost Element", function()
        game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Frost")
    end)



local fd = page9:addSection("Unlock Lightning Element")
     fd:addButton("Unlock Lightning Element", function()
    game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Lightning")
    end)

  
  
    
local fds = page9:addSection("Unlock Inferno Element")
     fds:addButton("Unlock Inferno Element", function()
       game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Inferno")
    end)
    




    local Electral = page9:addSection("Unlock Electral Chaos Element")
    Electral:addButton("Unlock Electral Chaos Element", function()
        game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Electral Chaos")
    end)






    local Masterful = page9:addSection("Unlock Masterful Wrath Element")
    Masterful:addButton("Unlock Masterful Wrath Element", function()
        game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Masterful Wrath")
    end)






    local Shadow = page9:addSection("Unlock Shadow Charge Element")
    Shadow:addButton("Unlock Shadow Charge Element", function()
        game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Shadow Charge")
    end)











    local Shadowfire = page9:addSection("Unlock Shadowfire Element")
    Shadowfire:addButton("Unlock Shadowfire Element", function()
        game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Shadowfire")
    end)









    local Eternity = page9:addSection("Unlock Eternity Storm Element")
    Eternity:addButton("Unlock Eternity Storm Element", function()
        game.ReplicatedStorage.rEvents.elementMasteryEvent:FireServer("Eternity Storm")
    end)












    local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/2NyAaSRtJu")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")







    -- themes
    local themes = {
        Background = Color3.fromRGB(24, 24, 24),
        Glow = Color3.fromRGB(0, 0, 0),
        Accent = Color3.fromRGB(10, 10, 10),
        LightContrast = Color3.fromRGB(20, 20, 20),
        DarkContrast = Color3.fromRGB(14, 14, 14),
        TextColor = Color3.fromRGB(255, 255, 255)
        }
        
            
        -- Theme page
        local settings = venyx:addPage("Settings", 5012544693)
        local colors = settings:addSection("Colors")
        local setting = settings:addSection("Settings")
        
        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
        print("Activated Keybind")
        venyx:toggle()
        end, function()
        print("Changed Keybind")
        end)
        
        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
        colors:addColorPicker(theme, color, function(color3)
        venyx:setTheme(theme, color3)
        end)
        end
    
    
    
    
    
    
    
    
    
    
    
    -- load
        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
        end












































































































        if game.PlaceId == 1224212277 then
            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
            local venyx = library.new("Ez W Hub: Mad City", 5013109572)













            local page3 = venyx:addPage("Main", 5012544693)
            
local Farm = page3:addSection("Farm Xp")
local RANKUP
    Farm:addToggle("Farm Xp", nil, function(bool)
        game:GetService("ReplicatedStorage").RemoteFunction:InvokeServer("SetTeam", "Police")
wait(.75)
game:GetService("RunService").RenderStepped:Connect(function()
for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
   if v.Name == "Handcuffs" then v.Parent = game:GetService("Players").LocalPlayer.Character
   end
end
game:GetService("ReplicatedStorage").Event:FireServer("Eject", game:GetService("Players").LocalPlayer)
end)
		RANKUP = bool
    end)






    local Farm = page3:addSection("Drive on Water")
    local RANKUP
    Farm:addToggle("Drive on Water", nil, function(bool)
        game:GetService("Workspace").ObjectSelection[game.Players.LocalPlayer.Name .. "'s Vehicle"].CarChassis.HoverMode.Value = true
		RANKUP = bool
    end)



    local Farm = page3:addSection("Walk on Water")
    local RANKUP
    Farm:addToggle("Walk on Water", nil, function(bool)
        for k,v in pairs(game:GetService("Workspace").Water:GetChildren()) do
            v.CanCollide = true
            v.Anchored = true
            v.Material = "Ice"
         end
		RANKUP = bool
    end)

            

    local Farm = page3:addSection("Infinite Nitro")
    local RANKUP
    Farm:addToggle("Infinite Nitro", nil, function(bool)
        game:GetService("RunService").RenderStepped:Connect(function()
            if workspace.ObjectSelection:FindFirstChild(game.Players.LocalPlayer.Name.."'s Vehicle") then
            pcall(function()workspace.ObjectSelection[game.Players.LocalPlayer.Name.."'s Vehicle"].CarChassis.Boost.Value = 20;end)
            end
            end)
		RANKUP = bool
    end)



    local Farm = page3:addSection("Crash Server")
    local RANKUP
    Farm:addToggle("Crash Server", nil, function(bool)
        loadstring(game:HttpGet(('https://raw.githubusercontent.com/Cesare0328/my-scripts/main/Mad%20Shitty%20instant%20crash%20server'),true))()
		RANKUP = bool
    end)




    local dfdf = page3:addSection("Rejoin Server")
    
    
    dfdf:addButton("Rejoin", function()
        game:GetService("TeleportService"):Teleport(game.PlaceId)
    end)







            



    local page4 = venyx:addPage("Weapons", 5012544693)
    local Farm = page4:addSection("Inf Ammo")
    local RANKUP
    Farm:addToggle("Inf Ammo", nil, function(bool)
        local function main(v)
            if v.Name == "RifleScript" or v.Name == "ShotgunScript" or v.Name == "PistolScript" or v.Name == "TazerScript" or v.Name == "PowerScript" then
                local a = getsenv(v)
                if debug.getupvalues(a.Reload) then
                    debug.setupvalue(a.Reload, 2, math.huge)
                end
            end
         end
         
         for _, v in pairs(game.Players.LocalPlayer.Backpack:GetDescendants()) do main(v) end
         for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do main(v) end
		RANKUP = bool
    end)








            
            
            
            local page2 = venyx:addPage("Local Player", 5012544693)
            local Farm = page2:addSection("Local Player")
    
            local Farm = page2:addSection("Infinite Jump")
        local RANKUP
        Farm:addToggle("Inf Jump", nil, function(bool)
            game:GetService("UserInputService").JumpRequest:connect(function()
                game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
            end)
            RANKUP = bool
        end)
    
    
    
    
    
        local Farm = page2:addSection("Anti-Afk")
        local RANKUP
        Farm:addToggle("Anti-Afk", nil, function(bool)
            wait(0.5)local ba=Instance.new("ScreenGui")
            local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
            local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
            ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
            ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
            ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
            ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
            ca.TextSize=22;da.Parent=ca
            da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
            da.Size=UDim2.new(0,304,0,107)_b.Parent=da
            _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
            _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
            _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
            ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
            ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
            ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
            game:service'Players'.LocalPlayer.Idled:connect(function()
            bb:CaptureController()bb:ClickButton2(Vector2.new())
            ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
            RANKUP = bool
        end)
    
    
    
        local Farm = page2:addSection("Fly with (E)")
        local RANKUP
        Farm:addToggle("Fly (E)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/7rXZ9VNc", true))()
            RANKUP = bool
        end)
    
    



        local Title = page2:addSection("Reset Character")
    
    
        Title:addButton("Reset", function()
            game.Players.LocalPlayer.Character.Head:Remove()
        end)
    
    



    
    
        local Farm = page2:addSection("Noclip with (R)")
        local RANKUP
        Farm:addToggle("Noclip (R)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()		
            RANKUP = bool
        end)
    
    
    



        local Farm = page2:addSection("God Mode")
        local RANKUP
        Farm:addToggle("God Mode", nil, function(bool)
            loadstring(game:HttpGet(('https://raw.githubusercontent.com/Cesare0328/my-scripts/main/Mad%20City%20GodMode'),true))()
            RANKUP = bool
        end)


    
    
    
        local Farm = page2:addSection("Alt Delete")
        local RANKUP
        Farm:addToggle("Alt Delet", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()		
            RANKUP = bool
        end)
    
    
    
    
        local Farm = page2:addSection("Ctrl Teleport")
        local RANKUP
        Farm:addToggle("Ctrl Teleport", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/gp9y2Wht", true))()	
            RANKUP = bool
        end)
    
    
    
        local Farm = page2:addSection("God Mode")
        local RANKUP
        Farm:addToggle("God Mode", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/MSZAznxp", true))()
            RANKUP = bool
        end)































        local page5 = venyx:addPage("Credits", 5012544693)
        local Discord = page5:addSection("Discord")
        
        
        Discord:addButton("Copy Discord Link", function()
            setclipboard("https://discord.gg/2NyAaSRtJu")
        end)
        local Discord = page5:addSection("Credits")
        local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
        
        
        
        
        
        
        
            -- themes
            local themes = {
                Background = Color3.fromRGB(24, 24, 24),
                Glow = Color3.fromRGB(0, 0, 0),
                Accent = Color3.fromRGB(10, 10, 10),
                LightContrast = Color3.fromRGB(20, 20, 20),
                DarkContrast = Color3.fromRGB(14, 14, 14),
                TextColor = Color3.fromRGB(255, 255, 255)
                }
                
                    
                -- Theme page
                local settings = venyx:addPage("Settings", 5012544693)
                local colors = settings:addSection("Colors")
                local setting = settings:addSection("Settings")
                
                setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                print("Activated Keybind")
                venyx:toggle()
                end, function()
                print("Changed Keybind")
                end)
                
                for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                colors:addColorPicker(theme, color, function(color3)
                venyx:setTheme(theme, color3)
                end)
                end
            
            
            
            
            
            
            
            
            
            
            
            -- load
                venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                end




















































 







               
























































            if game.PlaceId == 3101667897 then
            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
            local venyx = library.new("Ez W Hub: Legend Of Speed", 5013109572)



local page2 = venyx:addPage("AutoFarm", 5012544693)
                    local Farm = page2:addSection("Speed and Level Farm")
local RANKUP
    Farm:addToggle("AutoFarm", nil, function(bool)
        while wait(0.1) do
            local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3)
            end
             
            while wait(0.1) do
            local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3)
            end
             
            while wait(0.1) do
            local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3)
            end
             
            while wait(0.1) do
            local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3)
            end
             
            while wait(0.1) do
            local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Gem" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Yellow Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Orange Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3) local A_1 = "collectOrb" local A_2 = "Blue Orb" local A_3 = "City" local Event = game:GetService("ReplicatedStorage").rEvents.orbEvent Event:FireServer(A_1, A_2, A_3)
            end
		RANKUP = bool
    end)




    Farm:addButton("Auto Orbs And Diemonds", function()
        loadstring(game:HttpGet(('https://raw.githubusercontent.com/goodluck3646/legends-of-speed-mod/main/README.md'),true))()
        end)



        Farm:addButton("Auto Collect Orbs", function()
            getgenv().farm = true

local PlayerRoot = game.Players.LocalPlayer.Character.HumanoidRootPart

while getgenv().farm do -- you don't need ==true in most cases
  wait(0.2) -- always add a wait when using while ... do
  for i,v in pairs(game:GetService("Workspace").orbFolder.City:GetDescendants()) do
      if v.name == "TouchInterest" and v.Parent then
          firetouchinterest(v.Parent, PlayerRoot, 0)
          firetouchinterest(v.Parent, PlayerRoot, 1)
          wait()
      end
  end
end
end)












                    local page2 = venyx:addPage("Esp", 5012544693)
                    
                    local Farm1 = page2:addSection("Player Esp")
                    local RANKUP
                    Farm1:addToggle("Esp", nil, function(bool)
                        local MainParent = game.workspace.Terrain or nil
local LineFrame = Instance.new("ScreenGui",MainParent)
LineFrame.Name = "Lines"
LineFrame.Enabled = false
ToggleKey = Enum.KeyCode.F1
local Spotted = {};
local CharacterMotors = {}
CharacterMotors.GetMotors = function(char)
    local Motors = {}
        for i,v in pairs(char:GetDescendants()) do
            if v:IsA("Motor6D") then
                if v.Part0 and v.Part1 then--and v.Part0.Name ~= "HumanoidRootPart" and v.Part1.Name ~= "HumanoidRootPart" then
                    table.insert(Motors,{v.Part0,v.Part1})
                end
            end
        end
    table.insert(Motors,{char:FindFirstChild("Head") or char.PrimaryPart,"Camera"})
    CharacterMotors[char] = Motors
    return CharacterMotors[char]
end
        
lerp = function(a, b, t)
    return a + (b - a) * t
end
 
local ESP = {Characters = {}}
ESP.Visible = true
ESP.Init = function(char,plr)
    --if (game:GetService("Players").LocalPlayer.Team == nil or plr.Team ~= game:GetService("Players").LocalPlayer.Team) then
        char.DescendantAdded:Connect(function()
            CharacterMotors.GetMotors(char)
        end)
        
        local BillboardUi = Instance.new("BillboardGui")
        BillboardUi.AlwaysOnTop = true
        BillboardUi.Size = UDim2.new(3,60,1,30)
        BillboardUi.StudsOffsetWorldSpace = Vector3.new(0,-4.5,0)
        BillboardUi.Adornee = char:WaitForChild("HumanoidRootPart")
        
        local PlayerName = Instance.new("TextLabel",BillboardUi)
        PlayerName.BackgroundTransparency = 1
        PlayerName.TextColor3 = (game:GetService("Players"):GetPlayerFromCharacter(char)).TeamColor.Color
        PlayerName.Size = UDim2.new(1,0,.3,0)
        PlayerName.ZIndex = 2
        PlayerName.Text = char.Name
        PlayerName.TextScaled = true
        PlayerName.TextStrokeTransparency = .25
        PlayerName.Font = Enum.Font.GothamBold
        PlayerName.TextStrokeColor3 = Color3.fromRGB(33, 33, 33)
        
        local Distance = PlayerName:Clone()
        Distance.Parent = BillboardUi
        Distance.Font = Enum.Font.Gotham
        Distance.TextColor3 = Color3.new(1,1,1)
        Distance.Position = UDim2.new(0,0,.3,0)
        
        local Health = PlayerName:Clone()
        Health.Parent = BillboardUi
        Health.Font = Enum.Font.Gotham
        Health.Position = UDim2.new(0,0,.6,0)
        
        ESP.Characters[char] = {PlayerName,Distance,Health,BillboardUi}
    --end
end
ESP.Render = function()
    
    for i,v in pairs(ESP.Characters) do
        pcall(function()
            local shrink = ((((game.Workspace.CurrentCamera.CFrame.p) - i.HumanoidRootPart.Position).Magnitude)/1500)+1
            v[2].Text = math.floor(((game.Workspace.CurrentCamera.CFrame.p) - i.HumanoidRootPart.Position).Magnitude+.5)
            v[3].Text = math.floor(i.Humanoid.Health).."/"..i.Humanoid.MaxHealth.." - "..math.floor(((i.Humanoid.Health/i.Humanoid.MaxHealth)*100)+.5).."%"
            v[3].TextColor3 = Color3.fromHSV((i.Humanoid.Health/i.Humanoid.MaxHealth) * (80/255),1,1)
            if not Spotted[i] then
                --v[1].TextTransparency = lerp(v[1].TextTransparency,.6,0.05)
            else
                --v[1].TextTransparency = lerp(v[1].TextTransparency,0,0.1)
            end
            v[1].TextColor3 = (game:GetService("Players"):GetPlayerFromCharacter(i)).TeamColor.Color
            --v[1].TextStrokeTransparency = 1-((1-v[1].TextTransparency)/2)
            --v[2].TextTransparency = v[1].TextTransparency
            --v[2].TextStrokeTransparency = v[1].TextStrokeTransparency
            --v[3].TextTransparency = v[1].TextTransparency
            --v[3].TextStrokeTransparency = v[1].TextStrokeTransparency
            v[4].Size = UDim2.new(3,60/shrink,1,30/shrink)
            v[1].Visible = ESP.Visible
            v[2].Visible = ESP.Visible
            v[3].Visible = ESP.Visible
            v[4].Parent = MainParent
            
        end)
    end
    
end
 
local Perspective = {}
Perspective.CalculatePoint = function(position,cam)
    local vector, onScreen = cam:WorldToScreenPoint(position)
    return Vector2.new(vector.X, vector.Y),vector.Z,onScreen
end
 
local Draw = {UsedLines = {}}
Draw.Line = function(a,b,line,width)
    if a and b then 
        local lerp = a:Lerp(b,.5)
        local Magnitude = (a-b).Magnitude
        line.AnchorPoint = Vector2.new(0.5,.5)
        line.Position = UDim2.new(lerp.X/game.Workspace.CurrentCamera.ViewportSize.X,0,(lerp.Y/(game.Workspace.CurrentCamera.ViewportSize.Y-36)),36/2)
        line.Size = UDim2.new(Magnitude/line.Parent.AbsoluteSize.X,0,0,width)
        line.Rotation = math.deg(math.atan2(a.y - b.y, a.x - b.x))
    else
        line:Destroy()
    end
end
 
 
Draw.Character = function(player,lines,cam)
    local Motors = CharacterMotors[player]
    if not Motors then
        Motors = CharacterMotors.GetMotors(player)
    end
 
    for i,v in pairs(Motors) do
        if v[1] and v[2] then
            local FoundLine = nil
            for i,v in pairs(lines:GetChildren()) do
                if Draw.UsedLines[v] == nil then
                    Draw.UsedLines[v] = true
                    FoundLine = v
                    break
                end
            end
            local a2d,az,screen = Perspective.CalculatePoint(v[1].Position,cam)
            local b2d,bz,screen2
            local v2pos = v[2].Position
            Spotted[player] = false
            if v[2] == "Camera" then
                local ray = Ray.new(v[1].Position, (cam.CFrame.p - v[1].Position).unit * (cam.CFrame.p - v[1].Position).Magnitude)
                local part, position = workspace:FindPartOnRayWithIgnoreList(ray, {game:GetService("Players").LocalPlayer.Character,player}, false, true)
                if part then
                    screen = false
                    screen2 = false
                else
                    Spotted[player] = true
                    b2d,bz,screen2 = Vector2.new(cam.ViewportSize.x/2, cam.ViewportSize.y),0,true   
                    screen = true
                end
                v2pos = v[1].Position
            else
                b2d,bz,screen2 = Perspective.CalculatePoint(v[2].Position,cam)  
            end
            if screen and screen2 and (v[1].Position-v2pos).Magnitude <= 5 then
                if not FoundLine then
                    FoundLine = Instance.new("Frame")
                    FoundLine.BackgroundColor3 = Color3.new(1,1,1)
                    FoundLine.BackgroundTransparency = .25
                    FoundLine.BorderSizePixel = 0
                    FoundLine.Parent = lines    
                    Draw.UsedLines[FoundLine] = true
                end
                if screen then
                    Draw.Line(a2d,b2d,FoundLine,1)
                else
                    Draw.Line(b2d,a2d,FoundLine,1)
                end
            elseif FoundLine then
                FoundLine:Destroy()
            end
        end
    end
end
 
Draw.ResetLines = function(lines)
    for i,v in pairs(lines:GetChildren()) do
        if Draw.UsedLines[v] == nil then
            v:Destroy()
        end
    end
    Draw.UsedLines = {}
end
 
local AddPlayer = function(plr)
    coroutine.resume(coroutine.create(function()
        if plr ~= game:GetService("Players").LocalPlayer  then
            if plr.Character then
                ESP.Init(plr.Character,plr)
            end
            plr.CharacterAdded:Connect(function(cha)
                ESP.Init(cha,plr)
            end)
        end
    end))
end
 
for i,v in pairs(game:GetService("Players"):GetChildren()) do
    AddPlayer(v)
end
game:GetService("Players").PlayerAdded:Connect(function(v)
    AddPlayer(v)
end)
game:GetService("UserInputService").InputBegan:connect(function(inputObject)
    if inputObject.KeyCode == ToggleKey then
        ESP.Visible = not ESP.Visible
    end
end)
game:GetService("RunService").RenderStepped:Connect(function()
    ESP.Render()
    for i,v in pairs(game:GetService("Players"):GetChildren()) do
        if v.Character and v ~= game:GetService("Players").LocalPlayer and (game:GetService("Players").LocalPlayer.Team == nil or v.Team ~= game:GetService("Players").LocalPlayer.Team) then
            if v.Character.PrimaryPart and (v.Character.PrimaryPart.Position - game.Workspace.CurrentCamera.CFrame.Position).Magnitude <= 200 then
                Draw.Character(v.Character,LineFrame,game.Workspace.CurrentCamera)
            end
        end
    end
    Draw.ResetLines(LineFrame)
end)

                        RANKUP = bool
                    end)
                
                
                
                
















                    local page2 = venyx:addPage("Local Player", 5012544693)
            local Farm = page2:addSection("Local Player")
    

    
            local Farm = page2:addSection("Infinite Jump")
        local RANKUP
        Farm:addToggle("Inf Jump", nil, function(bool)
            game:GetService("UserInputService").JumpRequest:connect(function()
                game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")      
            end)
            RANKUP = bool
        end)
    
    
    
    
    
        local Farm = page2:addSection("Anti-Afk")
        local RANKUP
        Farm:addToggle("Anti-Afk", nil, function(bool)
            wait(0.5)local ba=Instance.new("ScreenGui")
            local ca=Instance.new("TextLabel")local da=Instance.new("Frame")
            local _b=Instance.new("TextLabel")local ab=Instance.new("TextLabel")ba.Parent=game.CoreGui
            ba.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ca.Parent=ba;ca.Active=true
            ca.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ca.Draggable=true
            ca.Position=UDim2.new(0.698610067,0,0.098096624,0)ca.Size=UDim2.new(0,304,0,52)
            ca.Font=Enum.Font.SourceSansSemibold;ca.Text="Anti Afk Kick Script"ca.TextColor3=Color3.new(0,1,1)
            ca.TextSize=22;da.Parent=ca
            da.BackgroundColor3=Color3.new(0.196078,0.196078,0.196078)da.Position=UDim2.new(0,0,1.0192306,0)
            da.Size=UDim2.new(0,304,0,107)_b.Parent=da
            _b.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)_b.Position=UDim2.new(0,0,0.800455689,0)
            _b.Size=UDim2.new(0,304,0,21)_b.Font=Enum.Font.Arial;_b.Text="Made by: RealLeon#0005"
            _b.TextColor3=Color3.new(1,1,1)_b.TextSize=20;ab.Parent=da
            ab.BackgroundColor3=Color3.new(0.176471,0.176471,0.176471)ab.Position=UDim2.new(0,0,0.158377379,0)
            ab.Size=UDim2.new(0,304,0,44)ab.Font=Enum.Font.ArialBold;ab.Text="Status: Script Started"
            ab.TextColor3=Color3.new(1,1,1)ab.TextSize=20;local bb=game:service'VirtualUser'
            game:service'Players'.LocalPlayer.Idled:connect(function()
            bb:CaptureController()bb:ClickButton2(Vector2.new())
            ab.Text="You went idle and ROBLOX tried to kick you but we reflected it!"wait(2)ab.Text="Script Re-Enabled"end)
            RANKUP = bool
        end)
    
    
    
        local Farm = page2:addSection("Fly with (E)")
        local RANKUP
        Farm:addToggle("Fly (E)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/7rXZ9VNc", true))()
            RANKUP = bool
        end)
    
    



        local Title = page2:addSection("Reset Character")
    
    
        Title:addButton("Reset", function()
            game.Players.LocalPlayer.Character.Head:Remove()
        end)
    
    



    
    
        local Farm = page2:addSection("Noclip with (R)")
        local RANKUP
        Farm:addToggle("Noclip (R)", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/2pwTjwS4", true))()		
            RANKUP = bool
        end)
    



    
    
    
        local Farm = page2:addSection("Alt Delete")
        local RANKUP
        Farm:addToggle("Alt Delet", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/DThr62Cn", true))()		
            RANKUP = bool
        end)
    
    
    
    
        local Farm = page2:addSection("Ctrl Teleport")
        local RANKUP
        Farm:addToggle("Ctrl Teleport", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/gp9y2Wht", true))()	
            RANKUP = bool
        end)
    
    
    
        local Farm = page2:addSection("God Mode")
        local RANKUP
        Farm:addToggle("God Mode", nil, function(bool)
            loadstring(game:HttpGet("https://pastebin.com/raw/MSZAznxp", true))()
            RANKUP = bool
        end)



        local page5 = venyx:addPage("Credits", 5012544693)
        local Discord = page5:addSection("Discord")
        
        
        Discord:addButton("Copy Discord Link", function()
            setclipboard("https://discord.gg/2NyAaSRtJu")
        end)
        local Discord = page5:addSection("Credits")
        local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
        
        
        
        
        
        
        
            -- themes
            local themes = {
                Background = Color3.fromRGB(24, 24, 24),
                Glow = Color3.fromRGB(0, 0, 0),
                Accent = Color3.fromRGB(10, 10, 10),
                LightContrast = Color3.fromRGB(20, 20, 20),
                DarkContrast = Color3.fromRGB(14, 14, 14),
                TextColor = Color3.fromRGB(255, 255, 255)
                }
                
                    
                -- Theme page
                local settings = venyx:addPage("Settings", 5012544693)
                local colors = settings:addSection("Colors")
                local setting = settings:addSection("Settings")
                
                setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                print("Activated Keybind")
                venyx:toggle()
                end, function()
                print("Changed Keybind")
                end)
                
                for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                colors:addColorPicker(theme, color, function(color3)
                venyx:setTheme(theme, color3)
                end)
                end
                
            -- load
                venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                end


































































            if game.PlaceId == 292439477 then
            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
            local venyx = library.new("Ez W Hub: Phantom Forces", 5013109572)



            local page3 = venyx:addPage("Aimbot", 5012544693)
            
            local Farm = page3:addSection("Silent Aim")
            page3:addButton("Silent Aim", function()
                -- Credits to integerisqt!
-- Have a great day!
local Players = game:GetService("Players")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local GameLogic, CharTable, Trajectory
for I,V in pairs(getgc(true)) do
    if type(V) == "table" then
        if rawget(V, "gammo") then
            GameLogic = V
        end
    elseif type(V) == "function" then
        if debug.getinfo(V).name == "getbodyparts" then
            CharTable = debug.getupvalue(V, 1)
        elseif debug.getinfo(V).name == "trajectory" then
            Trajectory = V
        end
    end
    if GameLogic and CharTable and Trajectory then break end
end

local function Closest()
    local Max, Close = math.huge
    for I,V in pairs(Players:GetPlayers()) do
        if V ~= LocalPlayer and V.Team ~= LocalPlayer.Team and CharTable[V] then
            local Pos, OnScreen = Camera:WorldToScreenPoint(CharTable[V].head.Position)
            if OnScreen then
                local Dist = (Vector2.new(Pos.X, Pos.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                if Dist < Max then
                    Max = Dist
                    Close = V
                end
            end
        end
    end
    return Close
end
local MT = getrawmetatable(game)
local __index = MT.__index
setreadonly(MT, false)
MT.__index = newcclosure(function(self, K)
    if not checkcaller() and GameLogic.currentgun and GameLogic.currentgun.data and (self == GameLogic.currentgun.barrel or tostring(self) == "SightMark") and K == "CFrame" then
        local CharChosen = (CharTable[Closest()] and CharTable[Closest()].head)
        if CharChosen then
            local _, Time = Trajectory(self.Position, Vector3.new(0, -workspace.Gravity, 0), CharChosen.Position, GameLogic.currentgun.data.bulletspeed)
            return CFrame.new(self.Position, CharChosen.Position + (Vector3.new(0, -workspace.Gravity / 2, 0)) * (Time ^ 2) + (CharChosen.Velocity * Time))
        end
    end
    return __index(self, K)
end)
setreadonly(MT, true)
                end)





                local page5 = venyx:addPage("Credits", 5012544693)
            local Discord = page5:addSection("Discord")
            
            
            Discord:addButton("Copy Discord Link", function()
                setclipboard("https://discord.gg/JdEK5qN7Yb")
            end)
            local Discord = page5:addSection("Credits")
            local d = page5:addSection("Made by: Leon!#0831")
            local d = page5:addSection("Scripter: Leon!#0831")
        
        
        
        
        
        
        
            -- themes
            local themes = {
                Background = Color3.fromRGB(24, 24, 24),
                Glow = Color3.fromRGB(0, 0, 0),
                Accent = Color3.fromRGB(10, 10, 10),
                LightContrast = Color3.fromRGB(20, 20, 20),
                DarkContrast = Color3.fromRGB(14, 14, 14),
                TextColor = Color3.fromRGB(255, 255, 255)
                }
                
                    
                -- Theme page
                local settings = venyx:addPage("Settings", 5012544693)
                local colors = settings:addSection("Colors")
                local setting = settings:addSection("Settings")
                
                setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                print("Activated Keybind")
                venyx:toggle()
                end, function()
                print("Changed Keybind")
                end)
                
                for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                colors:addColorPicker(theme, color, function(color3)
                venyx:setTheme(theme, color3)
                end)
                end
                
            -- load
                venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                end


                






























                if game.PlaceId == 443406476 then
                    local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                    local venyx = library.new("Vex Hub: Projekt Lazarus", 5013109572)




                 
   
local section1 = venyx:addPage("Main", 8162117119)
                     local section1 = section1:addSection("Main")



                    
                    section1:addButton("One shot Zombies", function()
                        hookfunction(gcinfo, function()
                            return math.random(200,350)
                         end)
                         
                         -- // Constants \\ --
                         -- [ Services ] --
                         local Services = setmetatable({}, {__index = function(Self, Index)
                            local NewService = game:GetService(Index)
                            if NewService then
                                Self[Index] = NewService
                            end
                            return NewService
                         end})
                         
                         -- [ LocalPlayer ] --
                         local LocalPlayer = Services.Players.LocalPlayer
                         
                         -- // Variables \\ --
                         local Connections = {
                            Weapon1 = nil;
                            Weapon2 = nil;
                            Weapon3 = nil;
                            Backpack = nil;
                         }
                         
                         local RoundNumber = workspace.RoundNum
                         
                         -- // Functions \\ --
                         local function CharacterAdded(Character)
                            local Backpack = LocalPlayer:WaitForChild('Backpack')
                         
                            local function ChildAdded(Child)
                                if Child.Name == "Weapon1" or Child.Name == "Weapon2" or Child.Name == "Weapon3" then
                                    local Module = require(Child)
                                    
                                    if Connections[Child.Name] then
                                        Connections[Child.Name]:Disconnect()
                                        Connections[Child.Name] = nil
                                    end
                         
                                    Connections[Child.Name] = Services.RunService.RenderStepped:Connect(function()
                                        Module.Ammo = Module.MagSize + 1
                                        Module.StoredAmmo = Module.MaxAmmo
                                        Module.HeadShot = 150 + (RoundNumber.Value * 150)
                                        Module.TorsoShot = 150 + (RoundNumber.Value * 150)
                                        Module.LimbShot = 150 + (RoundNumber.Value * 150)
                                        Module.BulletPenetration = 10
                                    end)
                                end
                            end
                         
                            if Connections.Backpack then
                                Connections.Backpack:Disconnect()
                                Connections.Backpack = nil
                            end
                         
                            for i,v in ipairs(Backpack:GetChildren()) do
                                ChildAdded(v)
                            end
                            Connections.Backpack = Backpack.ChildAdded:Connect(ChildAdded)
                         end
                         
                         -- // Event Listeners \\ --
                         LocalPlayer.CharacterAdded:Connect(CharacterAdded)
                         CharacterAdded(LocalPlayer.Character)
                         
                         -- // Metatable \\ --
                         local RawMetatable = getrawmetatable(game)
                         local __Namecall = RawMetatable.__namecall
                         
                         setreadonly(RawMetatable, false)
                         
                         RawMetatable.__namecall = newcclosure(function(Object, ...)
                            local NamecallMethod = getnamecallmethod()
                            local Arguments = {...}
                         
                            if typeof(Object) == "Instance" and Object.IsA(Object, "RemoteEvent") then
                                if tostring(Object) == "Damage" and NamecallMethod == "FireServer" then
                                    Arguments[1].Damage = Arguments[1].BodyPart.Parent.Humanoid.MaxHealth + 10
                                end
                            end
                         
                            return __Namecall(Object, unpack(Arguments))
                         end)
                         
                         setreadonly(RawMetatable, true)
                         
                         -- // Actions \\ --
                         --LocalPlayer.Character.Health:Destroy()
                        end)






                    local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/JdEK5qN7Yb")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: Leon!#0831")
                    local d = page5:addSection("Scripter: Leon!#0831")
                
                
                
                
                
                
                
                    -- themes
                    local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                            
                        -- Theme page
                        local settings = venyx:addPage("Settings", 5012544693)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        
                    -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end























































                        if game.PlaceId == 192800 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Vex Hub: Work At A Pizza Place", 5013109572)


    local section1 = venyx:addPage("Farming", 8162117119)
    local section1 = section1:addSection("Farming")



    section1:addButton("Auto Farm", function()
        if game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") then
            for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v.Name:len() == 2 then
                    v.Parent = game.Players.LocalPlayer.Character
                end
            end
            
            wait()
            
            local item = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Name
            
                    for i,v in pairs(game.Workspace.Houses:GetChildren()) do
                        for i,v in pairs(v:GetChildren()) do
                            if v.Name == "Address" then
                                print(v.Value)
                                if v.Value == item then
                                    for i,v in pairs(v.Parent.Upgrades:GetChildren()) do
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Parent.Parent.Upgrades[v.Name].Doors.FrontDoorMain.DoorTouch.CFrame * CFrame.new(-5, 0, 0)
                                        wait(8)
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(64.7216568, 6.63000107, -11.3157063)
                                        wait(1)
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(58.4695549, 6.63000107, -9.41764355)
                                        wait(1)
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(68.068222, 6.63000107, -7.46636343)
                                        wait(1)
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(68.9409561, 6.62999964, -11.2087212)
                                        wait(1)
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(64.0699768, 6.63000107, -11.5208979)
                                        wait(0.5)
                                        wait(1)
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(59.1558762, 6.63000107, -7.64516211)
                                    end
                                end
                            end
                        end
                    end
        else
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(64.7216568, 6.63000107, -11.3157063)
            wait(1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(58.4695549, 6.63000107, -9.41764355)
            wait(1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(68.068222, 6.63000107, -7.46636343)
            wait(1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(68.9409561, 6.62999964, -11.2087212)
            wait(1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(64.0699768, 6.63000107, -11.5208979)
            wait(0.5)
            wait(1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(59.1558762, 6.63000107, -7.64516211)
            
        end
    

        end)




        
            
            



        section1:addButton("Delete all Players", function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/BlastingStone/MyLuaStuff/master/WaaPPEraser.lua"))()
            end)

            







                            local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/JdEK5qN7Yb")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: Leon!#0831")
                    local d = page5:addSection("Scripter: Leon!#0831")
                
                
                
                
                
                
                
                    -- themes
                    local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                            
                        -- Theme page
                        local settings = venyx:addPage("Settings", 5012544693)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        
                    -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end
        

































                        if game.PlaceId == 4520749081 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Vex Hub: King Legacy", 5013109572)
                        
                            local section1 = venyx:addPage("Farming", 8162117119)
                            local section1 = section1:addSection("Farming")











                            local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/JdEK5qN7Yb")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: Leon!#0831 and Zerio#0880")
                    local d = page5:addSection("Scripter: Zerio#0880")
                
                
                
                
                
                
                
                    -- themes
                    local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                            
                        -- Theme page
                        local settings = venyx:addPage("Settings", 5012544693)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        
                    -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end




































                        if game.PlaceId == 2753915549 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Vex Hub: Blox Fruits", 5013109572)
                        
                            local section1 = venyx:addPage("Farming", 8162117119)
                            local section1 = section1:addSection("Farming")















                            local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/JdEK5qN7Yb")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: Leon!#0831 and Zerio#0880")
                    local d = page5:addSection("Scripter: Zerio#0880")
                
                
                
                
                
                
                
                    -- themes
                    local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                            
                        -- Theme page
                        local settings = venyx:addPage("Settings", 5012544693)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        
                    -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end































                        if game.PlaceId == 221718525 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Vex Hub: Ninja Tycoon", 5013109572)
                        
                            local section1 = venyx:addPage("Farming", 817160385817119)
                            local section1 = section1:addSection("Farming")



                            section1:addButton("Auto Click on Convery", function()
                                function getTycoon()
                                    for i,v in pairs(game:GetService("Workspace")["Zednov's Tycoon Kit"].Tycoons:GetChildren()) do
                                        if v.Owner.Value == game:GetService("Players").LocalPlayer then
                                            return v
                                        end
                                    end
                                    return nil
                                end
                                 
                                local tycoon = getTycoon()
                                if tycoon == nil then
                                    repeat wait(0.5) tycoon = getTycoon() until tycoon ~= nil
                                end
                                 
                                repeat wait() until tycoon:FindFirstChild("PurchasedObjects") ~= nil
                                repeat wait() until tycoon.PurchasedObjects:FindFirstChild("Mine") ~= nil
                                 
                                while true do
                                    fireclickdetector(tycoon.PurchasedObjects.Mine.Clicker.ClickDetector)
                                    wait()
                                end
                            end)



                           






                            








                            local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/2NyAaSRtJu")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
                    
                
                
                
                
                
                
                
                    -- themes
                    local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                            
                        -- Theme page
                        local settings = venyx:addPage("Settings", 8087082660)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        
                    -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end
























































                        if game.PlaceId == 6490016198 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Ez W Hub: Slayer Tycoon", 5013109572)




                    local page = venyx:addPage("Farming", 5012544693)
                    local section1 = page:addSection("Farming")

                    section1:addToggle("Auto Mine Wood", nil, function(state)
                        if state then
                            print("Toggle On")
                            shared.Enabled = true

local plr = game.Players.LocalPlayer
local char = plr.Character
local hatchet = plr.Backpack.Hatchet or char.Hatchet


for i,v in pairs(workspace.Map:GetChildren())do
   if v:FindFirstChild("WoodHitPart") and v.Leaves.Transparency == 0 and shared.Enabled then
       repeat wait()
           char.Humanoid:EquipTool(hatchet)
           wait()
           hatchet:Activate()
           char:SetPrimaryPartCFrame(v.WoodHitPart.CFrame)
       until v.Leaves.Transparency == 1
   end
end
                        else
                            print("Toggle Off")
                            shared.Enabled = false

local plr = game.Players.LocalPlayer
local char = plr.Character
local hatchet = plr.Backpack.Hatchet or char.Hatchet


for i,v in pairs(workspace.Map:GetChildren())do
   if v:FindFirstChild("WoodHitPart") and v.Leaves.Transparency == 0 and shared.Enabled then
       repeat wait()
           char.Humanoid:EquipTool(hatchet)
           wait()
           hatchet:Activate()
           char:SetPrimaryPartCFrame(v.WoodHitPart.CFrame)
       until v.Leaves.Transparency == 1
   end
end
                        end
                    end)
                    



                    section1:addToggle("Farm Money", nil, function(state)
                        if state then
                            print("Toggle On")
                            --https://www.roblox.com/games/6490016198/Slayer-Tycoon-v1-1


_G.Toggle = enabled --Change to enabled to enable the money farm, Change to anything to disable.

loadstring(game:HttpGet('https://raw.githubusercontent.com/MonkeyDLuffyx/Scripts/Slayer-Tycoon-(v1.1)/Slayer%20Tycoon%20Money%20Farm.lua', true))()
                    
                        else
                            print("Toggle Off")
                            --https://www.roblox.com/games/6490016198/Slayer-Tycoon-v1-1


_G.Toggle = false --Change to enabled to enable the money farm, Change to anything to disable.

loadstring(game:HttpGet('https://raw.githubusercontent.com/MonkeyDLuffyx/Scripts/Slayer-Tycoon-(v1.1)/Slayer%20Tycoon%20Money%20Farm.lua', true))()
                    
                        end
                    end)
                    

                    
                    
                        
                    
                    local section2 = page:addSection("Stealing")
                    section2:addToggle("Bag Grabber", nil, function(state)
                        if state then
                            print("Toggle On")
                            _G.Toggle = true --Change to true to enable the bag grabber, Change to false to disable.

                            loadstring(game:HttpGet('https://raw.githubusercontent.com/MonkeyDLuffyx/Scripts/Slayer-Tycoon-(v1.1)/Slayer%20Tycoon%20(v1.1)%20Money%20Bag%20Grabber', true))()                            
                        else
                            print("Toggle Off")
                            _G.Toggle = false --Change to true to enable the bag grabber, Change to false to disable.

loadstring(game:HttpGet('https://raw.githubusercontent.com/MonkeyDLuffyx/Scripts/Slayer-Tycoon-(v1.1)/Slayer%20Tycoon%20(v1.1)%20Money%20Bag%20Grabber', true))()
                    
                        end
                    end)
                    
                    
                    section2:addToggle("Auto Steal Money", nil, function(state)
	if state then
        print("Toggle On")
getgenv().toggleison = true; --set this to false if you want to turn it off or true to turn on

while getgenv().toggleison do
   wait(1)
for i,v in pairs(game:GetService("Workspace").TycoonSets.Tycoons:GetDescendants()) do
   if v:IsA("TouchTransmitter") and v.Parent.Name == "Giver" then
      firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 0) 
      firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 1)
   end
end
end
    else
        print("Toggle Off")
        getgenv().toggleison = false; --set this to false if you want to turn it off or true to turn on

while getgenv().toggleison do
   wait(1)
for i,v in pairs(game:GetService("Workspace").TycoonSets.Tycoons:GetDescendants()) do
   if v:IsA("TouchTransmitter") and v.Parent.Name == "Giver" then
      firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 0) 
      firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 1)
   end
end
end

    end
end)

                    
                    

                    local page5 = venyx:addPage("Credits", 5012544693)
                    local Discord = page5:addSection("Discord")
                    
                    
                    Discord:addButton("Copy Discord Link", function()
                        setclipboard("https://discord.gg/2NyAaSRtJu")
                    end)
                    local Discord = page5:addSection("Credits")
                    local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
                    
                
                
                
                
                
                
                
                    -- themes
                    local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                            
                        -- Theme page
                        local settings = venyx:addPage("Settings", 8087082660)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        
                    -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end























































                        if game.PlaceId == 2986677229 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Ez W Hub: Giant Simulator", 5013109572)
                        
                            local section1 = venyx:addPage("Autofarm", 8162117119)

                            local section1 = section1:addSection("Farming")

                            section1:addToggle("Snowmans Autofarm", nil, function(state)
                                if state then
                                    print("Toggle On")
                                    _G.on = true

                                    while _G.on do wait(0.1)
                                        for i,v in pairs(game:GetService("Workspace").NPC:GetDescendants()) do
                                            if v.Name == 'Snowman' then
                                            local root = game.Players.LocalPlayer.Character.HumanoidRootPart
                                            root.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,3)
                                    
                                    game:GetService("ReplicatedStorage").Aero.AeroRemoteServices.GameService.WeaponAttackStart:FireServer()
                                    wait(0.1)
                                    game:GetService("ReplicatedStorage").Aero.AeroRemoteServices.GameService.WeaponAnimComplete:FireServer()
                                            end
                                        end
                                    end
                                else
                                    print("Toggle Off")
                                    _G.on = false

                                    while _G.on do wait(0.1)
                                        for i,v in pairs(game:GetService("Workspace").NPC:GetDescendants()) do
                                            if v.Name == 'Snowman' then
                                            local root = game.Players.LocalPlayer.Character.HumanoidRootPart
                                            root.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,3)
                                    
                                    game:GetService("ReplicatedStorage").Aero.AeroRemoteServices.GameService.WeaponAttackStart:FireServer()
                                    wait(0.1)
                                    game:GetService("ReplicatedStorage").Aero.AeroRemoteServices.GameService.WeaponAnimComplete:FireServer()
                                            end
                                        end
                                    end
                                end
                            end)
                            
                            



                            section1:addButton("XP Farming", function()
                                while wait() do
                                    game:GetService("ReplicatedStorage").Aero.AeroRemoteServices.GameService.WeaponAnimComplete:FireServer()
                                    game:GetService("ReplicatedStorage").Aero.AeroRemoteServices.GameService.WeaponAttackStart:FireServer()
                                    end
                            end)
                            



                            
                            local page5 = venyx:addPage("Credits", 5012544693)
                            local Discord = page5:addSection("Discord")
                            
                            
                            Discord:addButton("Copy Discord Link", function()
                                setclipboard("https://discord.gg/2NyAaSRtJu")
                            end)
                            local Discord = page5:addSection("Credits")
                            local d = page5:addSection("Made by: rblx-scripts.com#0031 and Auick#0163")
                            
                        
                        
                        
                        
                        
                        
                        
                            -- themes
                            local themes = {
                                Background = Color3.fromRGB(24, 24, 24),
                                Glow = Color3.fromRGB(0, 0, 0),
                                Accent = Color3.fromRGB(10, 10, 10),
                                LightContrast = Color3.fromRGB(20, 20, 20),
                                DarkContrast = Color3.fromRGB(14, 14, 14),
                                TextColor = Color3.fromRGB(255, 255, 255)
                                }
                                
                                    
                                -- Theme page
                                local settings = venyx:addPage("Settings", 8087082660)
                                local colors = settings:addSection("Colors")
                                local setting = settings:addSection("Settings")
                                
                                setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                                print("Activated Keybind")
                                venyx:toggle()
                                end, function()
                                print("Changed Keybind")
                                end)
                                
                                for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                                colors:addColorPicker(theme, color, function(color3)
                                venyx:setTheme(theme, color3)
                                end)
                                end
                                
                            -- load
                                venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end
                            













































                        if game.PlaceId == 286090429 then
                            local library = loadstring(game:HttpGet("https://pastebin.com/raw/qwdPKKDN"))()
                            local venyx = library.new("Ez W Hub: Arsenal", 5013109572)
                            
                            local themes = {
                               Background = Color3.fromRGB(24, 24, 24),
                               Glow = Color3.fromRGB(0, 0, 0),
                               Accent = Color3.fromRGB(10, 10, 10),
                               LightContrast = Color3.fromRGB(20, 20, 20),
                               DarkContrast = Color3.fromRGB(14, 14, 14),
                               TextColor = Color3.fromRGB(255, 255, 255)
                            }
                            
                            --Coded by Tyris & Doiv (void)
                            local mouse = game.Players.LocalPlayer:GetMouse()
                            local BodyParts = {'LeftFoot', 'LeftHand', 'LeftLowerArm', 'LeftLowerLeg', 'LeftUpperArm', 'LeftUpperLeg', 'LowerTorso', 'RightFoot', 'RightHand', 'RightLowerArm', 'RightLowerLeg', 'RightUpperLeg', 'RightUpperArm', 'UpperTorso', 'Head'}
                            local invitecode = ""
                            local HAMEWARE_Chatspam = {"Ez W Hub ON TOP!", "OWNING ANY OTHER CHEAT THEN Ez W Hub MAKES YOU AN IDIOT LIBERAL", "Ez W Hub PENCE 2020", "Ez W Hub WINNING", "GET GOOD GET Ez W Hub", "discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode, "HAMEWARE | TWO STUDS AHEAD OF THE GAME"}
                            local Furry_Chatspam = {'UwU Sowwiez! Im using hameware and owning youwww </3', 'OwO hameware is tapping aww of youw fwiends :c', 'e.e you arent using hameware?? Dat makes meh angerye!! >:c', '>.< I am tapping eyes closed with hameware~', ':3 come get hameware! discoard.gg/'..invitecode, 'OvO Ez W Hub is slotted!! C:', 'UvU no challenge for Ez W Hub! </3'}
                            local Swiss_Chatspam = {'SalÃ¼ zÃ¤mme Ig bin en schwiizer.', 'Hei u-huara dreck isch denn da imfall', 'Ier sing alli extrem schlecht i dem spiil lol', 'Wa wennd ier eigentlich, ich bin eh besser also leafet doch???', 'Han kei bock meh gege euch spiele, ier sind alli extrem schlecht', 'Boah alter in zuri hets boes fuetz!', 'Ig schwoer Ez W Hub isch immer ontop!', 'Hameware isch de best script wo nid full-public isch', 'holl der doch Ez W Hub! discord.gg/'..invitecode}
                            local HvH_Chatspam = {"HHHHHH D0g owned by rblx-scripts.com user hhh", "No Ez W Hub no talk dog LLLL", "hhhh imagine not owning Ez W Hub NN dog 2k20 Ez W Hub", "come 5v5 dumb dog", "Absolute dog hhhh no Ez W Hub no talk nn", "I'm hvh legende so shhhh", "hdf eins du hs", 'einsclick hdf hund', 'schnauze nn ich bin hvh legende', 'Hvh legend here', 'Ez W Hub Ez W Hub nr #1 cheat', 'Antiaim top of the game'}
                            local China_Chatspam = {"Ez W Hubä½³", "Ez W Hub¸è¡£", "èæ¬é»å®¢è½¯ä»¶", "äºé©¬é", "æ·éè", "æåæºé»å®¢hameware", "å¤©å®é¨å¹¿åºæ¯åçï¼ä¸é¢æhameware, tianamen square", "ä¹æ²»Â·å¼æ´ä¼å¾·", "ç·äººå¥³äººç«ä¸­å½é¡¶", "å¯æçé»äºº", "æ¯ç²è´´è½¯ä»¶", "xå¼å¾", "æ°´å°ç", "é´èææ¯", "é»è²çæ´»æ æè°BLM", "femboyesæ¯åæ§æ"}
                            local uion = true
                            local circle = Drawing.new("Circle")
                            local LP = game:GetService("Players").LocalPlayer
                            circle.Visible = false
                            local fakeanim = Instance.new('Animation', workspace)
                            fakeanim.AnimationId = 'rbxassetid://0'
                            local userInputService = game:GetService("UserInputService")
                            userInputService.MouseBehavior = Enum.MouseBehavior.Default
                            
                            local target;
                            local bodyname;
                            local ChatDebounce = false
                            local NameTags_Toggled = false
                            local ArmChams = false
                            local WeaponChams = false
                            local ArmMaterial = 'Plastic'
                            local WeaponMaterial = 'Plastic'
                            local debris = game:GetService("Workspace").Debris
                            local SilentAimFOV_Thickness = 1
                            local Show_SILENTAIMFOV = false
                            local CollectDebris = false
                            local SilentAim_Toggled = false
                            local NoAnims_Toggle = false
                            local Teamcheck_Toggled = false
                            local Visuals_Toggled = false
                            local Chams_Toggled = false
                            local SilentAimFOV_Filled = false
                            local AntiAim_Toggle = false
                            local isthirdperson = false
                            local ChatSpam = false
                            local Movement_Toggled = false
                            local Bhop_Toggled = false
                            local Chatspam_Toggled = false
                            local Bhop_Speed = 1
                            local Chatspam_Wait = 1
                            local Chatspam_Type = nil
                            local SilentAim_FOV = 0
                            local SilentAimFOV_Transparency = 0
                            local silentaim_headhitchance = 0
                            local silentaim_bodyhitchance = 0
                            local Pitch_Type = nil
                            local Yaw_Type = nil
                            local AntiAim_Speed = 0
                            local CustomPitch_Value = 0
                            local ArmChams_Color = Color3.new(50, 50, 50)
                            local WeaponChams_Color = Color3.new(50, 50, 50)
                            local SilentAimFOV_Numsides = 3
                            local CustomYaw_Value = 0
                            local leftrotation = CFrame.new(-150, 0, 0)
                            local rightrotation = CFrame.new(150, 0, 0)
                            local backrotation = CFrame.new(-4, 0, 0)
                            local ChamsColor = Color3.fromRGB(50, 50, 50)
                            local SilentAimFOV_Color = Color3.fromRGB(50, 50, 50)
                            local defaultvector = Vector2.new(workspace.CurrentCamera.ViewportSize.X / 2, workspace.CurrentCamera.ViewportSize.Y / 2)
                            local hed = Instance.new('Part', workspace.Terrain)
                            local rhead = Instance.new('Part', hed)
                            local rtors = Instance.new('Part', hed)
                            rhead.Name = "Head"
                            rtors.Name = 'UpperTorso'
                            
                            
                            
                            local page = venyx:addPage("Home", 8162117119)
                            local section1 = page:addSection("Credits")
                            section1:addButton("Made by: rblx-scripts.com#0031 and Auick#0163")
                            section1:addButton("Premium founder: Auick#0163")
                            
                            local section2 = page:addSection("Premium Features")
                            section2:addButton("More Supported Games")
                            section2:addButton("Better Scripts")
                            
                            local section4 = page:addSection("How to get Premium")
                            section4:addButton("Join our discord server go to our website.")
                            section4:addButton("if you want buy it with paypal dm me first.")
                            section4:addButton("My discord name is: rblx-scripts.com#0031")
                            
                            section4:addButton("Copy Website Link to clipboard", function()
                                setclipboard("https://www.ezwhub.xyz/")
                            end)
                            
                            section4:addButton("Copy Discord Link to clipboard", function()
                                setclipboard("https://discord.gg/2NyAaSRtJu")
                            end)
                            local section3 = page:addSection("Support")
                            section3:addButton("Join our discord server for the Support")
                            
                            local page = venyx:addPage("Aimbot", 8419290798)
                            local section1 = page:addSection("Silent Aimbot")
                            local section2 = page:addSection("Silent Aimbot Settings")
                            local addonsectionAIMBOT = page:addSection("Targets")
                            local addonsectionAIMBOTVisuals = page:addSection("Targets")
                            
                            section1:addToggle("Silent Aimbot", nil, function(value)
                               SilentAim_Toggled = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addToggle("Show SilentAim FOV", nil, function(value)
                               Show_SILENTAIMFOV = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addToggle("SilentAim FOV Filled", nil, function(value)
                               SilentAimFOV_Filled = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addSlider("SilentAim FOV Thickness", 1, 1, 5, function(value)
                               SilentAimFOV_Thickness = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addSlider("SilentAim FOV numsides", 3, 3, 100, function(value)
                               SilentAimFOV_Numsides = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addSlider("SilentAim FOV Transparency", 0, 0, 100, function(value)
                               SilentAimFOV_Transparency = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addColorPicker('SilentAim FOV Color', Color3.fromRGB(50, 50, 50), function(color3)
                               SilentAimFOV_Color = color3
                            end)
                            
                            addonsectionAIMBOT:addToggle("TeamCheck", nil, function(value)
                               Teamcheck_Toggled = value
                            end)
                            
                            section2:addSlider("Silent Aimbot FOV", 0, 0, 500, function(value)
                               SilentAim_FOV = value
                            end)
                            
                            section2:addSlider("Head hitchance", 0, 0, 100, function(value)
                               silentaim_headhitchance = value
                            end)
                            
                            section2:addSlider("Body hitchance", 0, 0, 100, function(value)
                               silentaim_bodyhitchance = value
                            end)
                            
                            local Visuals = venyx:addPage("Visuals", 8419618272)
                            local section3 = Visuals:addSection("Chams")
                            local addonsectionVISUALS = Visuals:addSection("Local")
                            
                            section3:addToggle("Visuals", nil, function(value)
                               Visuals_Toggled = value
                            end)
                            
                            section3:addToggle("Nametag Esp", nil, function(value)
                               NameTags_Toggled = value
                            end)
                            
                            section3:addToggle("Chams", nil, function(value)
                               Chams_Toggled = value
                            end)
                            
                            section3:addColorPicker('Chams Color', Color3.fromRGB(50, 50, 50), function(color3)
                               ChamsColor = color3
                            end)
                            
                            
                            addonsectionVISUALS:addKeybind("ThirdPerson keybind", Enum.KeyCode.X, function()
                               if not isthirdperson then
                                   isthirdperson = true
                               else
                                   isthirdperson = false
                               end
                               
                            end, function()
                            end)
                            
                            
                            
                            
                            addonsectionVISUALS:addToggle("Arm Chams", nil, function(value)
                               ArmChams = value
                            end)
                            
                            addonsectionVISUALS:addToggle('Weapon Chams', nil, function(value)
                               WeaponChams = value
                            end)
                            
                            addonsectionVISUALS:addColorPicker('Arm Color', Color3.fromRGB(50, 50, 50), function(color3)
                               ArmChams_Color = color3
                            end)
                            
                            addonsectionVISUALS:addColorPicker('Weapon Color', Color3.fromRGB(50, 50, 50), function(color3)
                               WeaponChams_Color = color3
                            end)
                            
                            addonsectionVISUALS:addDropdown("Arm Material", {"Plastic", "ForceField", "Wood", "Grass"}, function(text)
                               ArmMaterial = text
                            end)
                            
                            addonsectionVISUALS:addDropdown("Weapon Material", {"Plastic", "ForceField", "Wood", "Grass"}, function(text)
                               WeaponMaterial = text
                            end)
                            
                            
                            local AAPage = venyx:addPage("Anti-Aim", 8419589524)
                            local section4 = AAPage:addSection("Main")
                            
                            
                            
                            section4:addToggle("AntiAim Toggle", nil, function(value)
                               AntiAim_Toggle = value
                            end)
                            
                            section4:addToggle("Disable Animations", nil, function(value)
                               NoAnims_Toggle = value
                            end)
                            
                            
                            
                            
                        
                            local page = venyx:addPage("Gun Mods", 8419339309)
                            local section1 = page:addSection("Gun Mods")
                            section1:addToggle("FireRate (With 300 Amo)", nil, function(state)
                                if state then
                                    print("Toggle On")
                                    for i,v in next, game.ReplicatedStorage.Weapons:GetChildren() do
                                        for i,c in next, v:GetChildren() do -- for some reason, using GetDescendants dsent let you modify weapon ammo, so I do this instead
                                        for i,x in next, getconnections(c.Changed) do
                                        x:Disable() -- probably not needed
                                        end
                                        if c.Name == "Ammo" or c.Name == "StoredAmmo" then
                                        c.Value = 300 -- don't set this above 300 or else your guns wont work
                                        elseif c.Name == "AReload" or c.Name == "RecoilControl" or c.Name == "EReload" or c.Name == "SReload" or c.Name == "ReloadTime" or c.Name == "EquipTime" or c.Name == "Spread" or c.Name == "MaxSpread" then
                                        c.Value = 0
                                        elseif c.Name == "Range" then
                                        c.Value = 9e9
                                        elseif c.Name == "Auto" then
                                        c.Value = true
                                        elseif c.Name == "FireRate" or c.Name == "BFireRate" then
                                        c.Value = 0.02 -- don't set this lower than 0.02 or else your game will crash
                                        end
                                        end
                                        end
                                else
                                    print("Toggle Off")
                                    for i,v in next, game.ReplicatedStorage.Weapons:GetChildren() do
                                        for i,c in next, v:GetChildren() do -- for some reason, using GetDescendants dsent let you modify weapon ammo, so I do this instead
                                        for i,x in next, getconnections(c.Changed) do
                                        x:Disable() -- probably not needed
                                        end
                                        if c.Name == "Ammo" or c.Name == "StoredAmmo" then
                                        c.Value = 230 -- don't set this above 300 or else your guns wont work
                                        elseif c.Name == "AReload" or c.Name == "RecoilControl" or c.Name == "EReload" or c.Name == "SReload" or c.Name == "ReloadTime" or c.Name == "EquipTime" or c.Name == "Spread" or c.Name == "MaxSpread" then
                                        c.Value = 0
                                        elseif c.Name == "Range" then
                                        c.Value = 9e9
                                        elseif c.Name == "Auto" then
                                        c.Value = false
                                        elseif c.Name == "FireRate" or c.Name == "BFireRate" then
                                        c.Value = 0.02 -- don't set this lower than 0.02 or else your game will crash
                                        end
                                        end
                                        end
                            
                                end
                            end)
                        
                                
                                section1:addButton("300 Amo (If you need more reset)", function()
                                    for i,v in next, game.ReplicatedStorage.Weapons:GetChildren() do
                                        for i,c in next, v:GetChildren() do -- for some reason, using GetDescendants dsent let you modify weapon ammo, so I do this instead
                                        for i,x in next, getconnections(c.Changed) do
                                        x:Disable() -- probably not needed
                                        end
                                        if c.Name == "Ammo" or c.Name == "StoredAmmo" then
                                        c.Value = 300 -- don't set this above 300 or else your guns wont work
                                        elseif c.Name == "AReload" or c.Name == "RecoilControl" or c.Name == "EReload" or c.Name == "SReload" or c.Name == "ReloadTime" or c.Name == "EquipTime" or c.Name == "Spread" or c.Name == "MaxSpread" then
                                        c.Value = 0
                                        elseif c.Name == "Range" then
                                        c.Value = 9e9
                                        elseif c.Name == "Auto" then
                                        c.Value = false
                                        elseif c.Name == "FireRate" or c.Name == "BFireRate" then
                                        c.Value = 0.02 -- don't set this lower than 0.02 or else your game will crash
                                        end
                                        end
                                        end
                                end)
                        
                        
                            
                            
                            
                            local Misc = venyx:addPage("Misc", 8419593613)
                            local Movement = Misc:addSection("Movement")
                            
                            local MiscLocal = Misc:addSection("Local")
                            
                            MiscLocal:addToggle("Collect Debris", nil, function(value)
                               CollectDebris = value
                            end)
                            
                            Movement:addToggle("Movement Modifiers", nil, function(value)
                               Movement_Toggled = value
                            end)
                            
                            Movement:addToggle("Bhop", nil, function(value)
                               Bhop_Toggled = value
                            end)
                            
                            Movement:addSlider("Bhop Speed", 1, 0, 100, function(value)
                               Bhop_Speed = value
                            end)
                            
                            
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                            
                            local theme = venyx:addPage("Settings", 8087082660)
                            local colors = theme:addSection("Colors")
                            local uitogl = theme:addSection("UI Toggle")
                            
                            uitogl:addKeybind("GUI Toggle Keybind", Enum.KeyCode.Insert, function(val)
                               if uion then
                                   userInputService.MouseBehavior = Enum.MouseBehavior.LockCenter
                                   uion = false
                               else
                                   userInputService.MouseBehavior = Enum.MouseBehavior.Default
                                   uion = true
                               end
                               venyx:toggle()
                            end, function()
                            end)
                            
                            for theme, color in pairs(themes) do
                               colors:addColorPicker(theme, color, function(color3)
                                   venyx:setTheme(theme, color3)
                               end)
                            end
                            
                            venyx:SelectPage(venyx.pages[1], true)
                            
                            local function BulletTracer(ray)
                            
                               local mid = ray.Origin + ray.Direction/2
                            
                               if workspace.Camera:FindFirstChild("Arms") then
                                   if workspace.Camera.Arms:FindFirstChild("Bullet") then
                                       local pr = Instance.new("Part")
                                       pr.Parent = workspace
                                       pr.Anchored = true
                                       pr.CFrame = CFrame.new(mid, ray.Origin)
                                       pr.Size = Vector3.new(BulletTracer_Thickness, BulletTracer_Thickness, ray.Direction.Magnitude)
                                       pr.Color = BulletTracers_Color
                                       pr.Transparency = BulletTracers_Transparency
                                       pr.Material = Enum.Material.Neon
                                       print('Rayd')
                                       wait(3)
                                       pr:Destroy()
                                   end
                               end
                            
                            end
                            
                            
                            local function convert_rgb_to_vertex(c3)
                               return Vector3.new(c3.R, c3.G, c3.B)
                            end
                            local mt = getrawmetatable(game)
                            local oldNamecall = mt.__namecall
                            local oldIndex = mt.__index
                            if setreadonly then
                               setreadonly(mt, false)
                            else
                               make_writeable(mt, true)
                            end
                            local namecallMethod = getnamecallmethod or get_namecall_method
                            local newClose = newcclosure or function(f)
                               return f
                            end
                            mt.__namecall = newClose(function(...)
                               local method = namecallMethod()
                               local args = {...}
                            
                               if method == "FindPartOnRayWithIgnoreList" then
                                   if SilentAim_Toggled then
                                       args[2] = Ray.new(workspace.CurrentCamera.CFrame.Position, (target[bodyname].CFrame.p - workspace.CurrentCamera.CFrame.Position).unit * 500)
                                   end
                               elseif method == 'LoadAnimation' and tostring(args[2]) == 'RunForward' or tostring(args[2]) == 'RunBackward' or
                                   tostring(args[2]) == 'RunLeft' or tostring(args[2]) == 'RunRight' then
                                   if NoAnims_Toggle then
                                       args[2] = fakeanim
                                   end
                               elseif method == 'FireServer' and tostring(args[1]) == "ControlTurn" then
                                   if AntiAim_Toggle then
                                       if Pitch_Type == "Custom" then
                                           args[2] = CustomPitch_Value
                                       elseif Pitch_Type == 'Down' then
                                           args[2] = -1.5
                                       elseif Pitch_Type == "Up" then
                                           args[2] = 1.5
                                       elseif Pitch_Type == "Zero" then
                                           args[2] = 0
                                       end
                                   end
                               end
                            
                               return oldNamecall(unpack(args))
                            end)
                            
                            mt.__index = newcclosure(function(self, ...)
                               local arg = {...}
                            
                               if isthirdperson then
                                   if arg[1] == 'CameraMode' then
                                       return Enum.CameraMode.Classic
                                   end
                               end
                            
                            
                               return oldIndex(self, ...)
                            end)
                            local newmt = mt.__newindex
                            local namecall = mt.__namecall
                            setreadonly(mt,false)
                            newmt = newcclosure(function(self,args,value)
                               if checkcaller() then
                                   return new(self,args,value)
                               end
                               if args:lower() == "walkspeed" or args == "WalkSpeed" then
                                   return
                               end
                               return newmt(self,args,value)
                            end)
                            
                            
                            if setreadonly then
                               setreadonly(mt, true)
                            else
                               make_writeable(mt, false)
                            end
                            
                            function characterrotate(pos)
                               pcall(function()
                                   if game.Players.LocalPlayer.Character then
                                       game.Players.LocalPlayer.Character.Humanoid.AutoRotate = false
                                       local gyro = Instance.new('BodyGyro')
                                       gyro.D = 0
                                       gyro.P = 1000000
                                       gyro.MaxTorque = Vector3.new(0, 1000000, 0)
                                       gyro.Parent = game.Players.LocalPlayer.Character.UpperTorso
                                       gyro.CFrame = CFrame.new(gyro.Parent.Position, pos)
                                       wait()
                                       gyro:Destroy()
                                   end
                               end)
                            end
                            
                            function GetTarget()
                               local fob = SilentAim_FOV
                               local nearestcharacter = nil
                               pcall(function()
                                   local t = nil
                                   local m = LP:GetMouse()
                                   for _, PL in pairs(game.Players:GetPlayers()) do
                                       if PL.Character and PL.Character:FindFirstChild("Head") then
                                           if PL ~= LP then
                                               if Teamcheck_Toggled == false then
                                                   if PL ~= nearestcharacter then
                                                       local vector, onScreen = workspace.CurrentCamera:WorldToScreenPoint(PL.Character.Head.CFrame.p)
                                                       local dist = (Vector2.new(vector.X, vector.Y) - Vector2.new(m.X, m.Y)).Magnitude
                                                       if dist < fob then
                                                           if 0 < PL.Character.Humanoid.Health then
                                                               nearestcharacter = PL.Character
                                                               fob = dist
                                                           end
                                                       end
                                                   end
                                               else
                                                   if PL.TeamColor ~= LP.TeamColor then
                                                       if PL ~= nearestcharacter then
                                                           local vector, onScreen = workspace.CurrentCamera:WorldToScreenPoint(PL.Character.Head.CFrame.p)
                                                           local dist = (Vector2.new(vector.X, vector.Y) - Vector2.new(m.X, m.Y)).Magnitude
                                                           if dist < fob then
                                                               if 0 < PL.Character.Humanoid.Health then
                                                                   nearestcharacter = PL.Character
                                                                   fob = dist
                                                               end
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       end
                                   end
                               end)
                               return nearestcharacter
                            end
                            
                            function isInTable(table, tofind)
                               local found = false
                               for _,v in pairs(table) do
                                   if v==tofind then
                                       found = true
                                       break;
                                   end
                               end
                               return found
                            end
                            
                            TweenStatus = nil
                            
                            local TweenService = game:GetService("TweenService")
                            TweenCFrame = Instance.new("CFrameValue")
                            
                            
                            function tweenstuff(partpos)
                               TweenStatus = true
                               TweenCFrame.Value = workspace.CurrentCamera.CFrame
                               local tweenframe = TweenService:Create(TweenCFrame, TweenInfo.new(0.2),{Value = CFrame.new(workspace.CurrentCamera.CFrame.Position, partpos)})
                               tweenframe:Play()
                               tweenframe.Completed:Wait()
                               TweenStatus = nil
                               TweenCFrame.Value = CFrame.new(0,0,0)
                            end
                            
                            
                            while true do
                            
                            
                               if Movement_Toggled then
                                   
                                   if Bhop_Toggled then
                                       if userInputService:IsKeyDown(Enum.KeyCode.Space) then
                                           if LP.Character then
                                               LP.Character['Humanoid'].Jump = true
                                               LP.Character['Humanoid'].WalkSpeed =  Bhop_Speed
                                           end
                                       end
                                   end
                               end
                            
                            
                               if Visuals_Toggled then
                            
                                   if NameTags_Toggled then
                                       if Teamcheck_Toggled then
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.TeamColor ~= LP.TeamColor then
                                                       if V.Character and V.Character:FindFirstChild("Head") then
                                                           if V.Character.Head:FindFirstChild("TotallyNotNAMEESP") then
                                                               V.Character.Head['TotallyNotNAMEESP'].TextLabel.TextColor3 = ChamsColor
                                                           else
                                                               local bbgui = Instance.new("BillboardGui",  V.Character['Head'])
                                                               bbgui.Name = "TotallyNotNAMEESP"
                                                               bbgui.AlwaysOnTop = true
                                                               bbgui.StudsOffset = Vector3.new(0, 2, 0)
                                                               bbgui.ClipsDescendants = false
                                                               bbgui.Enabled = true
                                                               bbgui.Size = UDim2.new(0, 200,0, 50)
                            
                                                               local boxha = Instance.new('TextLabel', bbgui)
                                                               boxha.Size = UDim2.new(0, 200,0, 50)
                                                               boxha.TextColor3 = ChamsColor
                                                               boxha.Text = V.Name
                                                               boxha.Font = Enum.Font.Code
                                                               boxha.TextSize = 20
                                                               boxha.BackgroundTransparency = 1
                                                               boxha.BorderSizePixel = 0
                                                               boxha.Visible = true
                                                               boxha.Size = UDim2.new(0, 200,0, 50)
                                                               boxha.TextWrapped = true
                                                           end
                                                       end
                                                   elseif V.TeamColor == LP.TeamColor then
                                                       if V.Character and V.Character:FindFirstChild("Head") then
                                                           if V.Character.Head:FindFirstChild("TotallyNotNAMEESP") then
                                                               V.Character.Head['TotallyNotNAMEESP']:Destroy()
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       else
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.Character and V.Character:FindFirstChild("Head") then
                                                       if V.Character.Head:FindFirstChild("TotallyNotNAMEESP") then
                                                           V.Character.Head['TotallyNotNAMEESP'].TextLabel.TextColor3 = ChamsColor
                                                       else
                                                           local bbgui = Instance.new("BillboardGui",  V.Character['Head'])
                                                           bbgui.Name = "TotallyNotNAMEESP"
                                                           bbgui.AlwaysOnTop = true
                                                           bbgui.StudsOffset = Vector3.new(0, 2, 0)
                                                           bbgui.ClipsDescendants = false
                                                           bbgui.Enabled = true
                                                           bbgui.Size = UDim2.new(0, 200,0, 50)
                                                           local boxha = Instance.new('TextLabel', bbgui)
                                                           boxha.Size = UDim2.new(0, 200,0, 50)
                                                           boxha.TextColor3 = ChamsColor
                                                           boxha.Text = V.Name
                                                           boxha.Font = Enum.Font.Code
                                                           boxha.TextSize = 20
                                                           boxha.BackgroundTransparency = 1
                                                           boxha.BorderSizePixel = 0
                                                           boxha.Visible = true
                                                           boxha.Size = UDim2.new(0, 200,0, 50)
                                                           boxha.TextWrapped = true
                                                       end
                                                   end
                                               end
                                           end
                                       end
                                   end
                                   if Chams_Toggled then
                                       if Teamcheck_Toggled then
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.TeamColor ~= LP.TeamColor then
                                                       if V.Character then
                                                           for X,Z in pairs(V.Character:GetChildren()) do
                                                               if Z.ClassName == 'MeshPart' or Z.ClassName == 'Part' and isInTable(BodyParts, Z.Name) then
                                                                   if Z:FindFirstChild("TotallyNotESP") then
                                                                       Z['TotallyNotESP'].Color3 = ChamsColor
                                                                   else
                                                                       if Z.Name == 'Head' then
                                                                           local headha = Instance.new("CylinderHandleAdornment",Z)
                                                                           headha.Adornee = Z
                                                                           headha.Transparency = 0
                                                                           headha.AlwaysOnTop = true
                                                                           headha.Name = "TotallyNotESP"
                                                                           headha.ZIndex = 1
                                                                           headha.Color3 = ChamsColor
                                                                           headha.Height = 1.3
                                                                       else
                                                                           local boxha = Instance.new("BoxHandleAdornment",Z)
                                                                           boxha.Adornee = Z
                                                                           boxha.Transparency = 0
                                                                           boxha.AlwaysOnTop = true
                                                                           boxha.Name = "TotallyNotESP"
                                                                           boxha.Size = Z.Size
                                                                           boxha.ZIndex = 1
                                                                           boxha.Color3 = ChamsColor
                                                                       end
                                                                   end
                                                               end
                                                           end
                                                       end
                                                   elseif V.TeamColor == LP.TeamColor then
                                                       if V.Character then
                                                           for X,Z in pairs(V.Character:GetChildren()) do
                                                               if Z.ClassName == 'MeshPart' or Z.ClassName == 'Part' and isInTable(BodyParts, Z.Name) then
                                                                   if Z:FindFirstChild("TotallyNotESP") then
                                                                       Z['TotallyNotESP']:Destroy()
                                                                   end
                                                               end
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       else
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.Character then
                                                       for X,Z in pairs(V.Character:GetChildren()) do
                                                           if Z.ClassName == 'MeshPart' or Z.ClassName == 'Part' and isInTable(BodyParts, Z.Name) then
                                                               if Z:FindFirstChild("TotallyNotESP") then
                                                                   Z['TotallyNotESP'].Color3 = ChamsColor
                                                               else
                                                                   if Z.Name == 'Head' then
                                                                       local headha = Instance.new("CylinderHandleAdornment",Z)
                                                                       headha.Adornee = Z
                                                                       headha.Transparency = 0
                                                                       headha.AlwaysOnTop = true
                                                                       headha.Name = "TotallyNotESP"
                                                                       headha.ZIndex = 1
                                                                       headha.Color3 = ChamsColor
                                                                       headha.Height = 1.3
                                                                   else
                                                                       local boxha = Instance.new("BoxHandleAdornment",Z)
                                                                       boxha.Adornee = Z
                                                                       boxha.Transparency = 0
                                                                       boxha.AlwaysOnTop = true
                                                                       boxha.Name = "TotallyNotESP"
                                                                       boxha.Size = Z.Size
                                                                       boxha.ZIndex = 1
                                                                       boxha.Color3 = ChamsColor
                                                                   end
                                                               end
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       end
                                   end
                               end
                            
                            
                               if Chatspam_Toggled then
                                   if not ChatDebounce then
                                       spawn(function()
                                           ChatDebounce = true
                                           while ChatDebounce do
                                               if Chatspam_Type == 'Ez W Hub' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(HAMEWARE_Chatspam[math.random(1, #HAMEWARE_Chatspam)], false, false, false, true)
                                               elseif Chatspam_Type == 'Furry' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(Furry_Chatspam[math.random(1, #Furry_Chatspam)], false, false, false, true)
                                               elseif Chatspam_Type == 'Swiss' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(Swiss_Chatspam[math.random(1, #Swiss_Chatspam)], false, false, false, true)
                                               elseif Chatspam_Type == 'HvH' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(HvH_Chatspam[math.random(1, #HvH_Chatspam)], false, false, false, true)
                                                   elseif Chatspam_Type == 'China' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(China_Chatspam[math.random(1, #China_Chatspam)], false, false, false, true)
                                               end
                                               wait(Chatspam_Wait)
                                               if not Chatspam_Toggled then
                                                   ChatDebounce = false
                                                   break
                                               end
                                           end
                                       end)
                                   end
                               end
                            
                               if AntiAim_Toggle then
                                   if Yaw_Type == "Custom" then
                                       characterrotate(CFrame.new(CustomYaw_Value, 0, 0))
                                   elseif Yaw_Type == "Jitter" then
                                       if game.Players.LocalPlayer.Character then
                                           game.Players.LocalPlayer.Character:WaitForChild("Humanoid").AutoRotate = false
                                           local spin = Instance.new('BodyAngularVelocity', game.Players.LocalPlayer.Character:FindFirstChild('HumanoidRootPart'))
                                           spin.AngularVelocity = Vector3.new(0, math.random(-60000, 55000), 0)
                                           spin.MaxTorque = Vector3.new(0, 35000, 0)
                                           wait()
                                           spin:Destroy()
                                       end
                                   elseif Yaw_Type == "Spin" then
                                       if game.Players.LocalPlayer.Character then
                                           game.Players.LocalPlayer.Character:WaitForChild("Humanoid").AutoRotate = false
                                           local spin = Instance.new('BodyAngularVelocity', game.Players.LocalPlayer.Character:FindFirstChild('HumanoidRootPart'))
                                           spin.AngularVelocity = Vector3.new(0, AntiAim_Speed * 100, 0)
                                           spin.MaxTorque = Vector3.new(0, 23000, 0)
                                           wait()
                                           spin:Destroy()
                                       end
                                   elseif Yaw_Type == "Back" then
                                       characterrotate((workspace.CurrentCamera.CFrame * backrotation).p)
                                   end
                               end
                            
                               if isthirdperson then
                                   userInputService.MouseBehavior = Enum.MouseBehavior.LockCenter  
                                   LP.CameraMode = 'Classic'
                                   game.Players.LocalPlayer.CameraMaxZoomDistance = 12
                                   game.Players.LocalPlayer.CameraMinZoomDistance = 12
                               else
                                   LP.CameraMode = 'LockFirstPerson'
                                   game.Players.LocalPlayer.CameraMaxZoomDistance = 0
                                   game.Players.LocalPlayer.CameraMinZoomDistance = 0
                               end
                            
                               if CollectDebris then
                                   for i,v in pairs(debris:GetChildren()) do
                                       if v.Name == "DeadHP" or v.Name == "DeadAmmo" then
                                           v.CFrame = LP.Character.HumanoidRootPart.CFrame * CFrame.new(0,0.2,0)
                                       end
                                   end
                               end
                            
                            
                               if SilentAim_Toggled then
                            
                                   local xd = math.random(0, 100);
                                   if (silentaim_headhitchance or 0) <= xd then
                                       bodyname = 'UpperTorso'
                                   elseif (silentaim_bodyhitchance or 0) >= xd then
                                       bodyname = 'Head'
                                   else
                                       bodyname = 'Head'
                                   end
                                   local yeet = GetTarget()
                                   if yeet then
                                       target = yeet
                                   else
                                       target = hed
                                   end
                            
                                   if Show_SILENTAIMFOV then
                                       circle.Visible = true
                                       circle.Thickness = SilentAimFOV_Thickness
                                       circle.NumSides = SilentAimFOV_Numsides
                                       circle.Radius = SilentAim_FOV
                                       circle.Filled = SilentAimFOV_Filled
                                       circle.Position = defaultvector
                                       circle.Color = SilentAimFOV_Color
                                       circle.Transparency = SilentAimFOV_Transparency / 100
                                   else
                                       circle.Visible = false
                                   end
                            
                               end
                            
                            
                               if ArmChams then
                                   if not workspace.Camera:FindFirstChild("Arms") then
                                       wait()
                                   else
                                       for i,v in pairs(workspace.Camera.Arms:GetDescendants()) do
                                           if v.Name == 'Right Arm' or v.Name == 'Left Arm' then
                                               if v:IsA("BasePart") then
                                                   v.Material = Enum.Material[ArmMaterial]
                                                   v.Color = ArmChams_Color
                                               end
                                           elseif v:IsA("SpecialMesh") then
                                               if v.TextureId == '' then
                                                   v.TextureId = 'rbxassetid://0'
                                                   v.VertexColor = convert_rgb_to_vertex(ArmChams_Color)
                                               end
                                           elseif v.Name == 'L' or v.Name == 'R' then
                                               v:Destroy()
                                           end
                                       end
                                   end
                               end
                            
                               if WeaponChams then
                                   if not workspace.Camera:FindFirstChild("Arms") then
                                       wait()
                                   else
                                       for i,v in pairs(workspace.Camera.Arms:GetDescendants()) do
                                           if v:IsA("MeshPart") then
                                               v.Material = Enum.Material[WeaponMaterial]
                                               v.Color = WeaponChams_Color
                                           end
                                       end
                                   end
                               end
                            
                            
                               game:GetService("RunService").RenderStepped:Wait()
                            
                            end
                        
                        
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        
                        
                        
                        
                        
                        
                        
                        




































                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        if game.PlaceId == 4616652839 then
                        --variables
                        local player = game.Players.LocalPlayer
                        local mission = player.PlayerGui:WaitForChild("Main"):WaitForChild("ingame"):WaitForChild("Missionstory")
                        local menuplace = 4616652839
                        local forestplace = 5447073001
                        local rainplace = 5084678830
                        local trainingplace = 5431071837
                        local akatsukiplace = 5431069982
                        local worldxplace = 5943874201
                        local villageplace = game:GetService("Workspace"):FindFirstChild("rank")
                        local warplace = game:GetService("Workspace"):FindFirstChild("warmode")
                        function toTarget(pos, targetPos, targetCFrame)
                        local tween_s = game:service"TweenService"
                        local info = TweenInfo.new((targetPos - pos).Magnitude/getgenv().speed, Enum.EasingStyle.Linear)
                        local tween, err = pcall(function()
                        local tween = tween_s:Create(game:GetService("Players").LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = targetCFrame * CFrame.fromAxisAngle(Vector3.new(1,0,0), math.rad(90))})
                        tween:Play()
                        end)
                        if not tween then return err end
                        end
                        
                        --UI Lib Loading
                        
                        local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                        local venyx = library.new("Ez W Hub: Shindo Life", 5013109572)
                        
                        local page = venyx:addPage("Home", 8162117119)
                            local section1 = page:addSection("Credits")
                            section1:addButton("Made by: rblx-scripts.com#0031 and Auick#0163")
                            section1:addButton("Premium founder: Auick#0163")
                            
                            local section2 = page:addSection("Premium Features")
                            section2:addButton("More Supported Games")
                            section2:addButton("Better Scripts")
                            
                            local section4 = page:addSection("How to get Premium")
                            section4:addButton("Join our discord server go to our website.")
                            section4:addButton("if you want buy it with paypal dm me first.")
                            section4:addButton("My discord name is: rblx-scripts.com#0031")
                            
                            section4:addButton("Copy Website Link to clipboard", function()
                                setclipboard("https://www.ezwhub.xyz/")
                            end)
                            
                            section4:addButton("Copy Discord Link to clipboard", function()
                                setclipboard("https://discord.gg/2NyAaSRtJu")
                            end)
                            local section3 = page:addSection("Support")
                            section3:addButton("Join our discord server for the Support")
                        
                        
                        
                        
                        -- themes
                        local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                        
                        
                        
                        --Two page
                        local page2 = venyx:addPage("Autofarm", 8171603858)
                        local Farm = page2:addSection("Mission Farm")
                        local Scroll = page2:addSection("Scroll Farm")
                        getgenv().speed = 500
                        
                        
                        local autofarm
                        Farm:addToggle("AutoFarm", nil, function(bool)
                        autofarm = bool
                        end)
                        
                        local gift
                        Farm:addToggle("Farm Gift Box", nil, function(bool)
                        gift = bool
                        end)
                        
                        local RANKUP
                        Farm:addToggle("AutoRank", nil, function(bool)
                        RANKUP = bool
                        end)
                        
                        local jinfarm
                        Scroll:addToggle("Jin Farm", nil, function(bool)
                        jinfarm = bool
                        end)
                        
                        Scroll:addToggle("Scroll Farm", nil, function(bool)
                        scrollfarm = bool
                        end)
                        
                        
                        
                        
                        --Three page
                        local page3 = venyx:addPage("Quests Maker", 8419465385)
                        local d = page3:addSection("Quests Maker")
                        
                        d:addButton("Rush",function()
                        for i = 1,300 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("rushw")
                        wait(.25)
                        end
                        end)
                        
                        d:addButton("Jumps",function()
                        for v = 1,300 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("takemovement2")
                        wait(.25)
                        end
                        end)
                        
                        d:addButton("Chakra Charges",function()
                        for i = 1,500 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("key","c")
                        wait(.1)
                        game.Players.LocalPlayer.Character.combat.update:FireServer("key","cend")
                        wait(.5)
                        end
                        end)
                        
                        d:addButton("Punches",function()
                        for i = 1,999 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("mouse1",true)
                        wait(.3)
                        end
                        end)
                        
                        d:addButton("TP TrainLog",function()
                        local player = game.Players.LocalPlayer
                        toTarget(player.Character.HumanoidRootPart.Position,workspace.npc.logtraining:FindFirstChild("HumanoidRootPart").Position,CFrame.new(game:GetService("Workspace").npc.logtraining:FindFirstChild("HumanoidRootPart").Position))
                        end)
                        
                        game:GetService('RunService').Stepped:connect(function()
                        if autofarm or gift then
                        pcall(function()
                        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                        end)
                        end
                        end)
                        local green = "http://www.roblox.com/asset/?id=5459241648"
                        local red = "http://www.roblox.com/asset/?id=5459241799"
                        local candy = "http://www.roblox.com/asset/?id=6078390771"
                        spawn(function()
                        while wait() do
                        if autofarm then
                        if  player.currentmission.Value == nil then
                            for i,v in pairs(workspace.missiongivers:GetChildren()) do
                                pcall(function()
                                    if player.currentmission.Value == nil and v.Name == "" and v:FindFirstChild("Head") and v.Head:FindFirstChild("givemission").Enabled and v.Head.givemission:FindFirstChild("color").Visible  then
                                        local TALK = v:FindFirstChild("Talk")
                                        local lvl = player.statz.lvl.lvl.Value
                                        if lvl <= 699 then
                                            if player.currentmission.Value == nil  and v.Talk:FindFirstChild("typ").Value == "defeat" and v.Head.givemission.Enabled and v.Head.givemission.color.Visible and v.Head.givemission.color.Image == green then
                                                local getmission = v:FindFirstChild("HumanoidRootPart")
                                                local clienttalk = v:FindFirstChild("CLIENTTALK")
                                                repeat wait(.3)
                                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-8,0)))
                                                    if (player.Character.HumanoidRootPart.Position-v.HumanoidRootPart.Position).Magnitude < 10 then
                                                        clienttalk:FireServer()
                                                        wait(.3)
                                                        clienttalk:FireServer("accept")
                                                    end
                                                until mission.Visible or v:FindFirstChild("Head").givemission.Enabled == false or player.currentmission.Value == "mission" or not autofarm
                                            end
                                        elseif lvl >= 700 then
                                            if player.currentmission.Value == nil and TALK.typ.Value == "defeat" and v.Head.givemission.Enabled and v.Head.givemission.color.Visible and v.Head.givemission.color.Image == green or v.Head.givemission.color.Image == red then
                                                local getmission = v:FindFirstChild("HumanoidRootPart")
                                                local clienttalk = v:FindFirstChild("CLIENTTALK")
                                                repeat wait(.3)
                                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-8,0)))
                                                    if (player.Character.HumanoidRootPart.Position-v.HumanoidRootPart.Position).Magnitude < 10 then
                                                        clienttalk:FireServer()
                                                        wait(.3)
                                                        clienttalk:FireServer("accept")
                                                    end
                                                until mission.Visible or v:FindFirstChild("Head").givemission.Enabled == false or player.currentmission.Value == "mission" or not autofarm
                                            end
                                        end
                                    end
                                end)
                            end
                        else
                            for i,v in pairs(workspace.npc:GetChildren()) do
                                pcall(function()
                                    if v.ClassName == "Model" and v:FindFirstChild("npctype") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 then
                                        repeat wait(.5)
                                            toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-8,0)))
                                            v.Humanoid.Health = 0
                                        until v.Humanoid.Health == 0 or not autofarm or player.currentmission.Value == nil
                                    end
                                end)
                            end
                        end
                        end
                        end
                        end)
                        spawn(function()
                        while wait() do
                        if gift then
                        local spins = player.statz.spins.Value
                        if spins < 500 then
                            for i,v in pairs(workspace.missiongivers:GetChildren()) do
                                pcall(function()
                                    if mission.Visible == false and v.ClassName == "Model" and v:FindFirstChild("Head"):FindFirstChild("givemission").Enabled and v:FindFirstChild("CLIENTTALK") and v:FindFirstChild("Talk") and string.find(v.Talk.talk1.Value, "Happy holidays, here is 1 FREE spin!") and v.Talk:FindFirstChild("typ").Value == "halloweenevent" and v.Head.givemission.color.Image == gift then
                                        repeat wait(.3)
                                            toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-5,0)))
                                            v.CLIENTTALK:FireServer()
                                            wait(.2)
                                            v.CLIENTTALK:FireServer("accept")
                                        until v:FindFirstChild("Head").givemission.Enabled == false or not gift
                                    end
                                end)
                            end
                        else
                            print("max spins reached 500")
                        end
                        end
                        end
                        end)
                        local function SCROLLFARM()
                        for i,v in pairs(game.workspace.GLOBALTIME:GetChildren()) do
                        if v.ClassName == "Model" and v:FindFirstChild("sh") and v.sh.Position.Y > -1000 and v.sh.Position.Y < 2000 then
                        local scrollA = v.sh:FindFirstChild("invoke")
                        print("SCROLL SPAWNED")
                        pcall(function()
                            toTarget(game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position,v.sh.Position,CFrame.new(v.sh.Position))
                        end)
                        scrollA:FireServer(game.Players.LocalPlayer)
                        fireclickdetector(v.sh.ClickDetector)
                        end
                        end
                        end
                        local function SCROLLFARM1()
                        for i,v in pairs(game.workspace:GetChildren()) do
                        if v.ClassName == "Model" and v:FindFirstChild("sh") and v.sh.Position.Y > -1000 and v.sh.Position.Y < 2000 then
                        local scrollA = v.sh:FindFirstChild("invoke")
                        print("SCROLL SPAWNED in workspace")
                        pcall(function()
                            toTarget(game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position,v.sh.Position,CFrame.new(v.sh.Position))
                            scrollA:FireServer(game.Players.LocalPlayer)
                            fireclickdetector(v.sh.ClickDetector)
                        end)
                        end
                        end
                        end
                        
                        spawn(function()
                        while wait() do
                        if scrollfarm then
                        repeat wait()
                            SCROLLFARM()
                            SCROLLFARM1()
                        until not scrollfarm or not war or not war2
                        end
                        end
                        end)
                        
                        game:GetService('RunService').Stepped:connect(function()
                        if war or war2 then
                        pcall(function()
                        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                        end)
                        end
                        end)
                        
                        spawn(function()
                        while wait() do
                        if war or war2 then
                        repeat wait()
                            SCROLLFARM()
                            SCROLLFARM1()
                        until not scrollfarm or not war or not war2
                        end
                        end
                        end)
                        spawn(function()
                        while wait() do
                        if war then
                        pcall(function()
                            refresh:Refresh("War Completed: " .. count)
                            refreshC:Refresh("Round: " .. workspace.warserver.round.Value)
                        end)
                        for i,v in pairs(workspace.npc:GetChildren()) do
                            if workspace.warserver:FindFirstChild("zetsu").Value > 0 and string.find(workspace.warserver.text.Value, "Left") or string.find(workspace.warserver.text.Value, "DEFEAT") and v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and not v:FindFirstChild("megaboss") then
                                wait(.2)
                                pcall(function()
                                    v.Humanoid.Health = 0
                                end)
                            elseif v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and v:FindFirstChild("megaboss") then
                                wait(6)
                                pcall(function()
                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position))
                                    v.Humanoid.Health = 0
                                end)
                            end
                        end
                        if reset then
                            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                                if v.Name == "warserver" and v:FindFirstChild("round").Value > 20 then
                                    wait(5)
                                    player.Character:BreakJoints()
                                    repeat wait()
                                    until v.round.Value == 0
                                    count = count + 1
                                end
                            end
                        end
                        end
                        end
                        end)
                        
                        spawn(function()
                        while wait() do
                        if war2 then
                        refresh:Refresh("War Completed: " .. count)
                        refreshC:Refresh("Round: " .. workspace.warserver.round.Value)
                        for i,v in pairs(workspace.npc:GetChildren()) do
                            if workspace.warserver:FindFirstChild("zetsu").Value > 0 and string.find(workspace.warserver.text.Value, "Left") or string.find(workspace.warserver.text.Value, "DEFEAT") and v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and not v:FindFirstChild("megaboss") then
                                pcall(function()
                                    repeat wait()
                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-12,0)))
                                    wait(.3)
                                    v.Humanoid.Health = 0
                                    until v.Humanoid.Health == 0
                                end)
                            elseif v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and v:FindFirstChild("megaboss") then
                                wait(8)
                                pcall(function()
                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-25,0)))
                                    v.Humanoid.Health = 0
                                end)
                            else
                                wait()
                            end
                        end
                        if reset then
                            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                                if v.Name == "warserver" and v:FindFirstChild("round").Value > 20 then
                                    wait(5)
                                    player.Character:BreakJoints()
                                    repeat wait()
                                    until v.round.Value == 0
                                    count = count + 1
                                end
                            end
                        end
                        end
                        end
                        end)
                        
                        local function JINFARM()
                        for i,v in pairs(game:GetService("Workspace").npc:GetChildren()) do
                        if v.Name == "npc1" then
                        repeat wait()
                            pcall(function()
                                toTarget(game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-25,0)))
                                player.Character.combat.update:FireServer("mouse1", true)
                                wait(.1)
                                v.Humanoid.HealthChanged:Connect(function()
                                    v.Humanoid.Health = 0
                                end)
                            end)
                        until v.Humanoid.Health == 0 or not jinfarm
                        end
                        end
                        end
                        spawn(function()
                        while wait() do
                        if jinfarm then
                        JINFARM()
                        end
                        end
                        end)
                        spawn(function()
                        while wait() do
                        if RANKUP and player.statz.lvl:FindFirstChild("lvl").Value == 1000 then
                        repeat wait()
                            game.Players.LocalPlayer.startevent:FireServer("rankup")
                        until player.statz.lvl:FindFirstChild("lvl").Value == 1 or not RANKUP
                        end
                        end
                        end)
                        
                        --
                        
                        
                        -- Theme page
                        local settings = venyx:addPage("Settings", 8419885246)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        end
                        
                        -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end






















































                        

                        if game.PlaceId == 286090429 then
                            local library = loadstring(game:HttpGet("https://pastebin.com/raw/qwdPKKDN"))()
                            local venyx = library.new("Ez W Hub: Arsenal", 5013109572)
                            
                            local themes = {
                               Background = Color3.fromRGB(24, 24, 24),
                               Glow = Color3.fromRGB(0, 0, 0),
                               Accent = Color3.fromRGB(10, 10, 10),
                               LightContrast = Color3.fromRGB(20, 20, 20),
                               DarkContrast = Color3.fromRGB(14, 14, 14),
                               TextColor = Color3.fromRGB(255, 255, 255)
                            }
                            
                            --Coded by Tyris & Doiv (void)
                            local mouse = game.Players.LocalPlayer:GetMouse()
                            local BodyParts = {'LeftFoot', 'LeftHand', 'LeftLowerArm', 'LeftLowerLeg', 'LeftUpperArm', 'LeftUpperLeg', 'LowerTorso', 'RightFoot', 'RightHand', 'RightLowerArm', 'RightLowerLeg', 'RightUpperLeg', 'RightUpperArm', 'UpperTorso', 'Head'}
                            local invitecode = ""
                            local HAMEWARE_Chatspam = {"Ez W Hub ON TOP!", "OWNING ANY OTHER CHEAT THEN Ez W Hub MAKES YOU AN IDIOT LIBERAL", "Ez W Hub PENCE 2020", "Ez W Hub WINNING", "GET GOOD GET Ez W Hub", "discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode.." discoard.gg/"..invitecode, "HAMEWARE | TWO STUDS AHEAD OF THE GAME"}
                            local Furry_Chatspam = {'UwU Sowwiez! Im using hameware and owning youwww </3', 'OwO hameware is tapping aww of youw fwiends :c', 'e.e you arent using hameware?? Dat makes meh angerye!! >:c', '>.< I am tapping eyes closed with hameware~', ':3 come get hameware! discoard.gg/'..invitecode, 'OvO Ez W Hub is slotted!! C:', 'UvU no challenge for Ez W Hub! </3'}
                            local Swiss_Chatspam = {'SalÃ¼ zÃ¤mme Ig bin en schwiizer.', 'Hei u-huara dreck isch denn da imfall', 'Ier sing alli extrem schlecht i dem spiil lol', 'Wa wennd ier eigentlich, ich bin eh besser also leafet doch???', 'Han kei bock meh gege euch spiele, ier sind alli extrem schlecht', 'Boah alter in zuri hets boes fuetz!', 'Ig schwoer Ez W Hub isch immer ontop!', 'Hameware isch de best script wo nid full-public isch', 'holl der doch Ez W Hub! discord.gg/'..invitecode}
                            local HvH_Chatspam = {"HHHHHH D0g owned by rblx-scripts.com user hhh", "No Ez W Hub no talk dog LLLL", "hhhh imagine not owning Ez W Hub NN dog 2k20 Ez W Hub", "come 5v5 dumb dog", "Absolute dog hhhh no Ez W Hub no talk nn", "I'm hvh legende so shhhh", "hdf eins du hs", 'einsclick hdf hund', 'schnauze nn ich bin hvh legende', 'Hvh legend here', 'Ez W Hub Ez W Hub nr #1 cheat', 'Antiaim top of the game'}
                            local China_Chatspam = {"Ez W Hubä½³", "Ez W Hub¸è¡£", "èæ¬é»å®¢è½¯ä»¶", "äºé©¬é", "æ·éè", "æåæºé»å®¢hameware", "å¤©å®é¨å¹¿åºæ¯åçï¼ä¸é¢æhameware, tianamen square", "ä¹æ²»Â·å¼æ´ä¼å¾·", "ç·äººå¥³äººç«ä¸­å½é¡¶", "å¯æçé»äºº", "æ¯ç²è´´è½¯ä»¶", "xå¼å¾", "æ°´å°ç", "é´èææ¯", "é»è²çæ´»æ æè°BLM", "femboyesæ¯åæ§æ"}
                            local uion = true
                            local circle = Drawing.new("Circle")
                            local LP = game:GetService("Players").LocalPlayer
                            circle.Visible = false
                            local fakeanim = Instance.new('Animation', workspace)
                            fakeanim.AnimationId = 'rbxassetid://0'
                            local userInputService = game:GetService("UserInputService")
                            userInputService.MouseBehavior = Enum.MouseBehavior.Default
                            
                            local target;
                            local bodyname;
                            local ChatDebounce = false
                            local NameTags_Toggled = false
                            local ArmChams = false
                            local WeaponChams = false
                            local ArmMaterial = 'Plastic'
                            local WeaponMaterial = 'Plastic'
                            local debris = game:GetService("Workspace").Debris
                            local SilentAimFOV_Thickness = 1
                            local Show_SILENTAIMFOV = false
                            local CollectDebris = false
                            local SilentAim_Toggled = false
                            local NoAnims_Toggle = false
                            local Teamcheck_Toggled = false
                            local Visuals_Toggled = false
                            local Chams_Toggled = false
                            local SilentAimFOV_Filled = false
                            local AntiAim_Toggle = false
                            local isthirdperson = false
                            local ChatSpam = false
                            local Movement_Toggled = false
                            local Bhop_Toggled = false
                            local Chatspam_Toggled = false
                            local Bhop_Speed = 1
                            local Chatspam_Wait = 1
                            local Chatspam_Type = nil
                            local SilentAim_FOV = 0
                            local SilentAimFOV_Transparency = 0
                            local silentaim_headhitchance = 0
                            local silentaim_bodyhitchance = 0
                            local Pitch_Type = nil
                            local Yaw_Type = nil
                            local AntiAim_Speed = 0
                            local CustomPitch_Value = 0
                            local ArmChams_Color = Color3.new(50, 50, 50)
                            local WeaponChams_Color = Color3.new(50, 50, 50)
                            local SilentAimFOV_Numsides = 3
                            local CustomYaw_Value = 0
                            local leftrotation = CFrame.new(-150, 0, 0)
                            local rightrotation = CFrame.new(150, 0, 0)
                            local backrotation = CFrame.new(-4, 0, 0)
                            local ChamsColor = Color3.fromRGB(50, 50, 50)
                            local SilentAimFOV_Color = Color3.fromRGB(50, 50, 50)
                            local defaultvector = Vector2.new(workspace.CurrentCamera.ViewportSize.X / 2, workspace.CurrentCamera.ViewportSize.Y / 2)
                            local hed = Instance.new('Part', workspace.Terrain)
                            local rhead = Instance.new('Part', hed)
                            local rtors = Instance.new('Part', hed)
                            rhead.Name = "Head"
                            rtors.Name = 'UpperTorso'
                            
                            
                            
                            local page = venyx:addPage("Home", 8162117119)
                            local section1 = page:addSection("Credits")
                            section1:addButton("Made by: rblx-scripts.com#0031 and Auick#0163")
                            section1:addButton("Premium founder: Auick#0163")
                            
                            local section2 = page:addSection("Premium Features")
                            section2:addButton("More Supported Games")
                            section2:addButton("Better Scripts")
                            
                            local section4 = page:addSection("How to get Premium")
                            section4:addButton("Join our discord server go to our website.")
                            section4:addButton("if you want buy it with paypal dm me first.")
                            section4:addButton("My discord name is: rblx-scripts.com#0031")
                            
                            section4:addButton("Copy Website Link to clipboard", function()
                                setclipboard("https://www.ezwhub.xyz/")
                            end)
                            
                            section4:addButton("Copy Discord Link to clipboard", function()
                                setclipboard("https://discord.gg/2NyAaSRtJu")
                            end)
                            local section3 = page:addSection("Support")
                            section3:addButton("Join our discord server for the Support")
                            
                            local page = venyx:addPage("Aimbot", 8419290798)
                            local section1 = page:addSection("Silent Aimbot")
                            local section2 = page:addSection("Silent Aimbot Settings")
                            local addonsectionAIMBOT = page:addSection("Targets")
                            local addonsectionAIMBOTVisuals = page:addSection("Targets")
                            
                            section1:addToggle("Silent Aimbot", nil, function(value)
                               SilentAim_Toggled = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addToggle("Show SilentAim FOV", nil, function(value)
                               Show_SILENTAIMFOV = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addToggle("SilentAim FOV Filled", nil, function(value)
                               SilentAimFOV_Filled = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addSlider("SilentAim FOV Thickness", 1, 1, 5, function(value)
                               SilentAimFOV_Thickness = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addSlider("SilentAim FOV numsides", 3, 3, 100, function(value)
                               SilentAimFOV_Numsides = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addSlider("SilentAim FOV Transparency", 0, 0, 100, function(value)
                               SilentAimFOV_Transparency = value
                            end)
                            
                            addonsectionAIMBOTVisuals:addColorPicker('SilentAim FOV Color', Color3.fromRGB(50, 50, 50), function(color3)
                               SilentAimFOV_Color = color3
                            end)
                            
                            addonsectionAIMBOT:addToggle("TeamCheck", nil, function(value)
                               Teamcheck_Toggled = value
                            end)
                            
                            section2:addSlider("Silent Aimbot FOV", 0, 0, 500, function(value)
                               SilentAim_FOV = value
                            end)
                            
                            section2:addSlider("Head hitchance", 0, 0, 100, function(value)
                               silentaim_headhitchance = value
                            end)
                            
                            section2:addSlider("Body hitchance", 0, 0, 100, function(value)
                               silentaim_bodyhitchance = value
                            end)
                            
                            local Visuals = venyx:addPage("Visuals", 8419618272)
                            local section3 = Visuals:addSection("Chams")
                            local addonsectionVISUALS = Visuals:addSection("Local")
                            
                            section3:addToggle("Visuals", nil, function(value)
                               Visuals_Toggled = value
                            end)
                            
                            section3:addToggle("Nametag Esp", nil, function(value)
                               NameTags_Toggled = value
                            end)
                            
                            section3:addToggle("Chams", nil, function(value)
                               Chams_Toggled = value
                            end)
                            
                            section3:addColorPicker('Chams Color', Color3.fromRGB(50, 50, 50), function(color3)
                               ChamsColor = color3
                            end)
                            
                            
                            addonsectionVISUALS:addKeybind("ThirdPerson keybind", Enum.KeyCode.X, function()
                               if not isthirdperson then
                                   isthirdperson = true
                               else
                                   isthirdperson = false
                               end
                               
                            end, function()
                            end)
                            
                            
                            
                            
                            addonsectionVISUALS:addToggle("Arm Chams", nil, function(value)
                               ArmChams = value
                            end)
                            
                            addonsectionVISUALS:addToggle('Weapon Chams', nil, function(value)
                               WeaponChams = value
                            end)
                            
                            addonsectionVISUALS:addColorPicker('Arm Color', Color3.fromRGB(50, 50, 50), function(color3)
                               ArmChams_Color = color3
                            end)
                            
                            addonsectionVISUALS:addColorPicker('Weapon Color', Color3.fromRGB(50, 50, 50), function(color3)
                               WeaponChams_Color = color3
                            end)
                            
                            addonsectionVISUALS:addDropdown("Arm Material", {"Plastic", "ForceField", "Wood", "Grass"}, function(text)
                               ArmMaterial = text
                            end)
                            
                            addonsectionVISUALS:addDropdown("Weapon Material", {"Plastic", "ForceField", "Wood", "Grass"}, function(text)
                               WeaponMaterial = text
                            end)
                            
                            
                            local AAPage = venyx:addPage("Anti-Aim", 8419589524)
                            local section4 = AAPage:addSection("Main")
                            
                            
                            
                            section4:addToggle("AntiAim Toggle", nil, function(value)
                               AntiAim_Toggle = value
                            end)
                            
                            section4:addToggle("Disable Animations", nil, function(value)
                               NoAnims_Toggle = value
                            end)
                            
                            
                            
                            
                        
                            local page = venyx:addPage("Gun Mods", 8419339309)
                            local section1 = page:addSection("Gun Mods")
                            section1:addToggle("FireRate (With 300 Amo)", nil, function(state)
                                if state then
                                    print("Toggle On")
                                    for i,v in next, game.ReplicatedStorage.Weapons:GetChildren() do
                                        for i,c in next, v:GetChildren() do -- for some reason, using GetDescendants dsent let you modify weapon ammo, so I do this instead
                                        for i,x in next, getconnections(c.Changed) do
                                        x:Disable() -- probably not needed
                                        end
                                        if c.Name == "Ammo" or c.Name == "StoredAmmo" then
                                        c.Value = 300 -- don't set this above 300 or else your guns wont work
                                        elseif c.Name == "AReload" or c.Name == "RecoilControl" or c.Name == "EReload" or c.Name == "SReload" or c.Name == "ReloadTime" or c.Name == "EquipTime" or c.Name == "Spread" or c.Name == "MaxSpread" then
                                        c.Value = 0
                                        elseif c.Name == "Range" then
                                        c.Value = 9e9
                                        elseif c.Name == "Auto" then
                                        c.Value = true
                                        elseif c.Name == "FireRate" or c.Name == "BFireRate" then
                                        c.Value = 0.02 -- don't set this lower than 0.02 or else your game will crash
                                        end
                                        end
                                        end
                                else
                                    print("Toggle Off")
                                    for i,v in next, game.ReplicatedStorage.Weapons:GetChildren() do
                                        for i,c in next, v:GetChildren() do -- for some reason, using GetDescendants dsent let you modify weapon ammo, so I do this instead
                                        for i,x in next, getconnections(c.Changed) do
                                        x:Disable() -- probably not needed
                                        end
                                        if c.Name == "Ammo" or c.Name == "StoredAmmo" then
                                        c.Value = 230 -- don't set this above 300 or else your guns wont work
                                        elseif c.Name == "AReload" or c.Name == "RecoilControl" or c.Name == "EReload" or c.Name == "SReload" or c.Name == "ReloadTime" or c.Name == "EquipTime" or c.Name == "Spread" or c.Name == "MaxSpread" then
                                        c.Value = 0
                                        elseif c.Name == "Range" then
                                        c.Value = 9e9
                                        elseif c.Name == "Auto" then
                                        c.Value = false
                                        elseif c.Name == "FireRate" or c.Name == "BFireRate" then
                                        c.Value = 0.02 -- don't set this lower than 0.02 or else your game will crash
                                        end
                                        end
                                        end
                            
                                end
                            end)
                        
                                
                                section1:addButton("300 Amo (If you need more reset)", function()
                                    for i,v in next, game.ReplicatedStorage.Weapons:GetChildren() do
                                        for i,c in next, v:GetChildren() do -- for some reason, using GetDescendants dsent let you modify weapon ammo, so I do this instead
                                        for i,x in next, getconnections(c.Changed) do
                                        x:Disable() -- probably not needed
                                        end
                                        if c.Name == "Ammo" or c.Name == "StoredAmmo" then
                                        c.Value = 300 -- don't set this above 300 or else your guns wont work
                                        elseif c.Name == "AReload" or c.Name == "RecoilControl" or c.Name == "EReload" or c.Name == "SReload" or c.Name == "ReloadTime" or c.Name == "EquipTime" or c.Name == "Spread" or c.Name == "MaxSpread" then
                                        c.Value = 0
                                        elseif c.Name == "Range" then
                                        c.Value = 9e9
                                        elseif c.Name == "Auto" then
                                        c.Value = false
                                        elseif c.Name == "FireRate" or c.Name == "BFireRate" then
                                        c.Value = 0.02 -- don't set this lower than 0.02 or else your game will crash
                                        end
                                        end
                                        end
                                end)
                        
                        
                            
                            
                            
                            local Misc = venyx:addPage("Misc", 8419593613)
                            local Movement = Misc:addSection("Movement")
                            
                            local MiscLocal = Misc:addSection("Local")
                            
                            MiscLocal:addToggle("Collect Debris", nil, function(value)
                               CollectDebris = value
                            end)
                            
                            Movement:addToggle("Movement Modifiers", nil, function(value)
                               Movement_Toggled = value
                            end)
                            
                            Movement:addToggle("Bhop", nil, function(value)
                               Bhop_Toggled = value
                            end)
                            
                            Movement:addSlider("Bhop Speed", 1, 0, 100, function(value)
                               Bhop_Speed = value
                            end)
                            
                            
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                            
                            local theme = venyx:addPage("Settings", 8087082660)
                            local colors = theme:addSection("Colors")
                            local uitogl = theme:addSection("UI Toggle")
                            
                            uitogl:addKeybind("GUI Toggle Keybind", Enum.KeyCode.Insert, function(val)
                               if uion then
                                   userInputService.MouseBehavior = Enum.MouseBehavior.LockCenter
                                   uion = false
                               else
                                   userInputService.MouseBehavior = Enum.MouseBehavior.Default
                                   uion = true
                               end
                               venyx:toggle()
                            end, function()
                            end)
                            
                            for theme, color in pairs(themes) do
                               colors:addColorPicker(theme, color, function(color3)
                                   venyx:setTheme(theme, color3)
                               end)
                            end
                            
                            venyx:SelectPage(venyx.pages[1], true)
                            
                            local function BulletTracer(ray)
                            
                               local mid = ray.Origin + ray.Direction/2
                            
                               if workspace.Camera:FindFirstChild("Arms") then
                                   if workspace.Camera.Arms:FindFirstChild("Bullet") then
                                       local pr = Instance.new("Part")
                                       pr.Parent = workspace
                                       pr.Anchored = true
                                       pr.CFrame = CFrame.new(mid, ray.Origin)
                                       pr.Size = Vector3.new(BulletTracer_Thickness, BulletTracer_Thickness, ray.Direction.Magnitude)
                                       pr.Color = BulletTracers_Color
                                       pr.Transparency = BulletTracers_Transparency
                                       pr.Material = Enum.Material.Neon
                                       print('Rayd')
                                       wait(3)
                                       pr:Destroy()
                                   end
                               end
                            
                            end
                            
                            
                            local function convert_rgb_to_vertex(c3)
                               return Vector3.new(c3.R, c3.G, c3.B)
                            end
                            local mt = getrawmetatable(game)
                            local oldNamecall = mt.__namecall
                            local oldIndex = mt.__index
                            if setreadonly then
                               setreadonly(mt, false)
                            else
                               make_writeable(mt, true)
                            end
                            local namecallMethod = getnamecallmethod or get_namecall_method
                            local newClose = newcclosure or function(f)
                               return f
                            end
                            mt.__namecall = newClose(function(...)
                               local method = namecallMethod()
                               local args = {...}
                            
                               if method == "FindPartOnRayWithIgnoreList" then
                                   if SilentAim_Toggled then
                                       args[2] = Ray.new(workspace.CurrentCamera.CFrame.Position, (target[bodyname].CFrame.p - workspace.CurrentCamera.CFrame.Position).unit * 500)
                                   end
                               elseif method == 'LoadAnimation' and tostring(args[2]) == 'RunForward' or tostring(args[2]) == 'RunBackward' or
                                   tostring(args[2]) == 'RunLeft' or tostring(args[2]) == 'RunRight' then
                                   if NoAnims_Toggle then
                                       args[2] = fakeanim
                                   end
                               elseif method == 'FireServer' and tostring(args[1]) == "ControlTurn" then
                                   if AntiAim_Toggle then
                                       if Pitch_Type == "Custom" then
                                           args[2] = CustomPitch_Value
                                       elseif Pitch_Type == 'Down' then
                                           args[2] = -1.5
                                       elseif Pitch_Type == "Up" then
                                           args[2] = 1.5
                                       elseif Pitch_Type == "Zero" then
                                           args[2] = 0
                                       end
                                   end
                               end
                            
                               return oldNamecall(unpack(args))
                            end)
                            
                            mt.__index = newcclosure(function(self, ...)
                               local arg = {...}
                            
                               if isthirdperson then
                                   if arg[1] == 'CameraMode' then
                                       return Enum.CameraMode.Classic
                                   end
                               end
                            
                            
                               return oldIndex(self, ...)
                            end)
                            local newmt = mt.__newindex
                            local namecall = mt.__namecall
                            setreadonly(mt,false)
                            newmt = newcclosure(function(self,args,value)
                               if checkcaller() then
                                   return new(self,args,value)
                               end
                               if args:lower() == "walkspeed" or args == "WalkSpeed" then
                                   return
                               end
                               return newmt(self,args,value)
                            end)
                            
                            
                            if setreadonly then
                               setreadonly(mt, true)
                            else
                               make_writeable(mt, false)
                            end
                            
                            function characterrotate(pos)
                               pcall(function()
                                   if game.Players.LocalPlayer.Character then
                                       game.Players.LocalPlayer.Character.Humanoid.AutoRotate = false
                                       local gyro = Instance.new('BodyGyro')
                                       gyro.D = 0
                                       gyro.P = 1000000
                                       gyro.MaxTorque = Vector3.new(0, 1000000, 0)
                                       gyro.Parent = game.Players.LocalPlayer.Character.UpperTorso
                                       gyro.CFrame = CFrame.new(gyro.Parent.Position, pos)
                                       wait()
                                       gyro:Destroy()
                                   end
                               end)
                            end
                            
                            function GetTarget()
                               local fob = SilentAim_FOV
                               local nearestcharacter = nil
                               pcall(function()
                                   local t = nil
                                   local m = LP:GetMouse()
                                   for _, PL in pairs(game.Players:GetPlayers()) do
                                       if PL.Character and PL.Character:FindFirstChild("Head") then
                                           if PL ~= LP then
                                               if Teamcheck_Toggled == false then
                                                   if PL ~= nearestcharacter then
                                                       local vector, onScreen = workspace.CurrentCamera:WorldToScreenPoint(PL.Character.Head.CFrame.p)
                                                       local dist = (Vector2.new(vector.X, vector.Y) - Vector2.new(m.X, m.Y)).Magnitude
                                                       if dist < fob then
                                                           if 0 < PL.Character.Humanoid.Health then
                                                               nearestcharacter = PL.Character
                                                               fob = dist
                                                           end
                                                       end
                                                   end
                                               else
                                                   if PL.TeamColor ~= LP.TeamColor then
                                                       if PL ~= nearestcharacter then
                                                           local vector, onScreen = workspace.CurrentCamera:WorldToScreenPoint(PL.Character.Head.CFrame.p)
                                                           local dist = (Vector2.new(vector.X, vector.Y) - Vector2.new(m.X, m.Y)).Magnitude
                                                           if dist < fob then
                                                               if 0 < PL.Character.Humanoid.Health then
                                                                   nearestcharacter = PL.Character
                                                                   fob = dist
                                                               end
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       end
                                   end
                               end)
                               return nearestcharacter
                            end
                            
                            function isInTable(table, tofind)
                               local found = false
                               for _,v in pairs(table) do
                                   if v==tofind then
                                       found = true
                                       break;
                                   end
                               end
                               return found
                            end
                            
                            TweenStatus = nil
                            
                            local TweenService = game:GetService("TweenService")
                            TweenCFrame = Instance.new("CFrameValue")
                            
                            
                            function tweenstuff(partpos)
                               TweenStatus = true
                               TweenCFrame.Value = workspace.CurrentCamera.CFrame
                               local tweenframe = TweenService:Create(TweenCFrame, TweenInfo.new(0.2),{Value = CFrame.new(workspace.CurrentCamera.CFrame.Position, partpos)})
                               tweenframe:Play()
                               tweenframe.Completed:Wait()
                               TweenStatus = nil
                               TweenCFrame.Value = CFrame.new(0,0,0)
                            end
                            
                            
                            while true do
                            
                            
                               if Movement_Toggled then
                                   
                                   if Bhop_Toggled then
                                       if userInputService:IsKeyDown(Enum.KeyCode.Space) then
                                           if LP.Character then
                                               LP.Character['Humanoid'].Jump = true
                                               LP.Character['Humanoid'].WalkSpeed =  Bhop_Speed
                                           end
                                       end
                                   end
                               end
                            
                            
                               if Visuals_Toggled then
                            
                                   if NameTags_Toggled then
                                       if Teamcheck_Toggled then
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.TeamColor ~= LP.TeamColor then
                                                       if V.Character and V.Character:FindFirstChild("Head") then
                                                           if V.Character.Head:FindFirstChild("TotallyNotNAMEESP") then
                                                               V.Character.Head['TotallyNotNAMEESP'].TextLabel.TextColor3 = ChamsColor
                                                           else
                                                               local bbgui = Instance.new("BillboardGui",  V.Character['Head'])
                                                               bbgui.Name = "TotallyNotNAMEESP"
                                                               bbgui.AlwaysOnTop = true
                                                               bbgui.StudsOffset = Vector3.new(0, 2, 0)
                                                               bbgui.ClipsDescendants = false
                                                               bbgui.Enabled = true
                                                               bbgui.Size = UDim2.new(0, 200,0, 50)
                            
                                                               local boxha = Instance.new('TextLabel', bbgui)
                                                               boxha.Size = UDim2.new(0, 200,0, 50)
                                                               boxha.TextColor3 = ChamsColor
                                                               boxha.Text = V.Name
                                                               boxha.Font = Enum.Font.Code
                                                               boxha.TextSize = 20
                                                               boxha.BackgroundTransparency = 1
                                                               boxha.BorderSizePixel = 0
                                                               boxha.Visible = true
                                                               boxha.Size = UDim2.new(0, 200,0, 50)
                                                               boxha.TextWrapped = true
                                                           end
                                                       end
                                                   elseif V.TeamColor == LP.TeamColor then
                                                       if V.Character and V.Character:FindFirstChild("Head") then
                                                           if V.Character.Head:FindFirstChild("TotallyNotNAMEESP") then
                                                               V.Character.Head['TotallyNotNAMEESP']:Destroy()
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       else
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.Character and V.Character:FindFirstChild("Head") then
                                                       if V.Character.Head:FindFirstChild("TotallyNotNAMEESP") then
                                                           V.Character.Head['TotallyNotNAMEESP'].TextLabel.TextColor3 = ChamsColor
                                                       else
                                                           local bbgui = Instance.new("BillboardGui",  V.Character['Head'])
                                                           bbgui.Name = "TotallyNotNAMEESP"
                                                           bbgui.AlwaysOnTop = true
                                                           bbgui.StudsOffset = Vector3.new(0, 2, 0)
                                                           bbgui.ClipsDescendants = false
                                                           bbgui.Enabled = true
                                                           bbgui.Size = UDim2.new(0, 200,0, 50)
                                                           local boxha = Instance.new('TextLabel', bbgui)
                                                           boxha.Size = UDim2.new(0, 200,0, 50)
                                                           boxha.TextColor3 = ChamsColor
                                                           boxha.Text = V.Name
                                                           boxha.Font = Enum.Font.Code
                                                           boxha.TextSize = 20
                                                           boxha.BackgroundTransparency = 1
                                                           boxha.BorderSizePixel = 0
                                                           boxha.Visible = true
                                                           boxha.Size = UDim2.new(0, 200,0, 50)
                                                           boxha.TextWrapped = true
                                                       end
                                                   end
                                               end
                                           end
                                       end
                                   end
                                   if Chams_Toggled then
                                       if Teamcheck_Toggled then
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.TeamColor ~= LP.TeamColor then
                                                       if V.Character then
                                                           for X,Z in pairs(V.Character:GetChildren()) do
                                                               if Z.ClassName == 'MeshPart' or Z.ClassName == 'Part' and isInTable(BodyParts, Z.Name) then
                                                                   if Z:FindFirstChild("TotallyNotESP") then
                                                                       Z['TotallyNotESP'].Color3 = ChamsColor
                                                                   else
                                                                       if Z.Name == 'Head' then
                                                                           local headha = Instance.new("CylinderHandleAdornment",Z)
                                                                           headha.Adornee = Z
                                                                           headha.Transparency = 0
                                                                           headha.AlwaysOnTop = true
                                                                           headha.Name = "TotallyNotESP"
                                                                           headha.ZIndex = 1
                                                                           headha.Color3 = ChamsColor
                                                                           headha.Height = 1.3
                                                                       else
                                                                           local boxha = Instance.new("BoxHandleAdornment",Z)
                                                                           boxha.Adornee = Z
                                                                           boxha.Transparency = 0
                                                                           boxha.AlwaysOnTop = true
                                                                           boxha.Name = "TotallyNotESP"
                                                                           boxha.Size = Z.Size
                                                                           boxha.ZIndex = 1
                                                                           boxha.Color3 = ChamsColor
                                                                       end
                                                                   end
                                                               end
                                                           end
                                                       end
                                                   elseif V.TeamColor == LP.TeamColor then
                                                       if V.Character then
                                                           for X,Z in pairs(V.Character:GetChildren()) do
                                                               if Z.ClassName == 'MeshPart' or Z.ClassName == 'Part' and isInTable(BodyParts, Z.Name) then
                                                                   if Z:FindFirstChild("TotallyNotESP") then
                                                                       Z['TotallyNotESP']:Destroy()
                                                                   end
                                                               end
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       else
                                           for I,V in pairs (game.Players:GetPlayers()) do
                                               if V ~= LP then
                                                   if V.Character then
                                                       for X,Z in pairs(V.Character:GetChildren()) do
                                                           if Z.ClassName == 'MeshPart' or Z.ClassName == 'Part' and isInTable(BodyParts, Z.Name) then
                                                               if Z:FindFirstChild("TotallyNotESP") then
                                                                   Z['TotallyNotESP'].Color3 = ChamsColor
                                                               else
                                                                   if Z.Name == 'Head' then
                                                                       local headha = Instance.new("CylinderHandleAdornment",Z)
                                                                       headha.Adornee = Z
                                                                       headha.Transparency = 0
                                                                       headha.AlwaysOnTop = true
                                                                       headha.Name = "TotallyNotESP"
                                                                       headha.ZIndex = 1
                                                                       headha.Color3 = ChamsColor
                                                                       headha.Height = 1.3
                                                                   else
                                                                       local boxha = Instance.new("BoxHandleAdornment",Z)
                                                                       boxha.Adornee = Z
                                                                       boxha.Transparency = 0
                                                                       boxha.AlwaysOnTop = true
                                                                       boxha.Name = "TotallyNotESP"
                                                                       boxha.Size = Z.Size
                                                                       boxha.ZIndex = 1
                                                                       boxha.Color3 = ChamsColor
                                                                   end
                                                               end
                                                           end
                                                       end
                                                   end
                                               end
                                           end
                                       end
                                   end
                               end
                            
                            
                               if Chatspam_Toggled then
                                   if not ChatDebounce then
                                       spawn(function()
                                           ChatDebounce = true
                                           while ChatDebounce do
                                               if Chatspam_Type == 'Ez W Hub' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(HAMEWARE_Chatspam[math.random(1, #HAMEWARE_Chatspam)], false, false, false, true)
                                               elseif Chatspam_Type == 'Furry' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(Furry_Chatspam[math.random(1, #Furry_Chatspam)], false, false, false, true)
                                               elseif Chatspam_Type == 'Swiss' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(Swiss_Chatspam[math.random(1, #Swiss_Chatspam)], false, false, false, true)
                                               elseif Chatspam_Type == 'HvH' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(HvH_Chatspam[math.random(1, #HvH_Chatspam)], false, false, false, true)
                                                   elseif Chatspam_Type == 'China' then
                                                   game.ReplicatedStorage.Events.PlayerChatted:FireServer(China_Chatspam[math.random(1, #China_Chatspam)], false, false, false, true)
                                               end
                                               wait(Chatspam_Wait)
                                               if not Chatspam_Toggled then
                                                   ChatDebounce = false
                                                   break
                                               end
                                           end
                                       end)
                                   end
                               end
                            
                               if AntiAim_Toggle then
                                   if Yaw_Type == "Custom" then
                                       characterrotate(CFrame.new(CustomYaw_Value, 0, 0))
                                   elseif Yaw_Type == "Jitter" then
                                       if game.Players.LocalPlayer.Character then
                                           game.Players.LocalPlayer.Character:WaitForChild("Humanoid").AutoRotate = false
                                           local spin = Instance.new('BodyAngularVelocity', game.Players.LocalPlayer.Character:FindFirstChild('HumanoidRootPart'))
                                           spin.AngularVelocity = Vector3.new(0, math.random(-60000, 55000), 0)
                                           spin.MaxTorque = Vector3.new(0, 35000, 0)
                                           wait()
                                           spin:Destroy()
                                       end
                                   elseif Yaw_Type == "Spin" then
                                       if game.Players.LocalPlayer.Character then
                                           game.Players.LocalPlayer.Character:WaitForChild("Humanoid").AutoRotate = false
                                           local spin = Instance.new('BodyAngularVelocity', game.Players.LocalPlayer.Character:FindFirstChild('HumanoidRootPart'))
                                           spin.AngularVelocity = Vector3.new(0, AntiAim_Speed * 100, 0)
                                           spin.MaxTorque = Vector3.new(0, 23000, 0)
                                           wait()
                                           spin:Destroy()
                                       end
                                   elseif Yaw_Type == "Back" then
                                       characterrotate((workspace.CurrentCamera.CFrame * backrotation).p)
                                   end
                               end
                            
                               if isthirdperson then
                                   userInputService.MouseBehavior = Enum.MouseBehavior.LockCenter  
                                   LP.CameraMode = 'Classic'
                                   game.Players.LocalPlayer.CameraMaxZoomDistance = 12
                                   game.Players.LocalPlayer.CameraMinZoomDistance = 12
                               else
                                   LP.CameraMode = 'LockFirstPerson'
                                   game.Players.LocalPlayer.CameraMaxZoomDistance = 0
                                   game.Players.LocalPlayer.CameraMinZoomDistance = 0
                               end
                            
                               if CollectDebris then
                                   for i,v in pairs(debris:GetChildren()) do
                                       if v.Name == "DeadHP" or v.Name == "DeadAmmo" then
                                           v.CFrame = LP.Character.HumanoidRootPart.CFrame * CFrame.new(0,0.2,0)
                                       end
                                   end
                               end
                            
                            
                               if SilentAim_Toggled then
                            
                                   local xd = math.random(0, 100);
                                   if (silentaim_headhitchance or 0) <= xd then
                                       bodyname = 'UpperTorso'
                                   elseif (silentaim_bodyhitchance or 0) >= xd then
                                       bodyname = 'Head'
                                   else
                                       bodyname = 'Head'
                                   end
                                   local yeet = GetTarget()
                                   if yeet then
                                       target = yeet
                                   else
                                       target = hed
                                   end
                            
                                   if Show_SILENTAIMFOV then
                                       circle.Visible = true
                                       circle.Thickness = SilentAimFOV_Thickness
                                       circle.NumSides = SilentAimFOV_Numsides
                                       circle.Radius = SilentAim_FOV
                                       circle.Filled = SilentAimFOV_Filled
                                       circle.Position = defaultvector
                                       circle.Color = SilentAimFOV_Color
                                       circle.Transparency = SilentAimFOV_Transparency / 100
                                   else
                                       circle.Visible = false
                                   end
                            
                               end
                            
                            
                               if ArmChams then
                                   if not workspace.Camera:FindFirstChild("Arms") then
                                       wait()
                                   else
                                       for i,v in pairs(workspace.Camera.Arms:GetDescendants()) do
                                           if v.Name == 'Right Arm' or v.Name == 'Left Arm' then
                                               if v:IsA("BasePart") then
                                                   v.Material = Enum.Material[ArmMaterial]
                                                   v.Color = ArmChams_Color
                                               end
                                           elseif v:IsA("SpecialMesh") then
                                               if v.TextureId == '' then
                                                   v.TextureId = 'rbxassetid://0'
                                                   v.VertexColor = convert_rgb_to_vertex(ArmChams_Color)
                                               end
                                           elseif v.Name == 'L' or v.Name == 'R' then
                                               v:Destroy()
                                           end
                                       end
                                   end
                               end
                            
                               if WeaponChams then
                                   if not workspace.Camera:FindFirstChild("Arms") then
                                       wait()
                                   else
                                       for i,v in pairs(workspace.Camera.Arms:GetDescendants()) do
                                           if v:IsA("MeshPart") then
                                               v.Material = Enum.Material[WeaponMaterial]
                                               v.Color = WeaponChams_Color
                                           end
                                       end
                                   end
                               end
                            
                            
                               game:GetService("RunService").RenderStepped:Wait()
                            
                            end
                        
                        
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        
                        




































                        
                        
                        
                        
                        
                        if game.PlaceId == 4616652839 then
                        --variables
                        local player = game.Players.LocalPlayer
                        local mission = player.PlayerGui:WaitForChild("Main"):WaitForChild("ingame"):WaitForChild("Missionstory")
                        local menuplace = 4616652839
                        local forestplace = 5447073001
                        local rainplace = 5084678830
                        local trainingplace = 5431071837
                        local akatsukiplace = 5431069982
                        local worldxplace = 5943874201
                        local villageplace = game:GetService("Workspace"):FindFirstChild("rank")
                        local warplace = game:GetService("Workspace"):FindFirstChild("warmode")
                        function toTarget(pos, targetPos, targetCFrame)
                        local tween_s = game:service"TweenService"
                        local info = TweenInfo.new((targetPos - pos).Magnitude/getgenv().speed, Enum.EasingStyle.Linear)
                        local tween, err = pcall(function()
                        local tween = tween_s:Create(game:GetService("Players").LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = targetCFrame * CFrame.fromAxisAngle(Vector3.new(1,0,0), math.rad(90))})
                        tween:Play()
                        end)
                        if not tween then return err end
                        end
                        
                        --UI Lib Loading
                        
                        local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                        local venyx = library.new("Ez W Hub: Shindo Life", 5013109572)
                        
                        local page = venyx:addPage("Home", 8162117119)
                            local section1 = page:addSection("Credits")
                            section1:addButton("Made by: rblx-scripts.com#0031 and Auick#0163")
                            section1:addButton("Premium founder: Auick#0163")
                            
                            local section2 = page:addSection("Premium Features")
                            section2:addButton("More Supported Games")
                            section2:addButton("Better Scripts")
                            
                            local section4 = page:addSection("How to get Premium")
                            section4:addButton("Join our discord server go to our website.")
                            section4:addButton("if you want buy it with paypal dm me first.")
                            section4:addButton("My discord name is: rblx-scripts.com#0031")
                            
                            section4:addButton("Copy Website Link to clipboard", function()
                                setclipboard("https://www.ezwhub.xyz/")
                            end)
                            
                            section4:addButton("Copy Discord Link to clipboard", function()
                                setclipboard("https://discord.gg/2NyAaSRtJu")
                            end)
                            local section3 = page:addSection("Support")
                            section3:addButton("Join our discord server for the Support")
                        
                        
                        
                        
                        -- themes
                        local themes = {
                        Background = Color3.fromRGB(24, 24, 24),
                        Glow = Color3.fromRGB(0, 0, 0),
                        Accent = Color3.fromRGB(10, 10, 10),
                        LightContrast = Color3.fromRGB(20, 20, 20),
                        DarkContrast = Color3.fromRGB(14, 14, 14),
                        TextColor = Color3.fromRGB(255, 255, 255)
                        }
                        
                        
                        
                        
                        --Two page
                        local page2 = venyx:addPage("Autofarm", 8171603858)
                        local Farm = page2:addSection("Mission Farm")
                        local Scroll = page2:addSection("Scroll Farm")
                        getgenv().speed = 500
                        
                        
                        local autofarm
                        Farm:addToggle("AutoFarm", nil, function(bool)
                        autofarm = bool
                        end)
                        
                        local gift
                        Farm:addToggle("Farm Gift Box", nil, function(bool)
                        gift = bool
                        end)
                        
                        local RANKUP
                        Farm:addToggle("AutoRank", nil, function(bool)
                        RANKUP = bool
                        end)
                        
                        local jinfarm
                        Scroll:addToggle("Jin Farm", nil, function(bool)
                        jinfarm = bool
                        end)
                        
                        Scroll:addToggle("Scroll Farm", nil, function(bool)
                        scrollfarm = bool
                        end)
                        
                        
                        
                        
                        --Three page
                        local page3 = venyx:addPage("Quests Maker", 8419465385)
                        local d = page3:addSection("Quests Maker")
                        
                        d:addButton("Rush",function()
                        for i = 1,300 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("rushw")
                        wait(.25)
                        end
                        end)
                        
                        d:addButton("Jumps",function()
                        for v = 1,300 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("takemovement2")
                        wait(.25)
                        end
                        end)
                        
                        d:addButton("Chakra Charges",function()
                        for i = 1,500 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("key","c")
                        wait(.1)
                        game.Players.LocalPlayer.Character.combat.update:FireServer("key","cend")
                        wait(.5)
                        end
                        end)
                        
                        d:addButton("Punches",function()
                        for i = 1,999 do
                        game.Players.LocalPlayer.Character.combat.update:FireServer("mouse1",true)
                        wait(.3)
                        end
                        end)
                        
                        d:addButton("TP TrainLog",function()
                        local player = game.Players.LocalPlayer
                        toTarget(player.Character.HumanoidRootPart.Position,workspace.npc.logtraining:FindFirstChild("HumanoidRootPart").Position,CFrame.new(game:GetService("Workspace").npc.logtraining:FindFirstChild("HumanoidRootPart").Position))
                        end)
                        
                        game:GetService('RunService').Stepped:connect(function()
                        if autofarm or gift then
                        pcall(function()
                        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                        end)
                        end
                        end)
                        local green = "http://www.roblox.com/asset/?id=5459241648"
                        local red = "http://www.roblox.com/asset/?id=5459241799"
                        local candy = "http://www.roblox.com/asset/?id=6078390771"
                        spawn(function()
                        while wait() do
                        if autofarm then
                        if  player.currentmission.Value == nil then
                            for i,v in pairs(workspace.missiongivers:GetChildren()) do
                                pcall(function()
                                    if player.currentmission.Value == nil and v.Name == "" and v:FindFirstChild("Head") and v.Head:FindFirstChild("givemission").Enabled and v.Head.givemission:FindFirstChild("color").Visible  then
                                        local TALK = v:FindFirstChild("Talk")
                                        local lvl = player.statz.lvl.lvl.Value
                                        if lvl <= 699 then
                                            if player.currentmission.Value == nil  and v.Talk:FindFirstChild("typ").Value == "defeat" and v.Head.givemission.Enabled and v.Head.givemission.color.Visible and v.Head.givemission.color.Image == green then
                                                local getmission = v:FindFirstChild("HumanoidRootPart")
                                                local clienttalk = v:FindFirstChild("CLIENTTALK")
                                                repeat wait(.3)
                                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-8,0)))
                                                    if (player.Character.HumanoidRootPart.Position-v.HumanoidRootPart.Position).Magnitude < 10 then
                                                        clienttalk:FireServer()
                                                        wait(.3)
                                                        clienttalk:FireServer("accept")
                                                    end
                                                until mission.Visible or v:FindFirstChild("Head").givemission.Enabled == false or player.currentmission.Value == "mission" or not autofarm
                                            end
                                        elseif lvl >= 700 then
                                            if player.currentmission.Value == nil and TALK.typ.Value == "defeat" and v.Head.givemission.Enabled and v.Head.givemission.color.Visible and v.Head.givemission.color.Image == green or v.Head.givemission.color.Image == red then
                                                local getmission = v:FindFirstChild("HumanoidRootPart")
                                                local clienttalk = v:FindFirstChild("CLIENTTALK")
                                                repeat wait(.3)
                                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-8,0)))
                                                    if (player.Character.HumanoidRootPart.Position-v.HumanoidRootPart.Position).Magnitude < 10 then
                                                        clienttalk:FireServer()
                                                        wait(.3)
                                                        clienttalk:FireServer("accept")
                                                    end
                                                until mission.Visible or v:FindFirstChild("Head").givemission.Enabled == false or player.currentmission.Value == "mission" or not autofarm
                                            end
                                        end
                                    end
                                end)
                            end
                        else
                            for i,v in pairs(workspace.npc:GetChildren()) do
                                pcall(function()
                                    if v.ClassName == "Model" and v:FindFirstChild("npctype") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 then
                                        repeat wait(.5)
                                            toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-8,0)))
                                            v.Humanoid.Health = 0
                                        until v.Humanoid.Health == 0 or not autofarm or player.currentmission.Value == nil
                                    end
                                end)
                            end
                        end
                        end
                        end
                        end)
                        spawn(function()
                        while wait() do
                        if gift then
                        local spins = player.statz.spins.Value
                        if spins < 500 then
                            for i,v in pairs(workspace.missiongivers:GetChildren()) do
                                pcall(function()
                                    if mission.Visible == false and v.ClassName == "Model" and v:FindFirstChild("Head"):FindFirstChild("givemission").Enabled and v:FindFirstChild("CLIENTTALK") and v:FindFirstChild("Talk") and string.find(v.Talk.talk1.Value, "Happy holidays, here is 1 FREE spin!") and v.Talk:FindFirstChild("typ").Value == "halloweenevent" and v.Head.givemission.color.Image == gift then
                                        repeat wait(.3)
                                            toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-5,0)))
                                            v.CLIENTTALK:FireServer()
                                            wait(.2)
                                            v.CLIENTTALK:FireServer("accept")
                                        until v:FindFirstChild("Head").givemission.Enabled == false or not gift
                                    end
                                end)
                            end
                        else
                            print("max spins reached 500")
                        end
                        end
                        end
                        end)
                        local function SCROLLFARM()
                        for i,v in pairs(game.workspace.GLOBALTIME:GetChildren()) do
                        if v.ClassName == "Model" and v:FindFirstChild("sh") and v.sh.Position.Y > -1000 and v.sh.Position.Y < 2000 then
                        local scrollA = v.sh:FindFirstChild("invoke")
                        print("SCROLL SPAWNED")
                        pcall(function()
                            toTarget(game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position,v.sh.Position,CFrame.new(v.sh.Position))
                        end)
                        scrollA:FireServer(game.Players.LocalPlayer)
                        fireclickdetector(v.sh.ClickDetector)
                        end
                        end
                        end
                        local function SCROLLFARM1()
                        for i,v in pairs(game.workspace:GetChildren()) do
                        if v.ClassName == "Model" and v:FindFirstChild("sh") and v.sh.Position.Y > -1000 and v.sh.Position.Y < 2000 then
                        local scrollA = v.sh:FindFirstChild("invoke")
                        print("SCROLL SPAWNED in workspace")
                        pcall(function()
                            toTarget(game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position,v.sh.Position,CFrame.new(v.sh.Position))
                            scrollA:FireServer(game.Players.LocalPlayer)
                            fireclickdetector(v.sh.ClickDetector)
                        end)
                        end
                        end
                        end
                        
                        spawn(function()
                        while wait() do
                        if scrollfarm then
                        repeat wait()
                            SCROLLFARM()
                            SCROLLFARM1()
                        until not scrollfarm or not war or not war2
                        end
                        end
                        end)
                        
                        game:GetService('RunService').Stepped:connect(function()
                        if war or war2 then
                        pcall(function()
                        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                        end)
                        end
                        end)
                        
                        spawn(function()
                        while wait() do
                        if war or war2 then
                        repeat wait()
                            SCROLLFARM()
                            SCROLLFARM1()
                        until not scrollfarm or not war or not war2
                        end
                        end
                        end)
                        spawn(function()
                        while wait() do
                        if war then
                        pcall(function()
                            refresh:Refresh("War Completed: " .. count)
                            refreshC:Refresh("Round: " .. workspace.warserver.round.Value)
                        end)
                        for i,v in pairs(workspace.npc:GetChildren()) do
                            if workspace.warserver:FindFirstChild("zetsu").Value > 0 and string.find(workspace.warserver.text.Value, "Left") or string.find(workspace.warserver.text.Value, "DEFEAT") and v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and not v:FindFirstChild("megaboss") then
                                wait(.2)
                                pcall(function()
                                    v.Humanoid.Health = 0
                                end)
                            elseif v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and v:FindFirstChild("megaboss") then
                                wait(6)
                                pcall(function()
                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position))
                                    v.Humanoid.Health = 0
                                end)
                            end
                        end
                        if reset then
                            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                                if v.Name == "warserver" and v:FindFirstChild("round").Value > 20 then
                                    wait(5)
                                    player.Character:BreakJoints()
                                    repeat wait()
                                    until v.round.Value == 0
                                    count = count + 1
                                end
                            end
                        end
                        end
                        end
                        end)
                        
                        spawn(function()
                        while wait() do
                        if war2 then
                        refresh:Refresh("War Completed: " .. count)
                        refreshC:Refresh("Round: " .. workspace.warserver.round.Value)
                        for i,v in pairs(workspace.npc:GetChildren()) do
                            if workspace.warserver:FindFirstChild("zetsu").Value > 0 and string.find(workspace.warserver.text.Value, "Left") or string.find(workspace.warserver.text.Value, "DEFEAT") and v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and not v:FindFirstChild("megaboss") then
                                pcall(function()
                                    repeat wait()
                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-12,0)))
                                    wait(.3)
                                    v.Humanoid.Health = 0
                                    until v.Humanoid.Health == 0
                                end)
                            elseif v.ClassName == "Model" and v:FindFirstChild("npc") and string.find(v.Name, "npc") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Head.CFrame.Y > -1000 and v:FindFirstChild("megaboss") then
                                wait(8)
                                pcall(function()
                                    toTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-25,0)))
                                    v.Humanoid.Health = 0
                                end)
                            else
                                wait()
                            end
                        end
                        if reset then
                            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                                if v.Name == "warserver" and v:FindFirstChild("round").Value > 20 then
                                    wait(5)
                                    player.Character:BreakJoints()
                                    repeat wait()
                                    until v.round.Value == 0
                                    count = count + 1
                                end
                            end
                        end
                        end
                        end
                        end)
                        
                        local function JINFARM()
                        for i,v in pairs(game:GetService("Workspace").npc:GetChildren()) do
                        if v.Name == "npc1" then
                        repeat wait()
                            pcall(function()
                                toTarget(game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position,v.HumanoidRootPart.Position,CFrame.new(v.HumanoidRootPart.Position+Vector3.new(0,-25,0)))
                                player.Character.combat.update:FireServer("mouse1", true)
                                wait(.1)
                                v.Humanoid.HealthChanged:Connect(function()
                                    v.Humanoid.Health = 0
                                end)
                            end)
                        until v.Humanoid.Health == 0 or not jinfarm
                        end
                        end
                        end
                        spawn(function()
                        while wait() do
                        if jinfarm then
                        JINFARM()
                        end
                        end
                        end)
                        spawn(function()
                        while wait() do
                        if RANKUP and player.statz.lvl:FindFirstChild("lvl").Value == 1000 then
                        repeat wait()
                            game.Players.LocalPlayer.startevent:FireServer("rankup")
                        until player.statz.lvl:FindFirstChild("lvl").Value == 1 or not RANKUP
                        end
                        end
                        end)
                        
                        --
                        
                        
                        -- Theme page
                        local settings = venyx:addPage("Settings", 8419885246)
                        local colors = settings:addSection("Colors")
                        local setting = settings:addSection("Settings")
                        
                        setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
                        print("Activated Keybind")
                        venyx:toggle()
                        end, function()
                        print("Changed Keybind")
                        end)
                        
                        for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
                        colors:addColorPicker(theme, color, function(color3)
                        venyx:setTheme(theme, color3)
                        end)
                        end
                        end
                        
                        -- load
                        venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
                        end
                        















































                        if game.PlaceId == 537413528 then
                            local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/zxciaz/VenyxUI/main/Reuploaded"))() --someone reuploaded it so I put it in place of the original back up so guy can get free credit.
                            local venyx = library.new("Ez W Hub: Build A Boat For Treasure", 5013109572)
















                            local page = venyx:addPage("Home", 8162117119)
                            local section1 = page:addSection("Credits")
                            section1:addButton("Made by: rblx-scripts.com#0031 and Auick#0163")
                            section1:addButton("Premium founder: Auick#0163")
                            
                            local section2 = page:addSection("Premium Features")
                            section2:addButton("More Supported Games")
                            section2:addButton("Better Scripts")
                            
                            local section4 = page:addSection("How to get Premium")
                            section4:addButton("Join our discord server go to our website.")
                            section4:addButton("if you want buy it with paypal dm me first.")
                            section4:addButton("My discord name is: rblx-scripts.com#0031")
                            
                            section4:addButton("Copy Website Link to clipboard", function()
                                setclipboard("https://www.ezwhub.xyz/")
                            end)
                            
                            section4:addButton("Copy Discord Link to clipboard", function()
                                setclipboard("https://discord.gg/2NyAaSRtJu")
                            end)
                            local section3 = page:addSection("Support")
                            section3:addButton("Join our discord server for the Support")








                        
                            local section1 = venyx:addPage("Farming", 8419618272)
                            local section1 = section1:addSection("Farming")
                            section1:addButton("Autofarm", function()
                                local vu = game:GetService("VirtualUser")
game:GetService("Players").LocalPlayer.Idled:connect(function()
 vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
 wait(1)
 vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
end)
game.Players.LocalPlayer.Character.Head:Destroy()
wait(7)
spawn(function()
game:GetService("RunService").Stepped:connect(function()
game.Players.LocalPlayer.Character:WaitForChild("Humanoid"):ChangeState(11)
end) end)
game.Players.LocalPlayer.CharacterAdded:Connect(function()
Clone = game:GetService("Players").LocalPlayer.Character.LowerTorso.Root:Clone()
  game:GetService("Players").LocalPlayer.Character.LowerTorso.Root:Destroy()
  Clone.Parent = game:GetService("Players").LocalPlayer.Character
end)
game.Workspace.Gravity = 0
local CFrameEnd = CFrame.new(-51.1823959, 80.6168747, -536.437805)
local Time = 1
local tween =  game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd})
tween:Play()
tween.Completed:Wait(E)

local CFrameEnd = CFrame.new(-47.6731682, 66.860466, 8698.90137, 0.999818563, 0.00121844851, -0.0190091729, 8.06243428e-09, 0.997951984, 0.0639670715, 0.0190481842, -0.0639554635, 0.997770965)
local Time = 33
local tween =  game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd})
tween:Play()
tween.Completed:Wait(E)
wait(0.3)
local CFrameEnd = CFrame.new(-58.6682281, -359.746033, 9489.12891, -0.993616283, 0.0757325292, -0.0836138725, -2.70548408e-05, 0.74101454, 0.671488941, 0.112812653, 0.667204618, -0.736282051)
local Time = 1
local tween =  game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd})
tween:Play()
tween.Completed:Wait(E)
game.Players.LocalPlayer.CharacterAdded:Connect(function()
   repeat
       wait()
   until game.Players.LocalPlayer.Character
       wait(3.3)
       game.Workspace.Gravity = 0
local CFrameEnd = CFrame.new(-51.1823959, 80.6168747, -536.437805)
local Time = 1 -- Time in seconds
local tween =  game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd})
tween:Play()
tween.Completed:Wait(E)

local CFrameEnd = CFrame.new(-47.6731682, 66.860466, 8698.90137, 0.999818563, 0.00121844851, -0.0190091729, 8.06243428e-09, 0.997951984, 0.0639670715, 0.0190481842, -0.0639554635, 0.997770965)
local Time = 33
local tween =  game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd})
tween:Play()
tween.Completed:Wait(E)

local CFrameEnd = CFrame.new(-58.6682281, -359.746033, 9489.12891, -0.993616283, 0.0757325292, -0.0836138725, -2.70548408e-05, 0.74101454, 0.671488941, 0.112812653, 0.667204618, -0.736282051)
local Time = 1
local tween =  game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart, TweenInfo.new(Time), {CFrame = CFrameEnd})
tween:Play()
tween.Completed:Wait(E)
game.Workspace.Gravity = 200
end)
spawn(function()
   while wait (2) do
workspace.ClaimRiverResultsGold:FireServer()
     end
end)
                            end)



-- themes
local themes = {
    Background = Color3.fromRGB(24, 24, 24),
    Glow = Color3.fromRGB(0, 0, 0),
    Accent = Color3.fromRGB(10, 10, 10),
    LightContrast = Color3.fromRGB(20, 20, 20),
    DarkContrast = Cloolor3.fromRGB(14, 14, 14),
    TextColor = Cor3.fromRGB(255, 255, 255)
    }
    
        
    -- Theme page
    local settings = venyx:addPage("Settings", 5012544693)
    local colors = settings:addSection("Themes")
    local setting = settings:addSection("Settings")
    
    setting:addKeybind("Show/Hide Settings", Enum.KeyCode.P, function()
    print("Activated Keybind")
    venyx:toggle()
    end, function()
    print("Changed Keybind")
    end)
    
    for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
    colors:addColorPicker(theme, color, function(color3)
    venyx:setTheme(theme, color3)
    end)
 end
 -- load
 venyx:SelectPage(venyx.pages[1], true) -- no default for more freedom
 end



