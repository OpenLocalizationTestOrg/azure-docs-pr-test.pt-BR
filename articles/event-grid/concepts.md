---
title: conceitos de grade de eventos aaaAzure
description: "Descreve a Grade de Eventos do Azure e seus conceitos. Define vários componentes importantes da Grade de Eventos."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Conceitos da Grade de Eventos do Azure

principais conceitos Olá na grade de eventos do Azure são:

## <a name="events"></a>Eventos

Um evento é o mínimo de saudação de informações que descreve totalmente algo que ocorreram no sistema de saudação.  Cada evento tem informações comuns, como: origem do evento hello, evento de tempo de saudação levou local e o identificador exclusivo.  Cada evento também tem informações que são somente toohello relevantes de evento específico. Por exemplo, um evento sobre um novo arquivo que está sendo criado no armazenamento do Azure contém detalhes sobre o arquivo hello, como o valor de lastTimeModified hello. Ou, um evento sobre a reinicialização de uma máquina virtual contém o nome de saudação de máquina virtual de saudação e motivo Olá para reinicialização.

## <a name="event-sourcespublishers"></a>Origens/fornecedores do evento

Uma fonte de evento é onde ocorre o evento Olá. Por exemplo, armazenamento do Azure é a origem do evento Olá para blob criado eventos. Malha de VM do Azure é a origem do evento de saudação para eventos de máquina virtual. Fontes de evento são responsáveis por publicar eventos tooEvent grade.

## <a name="topics"></a>Tópicos

Os fornecedores categorizam eventos em tópicos. tópico de saudação inclui um ponto de extremidade em que o publicador Olá envia eventos. tipos de toocertain toorespond de eventos, os assinantes decidir qual toosubscribe tópicos para. Tópicos também fornecem um esquema de evento para que os assinantes possam descobrir como tooconsume Olá eventos adequadamente.

Os tópicos do sistema são tópicos internos fornecidos pelos serviços do Azure. Os tópicos personalizados são tópicos de aplicativo e de terceiros.

## <a name="event-subscriptions"></a>Assinaturas de evento

Uma assinatura orienta a Grade de Eventos sobre quais eventos em um tópico um assinante está interessado em receber.  Uma assinatura também contém informações sobre como os eventos devem ser entregues toohello assinante.

## <a name="event-handlers"></a>Manipuladores de eventos

De uma perspectiva de grade de eventos, um manipulador de eventos é local Olá onde o evento de saudação é enviado. manipulador de saudação usa algum evento de saudação de tooprocess ação adicional.  A Grade de Eventos dá suporte a vários tipos de assinante. Dependendo do tipo de saudação do assinante, a grade de eventos segue entrega de saudação tooguarantee diferentes mecanismos de evento hello.  HTTP webhook manipuladores de eventos, eventos de saudação é repetido até que o manipulador de saudação retorna um código de status `200 – OK`. Para fila de armazenamento do Azure, eventos Olá são repetidos até Olá serviço fila é o envio de mensagem de saudação toosuccessfully capaz de processo na fila de saudação.

## <a name="filters"></a>Filtros

Ao inscrever-se tooa tópico, você pode filtrar eventos de saudação enviadas toohello de ponto de extremidade. É possível filtrar por tipo de evento ou padrão de assunto. Para saber mais, confira [Esquema de assinatura da Grade de Eventos](subscription-creation-schema.md).

## <a name="security"></a>Segurança

Evento fornece segurança para assinatura tootopics e tópicos de publicação. Ao inscrever-se, você deve ter as permissões adequadas nos recursos de saudação ou tópico. Ao publicar, você deve ter um token SAS ou autenticação de chave para o tópico de saudação. Para saber mais, confira [Event Grid security and authentication](security-authentication.md) (Segurança e autenticação da Grade de Eventos).

## <a name="failed-delivery"></a>Falha na entrega

Quando a grade de eventos não pode confirmar que um evento foi recebido pelo ponto de extremidade do assinante hello, entrega novamente evento hello. Para saber mais, confira [Event Grid message delivery and retry](delivery-and-retry.md) (Entrega e repetição de mensagens da Grade de Eventos).

## <a name="next-steps"></a>Próximas etapas

* Para uma introdução tooEvent grade, consulte [sobre o evento grade](overview.md).
* tooquickly começar a usar a grade de eventos, consulte [rota e criar eventos personalizados com a grade de eventos do Azure](custom-event-quickstart.md).
