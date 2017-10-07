---
title: "Azure Active Directory B2C: configuração do LinkedIn | Microsoft Docs"
description: "Fornecer tooconsumers Inscreva-se e entrar com contas LinkedIn em seus aplicativos que são protegidos pelo Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas LinkedIn
## <a name="create-a-linkedin-application"></a>Criar um aplicativo do LinkedIn
toouse LinkedIn como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo LinkedIn e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta LinkedIn isso. Se você não tiver uma, poderá obtê-la em [https://www.linkedin.com/](https://www.linkedin.com/).

1. Vá toohello [site de desenvolvedores do LinkedIn](https://www.developer.linkedin.com/) e entre com suas credenciais de conta do LinkedIn.
2. Clique em **meus aplicativos** em Olá barra de menus superior e, em seguida, clique em **criar aplicativo**.
   
    ![LinkedIn — Novo aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. Em Olá **criar um novo aplicativo** formulário, preencha informações relevantes da saudação (**nome da empresa**, **nome**, **descrição**, **URL de logotipo do aplicativo**, **aplicativo Use**, **URL do site**, **Email comerciais** e **telefone comercial**).
4. Concordo toohello **LinkedIn API termos de uso** e clique em **enviar**.
   
    ![LinkedIn — Registrar aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Copie os valores de saudação do **ID do cliente** e **segredo do cliente**. (Você pode encontrá-los em **Chaves de Autenticação**.) Você precisará de ambos tooconfigure LinkedIn como um provedor de identidade em seu locatário.
   
   > [!NOTE]
   > **Segredo do Cliente** é uma credencial de segurança importante.
   > 
   > 
6. Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URLs de redirecionamento autorizado** campo (em **OAuth 2.0**). Substitua **{tenant}** pelo nome do locatário (por exemplo, contoso.onmicrosoft.com). Clique em **Adicionar** e depois em **Atualizar**. Olá **{locatário}** valor diferencia maiusculas de minúsculas.
   
    ![LinkedIn — Configurar aplicativo](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Configurar o LinkedIn como um provedor de identidade no locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "LI".
5. Clique em **Tipo do provedor de identidade**, selecione **LinkedIn** e clique em **OK**.
6. Clique em **configurar esse provedor de identidade** e digite Olá ID e o cliente segredo do cliente do hello LinkedIn aplicativo que você criou anteriormente.
7. Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração LinkedIn.

