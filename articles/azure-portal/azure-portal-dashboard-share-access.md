---
title: "aaaShare Azure painéis de portal usando o RBAC | Microsoft Docs"
description: "Este artigo explica como tooshare um painel no hello portal do Azure usando o controle de acesso baseado em função."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Compartilhar painéis do Azure usando o Controle de Acesso Baseado em Função
Depois de configurar um painel, você pode publicá-lo e compartilhá-lo com outros usuários na sua organização. Permitir que outras pessoas tooview seu painel usando o Azure [controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md). Atribuir um usuário ou grupo de função tooa dos usuários, e essa função define se os usuários podem exibir ou modificar Olá publicados no painel. 

Todos os painéis publicados são implementados como recursos do Azure, o que significa que eles existem como itens gerenciáveis dentro de sua assinatura e estão contidos em um grupo de recursos.  Do ponto de vista do controle de acesso, os painéis não são diferentes de outros recursos, como uma máquina virtual ou uma conta de armazenamento.

> [!TIP]
> Blocos individuais no painel de saudação impõem seus próprios requisitos de controle de acesso com base nos recursos de saudação que elas sejam exibidas.  Portanto, você pode criar um painel que é compartilhado amplamente ainda proteger dados de saudação em blocos individuais.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Noções básicas de controle de acesso de painéis
Com o controle de acesso baseado em função (RBAC), você pode atribuir usuários tooroles em três diferentes níveis de escopo:

* subscription
* grupo de recursos
* recurso

permissões de saudação que atribuir são herdadas de assinatura para baixo toohello recursos. Olá publicados no painel é um recurso. Portanto, você talvez já tenha tooroles usuários atribuídos para a assinatura de saudação que também funcionam para Olá publicados no painel. 

Aqui está um exemplo.  Digamos que você tem uma assinatura do Azure e vários membros da equipe tiverem sido atribuídos a funções de saudação do **proprietário**, **Colaborador**, ou **leitor** para assinatura de saudação. Os usuários que são proprietários ou colaboradores são capaz de toolist, exibir, criar, modificar ou excluir painéis em assinatura hello.  Os usuários que são leitores são capaz de toolist e exibir os painéis, mas não podem modificar ou excluí-los.  Os usuários com acesso de leitor estão toomake capaz de edições locais tooa publicados no painel (como, ao solucionar um problema), mas não é possível toopublish server de back toohello essas alterações.  Eles terão Olá opção toomake uma cópia privada de painel Olá para si mesmos

No entanto, você também pode atribuir o grupo de recursos de toohello de permissões que contém vários painéis ou tooan individual do painel. Por exemplo, você pode decidir que um grupo de usuários deve ter permissões limitadas em assinatura Olá mas maior painel específico tooa de acesso. Você atribui a função de tooa esses usuários para esse painel. 

## <a name="publish-dashboard"></a>Publicar painel
Vamos supor que você terminar de configurar um painel que você deseja tooshare com um grupo de usuários em sua assinatura. etapas de saudação abaixo descrevem um grupo personalizado chamado gerenciadores de armazenamento, mas você pode nomear o grupo como desejar. Para obter informações sobre como criar um grupo do Active Directory e adicionar usuários toothat grupo, consulte [gerenciar grupos no Active Directory do Azure](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. No painel de saudação, selecione **compartilhamento**.
   
     ![selecionar compartilhamento](./media/azure-portal-dashboard-share-access/select-share.png)
2. Antes de atribuir acesso, você deve publicar painel hello. Por padrão, painel Olá será chamado de grupo de recursos publicados tooa **painéis**. Selecione **Publicar**.
   
     ![Publicar](./media/azure-portal-dashboard-share-access/publish.png)

Seu painel agora foi publicado. Se permissões Olá herdadas de assinatura de saudação são adequadas, não é necessário toodo nada mais. Outros usuários na sua organização serão capaz de tooaccess e modificar o painel de saudação com base em suas funções de nível de assinatura. No entanto, para este tutorial, vamos atribuir um grupo de função tooa dos usuários para esse painel.

## <a name="assign-access-tooa-dashboard"></a>Atribuir o painel de controle do acesso tooa
1. Depois de publicar o painel hello, selecione **gerenciar usuários**.
   
     ![gerenciar usuários](./media/azure-portal-dashboard-share-access/manage-users.png)
2. Você verá uma lista de usuários existentes que já estão atribuídos a uma função desse painel. A lista de usuários existentes será diferente de imagem de saudação abaixo. Provavelmente, atribuições de saudação são herdadas da assinatura de saudação. tooadd um novo usuário ou grupo, selecione **adicionar**.
   
     ![adicionar usuário](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Selecione a função de saudação que representa as permissões de saudação você gostaria que toogrant. Neste exemplo, selecione **Colaborador**.
   
     ![escolher função](./media/azure-portal-dashboard-share-access/select-role.png)
4. Selecione o usuário hello ou grupo que você deseja tooassign toohello função. Se você não vir usuário Olá ou grupo que você está procurando na lista de hello, use a caixa de pesquisa de saudação. A lista de grupos disponíveis dependem grupos Olá que você criou no seu Active Directory.
   
     ![selecionar usuário](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Quando você terminar de adicionar usuários ou grupos, selecione **OK**. 
6. nova atribuição de saudação é adicionada toohello lista de usuários. Observe que seu **Acesso** é listado como **Atribuído**, em vez de **Herdado**.
   
     ![funções atribuídas](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Próximas etapas
* Para obter uma lista de funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).
* toolearn sobre o gerenciamento de recursos, consulte [recursos de gerenciamento Azure por meio do portal](resource-group-portal.md).

