---
title: aaaAzure exemplo de Script do PowerShell - Adicionar aplicativo cert tooa cluster | Microsoft Docs
description: Script do PowerShell do Azure de exemplo - adicionar um cluster do aplicativo certificado tooa do Service Fabric.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Adicionar um cluster de malha do serviço do aplicativo certificado tooa

Esse script de exemplo cria um certificado autoassinado no cofre de chaves do Azure especificado hello e instala tooall nós de cluster do Service Fabric hello. certificado Olá baixa também a pasta local tooa. nome de saudação do certificado de saudação baixado é Olá igual ao nome de saudação do certificado Olá no cofre de chaves hello. Personalize parâmetros Olá conforme necessário.

Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure. 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir: cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Adicione que uma escala de máquina virtual toohello de certificado novo aplicativo definido que formam o cluster hello.  |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos adicionais do Azure Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).
