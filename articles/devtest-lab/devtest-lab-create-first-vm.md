---
title: "aaaCreate sua primeira VM em um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como toocreate sua primeira máquina virtual em um laboratório no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Criar a primeira VM no Azure DevTest Labs

Quando você inicialmente acessar DevTest Labs e deseja toocreate sua VM primeiro, você provavelmente vai fazer isso usando um pré-carregados [imagem do marketplace base](devtest-lab-configure-marketplace-images.md). Posteriormente no, você também será capaz de toochoose de um [imagem personalizada e uma fórmula](devtest-lab-add-vm.md) ao criar mais VMs. 

Este tutorial orienta usando Olá tooadd portal do Azure laboratório em DevTest Labs tooa VM primeiro.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Etapas tooadd seu primeiro laboratório tooa VM no Azure DevTest Labs
1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
1. Saudação de laboratórios, selecione lista laboratório Olá no qual você deseja toocreate Olá VM.  
1. No laboratório de saudação **visão geral** folha, selecione **+ adicionar**.  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Em Olá **escolher uma base** folha, selecione a imagem de um mercado para Olá VM.
1. Em Olá **Máquina Virtual** folha, digite um nome para a máquina virtual da nova Olá no hello **nome da máquina Virtual** caixa de texto.

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Insira um **nome de usuário** que tem privilégios de administrador na máquina virtual de saudação.  
1. Digite uma senha no campo de texto de saudação rotulado **digite um valor**.
1. Olá **tipo de disco de máquina Virtual** determina qual tipo de disco de armazenamento será permitido para máquinas virtuais de saudação laboratório hello.
1. Selecione **tamanho da máquina Virtual** e selecione uma das Olá predefinidos itens que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate.
1. Selecione **artefatos** - lista de saudação de artefatos - e selecione Configurar artefatos Olá que deseja que a imagem base do tooadd toohello.
    **Observação:** se você for novo laboratórios de tooDevTest ou configurando artefatos, consulte toohello [adicionar um tooa de artefato existente VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) seção e, em seguida, retornar aqui quando terminar.
1. Selecione **criar** tooadd Olá especificado laboratório toohello de VM.

   folha de laboratório Olá exibe o status de saudação da criação da VM Olá - primeiro como **criando**, em seguida, como **executando** após Olá VM foi iniciada.

## <a name="next-steps"></a>Próximas etapas
* Uma vez Olá VM tiver sido criada, você pode se conectar toohello VM selecionando **conectar** na folha de saudação da VM.
* Check-out [adicionar um laboratório de tooa VM](devtest-lab-add-vm.md) para obter informações mais completas sobre como adicionar VMs subsequentes no laboratório.
* Explorar Olá [Galeria de modelos do DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
