---
title: Registro de aplicativo do Active Directory de aaaAzure | Microsoft Docs
description: "Este artigo descreve como toouse Olá tooregister portal do Azure a um aplicativo com o Active Directory do Azure"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Registrar seu aplicativo com o locatário do Azure Active Directory

Você pode usar seu aplicativo de saudação tooregister portal do Azure com seu locatário do Azure Active Directory (AD do Azure). Isso cria uma ID de aplicativo para o aplicativo hello e permite que ele tooreceive tokens.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No painel de navegação esquerdo hello, escolha **mais serviços**, clique em **registros do aplicativo**e clique em **adicionar**.
4. Siga os prompts de saudação e criar um novo aplicativo. Se você desejar exemplos específicos para aplicativos da Web ou aplicativos nativos, confira nossos [inícios rápidos](active-directory-developers-guide.md).
  * Para aplicativos Web, fornecer Olá **URL de logon**, que é Olá a URL base do aplicativo, onde os usuários possam entrar ex `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicativos nativos, forneça um **URI de redirecionamento**, o AD do Azure usa tooreturn respostas de token. Insira um aplicativo de tooyour específico de valor,. por exemplo`http://MyFirstAADApp`
5. Depois de concluir o registro, o Azure AD atribui seu aplicativo um identificador de cliente exclusivo, Olá ID do aplicativo.

## <a name="update-application-settings-from-hello-azure-portal"></a>Atualizar configurações de aplicativo do portal do Azure de saudação

Você pode modificar facilmente as configurações do aplicativo existentes usando Olá portal do Azure. Por exemplo, talvez você queira tooconfigure uma URL de resposta, que é onde o Azure AD emite o token respostas. Você também pode desejar tooconfigure permissões tooother aplicativos, para a instância tooallow tooaccess seu aplicativo hello Microsoft Graph API. Você pode fazer isso por meio da página de configurações do aplicativo hello.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No painel de navegação esquerdo hello, escolha **mais serviços**, clique em **registros do aplicativo**e escolha o aplicativo hello lista.
4. Clique em **configurações** tooopen página de configurações de saudação para o aplicativo hello.
  * Olá **propriedades** página permite que você modifique Olá informações gerais sobre aplicativo hello. Isso inclui o nome do aplicativo hello, URL de entrada hello e URL de logout hello.
  * Olá **URLs de resposta** página permite que você tooadd uma URL de resposta, que é onde o AD do Azure envia respostas de token.
  * Olá **proprietários** página permite que você tooadd proprietários do aplicativo.
  * Olá **permissões** página permite que você tooconfigure permissões para o aplicativo hello. Por exemplo, Olá tooaccess Microsoft Graph API, clique em **adicionar** e selecione **Microsoft Graph** no seletor de saudação API, escolha permissão Olá necessária, por exemplo **ler dados do diretório** .
  * Olá **chaves** página permite que você tooadd segredos de aplicativo. Olá segredo será exibido apenas uma vez imediatamente após a criação, portanto, certifique-se de que toocopy-la para uso posterior.

## <a name="use-hello-inline-manifest-editor"></a>Use o editor de manifesto do hello embutido

Você pode usar o hello embutido editor manifesto toomodify certas propriedades do aplicativo que não são expostas diretamente no hello portal do Azure. Por exemplo, você pode usar URI de ID de aplicativo do aplicativo de saudação toomodify ou tooenable Olá fluxo implícito do OAuth 2.0, em vez de autorização de padrão de saudação conceder fluxo de código.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No painel de navegação esquerdo hello, escolha **mais serviços**, clique em **registros do aplicativo**e escolha o aplicativo hello lista.
4. Clique em **manifesto** de saudação página tooopen Olá embutido manifesto editor de aplicativo.
5. Diretamente, você pode fazer alterações toohello manifesto e salvá-lo quando estiver pronto. Como alternativa, você pode baixar tooopen manifesto Olá-lo em seu favorito Olá editor e o carregamento de atualização manifesto.

## <a name="next-steps"></a>Próximas etapas

1. Check-out Olá [início rápido](active-directory-developers-guide.md) para instruções passo a passo detalhada de aplicativos para executar a autenticação usando o Azure AD.
2. Confira a lista completa de exemplos de código no [GitHub](https://github.com/azure-samples).
