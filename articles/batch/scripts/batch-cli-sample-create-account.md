---
title: aaaAzure exemplo de Script CLI - criar uma conta de lote | Microsoft Docs
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="7f7bf-103">Crie uma conta de lote com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7f7bf-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="7f7bf-104">Esse script cria uma conta de lote do Azure e mostra como várias propriedades de conta Olá podem ser consultadas e atualizadas.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f7bf-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f7bf-105">Prerequisites</span></span>

<span data-ttu-id="7f7bf-106">Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="7f7bf-107">Script de exemplo de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="7f7bf-107">Batch account sample script</span></span>

<span data-ttu-id="7f7bf-108">Quando você criar uma conta de lote, por padrão os nós de computação são atribuídos internamente pelo serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="7f7bf-109">Nós de computação alocado será cota de núcleos separado do assunto tooa e conta Olá pode ser autenticada por meio de credenciais de chave compartilhada ou um token Dirctory ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="7f7bf-110">Conta do Lote usando o script de exemplo de assinatura de usuário</span><span class="sxs-lookup"><span data-stu-id="7f7bf-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="7f7bf-111">Você também pode optar por toohave lote criar seus nós de computação em sua própria assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="7f7bf-112">Contas que alocam computação nós em sua assinatura devem ser autenticadas por meio de um token do Active Directory do Azure e nós de computação Olá alocados contará até sua cota de assinatura.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="7f7bf-113">toocreate uma conta nesse modo, um deve especificar uma referência de Cofre de chaves ao criar conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7f7bf-114">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="7f7bf-114">Clean up deployment</span></span>

<span data-ttu-id="7f7bf-115">Depois de executar qualquer uma das Olá acima scripts de exemplo, execute Olá tooremove de comando a seguir, o grupo de recursos e recursos de todos os relacionados (inclusive contas em lotes, contas de armazenamento do Azure e cofres de chaves do Azure).</span><span class="sxs-lookup"><span data-stu-id="7f7bf-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7f7bf-116">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="7f7bf-116">Script explanation</span></span>

<span data-ttu-id="7f7bf-117">Esse script usa Olá comandos toocreate um grupo de recursos, a conta de lote e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="7f7bf-118">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7f7bf-119">Command</span><span class="sxs-lookup"><span data-stu-id="7f7bf-119">Command</span></span> | <span data-ttu-id="7f7bf-120">Observações</span><span class="sxs-lookup"><span data-stu-id="7f7bf-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7f7bf-121">az group create</span><span class="sxs-lookup"><span data-stu-id="7f7bf-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7f7bf-122">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7f7bf-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="7f7bf-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="7f7bf-124">Cria a conta do lote hello.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="7f7bf-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="7f7bf-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="7f7bf-126">Atualiza as propriedades da conta do lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="7f7bf-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="7f7bf-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="7f7bf-128">Recupera detalhes de saudação especificado conta do lote.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="7f7bf-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="7f7bf-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="7f7bf-130">Chaves de acesso de saudação recupera de saudação especificado conta do lote.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="7f7bf-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="7f7bf-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="7f7bf-132">Se autentica no hello especificado conta para obter interação de CLI do lote.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="7f7bf-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="7f7bf-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="7f7bf-134">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="7f7bf-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="7f7bf-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="7f7bf-136">Cria um cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="7f7bf-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="7f7bf-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="7f7bf-138">Atualize a política de segurança de saudação do Cofre de chaves especificado hello.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="7f7bf-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="7f7bf-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="7f7bf-140">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7f7bf-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f7bf-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f7bf-141">Next steps</span></span>

<span data-ttu-id="7f7bf-142">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7f7bf-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7f7bf-143">Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7f7bf-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
