---
title: "Controle de acesso com base em aaaRole no portal do Azure de saudação | Microsoft Docs"
description: "Introdução ao gerenciamento de acesso com controle de acesso baseado em função no hello Portal do Azure. Use função atribuições tooassign permissões tooyour recursos."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Usar os recursos do controle de acesso baseado em função toomanage acesso tooyour assinatura do Azure
> [!div class="op_single_selector"]
> * [Gerenciar o acesso por usuário ou grupo](role-based-access-control-manage-assignments.md)
> * [Gerenciar o acesso por recurso](role-based-access-control-configure.md)

O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Azure. Usando o RBAC, você pode conceder somente a quantidade Olá de acesso que os usuários precisam tooperform seus trabalhos. Este artigo ajuda a colocar em funcionamento com RBAC em Olá portal do Azure. Se você quiser saber mais sobre como o RBAC ajuda você a gerenciar o acesso, confira [O que é Controle de Acesso Baseado em Função](role-based-access-control-what-is.md).

Dentro de cada assinatura, você pode conceder a too2000 atribuições de função. 

## <a name="view-access"></a>Exibir o acesso
Você pode ver quem tem acesso tooa recursos, grupo de recursos ou assinatura de folha do principal Olá [portal do Azure](https://portal.azure.com). Por exemplo, queremos toosee quem tem acesso tooone dos nossos grupos de recursos:

1. Selecione **grupos de recursos** na barra de navegação Olá Olá esquerda.  
    ![Grupos de recursos - ícone](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Nome de Select Olá Olá do grupo de recursos de saudação **grupos de recursos** folha.
3. Selecione **(IAM) do controle de acesso** no menu esquerdo hello.  
4. folha de controle de acesso de saudação lista todos os usuários, grupos e aplicativos que receberam o grupo de recursos de toohello de acesso.  
   
    ![Folha Usuários - acesso herdado versus atribuído - captura de tela](./media/role-based-access-control-configure/view-access.png)

Observe que algumas funções passam muito**esse recurso** enquanto outros são **herdadas** -o de outro escopo. Acesso está atribuído especificamente o grupo de recursos de toohello ou herdado de uma assinatura de pai de toohello de atribuição.

> [!NOTE]
> Administradores de assinatura clássico e coadministradores são considerados proprietários de assinatura Olá no novo modelo de RBAC hello.

## <a name="add-access"></a>Adicionar acesso
Conceda acesso de dentro de recurso hello, grupo de recursos ou assinatura que é Olá escopo de atribuição de função hello.

1. Selecione **adicionar** na folha de controle de acesso de saudação.  
2. Função hello selecione que você deseja tooassign de saudação **selecionar uma função** folha.
3. Selecione Olá usuário, grupo ou aplicativo no diretório que você deseja acesso toogrant ao. Você pode pesquisar o diretório Olá com nomes de exibição, endereços de email e identificadores de objeto.  
   
    ![Folha Adicionar usuários - pesquisar - captura de tela](./media/role-based-access-control-configure/grant-access2.png)
4. Selecione **Okey** toocreate atribuição de saudação. Olá **Adicionando usuário** pop-up controla o progresso de saudação.  
    ![Adicionando barra de progresso do usuário - captura de tela](./media/role-based-access-control-configure/addinguser_popup.png)

Depois de adicionar com êxito uma atribuição de função, ele será exibido na Olá **usuários** folha.

## <a name="remove-access"></a>Remover acesso
1. Focalize o cursor sobre o nome de saudação da atribuição de saudação que você deseja tooremove. Uma caixa de seleção é exibida próximo nome toohello.
2. Use Olá caixas de seleção tooselect uma ou mais atribuições de função.
2. Selecione **Remover**.  
3. Selecione **Sim** tooconfirm remoção de saudação.

Atribuições herdadas não podem ser removidas. Se você precisar tooremove uma atribuição herdada, você precisa toodo-lo no hello escopo em que a atribuição de função hello foi criada. Em Olá **escopo** coluna, next muito**herdadas** há um link que utiliza recursos toohello onde essa função foi atribuída. Vá na lista de recursos de toohello atribuição de função tooremove hello.

![Folha Usuários - botão remover desativa o acesso herdado - captura de tela](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Acesso de toomanage outras ferramentas
Você pode atribuir funções e gerenciar o acesso com comandos de RBAC do Azure em ferramentas diferentes Olá portal do Azure.  Siga Olá links toolearn mais sobre os pré-requisitos de saudação e começar a trabalhar com comandos do hello RBAC do Azure.

* [PowerShell do Azure](role-based-access-control-manage-access-powershell.md)
* [Interface de linha de comando do Azure](role-based-access-control-manage-access-azure-cli.md)
* [API REST](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Próximas etapas
* [Criar relatório de histórico de alterações de acesso](role-based-access-control-access-change-history-report.md)
* Consulte Olá [funções internas de RBAC](role-based-access-built-in-roles.md)
* Defina suas próprias [Funções personalizadas no RBAC do Azure](role-based-access-control-custom-roles.md)

