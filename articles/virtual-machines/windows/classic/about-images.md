---
title: "imagens de aaaAbout para máquinas virtuais do Windows | Microsoft Docs"
description: "Saiba mais sobre como as imagens são usadas com máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Sobre imagens de máquinas virtuais do Windows
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações sobre como localizar e usar imagens no modelo do Gerenciador de recursos de hello, consulte [aqui](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Trabalhando com imagens

Você pode usar o módulo do PowerShell do Azure hello e tooyour de disponíveis imagens assinatura do Azure de saudação de toomanage portal do Azure hello. módulo do PowerShell do Azure Olá fornece mais opções de comando, para que você pode identificar exatamente o que você deseja toosee ou fazer. Olá portal do Azure fornece uma interface gráfica para muitas tarefas administrativas diárias de saudação.

Aqui estão alguns exemplos que usam o módulo do PowerShell do Azure hello.

* **Obter todas as imagens**:`Get-AzureVMImage`retorna uma lista de todas as imagens de saudação disponíveis na sua assinatura atual: suas imagens e aquelas fornecidas pelo Azure ou parceiros. lista de saudação resultante pode ser grande. Olá próximo exemplos mostram como tooget uma lista mais curta.
* **Obter as famílias de imagem**:`Get-AzureVMImage | select ImageFamily` obtém uma lista das famílias de imagem, mostrando as cadeias de caracteres da propriedade **ImageFamily**.
* **Obtenha todas as imagens em uma família específica**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Localizar imagens da VM**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` esse cmdlet funciona por meio da propriedade de DataDiskConfiguration hello, que se aplica somente a imagens tooVM de filtragem. Este exemplo também filtra Olá tooonly Olá rótulo e a imagem de nome de saída.
* **Salvar uma imagem generalizada**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Salvar uma imagem especializada**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > parâmetro OSState de saudação é necessário toocreate uma imagem VM, que inclui o disco do sistema operacional hello e discos de dados conectados. Se você não usar o parâmetro hello, Olá cmdlet cria uma imagem do sistema operacional. valor Olá parâmetro hello indica se a imagem de saudação é generalizada ou especializada, baseado em se o disco do sistema operacional Olá foi preparado para reutilização.

* **Excluir uma imagem**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Próximas etapas
Você também pode [criar uma máquina Windows usando o portal do Azure de saudação](tutorial.md).
