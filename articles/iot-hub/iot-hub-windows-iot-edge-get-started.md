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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="7b612-103">Explorar a arquitetura do Azure IoT Edge no Windows</span><span class="sxs-lookup"><span data-stu-id="7b612-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="7b612-104">Como toorun Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="7b612-104">How toorun hello sample</span></span>

<span data-ttu-id="7b612-105">Olá **build.cmd** script gera a saída no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="7b612-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="7b612-106">Essa saída inclui módulos de borda IoT dois Olá usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="7b612-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="7b612-107">Olá locais de script de compilação **logger.dll** em Olá **criar\\módulos\\agente\\depurar** pasta e **Olá\_world.dll**  em Olá **criar\\módulos\\hello_world\\depurar** pasta.</span><span class="sxs-lookup"><span data-stu-id="7b612-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="7b612-108">Usar estes caminhos para Olá **caminho do módulo** valores conforme Olá após o arquivo de configurações de JSON.</span><span class="sxs-lookup"><span data-stu-id="7b612-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="7b612-109">Olá Olá\_world\_processo de exemplo usa o arquivo de configuração de JSON Olá caminho tooa como um argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="7b612-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="7b612-110">Olá seguinte arquivo JSON de exemplo é fornecido no repositório do SDK de saudação em **exemplos\\Olá\_world\\src\\Olá\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="7b612-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="7b612-111">Isso funciona de arquivo de configuração como está a menos que você modifique Olá compilar módulos de saudação do script tooplace IoT borda ou amostra executáveis em locais não padrão.</span><span class="sxs-lookup"><span data-stu-id="7b612-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="7b612-112">caminhos de módulo Olá são diretório relativo toohello onde Olá Olá\_world\_sample.exe está localizado.</span><span class="sxs-lookup"><span data-stu-id="7b612-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="7b612-113">exemplo Hello JSON configuração arquivo padrões toowriting 'txt' no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="7b612-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="7b612-114">Navegue toohello **criar** pasta na raiz de saudação da sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="7b612-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="7b612-115">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b612-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
