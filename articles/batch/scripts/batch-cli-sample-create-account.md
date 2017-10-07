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
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Crie uma conta de lote com hello CLI do Azure

Esse script cria uma conta de lote do Azure e mostra como várias propriedades de conta Olá podem ser consultadas e atualizadas.

## <a name="prerequisites"></a>Pré-requisitos

Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.

## <a name="batch-account-sample-script"></a>Script de exemplo de conta do Lote

Quando você criar uma conta de lote, por padrão os nós de computação são atribuídos internamente pelo serviço de lote de saudação. Nós de computação alocado será cota de núcleos separado do assunto tooa e conta Olá pode ser autenticada por meio de credenciais de chave compartilhada ou um token Dirctory ativa do Azure.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Conta do Lote usando o script de exemplo de assinatura de usuário

Você também pode optar por toohave lote criar seus nós de computação em sua própria assinatura do Azure.
Contas que alocam computação nós em sua assinatura devem ser autenticadas por meio de um token do Active Directory do Azure e nós de computação Olá alocados contará até sua cota de assinatura. toocreate uma conta nesse modo, um deve especificar uma referência de Cofre de chaves ao criar conta de saudação.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Limpar implantação

Depois de executar qualquer uma das Olá acima scripts de exemplo, execute Olá tooremove de comando a seguir, o grupo de recursos e recursos de todos os relacionados (inclusive contas em lotes, contas de armazenamento do Azure e cofres de chaves do Azure).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, a conta de lote e relacionados todos os recursos a seguir. Cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Cria a conta do lote hello.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Atualiza as propriedades da conta do lote de saudação.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Recupera detalhes de saudação especificado conta do lote.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Chaves de acesso de saudação recupera de saudação especificado conta do lote.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Se autentica no hello especificado conta para obter interação de CLI do lote.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Cria uma conta de armazenamento. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Cria um cofre de chave. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Atualize a política de segurança de saudação do Cofre de chaves especificado hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).
