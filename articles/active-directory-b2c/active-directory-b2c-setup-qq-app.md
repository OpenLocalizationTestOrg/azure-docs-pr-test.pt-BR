---
title: "Azure Active Directory B2C: configuração do QQ | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas TQ em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas de TQ

> [!NOTE]
> Esse recurso está em visualização.
> 

## <a name="create-a-qq-application"></a>Criar um aplicativo QQ

toouse TQ como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo TQ e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta TQ isso. Se você não tiver uma, poderá obtê-la em [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Registre-se para o programa para desenvolvedores TQ Olá

1. Vá toohello [portal do desenvolvedor TQ](http://open.qq.com) e entre com suas credenciais de conta TQ.
2. Depois de entrar, vá muito[http://open.qq.com/reg](http://open.qq.com/reg) tooregister como um desenvolvedor.
3. No menu de saudação, selecione**个人**(desenvolvedor individuais).
4. Inserir informações de Olá necessárias no formulário de saudação e clique em**下一步**(próxima etapa).
5. Concluir o processo de verificação de email de saudação.

> [!NOTE]
> Você precisará toowait alguns toobe dias após registrar como um desenvolvedor. 

### <a name="register-a-qq-application"></a>Registrar um aplicativo do QQ

1. Vá muito[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Clique em **应用管理** (gerenciamento de aplicativo).
3. Clique em **创建应用** (criar aplicativo).
4. Insira as informações de aplicativo necessário hello.
5. Clique em **创建应用** (criar aplicativo).
6. Insira as informações de saudação necessária.
7. Para Olá**授权回调域**(URL de retorno de chamada), digite `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Por exemplo, se seu `tenant_name` é contoso.onmicrosoft.com, conjunto Olá URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Clique em **创建应用** (criar aplicativo).
9. Na página de confirmação de saudação, clique em**应用管理**página de gerenciamento (gerenciamento de aplicativo) tooreturn toohello aplicativo.
10. Clique em**查看**(exibição) próximo toohello aplicativo recém-criado.
11. Clique em **修改** (editar).
12. Da parte superior de saudação da página hello, copie Olá **ID do aplicativo** e **chave do aplicativo**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Configurar a QQ como um provedor de identidade em seu locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "QQ".
5. Clique em **Tipo de provedor de identidade**, selecione **QQ** e clique em **OK**.
6. Clique em **Configurar este provedor de identidade**
7. Digite hello **chave do aplicativo** que você copiou anteriormente como Olá **ID do cliente**.
8. Digite hello **segredo do aplicativo** que você copiou anteriormente como Olá **segredo do cliente**.
9. Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração TQ.

