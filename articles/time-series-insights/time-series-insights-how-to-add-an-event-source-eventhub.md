---
title: "aaaHow tooadd um ambiente Azure Insights de série de tempo do Hub de eventos evento fonte tooyour | Microsoft Docs"
description: "Este tutorial aborda como tooadd um evento que é fonte conectada tooan Hub de eventos tooyour Insights de série de tempo ambiente"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>Como uma fonte de evento de Hub de eventos de tooadd

Este tutorial aborda como toouse Olá tooadd portal do Azure a uma fonte de evento que lê de um ambiente de informações da série de tempo de tooyour do Hub de eventos.

## <a name="prerequisites"></a>Pré-requisitos

Você criou um Hub de eventos e estiver gravando tooit de eventos. Para saber mais sobre Hubs de Eventos, visite <https://azure.microsoft.com/services/event-hubs/>

> [Grupos de consumidores] Cada fonte de evento de informações da série de tempo precisa toohave seu próprio grupo de consumidores exclusivo que não é compartilhado com outros consumidores. Se vários leitores consumam eventos de Olá mesmo grupo de consumidores, todos os leitores são provavelmente toosee falhas. Observe que também há um limite de 20 grupos de consumidores por Hub de Eventos. Para obter detalhes, consulte Olá [guia de programação de Hubs de evento](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Escolher uma opção de importação

configurações de saudação de origem do evento Olá podem ser inseridas manualmente ou um hub de eventos pode ser selecionado de hubs de eventos de saudação são tooyou disponível.
Em Olá **opção Importar** seletor, escolha uma saudação as opções a seguir:

* Fornecer configurações de Hub de Eventos manualmente
* Usar o Hub de Eventos nas assinaturas disponíveis

### <a name="select-an-available-event-hub"></a>Selecionar um Hub de Eventos disponível

Olá tabela a seguir explica cada opção na guia da nova fonte de evento de saudação com sua descrição ao selecionar um Hub de eventos disponíveis como uma fonte de evento:

| Nome da Propriedade | Descrição |
| --- | --- |
| Nome da origem do evento | nome de saudação de sua fonte de evento. Esse nome deve ser exclusivo no ambiente de Análise de Séries Temporais.
| Fonte | Escolha **Hub de eventos** toocreate uma fonte de evento de Hub de eventos.
| ID da assinatura | Selecione a assinatura Olá no qual este hub de eventos foi criado.
| Namespace do Barramento de Serviço | Selecione o namespace de barramento de serviço de saudação que contém Olá Hub de eventos.
| Nome do Hub de Eventos | Selecione o nome de saudação do hello Hub de eventos.
| Nome da política do hub de eventos | Selecione a política de acesso de Olá compartilhado, que pode ser criada na guia Configurar do Hub de eventos de saudação. Cada política de acesso compartilhado tem um nome, as permissões definidas por você e as chaves de acesso. Olá compartilhado política de acesso para a origem do evento *deve* ter **ler** permissões.
| Grupo de consumidores do hub de eventos | eventos de tooread de grupo de consumidores de saudação de saudação Hub de eventos. É altamente recomendável toouse um grupo de consumidores exclusivo para a origem do evento.

### <a name="provide-event-hub-settings-manually"></a>Fornecer configurações de Hub de Eventos manualmente

Olá tabela a seguir explica cada propriedade no guia de nova fonte de evento de saudação com sua descrição ao inserir as configurações manualmente:

| Nome da Propriedade | Descrição |
| --- | --- |
| Nome da origem do evento | nome de saudação de sua fonte de evento. Esse nome deve ser exclusivo no ambiente de Análise de Séries Temporais.
| Fonte | Escolha **Hub de eventos** toocreate uma fonte de evento de Hub de eventos.
| ID da assinatura | assinatura de saudação no qual este hub de eventos foi criado.
| Grupo de recursos | assinatura de saudação no qual este hub de eventos foi criado.
| Namespace do Barramento de Serviço | Um namespace Barramento de Serviço é um contêiner para um conjunto de entidades de mensagens. Ao criar um novo Hub de Eventos, você também criou um namespace Barramento de Serviço.
| Nome do Hub de Eventos | nome de saudação do seu Hub de eventos. Quando você criou o hub de eventos, também deu a ele um nome específico
| Nome da política do hub de eventos | Olá política de acesso compartilhado, que pode ser criada na guia Configurar do Hub de eventos de saudação. Cada política de acesso compartilhado tem um nome, as permissões definidas por você e as chaves de acesso. Olá compartilhado política de acesso para a origem do evento *deve* ter **ler** permissões.
| Chave de política do hub de eventos | chave de acesso compartilhado Olá usado namespace de barramento de serviço de toohello tooauthenticate acesso. Digite hello chave primária ou secundária aqui.
| Grupo de consumidores do hub de eventos | eventos de tooread de grupo de consumidores de saudação de saudação Hub de eventos. É altamente recomendável toouse um grupo de consumidores exclusivo para a origem do evento.

## <a name="next-steps"></a>Próximas etapas

1. Adicionar um ambiente de tooyour de política de acesso de dados [dados definir políticas de acesso](time-series-insights-data-access.md)
1. Acessar seu ambiente no hello [Portal de Insights de série de tempo](https://insights.timeseries.azure.com)
