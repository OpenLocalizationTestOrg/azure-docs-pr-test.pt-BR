---
title: entrega de grade de eventos aaaAzure e repetir
description: "Descreve como a Grade de Eventos do Azure entrega eventos e como ela trata mensagens não entregues."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Entrega e repetição de mensagens da Grade de Eventos 

Este artigo descreve como a Grade de Eventos do Azure trata os eventos quando a entrega não é confirmada.

A entrega proporcionada pela Grade de Eventos tem um tempo de duração. Cada mensagem é entregue pelo menos uma vez para cada assinatura. Eventos são enviados imediatamente webhook toohello registrado de cada assinatura. Se um webhook não confirmar o recebimento de um evento dentro de 60 segundos de entrega de saudação primeira tentativa, grade de eventos tentativas de entrega de eventos de saudação.

## <a name="message-delivery-status"></a>Status de entrega da mensagem

Grade de eventos usa o recebimento de tooacknowledge de códigos de resposta HTTP de eventos. 

### <a name="success-codes"></a>Códigos de êxito

Olá seguintes códigos de resposta HTTP indicam que um evento foi entregue com êxito tooyour webhook. A Grade de Eventos considera entrega concluída.

- 200 OK
- 202 Aceito

### <a name="failure-codes"></a>Códigos de falha

Olá códigos de resposta HTTP a seguir indica que houve falha na tentativa de entrega de eventos. Grade de eventos tenta novamente o evento de saudação toosend. 

- 400 Solicitação Inválida
- 401 Não Autorizado
- 404 Não Encontrado
- 408 Tempo limite da solicitação
- 414 URI muito longo
- 500 Erro Interno do Servidor
- 503 Serviço Indisponível
- 504 Tempo Limite do Gateway

Qualquer outro código de resposta ou à falta de uma resposta indica uma falha. A Grade de Eventos repete a entrega. 

## <a name="retry-intervals"></a>Intervalos de repetição

A Grade de Eventos usa uma política de repetição de retirada exponencial para a entrega de eventos. Se o webhook não responde ou retorna um código de falha, grade de eventos tentativas de entrega em Olá agenda a seguir:

1. 10 segundos
2. 30 segundos
3. 1 minuto
4. 5 minutos
5. 10 minutos
6. 30 minutos
7. 1 hora

Grade de eventos adiciona um intervalos de repetição tooall aleatória pequena.

## <a name="retry-duration"></a>Duração da repetição

Durante a visualização de hello, a grade de eventos do Azure expirar todos os eventos que não são entregues dentro de duas horas. Antes da disponibilidade geral, esse tempo será maior too24 horas. 

## <a name="next-steps"></a>Próximas etapas

* Para uma introdução tooEvent grade, consulte [sobre o evento grade](overview.md).
* tooquickly começar a usar a grade de eventos, consulte [rota e criar eventos personalizados com a grade de eventos do Azure](custom-event-quickstart.md).
