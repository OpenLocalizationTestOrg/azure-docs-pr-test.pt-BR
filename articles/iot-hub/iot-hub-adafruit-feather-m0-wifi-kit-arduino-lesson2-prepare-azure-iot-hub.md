---
title: "Conecte-se Arduino tooAzure IoT - lição 2: registro de dispositivo | Microsoft Docs"
description: "Criar um grupo de recursos, criar um hub IoT do Azure e registrar Adafruit difusão M0 WiFi no hub do Azure IoT hello usando Olá CLI do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Conectando arduino toocloud, hub iot do azure, internet da nuvem de coisas, hub iot do azure criar dispositivo, nuvem arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>Crie seu Hub IoT e registre sua placa do Adafruit Feather M0 WiFi Arduino

## <a name="what-you-will-do"></a>O que você fará
* Crie um grupos de recursos.
* Crie o hub IoT do Azure no grupo de recursos de saudação.
* Adicione seu hub de Azure IoT Arduino placa toohello usando hello Azure interface de linha de comando (CLI do Azure).

Quando você usa Olá CLI do Azure tooadd seu hub de IoT tooyour Arduino board, serviço hello gera uma chave para sua tooauthenticate de quadro Arduino com o serviço de saudação. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshoot].

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como toouse Olá toocreate CLI do Azure com um hub IoT.
* Como toocreate uma identidade de dispositivo para seu Arduino placa em seu hub IoT.

## <a name="what-you-need"></a>O que você precisa
* Uma conta do Azure
* Um computador com hello CLI do Azure instalado

## <a name="create-your-iot-hub"></a>Criar seu Hub IoT
O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT. toocreate seu hub IoT, siga estas etapas:

1. Entre no tooyour conta do Azure executando Olá comando a seguir:

   ```bash
   az login
   ```

   Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.

2. Defina saudação padrão assinatura que você deseja toouse executando Olá comando a seguir:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`podem ser encontrados na saída Olá Olá `az login` ou hello `az account list` comando.

3. Registre o provedor de saudação executando o comando a seguir de saudação. Provedores de recursos são serviços que fornecem recursos para seu aplicativo. Você deve registrar o provedor de saudação antes de implantar Olá recursos do Azure que Olá ofertas do provedor.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Crie um grupo de recursos denominado exemplo iot na região Oeste dos EUA de saudação executando Olá comando a seguir:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`é o local de saudação criar seu grupo de recursos. Se você quiser toouse em outro local, você pode executar `az account list-locations -o table` toosee todos Olá locais Azure suporta.

5. Crie um hub IoT no grupo de recursos de exemplo iot Olá executando Olá comando a seguir:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

Por padrão, a ferramenta Olá cria um IoT Hub no tipo de preço grátis hello. Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nome de saudação do seu hub IoT deve ser globalmente exclusivo.
> Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>Registrar sua placa Arduino no Hub IoT
Cada dispositivo que envia o hub de IoT tooyour mensagens e recebe mensagens de seu hub IoT deve ser registrado com uma ID exclusiva.

Registre sua placa Arduino no Hub IoT executando o seguinte comando:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Resumo
Você criou um Hub IoT e registrou sua placa Arduino com uma identidade de dispositivo em seu Hub IoT. Você está pronto toolearn como toosend mensagens de seu hub de IoT tooyour Arduino quadro.

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo de função do Azure e um armazenamento do Azure conta tooprocess e o repositório de hub IoT mensagens][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md