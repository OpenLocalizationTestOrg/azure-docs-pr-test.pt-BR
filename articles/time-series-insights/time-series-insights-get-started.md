---
title: "um ambiente do Azure Insights de série de tempo de aaaCreate | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toocreate ambiente da série de tempo, conecte-a origem do evento tooan e pronto tooanalyze seus dados de evento em minutos."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Criar um novo ambiente de informações da série de tempo no hello portal do Azure

O ambiente de Análise de Séries Temporais é um recurso do Azure com capacidade de entrada e o armazenamento. Os clientes provisionar ambientes via Olá portal do Azure com capacidade de saudação necessária.

## <a name="steps-toocreate-hello-environment"></a>Ambiente de saudação toocreate etapas

Siga estas etapas toocreate seu ambiente:

1.  Entrar toohello [portal do Azure](https://portal.azure.com).
2.  Clique em hello mais sinal ("+") no hello canto superior esquerdo.
3.  Procure "Insights de série de tempo" na caixa de pesquisa de saudação.

  ![Criar ambiente de informações da série de tempo de saudação](media/get-started/getstarted-create-environment1.png)

4.  Selecione "Análise de Séries Temporais", clique em "Criar".

  ![Criar grupo de recursos de informações da série de tempo de saudação](media/get-started/getstarted-create-environment2.png)

5.  Especifique o nome do ambiente. Este nome representa ambiente Olá [explorer da série de tempo](https://insights.timeseries.azure.com).
6.  Selecione uma assinatura. Escolha uma que contenha a sua fonte de eventos. Informações da série de tempo pode detectar automaticamente Azure IoT Hub e recursos do Hub de eventos existentes no Olá a mesma assinatura.
7.  Selecione ou crie um grupo de recursos. Um grupo de recursos é uma coleção de recursos do Azure que são usados juntos.
8.  Selecione um local de hospedagem. tooavoid mover dados entre data centers, escolha um local que contém a origem do evento.
9.  Selecione um tipo de preço.
10. Selecione a capacidade. Você pode alterar a capacidade de um ambiente após a criação.
11. Crie seu ambiente. Você também pode fixar o dashboard de toohello seu ambiente para facilitar o acesso sempre que você entrar.

  ![Criar hello toodashboard de pin de informações da série de tempo](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Próximas etapas

* [Definir políticas de acesso de dados](time-series-insights-data-access.md) tooaccess seu ambiente no [Portal de Insights de série de tempo](https://insights.timeseries.azure.com)
* [Criar uma fonte de eventos](time-series-insights-add-event-source.md)
* [Enviar eventos](time-series-insights-send-events.md) toohello origem do evento
