---
title: aaaProblem entrando no site do painel de acesso toohello | Microsoft Docs
description: "Problemas de tootroubleshoot de diretrizes que podem ocorrer durante a tentativa de toosign em toouse Olá painel de acesso"
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Problema ao entrar no site do painel de acesso toohello

Olá painel de acesso é um portal baseado na web que permite que um usuário que tem um trabalho ou escola conta em aplicativos tooview e inicie baseado em nuvem do Azure Active Directory (AD do Azure) administrador Olá AD do Azure-los concedeu acesso ao. Um usuário com as edições do AD do Azure também pode usar grupos de autoatendimento e recursos de gerenciamento de aplicativo por meio do painel de acesso de saudação. Olá painel de acesso é separado do hello portal do Azure e não exige que os usuários toohave uma assinatura do Azure.

Os usuários podem entrar no toohello painel de acesso se tiverem uma conta corporativa ou de estudante no AD do Azure.

-   Os usuários podem ser autenticados diretamente no Azure AD.

-   Os usuários podem ser autenticados usando os Serviços de Federação do Active Directory (AD FS).

-   Os usuários podem ser autenticados pelo Windows Server Active Directory.

Se um usuário possui uma assinatura do Azure ou Office 365 e estiver usando Olá portal do Azure ou um aplicativo do Office 365, eles serão capaz toouse Olá painel de acesso diretamente sem a necessidade de toosign em novamente. Os usuários que não estão autenticados ser solicitada toosign no usando Olá username e password para suas contas no AD do Azure. Se a organização Olá configurou a federação, digitar o nome de usuário de saudação é suficiente.

## <a name="general-issues-toocheck-first"></a>Geral emite toocheck primeiro 

-   Verifique se o usuário hello está entrando toohello **corrigir URL**: <https://myapps.microsoft.com>

-   Certifique-se de navegador do usuário Olá adicionou Olá URL tooits **sites confiáveis**

-   Certifique-se de conta de usuário Olá **habilitado** para entradas.

-   Certifique-se de conta de usuário Olá **não bloqueada.**

-   Tornar-se de que usuário Olá **senha não está expirada ou esquecida.**

-   Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.

-   Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.

-   Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta.

-   Verifique se tooalso tente eliminar os cookies do seu navegador e tentar toosign em novamente.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Atende aos requisitos de navegador de saudação painel de acesso

Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou. toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello. Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.

Para SSO baseado em senha, navegadores de saudação do usuário podem ser:

-   Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior

-   Edge no Windows 10 Anniversary Edition ou posterior 

-   Chrome – No Windows 7 ou posterior e no MacOS X ou posterior

-   Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior


## <a name="problems-with-hello-users-account"></a>Problemas com a conta do usuário Olá

Acesso toohello painel de acesso pode ser bloqueada devido a problema tooa com a conta de usuário de saudação. Veja abaixo algumas maneiras de solucionar problemas dos usuários e suas configurações de conta:

-   [Verificar se existe uma conta de usuário no Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Verificar o status da conta do usuário](#check-a-users-account-status)

-   [Redefinir a senha de um usuário](#reset-a-users-password)

-   [Habilitar a redefinição de senha por autoatendimento](#enable-self-service-password-reset)

-   [Verificar o status da Autenticação Multifator de um usuário](#check-a-users-multi-factor-authentication-status)

-   [Verificar as informações de contato de autenticação de um usuário](#check-a-users-authentication-contact-info)

-   [Verificar as associações de grupo de um usuário](#check-a-users-group-memberships)

-   [Verificar as licenças atribuídas de um usuário](#check-a-users-assigned-licenses)

-   [Atribuir uma licença a um usuário](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Verificar se existe uma conta de usuário no Azure Active Directory

toocheck se uma conta de usuário estiver presente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Verifique as propriedades de saudação do hello usuário objeto toobe-se de que elas são conforme o esperado e nenhum dado está ausente.

### <a name="check-a-users-account-status"></a>Verificar o status da conta do usuário

toocheck um usuário status da conta, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **Perfil**.

8.  Em **configurações** Certifique-se de que **bloco entrar** está definido muito**não**.

### <a name="reset-a-users-password"></a>Redefinir a senha de um usuário

tooreset a senha do usuário, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em Olá **Redefinir senha** botão na parte superior de saudação da folha de usuário hello.

8.  Clique em hello **Redefinir senha** botão Olá **Redefinir senha** folha que aparece.

9.  Saudação de cópia **senha temporária** ou **insira uma nova senha** para usuário hello.

10. Se comunicar esse novo usuário toohello senha, eles toochange necessária essa senha durante o próximo entrar tooAzure do Active Directory.

### <a name="enable-self-service-password-reset"></a>Habilitar a redefinição de senha por autoatendimento

senha de autoatendimento tooenable redefinir, execute as etapas de implantação de saudação abaixo:

-   [Habilitar os usuários tooreset suas senhas do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Habilitar os usuários tooreset ou alterar suas senhas do Active Directory local](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Verificar o status da Autenticação Multifator de um usuário

toocheck um usuário do multi-factor status de autenticação seguem Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  Clique em Olá **multi-Factor Authentication** botão na parte superior de saudação da folha de saudação.

7.  Uma vez Olá **Portal de administração do multi-Factor Authentication** cargas, certifique-se você estiver usando Olá **usuários** guia.

8.  Localize usuário Olá Olá lista de usuários por pesquisa, filtragem ou classificação.

9.  Usuário Olá selecione da lista de saudação de usuários e **habilitar**, **desabilitar**, ou **impor** autenticação multifator conforme desejado.

   >[!NOTE]
   >Se um usuário estiver em um **imposto** de estado, você pode defini-las muito**desabilitado** temporariamente toolet-los de volta para sua conta. Quando eles forem novamente, você pode alterar seu estado muito**habilitado** novamente toorequire-los entre suas informações de contato durante o próximo registro de toore. Como alternativa, você pode seguir etapas Olá Olá [Verifique informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info) tooverify ou defina esses dados para eles.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Verificar as informações de contato de autenticação de um usuário

toocheck autenticação do usuário entre em contato com informações usadas para autenticação multifator, acesso condicional, proteção de identidade e de redefinição de senha, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **Perfil**.

8.  Role para baixo demais**informações de contato de autenticação**.

9.  **Revisão** dados saudação registrado para o usuário hello e atualização conforme necessário.

### <a name="check-a-users-group-memberships"></a>Verificar as associações de grupo de um usuário

toocheck um usuário as associações de grupo, execute as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **grupos** toosee que agrupa usuário Olá é membro.

### <a name="check-a-users-assigned-licenses"></a>Verificar as licenças atribuídas de um usuário

toocheck um usuário atribuído licenças, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.

### <a name="assign-a-user-a-license"></a>Atribuir uma licença a um usuário 

tooassign um usuário de tooa de licença, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Todos os usuários**.

6.  **Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.

7.  Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.

8.  Clique em Olá **atribuir** botão.

9.  Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.

10. **Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos. Clique em **OK** quando isso for concluído.

11. Clique em Olá **atribuir** botão tooassign usuário de toothis essas licenças.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Se essas etapas de solução de problemas não resolver o problema de saudação

Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email do usuário)

-   ID do locatário

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
