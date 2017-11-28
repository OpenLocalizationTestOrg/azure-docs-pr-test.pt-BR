---
title: "conversão de aaaData no gateway IoT com borda de IoT do Azure | Microsoft Docs"
description: "Use IoT gateway tooconvert Olá formato de dados de sensor por meio de um módulo personalizado de borda de IoT do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversão de dados do gateway iot, transformação de dados do gateway iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="cf1f3-104">Usar o gateway IoT para transformação dos dados de sensor com o Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="cf1f3-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="cf1f3-105">Antes de iniciar este tutorial, certifique-se de que ter concluído Olá lições a seguir na sequência:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="cf1f3-106">Configurar a NUC Intel como um gateway IoT</span><span class="sxs-lookup"><span data-stu-id="cf1f3-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="cf1f3-107">Usar IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf1f3-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="cf1f3-108">Uma finalidade de um gateway de Iot é tooprocess coletados dados antes de enviá-la toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="cf1f3-109">Borda de IoT do Azure apresenta módulos que podem ser o fluxo de trabalho de processamento de dados de saudação tooform criado e montado.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="cf1f3-110">Um módulo recebe uma mensagem, executa alguma ação nele e, em seguida, movê-lo para outros módulos tooprocess.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cf1f3-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="cf1f3-111">What you learn</span></span>

<span data-ttu-id="cf1f3-112">Você aprenderá como toocreate tooconvert um módulo mensagens de saudação SensorTag em um formato diferente.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cf1f3-113">O que fazer</span><span class="sxs-lookup"><span data-stu-id="cf1f3-113">What you do</span></span>

* <span data-ttu-id="cf1f3-114">Crie um módulo tooconvert uma mensagem recebida no formato do hello. JSON.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="cf1f3-115">Compile o módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-115">Compile hello module.</span></span>
* <span data-ttu-id="cf1f3-116">Adicione o aplicativo de exemplo hello módulo toohello Bilitar da borda do IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="cf1f3-117">Execute o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cf1f3-118">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="cf1f3-118">What you need</span></span>

* <span data-ttu-id="cf1f3-119">Olá tutoriais concluídas na sequência a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="cf1f3-120">Configurar a NUC Intel como um gateway IoT</span><span class="sxs-lookup"><span data-stu-id="cf1f3-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="cf1f3-121">Usar IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf1f3-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="cf1f3-122">Um cliente SSH executado no computador host.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="cf1f3-123">Recomenda-se o PuTTY no Windows.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="cf1f3-124">O Linux e o macOS já vêm com um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="cf1f3-125">Olá endereço IP e Olá username e password tooaccess Olá gateway de cliente SSH hello.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="cf1f3-126">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="cf1f3-127">Criar um módulo</span><span class="sxs-lookup"><span data-stu-id="cf1f3-127">Create a module</span></span>

1. <span data-ttu-id="cf1f3-128">No computador de host Olá, execute o cliente SSH hello e conecte-se toohello IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="cf1f3-129">Clone arquivos de origem de saudação do módulo de conversão de saudação do diretório base do GitHub toohello do gateway de IoT Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="cf1f3-130">Este é um módulo nativo do Azure borda escrito na linguagem de programação C de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="cf1f3-131">módulo Olá converte o formato de saudação de mensagens recebidas em Olá seguindo um:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="cf1f3-132">Compilar o módulo Olá</span><span class="sxs-lookup"><span data-stu-id="cf1f3-132">Compile hello module</span></span>

<span data-ttu-id="cf1f3-133">módulo de saudação toocompile, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="cf1f3-134">Você obtém um `libmy_module.so` após a compilação de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="cf1f3-135">Faça uma anotação de caminho absoluto do hello desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="cf1f3-136">Adicionar o aplicativo de exemplo hello módulo toohello Bilitar</span><span class="sxs-lookup"><span data-stu-id="cf1f3-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="cf1f3-137">Pasta de exemplos toohello vá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="cf1f3-138">Abra o arquivo de configuração de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="cf1f3-139">Adicionar um módulo inserindo Olá toohello de código a seguir `modules` seção.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="cf1f3-140">Substitua `[Your libmy_module.so path]` no código de saudação com caminho absoluto de saudação do hello libmy_module.so' arquivo.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="cf1f3-141">Substitua o código Olá Olá `links` seção com hello seguindo um:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="cf1f3-142">Pressione `ESC`e, em seguida, digite `:wq` toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="cf1f3-143">Executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="cf1f3-143">Run hello sample application</span></span>

1. <span data-ttu-id="cf1f3-144">Ligar Olá SensorTag.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="cf1f3-145">Definir variável de ambiente SSL_CERT_FILE Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="cf1f3-146">Execute o aplicativo de exemplo hello com módulo adicionado Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf1f3-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="cf1f3-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf1f3-147">Next steps</span></span>

<span data-ttu-id="cf1f3-148">Com êxito, que você use Olá IoT gateway tooconvert mensagem de saudação SensorTag em formato do hello. JSON.</span><span class="sxs-lookup"><span data-stu-id="cf1f3-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
