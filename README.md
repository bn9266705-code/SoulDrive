local Player = game:GetService("Players").LocalPlayer
local CurrentRig = Player.Character

local CHAR = "Guest1337"

local SHIRT = "http://www.roblox.com/asset/?id=75801882168409"
local PANTS = "http://www.roblox.com/asset/?id=136961770390363"
local FACE_MESH = "rbxassetid://83341561734918"
local FACE_TEX = "rbxassetid://137770144723092"
local FACE_SCALE = Vector3.new(0.957, 0.957, 0.957)
local GIRL_TORSO_MESH = 48112070
local WHITE = Color3.fromRGB(255, 255, 255)

local function CF12(x, y, z, r00, r01, r02, r10, r11, r12, r20, r21, r22)
  return CFrame.new(x, y, z, r00, r01, r02, r10, r11, r12, r20, r21, r22)
end

local function Accs(name, char, mesh, tex, scale, c0, c1, welded)
  local acc = Instance.new("Accessory")
  acc.Name = name
  acc.Parent = char
  local h = Instance.new("Part")
  h.Name = "Handle"
  h.Anchored = false
  h.Massless = true
  h.CanCollide = false
  h.Size = Vector3.new(1, 1, 1)
  h.Parent = acc
  local m = Instance.new("SpecialMesh")
  m.Name = "Mesh"
  m.MeshId = mesh
  m.TextureId = tex
  m.Scale = scale or Vector3.new(1, 1, 1)
  m.Parent = h
  local part = char:FindFirstChild(welded)
  if not part then return end
  local w = Instance.new("Weld")
  w.Name = "AccessoryWeld"
  w.Part0 = h
  w.Part1 = part
  w.C0 = c0
  w.C1 = c1 or CFrame.new()
  w.Parent = h
end

local function strip(P)
  for _, v in ipairs(P:GetChildren()) do
    if v:IsA("Accessory") or v:IsA("Hat") or v:IsA("Shirt") or v:IsA("Pants") or v:IsA("ShirtGraphic") or v:IsA("CharacterMesh") then
      pcall(function() v:Destroy() end)
    end
    if v.Name == "Clothing" or v.Name == "ExpressionHolder" or v.Name == "Cape" or v.Name == "Model" then
      pcall(function() v:Destroy() end)
    end
  end
end

local function setFace(P)
  local head = P:FindFirstChild("Head")
  if not head then return end
  for _, d in ipairs(head:GetChildren()) do
    if d:IsA("Decal") then
      local n = string.lower(d.Name)
      if n == "face" or n == "customface" or d.Face == Enum.NormalId.Front then
        pcall(function() d:Destroy() end)
      end
    end
  end
  local mesh = head:FindFirstChildOfClass("SpecialMesh") or head:FindFirstChild("Mesh")
  if not mesh then
    mesh = Instance.new("SpecialMesh")
    mesh.Name = "Mesh"
    mesh.Parent = head
  end
  mesh.MeshType = Enum.MeshType.FileMesh
  mesh.MeshId = FACE_MESH
  mesh.TextureId = FACE_TEX
  mesh.Scale = FACE_SCALE
end

local function setGirlTorso(P)
  for _, v in ipairs(P:GetChildren()) do
    if v:IsA("CharacterMesh") and (v.BodyPart == Enum.BodyPart.Torso or tostring(v.Name):find("Torso") or tostring(v.Name):find("torso")) then
      v:Destroy()
    end
  end
  local cm = Instance.new("CharacterMesh")
  cm.Name = "ROBLOX Girl Torso"
  cm.BodyPart = Enum.BodyPart.Torso
  cm.MeshId = GIRL_TORSO_MESH
  cm.Parent = P
end

local function cloth(P)
  local s = Instance.new("Shirt", P)
  s.ShirtTemplate = SHIRT
  local p = Instance.new("Pants", P)
  p.PantsTemplate = PANTS
end

local function body(P)
  for _, n in ipairs({"Head", "Torso", "Left Arm", "Right Arm", "Left Leg", "Right Leg"}) do
    local L = P:FindFirstChild(n)
    if L and L:IsA("BasePart") then
      L.Transparency = 0
      L.Color = WHITE
    end
  end
end

local C1_HEAD = CF12(0, 0.6, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
local C1_NECK = CF12(0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
local C1_FACE = CF12(0, 0, -0.6, 1, 0, 0, 0, 1, 0, 0, 0, 1)
local C1_WAIST = CF12(0, -1, 0.5, 1, 0, 0, 0, 1, 0, 0, 0, 1)

local function equipAccs(P)
  Accs("Ears", P, "rbxassetid://14261000226", "rbxassetid://15410063145", Vector3.new(1, 1, 1),
    CF12(0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1), C1_HEAD, "Head")
  Accs("SpikeyHair", P, "rbxassetid://130011686754512", "rbxassetid://18999927178", Vector3.new(1, 1, 1),
    CF12(-0.121, 1.108, 0, 0, 0, 1, 0, 1, 0, -1, 0, 0), C1_HEAD, "Head")
  Accs("BellCollar", P, "rbxassetid://17599539067", "rbxassetid://17599241458", Vector3.new(1, 1, 1),
    CF12(-0.0170211792, 0.350349426, -0.184863195, -1, 0, 0, 0, 1, 0, 0, 0, -1), C1_NECK, "Torso")
  Accs("MaidTail", P, "rbxassetid://110730919539000", "rbxassetid://117459734827897", Vector3.new(1, 1, 1),
    CF12(0, -0.135421395, -1.02638626, 1, 0, 0, 0, 1, 0, 0, 0, 1), C1_WAIST, "Torso")
  Accs("FaceBlush", P, "rbxassetid://88257329712279", "http://www.roblox.com/asset/?id=75732475673358", Vector3.new(1, 1, 1),
    CF12(-0.006, 0.151, 0.014, 1, 0, 0, 0, 1, 0, 0, 0, 1), C1_FACE, "Head")
  Accs("FlowerPin", P, "rbxassetid://8034834230", "rbxassetid://8034888598", Vector3.new(1, 1, 1),
    CF12(-0.522, -0.06, -0.322, -1, 0, 0, 0, 1, 0, 0, 0, -1), C1_HEAD, "Head")
  Accs("WolfCut", P, "rbxassetid://8289554071", "rbxassetid://8832886364", Vector3.new(1, 1, 1),
    CF12(-0.005, 0.117, 0.125, -1, 0, 0, 0, 1, 0, 0, 0, -1), C1_HEAD, "Head")
  Accs("CurlyHair", P, "rbxassetid://13556307008", "http://www.roblox.com/asset/?id=13083397347", Vector3.new(1, 1, 1),
    CF12(-0.061, 1.248, -0.074, 1, 0, 0, 0, 1, 0, 0, 0, 1), C1_HEAD, "Head")
end

local function DoMorph(P)
  if not P then return end
  if P.Name ~= CHAR then return end
  if P:GetAttribute("SkinName") and P:GetAttribute("SkinName") ~= "" then return end

  strip(P)
  body(P)
  setGirlTorso(P)
  cloth(P)
  setFace(P)
  equipAccs(P)

  task.delay(0.5, function()
    if P and P.Parent then
      setFace(P)
      setGirlTorso(P)
    end
  end)
end

if CurrentRig then
  task.spawn(function()
    task.wait(0.6)
    DoMorph(CurrentRig)
  end)
end

Player.CharacterAdded:Connect(function(Rig)
  task.wait(0.6)
  DoMorph(Rig)
end)
