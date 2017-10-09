---
title: "configurações de imagens do Azure Marketplace aaaConfigure no Azure DevTest Labs | Microsoft Docs"
description: Configure quais imagens do Azure Marketplace podem ser usadas ao criar uma VM no Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Definir configurações de imagem do Azure Marketplace no Azure DevTest Labs
DevTest Labs dá suporte ao criar máquinas virtuais baseadas em imagens do Azure Marketplace dependendo de como você configurou o Azure Marketplace imagens toobe usado no laboratório. Este artigo mostra como toospecify que, se houver, imagens do Azure Marketplace podem ser usado ao criar máquinas virtuais em um laboratório. Isso garante que sua equipe tem apenas acesso toohello Marketplace imagens. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Selecionar quais imagens do Azure Marketplace são permitidas durante a criação de uma VM
1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello. 
4. Na folha do laboratório hello, selecione **políticas e configurações**.
5. Na folha **Configurações e políticas** do laboratório, em **Bases da Máquina Virtual**, selecione **Imagens do Marketplace**.
6. Especifique se deseja que todos os Olá qualificado toobe de imagens do Azure Marketplace disponível para uso como uma base de uma nova VM. Se você selecionar **Sim**, em seguida, todas as imagens do Azure Marketplace Olá que atendem a Olá a todos os critérios a seguir são permitidos em laboratório hello:
   
   * imagem de saudação cria uma única VM, **e**
   * imagem de saudação usa o Azure Resource Manager tooprovision VMs, **e**
   * imagem Olá não exige a compra um plano de licenciamento adicionais
     
    Se você não quiser que nenhum toobe imagens permitido, ou você deseja toospecify quais imagens podem ser usados, selecione **não**.
     
     ![Opção tooallow todos os toobe de imagens do Marketplace usado como base imagens para máquinas virtuais](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Se você selecionar **não** toohello anterior etapa, hello **permitidos imagens/selecionar todos os** caixa de seleção está habilitada. 
   Você pode usar essa opção junto com hello pesquisa caixa tooquickly selecionar ou desmarcar todos os itens de saudação exibidos na lista de saudação.
   * Selecione imagens do Azure Marketplace Olá tooallow você deseja para a criação de VM individualmente, marcando a caixa de seleção de cada imagem correspondente.
   * Não selecione nada na lista de saudação se você não quiser tooallow qualquer toobe de imagens do Azure Marketplace usado no laboratório de saudação.
   
    ![Você pode especificar quais imagens do Marketplace podem ser usadas como imagens base para VMs](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Depois de ter configurado como imagens do Azure Marketplace são permitidas durante a criação de uma máquina virtual, o hello próxima etapa é muito[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).

