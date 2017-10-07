---
title: "Tutorial: integração do Azure Active Directory com o Cisco Webex | Microsoft Docs"
description: "Saiba como toouse Cisco Webex com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Tutorial: integração do Active Directory do Azure ao Cisco Webex
Olá objetivo deste tutorial é a integração do Azure e do Cisco Webex Olá tooshow.  
cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Um locatário do Cisco Webex

Após concluir este tutorial, Olá AD do Azure usuários atribuídos tooCisco Webex será toosingle capaz de entrada para o aplicativo hello no site da empresa do Cisco Webex (serviço iniciado pelo provedor logon) ou usando Olá [toohello de Introdução Acessar o painel](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

* Habilitando Olá integração de aplicativos para Cisco Webex
* Configuração do SSO (logon único)
* Configurando o provisionamento de usuários
* Atribuindo usuários

![Cenário](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Cenário")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Habilitar Olá integração de aplicativos para Cisco Webex
Olá objetivo desta seção é toooutline como integração de aplicativos tooenable Olá para Cisco Webex.

**integração do aplicativo hello tooenable para Cisco Webex, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
   ![Aplicativos](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
   ![Adicionar aplicativo](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
   ![Adicionar um aplicativo da galeria](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **Cisco Webex**.
   
   ![Galeria de Aplicativos](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galeria de Aplicativos")
7. No painel de resultados de saudação, selecione **Cisco Webex**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooCisco Webex com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.  

Como parte desse procedimento, será necessário toocreate um certificado codificado em base 64. Se você não estiver familiarizado com esse procedimento, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **Cisco Webex** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurar logon único")
2. Em Olá **como você gostaria usuários toosign em tooCisco Webex** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
   ![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurar logon único")
3. Em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**.
   
   ![Configurar URL do Aplicativo](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurar URL do Aplicativo")   
   1. Em Olá **URL de logon** caixa de texto, digite a URL do locatário Cisco Webex (por exemplo: *http://contoso.webex.com*).
   2. Em hello **URL de resposta do Cisco Webex** caixa de texto, tipo de sua **URL Cisco Webex AssertionConsumerService** (por exemplo: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. Em Olá **configurar logon único no Cisco Webex** página, toodownload seu certificado, clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação em seu computador.
   
   ![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurar logon único")
5. Em uma janela diferente do navegador da Web, faça logon em seu site de empresa do Cisco Webex como administrador.
6. No menu de saudação na parte superior de saudação, clique em **administração de Site**.
   
   ![Administração de Site](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Administração de Site")
7. Em Olá **Gerenciar Site** seção, clique em **configuração SSO**.
   
   ![Configuração de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Configuração de SSO")
8. Na seção de configuração de SSO da Web federado do hello, execute Olá etapas a seguir:
   
   ![Configuração de SSO Federado](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuração de SSO Federado")  
   1. De saudação **protocolo Federation** lista, selecione **SAML 2.0**.
   2. Crie um arquivo **codificado em base 64** usando o certificado baixado.  
    >[!TIP]
    >Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Abra seu certificado codificado em base 64 no bloco de notas e, em seguida, Olá de copiar conteúdo dele.
   4. Clique em **Importar Metadados do SAML**e cole o certificado codificado em Base 64.
   5. Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-Olá **emissor para SAML (ID IdP)** caixa de texto.
   6. Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página de diálogo, Olá cópia **URL de logon remoto** valor e, em seguida, cole-Olá **logon de serviço de SSO do cliente URL** caixa de texto.
   7. De saudação **formato NameID** lista, selecione **endereço de Email**.
   8. Em Olá **AuthnContextClassRef** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:ac:classes:Password**.
   9. Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página de diálogo, Olá cópia **URL de Logout remoto** valor e, em seguida, cole-Olá **Logout de serviço de SSO do cliente URL** caixa de texto.
   10. Clique em **Atualizar**.
9. Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página da caixa de diálogo, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir**.
   
   ![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurar logon único")
   
## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário

Em ordem tooenable AD do Azure usuários toolog no Cisco Webex, eles devem ser provisionados no Cisco Webex.  

* No caso de saudação do Cisco Webex, o provisionamento é uma tarefa manual.

**tooprovision contas de usuário, executar Olá seguintes etapas:**

1. Faça logon no tooyour **Cisco Webex** locatário.
2. Vá muito**gerenciar usuários \> adicionar usuário**.
   
   ![Adicionar Usuários](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Adicionar Usuários")
3. Na seção Adicionar usuário do hello, execute Olá etapas a seguir:
   
   ![Adicionar Usuário](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Adicionar Usuário")   
   1. Para **Tipo de Conta**, selecione **Host**.
   2. Digite as informações de saudação de um usuário existente do AD do Azure em Olá caixas de texto a seguir: **nome, Sobrenome**, **nome de usuário**, **Email**, **senha**, **Confirmar senha**.
   3. Clique em **Adicionar**.

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Cisco Webex usuário conta ou APIs fornecidas pelo Cisco Webex tooprovision contas de usuário do AAD. 
> 

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooCisco Webex, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em Olá **Cisco Webex** página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir usuários](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Atribuir usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

