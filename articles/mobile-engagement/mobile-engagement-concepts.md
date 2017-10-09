---
title: conceitos de contrato aaaMobile | Microsoft Docs
description: Conceitos do Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Conceitos do Azure Mobile Engagement
Mobile Engagement define algumas plataformas tooall suportada conceitos comuns. Este artigo descreve resumidamente os conceitos.

Este artigo é um bom começo, se você estiver tooMobile novo contrato. Verifique também se tooread Olá documentação toohello específico plataforma que você está usando, como ele será refinar conceitos Olá descritos neste artigo com mais detalhes e exemplos, bem como limitações possíveis.

## <a name="devices-and-users"></a>Dispositivos e usuários
O Mobile Engagement identifica os usuários gerando um identificador exclusivo para cada dispositivo. Esse identificador é chamado de identificador de dispositivo hello (ou `deviceid`). Ele é gerado de forma que a execução de todos os aplicativos de Olá mesmo compartilhamento de dispositivo Olá mesmo identificador de dispositivo.

Implicitamente, isso significa que o Mobile Engagement considera um dispositivo toobelong tooexactly um usuário, e assim, os usuários e dispositivos são conceitos equivalentes.

## <a name="sessions-and-activities"></a>Sessões e atividades
Uma sessão é um uso de aplicativo hello executado por um usuário, do usuário Olá Olá inicia a usá-lo, Olá paradas de usuário.

Uma atividade é um uso de uma determinada peça subgrupos de aplicativo hello executada por um usuário (normalmente é uma tela, mas pode ser qualquer coisa adequado toohello aplicativo).

Um usuário só pode executar uma atividade por vez.

Uma atividade é identificada por um nome (limitado too64 caracteres) e, opcionalmente, pode inserir alguns dados adicionais (no limite de saudação de 1024 bytes).

Sessões são automaticamente computadas de sequência de saudação de atividades executadas pelos usuários. Uma sessão é iniciada quando o usuário Olá inicia sua primeira atividade e é interrompido quando ele termina sua última atividade. Isso significa que uma sessão não precisa toobe explicitamente iniciada ou interrompida. Em vez disso, as atividades são explicitamente iniciadas ou interrompidas. Se nenhuma atividade for relatada, nenhuma sessão será relatada.

## <a name="events"></a>Eventos
Eventos são ações de instantâneo tooreport usados (como o botão pressionado ou artigos lidos por usuários).

Um evento pode ser relacionado toohello sessão atual, tooa executando o trabalho, ou pode ser um evento autônomo.

Um evento é identificado por um nome (limitado too64 caracteres) e, opcionalmente, pode inserir alguns dados adicionais (no limite de saudação de 1024 bytes).

## <a name="error"></a>Erro
Os erros são usados tooreport problemas detectados corretamente pelo aplicativo hello (como ações de usuário incorreto, ou falhas de chamadas de API).

Um erro pode ser relacionado toohello sessão atual, tooa executando o trabalho, ou pode ser um erro de autônomo.

Um erro é identificado por um nome (limitado too64 caracteres) e, opcionalmente, pode inserir alguns dados adicionais (no limite de saudação de 1024 bytes).

## <a name="job"></a>Trabalho
As tarefas são ações tooreport usado com uma duração (como duração de chamadas de API, exibir tempo de anúncios, a duração das tarefas em segundo plano ou duração de ações de usuário).

Um trabalho não é relacionado tooa sessão, porque uma tarefa pode ser executada em segundo plano hello, sem qualquer interação do usuário.

Um trabalho é identificado por um nome (limitado too64 caracteres) e, opcionalmente, pode inserir alguns dados adicionais (no limite de saudação de 1024 bytes).

## <a name="crash"></a>Falha
Falhas são emitidas automaticamente pelo Olá aplicativo do SDK do Mobile Engagement tooreport falhas de falhas de onde os problemas não detectados pelo aplicativo hello torná-lo.

## <a name="application-information"></a>Informações do aplicativo
Informações do aplicativo (ou informações de aplicativo) é usado tootag usuários, ou seja, tooassociate alguns usuários toohello de dados de um aplicativo (Isso é cookies tooweb semelhante, exceto que as informações de aplicativo são armazenadas no lado do servidor de saudação na plataforma do Azure Mobile Engagement Olá).

Informações de aplicativo podem ser registradas usando a API do SDK do Mobile Engagement de saudação ou usando a plataforma do Mobile Engagement de saudação API do dispositivo.

Informações do aplicativo são um dispositivo de tooa associado do par chave/valor. chave de saudação é o nome de saudação de informações de aplicativo hello (limitado too64 ASCII letras [a-zA-Z], [0-9] de números e sublinhados [_]). o valor de saudação (limitado too1024 caracteres) pode ser qualquer cadeia de caracteres, o inteiro, a data (AAAA-MM-dd) ou o booleano (verdadeiro ou falso).

Qualquer número de informações de aplicativo pode ser dispositivo tooa associado, dentro dos limites de saudação definidos pelos termos de preço do hello Mobile Engagement. Para uma determinada chave, Mobile Engagement só mantém o controle de conjunto de valor mais recente hello (nenhum histórico). Definindo ou alterando o valor de saudação de informações de um aplicativo força o Mobile Engagement toore-avaliar critérios de público definido neste aplicativo informações (se houver) que significa que essas informações de aplicativo podem ser envios por push em tempo real de tootrigger usado.

## <a name="extra-data"></a>Dados extras
Dados extras (ou extras) são alguns dados arbitrários que podem ser anexados tooevents, erros, atividades e trabalhos.

Extras são estruturadas da mesma forma tooJSON objetos: eles são feitos de uma árvore de pares chave/valor. As chaves são letras ASCII de too64 limitada [a-zA-Z], [0-9] de números e sublinhados [_]) e tamanho total de saudação do extras é limitado too1024 caracteres (uma vez codificadas em JSON, Olá SDK do Mobile Engagement).

a árvore inteira Olá de pares chave/valor é armazenado como um objeto JSON. No entanto, somente Olá primeiro nível de chaves/valores é decomposta toobe diretamente acessível toosome avançado funções como segmentos (por exemplo, você pode definir facilmente um segmento chamado "SciFi ventiladores" que é composto de todos os usuários que enviou o evento de saudação de pelo menos 10 vezes chamado "content_viewed" com chave hello "tipo_de_conteúdo" conjunto toohello valor "scifi" no hello último mês). Portanto, ele é altamente recomendável toosend extras somente feitas de listas simples de pares chave/valor usando valores escalares (por exemplo, cadeias de caracteres, datas, números inteiros ou booleano).

## <a name="next-steps"></a>Próximas etapas
* [Visão geral do SDK do Windows Universal para o Azure Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md)
* [Visão geral do SDK do Windows Phone Silverlight para o Azure Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)
* [SDK do iOS para o Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [SDK do Android do Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

