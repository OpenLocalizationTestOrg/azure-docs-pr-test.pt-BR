---
title: "aaaCreate um laboratório no Azure DevTest Labs | Microsoft Docs"
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
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Criar Laboratórios de Desenvolvimento/Teste do Azure
Um laboratório no Azure DevTest Labs é infraestrutura Olá que abrange um grupo de recursos, como máquinas virtuais (VMs), que lhe permite melhor gerenciar esses recursos, especificando limites e cotas. Este artigo orienta você pelo processo de saudação de criação de um laboratório com hello portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
toocreate um laboratório, você precisa:

* Uma assinatura do Azure. toolearn sobre as opções de compra do Azure, consulte [como toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). Você deve ser o proprietário de saudação do laboratório de Olá Olá assinatura toocreate.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Etapas toocreate um laboratório no Azure DevTest Labs
Olá, as etapas a seguir ilustra como toouse Olá toocreate portal do Azure um laboratório no Azure DevTest Labs. 

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. No menu principal do hello no lado esquerdo do hello, selecione **mais serviços** (final Olá Olá lista).

    ![Opção do menu Mais serviços](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Na lista de saudação de serviços disponíveis, **DevTest Labs**.
1. Em Olá **DevTest Labs** folha, selecione **adicionar**.
   
    ![Adicionar um laboratório](./media/devtest-lab-create-lab/add-lab-button.png)

1. Em Olá **criar um laboratório de DevTest** folha:
   
    1. Insira um **nome do laboratório** laboratório novo hello.
    2. Selecione Olá **assinatura** tooassociate com laboratório hello.
    3. Selecione um **local** no laboratório de saudação que toostore.
    4. Selecione **desligamento automático** toospecify tooenable - e definir parâmetros de saudação para - Olá automáticas desligar do laboratório Olá todas as VMs. Hello desligamento automático é principalmente uma economia de custo de recurso no qual você pode especificar quando deseja Olá VM tooautomatically ser desligada. Você pode alterar as configurações de desligamento automático depois de criar o laboratório Olá seguindo Olá etapas descritas no artigo Olá, [gerenciar todas as políticas para um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Selecione **tooDashboard Pin** se você deseja um atalho de saudação laboratório tooappear no painel do portal hello.
    6. Selecione **opções de automação** tooget modelos de Gerenciador de recursos do Azure para a automação de configuração. 
    7. Selecione **Criar**. Depois de selecionar **criar**, Olá **DevTest Labs** exibe folha. Você pode monitorar o status de saudação do processo de criação de laboratório Olá observando Olá **notificações** área. Depois de concluído, atualize o laboratório do hello página toosee Olá recém-criado na lista de saudação de laboratórios.  
    
    ![Criar uma folha de laboratório](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Depois que você criou seu laboratório, aqui estão alguns próxima tooconsider de etapas:

* [Laboratório de tooa acesso seguro](devtest-lab-add-devtest-user.md).
* [Definir políticas de laboratório](devtest-lab-set-lab-policy.md).
* [Criar um modelo de laboratório](devtest-lab-create-template.md).
* [Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).
* [Adicionar uma VM com o laboratório de tooa artefatos](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

