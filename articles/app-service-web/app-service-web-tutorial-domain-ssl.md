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
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="27a0e-104">Adicionar domínio personalizado e o aplicativo de web do Azure tooan SSL</span><span class="sxs-lookup"><span data-stu-id="27a0e-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="27a0e-105">Este tutorial mostra como tooquickly mapear um aplicativo web do Azure de tooyour de nome de domínio personalizado e, em seguida, protegê-lo com um certificado SSL personalizado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="27a0e-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="27a0e-106">Before you begin</span></span>

<span data-ttu-id="27a0e-107">Antes de executar este exemplo, instalar Olá [2.0 do CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.</span><span class="sxs-lookup"><span data-stu-id="27a0e-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="27a0e-108">Você também precisa página de configuração do acesso administrativo toohello DNS para o seu provedor do respectivos domínios.</span><span class="sxs-lookup"><span data-stu-id="27a0e-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="27a0e-109">Por exemplo, tooadd `www.contoso.com`, você precisa toobe tooconfigure capaz de entradas DNS para `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="27a0e-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="27a0e-110">Por fim, é necessário um válido. Arquivo PFX _e_ sua senha para certificado SSL Olá deseja tooupload e estabeleça uma ligação.</span><span class="sxs-lookup"><span data-stu-id="27a0e-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="27a0e-111">Esse certificado SSL deve ser o nome de domínio personalizado de saudação configurado toosecure desejado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="27a0e-112">Em Olá exemplo acima, o certificado SSL deve proteger `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="27a0e-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="27a0e-113">Etapa 1 - Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="27a0e-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="27a0e-114">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="27a0e-114">Log in tooAzure</span></span>

<span data-ttu-id="27a0e-115">Estamos agora vai toouse Olá 2.0 do CLI do Azure em um terminal toocreate Olá recursos necessário toohost nosso aplicativo Node.js no Azure.</span><span class="sxs-lookup"><span data-stu-id="27a0e-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="27a0e-116">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="27a0e-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="27a0e-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="27a0e-117">Create a resource group</span></span>   
<span data-ttu-id="27a0e-118">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="27a0e-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="27a0e-119">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos Web, bancos de dados e contas de armazenamento, são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="27a0e-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="27a0e-120">toosee quais possíveis valores que você podem usar para `---location`, use Olá `az appservice list-locations` comando CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="27a0e-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="27a0e-121">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="27a0e-121">Create an App Service plan</span></span>

<span data-ttu-id="27a0e-122">Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="27a0e-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="27a0e-123">Olá, exemplo a seguir cria um plano de serviço de aplicativo chamado `myAppServicePlan` usando Olá **básica** preço.</span><span class="sxs-lookup"><span data-stu-id="27a0e-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="27a0e-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="27a0e-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="27a0e-125">Quando Olá plano de serviço de aplicativo tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="27a0e-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="27a0e-126">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="27a0e-126">Create a web app</span></span>

<span data-ttu-id="27a0e-127">Agora que foi criado um plano de serviço de aplicativo, criar um aplicativo web em Olá `myAppServicePlan` plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27a0e-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="27a0e-128">Fornece de aplicativo de web Hello você estiver uma hospedagem toodeploy de espaço em seu código, bem como fornece uma URL para você Olá tooview aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="27a0e-129">Saudação de uso [web do serviço de aplicativo az criar](/cli/azure/appservice/web#create) comando toocreate Olá web app.</span><span class="sxs-lookup"><span data-stu-id="27a0e-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="27a0e-130">O comando Olá abaixo, substitua por seu próprio nome exclusivo do aplicativo onde você pode ver Olá `<app_name>` espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="27a0e-131">Esse nome exclusivo será usado como parte de Olá Olá padrão do nome de domínio de aplicativo da web hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="27a0e-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="27a0e-132">Posteriormente, você pode mapear qualquer entrada DNS personalizado, toohello aplicativo da web antes de você expor tooyour usuários.</span><span class="sxs-lookup"><span data-stu-id="27a0e-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="27a0e-133">Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="27a0e-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

<span data-ttu-id="27a0e-134">De saudação saída JSON, `defaultHostName` mostra o nome do domínio do seu aplicativo web padrão.</span><span class="sxs-lookup"><span data-stu-id="27a0e-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="27a0e-135">No seu navegador, navegue toothis endereço.</span><span class="sxs-lookup"><span data-stu-id="27a0e-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="27a0e-137">Etapa 2 - Configurar o mapeamento DNS</span><span class="sxs-lookup"><span data-stu-id="27a0e-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="27a0e-138">Nesta etapa, você adiciona um mapeamento de nome de domínio padrão do aplicativo um domínio personalizado tooyour da web, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="27a0e-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="27a0e-139">Normalmente, você executa essa etapa no site do provedor de domínio.</span><span class="sxs-lookup"><span data-stu-id="27a0e-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="27a0e-140">Cada site do registrador de domínio é um pouco diferente, portanto, você deve consultar a documentação do provedor.</span><span class="sxs-lookup"><span data-stu-id="27a0e-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="27a0e-141">Estas são algumas diretrizes gerais.</span><span class="sxs-lookup"><span data-stu-id="27a0e-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="27a0e-142">Navegue tootooDNS página de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="27a0e-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="27a0e-143">Primeiro, faça logon no site do registrador de domínio tooyour.</span><span class="sxs-lookup"><span data-stu-id="27a0e-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="27a0e-144">Em seguida, localize a página de saudação para gerenciar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="27a0e-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="27a0e-145">Procure links ou áreas do site Olá rotulada **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="27a0e-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="27a0e-146">Geralmente, você pode encontrar o link de saudação exibindo as informações da conta e, em seguida, procurando, como um link **Meus domínios**.</span><span class="sxs-lookup"><span data-stu-id="27a0e-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="27a0e-147">Quando encontrar a página, procure por um link que permita adicionar ou editar os registros DNS.</span><span class="sxs-lookup"><span data-stu-id="27a0e-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="27a0e-148">Pode ser um **Arquivo de zona**, link de **Registros DNS** ou um link de configuração **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="27a0e-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="27a0e-149">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="27a0e-149">Create a CNAME record</span></span>

<span data-ttu-id="27a0e-150">Adicionar um registro CNAME que mapeia o nome de domínio padrão do aplicativo do web tooyour nome hello subdomínio desejado (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome exclusivo do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="27a0e-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="27a0e-151">Para Olá `www.contoso.com` exemplo, criar um CNAME que mapeia Olá `www` hostname muito`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="27a0e-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="27a0e-152">Etapa 3 – configurar o domínio personalizado Olá em seu aplicativo web</span><span class="sxs-lookup"><span data-stu-id="27a0e-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="27a0e-153">Quando você terminar de configurar o mapeamento de nome de host Olá no site do provedor de domínio, você está domínio personalizado de saudação tooconfigure pronto em seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="27a0e-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="27a0e-154">Saudação de uso [az serviço de aplicativo web configuração hostname adicionar](/cli/azure/appservice/web/config/hostname#add) comando tooadd essa configuração.</span><span class="sxs-lookup"><span data-stu-id="27a0e-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="27a0e-155">O comando Olá abaixo, substitua `<app_name>` com seu nome de aplicativo exclusivo e < your_custom_domain > com nome de domínio totalmente qualificado de personalizado de saudação (por exemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="27a0e-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="27a0e-156">domínio personalizado Olá agora é totalmente mapeado tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="27a0e-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="27a0e-157">No seu navegador, navegue toohello nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="27a0e-158">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="27a0e-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="27a0e-160">Etapa 4: associar um certificado SSL personalizado, tooyour aplicativo da web</span><span class="sxs-lookup"><span data-stu-id="27a0e-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="27a0e-161">Agora você tem um aplicativo web do Azure, com nome de domínio de saudação desejado na barra de endereços do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="27a0e-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="27a0e-162">No entanto, se você navegar toohello `https://<your_custom_domain>` agora, você não receberá um erro de certificado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="27a0e-164">Esse erro ocorre porque seu aplicativo Web ainda não possui uma associação de certificado SSL que corresponda ao nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="27a0e-165">No entanto, você não obterá um erro se você navegar muito`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="27a0e-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="27a0e-166">Isso ocorre porque o seu aplicativo, bem como todos os aplicativos de serviço de aplicativo do Azure, é protegida com certificado SSL Olá Olá `*.azurewebsites.net` domínio curinga por padrão.</span><span class="sxs-lookup"><span data-stu-id="27a0e-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="27a0e-167">Em ordem tooaccess seu aplicativo web pelo nome do seu domínio personalizado, é necessário certificado SSL toobind Olá para seu aplicativo de web toohello domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="27a0e-168">Você fará isso nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="27a0e-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="27a0e-169">Carregar certificado SSL Olá</span><span class="sxs-lookup"><span data-stu-id="27a0e-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="27a0e-170">Carregar certificado SSL Olá para seu aplicativo de web tooyour domínio personalizado usando Olá [carregamento de ssl az serviço de aplicativo web config](/cli/azure/appservice/web/config/ssl#upload) comando.</span><span class="sxs-lookup"><span data-stu-id="27a0e-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="27a0e-171">O comando Olá abaixo, substitua `<app_name>` com o nome exclusivo do aplicativo, `<path_to_ptx_file>` com hello tooyour de caminho. Arquivo PFX e `<password>` com a senha do certificado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="27a0e-172">Quando o certificado de saudação é carregado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a0e-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="27a0e-173">De saudação saída JSON, `thumbprint` mostra a impressão digital do certificado que o carregado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="27a0e-174">Copie seu valor para a próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a0e-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="27a0e-175">Associar o aplicativo web do hello carregado SSL certificado toohello</span><span class="sxs-lookup"><span data-stu-id="27a0e-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="27a0e-176">Seu aplicativo web agora tem o nome de domínio personalizado de saudação desejado, e ele também tem um certificado SSL que protege o domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="27a0e-177">Olá somente coisa toodo esquerdo é toobind Olá certificado carregado toohello web app.</span><span class="sxs-lookup"><span data-stu-id="27a0e-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="27a0e-178">Você pode fazer isso usando Olá [ligação ssl do az serviço de aplicativo web config](/cli/azure/appservice/web/config/ssl#bind) comando.</span><span class="sxs-lookup"><span data-stu-id="27a0e-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="27a0e-179">O comando Olá abaixo, substitua `<app_name>` com o nome exclusivo do aplicativo e `<thumbprint-from-previous-output>` com impressão digital de certificado Olá obter do comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="27a0e-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="27a0e-180">az appservice web config ssl bind --name <nome_do_aplicativo> --resource-group myResourceGroup --certificate-thumbprint <miniatura-da-saída-anterior> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="27a0e-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="27a0e-181">Quando o certificado de saudação está acoplado tooyour web app, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a0e-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="27a0e-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<nome_do_aplicativo>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<nome_do_aplicativo>.azurewebsites.net", "<nome_do_aplicativo>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<nome_do_aplicativo>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<nome_do_aplicativo>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<nome_do_aplicativo>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<nome_do_aplicativo>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="27a0e-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="27a0e-183">No seu navegador, navegue tooHTTPS de ponto de extremidade do seu nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="27a0e-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="27a0e-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="27a0e-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="27a0e-186">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="27a0e-186">More resources</span></span>

<span data-ttu-id="27a0e-187">[Comprar e configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](custom-dns-web-site-buydomains-web-app.md)
[Comprar e configurar um certificado SSL para o Serviço de Aplicativo do Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="27a0e-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
