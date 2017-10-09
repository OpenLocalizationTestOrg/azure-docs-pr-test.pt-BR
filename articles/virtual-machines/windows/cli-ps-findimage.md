---
title: imagens do aaaSelect VM do Windows no Azure | Microsoft Docs
description: "Saiba como toouse do Azure PowerSHell toodetermine Olá publisher, oferta, SKU e versão para imagens de VM do Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Como as imagens de toofind VM do Windows no hello Azure Marketplace com o Azure PowerShell

Este tópico descreve como toouse do Azure PowerShell toofind VM imagens no hello Azure Marketplace. Use este toospecify informações sobre uma imagem do Marketplace quando você criar uma VM do Windows.

Certifique-se de que instalou e configurou o hello mais recente [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tabela das imagens do Windows mais usadas
| PublisherName | Oferta | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-with-Containers |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Localizar imagens específicas


Ao criar uma nova máquina virtual com o Gerenciador de recursos do Azure, em alguns casos é necessário toospecify uma imagem com a combinação de saudação do hello propriedades da imagem a seguir:

* Editor
* Oferta
* SKU

Por exemplo, usar esses valores com hello [AzureRMVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet do PowerShell, ou com um modelo de grupo de recursos no qual você deve especificar o tipo de saudação da VM toobe criado.

Se você precisar toodetermine esses valores, você pode executar Olá [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), e [AzureRMVMImageSku Get](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets imagens de saudação toonavigate. Você determina estes valores:

1. Editores de imagem de saudação de lista.
2. Para um determinado editor, liste suas ofertas.
3. Para uma determinada oferta, liste seus SKUs.

Primeiro, lista Editores Olá com hello comandos a seguir:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Preencha o nome do publicador escolhido e execute Olá comandos a seguir:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Preencha o nome da oferta escolhido e execute Olá comandos a seguir:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Da saída de saudação de saudação `Get-AzureRMVMImageSku` de comando, você tem todas as informações de saudação, você precisa de imagem de saudação toospecify para uma nova máquina virtual.

a seguir Olá mostra um exemplo completo:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Saída:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Para o publicador de "MicrosoftWindowsServer" hello:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Saída:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Oferta de "WindowsServer" hello:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Saída:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

Nesta lista, copiar Olá escolhida o nome da SKU, e você tem todas as informações de saudação de saudação `Set-AzureRMVMSourceImage` cmdlet do PowerShell ou para um modelo de grupo de recursos.

## <a name="next-steps"></a>Próximas etapas
Agora você pode escolher a imagem de saudação com precisão você deseja toouse. toocreate uma máquina virtual rapidamente usando informações da imagem hello, que você acabou de encontrar, consulte [criar uma máquina virtual do Windows com o PowerShell](quick-create-powershell.md).
