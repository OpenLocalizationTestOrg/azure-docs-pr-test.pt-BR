---
title: aaaAzure APIs do SDK do Mobile Engagement Web | Microsoft Docs
description: "Olá procedimentos para Olá Web SDK e atualizações mais recentes para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Saudação de usar a API do Azure Mobile Engagement em um aplicativo web
Este é um documento de toohello adição que informa como muito[integrar o Mobile Engagement em um aplicativo web](mobile-engagement-web-integrate-engagement.md). Ele fornece detalhes sobre como toouse Olá tooreport da API do Azure Mobile Engagement suas estatísticas do aplicativo.

Olá Mobile Engagement API fornecida pelo Olá `engagement.agent` objeto. Olá padrão da Web SDK do Azure Mobile Engagement alias é `engagement`. Você pode redefinir este alias da configuração de SDK hello.

## <a name="mobile-engagement-concepts"></a>Conceitos do Mobile Engagement
Olá seguintes partes refinar comuns [conceitos do Mobile Engagement](mobile-engagement-concepts.md) de plataforma da web de saudação.

### <a name="session-and-activity"></a>`Session` e `Activity`
Se o usuário Olá permanecer ocioso por mais de alguns segundos entre duas atividades, hello sequência do usuário de atividades é dividida em duas sessões distintas. Esses alguns segundos são chamados de tempo limite da sessão hello.

Se seu aplicativo da web não declara final Olá de atividades do usuário por si só (por chamada hello `engagement.agent.endActivity` função), servidor do Mobile Engagement Olá expira automaticamente Olá sessão de usuário dentro de três minutos após a página de aplicativo hello está fechada. Isso é chamado de tempo limite de sessão de servidor de saudação.

### `Crash`
Relatórios automatizados de exceções não identificadas de JavaScript não são criados por padrão. No entanto, você pode relatar falhas manualmente usando Olá `sendCrash` função (consulte a seção de saudação nos relatórios de falhas).

## <a name="reporting-activities"></a>Relatando atividades
Relatório de atividade de usuário inclui quando um usuário inicia uma nova atividade e quando o usuário Olá termina a atividade atual de saudação.

### <a name="user-starts-a-new-activity"></a>O usuário inicia uma nova atividade
    engagement.agent.startActivity("MyUserActivity");

Você precisa toocall `startActivity()` alterações de cada atividade de usuário do tempo. Olá primeira chamada toothis função inicia uma nova sessão de usuário.

### <a name="user-ends-hello-current-activity"></a>Usuário encerra a atividade atual de saudação
    engagement.agent.endActivity();

Você precisa toocall `endActivity()` pelo menos uma vez quando o usuário Olá termina sua última atividade. Isso informa Olá Web SDK do Mobile Engagement que usuário hello está ocioso no momento e que a sessão de usuário Olá precisa toobe fechado após a expiração do tempo limite da sessão hello. Se você chamar `startActivity()` antes do tempo limite da sessão Olá expira, a sessão Olá simplesmente é retomado.

Como não há nenhuma chamada confiável para quando a janela do navegador hello está fechada, geralmente é final de saudação toocatch difíceis ou impossíveis de atividades do usuário dentro de um ambiente web. Por que é Olá Mobile Engagement servidor expira automaticamente sessão de usuário hello dentro de três minutos após a página de aplicativo hello está fechada.

## <a name="reporting-events"></a>Relatando eventos
Relatórios sobre eventos abordam eventos de sessão e eventos autônomos.

### <a name="session-events"></a>Eventos de sessão
Eventos de sessão normalmente são ações de saudação tooreport usado executadas por um usuário durante a sessão de saudação do usuário.

**Exemplo sem dados adicionais:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Exemplo com dados adicionais:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Eventos autônomos
Ao contrário de eventos de sessão, podem ocorrer eventos de autônomo fora do contexto de saudação de uma sessão.

Para isso, use ``engagement.agent.sendEvent`` em vez de ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Relatando erros
Relatórios de erros abordam erros de sessão e autônomos.

### <a name="session-errors"></a>Erros de sessão
Erros de sessão normalmente são erros de saudação tooreport usadas que têm um impacto no usuário Olá durante a sessão do usuário hello.

**Exemplo sem dados adicionais:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Exemplo com dados adicionais:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Erros autônomos
Ao contrário dos erros de sessão, podem ocorrer erros de autônomo fora do contexto de saudação de uma sessão.

Para isso, use `engagement.agent.sendError` em vez de `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Relatando trabalhos
Relatórios sobre trabalhos abrangem erros e eventos que ocorrem durante um trabalho de emissão de relatórios e relatórios de falhas.

**Exemplo:**

Se você quiser toomonitor uma solicitação AJAX, você usaria o seguinte hello:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Relatando erros durante um trabalho
Erros podem ser relacionada tooa executando o trabalho em vez de toohello sessão do usuário atual.

**Exemplo:**

Se você quiser tooreport um erro se uma solicitação AJAX falha:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Relatar eventos durante um trabalho
Os eventos podem ser relacionada tooa executando o trabalho em vez de toohello a sessão atual do usuário, graças toohello `engagement.agent.sendJobEvent` função.

Essa função funciona exatamente como `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Relatando falhas
Saudação de uso `sendCrash` função tooreport falhas manualmente.

Olá `crashid` argumento é uma cadeia de caracteres que identifica o tipo de saudação de travamento.
Olá `crash` argumento geralmente é o rastreamento de pilha de saudação de travamento hello como uma cadeia de caracteres.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Parâmetros adicionais
Você pode anexar dados arbitrários tooan eventos, erro, atividade ou trabalho.

dados de saudação podem ser qualquer objeto JSON (mas não uma matriz ou tipo primitivo).

**Exemplo:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>limites
Limites que se aplicam a parâmetros tooextra são áreas de saudação de expressões regulares para chaves, tipos de valor e tamanho.

#### <a name="keys"></a>simétricas
Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:

    ^[a-zA-Z][a-zA-Z_0-9]*

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="values"></a>Valores
Os valores são toostring limitado, número e tipos boolianos.

#### <a name="size"></a>Tamanho
Extras são limitados too1, 024 caracteres por chamada (após Olá Web SDK do Mobile Engagement codifica em JSON).

## <a name="reporting-application-information"></a>Relatando informações de aplicativo
Você pode relatar informações (ou quaisquer outras informações específicas do aplicativo) de rastreamento manualmente usando Olá `sendAppInfo()` função.

Observe que essas informações podem ser enviadas de forma incremental. Somente Olá valor mais recente para uma chave específica será mantido para um dispositivo específico.

Como o evento extras, você pode usar informações de aplicativo tooabstract do objeto JSON. Observe que matrizes ou subobjetos são tratados como cadeias de caracteres simples (usando a serialização JSON).

**Exemplo:**

Aqui está um exemplo de código de gênero do usuário Olá envio e a data de nascimento:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>limites
Limites que se aplicam a tooapplication informações estão em áreas de saudação de expressões regulares de chaves e tamanho.

#### <a name="keys"></a>simétricas
Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:

    ^[a-zA-Z][a-zA-Z_0-9]*

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Informações do aplicativo são limitado too1, 024 caracteres por chamada (após Olá Web SDK do Mobile Engagement codifica em JSON).

Em Olá anterior de exemplo, hello JSON enviado toohello server é 44 caracteres:

    {"birthdate":"1983-12-07","gender":"female"}
