---
title: aaaAzure exemplo de Script do PowerShell - dimensionar um aplicativo web em todo o mundo com uma arquitetura de alta disponibilidade | Microsoft Docs
description: Exemplo de Script do Azure PowerShell - Dimensionar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>Escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade

Nesse cenário, você criará um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego. Depois que o exercício de saudação for concluído, você terá uma alta disponibilidade arquitetura que permite que fornece disponibilidade global do seu aplicativo web com base na menor latência de rede hello.

Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

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
| [New-AzureRMTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Cria um perfil do Gerenciador de Tráfego. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Cria um Plano do Serviço de Aplicativo. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Cria um aplicativo web. |
| [New-AzureRMTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Cria um ponto de extremidade em um perfil do Gerenciador de Tráfego. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).
