---
title: "autenticação de aaaAdd no Apache Cordova com os aplicativos móveis | Microsoft Docs"
description: "Saiba como toouse aplicativos móveis de usuários do serviço de aplicativo do Azure tooauthenticate do seu aplicativo Apache Cordova por meio de uma variedade de provedores de identidade, como Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Adicionar aplicativo do Apache Cordova de tooyour de autenticação
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Resumo
Neste tutorial, você pode adicionar projeto de início rápido do autenticação toohello todolist no Apache Cordova usando um provedor de identidade com suporte. Este tutorial baseia-se a saudação [começar com aplicativos móveis] tutorial, que deve ser concluído primeiro.

## <a name="register"></a>Registrar seu aplicativo para autenticação e configurar saudação do serviço de aplicativo
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Assista a um vídeo que mostra etapas semelhantes](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Restringir permissões tooauthenticated usuários
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Agora, você pode verificar que essa back-end do acesso anônimo tooyour foi desabilitada. No Visual Studio:

* Projeto Olá abertos que você criou quando você concluiu o tutorial Olá [começar com aplicativos móveis].
* Executar o aplicativo no hello **emulador Android da Google**.
* Verifique se que uma falha inesperada da Conexão é exibida após o início do aplicativo hello.

Em seguida, atualize os usuários tooauthenticate de aplicativo hello antes de solicitar recursos de back-end de aplicativo móvel hello.

## <a name="add-authentication"></a>Adicionar autenticação toohello aplicativo
1. Abra seu projeto no **Visual Studio**, em seguida, Olá `www/index.html` arquivo para edição.
2. Localizar Olá `Content-Security-Policy` marca meta na seção de cabeçalho de saudação.  Adicione Olá OAuth host toohello lista de origens permitidas.

   | Provedor | Nome do provedor do SDK | Host OAuth |
   |:--- |:--- |:--- |
   | Active Directory do Azure | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    Veja a seguir um exemplo de Política de segurança de conteúdo (implementada para o Active Directory do Azure):

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Substituir `https://login.microsoftonline.com` com host OAuth Olá Olá anterior da tabela.  Para obter mais informações sobre a marca de meta de política de segurança de conteúdo hello, consulte Olá [documentação da política de segurança de conteúdo].

    Alguns provedores de autenticação não exigem mudanças no Content-Security-Policy quando usado em dispositivos móveis apropriados.  Por exemplo, nenhuma mudança na Política de segurança de conteúdo será necessária ao usar a autenticação do Google em um dispositivo Android.

3. Olá abrir `www/js/index.js` para edição de arquivos, localize Olá `onDeviceReady()` método, e na criação de cliente Olá código adicionar Olá código a seguir:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Esse código substitui Olá um código existente que cria a referência de tabela hello e atualiza a saudação da interface do usuário.

    método de login () do Hello inicia a autenticação com o provedor de saudação. método do Hello login () é uma função assíncrona que retorna uma promessa de JavaScript.  rest Olá da inicialização de saudação é colocada dentro Olá promessa resposta para que não será executado até que o método de login () do hello é concluído.

4. No código de saudação que você acabou de adicionar, substituir `SDK_Provider_Name` com nome de saudação do seu provedor de logon. Por exemplo, para o Azure Active Directory, use `client.login('aad')`.
5. Execute seu projeto.  Quando o projeto Olá concluiu a inicialização, seu aplicativo mostra a página de logon do OAuth Olá para Olá escolhido o provedor de autenticação.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais [Sobre autenticação] com o Serviço de Aplicativo do Azure.
* Continuar o tutorial Olá adicionando [notificações por Push] tooyour Apache Cordova app.

Saiba como toouse Olá SDKs.

* [SDK do Apache Cordova]
* [SDK do Servidor ASP.NET]
* [SDK do Servidor Node.js]

<!-- URLs. -->
[começar com aplicativos móveis]: app-service-mobile-cordova-get-started.md
[documentação da política de segurança de conteúdo]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[notificações por Push]: app-service-mobile-cordova-get-started-push.md
[Sobre autenticação]: app-service-mobile-auth.md
[SDK do Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK do Servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK do Servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
