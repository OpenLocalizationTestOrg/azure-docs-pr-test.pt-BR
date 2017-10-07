---
title: "atribuições de acesso de recursos do Azure aaaView | Microsoft Docs"
description: "Exibir e gerenciar todas as atribuições de controle de acesso baseado em função Olá para qualquer usuário ou grupo no hello portal do Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Exibir as atribuições de acesso para usuários e grupos no hello portal do Azure
> [!div class="op_single_selector"]
> * [Gerenciar o acesso por usuário ou grupo](role-based-access-control-manage-assignments.md)
> * [Gerenciar o acesso por recurso](role-based-access-control-configure.md)

Com controle de acesso baseado em função (RBAC) em hello Azure Active Directory (AD do Azure), você pode gerenciar o acesso tooyour Azure recursos. 

Acesso atribuído com RBAC é refinado porque você pode restringir as permissões de saudação de duas maneiras:

* **Escopo:** atribuições de função RBAC são assinatura específica tooa no escopo, o grupo de recursos ou o recurso. Um usuário recebe acesso tooa único recurso não é possível acessar outros recursos Olá mesma assinatura.
* **Função:** no escopo de saudação de atribuição de saudação, o acesso é reduzido ainda mais atribuindo uma função. Funções podem ser de alto nível, como proprietário, ou específicas, como leitor de máquina virtual.

Funções podem ser atribuídas somente de dentro de assinatura Olá, grupo de recursos ou recurso que é Olá escopo de atribuição de saudação. Mas você pode exibir todas as atribuições de acesso de saudação para um determinado usuário ou grupo em um único lugar. Você pode ter até too2000 atribuições de função em cada assinatura. 

Obter mais informações sobre como muito[usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Exibir atribuições de acesso
toolook backup atribuições de acesso Olá para um único usuário ou grupo, iniciar no Active Directory do Azure no hello [portal do Azure](http://portal.azure.com).

1. Selecione **Azure Active Directory**. Se essa opção não estiver visível na sua lista de navegação, selecione **mais serviços** e, em seguida, role para baixo toofind **Active Directory do Azure**.
2. Selecione **Usuários e Grupos** e **Todos os usuários** ou **Todos os grupos**. Para este exemplo, vamos focar em usuários individuais.
    ![Gerenciar usuários e grupos no Azure Active Directory – captura de tela](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Pesquisa de usuário Olá por nome ou o nome de usuário.
4. Selecione **recursos do Azure** na folha de usuário hello. Todas as atribuições de acesso Olá para esse usuário são exibidos.

### <a name="read-permissions-tooview-assignments"></a>Tooview atribuições de permissões de leitura
Esta página mostra apenas as atribuições de acesso de saudação que você tenha permissão tooread. Por exemplo, você tem acesso de leitura toosubscription A e vá toohello toocheck de folha de recursos do Azure atribuições do usuário. É possível ver as atribuições de acesso dele para a assinatura A, mas não é possível ver que ele também tem acesso a atribuições na assinatura B.

## <a name="delete-access-assignments"></a>Excluir atribuições de acesso
Desta folha, você pode excluir atribuições de acesso que foram atribuídas diretamente tooa usuário ou grupo. Se a atribuição de acesso de saudação foi herdada de um grupo pai, você precisa toogo toohello recursos ou assinatura e gerenciar a atribuição de saudação existe.

1. Na lista de saudação de todas as atribuições de acesso de saudação para um usuário ou grupo, selecione Olá um deseja toodelete.
2. Selecione **remover** e **Sim** tooconfirm.
    ![Remover atribuição de acesso – captura de tela](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Próximas etapas

* Introdução ao controle de acesso baseado em função muito[usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](role-based-access-control-configure.md)
* Consulte Olá [funções internas de RBAC](role-based-access-built-in-roles.md)

