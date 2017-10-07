---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 2: registro de dispositivo | Microsoft Docs"
description: "Criar um grupo de recursos, criar um hub IoT do Azure e registrar Pi no hub do Azure IoT hello usando Olá CLI do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: nuvem raspberry pi, pi cloud connect
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Criar seu Hub IoT e registrar o Raspberry Pi 3
## <a name="what-you-will-do"></a>O que você fará
* Crie um grupos de recursos.
* Crie o hub IoT do Azure no grupo de recursos de saudação.
* Adicione framboesa Pi 3 toohello Azure IoT hub usando hello Azure interface de linha de comando (CLI do Azure).

Quando você usa o hub IoT tooyour de Pi do hello CLI do Azure tooadd, o serviço hello gera uma chave para tooauthenticate Pi com o serviço de saudação. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como toouse Olá toocreate CLI do Azure com um hub IoT.
* Como toocreate uma identidade de dispositivo para Pi em seu hub IoT.

## <a name="what-you-need"></a>O que você precisa
* Uma conta do Azure
* Um Mac ou um computador com Windows com hello CLI do Azure instalado

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
> nome de saudação do seu hub IoT deve ser globalmente exclusivo. Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.

## <a name="register-pi-in-your-iot-hub"></a>Registrar o Pi em seu Hub IoT
Cada dispositivo que envia o hub de IoT tooyour mensagens e recebe mensagens de seu hub IoT deve ser registrado com uma ID exclusiva.

Registre seu Pi no hub executando o seguinte comando:

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a>Resumo
Você criou um Hub IoT do Azure e registrou seu Pi com uma identidade de dispositivo em seu Hub IoT. Você está pronto toolearn como toosend mensagens do hub de IoT tooyour Pi.

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo de função do Azure e um armazenamento do Azure conta tooprocess e o repositório de hub IoT mensagens](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

