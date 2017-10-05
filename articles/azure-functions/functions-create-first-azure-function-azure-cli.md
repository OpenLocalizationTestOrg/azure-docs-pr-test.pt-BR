---
title: "Criar sua primeira função na CLI do Azure | Microsoft Docs"
description: "Aprenda a criar sua primeira Função do Azure para a execução sem servidor usando a CLI do Azure."
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
ms.openlocfilehash: 8bd3e4bb7423db44c48b04f25edcf1074e6ea0bd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-the-azure-cli"></a><span data-ttu-id="3d868-103">Criar sua primeira função usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3d868-103">Create your first function using the Azure CLI</span></span>

<span data-ttu-id="3d868-104">Este tutorial de início rápido explica como usar o Azure Functions para criar sua primeira função.</span><span class="sxs-lookup"><span data-stu-id="3d868-104">This quickstart tutorial walks through how to use Azure Functions to create your first function.</span></span> <span data-ttu-id="3d868-105">É possível usar a CLI do Azure para criar um aplicativo de funções, que é a infraestrutura sem servidor que hospeda sua função.</span><span class="sxs-lookup"><span data-stu-id="3d868-105">You use the Azure CLI to create a function app, which is the serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="3d868-106">O código de função em si é implantado de um repositório de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="3d868-106">The function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="3d868-107">Você pode seguir as etapas abaixo usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="3d868-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3d868-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d868-108">Prerequisites</span></span> 

<span data-ttu-id="3d868-109">Antes de executar este exemplo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3d868-109">Before running this sample, you must have the following:</span></span>

