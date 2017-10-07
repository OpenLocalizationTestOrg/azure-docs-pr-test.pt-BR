---
title: "Dispositivo simulado e Gateway do IoT do Azure - Introdução | Microsoft Docs"
description: "Introdução ao IoT Gateway Starter Kit, criar o hub IoT do Azure e conecte Gateway toohello IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do Azure, iot gateway, guia de Introdução com hello internet das coisas, iot toolkit"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Introdução ao Kit de Início do Gateway IoT com um dispositivo simulado

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Dispositivo Simulado](iot-hub-gateway-kit-c-sim-get-started.md)

Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). Você estará trabalhando com a NUC da Intel executando o Linux Wind River. Você aprenderá como tooseamleesly se conectar a sua nuvem de toohello dispositivos usando o Azure IoT Hub.

***
**Ainda não tem um kit?:** Clique [aqui](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Lição 1: Configurar sua NUC
![Diagrama de ponta a ponta da Lição 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

Nesta lição, você configura NUC Intel (unidade próximo de computação) em Olá Kit como um gateway IoT do Azure, instala pacote do Azure IoT borda Olá em NUC e executar uma exemplo tooverify Olá gateway a funcionalidade do aplicativo.

*Estimado tempo toocomplete: 15 minutos*

Vá muito[configurar NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lição 2: Criar seu Hub IoT
![Diagrama de ponta a ponta da Lição 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

Nesta lição, você instala ferramentas hello e software no computador host. Em seguida, criar sua conta gratuita do Azure, provisionar seu hub IoT do Azure e criar seu primeiro dispositivo no hub IoT de saudação.

Conclua a Lição 1 antes de iniciar esta lição.

### <a name="get-hello-tools"></a>Obter ferramentas Olá
Instale o software e ferramentas de saudação no computador host.

*Estimado tempo toocomplete: 20 minutos*

Vá muito[obter ferramentas Olá](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Criar um Hub IoT e registrar seu dispositivo
Criar seu grupo de recursos, provisionar o hub IoT do Azure primeiro e adicionar o primeiro dispositivo toohello IoT hub usando Olá CLI do Azure.

*Estimado tempo toocomplete: 10 minutos*

Vá muito[criar um hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Lição 3: Receber mensagens de dispositivo simulado hello e ler mensagens de seu hub IoT
Nesta lição, você usará configuração de saudação tooautomate scripts e execução de um aplicativo de dispositivo simulado em seu gateway. aplicativo de dispositivo simulado Hello gera dados de temperatura de exemplo e o envia tooan módulos de hubs de IoT. Olá pacotes de módulo de hub IoT dados saudação recebidos e o envia tooyour IoT hub por meio da estrutura de gateway Olá fornecida no Azure IoT Edge.

![Diagrama de ponta a ponta da Lição 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Configurar e executar um dispositivo simulado
Prepare os códigos de exemplo hello. Em seguida, configurar e executar o aplicativo de exemplo hello simulado dispositivo.

*Estimado tempo toocomplete: 15 minutos*

Vá muito[configurar e executar um dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Ler mensagens de seu Hub IoT
Execute um código de exemplo em suas mensagens de saudação do tooread de computador host do seu hub IoT.

*Estimado tempo toocomplete: 15 minutos*

Vá muito[ler mensagens de seu hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lição 4: Salvar mensagens tooAzure o armazenamento de tabela
Crie um aplicativo de função do Azure que obtém as mensagens de entrada de seu hub IoT e grava o armazenamento de tabela tooAzure.

![Diagrama de ponta a ponta da Lição 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure
Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.

*Estimado tempo toocomplete: 10 minutos*

Vá muito[criar uma conta de armazenamento do Azure e o aplicativo de função do Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Ler mensagens mantidas no Armazenamento de Tabelas do Azure
Monitorar mensagens de saudação do gateway para a nuvem, como eles são gravados tooAzure o armazenamento de tabela.

*Estimado tempo toocomplete: 5 minutos*

Vá muito[ler mensagens mantido no armazenamento de tabela do Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Solucionar problemas
Se você tiver problemas durante lições hello, procurar soluções Olá [solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) artigo.

## <a name="explore-more"></a>Explorar mais
Visite Olá [zona de desenvolvedor Intel IoT Gateway Kit](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn mais.
