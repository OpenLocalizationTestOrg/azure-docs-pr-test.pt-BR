---
title: aaaGet iniciado com borda de IoT do Azure (Windows) | Microsoft Docs
description: "Como toobuild um gateway de extremidade de IoT do Azure em um Windows do computador e saiba mais sobre conceitos principais no Azure IoT Edge como módulos e arquivos de configuração JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Explorar a arquitetura do Azure IoT Edge no Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Como toorun Olá exemplo

Olá **build.cmd** script gera a saída no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório. Essa saída inclui módulos de borda IoT dois Olá usados neste exemplo.

Olá locais de script de compilação **logger.dll** em Olá **criar\\módulos\\agente\\depurar** pasta e **Olá\_world.dll**  em Olá **criar\\módulos\\hello_world\\depurar** pasta. Usar estes caminhos para Olá **caminho do módulo** valores conforme Olá após o arquivo de configurações de JSON.

Olá Olá\_world\_processo de exemplo usa o arquivo de configuração de JSON Olá caminho tooa como um argumento de linha de comando. Olá seguinte arquivo JSON de exemplo é fornecido no repositório do SDK de saudação em **exemplos\\Olá\_world\\src\\Olá\_world\_win.json**. Isso funciona de arquivo de configuração como está a menos que você modifique Olá compilar módulos de saudação do script tooplace IoT borda ou amostra executáveis em locais não padrão.

> [!NOTE]
> caminhos de módulo Olá são diretório relativo toohello onde Olá Olá\_world\_sample.exe está localizado. exemplo Hello JSON configuração arquivo padrões toowriting 'txt' no diretório de trabalho atual.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Navegue toohello **criar** pasta na raiz de saudação da sua cópia local da saudação **iot borda** repositório.

1. Execute Olá comando a seguir:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
