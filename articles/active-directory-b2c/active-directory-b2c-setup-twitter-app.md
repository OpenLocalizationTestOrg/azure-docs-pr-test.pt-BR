---
title: "Azure Active Directory B2C: configuração do Twitter | Microsoft Docs"
description: "Fornece tooconsumers se inscrever e fazer logon com contas do Twitter em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Twitter

> [!NOTE]
> Esse recurso está em visualização.
> 

## <a name="create-a-twitter-application"></a>Criar um aplicativo do Twitter
toouse do Twitter como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), precisa toocreate um aplicativo do Twitter e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta de desenvolvedor do Twitter isso. Se não tiver uma, você poderá obtê-la em [https://dev.twitter.com/](https://dev.twitter.com/).

1. Vá toohello [site do desenvolvedor do Twitter](https://dev.twitter.com/) e entre com suas credenciais.
2. Clique em **Meus aplicativos** em **Ferramentas e Suporte** e, em seguida, clique em **Criar Novo Aplicativo**. 
3. No formulário de hello, forneça um valor para Olá **nome**, **descrição**, e **site**.
4. Para Olá **URL de retorno de chamada**, digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Certifique-se de que tooreplace **{locatário}** com o nome do locatário (por exemplo, contosob2c.onmicrosoft.com).
5. Verificar Olá caixa tooagree toohello **contrato de desenvolvedor** e clique em **criar seu aplicativo Twitter**.
6. Depois que o aplicativo hello for criado, clique em **chaves e Tokens de acesso**.
7. Copie o valor de saudação do **chave do consumidor** e **segredo do consumidor**. Você precisará de ambos tooconfigure Twitter como um provedor de identidade em seu locatário.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Configurar o Twitter como um provedor de identidade em seu locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "Twitter".
5. Clique em **Tipo de provedor de identidade**, selecione **Twitter** e clique em **OK**.
6. Clique em **configurar esse provedor de identidade** e digite Olá Twitter **chave do consumidor** para Olá **id do cliente** e Olá Twitter **segredo do consumidor**para Olá **segredo do cliente**.
7. Clique em **Okey**e, em seguida, clique em **criar** toosave sua configuração do Twitter.

