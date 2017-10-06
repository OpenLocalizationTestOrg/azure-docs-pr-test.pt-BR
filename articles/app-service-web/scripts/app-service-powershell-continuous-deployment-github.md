---
title: "aaaAzure exemplo de Script do PowerShell - criar um aplicativo web com implantação contínua do GitHub | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell - criar um aplicativo Web com a implantação contínua do GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>Criar um aplicativo web com a implantação contínua do GitHub

Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, define a implantação contínua de um repositório GitHub. Para implantação do GitHub sem a implantação contínua, veja [Criar um aplicativo Web e implantar o código do GitHub](app-service-powershell-deploy-github.md).

Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview). Além disso, verifique se:

- Foi criada uma conexão com o Azure usando Olá `az login` comando.
- código do aplicativo Hello está em um repositório GitHub público ou privado que você possui.
- Você [criou um token de acesso em sua conta do GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Cria um Plano do Serviço de Aplicativo. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Cria um aplicativo web. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Modifica um recurso em um grupo de recursos. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).
