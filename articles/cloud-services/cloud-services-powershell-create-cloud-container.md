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
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="76e93-104">Use um comando de PowerShell do Azure toocreate um contêiner de serviço de nuvem vazio</span><span class="sxs-lookup"><span data-stu-id="76e93-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="76e93-105">Este artigo explica como tooquickly criar um contêiner de serviços de nuvem usando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="76e93-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="76e93-106">Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="76e93-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="76e93-107">Instalar o cmdlet do PowerShell do Microsoft Azure Olá Olá [downloads do Azure PowerShell](http://aka.ms/webpi-azps) página.</span><span class="sxs-lookup"><span data-stu-id="76e93-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="76e93-108">Abra um prompt de comando do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="76e93-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="76e93-109">Saudação de uso [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign no.</span><span class="sxs-lookup"><span data-stu-id="76e93-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="76e93-110">Para obter instruções adicionais sobre como instalar o cmdlet do PowerShell do Azure hello e conexão tooyour assinatura do Azure, consulte muito[como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76e93-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="76e93-111">Saudação de uso **New-AzureService** cmdlet toocreate um contêiner de serviço de nuvem do Azure vazio.</span><span class="sxs-lookup"><span data-stu-id="76e93-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="76e93-112">Execute esse cmdlet de saudação do tooinvoke de exemplo:</span><span class="sxs-lookup"><span data-stu-id="76e93-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="76e93-113">Para obter mais informações sobre como criar um serviço de nuvem do Azure hello, execute:</span><span class="sxs-lookup"><span data-stu-id="76e93-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="76e93-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76e93-114">Next steps</span></span>
* <span data-ttu-id="76e93-115">Olá toomanage implantação de serviço de nuvem, consulte toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) comandos.</span><span class="sxs-lookup"><span data-stu-id="76e93-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="76e93-116">Você também pode consultar muito[como serviços em nuvem tooconfigure](cloud-services-how-to-configure.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="76e93-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="76e93-117">toopublish seu serviço de nuvem tooAzure de projeto, consulte toohello **PublishCloudService.ps1** código de exemplo do [entrega contínua para o serviço de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="76e93-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
