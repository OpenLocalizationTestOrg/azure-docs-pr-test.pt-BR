---
title: "aaaView e usar do Azure Resource Manager modelo uma máquina virtual | Microsoft Docs"
description: "Saiba como toouse Olá modelo do Gerenciador de recursos do Azure de uma máquina virtual toocreate outras VMs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Usar o modelo do Azure Resource Manager de uma máquina virtual

Ao criar uma máquina virtual (VM) em DevTest Labs por meio de saudação [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), você pode exibir o modelo do Azure Resource Manager Olá antes de salvar Olá VM. Hello modelo pode ser usado como uma base toocreate mais máquinas virtuais do laboratório com hello mesmas configurações.

Este artigo descreve como tooview Olá modelo do Gerenciador de recursos durante a criação de uma máquina virtual e como toodeploy-lo posteriormente criação tooautomate de Olá mesma VM.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Modelos do Resource Manager de várias VMs vs. de uma única VM
Há duas maneiras toocreate VMs em DevTest Labs usando um modelo do Gerenciador de recursos: provisionar Olá Microsoft.DevTestLab/labs/virtualmachines recursos ou provisionar Olá Microsoft.Commpute/virtualmachines recursos. Cada um é usado em cenários diferentes e exige permissões diferentes.

- Modelos do Gerenciador de recursos que usam um tipo de recurso Microsoft.DevTestLab/labs/virtualmachines (conforme declarado na propriedade de "recurso" hello no modelo de saudação) podem provisionar máquinas virtuais do laboratório individuais. Em seguida, cada VM aparece como um único item na lista de máquinas virtuais do DevTest Labs hello:

   ![Lista de máquinas virtuais como itens individuais na lista de máquinas virtuais do DevTest Labs Olá](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Este tipo de modelo do Gerenciador de recursos pode ser provisionado com hello comando do PowerShell do Azure **New-AzureRmResourceGroupDeployment** ou por meio de saudação comando CLI do Azure **criar implantação de grupo az** . Isso requer permissões de administrador, para que os usuários atribuídos a uma função de usuário do DevTest Labs não é possível executar a implantação de saudação. 

- Modelos do Gerenciador de recursos que usam um tipo de recurso Microsoft.Compute/virtualmachines podem provisionar várias VMs como um único ambiente na lista de máquinas virtuais do DevTest Labs hello:

   ![Lista de máquinas virtuais como itens individuais na lista de máquinas virtuais do DevTest Labs Olá](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   VMs no hello mesmo ambiente pode ser administrado juntos e compartilhamento Olá mesmo ciclo de vida. Os usuários atribuídos a uma função de usuário do DevTest Labs podem criar ambientes usando esses modelos como Olá administrador configurou laboratório Olá dessa maneira.

Olá restante deste artigo aborda modelos do Gerenciador de recursos que usam Mirosoft.DevTestLab/labs/virtualmachines. Eles são usados pela criação da VM de laboratório laboratório administradores tooautomate (por exemplo, claimable VMs) ou a geração de imagem dourada (por exemplo, a fábrica de imagem).

[Práticas recomendadas para a criação de modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) oferece muitas toohelp diretrizes e sugestões criar modelos do Azure Resource Manager toouse fácil e confiável.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Exibir e salvar o modelo do Azure Resource Manager de uma máquina virtual
1. Siga as etapas de saudação em [criar sua primeira VM em um laboratório](devtest-lab-create-first-vm.md) toobegin criar uma máquina virtual.
1. Insira as informações de saudação necessários para sua máquina virtual e adicione qualquer artefato que você deseja para essa VM.
1. Na parte inferior de saudação da janela de configurações de configurar hello, escolha **modelo do ARM exibição**.

   ![Botão Exibir modelo ARM](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Copie e salve toouse de modelo do Gerenciador de recursos de saudação posterior toocreate outra máquina virtual.

   ![Toosave de modelo de Gerenciador de recursos para uso posterior](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Depois de salvar o modelo do Gerenciador de recursos de saudação, você deve atualizar seção de parâmetros de saudação do modelo de saudação antes de você pode usá-lo. Você pode criar um parameter.json que personaliza apenas parâmetros de hello, fora do modelo de Gerenciador de recursos real hello. 

![Personalizar parâmetros usando um arquivo JSON](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Implantar um modelo de Gerenciador de recursos toocreate uma VM
Depois de salvar um modelo do Gerenciador de recursos e personalizado para suas necessidades, você pode usar tooautomate criação de VM. [Implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) descreve como toouse PowerShell do Azure com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos. [Implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) descreve como toouse CLI do Azure com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos.

> [!NOTE]
> Somente um usuário com permissões de proprietário de laboratório pode criar VMs de um modelo do Resource Manager usando o Azure PowerShell. Se você quiser usar um modelo do Gerenciador de recursos de criação de VM tooautomate e tiver apenas permissões de usuário, você pode usar o hello [ **az laboratório vm criar** do hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Próximas etapas
* Saiba como muito[criar ambientes de várias VMs com modelos do Gerenciador de recursos](devtest-lab-create-environment-from-arm.md).
* Explorar mais modelos de Gerenciador de recursos de início rápido para a automação do DevTest Labs Olá [repositório público do DevTest Labs GitHub](https://github.com/Azure/azure-quickstart-templates).
