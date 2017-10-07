---
title: "Azure Active Directory B2C: configuração do Weibo | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas Weibo em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas de Weibo

> [!NOTE]
> Esse recurso está em visualização. Não use esse provedor de identidade no ambiente de produção.
> 

## <a name="create-a-weibo-application"></a>Criar um aplicativo Weibo

toouse Weibo como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo Weibo e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta Weibo isso. Caso não tenha, você pode obter uma em [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Registre-se para o programa para desenvolvedores Weibo Olá

1. Vá toohello [portal do desenvolvedor Weibo](http://open.weibo.com/) e entre com suas credenciais de conta Weibo.
2. Depois de entrar, clique em seu nome de exibição no canto superior direito de saudação.
3. No menu suspenso hello, selecione**编辑开发者信息**(Editar informações do desenvolvedor).
4. Inserir informações de Olá necessárias no formulário de saudação e clique em**提交**(envio).
5. Concluir o processo de verificação de email de saudação.
6. Vá toohello [página de verificação de identidade](http://open.weibo.com/developers/identity/edit).
7. Inserir informações de Olá necessárias no formulário de saudação e clique em**提交**(envio).

### <a name="register-a-weibo-application"></a>Registrar um aplicativo Weibo

1. Vá toohello [nova página de registro de aplicativo Weibo](http://open.weibo.com/apps/new).
2. Insira as informações de aplicativo necessário hello.
3. Clique em **创建** (criar).
4. Copie os valores de saudação do **chave do aplicativo** e **segredo do aplicativo**. Você precisará dessas informações posteriormente.
5. Carregar fotos Olá necessários e insira informações necessárias hello.
6. Clique em **保存以上信息** (salvar).
7. Clique em **高级信息** (informações avançadas).
8. Clique em**编辑**próximo campo de toohello (Editar) para OAuth 2.0**授权设置**(URL de redirecionamento).
9. Insira `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` para **授权设置** (URL de redirecionamento) do OAuth2.0. Por exemplo, se seu `tenant_name` é contoso.onmicrosoft.com, conjunto Olá URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Clique em **提交** (enviar).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Configurar o Weibo como um provedor de identidade em seu locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "Weibo".
5. Clique em **Tipo de provedor de identidade**, selecione **Weibo** e clique em **OK**.
6. Clique em **Configurar este provedor de identidade**
7. Digite hello **chave do aplicativo** que você copiou anteriormente como Olá **ID do cliente**.
8. Digite hello **segredo do aplicativo** que você copiou anteriormente como Olá **segredo do cliente**.
9. Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração Weibo.

