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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="42987-103">Explorar a arquitetura do Edge IoT do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="42987-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="42987-104">Como toorun Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="42987-104">How toorun hello sample</span></span>

<span data-ttu-id="42987-105">Olá **build.sh** script gera a saída no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="42987-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="42987-106">Essa saída inclui módulos de borda IoT dois Olá usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="42987-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="42987-107">Olá locais de script de compilação **liblogger.so** em Olá **compilação/módulos/agente/** pasta e **libhello\_world.so** em hello **build / módulos/hello_world/** pasta.</span><span class="sxs-lookup"><span data-stu-id="42987-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="42987-108">Usar estes caminhos para Olá **caminho do módulo** valores conforme Olá arquivo de configurações de JSON de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="42987-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="42987-109">Olá Olá\_world\_processo de exemplo usa o arquivo de configuração de JSON do hello caminho tooa um argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="42987-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="42987-110">Olá seguinte arquivo JSON de exemplo é fornecido no repositório do SDK de saudação em **exemplos/Olá\_src/world/Olá\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="42987-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="42987-111">Isso funciona de arquivo de configuração como está a menos que você modifique Olá compilar módulos de saudação do script tooplace IoT borda ou amostra executáveis em locais não padrão.</span><span class="sxs-lookup"><span data-stu-id="42987-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="42987-112">Olá, caminhos de módulo são toohello relativo atual diretório de trabalho de onde Olá Olá\_world\_exemplo executável é iniciado, não Olá diretório onde Olá executável está localizado.</span><span class="sxs-lookup"><span data-stu-id="42987-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="42987-113">exemplo Hello JSON configuração arquivo padrões toowriting 'txt' no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="42987-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="42987-114">Navegue toohello **criar** pasta na raiz de saudação da sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="42987-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="42987-115">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="42987-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

