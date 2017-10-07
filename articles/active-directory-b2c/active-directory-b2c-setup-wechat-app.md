---
title: "Azure Active Directory B2C: configuração WeChat | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas WeChat em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas de WeChat

> [!NOTE]
> Esse recurso está em visualização.
> 

## <a name="create-a-wechat-application"></a>Criar um aplicativo WeChat

toouse WeChat como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo WeChat e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta WeChat isso. Caso não tenha, você pode obter uma inscrevendo-se em um dos aplicativos móveis ou usando o número do seu QQ. Depois disso, obter sua conta registrada com o programa para desenvolvedores WeChat hello. Você pode encontrar mais informações [aqui](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>Registrar um aplicativo WeChat

1. Vá muito[https://open.weixin.qq.com/](https://open.weixin.qq.com/) e faça logon.
2. Clique em **管理中心** (centro de gerenciamento).
3. Siga as etapas necessárias de saudação tooregister um novo aplicativo.
4. Para **授权回调域** (URL de retorno de chamada), digite `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Por exemplo, se seu `tenant_name` é contoso.onmicrosoft.com, conjunto Olá URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Localizar e copiar Olá **ID do aplicativo** e **chave do aplicativo**. Você precisará delas mais tarde.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Configurar o WeChat como um provedor de identidade em seu locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "WeChat".
5. Clique em **Tipo de provedor de identidade**, selecione **WeChat** e clique em **OK**.
6. Clique em **Configurar este provedor de identidade**
7. Digite hello **chave do aplicativo** que você copiou anteriormente como Olá **ID do cliente**.
8. Digite hello **segredo do aplicativo** que você copiou anteriormente como Olá **segredo do cliente**.
9. Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração WeChat.

