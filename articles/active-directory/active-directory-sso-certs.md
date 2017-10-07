---
title: "aaaManage certificados de federação no AD do Azure | Microsoft Docs"
description: "Saiba como data de validade de saudação toocustomize para seus certificados de Federação e como toorenew certificados que expirará em breve."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Gerenciar certificados para logon único federado no Azure Active Directory
Este artigo aborda a perguntas comuns e informações relacionadas a certificados toohello Azure Active Directory (AD do Azure) cria tooestablish federado single sign-on (SSO) tooyour aplicativos SaaS. Adicione aplicativos da Galeria de aplicativos do AD do Azure hello, ou usando um modelo de aplicativo não Galeria. Configure o aplicativo hello usando a opção de SSO Olá federado.

Este artigo é tooapps somente relevantes que são configurado toouse SSO do AD do Azure por meio de Federação do SAML, conforme mostrado no exemplo a seguir de saudação:

![Logon Único do AD do Azure](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Certificado gerado automaticamente para aplicativos da galeria e inexistentes na galeria
Quando você adiciona um novo aplicativo da Galeria hello e configurar um baseado no SAML logon, o AD do Azure gera um certificado para o aplicativo hello que seja válido por três anos. Você pode baixar esse certificado do hello **o certificado de autenticação SAML** seção. Para aplicativos de galeria, esta seção pode mostrar um certificado de saudação toodownload opção ou metadados, dependendo do requisito de saudação do aplicativo hello.

![Logon único do Azure AD](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Personalizar a data de validade Olá para o seu certificado de Federação e distribuí-lo sobre tooa novo certificado
Por padrão, os certificados são definidos tooexpire após três anos. Você pode escolher uma data de validade diferentes para o seu certificado Concluindo Olá etapas a seguir.
capturas de tela de saudação usam Salesforce para bem Olá de exemplo, mas essas etapas podem aplicar o aplicativo de SaaS tooany federado.

1. Em Olá [portal do Azure](https://aad.portal.azure.com), clique em **aplicativo empresarial** em Olá painel esquerdo e, em seguida, clique em **novo aplicativo** em Olá **visão geral** página:

   ![Assistente de configuração de SSO Olá aberto](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Procure o aplicativo da Galeria hello e, em seguida, selecione aplicativo hello que você deseja tooadd. Se você não encontrar o aplicativo hello necessários, adicionar o aplicativo hello usando Olá **aplicativo Galeria não** opção. Este recurso está disponível apenas no hello SKU do Azure AD Premium (P1 e P2).

    ![Logon único do Azure AD](./media/active-directory-sso-certs/add_gallery_application.png)

3. Clique em hello **o logon único** link no hello esquerda do painel e altere **modo de logon único** muito**baseado no SAML logon**. Isso gera um certificado válido por três anos para seu aplicativo.

4. toocreate um novo certificado, clique em Olá **criar novo certificado** link no hello **o certificado de autenticação SAML** seção.

    ![Gerar um novo certificado](./media/active-directory-sso-certs/create_new_certficate.png)

5. Olá **criar um novo certificado** link abre o controle de calendário hello. Você pode definir qualquer data e hora do backup toothree anos de saudação data atual. Olá selecionado data e hora é Olá nova data de expiração do seu novo certificado. Clique em **Salvar**.

    ![Baixar e carregar certificado Olá](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Agora o novo certificado de saudação é toodownload disponível. Clique em Olá **certificado** toodownload link-lo. Neste momento, seu certificado não está ativo. Quando você desejar tooroll pela toothis certificado, selecione Olá **ativar o novo certificado** caixa de seleção e clique em **salvar**. Desse ponto, o AD do Azure inicia usando Olá novo certificado de assinatura de resposta de saudação.

7.  toolearn como Olá tooupload certificado tooyour determinado aplicativo de SaaS, clique em Olá **tutorial de configuração do aplicativo de exibição** link.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Renovar um certificado que vencerá em breve
Olá seguinte renovação deve resultar em nenhum tempo de inatividade significativo para seus usuários. Olá as capturas de tela deste recurso, seção Salesforce como um exemplo, mas essas etapas podem aplicar o aplicativo de SaaS tooany federado.

1. Em Olá **Active Directory do Azure** aplicativo **o logon único** página, gerar Olá novo certificado para o seu aplicativo. Você pode fazer isso clicando Olá **criar novo certificado** link no hello **o certificado de autenticação SAML** seção.

    ![Gerar um novo certificado](./media/active-directory-sso-certs/create_new_certficate.png)

2. Selecione Olá desejado data de expiração para o novo certificado e clique em **salvar**.

3. Baixar certificado Olá Olá **certificado de autenticação de SAML** opção. Tela de configuração de logon único carregamento Olá certificado toohello SaaS do novo aplicativo. toolearn como toodo isso para que seu aplicativo SaaS específico, clique em Olá **tutorial de configuração do aplicativo de exibição** link.
   
4. tooactivate Olá novo certificado no AD do Azure, selecione Olá **ativar o novo certificado** caixa de seleção e clique em Olá **salvar** botão na parte superior de saudação da página de saudação. Isso faz sobre o novo certificado de saudação em saudação do lado do AD do Azure. status de saudação do certificado Olá muda de **novo** muito**Active**. Desse ponto, o AD do Azure inicia usando Olá novo certificado de assinatura de resposta de saudação. 
   
    ![Gerar um novo certificado](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Artigos relacionados
* [Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [Índice de artigos para gerenciamento de aplicativos no Azure Active Directory](active-directory-apps-index.md)
* [Acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md)
* [Solução de problemas de logon único baseado em SAML](active-directory-saml-debugging.md)
