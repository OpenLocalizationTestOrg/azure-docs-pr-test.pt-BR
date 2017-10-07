---
title: "aaaAdd laboratório tooa uma VM do Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooadd laboratório tooa uma máquina virtual do Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Adicionar um laboratório de tooa VM no Azure DevTest Labs
Se você já tiver [criado sua primeira VM](devtest-lab-create-first-vm.md), provavelmente isso foi feito por meio de uma [imagem do Marketplace](devtest-lab-configure-marketplace-images.md) pré-carregada. Agora, se você quiser tooadd subsequentes VMs tooyour laboratório, você também pode escolher um *base* seja um [imagem personalizada](devtest-lab-create-template.md) ou um [fórmula](devtest-lab-manage-formulas.md). Este tutorial orienta você a usar o hello tooadd portal do Azure um laboratório de tooa VM em DevTest Labs.

Este artigo mostra como toomanage Olá artefatos para uma VM no laboratório.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Etapas tooadd laboratório tooa uma VM do Azure DevTest Labs
1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
1. Saudação de laboratórios, selecione lista laboratório Olá no qual você deseja toocreate Olá VM.  
1. No laboratório de saudação **visão geral** folha, selecione **+ adicionar**.  

    ![Botão Adicionar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Em Olá **escolher uma base** folha, selecione uma base para Olá VM.
1. Em Olá **Máquina Virtual** folha, digite um nome para a máquina virtual da nova Olá no hello **nome da máquina Virtual** caixa de texto.

    ![Folha VM de Laboratório](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Insira um **nome de usuário** que tem privilégios de administrador na máquina virtual de saudação.  
1. Se você quiser toouse uma senha armazenada em seu [armazenamento secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecione **usar um segredo salvo**e especifique um valor de chave que corresponde a tooyour segredo (senha). Caso contrário, digite uma senha no campo de texto de saudação rotulado **digite um valor**.
1. Olá **tipo de disco de máquina Virtual** determina qual tipo de disco de armazenamento será permitido para máquinas virtuais de saudação laboratório hello.
1. Selecione **tamanho da máquina Virtual** e selecione uma das Olá predefinidos itens que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate.
1. Selecione **artefatos** - lista de saudação de artefatos - e selecione Configurar artefatos Olá que deseja que a imagem base do tooadd toohello.
    **Observação:** se você for novo laboratórios de tooDevTest ou configurando artefatos, consulte toohello [adicionar um tooa de artefato existente VM](#add-an-existing-artifact-to-a-vm) seção e, em seguida, retornar aqui quando terminar.
1. Selecione **configurações avançadas** opções de opções e expiração de rede da VM do tooconfigure hello. 

   tooset uma opção de expiração, escolha Olá Calendário ícone toospecify uma data na qual Olá VM será excluída automaticamente.  Por padrão, a saudação VM nunca expirará. 
1. Se você quiser tooview ou copia modelo do Azure Resource Manager Olá, consulte toohello [do Azure Resource Manager Salvar modelo](#save-azure-resource-manager-template) seção e retornar aqui quando terminar.
1. Selecione **criar** tooadd Olá especificado laboratório toohello de VM.
1. folha de laboratório Olá exibe o status de saudação da criação da VM Olá - primeiro como **criando**, em seguida, como **executando** após Olá VM foi iniciada.

> [!NOTE]
> [Adicionar uma VM claimable](devtest-lab-add-claimable-vm.md) mostra como toomake Olá VM claimable para que ele esteja disponível para uso por qualquer usuário no laboratório de saudação.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Adicionar um tooa de artefato VM existente
Durante a criação de uma VM, você pode adicionar artefatos existentes. Cada laboratório inclui os artefatos de saudação repositório de artefato do público DevTest Labs, bem como artefatos que você tenha criado e adicionado tooyour possui o repositório de artefato.

* Azure DevTest Labs *artefatos* permitem que você especifique *ações* que são executadas quando Olá VM é provisionada, como execução de scripts do Windows PowerShell, executando comandos Bash e instalar o software.
* Artefato *parâmetros* permitem que você personalize o artefato de saudação para seu cenário específico

toodiscover como artefatos toocreate, consulte Olá artigo, [Saiba como tooauthor seus próprios artefatos para usam com o DevTest Labs](devtest-lab-artifact-author.md).

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
1. Saudação de laboratórios, selecione lista laboratório Olá contendo Olá VM com o qual você deseja toowork.  
1. Selecione **Minhas máquinas virtuais**.
1. Selecione Olá desejado VM.
1. Selecione **Artefatos**. 
1. Selecione **Aplicar artefatos**.
1. Em Olá **aplicar artefatos** folha, artefato Olá selecione desejar tooadd toohello VM.
1. Em Olá **adicionar artefato** folha, insira os valores de parâmetro hello necessárias e os parâmetros opcionais que você precisa.  
1. Selecione **adicionar** toohello de artefato e retornar Olá tooadd **aplicar artefatos** folha.
1. Continue adicionando artefatos à sua VM conforme o necessário.
1. Quando você tiver adicionado seus artefatos, você poderá [alterar ordem de saudação quais Olá artefatos são executados](#change-the-order-in-which-artifacts-are-run). Você também pode voltar muito[exibir ou modificar um artefato](#view-or-modify-an-artifact).
1. Quando você terminar de adicionar artefatos, selecione **Aplicar**

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Alterar ordem de saudação artefatos são executados
Por padrão, ações de saudação de artefatos de saudação são executadas em ordem de saudação na qual eles são adicionados toohello VM. Olá etapas a seguir ilustram como toochange Olá a ordem na qual Olá artefatos são executados.

1. Na parte superior de saudação do hello **aplicar artefatos** folha, link Olá selecione indicando o número Olá artefatos que foram adicionados toohello VM.
   
    ![Número de artefatos adicionados tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Em Olá **selecionado artefatos** folha, arrastar e soltar artefatos Olá em Olá desejado ordem. **Observação:** se você tiver dificuldade arrastando o artefato Olá, certifique-se de que você estiver arrastando da saudação lado esquerdo de artefato de saudação. 
1. Selecione **OK** quando tiver concluído.  

## <a name="view-or-modify-an-artifact"></a>exibir ou modificar um artefato
Olá etapas a seguir ilustram como tooview ou modificar parâmetros de saudação de um artefato:

1. Na parte superior de saudação do hello **aplicar artefatos** folha, link Olá selecione indicando o número Olá artefatos que foram adicionados toohello VM.
   
    ![Número de artefatos adicionados tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Em Olá **selecionado artefatos** folha, artefato Olá selecione que você deseja tooview ou edita.  
1. Em Olá **adicionar artefato** folha, faça quaisquer alterações necessárias e selecione **Okey** tooclose Olá **adicionar artefato** folha.
1. Selecione **Okey** tooclose Olá **selecionado artefatos** folha.

## <a name="save-azure-resource-manager-template"></a>Salvar modelo do Azure Resource Manager
Um modelo do Gerenciador de recursos do Azure fornece uma forma declarativa toodefine uma implantação repetível. Olá, as etapas a seguir explica como toosave Olá modelo do Gerenciador de recursos do Azure para Olá VM que está sendo criado.
Uma vez salvo, você pode usar modelo do Azure Resource Manager Olá muito[implantar novas VMs com o Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. Em Olá **Máquina Virtual** folha, selecione **modelo do ARM exibição**.
2. Em Olá **modelo de exibição do Azure Resource Manager** folha, o texto do modelo Olá select.
3. Copiar Olá texto selecionado toohello área de transferência.
4. Selecione **Okey** tooclose Olá **folha do modelo de Gerenciador de recursos de visualização do Azure**.
5. Abra um editor de texto.
6. Cole o texto do modelo de saudação da área de transferência hello.
7. Salve o arquivo hello para uso posterior.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Próximas etapas
* Uma vez Olá VM tiver sido criada, você pode se conectar toohello VM selecionando **conectar** na folha de saudação da VM.
* Saiba como muito[criar artefatos personalizados para sua VM do DevTest Labs](devtest-lab-artifact-author.md).
* Explorar Olá [Galeria de modelos do DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
