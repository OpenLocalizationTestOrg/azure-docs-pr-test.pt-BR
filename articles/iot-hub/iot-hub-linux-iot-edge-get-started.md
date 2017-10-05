---
title: "Introdução ao Azure IoT Edge (Linux) |Microsoft Docs"
description: "Como criar um gateway em um computador Linux e saber mais sobre os principais conceitos Edge IoT do Azure, tais como módulos e arquivos de configuração JSON."
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="1db9e-103">Explorar a arquitetura do Edge IoT do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="1db9e-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="1db9e-104">Como executar a amostra</span><span class="sxs-lookup"><span data-stu-id="1db9e-104">How to run the sample</span></span>

<span data-ttu-id="1db9e-105">O script **build.sh** gera sua saída na pasta **build** na cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="1db9e-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="1db9e-106">Essa saída inclui os dois módulos do Edge IoT usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="1db9e-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="1db9e-107">O script de build coloca **liblogger.so** na pasta **build/modules/logger/** e **libhello\_world.so** na pasta **build/modules/hello_world/**.</span><span class="sxs-lookup"><span data-stu-id="1db9e-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="1db9e-108">Use esses caminhos para os valores de **caminho do módulo**, conforme mostrado no arquivo de configurações do JSON de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1db9e-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="1db9e-109">O processo hello\_world\_sample leva o caminho até um arquivo de configuração JSON como um argumento na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1db9e-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="1db9e-110">O arquivo JSON de exemplo a seguir é fornecido no repositório SDK em **samples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="1db9e-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="1db9e-111">Este arquivo de configuração funciona da forma como está, a menos que você tenha modificado o script de build para colocar os módulos ou os executáveis de exemplo do IoT Edge em locais não padrão.</span><span class="sxs-lookup"><span data-stu-id="1db9e-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="1db9e-112">Os caminhos do módulo são relativos ao diretório de trabalho atual de onde o executável hello\_world\_sample é iniciado, não ao diretório onde o executável está localizado.</span><span class="sxs-lookup"><span data-stu-id="1db9e-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="1db9e-113">O arquivo de configuração do JSON de exemplo assume o padrão de gravar 'log.txt' no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="1db9e-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="1db9e-114">Navegue até a pasta **build** na raiz da sua cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="1db9e-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="1db9e-115">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1db9e-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

