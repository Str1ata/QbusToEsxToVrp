# QbusToEsx Qbus Komut Dosyalarını ESX'e Dönüştürme, kesintisiz güncelleme.
# Anlaşmazlık: www.discord.gg/mdtyazilim

# QbusToEsx Qbus ve ESX Komut Dosyalarını vRP'ye dönüştürme, kesintisiz güncelleme.
# Uyuşmazlık: https://discord.gg/DAdDZv6A5G
--------------------------------------------------------------------------------------------------
Qbus Temeli Ve ESX temeli.
 ```lua
QBCore = nil 

Citizen.CreateThread(function()
	while QBCore == nil do
		TriggerEvent('QBCore:GetObject', function(obj) QBCore = obj end)
		Citizen.Wait(30) -- Saniye Bekletme
	end
end)
```
Altaki yeni olanlar için -- üsteki eski sürüm için, çalışmaz ise ikisinide dene...
```lua
local QBCore = exports['qb-core']:GetCoreObject()
```

# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- fxmanifest bir tek

client_scripts {
	"@vrp/lib/utils.lua",
	"client.lua",
}

server_scripts {
	"@vrp/lib/utils.lua",
	"server.lua",
}

-- Server bir tek
local Tunnel = module("vrp","lib/Tunnel")
local Proxy = module("vrp","lib/Proxy")
vRP = Proxy.getInterface("vRP")
vRPclient = Tunnel.getInterface("vRP")

-- client bir tek
local Proxy = module("vrp","lib/Proxy")
local Tunnel = module("vrp", "lib/Tunnel")
vRP = Proxy.getInterface("vRP")
```

# ALTAKİ ESX
```lua
ESX = nil

