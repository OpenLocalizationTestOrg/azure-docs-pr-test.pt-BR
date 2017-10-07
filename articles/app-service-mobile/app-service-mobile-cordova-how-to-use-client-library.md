---
title: "aaaHow tooUse plug-in do Apache Cordova para aplicativos móveis do Azure"
description: "Como tooUse plug-in do Apache Cordova para aplicativos móveis do Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>Como biblioteca de cliente do Apache Cordova toouse para aplicativos móveis do Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Este guia ensina usando hello mais recente de cenários comuns de tooperform [plug-in do Apache Cordova para aplicativos móveis do Azure]. Se você for novo tooAzure os aplicativos móveis, primeiro conclua [início rápido do Azure Mobile aplicativos] toocreate um back-end, crie uma tabela e baixar um projeto do Apache Cordova pré-criado. Neste guia, vamos nos concentrar no lado do cliente Olá plug-in do Apache Cordova.

## <a name="supported-platforms"></a>Plataformas com suporte
Esse SDK dá suporte à versão 6.0.0 do Apache Cordova e posterior nos dispositivos iOS, Android e Windows.  suporte a plataformas Olá é o seguinte:

* API do Android 19 a 24 (KitKat usando Nougat).
* iOS versão 8.0 e posterior.
* Windows Phone 8.1.
* Plataforma Universal do Windows.

## <a name="Setup"></a>Configuração e pré-requisitos
Este guia pressupõe que você tenha criado um back-end com uma tabela. Este guia presume que tabela Olá tenha Olá mesmo esquema de tabelas Olá esses tutoriais. Este guia também pressupõe que você adicionou o código de tooyour Olá plug-in do Apache Cordova.  Se você não tiver feito isso, você pode adicionar o projeto de tooyour Olá Apache Cordova plug-in na linha de comando hello:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Para saber mais sobre como criar [seu primeiro aplicativo do Apache Cordova], consulte a documentação.

## <a name="ionic"></a>Configurar um aplicativo Ionic v2

tooproperly configurar um projeto Ionic v2, primeiro criar um aplicativo básico e adicionar plug-in Cordova de saudação:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Adicionar Olá linhas seguintes muito`app.component.ts` objeto de toocreate saudação do cliente:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

Você agora pode compilar e executar o projeto Olá no navegador de saudação:

```
ionic platform add browser
ionic run browser
```

plug-in de Cordova de aplicativos móveis do Azure Olá dá suporte a ambos os aplicativos Ionic v1 e v2.  Somente aplicativos Olá v2 Ionic requerem a declaração adicional para Olá `WindowsAzure` objeto.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Como autenticar usuários
O Serviço de Aplicativo do Azure oferece suporte à autenticação e autorização de usuários de aplicativos usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft e Twitter. Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários. Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização nos scripts de servidor. Para obter mais informações, consulte Olá [Introdução à autenticação] tutorial.

Ao usar a autenticação em um aplicativo do Apache Cordova, Olá plug-ins do Cordova a seguir deve estar disponível:

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

Dois fluxos de autenticação são suportados: um server flow e um client flow.  fluxo do servidor de saudação fornece experiência de autenticação mais simples de Olá, como ele se baseia na interface de autenticação do provedor de saudação da web. Olá fluxo cliente permite integração mais profunda com recursos específicos do dispositivo, como single-sign-on pois depende de SDKs de específico do dispositivo específico do provedor.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Como configurar o Serviço de Aplicativo Móvel para URLs de redirecionamento externo.
Vários tipos de aplicativos do Apache Cordova usam um toohandle de capacidade de loopback que OAuth UI flui.  Fluxos de OAuth UI no localhost causam problemas desde que o serviço de autenticação da saudação só sabe como tooutilize seu serviço por padrão.  Exemplos de fluxos de interface do usuário OAuth problemáticos incluem:

* emulador do Ripple Hello.
* Recarregamento dinâmico com Ionic.
* Em execução Olá móvel back-end localmente
* Executando o back-end de saudação móvel em um serviço de aplicativo do Azure diferente que a autenticação fornecendo uma saudação.

Siga essas instruções tooadd sua configuração de toohello configurações locais:

1. Faça logon no toohello [portal do Azure]
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu aplicativo móvel.
3. Clique em **Ferramentas**
4. Clique em **Gerenciador de recursos** no menu OBSERVE Olá, em seguida, clique em **vá**.  Uma nova janela ou guia é aberta.
5. Expanda Olá **config**, **authsettings** nós para o seu site na navegação esquerda hello.
6. Clique em **Editar**
7. Procure o elemento de "allowedExternalRedirectUrls" hello.  Ele pode ser definido toonull ou uma matriz de valores.  Alterar Olá valor toohello seguinte valor:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Substitua URLs Olá Olá URLs do serviço.  Exemplos incluem "http://localhost:3000" (para Olá serviço de exemplo do Node. js) ou "http://localhost:4400" (para o serviço de ondulação Olá).  No entanto, essas URLs são exemplos - sua situação, incluindo serviços de saudação mencionados nos exemplos Olá, podem ser diferentes.
8. Clique em Olá **leitura/gravação** botão no canto superior direito de saudação da tela hello.
9. Clique em Olá verde **colocar** botão.

configurações de saudação são salvas neste momento.  Não feche a janela do navegador Olá até que as configurações de saudação concluiu a salvar.
Também adicione essas configurações de CORS loopback URLs toohello para o serviço de aplicativo:

1. Faça logon no toohello [portal do Azure]
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu aplicativo móvel.
3. folha de configurações de saudação é aberto automaticamente.  Se não for, clique em **Todas as Configurações**.
4. Clique em **CORS** menu Olá API.
5. Digite a URL Olá que você deseja tooadd na caixa Olá fornecida e pressione Enter.
6. Insira URLs adicionais conforme necessário.
7. Clique em **salvar** toosave configurações de saudação.

Leva aproximadamente 10 a 15 segundos para efeito de tootake do hello novas configurações.

## <a name="register-for-push"></a>Como registrar notificações por push
Instalar Olá [phonegap de plug-in de push] toohandle notificações de envio.  Este plug-in pode ser facilmente adicionada usando o `cordova plugin add` comando na linha de comando hello, ou por meio do instalador de plug-in de Git hello dentro do Visual Studio.  O código a seguir em seu aplicativo Apache Cordova registra seu dispositivo para notificações por push:

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Use notificações de push de toosend Olá SDK de Hubs de notificação do servidor de saudação.  Nunca envie notificações por push diretamente dos clientes. Fazer assim pode ser usado tootrigger um ataque de negação de serviço em relação a Hubs de notificação ou Olá PNS.  Olá PNS pode proibir o tráfego como resultado de tais ataques.

## <a name="more-information"></a>Mais informações

Você pode encontrar detalhes de API detalhadas em nossa [Documentação da API](http://azure.github.io/azure-mobile-apps-js-client/).

<!-- URLs. -->
[portal do Azure]: https://portal.azure.com
[início rápido do Azure Mobile aplicativos]: app-service-mobile-cordova-get-started.md
[Introdução à autenticação]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[plug-in do Apache Cordova para aplicativos móveis do Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[seu primeiro aplicativo do Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap de plug-in de push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
