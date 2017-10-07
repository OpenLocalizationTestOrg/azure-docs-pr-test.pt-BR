---
title: "aaaHow tooconfigure federado SSO para um aplicativo não Galeria | Microsoft Docs"
description: "Logon único para um aplicativo não Galeria personalizado que você deseja toointegrate com o Azure AD como federado tooconfigure"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Logon único para um aplicativo da Galeria não como federado tooconfigure

tooconfigure um aplicativo não galeria, é necessário toohave do Azure AD premium e aplicativo hello suporta SAML 2.0. Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="overview-of-steps-required"></a>Visão geral das etapas necessárias
Abaixo está uma visão geral de alto nível da saudação etapas necessárias tooconfigure federado logon único para uma galeria-não (por exemplo, personalizado) aplicativo.

-   [Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)](#_Configuring_single_sign-on)

-   [Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperar certificado e metadados Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)](#_Configuring_single_sign-on)

-   [Atribuir usuários toohello aplicativo](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a>Configurando aplicativos único logon toonon-Galeria

tooconfigure logon único para um aplicativo que não está na Galeria do Azure AD hello, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.

6.  Clique em **aplicativo Galeria não** em Olá **adicionar seu próprio aplicativo** seção

7.  Digite o nome de saudação do aplicativo hello em hello **nome** caixa de texto.

8.  Clique em **adicionar** botão, o aplicativo de hello tooadd.

9.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

10. Selecione **baseado no SAML logon** em Olá **modo** lista suspensa.

11. Digite os valores hello necessárias nas **URLs e domínio.** Você deve obter esses valores do fornecedor do aplicativo hello.

   1. aplicativo de hello tooconfigure como iniciado pelo IdP SSO, digite Olá URL de resposta e Olá identificador.

   2. **Opcional:** tooconfigure aplicativo de hello como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.

12. Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.

13. **Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   1. clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2. Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

14. Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello. Além disso, você tem URLs do AD do Azure e o certificado necessário para o aplicativo hello.

15. [Atribua usuários toohello aplicativo.](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo

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

 >[! Observação} AD do Azure Selecionar formato Olá Olá NameID identificador do atributo (usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML. Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.
 >
 >

9.  tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   1. clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2. Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Download de metadados do AD do Azure hello ou certificado

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

## <a name="assign-users-toohello-application"></a>Atribuir usuários toohello aplicativo

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

Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Personalizando Olá SAML declarações enviadas tooan aplicativo

toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
