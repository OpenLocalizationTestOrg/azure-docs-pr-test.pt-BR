---
title: "aaaWeather previsão usando o aprendizado de máquina do Azure com dados de IoT Hub | Microsoft Docs"
description: "Use o aprendizado de máquina do Azure toopredict Olá chance de chuva com base em umidade e temperatura Olá seu hub IoT coleta de um sensor de dados."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Machine Learning de previsão do tempo"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Previsão do tempo usando dados de sensor de saudação do seu hub IoT no aprendizado de máquina do Azure

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Aprendizado de máquina é uma técnica de ciência de dados que ajuda os computadores a aprender com as tendências, resultados e existente comportamentos futuras tooforecast de dados. O aprendizado de máquina do Azure é um serviço em nuvem análise preditiva que torna possível tooquickly criar e implantar modelos de previsão como soluções de análise.

## <a name="what-you-learn"></a>O que você aprenderá

Você aprenderá como toouse aprendizado de máquina do Azure toodo previsão do tempo (chance de chuva) usando Olá temperatura e umidade dados de seu hub IoT do Azure. chance de saudação de chuva é saída de saudação de um modelo de previsão do tempo preparada. modelo de saudação se baseia a chance de tooforecast dados históricos de chuva com base em temperatura e umidade.

## <a name="what-you-do"></a>O que fazer

- Implante o modelo de previsão do tempo de saudação como um serviço web.
- Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.
- Criar um trabalho de análise de fluxo e configurar o trabalho Olá para:
  - Leia dados de temperatura e umidade no Hub IoT.
  - Chame a chance de chuva Olá web serviço tooget hello.
  - Salve o armazenamento de BLOBs do Azure tooan resultados da saudação.
- Use a previsão do tempo de saudação do Microsoft Azure Storage Explorer tooview.

## <a name="what-you-need"></a>O que você precisa

- Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:
  - Uma assinatura ativa do Azure.
  - Um hub IoT do Azure em sua assinatura.
  - Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.
