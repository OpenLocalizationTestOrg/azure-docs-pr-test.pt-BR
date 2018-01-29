---
title: "Criar um contêiner do serviço de nuvem com o PowerShell | Microsoft Docs"
description: "Este artigo explica como criar um contêiner do serviço de nuvem com o PowerShell. O contêiner hospeda funções da Web e de trabalho."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: cd703feb7bf5af765fc3a5448464499aa7b48d6a
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a>Usar um comando do Azure PowerShell para criar um contêiner de serviço de nuvem vazio
Este artigo explica como criar rapidamente um contêiner de Serviços de Nuvem usando cmdlets do Azure PowerShell. Siga as etapas abaixo:

1. Instale o cmdlet do Microsoft Azure PowerShell da página [Baixar o Azure PowerShell](http://aka.ms/webpi-azps) .
2. Abra o prompt de comando do PowerShell.
3. Use [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) para entrar.

   > [!NOTE]
   > Para obter mais instruções sobre a instalação do cmdlet do Azure PowerShell e conectar-se à sua assinatura do Azure, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Use **New-AzureService** para criar um contêiner de serviço de nuvem do Azure vazio.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Siga este exemplo para invocar o cmdlet:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Para obter mais informações sobre como criar o serviço de nuvem do Azure, execute:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Próximas etapas
* Para gerenciar a implantação do serviço de nuvem, consulte os comandos [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx). Você também pode consultar [Como configurar os serviços de nuvem](cloud-services-how-to-configure-portal.md) para saber mais.
* Para publicar seu projeto de serviço de nuvem no Azure, consulte o exemplo de código **PublishCloudService.ps1** em [Fornecimento contínuo de serviço de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).
