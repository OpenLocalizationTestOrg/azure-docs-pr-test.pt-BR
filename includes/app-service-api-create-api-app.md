
<span data-ttu-id="7a98c-101">Crie um [aplicativo de API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) no plano do Serviço de Aplicativo do `myAppServicePlan` com o comando [az webapp create](/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="7a98c-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="7a98c-102">O aplicativo Web fornece um espaço de hospedagem para sua API e fornece uma URL para exibir o aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="7a98c-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="7a98c-103">No comando a seguir, substitua *\<nome_do_aplicativo >* por um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="7a98c-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="7a98c-104">Se `<app_name>` não for exclusivo, você obterá a mensagem de erro "O site com o nome <nome_do_aplicativo> fornecido já existe."</span><span class="sxs-lookup"><span data-stu-id="7a98c-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="7a98c-105">A URL padrão do aplicativo Web é `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="7a98c-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="7a98c-106">Quando o aplicativo Web tiver sido criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a98c-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

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