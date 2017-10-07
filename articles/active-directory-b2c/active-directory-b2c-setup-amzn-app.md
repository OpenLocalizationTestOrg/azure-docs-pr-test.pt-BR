---
title: "Azure Active Directory B2C: configuração da Amazon | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas do Amazon em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Amazon
## <a name="create-an-amazon-application"></a>Criar um aplicativo da Amazon
toouse Amazon como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo Amazon e fornecê-lo com os parâmetros de saudação à direita. É necessário um toodo de conta do Amazon isso. Se você não tiver uma, poderá obtê-la em [http://www.amazon.com/](http://www.amazon.com/).

1. Vá toohello [Amazon Developer Center](https://login.amazon.com/) e entre com suas credenciais de conta do Amazon.
2. Se você ainda não tiver feito isso, clique em **inscrever-se**, execute as etapas de registro de desenvolvedor hello e aceitar a política de saudação.
3. Clique em **Registrar novo aplicativo**.
   
    ![Registrar um novo aplicativo no site da Amazon Olá](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Forneça as informações do aplicativo (**Nome**, **Descrição** e **URL do Aviso de Privacidade**) e clique em **Salvar**.
   
    ![Fornecendo informações de aplicativo para registrar um novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. Em Olá **configurações Web** seção valores de saudação de cópia de **ID do cliente** e **segredo do cliente**. (É necessário tooclick Olá **Mostrar segredo** botão toosee isso.) Você precisará de ambos deles tooconfigure Amazon como um provedor de identidade em seu locatário. Clique em **editar** na parte inferior da saudação da seção de saudação. **Segredo do Cliente** é uma credencial de segurança importante.
   
    ![Fornecendo a ID e o Segredo do Cliente para seu novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Digite `https://login.microsoftonline.com` em Olá **permitido origens do JavaScript** campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **permitidas URLs de retorno** campo. Substitua **{tenant}** pelo nome do locatário (por exemplo, contoso.onmicrosoft.com). Clique em **Salvar**. Olá **{locatário}** valor diferencia maiusculas de minúsculas.
   
    ![Fornecendo JavaScript Origins e URLs de Retorno para o novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Configurar a Amazon como um provedor de identidade em seu locatário
1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Na folha de recursos Olá B2C, clique em **provedores de identidade**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um amigável **nome** para configuração do provedor de identidade hello. Por exemplo, insira “Amzn”.
5. Clique em **Tipo de provedor de identidade**, selecione **Amazon** e clique em **OK**.
6. Clique em **configurar esse provedor de identidade** e digite Olá ID e o cliente segredo do cliente do hello aplicativo Amazon que você criou anteriormente.
7. Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração da Amazon.

