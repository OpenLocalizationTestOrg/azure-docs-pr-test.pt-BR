<span data-ttu-id="78886-101">Criar um [aplicativo web](../articles/app-service-web/app-service-web-overview.md) em Olá `myAppServicePlan` plano de serviço de aplicativo com hello [az webapp criar](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="78886-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="78886-102">Olá web app fornece um espaço de hospedagem para o seu código e fornece um aplicativo do URL tooview Olá implantado.</span><span class="sxs-lookup"><span data-stu-id="78886-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="78886-103">Olá a seguir de comando, substitua  *\<app_name >* com um nome exclusivo (caracteres válidos são `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="78886-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="78886-104">Se `<app_name>` for não exclusivo, você obter mensagem de erro hello "Site com determinado nome < app_name > já existe".</span><span class="sxs-lookup"><span data-stu-id="78886-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="78886-105">Olá URL do aplicativo web de saudação padrão é `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="78886-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="78886-106">Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="78886-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="78886-107">Procure toohello site toosee seu aplicativo web criado recentemente.</span><span class="sxs-lookup"><span data-stu-id="78886-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
