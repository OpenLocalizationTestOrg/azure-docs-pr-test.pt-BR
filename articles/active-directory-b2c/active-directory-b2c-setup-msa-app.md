---
title: "Azure Active Directory B2C: configuração da conta da Microsoft | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas da Microsoft em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers Inscreva-se e entrar com contas da Microsoft
## <a name="create-a-microsoft-account-application"></a>Criar um aplicativo de conta da Microsoft
toouse Microsoft conta como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo de conta da Microsoft e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta Microsoft isso. Se não tiver uma, você poderá obtê-la em [https://www.live.com/](https://www.live.com/).

1. Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e entre com suas credenciais de conta da Microsoft.
2. Clique em **Adicionar um aplicativo**.
   
    ![Conta da Microsoft – Adicionar um novo aplicativo](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Forneça um **Nome** para seu aplicativo e clique em **Criar aplicativos**.
   
    ![Conta da Microsoft – Nome do aplicativo](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Copie o valor de saudação do **Id do aplicativo**. Você precisará dele tooconfigure conta da Microsoft como um provedor de identidade em seu locatário.
   
    ![Conta da Microsoft - Id do Aplicativo](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Clique em **Adicionar plataforma** e escolha **Web**.
   
    ![Conta da Microsoft - Adicionar plataforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Conta da Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URIs de redirecionamento** campo. Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).
   
    ![Conta da Microsoft – URL de redirecionamento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Clique em **gerar nova senha** em Olá **segredos do aplicativo** seção. Cópia Olá nova senha exibida na tela. Você precisará dele tooconfigure conta da Microsoft como um provedor de identidade em seu locatário. A senha é uma credencial de segurança importante.
   
    ![Conta da Microsoft - Gerar nova senha](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Conta da Microsoft - Nova senha](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Caixa de saudação de seleção que diz **suporte do SDK do Live** em Olá **opções avançadas de** seção. Clique em **Salvar**.
   
    ![Conta da Microsoft - Suporte ao SDK do Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Configurar a conta da Microsoft como um provedor de identidade no locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira "MSA".
5. Clique em **Tipo do provedor de identidade**, selecione **Conta da Microsoft** e clique em **OK**.
6. Clique em **configurar esse provedor de identidade** e digite Olá Id do aplicativo e a senha da saudação aplicativo de conta da Microsoft que você criou anteriormente.
7. Clique em **Okey** e, em seguida, clique em **criar** toosave configuração de conta do Microsoft.

