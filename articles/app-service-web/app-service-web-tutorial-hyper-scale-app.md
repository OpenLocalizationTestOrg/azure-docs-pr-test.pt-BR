---
title: aaaBuild um aplicativo de hyper-escala no Azure | Microsoft Docs
description: "Saiba como toouse diferentes serviços do Azure toomaximize Olá desempenho de um aplicativo ASP.NET no Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Criar um aplicativo Web de hiperescala no Azure

Este tutorial mostra como tooscale-out de um aplicativo da web ASP.NET no Azure toomaximize usuário solicita.

Antes de iniciar este tutorial, certifique-se de que [Olá CLI do Azure está instalado](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) em seu computador. Além disso, você precisa [Visual Studio](https://www.visualstudio.com/vs/) em seu aplicativo de amostra do computador local toorun hello.

## <a name="step-1---get-sample-application"></a>Etapa 1 – Obter aplicativo de exemplo
Nesta etapa, você configura o local do projeto ASP.NET Olá.

### <a name="clone-hello-application-repository"></a>Repositório de aplicativo de saudação do clone

Terminal de linha de comando Olá aberto de sua escolha e `CD` tooa diretório de trabalho. Em seguida, seguir Olá execução comandos aplicativo de exemplo hello tooclone. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Executar o aplicativo de exemplo hello no Visual Studio

Abra a solução de saudação no Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Tipo `F5` toorun aplicativo de hello.

Este aplicativo de web do ASP.NET de exemplo vem de modelo de padrão de saudação e persiste o cache de saída de saudação de sessões e usos de usuário. Observe `HighScaleApp\Controllers\HomeController.cs`. Olá `Index()` método adiciona uma parte da sessão de toohello de dados.

```csharp
Session.Add("visited", "true"); 
```

E hello `About()` e `Contact()` sua saída de cache de métodos.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Etapa 2: implantar tooAzure
Nesta etapa, você cria um aplicativo web do Azure e implanta seu tooit de aplicativo do ASP.NET de exemplo.

### <a name="create-a-resource-group"></a>Criar um grupo de recursos   
Use [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) toocreate um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) na região Europa Ocidental de saudação. Um grupo de recursos é onde você coloca todos os Olá recursos do Azure que você deseja toomanage juntos, como Olá web app e qualquer banco de dados SQL back-end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee quais possíveis valores que você podem usar para `---location`, use Olá [locais de lista do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) comando.

