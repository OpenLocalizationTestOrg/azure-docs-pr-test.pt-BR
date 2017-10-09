---
title: "logon único aaaProblems entrar tooan aplicativo Galeria do AD do Azure configurado para federado | Microsoft Docs"
description: "Como tootroubleshoot problemas de aplicativo da Galeria do AD do Azure configurado para logon único senha"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a>Problemas para entrar no tooan aplicativo da Galeria do AD do Azure configurado para logon único federado

Olá painel de acesso é um portal baseado na web que permite que um usuário que tem um trabalho ou escola conta em aplicativos tooview e inicie baseado em nuvem do Azure Active Directory (AD do Azure) administrador Olá AD do Azure-los concedeu acesso ao. Um usuário com as edições do AD do Azure também pode usar grupos de autoatendimento e recursos de gerenciamento de aplicativo por meio do painel de acesso de saudação. Olá painel de acesso é separado do hello portal do Azure e não exige que os usuários toohave uma assinatura do Azure.

toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello. Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Atende aos requisitos de navegador de saudação painel de acesso

Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou. toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello. Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.

Para SSO baseado em senha, navegadores de saudação do usuário podem ser:

-   Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior

-   Chrome – No Windows 7 ou posterior e no MacOS X ou posterior

-   Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior

>[!NOTE]
>extensão SSO baseada em senha Olá ficam disponíveis para o Edge no Windows 10 quando as extensões de navegador tornam-se com suporte para a borda.
>
>

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

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configurar uma política de grupo para o Internet Explorer

Você pode configurar uma política de grupo que permitem que você extensão do painel de acesso de saudação do tooremotely instalar para o Internet Explorer em computadores de seus usuários.

os pré-requisitos de saudação incluem:

-   Você configurou o [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e você tiver ingressado domínio de tooyour máquinas dos usuários.

-   Você deve ter hello "Editar configurações de" permissão tooedit Olá objeto de política de grupo (GPO). Por padrão, membros da saudação grupos de segurança a seguir têm essa permissão: os administradores de domínio, administradores de empresa e proprietários de criadores de diretiva de grupo. [Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Siga o tutorial Olá [como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a política de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para obter instruções passo a passo sobre como tooconfigure Olá a política de grupo e implantá-lo toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Solucionar problemas de saudação painel de acesso no Internet Explorer

Siga Olá [solucionar Olá extensão do painel de acesso para o Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guia para acessar uma ferramenta de diagnóstico e instruções passo a passo sobre como configurar a extensão de saudação do IE.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo da Galeria do Azure AD

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo da Galeria do Azure AD Olá](#_Add_an_application)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application-for-password-single-sign-on)

-   [Atribuir usuários toohello aplicativo](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Adicionar um aplicativo da Galeria do Azure AD Olá

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**

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

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Modo de seleção Olá **com base em senha de logon.**

9.  [Atribuir usuários toohello aplicativo](#_How_to_assign).

10. Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação. Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.

### <a name="assign-users-toohello-application"></a>Atribuir usuários toohello aplicativo

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

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a>Se eles solucionar etapas não resolverem o problema de Olá 
Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email de usuário)

-   TenantID

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
