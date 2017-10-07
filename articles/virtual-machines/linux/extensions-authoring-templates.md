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
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Criando modelos do Azure Resource Manager com extensões de VM do Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Da CLI do Azure, execute Olá comando a seguir:

      Azure VM extension list

Esse comando retorna Olá-nome do fornecedor, nome de extensão e versão da seguinte:

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

toolook em exemplos de configurações para extensões do Linux, clique em documentação Olá consulte [Linux eExtensions exemplos](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Consulte toohello tooget um modelo totalmente completo com extensões de VM a seguir.

[Extensão do Script Personalizado em uma VM do Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Depois de criar o modelo de Olá, você pode implantá-lo usando Olá CLI do Azure.

