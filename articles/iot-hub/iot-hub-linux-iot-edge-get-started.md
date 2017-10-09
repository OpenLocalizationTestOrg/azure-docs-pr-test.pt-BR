---
title: aaaGet iniciado com borda de IoT do Azure (Linux) | Microsoft Docs
description: "Como toobuild um gateway em um Linux computador e saiba mais sobre conceitos principais no Azure IoT Edge como módulos e arquivos de configuração JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Explorar a arquitetura do Edge IoT do Azure no Linux

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Como toorun Olá exemplo

Olá **build.sh** script gera a saída no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório. Essa saída inclui módulos de borda IoT dois Olá usados neste exemplo.

Olá locais de script de compilação **liblogger.so** em Olá **compilação/módulos/agente/** pasta e **libhello\_world.so** em hello **build / módulos/hello_world/** pasta. Usar estes caminhos para Olá **caminho do módulo** valores conforme Olá arquivo de configurações de JSON de exemplo a seguir.

Olá Olá\_world\_processo de exemplo usa o arquivo de configuração de JSON do hello caminho tooa um argumento de linha de comando. Olá seguinte arquivo JSON de exemplo é fornecido no repositório do SDK de saudação em **exemplos/Olá\_src/world/Olá\_world\_lin.json**. Isso funciona de arquivo de configuração como está a menos que você modifique Olá compilar módulos de saudação do script tooplace IoT borda ou amostra executáveis em locais não padrão.

> [!NOTE]
> Olá, caminhos de módulo são toohello relativo atual diretório de trabalho de onde Olá Olá\_world\_exemplo executável é iniciado, não Olá diretório onde Olá executável está localizado. exemplo Hello JSON configuração arquivo padrões toowriting 'txt' no diretório de trabalho atual.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Navegue toohello **criar** pasta na raiz de saudação da sua cópia local da saudação **iot borda** repositório.

1. Execute Olá comando a seguir:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

