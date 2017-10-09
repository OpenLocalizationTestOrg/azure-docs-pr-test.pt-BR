---
title: "Dispositivo SensorTag e Gateway de IoT do Azure - Introdução | Microsoft Docs"
description: "Introdução ao IoT Gateway Starter Kit, criar o hub IoT do Azure e conecte-se o hub IoT de toohello SensorTag e Gateway"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do Azure, iot gateway, guia de Introdução com hello internet das coisas, iot toolkit"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Introdução ao Kit de Início do Gateway IoT com um SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Dispositivo Simulado](iot-hub-gateway-kit-c-sim-get-started.md)

Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). Você trabalhará com NUC Intel que está executando o Linux vento rio e hello [SensorTag de TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). Você aprenderá como tooseamleesly se conectar a sua nuvem de toohello dispositivos usando o Azure IoT Hub.

***
**Ainda não tem um kit?:** Clique [aqui](https://aka.ms/gateway-kit). **Não é tem um SensorTag?:** [Comece com um dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) ou [compre um SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>Lição 1: Configurar sua NUC
![Diagrama de ponta a ponta da Lição 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

Nesta lição, você configura NUC Intel (unidade próximo de computação) em Olá Kit como um gateway IoT do Azure, instala pacote do Azure IoT borda Olá em NUC e executar uma exemplo tooverify Olá gateway a funcionalidade do aplicativo.

*Estimado tempo toocomplete: 15 minutos*

Vá muito[configurar NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lição 2: Criar seu Hub IoT
![Diagrama de ponta a ponta da Lição 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

Nesta lição, você instala ferramentas hello e software no computador host. Em seguida, criar sua conta gratuita do Azure, provisionar seu hub IoT do Azure e criar seu primeiro dispositivo no hub IoT de saudação.

Conclua a Lição 1 antes de iniciar esta lição.

### <a name="get-hello-tools"></a>Obter ferramentas Olá
Instale o software e ferramentas de saudação no computador host.

*Estimado tempo toocomplete: 20 minutos*

Vá muito[obter ferramentas Olá](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Criar um Hub IoT e registrar seu dispositivo
Criar seu grupo de recursos, provisionar o hub IoT do Azure primeiro e adicionar o primeiro dispositivo toohello IoT hub usando Olá CLI do Azure.

*Estimado tempo toocomplete: 10 minutos*

Vá muito[criar um hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Lição 3: Receber mensagens de SensorTag e ler mensagens do seu Hub IoT
Nesta lição, você usará configuração de saudação tooautomate scripts e execução de um aplicativo de exemplo Bilitar no seu gateway. Esses aplicativos usam um conjunto de módulos tooaggregate e transformar dados, processam comandos ou executam diversas tarefas relacionadas. Os módulos comunicam-se uns com os outros por meio de um agente de mensagem. aplicativo de exemplo Hello tem um módulo Bilitar e um módulo de hub IoT. módulo de Bilitar Olá recebe dados de Bilitar SensorTag. Olá pacotes de módulo de hub IoT dados saudação recebidos e o envia tooyour IoT hub por meio da estrutura de gateway Olá fornecida no Azure IoT Edge.

![Diagrama de ponta a ponta da Lição 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>Configurar e executar o aplicativo de exemplo hello Bilitar
Configure a conectividade de saudação entre SensorTag e seu gateway. Em seguida, conclua a configuração de saudação e executar o aplicativo de exemplo hello Bilitar.

*Estimado tempo toocomplete: 15 minutos*

Vá muito[configurar e executar hello Bilitar aplicativo de exemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Ler mensagens de seu Hub IoT
Execute código de exemplo no host do seu computador tooread mensagens de seu hub IoT.

*Estimado tempo toocomplete: 15 minutos*

Vá muito[ler mensagens de seu hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lição 4: Salvar mensagens tooAzure o armazenamento de tabela
Crie um aplicativo de função do Azure que obtém as mensagens de entrada de seu hub IoT e grava o armazenamento de tabela tooAzure.

![Diagrama de ponta a ponta da Lição 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure
Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.

*Estimado tempo toocomplete: 10 minutos*

Vá muito[criar uma conta de armazenamento do Azure e o aplicativo de função do Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Ler mensagens mantidas no Armazenamento de Tabelas do Azure
Monitorar mensagens de saudação do gateway para a nuvem, como eles são gravados tooAzure o armazenamento de tabela.

*Estimado tempo toocomplete: 5 minutos*

Vá muito[ler mensagens mantido no armazenamento de tabela do Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Solucionar problemas
Se você tiver problemas durante lições hello, procurar soluções Olá [solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) artigo.

## <a name="explore-more"></a>Explorar mais
Visite Olá [zona de desenvolvedor Intel IoT Gateway Kit](http://software.intel.com/iot/microsoft-azure) toolearn mais.
