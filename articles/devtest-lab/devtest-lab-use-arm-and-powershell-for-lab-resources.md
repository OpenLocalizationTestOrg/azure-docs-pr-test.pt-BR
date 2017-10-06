---
title: "aaaCreate ou modificar laboratórios automaticamente usando modelos do Gerenciador de recursos do Azure com o PowerShell | Microsoft Docs"
description: "Saiba como modelos do Azure Resource Manager toouse com PowerShell toocreate ou modificar laboratórios automaticamente em um laboratório de DevTest"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Criar ou modificar laboratórios automaticamente usando modelos do Azure Resource Manager e o PowerShell

Laboratórios DevTest fornece muitos modelos de Azure Resource Manager e scripts do PowerShell que podem ajudá-lo rapidamente e criar automaticamente os novos laboratórios ou modificar laboratórios existentes e implantar esses recursos.

Este artigo ajuda a guiá-lo pelo processo de saudação do usando esses modelos e scripts tooautomate Olá a criação, modificação e implantação de seus laboratórios. Este artigo mostra onde você pode encontrar mais informações sobre como toouse PowerShell tooperform algumas tarefas comuns no DevTest Labs.

## <a name="step-1-gather-your-templates-and-scripts"></a>Etapa 1: Coletar seus modelos e scripts
Você pode encontrar [modelos do Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) e [scripts do PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) pré-realizados em nosso [repositório Github](https://github.com/Azure/azure-devtestlab) público. Use-os como estão, ou personalize-os para suas necessidades e armazene-os em seu próprio [repositório particular do Git](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Etapa 2: Modificar o modelo do Azure Resource Manager
Você pode seguir as etapas de saudação em [criar seu primeiro modelo do Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) se você nunca tiver criado um modelo antes.

Além disso, [práticas recomendadas para a criação de modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) oferece muitas toohelp diretrizes e sugestões criar modelos do Azure Resource Manager toouse fácil e confiável. Normalmente, você usará uma variação de uma das abordagens de saudação ou exemplos fornecidos e modificar o modelo para suas necessidades.

## <a name="step-3-deploy-resources-with-powershell"></a>Etapa 3: Implantar recursos com o PowerShell
Depois que você personalizou os modelos e os scripts, execute as etapas de saudação necessário muito[implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). artigo Olá fornece informações gerais sobre como usar o PowerShell do Azure com o Azure Resource Manager modelos toodeploy tooAzure seus recursos.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Tarefas comuns que você pode executar nos laboratórios de DevTest usando o PowerShell
Há várias outras tarefas comuns que você pode automatizar usando o PowerShell. Olá seguintes seções da documentação de saudação descrevem Olá etapas necessárias tooperform essas tarefas.

* [Criar uma imagem personalizada de um arquivo VHD usando o PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Carregar conta de armazenamento do toolab do arquivo VHD usando o PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Adicionar um laboratório de tooa de usuário externo usando o PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Criar uma função personalizada do laboratório usando o PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Próximas etapas
* Saiba como toocreate uma [repositório Git particular](devtest-lab-add-artifact-repo.md) onde você armazenará seus modelos personalizados ou scripts.
* Explorar Olá [modelos do Gerenciador de recursos do Azure da Galeria de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).
