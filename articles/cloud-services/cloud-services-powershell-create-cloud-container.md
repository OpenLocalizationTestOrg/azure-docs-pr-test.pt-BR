---
title: "aaaCreate um contêiner de serviço de nuvem com o PowerShell | Microsoft Docs"
description: "Este artigo explica como o contêiner com o PowerShell de serviço toocreate uma nuvem. contêiner de saudação hospeda funções da web e de trabalho."
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
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Use um comando de PowerShell do Azure toocreate um contêiner de serviço de nuvem vazio
Este artigo explica como tooquickly criar um contêiner de serviços de nuvem usando cmdlets do PowerShell do Azure. Siga as etapas de saudação abaixo:

1. Instalar o cmdlet do PowerShell do Microsoft Azure Olá Olá [downloads do Azure PowerShell](http://aka.ms/webpi-azps) página.
2. Abra um prompt de comando do PowerShell hello.
3. Saudação de uso [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign no.

   > [!NOTE]
   > Para obter instruções adicionais sobre como instalar o cmdlet do PowerShell do Azure hello e conexão tooyour assinatura do Azure, consulte muito[como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Saudação de uso **New-AzureService** cmdlet toocreate um contêiner de serviço de nuvem do Azure vazio.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Execute esse cmdlet de saudação do tooinvoke de exemplo:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Para obter mais informações sobre como criar um serviço de nuvem do Azure hello, execute:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Próximas etapas
* Olá toomanage implantação de serviço de nuvem, consulte toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) comandos. Você também pode consultar muito[como serviços em nuvem tooconfigure](cloud-services-how-to-configure.md) para obter mais informações.
* toopublish seu serviço de nuvem tooAzure de projeto, consulte toohello **PublishCloudService.ps1** código de exemplo do [entrega contínua para o serviço de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).
