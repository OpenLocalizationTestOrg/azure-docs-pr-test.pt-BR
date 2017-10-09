Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Olá, exemplo a seguir cria um plano de serviço de aplicativo chamado `myAppServicePlan` em Olá **livre** preço:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Quando Olá plano de serviço de aplicativo tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```