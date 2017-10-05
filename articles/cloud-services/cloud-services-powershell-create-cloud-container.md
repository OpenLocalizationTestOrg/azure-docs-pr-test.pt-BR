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
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="3fc6c-104">Usar um comando do Azure PowerShell para criar um contêiner de serviço de nuvem vazio</span><span class="sxs-lookup"><span data-stu-id="3fc6c-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="3fc6c-105">Este artigo explica como criar rapidamente um contêiner de Serviços de Nuvem usando cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fc6c-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3fc6c-106">Siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="3fc6c-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="3fc6c-107">Instale o cmdlet do Microsoft Azure PowerShell da página [Baixar o Azure PowerShell](http://aka.ms/webpi-azps) .</span><span class="sxs-lookup"><span data-stu-id="3fc6c-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="3fc6c-108">Abra o prompt de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fc6c-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="3fc6c-109">Use [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) para entrar.</span><span class="sxs-lookup"><span data-stu-id="3fc6c-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fc6c-110">Para obter mais instruções sobre a instalação do cmdlet do Azure PowerShell e conectar-se à sua assinatura do Azure, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3fc6c-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="3fc6c-111">Use **New-AzureService** para criar um contêiner de serviço de nuvem do Azure vazio.</span><span class="sxs-lookup"><span data-stu-id="3fc6c-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="3fc6c-112">Siga este exemplo para invocar o cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3fc6c-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="3fc6c-113">Para obter mais informações sobre como criar o serviço de nuvem do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="3fc6c-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="3fc6c-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3fc6c-114">Next steps</span></span>
* <span data-ttu-id="3fc6c-115">Para gerenciar a implantação do serviço de nuvem, consulte os comandos [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fc6c-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="3fc6c-116">Você também pode consultar [Como configurar os serviços de nuvem](cloud-services-how-to-configure.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="3fc6c-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="3fc6c-117">Para publicar seu projeto de serviço de nuvem no Azure, consulte o exemplo de código **PublishCloudService.ps1** em [Fornecimento contínuo de serviço de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="3fc6c-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
