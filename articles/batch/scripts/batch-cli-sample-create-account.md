---
title: "Amostra de script da CLI do Azure – Criar uma conta do Lote | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Criar uma conta do Lote"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="36b9a-103">Criar uma conta do Lote com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="36b9a-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="36b9a-104">Esse script cria uma conta do Lote do Azure e mostra como várias propriedades da conta podem ser consultadas e atualizadas.</span><span class="sxs-lookup"><span data-stu-id="36b9a-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36b9a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36b9a-105">Prerequisites</span></span>

<span data-ttu-id="36b9a-106">Instale a CLI do Azure usando as instruções fornecidas no [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="36b9a-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="36b9a-107">Script de exemplo de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="36b9a-107">Batch account sample script</span></span>

<span data-ttu-id="36b9a-108">Quando você cria uma conta do Lote, os nós de computação dessa conta são atribuídos internamente, por padrão, pelo serviço de Lote.</span><span class="sxs-lookup"><span data-stu-id="36b9a-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="36b9a-109">Nós de computação alocados estarão sujeitos a uma cota de núcleo separada e a conta poderá ser autenticada por meio de credenciais de Chave Compartilhada ou um token do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36b9a-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="36b9a-110">[!code-azurecli[principal](../../../cli_scripts/batch/create-account/create-account.sh "Criar Conta")]</span><span class="sxs-lookup"><span data-stu-id="36b9a-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="36b9a-111">Conta do Lote usando o script de exemplo de assinatura de usuário</span><span class="sxs-lookup"><span data-stu-id="36b9a-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="36b9a-112">Você também pode optar por fazer com que o Lote crie seus nós de computação na sua própria assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="36b9a-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="36b9a-113">Contas que alocam nós de computação em sua assinatura devem ser autenticadas por meio de um token do Azure Active Directory e os nós de computação distribuídos contarão para a sua cota de assinatura.</span><span class="sxs-lookup"><span data-stu-id="36b9a-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="36b9a-114">Para criar uma conta nesse modo, uma pessoa deve especificar uma referência do Key Vault ao criar a conta.</span><span class="sxs-lookup"><span data-stu-id="36b9a-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="36b9a-115">[!code-azurecli[principal](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Criar Conta Usando a Assinatura do Usuário")]</span><span class="sxs-lookup"><span data-stu-id="36b9a-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="36b9a-116">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="36b9a-116">Clean up deployment</span></span>

<span data-ttu-id="36b9a-117">Depois de executar qualquer um dos scripts de exemplo acima, execute o comando a seguir para remover o grupo de recursos e todos os recursos relacionados (incluindo contas do Lote, contas de Armazenamento do Azure e cofres de chaves do Azure).</span><span class="sxs-lookup"><span data-stu-id="36b9a-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="36b9a-118">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="36b9a-118">Script explanation</span></span>

<span data-ttu-id="36b9a-119">Este script usa os seguintes comandos para criar um grupo de recursos, uma conta do Lote e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="36b9a-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="36b9a-120">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="36b9a-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="36b9a-121">Command</span><span class="sxs-lookup"><span data-stu-id="36b9a-121">Command</span></span> | <span data-ttu-id="36b9a-122">Observações</span><span class="sxs-lookup"><span data-stu-id="36b9a-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="36b9a-123">az group create</span><span class="sxs-lookup"><span data-stu-id="36b9a-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="36b9a-124">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="36b9a-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="36b9a-125">az batch account create</span><span class="sxs-lookup"><span data-stu-id="36b9a-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="36b9a-126">Cria a conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="36b9a-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="36b9a-127">az batch account set</span><span class="sxs-lookup"><span data-stu-id="36b9a-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="36b9a-128">Atualiza as propriedades da conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="36b9a-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="36b9a-129">az batch account show</span><span class="sxs-lookup"><span data-stu-id="36b9a-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="36b9a-130">Recupera os detalhes da conta do Lote especificada.</span><span class="sxs-lookup"><span data-stu-id="36b9a-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="36b9a-131">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="36b9a-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="36b9a-132">Recupera as chaves de acesso da conta do Lote especificada.</span><span class="sxs-lookup"><span data-stu-id="36b9a-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="36b9a-133">az batch account login</span><span class="sxs-lookup"><span data-stu-id="36b9a-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="36b9a-134">Autentica na conta do Lote especificada para interação adicional com a CLI.</span><span class="sxs-lookup"><span data-stu-id="36b9a-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="36b9a-135">az storage account create</span><span class="sxs-lookup"><span data-stu-id="36b9a-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="36b9a-136">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="36b9a-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="36b9a-137">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="36b9a-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="36b9a-138">Cria um cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="36b9a-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="36b9a-139">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="36b9a-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="36b9a-140">Atualize a política de segurança do cofre de chaves especificado.</span><span class="sxs-lookup"><span data-stu-id="36b9a-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="36b9a-141">az group delete</span><span class="sxs-lookup"><span data-stu-id="36b9a-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="36b9a-142">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="36b9a-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36b9a-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36b9a-143">Next steps</span></span>

<span data-ttu-id="36b9a-144">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36b9a-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="36b9a-145">As amostras de script da CLI do Lote adicionais podem ser encontrados na [documentação do Lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="36b9a-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
