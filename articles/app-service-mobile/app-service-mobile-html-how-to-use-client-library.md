---
title: "aaaHow tooUse Olá SDK de JavaScript para aplicativos móveis do Azure"
description: "Como v tooUse para aplicativos móveis do Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Como o tooUse hello biblioteca de cliente JavaScript para aplicativos móveis do Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Este guia ensina usando hello mais recente de cenários comuns de tooperform [SDK de JavaScript para aplicativos móveis do Azure]. Se você for novo tooAzure os aplicativos móveis, primeiro conclua [início rápido do Azure Mobile aplicativos] toocreate um back-end e criar uma tabela. Este guia, vamos nos concentrar em usar o back-end de saudação móvel em aplicativos Web HTML/JavaScript.

## <a name="supported-platforms"></a>Plataformas com suporte
Podemos limite atual de toohello de suporte do navegador e versões de saudação da última principais navegadores: Microsoft Edge, Google Chrome, o Microsoft Internet Explorer e Mozilla Firefox.  Esperamos Olá SDK toofunction com qualquer navegador moderno relativamente.

pacote de saudação é distribuído como um módulo de JavaScript Universal, para que ele suporta globais, AMD, e formatos de CommonJS.

## <a name="Setup"></a>Configuração e pré-requisitos
Este guia pressupõe que você tenha criado um back-end com uma tabela. Este guia presume que tabela Olá tenha Olá mesmo esquema de tabelas Olá esses tutoriais.

Instalar Olá SDK de JavaScript de aplicativos móveis do Azure pode ser feito por meio de saudação `npm` comando:

```
npm install azure-mobile-apps-client --save
```

biblioteca de saudação também pode ser usada como um módulo ES2015, em ambientes de CommonJS como Browserify e Webpack e como uma biblioteca AMD.  Por exemplo:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

Você também pode usar uma versão pré-criado do hello SDK baixando diretamente do nosso CDN:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Como autenticar usuários
O Serviço de Aplicativo do Azure oferece suporte à autenticação e autorização de usuários de aplicativos usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft e Twitter. Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários. Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização nos scripts de servidor. Para obter mais informações, consulte Olá [Introdução à autenticação] tutorial.

Dois fluxos de autenticação são suportados: um server flow e um client flow.  fluxo do servidor de saudação fornece experiência de autenticação mais simples de Olá, como ele se baseia na interface de autenticação do provedor de saudação da web. Olá fluxo cliente permite integração mais profunda com recursos específicos do dispositivo, como single-sign-on como ele se baseia em SDKs específicos de provedor.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Como configurar o Serviço de Aplicativo Móvel para URLs de redirecionamento externo.
Vários tipos de aplicativos JavaScript usam um toohandle de capacidade de loopback que OAuth UI flui.  Esses recursos incluem:

* Executar o serviço localmente
* Usando o Live recarregar com hello Framework Ionic
* Redirecionando tooApp serviço para autenticação.

Em execução localmente pode causar problemas porque, por padrão, a autenticação é apenas do serviço de aplicativo configurado o acesso de tooallow do seu back-end do aplicativo móvel. Use Olá seguindo as etapas toochange Olá autenticação de tooenable de configurações do serviço de aplicativo ao executar o servidor de saudação localmente:

1. Faça logon no toohello [portal do Azure]
2. Navegue back-end de aplicativo móvel tooyour.
3. Selecione **Gerenciador de recursos** em Olá **ferramentas de desenvolvimento** menu.
4. Clique em **vá** Gerenciador de recursos de saudação tooopen do seu back-end do aplicativo móvel em uma nova guia ou janela.
5. Expanda Olá **config** > **authsettings** nó para seu aplicativo.
6. Clique em Olá **editar** botão tooenable edição do recurso de saudação.
7. Localize Olá **allowedExternalRedirectUrls** elemento, que deve ser nulo. Adicione as URLs em uma matriz:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Substitua Olá URLs na matriz Olá Olá URLs do serviço, que neste exemplo é `http://localhost:3000` para o serviço de exemplo hello local Node. js. Você também pode usar `http://localhost:4400` para serviço de ondulação hello ou outra URL, dependendo de como seu aplicativo está configurado.
8. Na parte superior de saudação da página de saudação, clique em **leitura/gravação**, em seguida, clique em **colocar** toosave suas atualizações.

Você também precisa tooadd Olá configurações de lista branca do mesmo loopback URLs toohello CORS:

1. Navegue back toohello [portal do Azure].
2. Navegue back-end de aplicativo móvel tooyour.
3. Clique em **CORS** em Olá **API** menu.
4. Insira cada URL no hello vazio **origens permitidas** caixa de texto.  Uma nova caixa de texto é criada.
5. Clique em **SALVAR**

Depois Olá back-end de atualizações, você será capaz de toouse Olá novas URLs de loopback em seu aplicativo.

<!-- URLs. -->
[início rápido do Azure Mobile aplicativos]: app-service-mobile-cordova-get-started.md
[Introdução à autenticação]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portal do Azure]: https://portal.azure.com/
[SDK de JavaScript para aplicativos móveis do Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
