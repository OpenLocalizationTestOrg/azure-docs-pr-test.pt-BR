---
title: "monitoramento remoto de aaaIoT e notificações com os aplicativos lógicos do Azure | Microsoft Docs"
description: "Uso do Azure lógica de aplicativos para o monitoramento de temperatura de IoT em seu hub IoT e automaticamente enviar caixa de correio de tooyour notificações de email para todas as anomalias detectado."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "monitoramento de iot, notificações de iot, monitoramento de temperatura de iot"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Monitoramento remoto IoT e notificações com o Aplicativo Lógico do Azure conectando o hub IoT e a caixa de correio

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Aplicativos lógicos do Azure fornece uma maneira tooautomate processos como uma série de etapas. Um aplicativo lógico pode se conectar com vários serviços e protocolos. Ele começa com um gatilho como “Quando uma conta é adicionada”, seguido por uma combinação de ações semelhantes a “enviar uma notificação por push”. Esse recurso torna os aplicativos lógicos uma solução de IoT perfeita para monitoramento de IoT, como alertas a anomalias, entre outros cenários de uso.

## <a name="what-you-learn"></a>O que você aprenderá

Você aprenderá como toocreate um aplicativo lógico que conecta o hub IoT e sua caixa de correio para monitoramento de temperatura e notificações. Quando a temperatura Olá estiver acima de 30 C, Olá marcas de aplicativo cliente `temperatureAlert = "true"` na mensagem de saudação envia tooyour IoT hub. mensagem de saudação gatilhos Olá lógica aplicativo toosend você uma notificação por email.

## <a name="what-you-do"></a>O que fazer

* Criar um namespace de barramento de serviço e adicione um tooit de fila.
* Adicione um ponto de extremidade e um hub de IoT roteamento regra tooyour.
* Crie, configure e teste um aplicativo lógico.

## <a name="what-you-need"></a>O que você precisa

* Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:
  * Uma assinatura ativa do Azure.
  * Um hub IoT do Azure em sua assinatura.
  * Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Criar um namespace de barramento de serviço e adicione um tooit de fila

### <a name="create-a-service-bus-namespace"></a>Criar um namespace de barramento de serviço

1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **integração corporativa** > **barramento de serviço**.
1. Fornece Olá informações a seguir:

   **Nome**: nome Olá Olá do barramento do serviço.

   **Tipo de preço**: clique em **Básico** > **Selecionar**. a camada básica Olá é suficiente para este tutorial.

   **Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.

   **Local**: Use Olá mesmo local que usa o hub IoT.
1. Clique em **Criar**.

   ![Criar um namespace de barramento de serviço no portal do Azure de saudação](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Adicionar uma fila do barramento de serviço

1. Abrir o namespace de barramento de serviço hello e, em seguida, clique em **+ fila**.
1. Insira um nome para a fila de saudação e, em seguida, clique em **criar**.
1. Abrir a fila do barramento de serviço hello e, em seguida, clique em **políticas de acesso compartilhado** > **+ adicionar**.
1. Insira um nome para a política de saudação, verifique **gerenciar**e, em seguida, clique em **criar**.

   ![Adicionar uma fila do barramento de serviço no portal do Azure de saudação](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Adicionar um ponto de extremidade e um hub de IoT roteamento regra tooyour

### <a name="add-an-endpoint"></a>Adicionar um ponto final

1. Abra o hub IoT, clique em Pontos de Extremidade > + Adicionar.
1. Digite hello informações a seguir:

   **Nome**: nome de saudação do ponto de extremidade de saudação.

   **Tipo de ponto de extremidade**: selecione **Fila do Barramento de Serviço**.

   **Namespace de barramento de serviço**: selecione Olá namespace criado por você.

   **Fila do barramento de serviço**: fila Olá selecione criada por você.
1. Clique em **OK**.

   ![Adicionar um hub do ponto de extremidade tooyour IoT em Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Adicionar uma regra de roteamento

1. No hub IoT, clique em **Rotas** > **+ Adicionar**.
1. Digite hello informações a seguir:

   **Nome**: nome de saudação da regra de roteamento de saudação.

   **Fonte de dados**: selecione **DeviceMessages**.

   **Ponto de extremidade**: Selecionar ponto de extremidade de saudação que você criou.

   **Cadeia de caracteres de consulta**: insira `temperatureAlert = "true"`.
1. Clique em **Salvar**.

   ![Adicionar uma regra de roteamento no hello portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Criar e configurar um aplicativo lógico

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico

1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **integração corporativa** > **aplicativo lógico**.
1. Digite hello informações a seguir:

   **Nome**: nome de saudação do aplicativo de lógica de saudação.

   **Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.

   **Local**: Use Olá mesmo local que usa o hub IoT.
1. Clique em **Criar**.

### <a name="configure-hello-logic-app"></a>Configurar o aplicativo de lógica de saudação

1. Abra o aplicativo de lógica de saudação que é aberta em Olá lógica do Designer de aplicativos.
1. No hello lógica do Designer de aplicativos, clique em **aplicativo lógica em branco**.

   ![Iniciar com um aplicativo em branco lógica em Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Clique em **Barramento de Serviço**.

   ![Selecione o barramento de serviço toostart criando seu aplicativo lógico no hello portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Clique em **Fila do Barramento de Serviço – quando uma ou mais mensagens chegam em uma fila (conclusão automática)**.
1. Crie uma conexão do barramento de serviço.
   1. Insira um nome de conexão.
   1. Clique em namespace de barramento de serviço hello > Olá política de barramento de serviço > **criar**.

      ![Criar uma conexão de barramento de serviço para seu aplicativo lógica no hello portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Clique em **continuar** após a conexão de barramento de serviço Olá é criado.
   1. Selecione a fila de saudação que você criou e insira `175` para **contagem máxima de mensagem**

      ![Especificar a contagem de máximo de mensagem de saudação para conexão de barramento de serviço Olá em seu aplicativo de lógica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Clique em "Salvar" botão toosave Olá alterações.

1. Crie uma conexão de serviço SMTP.
   1. Clique em **Nova etapa** > **Adicionar uma ação**.
   1. Tipo `SMTP`, clique em Olá **SMTP** no resultado da pesquisa de saudação do serviço e, em seguida, clique em **SMTP - Enviar Email**.

      ![Criar uma conexão SMTP no seu aplicativo lógica Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Insira informações de saudação SMTP da caixa de correio e, em seguida, clique em **criar**.

      ![Insira informações de conexão SMTP em seu aplicativo de lógica em Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Obter informações de saudação SMTP para [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), e [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).
   1. Insira seu endereço de email para **De** e **Para**, e `High temperature detected` para **Assunto** e **Corpo**.
   1. Clique em **Salvar**.

Olá lógica aplicativo está em funcionamento quando você salvá-lo.

## <a name="test-hello-logic-app"></a>Aplicativo de lógica de saudação do teste

1. Iniciar aplicativo cliente Olá que você implantar o dispositivo tooyour no [tooAzure ESP8266 conectar IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Aumentar a temperatura do ambiente Olá em torno de saudação SensorTag toobe acima c 30. Por exemplo, claro uma vela em torno de seu SensorTag.
1. Você deve receber uma notificação por email enviada pelo aplicativo de lógica de saudação.

   > [!NOTE]
   > O provedor de serviços de email pode ser necessário tooverify Olá remetente identidade toomake que é você quem envia email hello.

## <a name="next-steps"></a>Próximas etapas

Você criou com êxito um aplicativo lógico que conecta o hub IoT e sua caixa de correio para monitoramento e notificações de temperatura.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
