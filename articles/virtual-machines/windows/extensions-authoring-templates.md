---
title: "aaaAuthoring modelos com extensões de VM do Windows | Microsoft Docs"
description: "Saiba mais sobre como criar modelos do Azure Resource Manager com extensões de VMs do Windows"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Criando modelos do Azure Resource Manager com extensões de VM do Windows
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Do Azure PowerShell, execute hello Azure PowerShell cmdlet a seguir:

      Get-AzureVMAvailableExtension


Esse cmdlet retorna a versão, nome de extensão e nome do publicador Olá da seguinte maneira:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Essas três propriedades mapeiam muito "publisher", "tipo" e "typeHandlerVersion", respectivamente Olá acima trecho do modelo.

> [!NOTE]
> É sempre recomendado toouse hello mais recente versão tooget hello mais atualizado funcionalidade de extensão.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Identificando o esquema de saudação para parâmetros de configuração de extensão Olá
a próxima etapa Olá com a criação de um modelo de extensão é tooidentify formato de saudação para fornecer parâmetros de configuração. Cada extensão dá suporte a seu próprio conjunto de parâmetros.

toolook em exemplos de configurações para extensões do Windows, consulte [exemplos de extensões do Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Consulte toohello tooget um modelo totalmente completo com extensões de VM a seguir.

[Extensão de script personalizado em uma VM do Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Depois de criar o modelo de saudação, você pode implantar usando o PowerShell do Azure.

