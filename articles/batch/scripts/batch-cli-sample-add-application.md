---
title: aaaAzure exemplo de Script CLI - adicionar um aplicativo em lote | Microsoft Docs
description: "Amostra de Script da CLI do Azure – Adicionar um aplicativo no Lote"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Adicionar aplicativos tooAzure lote com a CLI do Azure

Este script demonstra como tooset um aplicativo para uso com um pool de lote do Azure ou uma tarefa. tooset um aplicativo, o executável, juntamente com quaisquer dependências, em um arquivo. zip do pacote. Neste zip executável do exemplo hello arquivo é denominado ' Meu-aplicativo-exe.zip'.

## <a name="prerequisites"></a>Pré-requisitos

- Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.
- Crie uma conta do lote do Azure caso ainda não tenha uma. Consulte [criar uma conta de lote com hello CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Limpar aplicativo

Depois de executar Olá acima script de exemplo, execute Olá tooremove comandos a seguir o aplicativo e todos os seus pacotes de aplicativo carregado.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá toocreate comandos a seguir, um aplicativo e carregar um pacote de aplicativo.
Cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | Criar um aplicativo.  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | Atualiza as propriedades de um aplicativo.  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Adiciona um toohello do pacote de aplicativo especificado aplicativo.  |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).
