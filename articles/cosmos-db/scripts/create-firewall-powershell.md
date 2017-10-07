---
title: aaaAzure PowerShell Script-criar um firewall para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Exemplo de script do Azure PowerShell – Criar um firewall para o Banco de Dados Cosmos do Azure"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 00dd2dd847c7ed0e35f5555c2b87b90977f137f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a>Banco de Dados Cosmos do Azure: Criar um firewall usando PowerShell

Este exemplo de script do PowerShell cria um firewall para qualquer tipo de conta de API do Banco de Dados Cosmos do Azure. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Limpar implantação

Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmResource](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | Cria um servidor lógico que hospeda um banco de dados ou pool elástico. |
| [Set-AzureRMResource](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | Modifica a conta de banco de dados de saudação. |
| [Remove-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).

Exemplos de script do PowerShell do Azure Cosmos DB adicionais podem ser encontrados no hello [scripts do PowerShell do Azure Cosmos DB](../powershell-samples.md).
