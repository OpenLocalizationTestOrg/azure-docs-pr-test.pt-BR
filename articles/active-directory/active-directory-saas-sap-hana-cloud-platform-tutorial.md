---
title: "Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Microsoft Docs"
description: "Saiba como toouse plataforma de nuvem HANA SAP com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Tutorial: Integração do Active Directory do Azure com a Plataforma de Nuvem HANA SAP
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e plataforma de nuvem HANA SAP.

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma conta da Plataforma de Nuvem HANA SAP

Após concluir este tutorial, Olá usuários AD do Azure que você atribuiu tooSAP a plataforma de nuvem HANA toosingle capaz de entrada no aplicativo hello usando Olá [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Você precisa toodeploy seu próprio aplicativo ou assina o aplicativo tooan em sua plataforma de nuvem HANA SAP conta tootest único logon. Neste tutorial, um aplicativo é implantado na conta de saudação.
> 
> 

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando Olá integração de aplicativos para a plataforma de nuvem HANA SAP
2. Configuração do SSO (logon único)
3. Atribuir um usuário de tooa de função
4. Atribuindo usuários

![Cenário](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Cenário")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Habilitando Olá integração de aplicativos para a plataforma de nuvem HANA SAP
Olá objetivo desta seção é toooutline como tooenable Olá integração de plataforma de nuvem HANA SAP.

**integração do aplicativo hello tooenable para a plataforma de nuvem HANA SAP, execute Olá etapas a seguir:**

1. No hello Portal de gerenciamento do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
    ![Aplicativos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
    ![Adicionar aplicativo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
    ![Adicionar um aplicativo da galeria](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **plataforma de nuvem HANA SAP**.
   
    ![Galeria de Aplicativos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galeria de Aplicativos")
7. No painel de resultados de saudação, selecione **plataforma de nuvem HANA SAP**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooSAP plataforma de nuvem HANA com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

Como parte desse procedimento, será necessário tooupload um locatário de plataforma de nuvem HANA SAP tooyour certificado codificado em base 64.  

Se você não estiver familiarizado com esse procedimento, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **plataforma de nuvem HANA SAP** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**caixa de diálogo.
   
    ![Configurar logon único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurar logon único")
2. Em Olá **como você gostaria usuários toosign em tooSAP plataforma de nuvem HANA** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurar Logon Único")
3. Em uma janela de navegador web diferente, faça logon no toohello cockpit da plataforma de nuvem de HANA SAP em https://account. \<host paisagem\>.ondemand.com/cockpit (por exemplo: *https://account.hanatrial.ondemand.com/cockpit*).
4. Clique em Olá **confiança** guia.
   
    ![Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Confiança")
5. Na seção de gerenciamento de confiança, execute Olá etapas a seguir:
   
    ![Obter Metadados](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obter Metadados")
   
   1. Clique em Olá **provedor de serviço Local** guia.
   2. Olá toodownload arquivo de metadados da plataforma de nuvem HANA SAP, clique em **obter metadados de**.
6. No hello Azure Active portal clássico, em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**.
   
    ![Configurar URL do Aplicativo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurar URL do Aplicativo")
   
   1. Em Olá **URL de logon** caixa de texto, digite a URL Olá usada pelo seu toosign usuários em sua **plataforma de nuvem HANA SAP** aplicativo. Isso é Olá URL de conta específica de um recurso protegido em seu aplicativo de plataforma de nuvem HANA SAP. Olá URL é baseada no saudação padrão a seguir: *https://\<applicationName\>\<accountName\>.\< host de paisagem\>.ondemand.com/\<caminho\_para\_protegido\_recurso\>*  (por exemplo: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Esta é a URL Olá em seu aplicativo de plataforma de nuvem HANA SAP que exige Olá tooauthenticate de usuário.
     > 

   2. Abrir o arquivo de metadados de plataforma de nuvem HANA SAP Olá baixado e localize Olá **ns3: assertionconsumerservice** marca.
   3. Copie o valor Olá Olá **local** de atributo e, em seguida, cole-Olá **URL de resposta de plataforma de nuvem do SAP HANA** caixa de texto.

7. Em Olá **configurar logon único na plataforma de nuvem HANA SAP** página, toodownload seus metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador.
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurar Logon Único")
8. Em Olá cockpit da plataforma de nuvem HANA SAP, em Olá **provedor de serviço Local** , execute Olá etapas a seguir:
   
    ![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Gerenciamento de Confiança")
   
  1. Clique em **Editar**.
  2. Para **Tipo de Configuração**, selecione **Personalizado**.
  3. Como **nome do provedor Local**, deixe o valor padrão de saudação.
  4. toogenerate um **chave de assinatura** e um **certificado de assinatura de** par de chaves, clique em **gerar par de chaves**.
  5. Para **Propagação de Entidade**, selecione **Desabilitado**.
  6. Para **Forçar Autenticação**, selecione **Desabilitado**.
  7. Clique em **Salvar**.

9. Clique em Olá **provedor de identidade confiável** guia e, em seguida, clique em **Adicionar provedor de identidade confiável**.
   
    ![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Gerenciamento de Confiança")
   
    >[!NOTE]
    >lista de saudação toomanage de provedores de identidade confiável, você precisa toohave escolhida Olá tipo de configuração personalizada na Olá seção do provedor de serviço Local. Para tipo de configuração padrão, você tem uma toohello confiança implícita e não editável SAP ID de serviço. Para Nenhum, não há configurações de confiança.
    > 
    > 

10. Clique em Olá **geral** guia e, em seguida, clique em **procurar** Olá tooupload baixou o arquivo de metadados.
    
    ![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Gerenciamento de Confiança")
    
    >[!NOTE]
    >Depois de carregar o arquivo de metadados de hello, Olá valores para **URL de logon único**, **URL de Logout único** e **certificado de assinatura** são preenchidas automaticamente.
    > 
    > 

11. Clique em Olá **atributos** guia.
12. Em Olá **atributos** guia, execute Olá etapa a seguir:
    
    ![Atributos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Atributos") 
  * Clique em **Adicionar atributo**e, em seguida, adicionar Olá seguintes atributos com base em asserção:
       
    | Atributo de Asserção | Atributo de Entidade |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |nome |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Sobrenome |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >configuração de Olá Olá atributos depende como Olá aplicativos na HCP são desenvolvidos, isto é, quais atributos eles esperam ter na resposta SAML de saudação e por qual nome (atributo de entidade) eles acessam esse atributo no código de saudação.
     > 
     >  

    1.  Olá **atributo padrão** em Olá captura de tela é apenas para fins de ilustração. Não é necessário o trabalho de cenário de saudação toomake.   
    2.  Olá nomes e valores para **atributo de entidade** mostrado no hello captura de tela dependem de como o aplicativo hello é desenvolvido. É possível que o seu aplicativo precise de mapeamentos diferentes.
     
13. Em Olá portal clássico do Azure, em Olá **configurar logon único na plataforma de nuvem HANA SAP** página de caixa de diálogo, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir**.
    
    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurar Logon Único")

###<a name="assertion-based-groups"></a>Grupos baseados em asserção
Como uma etapa opcional, você pode configurar grupos com base na asserção para seu Provedor de Identidade do Azure Active Directory.

Usar grupos na plataforma de nuvem HANA SAP permite atribuir toodynamically um ou mais tooone de usuários ou mais funções em seus aplicativos de plataforma de nuvem HANA SAP, determinados pelos valores de atributos em Olá SAML 2.0 asserção. 

Por exemplo, se hello asserção contém atributo hello "*contrato = temporário*", convém todos os usuários afetados toobe toohello adicionado grupo"*temporário*". grupo Hello "*temporário*" pode conter uma ou mais funções de um ou mais aplicativos implantados em sua conta da plataforma de nuvem HANA SAP.
 
Use grupos com base na asserção quando desejar atribuir toosimultaneously muitos tooone de usuários ou mais funções de aplicativos em sua conta da plataforma de nuvem HANA SAP. Se você quiser tooassign apenas um único ou pequeno número de usuários toospecific funções, é recomendável atribuí-las diretamente no hello "**autorizações**" guia de cockpit da plataforma de nuvem HANA SAP de saudação.

## <a name="assign-a-role-tooa-user"></a>Atribuir um usuário de tooa de função
Ordem tooenable AD do Azure usuários toolog na plataforma de nuvem HANA SAP, você deve atribuir funções no hello toothem de plataforma de nuvem HANA SAP.

**tooassign um usuário de tooa de função, execute Olá etapas a seguir:**

1. Faça logon no tooyour **plataforma de nuvem HANA SAP** cockpit.
2. Execute o seguinte hello:
   
   ![Autorizações](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizações")
   
  1. Clique em **Autorização**.
  2. Clique em Olá **usuários** guia.
  3. Em Olá **usuário** caixa de texto, o endereço de email do usuário do tipo hello.
  4. Clique em **atribuir** tooassign Olá tooa chave de criptografia.
  5. Clique em **Salvar**.

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooSAP plataforma de nuvem do HANA, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em Olá **plataforma de nuvem HANA SAP** página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir Usuários](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Atribuir Usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

