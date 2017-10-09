---
title: "aaaAdd um laboratório de tooa claimable VM no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooadd um laboratório de tooa claimable máquina de virtual no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Adicionar um laboratório de tooa claimable VM no Azure DevTest Labs
Adicionar um laboratório de tooa claimable VM em um toohow de maneira semelhante você [adicionar uma VM padrão](devtest-lab-add-vm.md) – de uma *base* seja um [imagem personalizada](devtest-lab-create-template.md), [fórmula](devtest-lab-manage-formulas.md), ou [imagem do Marketplace](devtest-lab-configure-marketplace-images.md). Este tutorial orienta você a usar Olá tooadd portal do Azure um laboratório de tooa VM claimable DevTest Labs e mostra o processo de saudação que um usuário segue tooclaim Olá VM.

> [!NOTE]
> Se você implantar máquinas virtuais do laboratório por meio de [modelos do Azure Resource Manager](devtest-lab-create-environment-from-arm.md), você pode criar VMs claimable por configuração Olá **allowClaim** tootrue de propriedade na seção de propriedades de saudação.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Etapas tooadd um laboratório de tooa claimable VM no Azure DevTest Labs
1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
1. Saudação de laboratórios, selecione lista laboratório Olá no qual você deseja toocreate Olá claimable VM.  
1. No laboratório de saudação **visão geral** folha, selecione **+ adicionar**.  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Em Olá **escolher uma base** folha, selecione uma base para Olá VM.
1. Em Olá **Máquina Virtual** folha, digite um nome para a máquina virtual da nova Olá no hello **nome da máquina Virtual** caixa de texto.

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Insira um **nome de usuário** que tem privilégios de administrador na máquina virtual de saudação.  
1. Se você quiser toouse uma senha armazenada em seu [armazenamento secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecione **usar um segredo salvo**e especifique um valor de chave que corresponde a tooyour segredo (senha). Caso contrário, digite uma senha no campo de texto de saudação rotulado **digite um valor**.
1. Olá **tipo de disco de máquina Virtual** determina qual tipo de disco de armazenamento será permitido para máquinas virtuais de saudação laboratório hello.
1. Selecione **tamanho da máquina Virtual** e selecione uma das Olá predefinidos itens que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate.
1. Selecione **artefatos** e, na lista de saudação de artefatos, selecionar e configurar os artefatos de saudação que deseja que a imagem base do tooadd toohello. Se você for novo laboratórios de tooDevTest ou configurando artefatos, consulte toohello [adicionar um tooa de artefato existente VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) seção e, em seguida, retornar aqui quando terminar.
1. Selecione **configurações avançadas** opções de opções e expiração de rede da VM do tooconfigure hello. Em **opções de declaração**, escolha **Sim** máquina de saudação toomake claimable.

  ![Escolha toomake Olá claimable de VM.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Se você quiser tooview ou copia modelo do Azure Resource Manager Olá, consulte toohello [do Azure Resource Manager Salvar modelo](devtest-lab-add-vm.md#save-azure-resource-manager-template) seção e retornar aqui quando terminar.
1. Selecione **criar** tooadd Olá especificado laboratório toohello de VM.
1. folha de laboratório Olá exibe o status de saudação da criação da VM Olá - primeiro como **criando**, em seguida, como **executando** após Olá VM foi iniciada.


## <a name="using-a-claimable-vm"></a>Usando uma VM declarável

Um usuário pode declaração qualquer VM na lista de saudação de "Máquinas de virtuais Claimable" seguindo uma destas etapas:

* Na lista de saudação de "Máquinas de virtuais Claimable" na parte inferior da saudação da folha de visão geral do laboratório hello, com o botão direito em uma saudação VMs na lista de saudação e escolha **máquina declaração**.

 ![Solicite uma VM declarável específica.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* Na parte superior de saudação do hello **visão geral** folha, escolha **declaração qualquer**. Uma máquina virtual aleatória é atribuída na lista de saudação de VMs claimable.

 ![Solicite uma VM declarável.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Depois que um usuário declara uma VM, ela é movida para cima em sua lista de “Minhas máquinas virtuais” e não é mais declarável por nenhum outro usuário.

## <a name="next-steps"></a>Próximas etapas
* Uma vez Olá VM tiver sido criada, você pode se conectar toohello VM selecionando **conectar** na folha de saudação da VM.
* Explorar Olá [DevTest Labs Azure Resource Manager QuickStart Galeria de modelos](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
