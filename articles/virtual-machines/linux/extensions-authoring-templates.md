---
title: "modelos de aaaAuthoring com extensões de VM do Linux | Microsoft Docs"
description: "Saiba mais sobre como criar modelos do Azure Resource Manager com extensões de VMs do Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="67b8f-103">Criando modelos do Azure Resource Manager com extensões de VM do Linux</span><span class="sxs-lookup"><span data-stu-id="67b8f-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="67b8f-104">Da CLI do Azure, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="67b8f-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="67b8f-105">Esse comando retorna Olá-nome do fornecedor, nome de extensão e versão da seguinte:</span><span class="sxs-lookup"><span data-stu-id="67b8f-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="67b8f-106">Essas três propriedades mapeiam muito "publisher", "tipo" e "typeHandlerVersion", respectivamente Olá acima trecho do modelo.</span><span class="sxs-lookup"><span data-stu-id="67b8f-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="67b8f-107">É sempre recomendado toouse hello mais recente versão tooget hello mais atualizado funcionalidade de extensão.</span><span class="sxs-lookup"><span data-stu-id="67b8f-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="67b8f-108">Identificando o esquema de saudação para parâmetros de configuração de extensão Olá</span><span class="sxs-lookup"><span data-stu-id="67b8f-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="67b8f-109">a próxima etapa Olá com a criação de um modelo de extensão é tooidentify formato de saudação para fornecer parâmetros de configuração.</span><span class="sxs-lookup"><span data-stu-id="67b8f-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="67b8f-110">Cada extensão dá suporte a seu próprio conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="67b8f-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="67b8f-111">toolook em exemplos de configurações para extensões do Linux, clique em documentação Olá consulte [Linux eExtensions exemplos](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67b8f-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="67b8f-112">Consulte toohello tooget um modelo totalmente completo com extensões de VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="67b8f-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="67b8f-113">Extensão do Script Personalizado em uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="67b8f-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="67b8f-114">Depois de criar o modelo de Olá, você pode implantá-lo usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="67b8f-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

