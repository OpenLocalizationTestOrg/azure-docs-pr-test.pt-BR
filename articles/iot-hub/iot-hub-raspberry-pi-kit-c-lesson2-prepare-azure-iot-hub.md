---
title: "Conectar Raspberry Pi (C) ao IoT do Azure - Lição 2: registrar dispositivo | Microsoft Docs"
description: Crie um grupo de recursos, crie um Hub IoT do Azure e registre o Pi nele usando a CLI do Azure.
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
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Criar seu Hub IoT e registrar o Raspberry Pi 3
## <a name="what-you-will-do"></a>O que você fará
* Crie um grupos de recursos.
* Criar seu hub IoT do Azure no grupo de recursos.
* Adicione o Raspberry Pi 3 para o Hub IoT do Azure usando a interface de linha de comando do Azure (CLI do Azure).

Quando você usa a CLI do Azure para adicionar o Pi ao Hub IoT, o serviço gera uma chave para autenticar o Pi com o serviço. Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como usar a CLI do Azure para criar um Hub IoT.
* Como criar uma identidade de dispositivo para seu Pi no Hub IoT.

## <a name="what-you-need"></a>O que você precisa
* Uma conta do Azure
* Um computador Mac ou Windows com a CLI do Azure instalada

## <a name="create-your-iot-hub"></a>Criar seu Hub IoT
O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT. Para criar seu Hub IoT, execute estas etapas:

1. Faça logon em sua conta do Azure executando o comando a seguir:

   ```bash
   az login
   ```

   Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.

2. Defina a assinatura padrão que deseja usar executando o seguinte comando:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name` podem ser encontrados na saída do `az login` ou do comando `az account list`.

3. Registre o provedor executando o comando a seguir. Provedores de recursos são serviços que fornecem recursos para seu aplicativo. Você deve registrar o provedor antes de implantar o recurso do Azure que o provedor oferece.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Crie um grupo de recursos denominado iot-sample na região Oeste dos EUA executando o seguinte comando:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus` é o local no qual você cria seu grupo de recursos. Se você quiser usar outro local, execute `az account list-locations -o table` para ver todos os locais com suporte do Azure.
 
5. Crie um hub IoT no grupo de recursos iot-sample executando o seguinte comando:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   Por padrão, a ferramenta cria um Hub IoT no tipo de preços gratuito. Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> O nome do hub IoT deve ser globalmente exclusivo. Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.

## <a name="register-pi-in-your-iot-hub"></a>Registrar o Pi em seu Hub IoT
Cada dispositivo que envia mensagens para/de seu Hub IoT deve ser registrado com uma ID exclusiva.

Registre seu Pi no hub executando o seguinte comando:

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a>Resumo
Você criou um Hub IoT do Azure e registrou seu Pi com uma identidade de dispositivo em seu Hub IoT. Você está pronto para saber como enviar mensagens do Pi para o Hub IoT.

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure para processar e armazenar mensagens do Hub IoT](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

