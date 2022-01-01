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
