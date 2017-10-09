---
title: "tempo de aaaReal visualização de dados de sensor do seu hub IoT do Azure – aplicativos Web | Microsoft Docs"
description: "Use o recurso de aplicativos Web de saudação do serviço de aplicativo do Microsoft Azure toovisualize temperatura e umidade dados coletados de sensor hello e enviados tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualização de dados em tempo real, visualização de dados dinâmicos, visualização de dados de sensor"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Visualizar os dados de sensor em tempo real de seu hub IoT do Azure usando o recurso de aplicativos Web de saudação do serviço de aplicativo do Azure

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>O que você aprenderá

Neste tutorial, você aprenderá como dados de sensor em tempo real toovisualize que recebe o hub IoT executando um aplicativo web que são hospedados em um aplicativo web. Se quiser tootry toovisualize Olá dados em seu hub IoT usando o Power BI, consulte [dados de sensor em tempo real de toovisualize usar o Power BI do Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>O que fazer

- Crie um aplicativo web no hello portal do Azure.
- Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.
- Configure dados do sensor Olá web aplicativo tooread do seu hub IoT.
- Carregar um toobe de aplicativo web hospedado pelo aplicativo web de saudação.
- Abra Olá web toosee em tempo real temperatura e umidade dados de aplicativo do seu hub IoT.

## <a name="what-you-need"></a>O que você precisa

- [Configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), que abrange Olá requisitos a seguir:
  - Uma assinatura ativa do Azure
  - Um Hub IoT em sua assinatura
  - Um aplicativo cliente que envia o hub de Iot tooyour mensagens
- [Baixar Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Criar um aplicativo Web

1. Em Olá [portal do Azure](https://ms.portal.azure.com/), clique em **novo** > **Web + móvel** > **aplicativo Web**.
2. Insira um nome exclusivo do trabalho, verifique se a assinatura de saudação, especifique um grupo de recursos e um local, selecione **Pin toodashboard**e, em seguida, clique em **criar**.

   Recomendamos que você selecione Olá mesmo local que o grupo de recursos. Isso ajuda a velocidade de processamento e reduz o custo de saudação de transferência de dados.

   ![Criar um aplicativo Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Configurar Olá web aplicativo tooread dados do seu hub IoT

1. Abra o aplicativo de web de saudação que tiver acabado de provisionar.
2. Clique em **configurações do aplicativo**e, em seguida, em **configurações do aplicativo**, adicionar Olá pares chave/valor a seguir:

   | Chave                                   | Valor                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Obtido de iothub-explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | nome de saudação do grupo de consumidores Olá que você adicione tooyour IoT hub  |

   ![Adicionar configurações tooyour web app com pares chave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Clique em **configurações do aplicativo**, em **configurações gerais**, Olá alternância **Web sockets** opção e, em seguida, clique em **salvar**.

   ![Saudação de ativar/desativar opção de soquetes da Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Carregar um toobe de aplicativo web hospedado pelo aplicativo web de saudação

No GitHub, foi disponibilizado um aplicativo Web que exibe dados de sensor em tempo real obtidos do seu Hub IoT. Você só precisa toodo é configurar Olá web aplicativo toowork com um repositório Git, baixar o aplicativo da web de saudação do GitHub e, em seguida, carregá-lo tooAzure para toohost de aplicativo web hello.

1. No aplicativo da web de saudação, clique em **opções de implantação** > **Escolher fonte** > **repositório Git Local**e, em seguida, clique em **Okey**.

   ![Configurar o repositório do Git web app implantação toouse Olá local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Clique em **credenciais de implantação**, crie um usuário nome e senha toouse tooconnect toohello repositório Git no Azure e, em seguida, clique em **salvar**.

3. Clique em **visão geral**e observe o valor de saudação do **url de clone de Git**.

   ![Obter URL de clone de Git de saudação do seu aplicativo web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Abra uma janela de terminal ou de comando no computador local.

5. Baixar o aplicativo da web de saudação do GitHub e carregá-lo tooAzure para toohost de aplicativo web hello. toodo caso, execute hello comandos a seguir:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<URL de clone de Git\> é Olá URL do repositório do Git Olá encontrado no hello **visão geral** página do aplicativo web de saudação.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Abrir Olá web toosee em tempo real temperatura e umidade dados de aplicativo do seu hub IoT

Em Olá **visão geral** página do seu aplicativo web, clique em Olá URL tooopen Olá web app.

![Obter URL de saudação do seu aplicativo web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Você deve ver dados de umidade e temperatura de saudação em tempo real do seu hub IoT.

![Página de aplicativo Web mostrando a umidade e a temperatura em tempo real](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Certifique-se de que o aplicativo de exemplo hello está em execução no seu dispositivo. Se não, você receberá um gráfico em branco, você poderá consultar toohello tutoriais em [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Próximas etapas
Você usou com êxito seus dados de sensor em tempo real de toovisualize de aplicativo da web do seu hub IoT.

Para um modo alternativo toovisualize de dados do Azure IoT Hub, consulte [dados de sensor em tempo real de toovisualize usar o Power BI de seu hub IoT](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
