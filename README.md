# PolisRevive
######### RAW PASTE; https://pastebin.com/m7LtzM2f

# Detta är något som jag tar från min server!
# Tänk på att allt ska sitta ihop fast i rad undervaran!


# Lägg till detta på din polismeny i client main.lua

			  {label = _U('revive player'),       value = 'revive'},
        
# Efter det lägger du till det här.

if action == 'revive' then
	local closestPlayer, closestDistance = ESX.Game.GetClosestPlayer()
  
	local closestPlayerPed = GetPlayerPed(closestPlayer)
  
	local health = GetEntityHealth(closestPlayerPed)
  
	if health == 0 then
  
	    local playerPed = GetPlayerPed(-1)
      
	    Citizen.CreateThread(function()
      
		   ESX.ShowNotification(_U('revive_inprogress'))
       
		   TaskStartScenarioInPlace(playerPed, 'CODE_HUMAN_MEDIC_TEND_TO_DEAD', 0, true)
       
		   Wait(10000)
       
		   ClearPedTasks(playerPed)
       
		   if GetEntityHealth(closestPlayerPed) == 0 then
       
			   TriggerServerEvent('esx_ambulancejob:revive', GetPlayerServerId(closestPlayer))
         
			   ESX.ShowNotification(_U('revive_complete'))
		   else
			ESX.ShowNotification(_U('isdead'))
      
		   end
		end)
     end
elseif action == 'identity_card' then

    OpenIdentityCardMenu(closestPlayer)
    
elseif action == 'body_search' then

    TriggerServerEvent('esx_policejob:message', GetPlayerServerId(closestPlayer), _U('being_searched'))
elseif.... 

# Nu ska du lägga till detta i din server main.lua

RegisterServerEvent('esx_ambulancejob:revive')
AddEventHandler('esx_ambulancejob:revive', function(target)
  TriggerClientEvent('esx_ambulancejob:revive', target)
end)

# Sen lägger du till en av de viktigaste sakerna i locales.lua

--Revive
['revive player'] = 'återuppliva spelare',

['revive_inprogress'] = 'återupplivning pågår',

['revive_complete'] = 'återupplivning klar',

['isdead'] = 'Spelare död,

##### ##### ##### ##### ##### ##### ##### ##### ##### ##### 

##### Sen så får du ändra allt om du vill ;)
##### Det kanske finns lite problem men då hoppas jag att ni löser det :)

Nu ska jag även säga tack till !Kepapi!

