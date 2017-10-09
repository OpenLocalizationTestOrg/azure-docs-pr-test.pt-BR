---
title: "modelo de saudação aaaDownload para uma VM do Azure | Microsoft Docs"
description: "Baixar Olá templatefor toohelp uma VM com a automação implantações no modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Baixar modelo de saudação para uma máquina virtual
Quando você cria uma máquina virtual no Azure usando o portal de saudação ou o PowerShell, um Gerenciador de recursos de modelo é criado automaticamente para você. Você pode usar essa cópia do modelo tooquickly uma implantação. modelo de saudação contém informações sobre todos os recursos de saudação em um grupo de recursos. Para uma máquina virtual, isso significa modelo Olá contém tudo o que é criado para oferecer suporte a saudação VM desse grupo de recursos, incluindo recursos de rede hello.

## <a name="download-hello-template-using-hello-portal"></a>Baixar modelo hello usando o portal de saudação
1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Menu de hub uma saudação, selecione **máquinas virtuais**.
3. Selecione máquina virtual de Olá Olá lista.
4. Selecione **Script de automação**.
5. Selecione **baixar** e salve o computador local do tooyour do arquivo hello. zip.
6. Abra o arquivo. zip de saudação e extração Olá arquivos tooa pasta. arquivo. zip de saudação conterá:
   
   * deploy.ps1
   * deploy.sh 
   * deployer.rb
   * DeploymentHelper.cs
   * parameters.json
   * template.json

arquivo de template.json Olá é o modelo de saudação.

## <a name="download-hello-template-using-powershell"></a>Baixar modelo hello usando o PowerShell
Você também pode baixar o arquivo de modelo do hello. JSON usando Olá [AzureRMResourceGroup de exportação](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet. Você pode usar o hello `-path` parâmetro tooprovide Olá filename e o caminho de arquivo do hello. JSON. Este exemplo mostra como o modelo de saudação do toodownload Olá para grupo de recursos denominado **myResourceGroup** toohello **C:\users\public\downloads** pasta no computador local.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a implantação de recursos usando modelos, consulte [passo a passo do Gerenciador de recursos modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).

