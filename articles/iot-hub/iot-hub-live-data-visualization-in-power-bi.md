---
title: "tempo de aaaReal visualização de dados de sensor do Azure IoT Hub – Power BI | Microsoft Docs"
description: Use o Power BI toovisualize temperatura e umidade dados coletados de sensor hello e enviados tooyour Azure IoT hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualização de dados em tempo real, visualização de dados dinâmicos, visualização de dados de sensor"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Visualizar dados de sensor em tempo real do Hub IoT usando o Power BI

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>O que você aprenderá

Você aprenderá como dados de sensor em tempo real de toovisualize que recebe o hub IoT do Azure pelo Power BI. Se você quiser tootry visualizar dados saudação em seu hub IoT com aplicativos da Web, consulte [dados do sensor em tempo real do toovisualize aplicativos de Web do Azure de uso do Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>O que fazer

- Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.
- Criar, configurar e executar um trabalho do Stream Analytics para transferência de dados de sua tooyour de hub IoT conta do Power BI.
- Criar e publicar um dado de saudação do Power BI relatório toovisualize.

## <a name="what-you-need"></a>O que você precisa

- Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:
  - Uma assinatura ativa do Azure.
  - Um hub IoT do Azure em sua assinatura.
  - Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.
- Uma conta do Power BI. ([Experimente gratuitamente o Power BI](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Criar, configurar e executar um trabalho do Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Criar um trabalho de Stream Analytics

1. No hello portal do Azure, clique em Novo > Internet das coisas > trabalho do Stream Analytics.
1. Digite hello informações de trabalho Olá a seguir.

   **Nome do trabalho**: nome de saudação do trabalho de saudação. Olá nome deve ser exclusivo.

   **Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.

   **Local**: Use Olá mesmo local que o grupo de recursos.

   **PIN toodashboard**: Selecione essa opção para o hub de IoT tooyour fácil acesso no painel de saudação.

   ![Criar um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Clique em **Criar**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Adicionar um trabalho de análise de fluxo de entrada toohello

1. Trabalho de análise de fluxo aberto hello.
1. Em **Topologia do Trabalho**, clique em **Entradas**.
1. Em Olá **entradas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:

   **Alias de entrada**: alias exclusivo Olá Olá entrada.

   **Origem**: selecione **hub IoT**.

   **Grupo de consumidores**: grupo de consumidores Olá selecione você acabou de criar.
1. Clique em **Criar**.

   ![Adicionar um trabalho de análise de fluxo de entrada tooa no Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Adicionar um trabalho de análise de fluxo de toohello de saída

1. Em **Topologia do Trabalho**, clique em **Saídas**.
1. Em Olá **saídas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:

   **Alias de saída**: alias exclusivo de saudação para saída de hello.

   **Coletor**: selecione **Power BI**.
1. Clique em **Autorizar** e depois entre na sua conta do Power BI.
1. Uma vez autorizado, digite Olá informações a seguir:

   **Espaço de trabalho de grupo**: selecione o espaço de trabalho do grupo de destino.

   **Nome do Conjunto de Dados**: insira um nome de conjunto de dados.

   **Nome da Tabela**: insira um nome de tabela.
1. Clique em **Criar**.

   ![Adicionar um trabalho de análise de fluxo de tooa de saída no Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurar consulta de saudação do trabalho do Stream Analytics Olá

1. Em **Topologia do Trabalho**, clique em **Consulta**.
1. Substituir `[YourInputAlias]` com alias Olá de entrada do trabalho de saudação.
1. Substituir `[YourOutputAlias]` com hello alias de saída do trabalho de saudação.
1. Clique em **Salvar**.

   ![Adicionar um trabalho de análise de fluxo de tooa de consulta no Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Executar trabalho do Stream Analytics Olá

No trabalho de análise de fluxo de saudação, clique em **iniciar** > **agora** > **iniciar**. Depois que o trabalho de saudação é iniciado com êxito, o status do trabalho Olá muda de **parado** muito**executando**.

![Executar um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Criar e publicar um dado de saudação do Power BI relatório toovisualize

1. Certifique-se de que o aplicativo de exemplo hello está em execução no seu dispositivo. Se não, você pode consultar toohello tutoriais em [configurar seu dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Entrar tooyour [Power BI](https://powerbi.microsoft.com/en-us/) conta.
1. Acesse o espaço de trabalho de grupo de toohello que você definiu quando criou saída Olá para o trabalho de análise de fluxo de saudação.
1. Clique em **Conjuntos de dados de streaming**.

   Você deve ver o dataset Olá listado que você especificou quando criou a saudação de saída para o trabalho de análise de fluxo de saudação.
1. Em **ações**, clique em toocreate de ícone Olá primeiro um relatório.

   ![Criar um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Crie uma temperatura em tempo real do tooshow de gráfico de linha ao longo do tempo.
   1. Na página de criação de relatório hello, adicione um gráfico de linhas.
   1. Em Olá **campos** painel, expanda a tabela Olá que você especificou quando criou a saída Olá para o trabalho de análise de fluxo de saudação.
   1. Arraste **EventEnqueuedUtcTime** muito**eixo** em Olá **visualizações** painel.
   1. Arraste **temperatura** muito**valores**.

      Agora, um gráfico de linhas é criado. eixo x da saudação exibe a data e hora no fuso horário UTC hello. eixo y da saudação mostra a temperatura do sensor de saudação.

      ![Adicionar um gráfico de linhas de temperatura tooa relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Crie outra linha gráfico tooshow em tempo real umidade ao longo do tempo. toodo isso, siga Olá mesmo as etapas acima e coloque **EventEnqueuedUtcTime** no eixo x do hello e **umidade** no eixo y da saudação.

   ![Adicionar um gráfico de linhas para umidade tooa relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Clique em **salvar** toosave relatório de saudação.
1. Clique em **arquivo** > **publicar tooweb**.
1. Clique em **Criar código incorporado** e clique em **Publicar**.

Você receberá o link do relatório Olá que você pode compartilhar com qualquer pessoa para acesso ao relatório e um relatório de saudação de toointegrate de trecho de código em seu blog ou site.

![Publicar um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

A Microsoft também oferece Olá [aplicativos móveis Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) para exibir e interagir com seus relatórios e dashboards do Power BI em seu dispositivo móvel.

## <a name="next-steps"></a>Próximas etapas

Você usou com êxito os dados do Power BI toovisualize sensor em tempo real do seu hub IoT do Azure.
Há um maneira alternativa toovisualize dados Azure IoT Hub. Consulte [dados do sensor em tempo real do toovisualize aplicativos de Web do Azure de uso do Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
