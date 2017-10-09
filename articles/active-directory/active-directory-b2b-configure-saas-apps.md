---
title: "aplicativos de SaaS aaaConfigure para colaboração B2B no Active Directory do Azure | Microsoft Docs"
description: "Exemplos de código e do PowerShell para colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Configurar aplicativos SaaS para colaboração B2B

A colaboração B2B do Azure Active Directory (Azure AD) funciona com a maioria dos aplicativos que se integra no Azure AD. Nesta seção, examinaremos as instruções de como configurar alguns aplicativos SaaS populares para usar com o B2B do Azure AD.

Antes de examinarmos as instruções específicas do aplicativo, aqui estão algumas regras gerais:

* Para a maioria dos aplicativos hello, configuração do usuário precisa toohappen manualmente. Ou seja, os usuários devem ser criados manualmente no aplicativo de saudação também.

* Para aplicativos que dão suporte a instalação automática, como o Dropbox, convites separados são criados nos aplicativos de saudação. Os usuários deve ser tooaccept-se de que cada convite.

* Em atributos de usuário hello, toomitigate quaisquer problemas com o disco de perfil de usuário danificado (UDP) em usuários convidados, sempre defina **identificador de usuário** muito**user.mail**.


## <a name="dropbox-business"></a>Dropbox Business

tooenable toosign de usuários usando sua conta de organização, você deve configurar manualmente Dropbox Business toouse AD do Azure como um provedor de identidade SAML Security Assertion Markup Language (). Se Dropbox Business não foi configurado toodo assim, ele não é possível solicitar ou permitam toosign usuários usando AD do Azure.

1. aplicativo de negócios Dropbox Olá tooadd no AD do Azure, selecione **aplicativos empresariais** Olá painel esquerdo e, em seguida, clique em **adicionar**.

  ![botão de "Adicionar" Hello na página de aplicativos da empresa de saudação](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. Em Olá **adicionar um aplicativo** janela, digite **dropbox** Olá caixa de pesquisa e, em seguida, selecione **Dropbox for Business** na lista de resultados de saudação.

  ![Pesquise "dropbox" em Olá adicionar uma página de aplicativo](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Em Olá **o logon único** página, selecione **o logon único** Olá painel esquerdo e, em seguida, digite **user.mail** em hello **identificador de usuário** caixa. (É definido como UPN por padrão.)

  ![Configurar o logon único para o aplicativo hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload Olá certificado toouse para configuração do Dropbox, selecione **configurar DropBox**e, em seguida, selecione **SAML Service URL de logon único** na lista de saudação.

  ![Baixando certificado Olá para configuração do Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Entrar tooDropbox com hello URL de logon da saudação **o logon único** página.

  ![página Olá entrar no Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. No menu de saudação, selecione **Console de administração**.

  ![link de "Console de administração" Hello no menu do Dropbox Olá](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. Em Olá **autenticação** caixa de diálogo, selecione **mais**, carregar certificado hello e, em seguida, em Olá **URL de logon** , digite a URL de saudação SAML SSO.

  ![Olá link "Mais" na caixa de diálogo de autenticação Olá recolhido](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Olá "URL de entrada" no hello expandido a caixa de diálogo de autenticação](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. configuração de usuário automático de tooconfigure no hello portal do Azure, selecione **provisionamento** no painel esquerdo do hello, selecione **automático** em Olá **modo de provisionamento** caixa e, em seguida, selecione **Autorizar**.

  ![Configurar o provisionamento automático de usuário no portal do Azure de saudação](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Depois usuários convidados ou membro foi configurados no aplicativo do Dropbox hello, eles recebem um convite separado do Dropbox. toouse logon único Dropbox, convidados devem aceitar o convite Olá clicando no link nele.

## <a name="box"></a>Box
Você pode habilitar os usuários tooauthenticate caixa convidados com suas contas do AD do Azure usando federação com base no protocolo SAML de saudação. Neste procedimento, você deve carregar metadados tooBox.com.

1. Adicione Olá caixa aplicativo de aplicativos corporativos de saudação.

2. Configure o logon único Olá ordem a seguir:

  ![Configurar logon único do Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. Em Olá **URL de logon** caixa, certifique-se de que o URL de entrada hello está definida corretamente para caixa em Olá portal do Azure. Essa URL é saudação do seu locatário Box.com. Você deve seguir a convenção de nomenclatura Olá *https://.box.com*.  
 Olá **identificador** não se aplica a toothis aplicativo, mas ela ainda aparecerá como um campo obrigatório.

 b. Em Olá **identificador de usuário** , digite **user.mail** (para o SSO para contas de convidado).

 c. Em **Certificado de Assinatura de SAML**, clique em **Criar novo certificado**.

 d. toobegin configurar seu locatário de Box.com toouse AD do Azure como um provedor de identidade, baixe o arquivo de metadados de saudação e salve-a como unidade local tooyour.

 e. Encaminhe Olá metadados arquivo toohello caixa equipe de suporte, que configura o logon único para você.

3. Para a instalação automática de usuários do AD do Azure, no painel esquerdo do hello, selecione **provisionamento**e, em seguida, selecione **autorizar**.

  ![Autorizar o Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Como convidados Dropbox, convidados caixa devem resgatar seu convite de saudação caixa aplicativo.

## <a name="next-steps"></a>Próximas etapas

Consulte Olá artigos colaboração B2B do Azure AD a seguir:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegação de convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
