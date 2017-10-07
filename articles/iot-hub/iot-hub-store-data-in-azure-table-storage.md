---
title: aaaSave tooAzure armazenamento de dados de mensagens de seu hub IoT | Microsoft Docs
description: "Use um toosave do aplicativo de função do Azure seu tooyour de mensagens do hub IoT armazenamento de tabela do Azure. mensagens de saudação do hub IoT contêm informações, como dados de sensor, que são enviadas do seu dispositivo IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: armazenamento de dados iot, armazenamento de dados de sensor iot
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Salvar mensagens de hub IoT que contêm o armazenamento de tabela do Azure do sensor dados tooyour

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>O que você aprenderá

Você aprenderá como toocreate uma conta de armazenamento do Azure e um Azure funcionam mensagens do aplicativo toostore IoT hub em seu armazenamento de tabela.

## <a name="what-you-do"></a>O que fazer

- Crie uma conta de armazenamento do Azure.
- Prepare seu hub IoT mensagens de tooread de conexão.
- Criar e implantar um aplicativo de funções do Azure.

## <a name="what-you-need"></a>O que você precisa

- [Configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) toocover Olá requisitos a seguir:
  - Uma assinatura ativa do Azure
  - Um hub IoT em sua assinatura 
  - Um aplicativo em execução que envia o hub de IoT tooyour mensagens

## <a name="create-an-azure-storage-account"></a>Criar uma conta de armazenamento do Azure

1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **armazenamento** > **conta de armazenamento**  >   **Criar**.

