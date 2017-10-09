---
title: grupos de aaaManaging no Active Directory do Azure | Microsoft Docs
description: "Como toocreate e gerenciar grupos toomanage Azure usuários usando o Active Directory do Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Gerenciamento de grupos no Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-groups-create-azure-portal.md)
> * [Portal clássico do Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Um dos recursos de saudação do gerenciamento de usuários do Active Directory do Azure (AD do Azure) é grupos de toocreate de capacidade de saudação de usuários. Realizar tarefas de gerenciamento de tooperform um grupo como a atribuição de permissões ou licenças tooa o número de usuários de uma vez. Você também pode usar grupos tooassign permissão de acesso

* Recursos como objetos no diretório Olá
* Diretório de toohello externo de recursos, como aplicativos SaaS, os serviços do Azure, sites do SharePoint ou recursos locais

Além disso, um proprietário do recurso também pode atribuir o grupo de AD do Azure tooan no acesso tooa recursos pertencente a outra pessoa. Essa atribuição concede aos membros de saudação do recurso grupo acesso toohello. Em seguida, proprietário de saudação do grupo de saudação gerencia a associação no grupo de saudação. Efetivamente, Olá recurso proprietário delegados toohello proprietário do hello grupo Olá permissão tooassign usuários tootheir recurso.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como toomanage os grupos no Centro de administração de saudação do AD do Azure, consulte [criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Como faço para criar um grupo?
Dependendo da saudação toowhich de serviços que sua organização tenha assinado, você pode criar um grupo usando uma das seguintes hello:

* Olá portal clássico do Azure
* portal de conta Olá Office 365
* portal de conta do Windows Intune Olá

Descreveremos tarefas como executadas no hello portal clássico do Azure. Para obter mais informações sobre como usar portais do Azure não toomanage seu diretório do AD do Azure, consulte [administrando seu diretório do AD do Azure](active-directory-administer.md).

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.
2. Selecione Olá **grupos** guia.
3. Selecione **Adicionar Grupo**.
4. Em Olá **adicionar grupo** janela, especifique o nome de saudação e Olá descrição de um grupo.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Como faço para adicionar ou remover usuários individuais em um grupo de segurança?
**tooadd um grupo de tooa de usuário individuais**

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.
2. Selecione Olá **grupos** guia.
3. Abra Olá grupo toowhich tooadd membros. Olá abrir **membros** guia da saudação grupo selecionado se ele ainda não estiver exibindo.
4. Selecione **Adicionar Membros**.
5. Em Olá **adicionar membros** página, o nome de saudação select de Olá usuário ou grupo que você deseja tooadd como um membro desse grupo. Certifique-se de que esse nome está adicionado toohello **selecionados** painel.

**tooremove um usuário individual de um grupo**

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.
2. Selecione Olá **grupos** guia.
3. Abra o grupo de saudação do qual você deseja tooremove membros.
4. Selecione Olá **membros** guia, nome selecione Olá Olá membro que você deseja tooremove deste grupo e, em seguida, clique em **remover**.
5. No prompt de hello, confirme se deseja tooremove esse membro do grupo de saudação.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Como gerenciar a associação de saudação de um grupo dinamicamente?
No AD do Azure, você pode facilmente configurar um toodetermine regra simples quais usuários são membros de toobe do grupo de saudação. Uma regra simples é aquele que faz uma única comparação. Por exemplo, se um grupo for atribuído tooa aplicativo SaaS, você pode configurar uma regra tooadd os usuários que têm um cargo de "Representante de vendas". Essa regra, em seguida, concede acesso toothis usuários de tooall de aplicativos SaaS com esse cargo em seu diretório.

Quando os atributos de uma alteração de usuário, sistema Olá avalia todas as regras de grupo dinâmico em um toosee de diretório se a alteração de atributo de saudação do usuário Olá dispararia qualquer grupo adiciona ou remove. Se um usuário satisfizer uma regra em um grupo, eles são adicionados como um membro do grupo toothat. Se eles não atendem mais regra Olá de um grupo, de que ele é membro, eles serão removidos como um membros desse grupo.

> [!NOTE]
> Você pode configurar uma regra de associação dinâmica em grupos de segurança ou em grupos do Office 365. Atualmente não há suporte a associações de grupo aninhado para tooapplications atribuição baseada em grupo.
>
> Associações dinâmicas para grupos requerem uma toobe de licença do Azure AD Premium atribuída a
>
> * administrador de saudação que gerencia a regra Olá em um grupo
> * Todos os membros do grupo de saudação
>
>

**associação dinâmica tooenable para um grupo**

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.
2. Selecione Olá **grupos** guia e grupo Olá abrir deseja tooedit.
3. Selecione Olá **configurar** guia e, em seguida, defina **habilitar associações dinâmicas** muito**Sim**.
4. Configurar uma única regra simple para Olá grupo toocontrol a associação dinâmica para funções desse grupo. Verifique se Olá **adicionar usuários onde** opção está selecionada e, em seguida, selecione uma propriedade de usuário na lista de hello (por exemplo, departamento, jobTitle, etc.)
5. Em seguida, selecione uma condição (Não É Igual a, Igual a, Não Começa com, Começa com, Não Contém, Contém, Não Corresponde, Corresponde).
6. Especifique um valor de comparação para a propriedade de usuário de saudação selecionada.

toolearn sobre como toocreate *avançados* regra (regras que podem conter várias comparações) para a associação de grupo dinâmico, consulte [usar atributos toocreate regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Informações adicionais
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