+ <span data-ttu-id="3d868-110">Uma conta do [GitHub](https://github.com) ativa.</span><span class="sxs-lookup"><span data-stu-id="3d868-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="3d868-111">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d868-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3d868-112">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3d868-112">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3d868-113">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="3d868-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="3d868-114">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3d868-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="3d868-115">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3d868-115">Create a resource group</span></span>

<span data-ttu-id="3d868-116">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3d868-116">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3d868-117">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos de funções, bancos de dados e contas de armazenamento, são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3d868-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="3d868-118">O seguinte exemplo cria um grupo de recursos chamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3d868-118">The following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="3d868-119">Se você não estiver usando o Cloud Shell, primeiro você deve entrar usando `az login`.</span><span class="sxs-lookup"><span data-stu-id="3d868-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="3d868-120">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3d868-120">Create an Azure Storage account</span></span>

<span data-ttu-id="3d868-121">O Functions usa uma conta de Armazenamento do Azure para manter o estado e outras informações sobre suas funções.</span><span class="sxs-lookup"><span data-stu-id="3d868-121">Functions uses an Azure Storage account to maintain state and other information about your functions.</span></span> <span data-ttu-id="3d868-122">Crie uma conta de armazenamento no grupo de recursos que você criou ao utilizar o comando [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="3d868-122">Create a storage account in the resource group you created by using the [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="3d868-123">No seguinte comando, substitua seu próprio nome da conta de armazenamento globalmente exclusivo quando vir o espaço reservado `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="3d868-123">In the following command, substitute your own globally unique storage account name where you see the `<storage_name>` placeholder.</span></span> <span data-ttu-id="3d868-124">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3d868-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="3d868-125">Depois que a conta de armazenamento for criada, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d868-125">After the storage account has been created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="3d868-126">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="3d868-126">Create a function app</span></span>

<span data-ttu-id="3d868-127">Você deve ter um aplicativo de funções para hospedar a execução de suas funções.</span><span class="sxs-lookup"><span data-stu-id="3d868-127">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="3d868-128">O aplicativo de funções fornece um ambiente para execução sem servidor do seu código de função.</span><span class="sxs-lookup"><span data-stu-id="3d868-128">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="3d868-129">Ele permite que você agrupe funções como uma unidade lógica para facilitar o gerenciamento, a implantação e o compartilhamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d868-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="3d868-130">Crie um aplicativo de funções ao usar o comando [az functionapp create](/cli/azure/functionapp#create).</span><span class="sxs-lookup"><span data-stu-id="3d868-130">Create a function app by using the [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="3d868-131">No seguinte comando, substitua seu próprio nome de aplicativo de funções exclusivo quando vir o espaço reservado `<app_name>` e o nome da conta de armazenamento para `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="3d868-131">In the following command, substitute your own unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="3d868-132">O `<app_name>` é usado como domínio DNS padrão para o aplicativo de funções, portanto, o nome deve ser exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="3d868-132">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="3d868-133">Por padrão, um aplicativo de funções é criado com o Plano de hospedagem de consumo, o que significa que os recursos são adicionados dinamicamente, conforme exigido por suas funções e você paga apenas quando funções estão em execução.</span><span class="sxs-lookup"><span data-stu-id="3d868-133">By default, a function app is created with the Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="3d868-134">Para obter mais informações, consulte [Escolher o plano de hospedagem correto](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="3d868-134">For more information, see [Choose the correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="3d868-135">Depois que o aplicativo de funções for criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d868-135">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="3d868-136">Agora que você tem um aplicativo de funções, é possível implantar o código de função real do repositório GitHub de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3d868-136">Now that you have a function app, you can deploy the actual function code from the GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="3d868-137">Implantar o código de função</span><span class="sxs-lookup"><span data-stu-id="3d868-137">Deploy your function code</span></span>  

<span data-ttu-id="3d868-138">Há várias maneiras de criar o código de função no novo aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="3d868-138">There are several ways to create your function code in your new function app.</span></span> <span data-ttu-id="3d868-139">Este tópico se conecta a um repositório de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3d868-139">This topic connects to a sample repository in GitHub.</span></span> <span data-ttu-id="3d868-140">Assim como anteriormente, no código a seguir, substitua o espaço reservado `<app_name>` pelo nome do aplicativo de funções que você criou.</span><span class="sxs-lookup"><span data-stu-id="3d868-140">As before, in the following code replace the `<app_name>` placeholder with the name of the function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="3d868-141">Após a definição de fonte de implantação, a CLI do Azure mostra informações semelhantes ao exemplo a seguir (valores nulos removidos para facilitar a leitura):</span><span class="sxs-lookup"><span data-stu-id="3d868-141">After the deployment source been set, the Azure CLI shows information similar to the following example (null values removed for readability):</span></span>

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

## <a name="test-the-function"></a><span data-ttu-id="3d868-142">Testar a função</span><span class="sxs-lookup"><span data-stu-id="3d868-142">Test the function</span></span>

<span data-ttu-id="3d868-143">Use o cURL para testar a função implantada em um computador Mac ou Linux, ou usando Bash no Windows.</span><span class="sxs-lookup"><span data-stu-id="3d868-143">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="3d868-144">Execute o seguinte comando cURL, substituindo o espaço reservado `<app_name>` pelo nome do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="3d868-144">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span></span> <span data-ttu-id="3d868-145">Acrescente a cadeia de caracteres de consulta `&name=<yourname>` à URL.</span><span class="sxs-lookup"><span data-stu-id="3d868-145">Append the query string `&name=<yourname>` to the URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Resposta de função mostrada em um navegador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="3d868-147">Caso não tenha o cURL disponível na linha de comando, digite a mesma URL no endereço do seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="3d868-147">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span></span> <span data-ttu-id="3d868-148">Novamente, substitua o espaço reservado `<app_name>` pelo nome do aplicativo de funções, e acrescente a cadeia de consulta `&name=<yourname>` à URL e execute a solicitação.</span><span class="sxs-lookup"><span data-stu-id="3d868-148">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Resposta de função mostrada em um navegador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="3d868-150">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="3d868-150">Clean up resources</span></span>

<span data-ttu-id="3d868-151">Outros inícios rápidos nessa coleção aproveitam esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="3d868-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="3d868-152">Se você planeja continuar trabalhando com inícios rápidos subsequentes ou com os tutoriais, não limpe os recursos criados nesse início rápido.</span><span class="sxs-lookup"><span data-stu-id="3d868-152">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="3d868-153">Caso contrário, use os comandos a seguir para excluir todos os recursos criados por esse início rápido:</span><span class="sxs-lookup"><span data-stu-id="3d868-153">If you do not plan to continue, use the following command to delete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="3d868-154">Quando solicitado, digite `y`.</span><span class="sxs-lookup"><span data-stu-id="3d868-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d868-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d868-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
