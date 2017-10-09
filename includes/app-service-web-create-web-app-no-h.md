Criar um [aplicativo web](../articles/app-service-web/app-service-web-overview.md) em Olá `myAppServicePlan` plano de serviço de aplicativo com hello [az webapp criar](/cli/azure/webapp#create) comando. 

Olá web app fornece um espaço de hospedagem para o seu código e fornece um aplicativo do URL tooview Olá implantado.

Olá a seguir de comando, substitua  *\<app_name >* com um nome exclusivo (caracteres válidos são `a-z`, `0-9`, e `-`). Se `<app_name>` for não exclusivo, você obter mensagem de erro hello "Site com determinado nome < app_name > já existe". Olá URL do aplicativo web de saudação padrão é `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```

Procure toohello site toosee seu aplicativo web criado recentemente.

```bash
http://<app_name>.azurewebsites.net
```
