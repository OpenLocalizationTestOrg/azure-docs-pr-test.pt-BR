---
title: "aaaCreate sua primeira função da saudação CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate do Azure a primeira função para a execução sem servidor usando Olá CLI do Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="49d66-103">Criar sua primeira função usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="49d66-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="49d66-104">Este tutorial de início rápido orienta como toouse toocreate de funções do Azure a primeira função.</span><span class="sxs-lookup"><span data-stu-id="49d66-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="49d66-105">Usar o hello CLI do Azure toocreate um aplicativo de função, que é Olá infraestrutura sem servidor que hospeda a função.</span><span class="sxs-lookup"><span data-stu-id="49d66-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="49d66-106">código de função Hello em si é implantado de um repositório de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="49d66-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="49d66-107">Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="49d66-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="49d66-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49d66-108">Prerequisites</span></span> 

<span data-ttu-id="49d66-109">Antes de executar este exemplo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="49d66-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="49d66-110">Uma conta do [GitHub](https://github.com) ativa.</span><span class="sxs-lookup"><span data-stu-id="49d66-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="49d66-111">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="49d66-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49d66-112">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="49d66-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="49d66-113">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="49d66-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49d66-114">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="49d66-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="49d66-115">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="49d66-115">Create a resource group</span></span>

<span data-ttu-id="49d66-116">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="49d66-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="49d66-117">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos de funções, bancos de dados e contas de armazenamento, são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="49d66-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="49d66-118">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="49d66-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="49d66-119">Se você não estiver usando o Cloud Shell, primeiro você deve entrar usando `az login`.</span><span class="sxs-lookup"><span data-stu-id="49d66-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="49d66-120">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="49d66-120">Create an Azure Storage account</span></span>

<span data-ttu-id="49d66-121">Funções usa um estado de toomaintain de conta de armazenamento do Azure e outras informações sobre suas funções.</span><span class="sxs-lookup"><span data-stu-id="49d66-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="49d66-122">Criar uma conta de armazenamento no grupo de recursos de saudação criado usando Olá [criar conta de armazenamento az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="49d66-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="49d66-123">Olá a seguir de comando, substitua seu próprio nome de conta de armazenamento exclusivo onde você pode ver Olá `<storage_name>` espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="49d66-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="49d66-124">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="49d66-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="49d66-125">Depois que tiver sido criada a conta de armazenamento hello, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="49d66-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a><span data-ttu-id="49d66-126">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="49d66-126">Create a function app</span></span>

<span data-ttu-id="49d66-127">Você deve ter uma função aplicativo toohost Olá a execução das funções.</span><span class="sxs-lookup"><span data-stu-id="49d66-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="49d66-128">Olá função aplicativo fornece um ambiente de execução sem servidor do seu código de função.</span><span class="sxs-lookup"><span data-stu-id="49d66-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="49d66-129">Ele permite que você agrupe funções como uma unidade lógica para facilitar o gerenciamento, a implantação e o compartilhamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="49d66-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="49d66-130">Criar um aplicativo de função usando Olá [functionapp az criar](/cli/azure/functionapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="49d66-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="49d66-131">Olá a seguir de comando, substitua seu próprio nome de aplicativo de função exclusiva onde você pode ver Olá `<app_name>` espaço reservado e hello nome de conta de armazenamento para `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="49d66-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="49d66-132">Olá `<app_name>` é usado como o domínio DNS à saudação padrão de saudação função aplicativo e o nome de saudação caso precisa toobe exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="49d66-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="49d66-133">Por padrão, um função de aplicativo é criado com hello consumo plano de hospedagem, que significa que os recursos são adicionados dinamicamente conforme exigido por funções, e você paga apenas quando funções estão em execução.</span><span class="sxs-lookup"><span data-stu-id="49d66-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="49d66-134">Para obter mais informações, consulte [plano de hospedagem correto escolha Olá](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="49d66-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="49d66-135">Após Olá função aplicativo foi criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="49d66-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="49d66-136">Agora que você tem um aplicativo de função, você pode implantar o código de função real de saudação do repositório de exemplo hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="49d66-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="49d66-137">Implantar o código de função</span><span class="sxs-lookup"><span data-stu-id="49d66-137">Deploy your function code</span></span>  

<span data-ttu-id="49d66-138">Há várias toocreate de maneiras seu código de função em seu novo aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="49d66-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="49d66-139">Este tópico se conecta tooa repositório de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="49d66-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="49d66-140">Como antes, Olá código a seguir substitua Olá `<app_name>` espaço reservado com o nome de saudação do aplicativo de função hello criado por você.</span><span class="sxs-lookup"><span data-stu-id="49d66-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="49d66-141">Após a implantação de saudação origem foi definido, Olá CLI do Azure mostra informações toohello semelhantes (valores nulos removidos para facilitar a leitura) de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="49d66-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a><span data-ttu-id="49d66-142">Função de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="49d66-142">Test hello function</span></span>

<span data-ttu-id="49d66-143">Use ondulação tootest Olá implantado função em um computador Mac ou Linux ou usando o Bash no Windows.</span><span class="sxs-lookup"><span data-stu-id="49d66-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="49d66-144">Executar Olá após a rotação de comando, substituindo Olá `<app_name>` espaço reservado com o nome de saudação do seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="49d66-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="49d66-145">Acrescente a cadeia de caracteres de consulta Olá `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="49d66-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Resposta de função mostrada em um navegador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="49d66-147">Se você não tiver ondulação disponível na linha de comando, digite Olá a mesma URL no endereço de saudação do navegador da web.</span><span class="sxs-lookup"><span data-stu-id="49d66-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="49d66-148">Novamente, substitua Olá `<app_name>` espaço reservado com o nome de saudação do seu aplicativo de função e acrescenta a cadeia de caracteres de consulta Olá `&name=<yourname>` toohello URL e executar a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="49d66-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Resposta de função mostrada em um navegador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="49d66-150">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="49d66-150">Clean up resources</span></span>

<span data-ttu-id="49d66-151">Outros inícios rápidos nessa coleção aproveitam esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="49d66-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="49d66-152">Se você planeja toocontinue toowork com tutoriais subsequentes ou com os tutoriais hello, faça não limpar os recursos de saudação criados neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="49d66-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="49d66-153">Se você não planeja toocontinue, use Olá toodelete de comando a seguir todos os recursos criados por este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="49d66-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="49d66-154">Quando solicitado, digite `y`.</span><span class="sxs-lookup"><span data-stu-id="49d66-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49d66-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49d66-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
