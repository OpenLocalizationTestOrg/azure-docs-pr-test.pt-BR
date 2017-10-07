---
title: "aaaHow tooadd um ambiente de Insights de série de tempo de Azure IoT Hub evento fonte tooyour | Microsoft Docs"
description: "Este tutorial aborda como tooadd um evento de origem que é conectado tooan ambiente do IoT Hub tooyour Insights de série de tempo"
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
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Como tooadd uma fonte de evento de IoT Hub

Este tutorial aborda como toouse Olá tooadd portal do Azure a uma fonte de evento que lê de um ambiente do IoT Hub tooyour Insights de série de tempo.

## <a name="prerequisites"></a>Pré-requisitos

Você criou um IoT Hub e estiver gravando tooit de eventos. Para saber mais sobre Hubs IoT, visite <https://azure.microsoft.com/services/iot-hub/>

> [Grupos de consumidores] Cada fonte de evento de informações da série de tempo precisa toohave seu próprio grupo de consumidores exclusivo que não é compartilhado com outros consumidores. Se vários leitores consumam eventos de Olá mesmo grupo de consumidores, todos os leitores são provavelmente toosee falhas. Para obter detalhes, consulte Olá [guia do desenvolvedor de IoT Hub](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Escolher uma opção de importação

configurações de saudação de origem do evento Olá podem ser inseridas manualmente ou um hub IoT pode ser selecionado de hubs IoT Olá de tooyou disponível.
Em Olá **opção Importar** seletor, escolha uma saudação as opções a seguir:

* Fornecer configurações de Hub IoT manualmente
* Usar o Hub IoT nas assinaturas disponíveis

### <a name="select-an-available-iot-hub"></a>Selecionar um Hub IoT disponível

Olá tabela a seguir explica cada opção na guia da nova fonte de evento de saudação com sua descrição ao selecionar um IoT Hub disponível como uma fonte de evento:

| Nome da Propriedade | Descrição |
| --- | --- |
| Nome da origem do evento | nome de saudação de sua fonte de evento. Esse nome deve ser exclusivo no ambiente de Análise de Séries Temporais.
| Fonte | Escolha **IoT Hub** toocreate uma fonte de evento de IoT Hub.
| ID da assinatura | Selecione a assinatura Olá no qual este hub IoT foi criado.
| Nome do Hub IoT | Selecione o nome de saudação do hello IoT Hub.
| Nome da política do Hub IoT | Selecione a política de acesso compartilhada de saudação, que pode ser encontrada no guia de configurações do IoT Hub de saudação. Cada política de acesso compartilhado tem um nome, as permissões definidas por você e as chaves de acesso. Olá compartilhado política de acesso para a origem do evento *deve* ter **serviço conectar** permissões.
| Grupo de consumidores do Hub IoT | eventos de tooread de grupo de consumidores de saudação de saudação IoT Hub. É altamente recomendável toouse um grupo de consumidores exclusivo para a origem do evento.

### <a name="provide-iot-hub-settings-manually"></a>Fornecer configurações de Hub IoT manualmente

Olá tabela a seguir explica cada propriedade no guia de nova fonte de evento de saudação com sua descrição ao inserir as configurações manualmente:

| Nome da Propriedade | Descrição |
| --- | --- |
| Nome da origem do evento | nome de saudação de sua fonte de evento. Esse nome deve ser exclusivo no ambiente de Análise de Séries Temporais.
| Fonte | Escolha **IoT Hub** toocreate uma fonte de evento de IoT Hub.
| ID da assinatura | assinatura de saudação no qual este hub IoT foi criado.
| Grupo de recursos | assinatura de saudação no qual este hub IoT foi criado.
| Nome do Hub IoT | nome de saudação do seu IoT Hub. Quando você criou o Hub IoT, também deu a ele um nome específico
| Nome da política do Hub IoT | política de acesso Olá compartilhado, que pode ser criada em Olá guia de configurações do IoT Hub. Cada política de acesso compartilhado tem um nome, as permissões definidas por você e as chaves de acesso. Olá compartilhado política de acesso para a origem do evento *deve* ter **serviço conectar** permissões.
| Chave de política do Hub IoT | chave de acesso compartilhado Olá usado namespace de barramento de serviço de toohello tooauthenticate acesso. Digite hello chave primária ou secundária aqui.
| Grupo de consumidores do Hub IoT | eventos de tooread de grupo de consumidores de saudação de saudação IoT Hub. É altamente recomendável toouse um grupo de consumidores exclusivo para a origem do evento.

## <a name="next-steps"></a>Próximas etapas

1. Adicionar um ambiente de tooyour de política de acesso de dados [dados definir políticas de acesso](time-series-insights-data-access.md)
1. Acessar seu ambiente no hello [Portal de Insights de série de tempo](https://insights.timeseries.azure.com)
