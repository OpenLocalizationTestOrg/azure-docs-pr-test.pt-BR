---
title: "autenticação aaaAdd no Android com aplicativos móveis | Microsoft Docs"
description: "Saiba como toouse Olá recurso de aplicativos móveis de usuários do serviço de aplicativo do Azure tooauthenticate do seu aplicativo do Android por meio de uma variedade de provedores de identidade, como Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Adicionar aplicativo do Android autenticação tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Resumo
Neste tutorial, você adicionar projeto de início rápido do autenticação toohello todolist no Android, usando um provedor de identidade com suporte. Este tutorial baseia-se a saudação [começar com aplicativos móveis] tutorial, que deve ser concluído primeiro.

## <a name="register"></a>Registrar seu aplicativo para autenticação e configurar o Serviço de Aplicativo do Azure
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo

A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo. Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação. Neste tutorial, usamos o esquema de URL Olá _appname_ em todo. No entanto, você pode usar o esquema de URL que quiser. Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis. redirecionamento de saudação tooenable no lado do servidor de saudação:

1. No hello [portal do Azure], selecione o serviço de aplicativo.

2. Clique em Olá **autenticação / autorização** opção de menu.

3. Em Olá **permitidas URLs de redirecionamento externo**, digite `appname://easyauth.callback`.  Olá _appname_ na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.  Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).  Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.

4. Clique em **OK**.

5. Clique em **Salvar**.

## <a name="permissions"></a>Restringir permissões tooauthenticated usuários
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* No Android Studio, abrir projeto de saudação é concluída com o tutorial Olá [começar com aplicativos móveis]. De saudação **executar** menu, clique em **executar aplicativo**e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.

     Essa exceção ocorre porque as tentativas de aplicativo hello tooaccess Olá volta encerrar como um usuário não autenticado, mas Olá *TodoItem* tabela agora requer autenticação.

Em seguida, você deve atualizar os usuários tooauthenticate de aplicativo hello antes de solicitar recursos do hello que terminar de volta a aplicativos móveis. 

## <a name="add-authentication-toohello-app"></a>Adicionar autenticação toohello aplicativo
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Tokens de autenticação de cache no cliente de saudação
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Próximas etapas
Agora que você concluiu este tutorial de autenticação básica, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:

* [Adicionar aplicativo do Android push notificações tooyour](app-service-mobile-android-get-started-push.md).
  Saiba como tooconfigure fazer seus aplicativos móveis encerrar notificações por push de toosend de hubs do toouse notificação do Azure.
* [Habilitar a sincronização offline para o aplicativo móvel Android](app-service-mobile-android-get-started-offline-data.md).
  Saiba como o tooadd offline dão suporte ao aplicativo tooyour usando um back-end de aplicativos móveis. Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[começar com aplicativos móveis]: app-service-mobile-android-get-started.md
