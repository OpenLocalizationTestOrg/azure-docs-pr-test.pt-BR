---
title: "aaaProblems entrar no aplicativo tooan do painel de acesso de saudação | Microsoft Docs"
description: "Como acessar um aplicativo a partir de problemas de tootroubleshoot Olá painel de acesso do AD do Microsoft Azure em myapps.microsoft.com"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Problemas para entrar no aplicativo tooan do painel de acesso de saudação

Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao. 

Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello. aplicativo Hello deve ser configurado corretamente e atribuído toohello usuário ou grupo Olá é um membro de toosee aplicativo Olá Olá painel de acesso.

tipo Hello de aplicativos que um usuário pode ver se enquadram em Olá categorias a seguir:

-   Aplicativos do Office 365

-   Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação

-   Aplicativos de SSO baseadas em senhas

-   Aplicativos com soluções de SSO existentes

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

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Atende aos requisitos de navegador de saudação painel de acesso

Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou. toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello. Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.

Para SSO baseado em senha, navegadores de saudação do usuário podem ser:

-   Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior

-   Edge no Windows 10 Anniversary Edition ou posterior

-   Chrome – No Windows 7 ou posterior e no MacOS X ou posterior

-   Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de navegador do painel de acesso

Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:

1.  Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.

2.  Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.

3.  Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.

4.  Com base em seu navegador é direcionado toohello link para download. **Adicionar** navegador de tooyour Olá extensão.

5.  Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.

6.  Quando estiver instalado, **reinicie** a sessão do navegador.

7.  Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha

Você também pode baixar a extensão Olá para Chrome e borda de links diretos da saudação abaixo:

-   [Extensão do Painel de Acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão do Painel de Acesso do Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Logon único para um aplicativo da Galeria do Azure AD como federado tooconfigure

Todos os aplicativos na Galeria do Azure AD Olá habilitado com a funcionalidade do Enterprise Single Sign-On tem um tutorial passo a passo disponível. Você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhadas.

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo da Galeria do Azure AD Olá](#add-an-application)

-   [Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperar certificado e metadados Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Atribuir usuários toohello aplicativo](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Adicionar um aplicativo da Galeria do Azure AD Olá

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha

6.  Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.

7.  Selecione aplicativo hello desejar tooconfigure para logon único.

8.  Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.

9.  Clique em **adicionar** botão, o aplicativo de hello tooadd.

Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurar logon único para um aplicativo da Galeria do AD do Azure Olá

tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Selecione **baseado no SAML logon** de saudação **modo** lista suspensa.

9.  Digite os valores hello necessárias nas **URLs e domínio.** Você deve obter esses valores do fornecedor do aplicativo hello.

   1. aplicativo de hello tooconfigure como SSO iniciado por SP, Olá logon na URL é um valor obrigatório. Para alguns aplicativos, Olá identificador também é um valor obrigatório.

   2. aplicativo de hello tooconfigure como iniciado pelo IdP SSO, Olá URL de resposta é um valor obrigatório. Para alguns aplicativos, Olá identificador também é um valor obrigatório.

10. **Opcional:** clique **Mostrar configurações de URL avançadas** se você quiser toosee Olá não obrigatórios valores.

11. Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.

12. **Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   1. clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2. Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

13. Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello. Além disso, você tem Olá URLs de metadados e o certificado necessário toosetup SSO com o aplicativo hello.

14. Clique em **salvar** toosave configuração de saudação.

15. Atribua usuários toohello aplicativo.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo

tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello deseja tooshow aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello você configurou o logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa. Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.

    >[!NOTE]
    >Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML. Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.
    >
    >

9.  tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   1. clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2. Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Download de metadados do AD do Azure hello ou certificado

os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello você configurou o logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna. Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.

    AD do Azure não fornece um URL de metadados de saudação de tooget. Olá metadados somente podem ser recuperados como um arquivo XML.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Logon único para um aplicativo da Galeria não como federado tooconfigure

tooconfigure um aplicativo não galeria, é necessário toohave do Azure AD premium e aplicativo hello suporta SAML 2.0. Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)](#configuring-single-sign-on)

-   [Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperar certificado e metadados Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)

tooconfigure logon único para um aplicativo que não está na Galeria do Azure AD hello, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha

6.  Clique em **aplicativo Galeria não** em Olá **adicionar seu próprio aplicativo** seção

7.  Digite o nome de saudação do aplicativo hello em hello **nome** caixa de texto.

8.  Clique em **adicionar** botão, o aplicativo de hello tooadd.

9.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

10. Selecione **baseado no SAML logon** em Olá **modo** suspenso

11. Digite os valores hello necessárias nas **URLs e domínio.** Você deve obter esses valores do fornecedor do aplicativo hello.

  1. aplicativo de hello tooconfigure como iniciado pelo IdP SSO, digite Olá URL de resposta e Olá identificador.

  2. **Opcional:** tooconfigure aplicativo de hello como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.

12. Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.

13. **Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   1. clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2. Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

14. Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello. Além disso, você tem URLs do AD do Azure e o certificado necessário para o aplicativo hello.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo

tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello você configurou o logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa. Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.

   >[!NOTE]
   >Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML. Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.
   >
   >

9.  tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   1. Clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2 Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Download de metadados do AD do Azure hello ou certificado

os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello você configurou o logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna. Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.

    AD do Azure não fornece um URL de metadados de saudação de tooget. Olá metadados somente podem ser recuperados como um arquivo XML.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo da Galeria do Azure AD

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo da Galeria do Azure AD Olá](#add-an-application)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Adicionar um aplicativo da Galeria do Azure AD Olá

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha

6.  Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello

7.  Selecionar aplicativo hello desejar tooconfigure para logon único

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

9.  Atribua usuários toohello aplicativo.

10. Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação. Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Como senha tooconfigure o logon único para um aplicativo não Galeria

tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo inexistente na galeria](#add-a-non-gallery-application)

-   [Configurar o aplicativo hello de senha single sign-on](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Adicionar um aplicativo inexistente na galeria

tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha

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

 * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

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

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se essas etapas de solução de problemas Olá não resolver o problema de saudação

Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email de usuário)

-   TenantID

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)

