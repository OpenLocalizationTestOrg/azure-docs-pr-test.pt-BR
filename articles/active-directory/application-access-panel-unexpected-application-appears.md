---
title: "aplicativos aaaHow aparecem no painel de acesso Olá | Microsoft Docs"
description: "Solução de problemas que um aplicativo é exibido no painel de acesso de saudação"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Como os aplicativos aparecem no painel de acesso Olá

Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao. Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello. Olá administrador pode provisionar Olá toohello usuário do aplicativo diretamente ou tooa grupo que um usuário faz parte do resultando em um aplicativo hello que aparecem no painel de acesso do usuário hello.

## <a name="general-issues-toocheck-first"></a>Geral emite toocheck primeiro

-   Se um aplicativo foi removido apenas um usuário ou grupo Olá usuário é membro de, tente toosign e sair novamente no painel de acesso do usuário Olá após toosee de alguns minutos se o aplicativo hello for removido.

-   Se uma licença apenas foi removida de um usuário ou grupo Olá é que um membro deste pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo Olá toobe alterações feita. Permitir tempo extra antes de entrar no painel de acesso de saudação.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemas relacionados tooassigning aplicativos toousers

Um usuário pode ver um aplicativo no respectivo painel de acesso porque ele foi anteriormente atribuídos tooit. Abaixo estão algumas maneiras toocheck:

-   [Verifique se um usuário é atribuído toohello aplicativo](#check-if-a-user-is-assigned-to-the-application)

-   [Verifique se um usuário está em uma licença relacionados ao aplicativo toohello](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Verifique se um usuário é atribuído toohello aplicativo

toocheck toohello aplicativo, é atribuído a um usuário siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

6.  **Pesquisa** para nome de saudação do aplicativo hello em questão.

7.  Clique em **Usuários e grupos**.

8.  Verifique toosee se o usuário é atribuído a toohello aplicativo.

  * Se você desejar tooremove Olá usuário do aplicativo hello, **clique linha hello** do usuário hello e selecione **excluir**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Verifique se um usuário está em uma licença relacionados ao aplicativo toohello

toocheck um usuário atribuído licenças, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.

   * Se o usuário Olá é atribuído a licença do Office tooan isso habilitar tooappear de aplicativos do Office de terceiros primeiro em Olá painel de acesso do usuário.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemas relacionados tooassigning aplicativos toogroups

Um usuário pode ver um aplicativo no respectivo painel de acesso porque fazem parte de um grupo que tenha sido atribuído um aplicativo hello. Abaixo estão algumas maneiras toocheck:

-   [Verificar as associações de grupo de um usuário](#check-a-users-group-memberships)

-   [Verifique se um usuário for um membro de um grupo atribuído a licença tooa](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Verificar as associações de grupo de um usuário

toocheck a associação do grupo, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **Grupos.**

8.  Verifique toosee se o usuário fizer parte de um aplicativo de toohello grupo atribuído.

   * Se você desejar tooremove Olá usuário do grupo de saudação **clique linha hello** do grupo de saudação e selecione Excluir.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Verifique se um usuário for um membro de um grupo atribuído a licença tooa

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **Grupos.**

8.  Clique em linha de saudação de um grupo específico.

9.  Clique em **licenças** toosee qual grupo de licenças Olá atribuiu tooit.

  * Se o grupo de saudação for atribuído a licença do Office tooan em que isso pode habilitar determinado tooappear de aplicativos do Office de terceiros primeiro Olá painel de acesso do usuário.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se essas etapas de solução de problemas Olá não resolver o problema de saudação

Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email do usuário)

-   ID do locatário

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)
