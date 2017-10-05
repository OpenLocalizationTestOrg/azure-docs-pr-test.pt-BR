---
title: "Criar uma Função do Azure que se conecta a um armazenamento Azure | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Criar uma função do Azure que se conecta a um armazenamento Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="a4b9c-103">Integrar o Aplicativo de funções à conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a4b9c-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="a4b9c-104">Este exemplo de script cria um Aplicativo de funções e uma Conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a4b9c-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a4b9c-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a4b9c-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a4b9c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a4b9c-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="a4b9c-108">Sample script</span></span>

<span data-ttu-id="a4b9c-109">Este exemplo cria um Aplicativo de funções do Azure e adiciona a cadeia de conexão de armazenamento para uma configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="a4b9c-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrar o Aplicativo de funções à conta de armazenamento do Azure")]</span><span class="sxs-lookup"><span data-stu-id="a4b9c-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="a4b9c-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="a4b9c-111">Clean up deployment</span></span>

<span data-ttu-id="a4b9c-112">Após a execução do exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo do Serviço de Aplicativo e todos os recursos relacionados:</span><span class="sxs-lookup"><span data-stu-id="a4b9c-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a4b9c-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a4b9c-113">Script explanation</span></span>

<span data-ttu-id="a4b9c-114">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-114">This script uses the following commands.</span></span> <span data-ttu-id="a4b9c-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a4b9c-116">Command</span><span class="sxs-lookup"><span data-stu-id="a4b9c-116">Command</span></span> | <span data-ttu-id="a4b9c-117">Observações</span><span class="sxs-lookup"><span data-stu-id="a4b9c-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a4b9c-118">az login</span><span class="sxs-lookup"><span data-stu-id="a4b9c-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="a4b9c-119">Logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-119">Login to Azure.</span></span> |
| [<span data-ttu-id="a4b9c-120">az group create</span><span class="sxs-lookup"><span data-stu-id="a4b9c-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a4b9c-121">Criar um grupo de recursos com local</span><span class="sxs-lookup"><span data-stu-id="a4b9c-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="a4b9c-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="a4b9c-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="a4b9c-123">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a4b9c-123">Create a storage account</span></span> |
| [<span data-ttu-id="a4b9c-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="a4b9c-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="a4b9c-125">Criar um novo aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="a4b9c-125">Create a new function app</span></span> |
| [<span data-ttu-id="a4b9c-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="a4b9c-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="a4b9c-127">Limpar</span><span class="sxs-lookup"><span data-stu-id="a4b9c-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a4b9c-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4b9c-128">Next steps</span></span>

<span data-ttu-id="a4b9c-129">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4b9c-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a4b9c-130">Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a4b9c-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
