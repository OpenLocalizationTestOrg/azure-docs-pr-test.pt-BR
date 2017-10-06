---
title: "aaaAzure integração do SDK do Mobile Engagement Web | Microsoft Docs"
description: "Olá atualizações mais recentes e procedimentos para Olá Web SDK do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Integrar o Azure Mobile Engagement em um aplicativo Web
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Olá neste artigo descrevem a análise do hello mais simples maneira tooactivate hello e funções no Azure Mobile Engagement em seu aplicativo web de monitoramento.

Siga Olá etapas tooactivate Olá relatórios de log que são necessária toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e technicals. Para estatísticas depende do aplicativo, como eventos, erros e trabalhos, você deve ativar relatórios de log manualmente usando Olá API do Azure Mobile Engagement. Para obter mais informações, saiba [como toouse Olá avançado marcação API em um aplicativo web do Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Introdução
[Baixar Olá Web SDK do Azure Mobile Engagement](http://aka.ms/P7b453).
Olá Mobile Engagement SDK da Web é enviado como um único arquivo de JavaScript, o azure-engagement.js, você tem tooinclude em cada página do seu site ou aplicativo web.

> [!IMPORTANT]
> Antes de executar esse script, você deve executar um script ou que você escreva tooconfigure Mobile Engagement para o seu aplicativo de trecho de código.
> 
> 

## <a name="browser-compatibility"></a>Compatibilidade de navegador
Olá Web SDK do Mobile Engagement usa JSON nativo de codificação e decodificação, além de solicitações do AJAX toocross domínio (terceira na especificação do W3C CORS Olá). Ele é compatível com hello navegadores a seguir:

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5 e superior
* Chrome 4+
* Safari 6+
* Opera 12 e superior

## <a name="configure-mobile-engagement"></a>Configurar o Mobile Engagement
Escrever um script que cria um global `azureEngagement` objeto do JavaScript, como no exemplo a seguir de saudação. Pelo fato de que seu site pode ter várias páginas, este exemplo supõe que este script esteja incluído em cada página. Neste exemplo, o objeto de JavaScript do hello é denominado `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Olá `connectionString` valor para seu aplicativo é exibido no portal do Azure hello.

> [!NOTE]
> `appVersionName` e `appVersionCode` são opcionais. No entanto, é recomendável configurá-los para que a análise possa processar informações de versão.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Incluir scripts do Mobile Engagement em suas páginas
Adicione páginas do Mobile Engagement scripts tooyour em uma saudação maneiras a seguir:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

Ou assim:

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Depois de saudação script do SDK do Mobile Engagement da Web é carregada, cria Olá **contrato** tooaccess alias Olá APIs do SDK. Você não pode usar essa configuração de SDK do alias toodefine hello. Esse alias é usado como uma referência nesta documentação.

Observe que se o alias do saudação padrão em conflito com outra variável global de sua página, você pode redefini-la na configuração Olá da seguinte maneira antes de carregar Olá Web SDK do Mobile Engagement:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Relatórios básicos
Os relatórios básicos no Mobile Engagement abordam as estatísticas de nível de sessão, como estatísticas sobre usuários, sessões, atividades e falhas.

### <a name="session-tracking"></a>Rastreamento de sessão
Uma sessão do Mobile Engagement é dividida em uma sequência de atividades, cada uma delas identificada por um nome.

Em um site clássico, é recomendável declarar uma atividade diferente em cada página do site. Para um site ou aplicativo web no qual Olá página atual nunca muda, talvez você queira tootrack atividades de saudação em menor escala, como na página de saudação.

Ou, toostart ou alterar hello atividade do usuário atual, chamada hello `engagement.agent.startActivity` função. Por exemplo:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

servidor do Mobile Engagement Olá automaticamente encerra uma sessão aberta em três minutos após a página de aplicativo hello está fechada.

Como alternativa, você pode encerrar uma sessão manualmente chamando `engagement.agent.endActivity`. Isso define too'Idle de atividade de usuário atual do hello.'  sessão de saudação terminará 10 segundos mais tarde, a menos que uma nova chamada muito`engagement.agent.startActivity` retoma a sessão de saudação.

Você pode configurar o atraso de 10 segundos Olá no objeto de contrato global hello, da seguinte maneira:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> Não é possível usar `engagement.agent.endActivity` em Olá `onunload` retorno de chamada porque você não pode fazer chamadas AJAX neste estágio.
> 
> 

## <a name="advanced-reporting"></a>Relatórios avançados
Opcionalmente, se você quiser trabalhos, erros e eventos específicos de aplicativos de tooreport, você precisa toouse Olá Mobile Engagement API. Você acessa Olá API do Mobile Engagement por meio de saudação `engagement.agent` objeto.

Você pode acessar todos Olá avançado de recursos do Mobile Engagement no hello Mobile Engagement API. Olá API é detalhado no artigo Olá [como toouse Olá avançado marcação API em um aplicativo web do Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Personalizar URLs Olá usadas para chamadas AJAX
Você pode personalizar URLs que Olá que usa o SDK do Mobile Engagement da Web. Por exemplo, tooredefine Olá log URL (Olá SDK ponto de extremidade para o log), você pode substituir a configuração de saudação assim:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Se suas funções de URL retornam uma cadeia de caracteres que começa com `/`, `//`, `http://`, ou `https://`, esquema de padrão de saudação não é usada. Por padrão, Olá `https://` esquema é usada para as URLs. Se desejar que o esquema padrão do toocustomize hello, substitua configuração hello, assim:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
