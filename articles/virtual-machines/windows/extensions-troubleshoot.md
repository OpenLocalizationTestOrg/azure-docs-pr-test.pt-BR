---
title: "falhas de extensão de VM do Windows aaaTroubleshooting | Microsoft Docs"
description: "Saiba mais sobre como solucionar falhas da extensão de VM do Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Solucionando problemas de falhas da extensão da VM do Windows no Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Exibindo o status da extensão
Os modelos do Azure Resource Manager podem ser executados no Azure PowerShell. Depois Olá modelo é executado, o status da extensão de saudação podem ser exibidos de ferramentas de linha de comando do Gerenciador de recursos do Azure ou hello.

Aqui está um exemplo:

PowerShell do Azure:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Aqui está a saída de exemplo hello:

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>Solução de problemas de falhas da extensão
### <a name="re-running-hello-extension-on-hello-vm"></a>Executar novamente a extensão de saudação em Olá VM
Se você estiver executando os scripts em Olá VM usando a extensão de Script personalizado, você pode executar, às vezes, um erro onde a VM foi criada com êxito mas script hello falhou. Sob essas conditons hello recomendado maneira toorecover desse erro é tooremove Olá extensão e novamente o modelo de saudação.
Observação: No futuro, essa funcionalidade seria tooremove avançado Olá necessidade para desinstalar a extensão de saudação.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Remover extensão de saudação do PowerShell do Azure
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Quando Olá extensão foi removida, o modelo de Olá pode ser executado novamente toorun Olá scripts Olá VM.

