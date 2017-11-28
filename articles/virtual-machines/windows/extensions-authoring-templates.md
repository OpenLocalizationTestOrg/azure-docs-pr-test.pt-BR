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
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="0e21e-103">Criando modelos do Azure Resource Manager com extensões de VM do Windows</span><span class="sxs-lookup"><span data-stu-id="0e21e-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="0e21e-104">Do Azure PowerShell, execute hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e21e-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="0e21e-105">Esse cmdlet retorna a versão, nome de extensão e nome do publicador Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0e21e-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="0e21e-106">Essas três propriedades mapeiam muito "publisher", "tipo" e "typeHandlerVersion", respectivamente Olá acima trecho do modelo.</span><span class="sxs-lookup"><span data-stu-id="0e21e-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="0e21e-107">É sempre recomendado toouse hello mais recente versão tooget hello mais atualizado funcionalidade de extensão.</span><span class="sxs-lookup"><span data-stu-id="0e21e-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="0e21e-108">Identificando o esquema de saudação para parâmetros de configuração de extensão Olá</span><span class="sxs-lookup"><span data-stu-id="0e21e-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="0e21e-109">a próxima etapa Olá com a criação de um modelo de extensão é tooidentify formato de saudação para fornecer parâmetros de configuração.</span><span class="sxs-lookup"><span data-stu-id="0e21e-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="0e21e-110">Cada extensão dá suporte a seu próprio conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="0e21e-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="0e21e-111">toolook em exemplos de configurações para extensões do Windows, consulte [exemplos de extensões do Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e21e-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0e21e-112">Consulte toohello tooget um modelo totalmente completo com extensões de VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e21e-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="0e21e-113">Extensão de script personalizado em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="0e21e-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="0e21e-114">Depois de criar o modelo de saudação, você pode implantar usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e21e-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

