---
title: "fórmulas de aaaManage no Azure DevTest Labs toocreate VMs | Microsoft Docs"
description: "Saiba como tooupdate e remova fórmulas do Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Gerenciar fórmulas do Azure DevTest Labs

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Este artigo ilustra como toocreate uma fórmula de uma base (imagem personalizada, imagem do Marketplace ou outra fórmula) ou em uma VM existente. Este artigo também orienta você por meio do gerenciamento de fórmulas existentes.

## <a name="create-a-formula"></a>Criar uma fórmula
Qualquer pessoa com DevTest Labs *usuários* permissões é capaz de toocreate VMs usando uma fórmula como base. Há duas maneiras de toocreate fórmulas: 

* De uma base - Use quando desejar toodefine todas as características de saudação da fórmula hello.
* De um laboratório existente VM - Use quando desejar toocreate uma fórmula com base nas configurações de saudação de uma VM existente.

Para saber mais sobre como adicionar usuários e permissões, consulte [Adicionar proprietários e usuários no Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Criar uma fórmula de uma base
Olá etapas a seguir o guiará Olá o processo de criação de uma fórmula de uma imagem personalizada, imagem do Marketplace ou outra fórmula.

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.

3. Saudação de laboratórios, selecione lista laboratório desejado hello.  

4. Na folha do laboratório hello, selecione **fórmulas (bases reutilizáveis)**.
   
    ![Menu Fórmula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Em Olá **fórmulas** folha, selecione **+ adicionar**.
   
    ![Adicionar uma fórmula](./media/devtest-lab-create-formulas/add-formula.png)

6. Em Olá **escolher uma base** folha, base select hello (imagem personalizada, imagem do Marketplace ou fórmula) do qual você deseja a fórmula de saudação toocreate.
   
    ![Lista de base](./media/devtest-lab-create-formulas/base-list.png)

7. Em Olá **criar fórmula** folha, especifique Olá valores a seguir:
   
    * **Nome da fórmula** – digite um nome para a fórmula. Esse valor é exibido na lista de saudação de base imagens quando você cria uma máquina virtual. nome da saudação é validado como digitá-lo e se não é válido, uma mensagem indica que os requisitos de saudação para um nome válido.
    * **Descrição** – digite uma descrição relevante para a fórmula. Esse valor está disponível no menu de contexto da fórmula hello quando você cria uma máquina virtual.
    * **Nome de usuário** – insira um nome de usuário para receber privilégios de administrador.
    * **Senha** - Insira - ou selecione na lista suspensa de saudação - um valor que está associado ao segredo hello (senha) que você deseja toouse para usuário especificado hello. Para obter mais informações sobre segredos hello, consulte [Azure DevTest Labs: repositório pessoal do segredo](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Tipo de disco de máquina virtual** – Especifique ou (unidade de disco rígido) de HDD ou SSD (unidade de estado sólido) tooindicate qual armazenamento em disco tipo é permitida para máquinas virtuais de saudação provisionadas usando essa imagem base.
    * * * VM tamanho * * - selecione um dos itens de saudação predefinido que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate. 
    * **Artefatos** -Olá selecione tooopen **adicionar artefatos** folha, em que você selecionar e configurar artefatos Olá que deseja que a imagem base do tooadd toohello. Para saber mais sobre artefatos, consulte [Gerenciar artefatos de VM no Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Configurações avançadas** -Olá selecione tooopen **avançado** folha de onde você configura Olá configurações a seguir:
        * **Rede virtual** -especificar Olá desejado de rede virtual.
        * **Subrede** -especifique a sub-rede de saudação desejada.    
        * **Configuração do endereço IP** -Especifique se deseja Olá público, privado ou compartilhado endereços IP. Para obter mais informações sobre endereços IP compartilhados, consulte [Noções básicas dos endereços IP compartilhados no Azure DevTest Labs](./devtest-lab-shared-ip.md).
        * **Tornar essa máquina claimable** -fazer uma máquina "claimable" significa que ele não será atribuído propriedade em tempo de saudação da criação. Em vez disso, os usuários do laboratório será máquina de saudação tootake capaz de propriedade ("declaração") na folha do laboratório hello.     
    * **Imagem** -este campo exibe o nome da imagem base do hello selecionada na folha de saudação anterior. 
     
       ![Criar fórmula](./media/devtest-lab-create-formulas/create-formula.png)

8. Selecione **criar** toocreate fórmula de saudação.

9. Quando a fórmula Olá tiver sido criada, ele exibe na lista Olá Olá **fórmulas** folha.

### <a name="create-a-formula-from-a-vm"></a>Criar uma fórmula de uma VM
Olá etapas a seguir orientará você durante saudação processo de criação de uma fórmula com base em uma VM existente. 

> [!NOTE]
> toocreate uma fórmula de uma VM, Olá VM deve ter sido criado após 30 de março de 2016. 
> 
> 

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello.  
4. No laboratório de saudação **visão geral** folha, selecione Olá VM da qual você deseja toocreate fórmula de saudação.
   
    ![VMs do Labs](./media/devtest-lab-create-formulas/my-vms.png)
5. Na folha de saudação da VM, selecione **criar fórmula (base reutilizável)**.
   
    ![Criar fórmula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Em Olá **criar fórmula** folha, insira um **nome** e **descrição** para sua nova fórmula.
   
    ![Folha Criar fórmula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Selecione **Okey** toocreate fórmula de saudação.

## <a name="modify-a-formula"></a>Modificar uma Fórmula
toomodify uma fórmula, siga estas etapas:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello.  
4. Na folha do laboratório hello, selecione **fórmulas (bases reutilizáveis)**.
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Em Olá **fórmulas de laboratório** folha, a fórmula Olá selecione desejar toomodify.
6. Em Olá **atualizar fórmula** folha, faça edições de saudação desejada e selecione **atualização**.

## <a name="delete-a-formula"></a>Excluir uma fórmula
toodelete uma fórmula, siga estas etapas:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello.  
4. Laboratório Olá **configurações** folha, selecione **fórmulas**.
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Em Olá **fórmulas de laboratório** folha, selecione Olá toohello de reticências à direita da fórmula Olá desejar toodelete.
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. No menu de contexto da fórmula hello, selecione **excluir**.
   
    ![Menu de contexto da Fórmula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Selecione **Sim** toohello caixa de diálogo de confirmação de exclusão.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas
* [Imagens personalizadas ou fórmulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Próximas etapas
Depois de criar uma fórmula para uso durante a criação de uma máquina virtual, a próxima etapa de saudação é muito[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).

