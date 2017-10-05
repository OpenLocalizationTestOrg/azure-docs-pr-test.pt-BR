---
title: "Introdução ao Azure IoT Edge (Windows) | Microsoft Docs"
description: "Como criar um gateway em do Azure IoT Edge um computador Windows e saber mais sobre os principais conceitos do Azure IoT Edge, como módulos e arquivos de configuração JSON."
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="0e5f1-103">Explorar a arquitetura do Azure IoT Edge no Windows</span><span class="sxs-lookup"><span data-stu-id="0e5f1-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="0e5f1-104">Como executar a amostra</span><span class="sxs-lookup"><span data-stu-id="0e5f1-104">How to run the sample</span></span>

<span data-ttu-id="0e5f1-105">O script **build.cmd** gera sua saída na pasta **build** na cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="0e5f1-106">Essa saída inclui os dois módulos do Edge IoT usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="0e5f1-107">O script de build coloca **logger.dll** na pasta **build\\modules\\logger\\Debug** e **hello\_world.dll** na pasta **build\\modules\\hello_world\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="0e5f1-108">Use esses caminhos para os valores de **caminho do módulo**, conforme mostrado no arquivo de configurações do JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="0e5f1-109">O processo hello\_world\_sample leva o caminho até um arquivo de configuração JSON como um argumento na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="0e5f1-110">O arquivo JSON de exemplo a seguir é fornecido no repositório SDK em **samples\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="0e5f1-111">Este arquivo de configuração funciona da forma como está, a menos que você tenha modificado o script de build para colocar os módulos ou os executáveis de exemplo do IoT Edge em locais não padrão.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="0e5f1-112">Os caminhos de módulo são relativos ao diretório em que se encontra o hello\_world\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="0e5f1-113">O arquivo de configuração do JSON de exemplo assume o padrão de gravar 'log.txt' no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="0e5f1-114">Navegue até a pasta **build** na raiz da sua cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="0e5f1-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="0e5f1-115">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e5f1-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
