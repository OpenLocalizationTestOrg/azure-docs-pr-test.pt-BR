---
title: "Azure Active Directory B2C: configuração do Google+ | Microsoft Docs"
description: "Fornece tooconsumers se inscrever e fazer logon com contas do Google + nos aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Google +
## <a name="create-a-google-application"></a>Criar um aplicativo do Google+
toouse Google + como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo do Google + e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta do Google + isso. Se não tiver uma, você poderá obtê-la em [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Vá toohello [Console de desenvolvedores do Google](https://console.developers.google.com/) e entre com suas credenciais de conta do Google +.
2. Clique em **Criar projeto**, insira um **Nome de projeto** e clique em **Criar**.
   
    ![Google+ – Introdução](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ – Novo projeto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Clique em **Manager API** e, em seguida, clique em **credenciais** em Olá barra de navegação esquerda.
4. Clique em Olá **tela de consentimento de OAuth** guia na parte superior da saudação.
   
    ![Google+ – Credenciais](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Selecione ou especifique um **Endereço de email** válido, forneça um **Nome de produto** e clique em **Salvar**.
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Clique em **Novas credenciais** e escolha **ID do cliente OAuth**.
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. Em **Tipo de aplicativo**, selecione **Aplicativo Web**.
   
    ![Google+ – Tela de consentimento do OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Forneça um **nome** para seu aplicativo, insira `https://login.microsoftonline.com` em Olá **origens do JavaScript autorizado** campo, e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **autorizados redirecionar URIs**campo. Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com). Olá **{locatário}** valor diferencia maiusculas de minúsculas. Clique em **Criar**.
   
    ![Google+ – Criar ID do cliente](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Copie os valores de saudação do **ID do cliente** e **segredo do cliente**. Você precisará de ambos tooconfigure Google + como um provedor de identidade em seu locatário. **Segredo do cliente** é uma credencial de segurança importante.
   
    ![Google+ – Segredo do cliente](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Configurar o Google+ como um provedor de identidade no locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "G+".
5. Clique em **Tipo de provedor de identidade**, selecione **Google** e clique em **OK**.
6. Clique em **configurar esse provedor de identidade** e digite Olá ID e o cliente segredo do cliente do hello Google + aplicativo que você criou anteriormente.
7. Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração do Google +.

