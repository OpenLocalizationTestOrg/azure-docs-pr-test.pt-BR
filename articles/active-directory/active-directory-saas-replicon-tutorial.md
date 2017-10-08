---
title: "Tutorial: Integração do Azure Active Directory com o Replicon | Microsoft Docs"
description: "Saiba como toouse Replicon com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Tutorial: Integração do Active Directory do Azure com o Replicon
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e Replicon. cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Um locatário do Replicon

Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooReplicon será toosingle capaz de usar o logon no aplicativo hello em seu site da empresa do Replicon (serviço iniciado pelo provedor logon), ou por meio de saudação [Introdução toohello acesso Painel](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando Olá integração de aplicativos para Replicon
2. Configuração do SSO (logon único)
3. Configurando o provisionamento de usuários
4. Atribuindo usuários

![Cenário](./media/active-directory-saas-replicon-tutorial/IC777798.png "Cenário")

## <a name="enable-hello-application-integration-for-replicon"></a>Habilitar Olá integração de aplicativos para Replicon
Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para Replicon.

**integração do aplicativo hello tooenable para Replicon, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos](./media/active-directory-saas-replicon-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
    ![Adicionar aplicativo](./media/active-directory-saas-replicon-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Adicionar um aplicativo da galeria](./media/active-directory-saas-replicon-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **Replicon**.
   
    ![Galeria de aplicativos](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galeria de aplicativos")
7. No painel de resultados de saudação, selecione **Replicon**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooReplicon com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **Replicon** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
    ![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurar logon único")
2. Em Olá **como você gostaria usuários toosign em tooReplicon** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurar logon único")
3. Em Olá **configurar URL do aplicativo** página, execute Olá etapas a seguir:
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurar URL do Aplicativo")
  1. Em Olá **Replicon URL de logon** caixa de texto, digite a URL do locatário Replicon (por exemplo: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. Em Olá **URL de resposta do Replicon** caixa de texto, digite a URL **AssertionConsumerService** URL (por exemplo: *https://global.replicon.com/! / saml2/empresa/sso/post*).  
      
     >[!NOTE]
     >Você pode obter a URL de saudação do hello Replicon metadados em: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Clique em **Avançar**.

4. Em Olá **configurar logon único no Replicon** página, toodownload seus metadados, clique em **baixar metadados**e, em seguida, salve os metadados de saudação em seu computador.
   
    ![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurar logon único")
5. Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Replicon como administrador.

6. tooconfigure SAML 2.0, execute Olá etapas a seguir:
   
    ![Habilitar autenticação de SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Habilitar autenticação de SAML")
  
  1. Olá toodisplay **EnableSAML Authentication2** caixa de diálogo, acrescente Olá tooyour URL, a seguir após a chave da empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * seguir Olá mostra o esquema de saudação de URL completa hello:  
   **https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Clique em Olá  **+**  tooexpand Olá **v20Configuration** seção.
   3. Clique em Olá  **+**  tooexpand Olá **metaDataConfiguration** seção.
   4. Clique em **Escolher arquivo**, tooselect seu arquivo XML de metadados de provedor de identidade e clique em **enviar**.

7. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
   
    ![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurar logon único")
   
## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário

Em ordem tooenable AD do Azure usuários toolog no Replicon, eles devem ser provisionados no Replicon.  

No caso de saudação do Replicon, o provisionamento é uma tarefa manual.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Em uma janela de navegador da Web, faça logon no site de sua empresa do Replicon como administrador.
2. Vá muito**administração \> usuários**.
   
    ![Usuários](./media/active-directory-saas-replicon-tutorial/IC777806.png "Usuários")
3. Clique em **+Adicionar Usuário**.
   
    ![Adicionar Usuário](./media/active-directory-saas-replicon-tutorial/IC777807.png "Adicionar Usuário")
4. Em Olá **perfil de usuário** , execute Olá etapas a seguir:
   
    ![Perfil de usuário](./media/active-directory-saas-replicon-tutorial/IC777808.png "Perfil de usuário")
   
  1. Em Olá **nome de logon** caixa de texto, Olá tipo AD do Azure endereço de email do usuário de saudação do AD do Azure que você deseja tooprovision.
  2. Para **Tipo de Autenticação**, selecione **SSO**.
  3. Em Olá **departamento** caixa de texto, digite departamento saudação do usuário.
  4. Para **Tipo de Funcionário**, selecione **Administrador**.
  5. Clique em **Salvar Perfil do Usuário**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Replicon usuário conta ou APIs fornecidas pelo Replicon tooprovision contas de usuário do AAD.
> 
> 

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooReplicon, executar Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.

2. Em Olá **Replicon** página de integração de aplicativos, clique em **atribuir usuários**.
   
    ![Atribuir usuários](./media/active-directory-saas-replicon-tutorial/IC777809.png "Atribuir usuários")

3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
    ![Sim](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

