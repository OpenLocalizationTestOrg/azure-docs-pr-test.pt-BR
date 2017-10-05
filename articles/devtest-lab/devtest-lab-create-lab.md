---
title: "Criar um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Crie um laboratório no Azure DevTest Labs para máquinas virtuais"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Criar Laboratórios de Desenvolvimento/Teste do Azure
Um laboratório no Azure DevTest Labs é a infraestrutura que abrange um grupo de recursos, como Máquinas Virtuais (VMs), que permite gerenciar melhor esses recursos especificando limites e cotas. Este artigo explica o processo de criação de um laboratório usando o portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Para criar um laboratório, você precisa de:

* Uma assinatura do Azure. Para saber mais sobre as opções de compra do Azure, consulte [Como comprar o Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [Avaliação gratuita de um mês](https://azure.microsoft.com/pricing/free-trial/). Você deve ser o proprietário da assinatura para criar o laboratório.

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a>Etapas para criar um laboratório n o Azure DevTest Labs
As etapas a seguir ilustram como usar o portal do Azure para criar um laboratório no Azure DevTest Labs. 

1. Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. No menu principal à esquerda, selecione **Mais Serviços** (na parte inferior da lista).

    ![Opção do menu Mais serviços](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Na lista de serviços disponíveis, **DevTest Labs**.
1. Na folha **Laboratórios de Desenvolvimento/Teste**, selecione **Adicionar**.
   
    ![Adicionar um laboratório](./media/devtest-lab-create-lab/add-lab-button.png)

1. Na folha **Criar um Laboratório de Desenvolvimento/Teste** :
   
    1. Insira um **Nome do Laboratório** para o novo laboratório.
    2. Selecione a **Assinatura** para associar ao laboratório.
    3. Selecione um **Local** no qual o laboratório será armazenado.
    4. Selecione **Desligamento Automático** para especificar se você deseja ativar e definir os parâmetros de desligamento automático de todas as VMs do laboratório. O recurso de autodesligamento é principalmente um recurso de economia de custos no qual você pode especificar quando deseja que a VM seja desligada automaticamente. Você pode alterar as configurações de autodesligamento após criar o laboratório seguindo as etapas descritas no artigo [Gerenciar todas as políticas de um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Selecione **Fixar no painel** se você deseja exibir um atalho do laboratório no painel do portal.
    6. Selecione **Opções de automação** para obter modelos do Azure Resource Manager para automação da configuração. 
    7. Selecione **Criar**. Depois de selecionar **Criar**, a folha **DevTest Labs** é exibida. Você pode monitorar o status do processo de criação do laboratório vendo a área **Notificações**. Depois de concluído, atualize a página para ver o laboratório recém-criado na lista de laboratórios.  
    
    ![Criar uma folha de laboratório](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Depois de criar seu laboratório, aqui estão algumas das próximas etapas a serem consideradas:

* [Proteger o acesso a um laboratório](devtest-lab-add-devtest-user.md).
* [Definir políticas de laboratório](devtest-lab-set-lab-policy.md).
* [Criar um modelo de laboratório](devtest-lab-create-template.md).
* [Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).
* [Adicionar uma VM com artefatos a um laboratório](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

