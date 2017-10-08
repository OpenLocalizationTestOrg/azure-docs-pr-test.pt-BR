---
title: "aplicativo da web SSL tooan do Azure e domínio personalizado aaaAdd | Microsoft Docs"
description: "Saiba como tooprepare do Azure web produção do aplicativo toogo adicionando sua identidade visual da empresa. Mapeie o aplicativo de web tooyour do (domínio banido) de nome de domínio personalizado Olá e protegê-lo com um certificado SSL personalizado."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Adicionar domínio personalizado e o aplicativo de web do Azure tooan SSL

Este tutorial mostra como tooquickly mapear um aplicativo web do Azure de tooyour de nome de domínio personalizado e, em seguida, protegê-lo com um certificado SSL personalizado. 

## <a name="before-you-begin"></a>Antes de começar

Antes de executar este exemplo, instalar Olá [2.0 do CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.

Você também precisa página de configuração do acesso administrativo toohello DNS para o seu provedor do respectivos domínios. Por exemplo, tooadd `www.contoso.com`, você precisa toobe tooconfigure capaz de entradas DNS para `contoso.com`.

Por fim, é necessário um válido. Arquivo PFX _e_ sua senha para certificado SSL Olá deseja tooupload e estabeleça uma ligação. Esse certificado SSL deve ser o nome de domínio personalizado de saudação configurado toosecure desejado. Em Olá exemplo acima, o certificado SSL deve proteger `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Etapa 1 - Criar um aplicativo Web do Azure

### <a name="log-in-tooazure"></a>Faça logon no tooAzure

Estamos agora vai toouse Olá 2.0 do CLI do Azure em um terminal toocreate Olá recursos necessário toohost nosso aplicativo Node.js no Azure.  Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Criar um grupo de recursos   
Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create). Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos Web, bancos de dados e contas de armazenamento, são implantados e gerenciados. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee quais possíveis valores que você podem usar para `---location`, use Olá `az appservice list-locations` comando CLI do Azure.

## <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Olá, exemplo a seguir cria um plano de serviço de aplicativo chamado `myAppServicePlan` usando Olá **básica** preço.

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

Quando Olá plano de serviço de aplicativo tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Criar um aplicativo Web

Agora que foi criado um plano de serviço de aplicativo, criar um aplicativo web em Olá `myAppServicePlan` plano de serviço de aplicativo. Fornece de aplicativo de web Hello você estiver uma hospedagem toodeploy de espaço em seu código, bem como fornece uma URL para você Olá tooview aplicativo implantado. Saudação de uso [web do serviço de aplicativo az criar](/cli/azure/appservice/web#create) comando toocreate Olá web app. 

O comando Olá abaixo, substitua por seu próprio nome exclusivo do aplicativo onde você pode ver Olá `<app_name>` espaço reservado. Esse nome exclusivo será usado como parte de Olá Olá padrão do nome de domínio de aplicativo da web hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no Azure. Posteriormente, você pode mapear qualquer entrada DNS personalizado, toohello aplicativo da web antes de você expor tooyour usuários. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

De saudação saída JSON, `defaultHostName` mostra o nome do domínio do seu aplicativo web padrão. No seu navegador, navegue toothis endereço.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Etapa 2 - Configurar o mapeamento DNS

Nesta etapa, você adiciona um mapeamento de nome de domínio padrão do aplicativo um domínio personalizado tooyour da web, `<app_name>.azurewebsites.net`. Normalmente, você executa essa etapa no site do provedor de domínio. Cada site do registrador de domínio é um pouco diferente, portanto, você deve consultar a documentação do provedor. Estas são algumas diretrizes gerais. 

### <a name="navigate-tootoodns-management-page"></a>Navegue tootooDNS página de gerenciamento

Primeiro, faça logon no site do registrador de domínio tooyour.  

Em seguida, localize a página de saudação para gerenciar registros DNS. Procure links ou áreas do site Olá rotulada **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**. Geralmente, você pode encontrar o link de saudação exibindo as informações da conta e, em seguida, procurando, como um link **Meus domínios**.

Quando encontrar a página, procure por um link que permita adicionar ou editar os registros DNS. Pode ser um **Arquivo de zona**, link de **Registros DNS** ou um link de configuração **Avançado**.

### <a name="create-a-cname-record"></a>Criar um registro CNAME

Adicionar um registro CNAME que mapeia o nome de domínio padrão do aplicativo do web tooyour nome hello subdomínio desejado (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome exclusivo do aplicativo).

Para Olá `www.contoso.com` exemplo, criar um CNAME que mapeia Olá `www` hostname muito`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Etapa 3 – configurar o domínio personalizado Olá em seu aplicativo web

Quando você terminar de configurar o mapeamento de nome de host Olá no site do provedor de domínio, você está domínio personalizado de saudação tooconfigure pronto em seu aplicativo web. Saudação de uso [az serviço de aplicativo web configuração hostname adicionar](/cli/azure/appservice/web/config/hostname#add) comando tooadd essa configuração. 

O comando Olá abaixo, substitua `<app_name>` com seu nome de aplicativo exclusivo e < your_custom_domain > com nome de domínio totalmente qualificado de personalizado de saudação (por exemplo, `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

domínio personalizado Olá agora é totalmente mapeado tooyour web app. No seu navegador, navegue toohello nome de domínio personalizado. Por exemplo:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Etapa 4: associar um certificado SSL personalizado, tooyour aplicativo da web

Agora você tem um aplicativo web do Azure, com nome de domínio de saudação desejado na barra de endereços do navegador hello. No entanto, se você navegar toohello `https://<your_custom_domain>` agora, você não receberá um erro de certificado. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Esse erro ocorre porque seu aplicativo Web ainda não possui uma associação de certificado SSL que corresponda ao nome de domínio personalizado. No entanto, você não obterá um erro se você navegar muito`https://<app_name>.azurewebsites.net`. Isso ocorre porque o seu aplicativo, bem como todos os aplicativos de serviço de aplicativo do Azure, é protegida com certificado SSL Olá Olá `*.azurewebsites.net` domínio curinga por padrão. 

Em ordem tooaccess seu aplicativo web pelo nome do seu domínio personalizado, é necessário certificado SSL toobind Olá para seu aplicativo de web toohello domínio personalizado. Você fará isso nesta etapa. 

### <a name="upload-hello-ssl-certificate"></a>Carregar certificado SSL Olá

Carregar certificado SSL Olá para seu aplicativo de web tooyour domínio personalizado usando Olá [carregamento de ssl az serviço de aplicativo web config](/cli/azure/appservice/web/config/ssl#upload) comando.

O comando Olá abaixo, substitua `<app_name>` com o nome exclusivo do aplicativo, `<path_to_ptx_file>` com hello tooyour de caminho. Arquivo PFX e `<password>` com a senha do certificado. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Quando o certificado de saudação é carregado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

De saudação saída JSON, `thumbprint` mostra a impressão digital do certificado que o carregado. Copie seu valor para a próxima etapa de saudação.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Associar o aplicativo web do hello carregado SSL certificado toohello

Seu aplicativo web agora tem o nome de domínio personalizado de saudação desejado, e ele também tem um certificado SSL que protege o domínio personalizado. Olá somente coisa toodo esquerdo é toobind Olá certificado carregado toohello web app. Você pode fazer isso usando Olá [ligação ssl do az serviço de aplicativo web config](/cli/azure/appservice/web/config/ssl#bind) comando.

O comando Olá abaixo, substitua `<app_name>` com o nome exclusivo do aplicativo e `<thumbprint-from-previous-output>` com impressão digital de certificado Olá obter do comando anterior hello. 

az appservice web config ssl bind --name <nome_do_aplicativo> --resource-group myResourceGroup --certificate-thumbprint <miniatura-da-saída-anterior> --ssl-type SNI

Quando o certificado de saudação está acoplado tooyour web app, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<nome_do_aplicativo>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<nome_do_aplicativo>.azurewebsites.net", "<nome_do_aplicativo>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<nome_do_aplicativo>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<nome_do_aplicativo>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<nome_do_aplicativo>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<nome_do_aplicativo>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

No seu navegador, navegue tooHTTPS de ponto de extremidade do seu nome de domínio personalizado. Por exemplo:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Mais recursos

[Comprar e configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](custom-dns-web-site-buydomains-web-app.md)
[Comprar e configurar um certificado SSL para o Serviço de Aplicativo do Azure](web-sites-purchase-ssl-web-site.md)