- Uma conta do Azure Machine Learning Studio. ([Experimente o Machine Learning Studio gratuitamente](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Implantar o modelo de previsão do tempo de saudação como um serviço web

1. Vá toohello [página de modelo de previsão do tempo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Clique em **Abrir no Studio** no Microsoft Azure Machine Learning Studio.
   ![Página de modelo de previsão Olá abrir clima na Galeria de inteligência de Cortana](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Clique em **executar** toovalidate Olá etapas no modelo de saudação. Esta etapa pode levar toocomplete 2 minutos.
   ![Modelo de previsão de clima Olá abrir no estúdio de aprendizado de máquina do Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Clique em **CONFIGURAR SERVIÇO WEB** > **Serviço Web Preditivo**.
   ![Implantar o modelo de previsão de clima Olá no estúdio de aprendizado de máquina do Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. No diagrama de hello, arraste Olá **Web serviço entrada** módulo em algum lugar próximo Olá **modelo de pontuação** módulo.
1. Conectar Olá **Web serviço entrada** módulo toohello **modelo de pontuação** módulo.
   ![Conectar dois módulos no Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Clique em **executar** toovalidate Olá etapas no modelo de saudação.
1. Clique em **IMPLANTAR o serviço da WEB** modelo de saudação toodeploy como um serviço web.
1. No painel de saudação do modelo hello, baixe Olá **Excel 2010 ou pasta de trabalho anterior** para **solicitação/resposta**.

   > [!Note]
   > Certifique-se de que você baixe Olá **Excel 2010 ou pasta de trabalho anterior** mesmo se você estiver executando uma versão posterior do Excel em seu computador.

   ![Baixar hello Excel para o ponto de extremidade de resposta da solicitação de saudação](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Abra a pasta de trabalho do Excel hello, anote Olá **URL do serviço WEB** e **chave de acesso**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Criar, configurar e executar um trabalho do Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Criar um trabalho de Stream Analytics

1. Em Olá [portal do Azure](https://ms.portal.azure.com/), clique em **novo** > **Internet das coisas** > **trabalho do Stream Analytics**.
1. Digite hello informações de trabalho Olá a seguir.

   **Nome do trabalho**: nome de saudação do trabalho de saudação. Olá nome deve ser exclusivo.

   **Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.

   **Local**: Use Olá mesmo local que o grupo de recursos.

   **PIN toodashboard**: Selecione essa opção para o hub de IoT tooyour fácil acesso no painel de saudação.

   ![Criar um trabalho do Stream Analytics no Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Clique em **Criar**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Adicionar um trabalho de análise de fluxo de entrada toohello

1. Trabalho de análise de fluxo aberto hello.
1. Em **Topologia do Trabalho**, clique em **Entradas**.
1. Em Olá **entradas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:

   **Alias de entrada**: alias exclusivo Olá Olá entrada.

   **Origem**: selecione **hub IoT**.

   **Grupo de consumidores**: grupo de consumidores Olá selecione criado por você.

   ![Adicionar um trabalho de análise de fluxo de entrada toohello no Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Clique em **Criar**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Adicionar um trabalho de análise de fluxo de toohello de saída

1. Em **Topologia do Trabalho**, clique em **Saídas**.
1. Em Olá **saídas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:

   **Alias de saída**: alias exclusivo de saudação para saída de hello.

   **Coletor**: selecione **Armazenamento de Blobs**.

   **Conta de armazenamento**: Olá conta de armazenamento para o armazenamento de blob. Você pode criar uma conta de armazenamento ou usar uma existente.

   **Contêiner**: contêiner Olá onde blob Olá é salvo. Você pode criar um contêiner ou usar um existente.

   **Formato de serialização de evento**: selecione **CSV**.

   ![Adicionar um trabalho de análise de fluxo de toohello de saída no Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Clique em **Criar**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Adicionar uma função toohello serviço Stream Analytics trabalho toocall Olá web implantado

1. Em **Topologia de Trabalho**, clique em **Funções** > **Adicionar**.
1. Digite hello informações a seguir:

   **Alias da Função**: insira `machinelearning`.

   **Tipo de Função**: selecione **Azure ML**.

   **Opção de importação**: selecione **Importar de outra assinatura**.

   **URL**: insira Olá URL do serviço WEB que você anotou para baixo da pasta de trabalho do Excel hello.

   **Chave**: insira Olá chave de acesso que você anotou para baixo da pasta de trabalho do Excel hello.

   ![Adicionar um trabalho de análise de fluxo de toohello de função no Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Clique em **Criar**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurar consulta de saudação do trabalho do Stream Analytics Olá

1. Em **Topologia do Trabalho**, clique em **Consulta**.
1. Substitua código existente Olá Olá código a seguir:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Substituir `[YourInputAlias]` com alias Olá de entrada do trabalho de saudação.

   Substituir `[YourOutputAlias]` com hello alias de saída do trabalho de saudação.

1. Clique em **Salvar**.

### <a name="run-hello-stream-analytics-job"></a>Executar trabalho do Stream Analytics Olá

No trabalho de análise de fluxo de saudação, clique em **iniciar** > **agora** > **iniciar**. Depois que o trabalho de saudação é iniciado com êxito, o status do trabalho Olá muda de **parado** muito**executando**.

![Executar trabalho do Stream Analytics Olá](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Usar a previsão do tempo de saudação do Microsoft Azure Storage Explorer tooview

Execute Olá cliente aplicativo toostart coletar e enviar temperatura e umidade hub de IoT tooyour de dados. Para cada mensagem que recebe o hub IoT, o trabalho do Stream Analytics Olá chama Olá previsão do tempo da web serviço tooproduce Olá chance de chuva. resultado de saudação é salvo, em seguida, tooyour armazenamento de BLOBs do Azure. Azure Storage Explorer é uma ferramenta que você pode usar o resultado de saudação tooview.

1. [Baixe e instale o Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).
1. Abra o Gerenciador de Armazenamento do Azure.
1. Entre tooyour conta do Azure.
1. Selecione sua assinatura.
1. Clique em sua assinatura > **Contas de Armazenamento** > sua conta de armazenamento > **Contêineres de Blobs** > seu contêiner.
1. Abra um resultado de saudação do toosee de arquivo. csv. os registros de última coluna Olá Olá chance de chuva.

   ![Obter resultados da previsão do tempo com o Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Resumo

Você usou com êxito a chance de saudação do aprendizado de máquina do Azure tooproduce de chuva com base nos dados de temperatura e umidade Olá que recebe o hub IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]