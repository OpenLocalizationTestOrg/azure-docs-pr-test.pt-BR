---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 2: registrar dispositivo| Microsoft Docs"
description: Crie um grupo de recursos, crie um Hub IoT do Azure e registre o Edison no Hub IoT do Azure usando a CLI do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>Criar seu Hub IoT e registrar o Intel Edison
## <a name="what-you-will-do"></a>O que você fará
* Crie um grupos de recursos.
* Criar seu hub IoT do Azure no grupo de recursos.
* Adicionar o Intel Edison ao Hub IoT do Azure usando a interface de linha de comando do Azure (CLI do Azure).

Quando você usa a CLI do Azure para adicionar o Edison ao Hub IoT, o serviço gera uma chave para a autenticação do Edison com o serviço. Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como usar a CLI do Azure para criar um Hub IoT.
* Como criar uma identidade de dispositivo para o Edison em seu Hub IoT.

## <a name="what-you-need"></a>O que você precisa
* Uma conta do Azure. Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
* Você deve ter a CLI do Azure instalada.

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
> O nome do hub IoT deve ser globalmente exclusivo.
> Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.


## <a name="register-edison-in-your-iot-hub"></a>Registrar o Edison em seu Hub IoT
Cada dispositivo que envia mensagens para/de seu Hub IoT deve ser registrado com uma ID exclusiva.

Registre o Edison em seu Hub IoT executando o seguinte comando:

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Resumo
Você criou um Hub IoT e registrou o Edison com uma identidade de dispositivo em seu Hub IoT. Você está pronto para saber como enviar mensagens do Edison para seu Hub IoT.

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure para processar e armazenar mensagens do Hub IoT][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md