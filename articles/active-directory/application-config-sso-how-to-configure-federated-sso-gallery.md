---
title: aaaHow tooconfigure federado SSO para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Logon único para um existente Galeria do Azure AD aplicativo e como usar tutoriais tooget ir rapidamente como federado tooconfigure"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Logon único para um aplicativo da Galeria do Azure AD como federado tooconfigure

Todos os aplicativos na Galeria de saudação do AD do Azure habilitado com o recurso de logon único corporativo tem um tutorial passo a passo disponível. Você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obter orientações passo a passo detalhadas.

## <a name="overview-of-steps-required"></a>Visão geral das etapas necessárias
tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:

-   [Adicionar um aplicativo da Galeria do Azure AD Olá](#add-an-application-from-the-azure-ad-gallery)

-   [Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperar certificado e metadados Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Atribuir usuários toohello aplicativo](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Adicionar um aplicativo da Galeria do Azure AD Olá

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

Após um curto período de tempo, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurar logon único para um aplicativo da Galeria do AD do Azure Olá

tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **coadministrador**.

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

   1. Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

13. Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello. Além disso, você tem Olá URLs de metadados e o certificado necessário toosetup SSO com o aplicativo hello.

14. Clique em **salvar** toosave configuração de saudação.

15. Atribua usuários toohello aplicativo.

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

  >[!NOTE] 
  >Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML. Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.
  >
  >

9.  tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:
  
   1. clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   2. Clique em **Salvar**. Você verá um novo atributo Olá na tabela de saudação.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Download de metadados do AD do Azure hello ou certificado

os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  *  Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos**.

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



