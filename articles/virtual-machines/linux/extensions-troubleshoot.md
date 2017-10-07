---
title: "aaaTroubleshooting VM Linux falhas de extensão | Microsoft Docs"
description: "Saiba mais sobre como solucionar falhas da extensão de VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Solucionando problemas de falhas de extensões de VM do Linux
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Exibindo o status da extensão
Modelos do Gerenciador de recursos do Azure podem ser executados de saudação CLI do Azure. Depois Olá modelo é executado, o status da extensão de saudação podem ser exibidos de ferramentas de linha de comando do Gerenciador de recursos do Azure ou hello.

Aqui está um exemplo:

CLI do Azure:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Solucionando falhas de Extensão:
### <a name="re-running-hello-extension-on-hello-vm"></a>Executar novamente a extensão de saudação em Olá VM
Se você estiver executando os scripts em Olá VM usando a extensão de Script personalizado, você pode executar, às vezes, um erro onde a VM foi criada com êxito mas script hello falhou. Sob essas conditons hello recomendado maneira toorecover desse erro é tooremove Olá extensão e novamente o modelo de saudação.
Observação: No futuro, essa funcionalidade seria tooremove avançado Olá necessidade para desinstalar a extensão de saudação.

#### <a name="remove-hello-extension-from-azure-cli"></a>Remover extensão de saudação da CLI do Azure
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Onde "nome do Publisher" corresponde a tipo de extensão toohello da saída de saudação da "máquina virtual do azure get-instância-exibição" e nome é o nome de saudação do recurso de extensão de saudação do modelo Olá

Quando Olá extensão foi removida, o modelo de Olá pode ser executado novamente toorun Olá scripts Olá VM.

