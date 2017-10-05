---
title: Adicionar um nome personalizado e SSL a um aplicativo Web do Azure| Microsoft Docs
description: "Saiba como preparar seu aplicativo Web do Azure para entrar em produção adicionando a marca da sua empresa. Mapeie o nome de domínio personalizado para seu aplicativo Web e proteja-o com um certificado SSL personalizado."
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
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="5d337-104">Adicionar um nome personalizado e SSL a um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="5d337-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="5d337-105">Este tutorial mostra como mapear rapidamente um nome de domínio personalizado para seu aplicativo Web do Azure e, depois, protegê-lo com um certificado SSL personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d337-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5d337-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5d337-106">Before you begin</span></span>

<span data-ttu-id="5d337-107">Antes de executar este exemplo, instale a [CLI 2.0 do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.</span><span class="sxs-lookup"><span data-stu-id="5d337-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="5d337-108">Também é necessário acesso administrativo à página de configuração de DNS para seu respectivo provedor de domínio.</span><span class="sxs-lookup"><span data-stu-id="5d337-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="5d337-109">Por exemplo, para adicionar `www.contoso.com`, você precisa ser capaz de configurar entradas DNS para `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="5d337-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="5d337-110">Por fim, você precisa de um arquivo .PFX válido _e_ de sua senha para o certificado SSL que você deseja carregar e associar.</span><span class="sxs-lookup"><span data-stu-id="5d337-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="5d337-111">Esse certificado SSL deve ser configurado para proteger o nome de domínio personalizado que você deseja.</span><span class="sxs-lookup"><span data-stu-id="5d337-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="5d337-112">No exemplo acima, seu certificado SSL deve proteger `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="5d337-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="5d337-113">Etapa 1 - Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="5d337-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="5d337-114">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="5d337-114">Log in to Azure</span></span>

<span data-ttu-id="5d337-115">Agora, usaremos a CLI 2.0 do Azure em uma janela do terminal para criar os recursos necessários para hospedar nosso aplicativo Node.js no Azure.</span><span class="sxs-lookup"><span data-stu-id="5d337-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="5d337-116">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="5d337-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="5d337-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5d337-117">Create a resource group</span></span>   
<span data-ttu-id="5d337-118">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5d337-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5d337-119">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos Web, bancos de dados e contas de armazenamento, são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5d337-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="5d337-120">Para ver quais são os valores possíveis para `---location`, use o comando `az appservice list-locations` da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d337-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="5d337-121">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d337-121">Create an App Service plan</span></span>

<span data-ttu-id="5d337-122">Criar um plano do Serviço de Aplicativo com o comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="5d337-122">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="5d337-123">O exemplo a seguir cria um Plano do Serviço de Aplicativo denominado `myAppServicePlan` usando o tipo de preço **Basic**.</span><span class="sxs-lookup"><span data-stu-id="5d337-123">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="5d337-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="5d337-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="5d337-125">Quando o Plano do Serviço de Aplicativo for criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5d337-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="5d337-126">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5d337-126">Create a web app</span></span>

<span data-ttu-id="5d337-127">Agora que um Plano do Serviço de Aplicativo foi criado, crie um Aplicativo Web no Plano do Serviço de Aplicativo `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="5d337-127">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="5d337-128">O aplicativo Web fornece um espaço de hospedagem para implantar seu código, bem como uma URL para exibir o aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="5d337-128">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="5d337-129">Use o comando [az appservice web create](/cli/azure/appservice/web#create) para criar o Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="5d337-129">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="5d337-130">No comando abaixo, substitua o espaço reservado `<app_name>` por seu próprio nome exclusivo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d337-130">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="5d337-131">O nome exclusivo será usado como a parte do nome de domínio padrão para o aplicativo Web, portanto, o nome deve ser exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="5d337-131">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="5d337-132">Posteriormente, você poderá mapear qualquer entrada DNS personalizada para o aplicativo Web antes de expor para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="5d337-132">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="5d337-133">Quando o aplicativo Web tiver sido criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5d337-133">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

<span data-ttu-id="5d337-134">Na saída JSON, `defaultHostName` mostra o nome de domínio padrão de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="5d337-134">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="5d337-135">Em seu navegador, navegue até este endereço.</span><span class="sxs-lookup"><span data-stu-id="5d337-135">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="5d337-137">Etapa 2 - Configurar o mapeamento DNS</span><span class="sxs-lookup"><span data-stu-id="5d337-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="5d337-138">Nesta etapa, você adiciona um mapeamento de um domínio personalizado para o nome de domínio padrão de seu aplicativo Web, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5d337-138">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="5d337-139">Normalmente, você executa essa etapa no site do provedor de domínio.</span><span class="sxs-lookup"><span data-stu-id="5d337-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="5d337-140">Cada site do registrador de domínio é um pouco diferente, portanto, você deve consultar a documentação do provedor.</span><span class="sxs-lookup"><span data-stu-id="5d337-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="5d337-141">Estas são algumas diretrizes gerais.</span><span class="sxs-lookup"><span data-stu-id="5d337-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="5d337-142">Navegue até a página de gerenciamento do DNS</span><span class="sxs-lookup"><span data-stu-id="5d337-142">Navigate to to DNS management page</span></span>

<span data-ttu-id="5d337-143">Primeiro, faça logon no site do registrador de domínio.</span><span class="sxs-lookup"><span data-stu-id="5d337-143">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="5d337-144">Depois, localize a página para gerenciar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="5d337-144">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="5d337-145">Procure links ou áreas do site rotuladas como **Nome de domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.</span><span class="sxs-lookup"><span data-stu-id="5d337-145">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="5d337-146">Normalmente, você pode encontrar o link exibindo as informações de conta e procurando um link como **Meus domínios**.</span><span class="sxs-lookup"><span data-stu-id="5d337-146">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="5d337-147">Quando encontrar a página, procure por um link que permita adicionar ou editar os registros DNS.</span><span class="sxs-lookup"><span data-stu-id="5d337-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="5d337-148">Pode ser um **Arquivo de zona**, link de **Registros DNS** ou um link de configuração **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="5d337-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="5d337-149">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="5d337-149">Create a CNAME record</span></span>

<span data-ttu-id="5d337-150">Adicione um registro CNAME que mapeie o nome de subdomínio desejado para o nome de domínio padrão de seu aplicativo Web (`<app_name>.azurewebsites.net`, em que `<app_name>` é o nome exclusivo do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="5d337-150">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="5d337-151">Para o exemplo `www.contoso.com`, crie um CNAME que mapeie o nome de host `www` para `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5d337-151">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="5d337-152">Etapa 3 - Configurar o domínio personalizado em seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5d337-152">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="5d337-153">Quando você terminar de configurar o mapeamento do nome de host no site do provedor de domínio, você estará pronto para configurar o domínio personalizado em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="5d337-153">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="5d337-154">Use o comando [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) para adicionar essa configuração.</span><span class="sxs-lookup"><span data-stu-id="5d337-154">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="5d337-155">No comando a seguir, substitua `<app_name>` pelo nome exclusivo de seu aplicativo, e <nome_do_seu_domínio> pelo nome de domínio personalizado totalmente qualificado (por exemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="5d337-155">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="5d337-156">O domínio personalizado agora está totalmente mapeado para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="5d337-156">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="5d337-157">Em seu navegador, navegue até o nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d337-157">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="5d337-158">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5d337-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="5d337-160">Etapa 4 - Associar um certificado SSL personalizado ao seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5d337-160">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="5d337-161">Agora você tem um aplicativo Web, com o nome de domínio desejado na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="5d337-161">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="5d337-162">No entanto, se você navegar até `https://<your_custom_domain>`, receberá um erro de certificado.</span><span class="sxs-lookup"><span data-stu-id="5d337-162">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="5d337-164">Esse erro ocorre porque seu aplicativo Web ainda não possui uma associação de certificado SSL que corresponda ao nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d337-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="5d337-165">No entanto, você não receberá um erro se navegar até `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5d337-165">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="5d337-166">Isso porque seu aplicativo, bem como todos os aplicativos do Serviço de Aplicativo do Azure, são protegidos com o certificado SSL para o domínio curinga `*.azurewebsites.net` por padrão.</span><span class="sxs-lookup"><span data-stu-id="5d337-166">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="5d337-167">Para acessar seu aplicativo Web pelo nome de seu domínio personalizado, associe o certificado SSL de seu domínio personalizado ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="5d337-167">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="5d337-168">Você fará isso nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="5d337-168">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="5d337-169">Carregar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="5d337-169">Upload the SSL certificate</span></span>

<span data-ttu-id="5d337-170">Carregue o certificado SSL de seu domínio personalizado em seu aplicativo Web usando o comando [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload).</span><span class="sxs-lookup"><span data-stu-id="5d337-170">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="5d337-171">No comando a seguir, substitua `<app_name>` pelo nome de seu aplicativo exclusivo, `<path_to_ptx_file>` pelo caminho até o arquivo .PFX e `<password>` pela senha do certificado.</span><span class="sxs-lookup"><span data-stu-id="5d337-171">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="5d337-172">Após o carregamento do certificado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d337-172">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="5d337-173">Na saída JSON, `thumbprint` mostra a impressão digital do certificado carregado.</span><span class="sxs-lookup"><span data-stu-id="5d337-173">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="5d337-174">Copie esse valor para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="5d337-174">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="5d337-175">Associar o certificado SSL carregado ao aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5d337-175">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="5d337-176">Agora, seu aplicativo Web tem o nome de domínio personalizado que você deseja, e também tem um certificado SSL que protege esse domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d337-176">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="5d337-177">Agora só resta associar o certificado carregado ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="5d337-177">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="5d337-178">Faça isso usando o comando [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind).</span><span class="sxs-lookup"><span data-stu-id="5d337-178">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="5d337-179">No comando a seguir, substitua `<app_name>` pelo nome exclusivo do aplicativo e `<thumbprint-from-previous-output>` pela impressão digital do certificado que você obteve com o comando anterior.</span><span class="sxs-lookup"><span data-stu-id="5d337-179">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="5d337-180">az appservice web config ssl bind --name <nome_do_aplicativo> --resource-group myResourceGroup --certificate-thumbprint <miniatura-da-saída-anterior> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="5d337-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="5d337-181">Após a associação do certificado ao seu aplicativo Web, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d337-181">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="5d337-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<nome_do_aplicativo>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<nome_do_aplicativo>.azurewebsites.net", "<nome_do_aplicativo>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<nome_do_aplicativo>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<nome_do_aplicativo>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<nome_do_aplicativo>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<nome_do_aplicativo>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="5d337-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="5d337-183">Em seu navegador, navegue até o ponto de extremidade HTTPS de seu nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d337-183">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="5d337-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5d337-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="5d337-186">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="5d337-186">More resources</span></span>

<span data-ttu-id="5d337-187">[Comprar e configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](custom-dns-web-site-buydomains-web-app.md)
[Comprar e configurar um certificado SSL para o Serviço de Aplicativo do Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="5d337-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