### <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo
Use [criar plano de serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Um plano de serviço de aplicativo é uma unidade de escala, o que pode incluir qualquer número de aplicativos que você deseja tooscale backup ou out junto over Olá mesmo infraestrutura de serviço de aplicativo. Cada plano também recebe um [tipo de preço](https://azure.microsoft.com/en-us/pricing/details/app-service/). Tipos mais alto incluem hardware melhor e mais recursos, como mais instâncias de escala horizontal.

Para este tutorial, B1 é Olá mínimo de camada que permite que instâncias toothree em expansão. Você sempre pode mover seu aplicativo para cima ou para baixo Olá preço posteriormente, executando [atualização de plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Criar um aplicativo Web
Use [web do serviço de aplicativo az criar](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate um aplicativo web com um nome exclusivo no `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Definir credenciais de implantação
Use [usuário de implantação da web do serviço de aplicativo de az definido](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset credenciais de sua implantação do nível de conta de serviço de aplicativo.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Configurar a implantação do Git
Use [controle de origem de web do serviço de aplicativo de az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure implantação local do Git.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Esse comando fornece uma saída semelhante à seguinte hello:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Olá Use retornado URL tooconfigure o Git remoto. Olá comando a seguir usa Olá precede o exemplo de saída.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Implantar o aplicativo de exemplo hello
Você está agora pronto toodeploy o aplicativo de exemplo. Execute `git push`.

```powershell
git push azure master
```

Quando solicitado para a senha, use senha Olá que você especificou quando executou `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>Procurar o aplicativo web de tooAzure
Use [procurar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee seu aplicativo em execução no Azure, execute este comando.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Etapa 3 - conectar tooRedis
Nesta etapa, você configura o Cache Redis do Azure como um aplicativo de web do Azure tooyour cache externo e colocados. Você pode rapidamente utilizar toocache Redis a saída de página. Além disso, ao escalar horizontalmente os aplicativos Web posteriormente, o Redis ajuda a persistir as sessões do usuário em várias instâncias de modo confiável.

### <a name="create-an-azure-redis-cache"></a>Criar um Cache Redis do Azure
Use [redis az criar](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate um Azure Redis Cache e salvar Olá JSON de saída. Use um nome exclusivo em `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Configurar Olá aplicativo toouse Redis
Formato de cadeia de caracteres de conexão de saudação para seu cache.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

segunda linha de saudação deve fornecer uma saída parecida com esta:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

No Visual Studio, crie um arquivo de configuração da web em sua raiz de projeto chamado `redis.config` e colar Olá seguindo o código para ele. Em `value`, use a cadeia de conexão de saudação do hello saída do PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Se você observar Olá `.gitignore` arquivo no seu repositório Git, você verá que esse arquivo é excluído do controle de origem. Dessa forma, as informações confidenciais são mantidas em segurança. 

Abra `Web.config`. Saudação de aviso `<appSettings file="redis.config">` elemento, que obtém a configuração de saudação criado no `redis.config`. 

Localizar Olá comentado seção inclui `<sessionState>` e `<caching>`. Remova os comentários dessa seção.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Esse código procura por cadeia de caracteres de conexão de Redis Olá você definiu no `RedisConnection`. 

Seu aplicativo agora usa Redis toomanage sessões e armazenamento em cache. Tipo `F5` toorun aplicativo de hello. Se desejar, você pode baixar dados Olá um Redis gerenciamento cliente toovisualize agora salvo toohello cache.

### <a name="configure-hello-connection-string-in-azure"></a>Configurar a cadeia de caracteres de conexão Olá no Azure

Para toowork seu aplicativo no Azure, você precisa tooconfigure Olá a mesma cadeia de conexão do Redis em seu aplicativo web do Azure. Como `redis.config` é mantida no controle de origem, não é implantado tooAzure quando você executa a implantação do Git.

Use [az serviço de aplicativo web configuração appsettings atualizar](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) cadeia de conexão de saudação tooadd com hello mesmo nome (`RedisConnection`).

az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup

Lembre-se de que `$connstring` contém a cadeia de caracteres de conexão de saudação formatada.

### <a name="redeploy-hello-application-tooazure"></a>Reimplantar Olá aplicativo tooAzure
Use Git comandos toopush tooAzure suas alterações

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Quando solicitado para a senha, use senha Olá que você especificou quando executou `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Procurar o aplicativo web do Azure de toohello
Use [procurar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) alterações de saudação toosee ao vivo no Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Etapa 4 - instâncias de toomultiple de escala
Olá plano de serviço de aplicativo é a unidade de escala de saudação para seus aplicativos web do Azure. tooscale-out do seu aplicativo web, você dimensionar Olá plano de serviço de aplicativo.

Use [atualização de plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale as instâncias de toothree do plano do serviço de aplicativo hello, que é Olá número máximo permitido pelo Olá B1 preço. Lembre-se de que B1 é hello preço que você escolheu quando criou Olá anteriormente plano de serviço de aplicativo. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Etapa 5 – Escalar geograficamente
Ao dimensionar geograficamente, executar seu aplicativo em várias regiões de saudação nuvem do Azure. Esta instalação fornece balanceamento de carga seu aplicativo ainda mais com base na geografia e reduz o tempo de resposta de saudação colocando os navegadores tooclient mais próximos do aplicativo.

Nesta etapa, você dimensionar o ASP.NET web aplicativo tooa segunda região com [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). No final da saudação da etapa Olá, você terá um aplicativo web em execução na Europa Ocidental (já criado) e um aplicativo web em execução no sudeste da Ásia (ainda não foi criado). Ambos os aplicativos serão atendidos a partir Olá mesmo URL do Gerenciador de tráfego.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Dimensionar o hello da camada de tooStandard de aplicativo Europa
No serviço de aplicativo, integração com o Azure Traffic Manager requer saudação padrão de preço. Use [atualização de plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale backup seu tooS1 de plano de serviço de aplicativo. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego 
Use [criar perfil do Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate um Gerenciador de tráfego de perfil e adicioná-lo tooyour grupo de recursos. Use um nome DNS exclusivo em $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Especifica que este perfil [roteia a extremidade mais próxima do usuário tráfego toohello](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Obter a ID de recursos de saudação do aplicativo do hello Europa
Use [Mostrar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Olá ID de recurso de seu aplicativo web.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Adicionar um ponto de extremidade do Gerenciador de tráfego para o aplicativo de Europa Olá
Use [criar ponto de extremidade de Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd tooyour um ponto de extremidade perfil do Gerenciador de tráfego e uso Olá ID de recurso de seu aplicativo web como Olá destino.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Obter URL de ponto de extremidade do Traffic Manager Olá
Perfil do Traffic Manager agora tem um ponto de extremidade de aplicativo da web existente que pontos tooyour. Use [Mostrar de perfil de Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget sua URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Copie saída de hello no seu navegador. Você deve ver o aplicativo Web novamente.

### <a name="create-an-azure-redis-cache-in-asia"></a>Criar um Cache Redis do Azure na Ásia
Agora, você pode replicar sua região Sudeste da Ásia de toohello de aplicativo de web do Azure. toostart, use [redis az criar](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate um segundo Azure Redis Cache do Sudeste da Ásia. Esse cache precisa toobe posicionada com seu aplicativo na Ásia.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`Fornece Olá nome de saudação do cache de saudação cache Europa Ocidental, Olá `-asia` sufixo.

### <a name="create-an-app-service-plan-in-asia"></a>Criar um plano do Serviço de Aplicativo na Ásia
Use [criar plano de serviço de aplicativo az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate um segundo serviço de aplicativo planejar na região do Sudeste Asiático hello, usando Olá S1 mesmo nível como plano de Ocidental hello.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Criar um aplicativo Web na Ásia
Use [web do serviço de aplicativo az criar](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate um segundo aplicativo de web.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`Fornece Olá nome do aplicativo Olá Olá Ocidental aplicativo, com hello `-asia` sufixo.

### <a name="configure-hello-connection-string-for-redis"></a>Configurar a cadeia de caracteres de conexão Olá para Redis
Use [az serviço de aplicativo web configuração appsettings atualizar](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web aplicativo Olá conexão string hello cache Sudeste da Ásia.

az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Configure a implantação de Git para o aplicativo do hello Ásia.
Use [controle de origem de web do serviço de aplicativo de az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure implantação do Git local para o aplicativo web da segunda hello.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Esse comando fornece uma saída semelhante à seguinte hello:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Olá Use retornado tooconfigure URL uma segunda Git remoto para seu repositório local. Olá comando a seguir usa Olá precede o exemplo de saída.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Implantar o aplicativo de exemplo
Executar `git push` toodeploy exemplo aplicativo toohello segundo Git remoto. 

```bash
git push azure-asia master
```

Quando solicitado para a senha, use senha Olá que você especificou quando executou `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Procurar toohello Ásia aplicativo
Use [procurar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify que seu aplicativo está em execução ao vivo no Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Obter a ID de recursos de saudação do hello Ásia aplicativo
Use [Mostrar de web do serviço de aplicativo az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Olá ID de recurso de seu aplicativo web do Sudeste da Ásia.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Adicionar um ponto de extremidade do Gerenciador de tráfego para o aplicativo de Ásia Olá
Use [criar ponto de extremidade de Gerenciador de tráfego de rede az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd um segundo toohello de ponto de extremidade perfil do Traffic Manager.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Adicionar aplicativos de tooweb de identificador de região
Use [az serviço de aplicativo web configuração appsettings atualizar](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd uma variável de ambiente específicas da região.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

O código do seu aplicativo já usa essa configuração de aplicativo. Observe `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Concluído!

Agora, tente tooaccess Olá URL do seu perfil do Gerenciador de tráfego de navegadores em regiões geográficas diferentes. Os navegadores cliente da Europa devem mostrar "ASP.NET Europa Ocidental" e o navegador cliente da Ásia deve mostrar "ASP.NET Sudeste Asiático".

## <a name="more-resources"></a>Mais recursos