2. Insira as informações necessárias para a conta de armazenamento Olá Olá:

   ![Criar uma conta de armazenamento no hello portal do Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Nome**: nome Olá Olá da conta de armazenamento. Olá nome deve ser exclusivo.

   * **Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.

   * **PIN toodashboard**: Selecione esta opção para o hub de IoT tooyour fácil acesso do painel de saudação.

3. Clique em **Criar**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Preparar o hub IoT mensagens de tooread de conexão

Hub IoT expõe um evento interno ponto de extremidade compatível com o hub tooenable aplicativos tooread IoT hub as mensagens. Enquanto isso, os aplicativos usam dados do seu hub IoT tooread de grupos de consumidor. Antes de criar um função do Azure aplicativo tooread de dados do seu hub IoT, Olá a seguir:

- Obter cadeia de caracteres de conexão de saudação do seu ponto de extremidade de hub IoT.
- Criar um grupo de consumidores para o Hub IoT.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>Obter cadeia de caracteres de conexão de saudação do seu ponto de extremidade de hub IoT

1. Abrir seu Hub IoT.

2. Em Olá **IoT Hub** painel, em **mensagens**, clique em **pontos de extremidade**.

3. Em Olá direita painel, em **pontos de extremidade internos**, clique em **eventos**.

4. Em Olá **propriedades** painel, Olá Observação valores a seguir:
   - Ponto de extremidade compatível com o hub de eventos
   - Nome compatível com o hub de eventos

   ![Obter cadeia de caracteres de conexão de saudação de seu ponto de extremidade de hub IoT em Olá portal do Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. Em Olá **IoT Hub** painel, em **configurações**, clique em **políticas de acesso compartilhado**.

6. Clique em **iothubowner**.

7. Saudação de Observação **chave primária** valor.

8. Crie cadeia de caracteres de conexão de saudação de seu ponto de extremidade de hub IoT da seguinte maneira:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Substituir `<Event Hub-compatible endpoint>` e `<Primary key>` com valores hello que você anotou anteriormente.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Criar um grupo de consumidores para o Hub IoT

1. Abrir seu Hub IoT.

2. Em Olá **IoT Hub** painel, em **mensagens**, clique em **pontos de extremidade**.

3. Em Olá direita painel, em **pontos de extremidade internos**, clique em **eventos**.

4. Em Olá **propriedades** painel, em **grupos de consumidores**, insira um nome e, em seguida, anote-lo.

5. Clique em **Salvar**.

## <a name="create-and-deploy-an-azure-function-app"></a>Criar e implantar um aplicativo de funções do Azure

1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **de computação** > **aplicativo função**  >   **Criar**.

2. Insira as informações necessárias para o aplicativo de função Olá Olá.

   ![Criar um aplicativo de função em Olá portal do Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Nome do aplicativo**: nome de saudação do aplicativo de função hello. Olá nome deve ser exclusivo.

   * **Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.

   * **Conta de armazenamento**: Olá conta de armazenamento que você criou.

   * **PIN toodashboard**: marque esta opção para fácil acesso toohello função aplicativo de painel de saudação.

3. Clique em **Criar**.

4. Após a função hello aplicativo foi criado, abra-o.

5. No aplicativo de função hello, crie uma nova função hello seguinte:

   a. Clique em **Nova Função**.

   b. Selecione **JavaScript** para **Linguagem** e **Processamento de Dados** para **Cenário**.

   c. Clique em **Criar essa função** e depois clique em **Nova Função**.

   d. Selecione **JavaScript** idioma Olá, e **processamento de dados** para o cenário de saudação.

   e. Clique em Olá **EventHubTrigger JavaScript** modelo.

   f. Insira as informações necessárias para o modelo de Olá Olá.

      * **Nome de sua função**: nome de saudação do função hello.

      * **Nome do Hub de evento**: nome de compatível com o hub de evento Olá que você anotou anteriormente.

      * **Conexão de Hub de evento**: cadeia de caracteres de conexão Olá de tooadd de ponto de extremidade do hello IoT hub que você criou, clique em **novo**.

   g. Clique em **Criar**.

6. Configure uma saída de função Olá Olá seguinte:

   a. Clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabela do Azure** > **Selecionar**.

      ![Adicionar o aplicativo de função de tooyour de armazenamento de tabela no Olá portal do Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Insira as informações necessárias Olá.

      * **Nome do parâmetro de tabela**: Use `outputTable`, que será usado na hello Azure código da função.
      
      * **Nome da tabela**: use `deviceData`.

      * **Conexão da conta de armazenamento**: clique em **Novo** e selecione ou insira sua conta de armazenamento. Se a conta de armazenamento de saudação não for exibida, consulte [requisitos de conta de armazenamento](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Clique em **Salvar**.

7. Em **Gatilhos**, clique em **Hub de Eventos do Azure (eventHubMessages)**.

8. Em **grupo de consumidores do Hub de eventos**, insira o nome de saudação do grupo de consumidores Olá que você criou e, em seguida, clique em **salvar**.

9. Clique em função hello tenha sido criado nos saudação à esquerda e, em seguida, clique em **exibir arquivos** em saudação à direita.

10. Substitua Olá código em `index.js` com os seguintes hello:

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. Clique em **Salvar**.

Agora você criou o aplicativo de função hello. Ele armazena as mensagens que seu hub IoT recebe em seu armazenamento de tabelas.

> [!NOTE]
> Você pode usar o hello **executar** botão tootest Olá função app. Quando você clica em **executar**, mensagem de saudação do teste é enviada tooyour IoT hub. chegada de saudação de mensagem de saudação deve disparar Olá função aplicativo toostart e, em seguida, salve o armazenamento de tabela de tooyour de mensagem de saudação. Olá **Logs** painel registra os detalhes de saudação do processo de saudação.

## <a name="verify-your-message-in-your-table-storage"></a>Verificar a mensagem no armazenamento de tabelas

1. Execute o aplicativo de exemplo hello em seu hub IoT do dispositivo toosend mensagens tooyour.

2. [Baixe e instale o Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).

3. Abra o Gerenciador de armazenamento, clique em **adicionar uma conta do Azure** > **entrar**e entre tooyour conta do Azure.

4. Clique em sua assinatura do Azure > **Contas de Armazenamento** > sua conta de armazenamento > **Tabelas** > **deviceData**.

   Você deve ver as mensagens enviadas do seu hub IoT de tooyour de dispositivo conectado Olá `deviceData` tabela.

## <a name="next-steps"></a>Próximas etapas

Você criou com êxito sua conta de armazenamento do Azure e o aplicativo de funções do Azure para armazenar mensagens que seu hub IoT recebe em seu armazenamento de tabelas.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