Citizen.CreateThread(function()
  while ESX == nil do
    TriggerEvent('esx:getSharedObject', function(obj) ESX = obj end)
    Citizen.Wait(30)-- Saniye Bekletme
  end
end)
```

--------------------------------------------------------------------------------------------------

Beyler Bu kısım Yoktu eklendi.
Anlamı:
Oyuncu Giriş Kısmı İlik Oyuna Girerken Lazım, Yani Server Dosyasıdır.
Bu olay, oyuncu sunucuya bağlandığında tetiklenir
```lua
RegisterNetEvent('QBCore:Client:OnPlayerLoaded')
AddEventHandler('QBCore:Client:OnPlayerLoaded',
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
RegisterServerEvent("vRP:playerSpawn")
AddEventHandler("vRP:playerSpawn",function(user_id,source,first_spawn)
end)
```

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:playerLoaded')
AddEventHandler('esx:playerLoaded',
```

--------------------------------------------------------------------------------------------------

Server Dosyası, Job Kısmı Meslek Kısmıdır.
```lua
RegisterNetEvent('QBCore:Client:OnJobUptade')
AddEventHandler('QBCore:Client:OnJobUptade', 
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
local source = source
local user_id = vRP.getUserId(source)
vRP.insertPermission(parseInt(user_id),tostring("Police"))
```

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:setJob')
AddEventHandler('esx:setJob',
```

--------------------------------------------------------------------------------------------------

Burdan Kontrol Edebilrsiniz.
https://esx-framework.github.io/es_extended/common/events/onplayerdeath/#example-client-side-usage
```lua
RegisterNetEvent('QBCore:Client:OnPlayerUnload')
AddEventHandler('QBCore:Client:OnPlayerUnload',
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- client bir tek
AddEventHandler('gameEventTriggered', function (name, args)
     if name == 'CEventNetworkEntityDamage' then
          local ped = PlayerPedId()
          local coords = GetEntityCoords(ped)
          local killer = GetPedKiller(ped)
          local cause = GetPedCauseOfDeath(ped)
     end
end)
```

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:onPlayerDeath')
AddEventHandler('esx:onPlayerDeath',
```

--------------------------------------------------------------------------------------------------

Beyler Bu kısım Yoktu eklendi.
Anlamı:
Bu işlev, en yakın oyuncu istemci kimliğini ve oynatıcıya olan mesafeyi alır.
```lua
QBCore.Functions.GetClosestPlayer()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
local source = source
local distance = 3
local nearestSource = vRPclient.nearestPlayer(source, distance)

-- client bir tek
local distance = 3
local nearestSource = vRP.nearestPlayer(distance)
```

# ALTAKİ ESX
```lua
ESX.Game.GetClosestPlayer()
```

--------------------------------------------------------------------------------------------------

3D li Yazı Ekleme, Cilent Dosyası. Örnek : https://media.discordapp.net/attachments/623207764314816562/812096508786507806/resim_1.png
```lua
QBCore.Functions.DrawText3D(1, 1, 1, 'Örnek')
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- client bir tek
local coords = { x = 1112.44, y = -641.48, z = 56.82 }
local loop = true
repeat
     Wait(1000)
     DrawText3D(coords.x,coords.y,coords.z,"Örnek")
until(loop == false)
```

# ALTAKİ ESX
```lua
DrawText3D(1, 1, 1, 'Örnek') -- (aşağısına function açmanız gerekmektedir.)
ESX.Game.Utils.DrawText3D(1, 1, 1, 'Örnek') -- ESX bunda gerek yok zaten var, fonksiyona.
```

--------------------------------------------------------------------------------------------------

Menu Aç Kapat ESX & QBCore De Ki Menüler Örnekler : https://prnt.sc/u4f7s5
```lua
QBCore.UI.Menu.Open
QBCore.UI.Menu.CloseAll() -- (menu default scripti kurmanız gerekmektedir.)
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua

```

# ALTAKİ ESX
```lua
ESX.UI.Menu.Open
ESX.UI.Menu.CloseAll()
```

--------------------------------------------------------------------------------------------------

Bildirim Scripti Örnek : https://dosya.turkmmo.com/2020/09/36521_efa54848705a4069cbedfc2770e50cf1.png
```lua
TriggerClientEvent("QBCore:Notify", "Text/Yazı", "success", 2500)

-- üsteki server -- altaki client

QBCore.Functions.Notify("Text/Yazı.", "error")
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- sadece 4 tip
local type = "negado"  -- reddedildi
local type = "sucesso"  -- başarı
local type = "aviso"  -- uyarı
local type = "Importante"  -- Önemli

local time = 4500 -- miliseconds

local mensage = "Örnek"
----------------------------

TriggerClientEvent('Notify',source,type,mensage,time)
-- üsteki server -- altaki client
TriggerEvent('Notify',type,mensage,time)
```

# ALTAKİ ESX
```lua
TriggerEvent('Notification',"Text/Yazı.")

-- üsteki server -- altaki client

ESX.ShowHelpNotification('Text/Yazı.')
```

--------------------------------------------------------------------------------------------------

Enventer İtem Kısmı.
```lua
xPlayer.Functions.GetItemByName 
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local itemName = "Örnek"
local user_id = vRP.getUserId(source)
local ammount = vRP.getInventoryItemAmount(user_id,itemName)
```

# ALTAKİ ESX
```lua
xPlayer.getInventoryItem
```
--------------------------------------------------------------------------------------------------

```lua
xPlayer.PlayerData.name 
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
local identity = vRP.getUserIdentity(user_id)

local fristName = identity.name
local lastName = identity.name2
```

# ALTAKİ ESX
```lua
xPlayer.getName()
```

--------------------------------------------------------------------------------------------------

Job Başlangıç kod.
```lua
RegisterNetEvent('QBCore:Client:OnJobUpdate')
AddEventHandler('QBCore:Client:OnJobUpdate', function(job)
    PlayerData.job = job
end)
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
local group = "police"
vRP.insertPermission(user_id,group)
```

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:setJob')
AddEventHandler('esx:setJob', function(job)
    PlayerData.job = job
end)
```

--------------------------------------------------------------------------------------------------

Para Ver Para Al Kısmı
```lua
Player.Functions.AddMoney('bank', amount, "Bank depost") -- banka
Player.Functions.RemoveMoney('cash', amount, "Bank depost") -- üstündeki para
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
local amount = 1000
vRP.setMoney(user_id,amount) -- banka
vRP.tryPayment(user_id,amount)-- üstündeki para
```
# ALTAKİ ESX
```lua
xPlayer.removeAccountMoney('bank', amount) --para kaldırma
xPlayer.addMoney(amount) -- para ekleme
```

--------------------------------------------------------------------------------------------------

Para Kısmı Data.
```lua
Player.PlayerData.money["bank"]
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
local moneyAmount = vRP.getMoney(user_id)
```

# ALTAKİ ESX
```lua
xPlayer.getAccount('bank').money
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.IsSpawnPointClear()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- client bir tek
IsAnyVehicleNearPoint(coords.x,coords.y,coords.z,distance) == false then
```

# ALTAKİ ESX
```lua
ESX.Game.IsSpawnPointClear()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.SetVehicleProperties()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua

```

# ALTAKİ ESX
```lua
ESX.Game.SetVehicleProperties()
```

--------------------------------------------------------------------------------------------------

Envanter İtem Silme Kısmı.
```lua
xPlayer.Functions.RemoveItem 
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)

local itemName = "Örnek"
local amount = 1
vRP.tryGetInventoryItem(user_id,itemName,amount,true)
```

# ALTAKİ ESX
```lua
xPlayer.removeInventoryItem 
```

--------------------------------------------------------------------------------------------------

Envanter İtem Ekleme Kısmı.
```lua
xPlayer.Functions.AddItem
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)

local itemName = "Örnek"
local amount = 1
vRP.giveInventoryItem(user_id,itemName,amount,true)
```

# ALTAKİ ESX
```lua
xPlayer.addInventoryItem
```

--------------------------------------------------------------------------------------------------

Karakter Kımsı Oyuncunun İd Si Gibi Birşey.
```lua
QBCore.Functions.GetPlayer(src)
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
```

# ALTAKİ ESX
```lua
ESX.GetPlayerFromId(src)
```


--------------------------------------------------------------------------------------------------

Tüm oyuncuları çeker.
```lua
QBCore.Functions.GetPlayers(src)
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.GetPlayers(src)
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.GetPlayerByCitizenId(src)
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
```

# ALTAKİ ESX
```lua
ESX.GetPlayerFromIdentifier(src)
```

--------------------------------------------------------------------------------------------------

Bu işlev, tüm sondaki beyaz boşlukları kaldırarak bir metni kırpar. Genellikle `GetVehicleNumberPlateText()` yerlileri dezenfekte ederken kullanılır.
#örnek
```lua
QBCore.Functions.MathTrim(GetVehicleNumberPlateText(vehicle))
````
#standart
```lua
QBCore.Functions.MathTrim 
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
local vehicle,vnetid,placa,vname,lock,banned,trunk,model,street = vRPclient.vehList(source,7)
```

# ALTAKİ ESX
```lua
ESX.Math.Trim(value)
```

--------------------------------------------------------------------------------------------------

Nill buşta bilinmiyor güncelencek
# ÖRNEK
```lua
QBCore.Functions.MathRound(GetVehicleBodyHealth(vehicle), 1),
```
#standart
```lua
QBCore.Functions.MathRound()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
local vehicle,vnetid,placa,vname,lock,banned,trunk,model,street = vRPclient.vehList(source,7)
```

# ALTAKİ ESX
# ÖRNEK
```lua
local deger - 5.444

print ('deger:' .. değer) - 5.444 -- döndürür
print ('deger yuvarlandı:' .. ESX.Math.Round(deger)) -- 5 döndürür
print ('deger yuvarlandı:' .. ESX.Math.Round(deger, 1)) -- 5,4 döndürür
```
#standart
```lua
ESX.Math.Round(değer, numaraOndalıkBasamaklar)
```

--------------------------------------------------------------------------------------------------

Araba Spawn Kısmı Konumu Vsb Şeyler.
```lua
QBCore.Functions.SpawnVehicle()
QBCore.Functions.DeleteVehicle()
QBCore.Functions.GetVehicleProperties()
QBCore.Functions.GetClosestVehicle()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
local vehicle,vnetid,placa,vname,lock,banned,trunk,model,street = vRPclient.vehList(source,7)
```

# ALTAKİ ESX
```lua
ESX.Game.SpawnVehicle()
ESX.Game.DeleteVehicle()
ESX.Game.GetVehicleProperties()
ESX.Game.GetClosestVehicle()
```
--(Eğer ESX.Game olan neredeyse her şey QBCore.Functions olarak aynı şekildedir.)


--------------------------------------------------------------------------------------------------

`qb-core/client/functions.lua`
bunu qb-core de client functions.lua. atın bir boş satıra
```lua
function QBCore.Functions.RequestNamedPtfxAsset(assetName, cb)
	if not HasNamedPtfxAssetLoaded(assetName) then
		RequestNamedPtfxAsset(assetName)

		while not HasNamedPtfxAssetLoaded(assetName) do
			Citizen.Wait(1)
		end
	end

	if cb ~= nil then
		cb()
	end
end
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua

```

# ALTAKİ ESX
```lua
function ESX.Streaming.RequestNamedPtfxAsset(assetName, cb)
	if not HasNamedPtfxAssetLoaded(assetName) then
		RequestNamedPtfxAsset(assetName)

		while not HasNamedPtfxAssetLoaded(assetName) do
			Citizen.Wait(1)
		end
	end

	if cb ~= nil then
		cb()
	end
end
```


--------------------------------------------------------------------------------------------------

`qb-core/client/functions.lua`
bunu qb-core de client functions.lua. atın bir boş satıra
```lua
function QBCore.Functions.DeleteObject(object)
	SetEntityAsMissionEntity(object, false, true)
	DeleteObject(object)
end
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua

```

# ALTAKİ ESX
```lua
function ESX.Game.DeleteObject(object)
	SetEntityAsMissionEntity(object, false, true)
	DeleteObject(object)
end
```

--------------------------------------------------------------------------------------------------

`qb-core/server/functions.lua`
bunu qb-core de server functions.lua. atın bir boş satıra
```lua
function QBCore.Functions.GetItemLabel(item)
	if QBCore.UseableItems[item] ~= nil then
		return QBCore.UseableItems[item].label
	end
end
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local index = vRP.itemIndexList(item)
```

# ALTAKİ ESX
```lua
function ESX.GetItemLabel(item)
	if ESX.Items[item] then
		return ESX.Items[item].label
	end
end
```

--------------------------------------------------------------------------------------------------

Oyuncu Kendi Karakterin.
```lua
QBCore.Functions.GetPlayerData()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.GetPlayerData()
```

--------------------------------------------------------------------------------------------------

İtem Oluşturma.
```lua
QBCore.Functions.CreateUseableItem()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.RegisterUsableItem()
```

--------------------------------------------------------------------------------------------------

Banka Para Kaldırma.
```lua
Player.Functions.RemoveMoney()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- server bir tek
local source = source
local user_id = vRP.getUserId(source)
local amount = 1000
vRP.tryPayment(user_id,amount)
```

# ALTAKİ ESX
```lua
xPlayer.removeMoney(money)
```

--------------------------------------------------------------------------------------------------

Dosya'lar İle Alakalı.
```lua
QBCore.Functions.CreateCallback()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
serverTunnel = {}
Tunnel.bindInterface("script-name",serverTunnel)

function serverTunnel.functionServerExemple(source,args)
     if args == "Örnek" then
          return true
     else
          return false
     end
end

-- client bir tek
clientTunnel = {}
Tunnel.bindInterface("script-name",clientTunnel)

function clientTunnel.functionClientExemple(source,args)
     if args == "Örnek" then
          return true
     else
          return false
     end
end
```

# ALTAKİ ESX
```lua
ESX.RegisterServerCallback()
```

--------------------------------------------------------------------------------------------------

Dosya'lar İle Alakalı.
```lua
QBCore.Functions.TriggerCallback()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
clientTunnel = Tunnel.getInterface("script-name")
clientTunnel.functionClientExemple(source,"Örnek")
-- client bir tek
serverTunnel = Tunnel.getInterface("script-name")
serverTunnel.functionServerExemple(source,"Örnek")
```

# ALTAKİ ESX
```lua
ESX.TriggerServerCallback()
```

--------------------------------------------------------------------------------------------------

qb'de cid esx'de identifier kullanılıyor olayı çözmeniz için ufak bir kod bloğu bıraktım.
```lua
QBCore.Functions.CreateCallback('system:fetchStatus', function(source, cb)
    local Player = QBCore.Functions.GetPlayer(source)

     if Player then
           exports['ghmattimysql']:execute('SELECT skills FROM players WHERE citizenid = @citizenid', {
               ['@citizenid'] = Player.PlayerData.citizenid
          }, function(status)
              if status ~= nil then
                   cb(json.decode(status))
              else
                   cb(nil)
              end
          end)
     else
          cb()
     end
end)
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
serverTunnel = {}
Tunnel.bindInterface("script-name",serverTunnel)

function serverTunnel.functionServerExemple(source,args)
     local source = source
     local user_id = vRP.getUserId(source)
     local _result = nil
	MySQL.Async.fetchAll('SELECT * FROM skills WHERE vrp_users = @owner', {['@owner'] = user_id,}, function (result)
    	     _result = result
     end)
	
	Wait(20)
	return _result
end
```

# ALTAKİ ESX
```lua
ESX.RegisterServerCallback("system:fetchStatus", function(source, cb)
    local src = source
    local user = ESX.GetPlayerFromId(src)


    local fetch = [[
         SELECT
              skills
         FROM
              users
         WHERE
              identifier = @identifier
    ]]

    MySQL.Async.fetchScalar(fetch, {
         ["@identifier"] = user.identifier

    }, function(status)

         if status ~= nil then
              cb(json.decode(status))
         else
              cb(nil)
         end

    end)
end)
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Shared.Items
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.GetItems()
```
--------------------------------------------------------------------------------------------------

Sql bağlama kısmı
```lua
QBCore.Functions.ExecuteSql()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
-- Server bir tek
local source = source
local user_id = vRP.getUserId(source)
local database = "vRP:multas"
local multas = 50
vRP.setUData(user_id,database,json.encode(parseInt(multas)))
```

# ALTAKİ ESX
```lua
ESX.ExecuteSql() --(ghmattimysql)
MySQL.Async.execute()
```

--------------------------------------------------------------------------------------------------


RegisterCommand - yani chat komut kısmı.
```lua
QBCore.Commands.Add()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
RegisterCommand("command-name", function(source,args,raw)
end)
```

# ALTAKİ ESX
```lua
RegisterCommand 
```
-- (RegisterCommand qbcore'da da çalışır.)

--------------------------------------------------------------------------------------------------

Karakter Kısmı Dır Data Sına Bağlama.
```lua
local Player = QBCore.Functions.GetPlayer(source)
['@citizenid'] = Player.PlayerData.citizenid -- çekme Player
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
local source = source
local user_id = vRP.getUserId(source)
["@identifier"] = user_id -- çekme user
```

# ALTAKİ ESX
```lua
local user = ESX.GetPlayerFromId(src)
["@identifier"] = user.identifier -- çekme user
```
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Shared.Trim()
QBCore.Shared.GroupDigits()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.Math.Trim()
ESX.Math.GroupDigits()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.GetClosestObject()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
GetClosestObjectOfType()
```

# ALTAKİ ESX
```lua
ESX.Game.GetClosestObject()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.GetVehicleInDirection()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua

```

# ALTAKİ ESX
```lua
ESX.Game.GetVehicleInDirection()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.GetPeds()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.Game.GetPeds()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.GetObjects()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.Game.GetObjects()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.GetClosestPed()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```

# ALTAKİ ESX
```lua
ESX.Game.GetClosestPed()
```

--------------------------------------------------------------------------------------------------

```lua
QBCore.Functions.SpawnObject()
```
# ÜSTEKİ QBUSCORE

# MERKEZ VRP
```lua
```


# ALTAKİ ESX
```lua
ESX.Game.SpawnObject()
```

--------------------------------------------------------------------------------------------------
