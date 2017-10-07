---
title: "toocontrol de controle de acesso baseado em função (RBAC) aaaAzure toocreate de direitos de acesso e gerenciar solicitações de suporte | Microsoft Docs"
description: "Toocontrol de controle de acesso baseado em função (RBAC) do Azure toocreate direitos de acesso e gerenciar solicitações de suporte"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Toocontrol de controle de acesso baseado em função (RBAC) do Azure toocreate direitos de acesso e gerenciar solicitações de suporte

O [RBAC (Controle de Acesso Baseado em Função)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permite gerenciamento de acesso refinado para o Azure.
Suporte à criação de solicitação no hello portal do Azure, [portal.azure.com](https://portal.azure.com), usa toodefine de modelo RBAC do Azure que pode criar e gerenciar solicitações de suporte.
Acesso atribuindo Olá apropriado RBAC função toousers, grupos e aplicativos em um determinado escopo, pode ser uma assinatura, o grupo de recursos ou um recurso.

Vejamos um exemplo: como proprietário do grupo de recursos com permissões de leitura no escopo de assinatura hello, você pode gerenciar todos os recursos de saudação no grupo de recursos de saudação, como sites, máquinas virtuais e sub-redes.
No entanto, quando você tenta toocreate uma solicitação de suporte no recurso de máquina virtual hello, encontrar hello erro a seguir

![Erro de assinatura](./media/create-manage-support-requests-using-access-control/subscription-error.png)

Gerenciamento de solicitação de suporte, você precisa de permissão de gravação ou uma função que tenha Olá suporte ação Microsoft.Support/* no hello assinatura escopo toobe capaz de toocreate e gerenciar solicitações de suporte.

Olá artigo a seguir explica como você pode usar toocreate de controle de acesso baseado em função (RBAC) personalizado do Azure e gerenciar solicitações de suporte em Olá portal do Azure.

## <a name="getting-started"></a>Introdução

Usando o exemplo hello acima, você seria capaz de toocreate uma solicitação de suporte para o recurso se você foram atribuídos a uma função RBAC personalizada na assinatura de saudação pelo proprietário da assinatura hello.
[Funções personalizadas de RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) podem ser criados usando o PowerShell do Azure, Azure Interface de linha de comando (CLI) e Olá API REST.

propriedade de ações de saudação de uma função personalizada especifica hello Azure operações toowhich Olá função concede acesso.
toocreate uma função personalizada para o gerenciamento de solicitação de suporte, uma função de saudação deve ter ação Olá Microsoft.Support/*

Aqui está um exemplo de uma função personalizada, você pode usar toocreate e gerenciar solicitações de suporte.
Chamamos essa função "Colaborador de solicitação de suporte" e isso é como fazemos referência a função personalizada toohello neste artigo.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Siga etapas Olá descritas em [este vídeo](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn como toocreate uma função personalizada para sua assinatura.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Criar e gerenciar solicitações de suporte em Olá portal do Azure

Vejamos um exemplo – você é proprietário de saudação de assinatura "Visual Studio assinatura do MSDN."
Se o ponto a ponto que é um toosome de proprietário do recurso Olá de grupos de recursos na assinatura e tem a assinatura de toohello de permissão de leitura.
Você deseja toogive acesso tooyour ponto a ponto, Joe, Olá capacidade toocreate e gerenciar tíquetes de suporte para recursos de saudação sob essa assinatura.

1. Olá primeira etapa é toogo toohello assinatura e em "Configurações" você ver uma lista de usuários. Clique em usuário Olá Joe quem tem acesso de leitor em Olá assinatura e permite atribuir um novo toohim de função personalizada.

    ![Adicionar função](./media/create-manage-support-requests-using-access-control/add-role.png)

2. Na folha de "Usuários" Olá, clique em "Adicionar". Função personalizada de hello "Colaborador de solicitação de suporte" Selecione na lista de saudação de funções

    ![Adicione a função colaborador de suporte](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Depois de selecionar o nome da função hello, clique em "Adicionar usuários" e insira as credenciais de email de Joe hello. Clique em “Selecionar”

    ![Adicionar usuários](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Clique em "Okey" tooproceed

    ![Adicionar acesso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. Agora você verá que o usuário Olá com função personalizada recém-adicionado hello "Suporte de solicitação Colaborador" na assinatura Olá para o qual você é proprietário de saudação

    ![Usuário adicionado](./media/create-manage-support-requests-using-access-control/user-added.png)

    Quando Joe faz logon no portal de hello, ele vê Olá assinatura toowhich que ele foi adicionado.

7. José clica em "Nova solicitação de suporte" da folha de "Ajuda e suporte" hello e pode criar solicitações de suporte para "Visual Studio Ultimate com MSDN"

    ![Nova solicitação de suporte](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Clique em "Todas as solicitações de suporte" Joe pode ver Olá lista solicitações de suporte criado para esta assinatura ![exibição de detalhes do caso](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Remover o acesso de solicitação de suporte em Olá portal do Azure

Assim como é possível toogrant acesso tooa usuário toocreate e gerenciar solicitações de suporte, é possível tooremove acesso usuário de saudação também.
tooremove Olá toocreate de capacidade e gerenciar solicitações de suporte, vá toohello assinatura, clique em "Configurações" e clique em Olá usuário (nesse caso, Pedro).
Clique em nome da função hello, "Colaborador de solicitação de suporte" e clique em "Remover"

![Remover acesso a solicitação de suporte](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Quando Joe fizer logon no portal de toohello e tenta toocreate uma solicitação de suporte, ele encontra Olá erro a seguir

![Erro de assinatura-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Joe não conseguirá ver as solicitações suporte quando clicar em "Todas as solicitações de suporte"

![exibição de detalhes do caso-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
