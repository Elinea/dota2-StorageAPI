#Storage API
######Storage API interface to store data for Dota 2 Custom Game players.
	
##How to setup
- Clone or download the `storageapi` folder into your addon's `vscript` folder
- Get API key from `http://dota2.tools/api/v1/storage/createApiKey?game=<Name of your custom game>&author=<Your name>` or make your own server receiver and edit `STORAGEAPI_API_URL` in `storage.lua`
- Check info on server responses at the bottom of this readme if you decide to build your own reciever

##Usage

```lua
require('storageapi/json')
require('storageapi/storage')

Storage:SetApiKey(api_key)

Storage:put( steam_id, data, function( resultTable, successBool )
	if successBool then
		print("Successfully put data in storage")
	end
end)

Storage:get( steam_id, function( resultTable, successBool )
	if successBool then
		DeepPrintTable(resultTable)
	end
end)
```

##Testing
`GET: STORAGEAPI_API_URL?api_key=<api_key>&steam_id=<steam_id>`

`PUT (POST): STORAGEAPI_API_URL?api_key=<api_key>&steam_id=<steam_id>&data=<json>`

##Server

`GET` with query string `api_key=<api_key>&steam_id=<steam_id>` should return
```json
{
	"data": {
		"api_key": string,
		"steam_id": string,
		"data": {
			json_object
		}
	}
}
```
`POST` with query string `api_key=<api_key>&steam_id=<steam_id>&data=<json>` should return
```json
{
  "data": {
    "success": true
  }
}
```

Errors should return
```json
{
  "errors": {
    "error_code": int,
    "message": string
  }
}
```