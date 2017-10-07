---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 2: registrar dispositivo | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Hub iot do Azure, nuvem de Internet das coisas, criar dispositivo de Hub IoT do Azure, SensorTag de TI, bli de TI
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Criar seu Hub IoT do Azure e registrar seu dispositivo

## <a name="what-you-will-do"></a>O que você fará

- Criar um grupos de recursos
- Criar seu primeiro Hub IoT
- Registre seu dispositivo em seu hub IoT usando Olá CLI do Azure. 

Quando você registra seu dispositivo em seu hub IoT, Olá serviço Azure IoT Hub gera uma chave para tooauthenticate de toouse seu dispositivo com o serviço de saudação. 

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Nesta lição, você aprenderá:

- Como toouse Olá toocreate CLI do Azure com um hub IoT.
- Como tooregister um dispositivo em um hub IoT.

## <a name="what-you-need"></a>O que você precisa

- Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, você pode [criar uma conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
- Você deve ter Olá que CLI do Azure instalado.

## <a name="create-an-iot-hub"></a>Crie um hub IoT

toocreate um hub IoT, siga estas etapas:

1. Entre no tooyour conta do Azure executando Olá comando a seguir:

   ```bash
   az login
   ```

   Todas as suas assinaturas disponíveis serão listadas após uma entrada bem-sucedida.

2. Defina o valor padrão de saudação assinatura do Azure que você deseja toouse executando Olá comando a seguir:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`podem ser encontrados na saída Olá Olá `az login` ou hello `az account list` comando.

3. Registre o provedor de saudação executando o comando a seguir de saudação. Provedores de recursos são serviços que fornecem recursos para seu aplicativo. Você deve registrar o provedor de saudação antes de implantar Olá recursos do Azure que Olá ofertas do provedor.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Criar um grupo de recursos denominado `iot-gateway` na região do Oeste dos EUA Olá executando Olá comando a seguir:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`é o local de saudação criar seu grupo de recursos. Se você quiser toouse em outro local, você pode executar `az account list-locations -o table` toosee todos Olá locais Azure suporta.

5. Criar um hub IoT em Olá `iot-gateway` grupo de recursos executando Olá comando a seguir:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Por padrão, a ferramenta Olá cria um IoT Hub no tipo de preço grátis hello. Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nome de saudação do seu hub IoT deve ser globalmente exclusivo. Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Registrar seu dispositivo em seu Hub IoT

Cada dispositivo que envia o hub de IoT tooyour mensagens e recebe mensagens de seu hub IoT deve ser registrado com uma ID exclusiva.
Registre seu dispositivo no Hub IoT do Azure executando o seguinte comando:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Resumo

Você criou um Hub IoT do Azure e registrou seu dispositivo lógico com uma identidade de dispositivo em seu Hub IoT. Você está pronto toolearn como tooconfigure e executar um gateway exemplo aplicativo toosend de dados do seu hub IoT tooyour de dispositivo físico Olá de nuvem.

## <a name="next-steps"></a>Próximas etapas
[Configurar e executar um aplicativo de exemplo de upload de nuvem de dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)