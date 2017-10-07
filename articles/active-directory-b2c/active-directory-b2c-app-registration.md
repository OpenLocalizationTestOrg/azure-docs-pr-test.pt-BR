---
title: 'Azure Active Directory B2C: registro de aplicativos | Microsoft Docs'
description: Como tooregister seu aplicativo com o Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: registrar seu aplicativo

Este Guia de início rápido ajuda você a registrar um aplicativo em um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos. Quando você terminar, seu aplicativo está registrado para uso no locatário Olá B2C do Azure.

## <a name="prerequisites"></a>Pré-requisitos

toobuild um aplicativo que aceita o consumidor Inscreva-se e entrar, você precisa primeiro aplicativo de hello tooregister com um locatário do Azure Active Directory B2C. Obter seu próprio locatário usando Olá etapas descritas em [criar um locatário Azure AD B2C](active-directory-b2c-get-started.md).

Os aplicativos criados na folha de saudação do Azure AD B2C em Olá portal do Azure devem ser gerenciados da saudação mesmo local. Se você editar aplicativos de B2C hello usando o PowerShell ou outro portal, eles se tornam sem suporte e não funcionam com o Azure AD B2C. Consulte os detalhes em Olá [falha aplicativos](#faulted-apps) seção. 

## <a name="navigate-toob2c-settings"></a>Navegue tooB2C configurações

Faça logon no toohello [portal do Azure](https://portal.azure.com/) como Olá Administrador Global do locatário Olá B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Escolha as próximas etapas com base no tipo de aplicativo hello que está sendo registrado:

* [Registrar um aplicativo Web](#register-a-web-app)
* [Registrar uma API Web](#register-a-web-api)
* [Registrar um aplicativo móvel ou nativo](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Registrar um aplicativo Web

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Se o aplicativo Web chamar uma API da Web protegida pelo Azure AD B2C, execute estas etapas:
   1. Criar um segredo do aplicativo, vai toohello **chaves** folha e clicando em Olá **gerar chave** botão. Anote Olá **chave do aplicativo** valor. Valor de saudação é usado como o segredo do aplicativo hello no código do aplicativo.
   2. Clique em **Acesso à API**, clique em **Adicionar** e selecione sua API da Web e escopos (permissões).

> [!NOTE]
> Um **Segredo de Aplicativo** é uma credencial de segurança importante e deve ser protegido adequadamente.
> 

[Saltar muito**próximas etapas**](#next-steps)

## <a name="register-a-web-api"></a>Registrar uma API Web

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Clique em **publicado escopos** tooadd mais escopos conforme o necessário. Por padrão, o escopo de "user_impersonation" hello é definido. o escopo user_impersonation Olá fornece tooaccess de capacidade de saudação outros aplicativos essa api em nome do usuário conectado do hello. Se desejar, o escopo user_impersonation Olá pode ser removido.

[Saltar muito**próximas etapas**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Registrar um aplicativo móvel ou nativo

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Saltar muito**próximas etapas**](#next-steps)

## <a name="limitations"></a>Limitações

### <a name="choosing-a-web-app-or-api-reply-url"></a>Escolher aplicativo Web ou URL de resposta da API

Atualmente, os aplicativos que são registrados com o Azure AD B2C são conjunto restrito tooa limitado de valores da URL de resposta. Olá resposta URL para serviços e aplicativos web deve começar com o esquema de saudação `https`, e respondam a todos os valores da URL devem compartilhar um único domínio DNS. Por exemplo, você não pode registrar um aplicativo Web que tenha uma destas URLs de resposta:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

sistema de registro de saudação compara Olá todo DNS nome de saudação existente resposta URL toohello DNS Olá da URL de resposta que você está adicionando. Olá tooadd da solicitação Olá nome DNS falhará se uma saudação seguintes condições for verdadeira:

* nome DNS todo Olá Olá novo da URL de resposta não coincide com nome DNS Olá Olá existente da URL de resposta.
* nome DNS todo Olá Olá novo da URL de resposta não é um subdomínio Olá existente da URL de resposta.

Por exemplo, se hello aplicativo tem essa URL de resposta:

`https://login.contoso.com`

Você pode adicionar tooit, como este:

`https://login.contoso.com/new`

Nesse caso, o nome DNS de saudação corresponder exatamente. Ou você pode fazer isto:

`https://new.login.contoso.com`

Nesse caso, você está fazendo referência tooa subdomínio DNS de login.contoso.com. Se você quiser toohave um aplicativo que tenha o logon east.contoso.com e west.contoso.com logon como responder a URLs, você deve adicionar as URLs de resposta nesta ordem:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Você pode adicionar Olá dois últimos porque eles são subdomínios Olá primeiro da URL de resposta, contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Escolher um URI de redirecionamento do aplicativo nativo

Há duas considerações importantes ao escolher um URI de redirecionamento para aplicativos móveis/nativo:

* **Exclusivo**: esquema de saudação do URI de redirecionamento Olá deve ser exclusiva para cada aplicativo. Em nosso exemplo (com.onmicrosoft.contoso.appname://redirect/path), usamos com.onmicrosoft.contoso.appname como esquema de saudação. É recomendável seguir esse padrão. Se dois aplicativos compartilharem Olá mesmo esquema, hello usuário vê uma caixa de diálogo "Escolha o aplicativo". Se o usuário Olá faz uma escolha incorreta, falha de logon de saudação.
* **Completo**: o URI de redirecionamento deve ter um esquema e um caminho. caminho de saudação deve conter pelo menos uma barra invertida após domínio hello (por exemplo, //contoso/ funciona e //contoso falhar).

Verifique se que há sem caracteres especiais, como o uri de redirecionamento sublinhados em hello.

### <a name="faulted-apps"></a>Aplicativos com falha

Os aplicativos B2C NÃO devem ser editados:

* Em outros portais de gerenciamento de aplicativo, como o [portal clássico do Azure](https://manage.windowsazure.com/) e o [Portal de Registro de Aplicativo](https://apps.dev.microsoft.com/).
* Uso da API do Graph ou do PowerShell

Se você editar o aplicativo hello B2C conforme descrito acima e tente tooedit-la novamente na folha de recursos de saudação do Azure AD B2C em Olá portal do Azure, torna-se um aplicativo com falha e o aplicativo não será mais utilizável com o Azure AD B2C. Você tem o aplicativo hello de toodelete e criá-la novamente.

toodelete Olá aplicativo, vá toohello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/) e excluir o aplicativo hello. Para toobe de aplicativo hello visível, é necessário toobe proprietário de saudação do aplicativo hello (e não apenas um administrador de locatário Olá).

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um aplicativo registrado com o Azure AD B2C, você pode executar uma das [nossos tutoriais de início rápido](active-directory-b2c-overview.md#get-started) tooget em funcionamento.

> [!div class="nextstepaction"]
> [Criar um aplicativo Web ASP.NET com inscrição, entrada e redefinição de senha](active-directory-b2c-devquickstarts-web-dotnet-susi.md)