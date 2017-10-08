---
title: aaaProblems entrar no aplicativo tooan usando um deeplink | Microsoft Docs
description: Como os problemas de tootroubleshoot acesso a um aplicativo de uma URL deeplink usando o Azure AD
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a>Problemas para entrar no aplicativo tooan usando um deeplink

Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao. 

Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello. aplicativo Hello deve ser configurado corretamente e atribuído toohello usuário ou grupo Olá é um membro de toosee aplicativo Olá Olá painel de acesso.

Acesso de usuário ou links profundos URLs são links que os usuários podem usar tooaccess seus aplicativos de SSO de senha diretamente da URL de seus navegadores de barras. Navegando toothis link, os usuários terão automaticamente conectado ao aplicativo hello sem ter que primeiro toogo toohello painel de acesso. Isso é hello link mesmo que os usuários usam tooaccess estes aplicativos de iniciador do aplicativo hello Office 365.

## <a name="general-issues-toocheck-first"></a>Geral emite toocheck primeiro

-   Verifique se seu usando um **navegador** que atende aos requisitos mínimos Olá Olá painel de acesso.

-   Certifique-se de navegador do usuário Olá adicionou URL Olá Olá aplicativo tooits **sites confiáveis**.

-   Certifique-se de aplicativo de hello toocheck é **configurado** corretamente.

-   Certifique-se de conta de usuário Olá **habilitado** para entradas.

-   Certifique-se de conta de usuário Olá **não bloqueada.**

-   Tornar-se de que usuário Olá **senha não está expirada ou esquecida.**

-   Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.

-   Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.

-   Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta.

-   Verifique se tooalso tente eliminar os cookies do seu navegador e tentar toosign em novamente.

## <a name="checking-hello-deeplink"></a>Verificando Olá deeplink

toocheck se você tiver deeplink correto do hello, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

7.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

8.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

9.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

10. Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

11. Selecione aplicativo hello para que deseja Olá seleção Olá deeplink.

12. Localizar o rótulo de saudação **URL de acesso do usuário**. O DeepLink deve corresponder a essa URL.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de navegador do painel de acesso

Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:

1.  Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.

2.  Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.

3.  Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.

4.  Com base em seu navegador é direcionado toohello link para download. **Adicionar** navegador de tooyour Olá extensão.

5.  Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.

6.  Quando estiver instalado, **reinicie** a sessão do navegador.

7.  Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha

Você também pode baixar a extensão Olá para Chrome e Firefox de links diretos da saudação abaixo:

-   [Extensão do Painel de Acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão do Painel de Acesso do Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo da Galeria do Azure AD

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo da Galeria do Azure AD Olá](#add-an-application-from-the-Azure-AD-gallery)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Adicionar um aplicativo da Galeria do Azure AD Olá

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **coadministrador**.

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.

6.  Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.

7.  Selecione aplicativo hello desejar tooconfigure para logon único.

8.  Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.

9.  Clique em **adicionar** botão, o aplicativo de hello tooadd.

Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar o aplicativo hello de senha single sign-on

tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  [Atribuir usuários toohello aplicativo](#how-to-assign-a-user-to-an-application-directly).

10. Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação. Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo não Galeria

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo inexistente na galeria](#add-a-non-gallery-application)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Adicionar um aplicativo inexistente na galeria

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **coadministrador**.

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.

6.  clique em **Aplicativo inexistente na galeria.**

7.  Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto. Selecione **Adicionar.**

Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar o aplicativo hello de senha single sign-on

tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

    1.  Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  Digite hello **URL de logon**. Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para. Certifique-se de campos de entrada hello são visíveis na URL de saudação.

10. Atribua usuários toohello aplicativo.

11. Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação. Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Como tooassign tooan aplicativo do usuário diretamente

tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.

13. Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.

15. Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.

Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se essas etapas de solução de problemas Olá não resolva o problema de saudação. 

Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email de usuário)

-   TenantID

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
