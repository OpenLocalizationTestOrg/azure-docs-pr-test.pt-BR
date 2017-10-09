---
title: "aaaCreate seu módulo de Azure IoT Gateway primeiro | Microsoft Docs"
description: "Crie um módulo e adicioná-lo a comportamentos de módulo tooa exemplo aplicativo toocustomize."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="7db70-103">Lição 5: Criar o primeiro módulo de Gateway de IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="7db70-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="7db70-104">Enquanto o Azure IoT borda permite toobuild módulos escritos em Java, .NET ou Node. js, este tutorial orienta você pelas etapas de saudação para a criação de um módulo em C.</span><span class="sxs-lookup"><span data-stu-id="7db70-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7db70-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7db70-105">What you will do</span></span>

- <span data-ttu-id="7db70-106">Compile e execute o aplicativo de exemplo hello hello_world em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="7db70-107">Crie um módulo e o compile no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="7db70-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="7db70-108">Adicionar Olá novo módulo toohello hello_world aplicativo de exemplo e, em seguida, executar o exemplo hello em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="7db70-109">novo módulo de saudação imprime mensagens de "hello_world" com um carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="7db70-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7db70-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7db70-110">What you will learn</span></span>

- <span data-ttu-id="7db70-111">Como toocompile e executar um aplicativo de exemplo em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="7db70-112">Como toocreate um módulo.</span><span class="sxs-lookup"><span data-stu-id="7db70-112">How toocreate a module.</span></span>
- <span data-ttu-id="7db70-113">Como tooadd módulo tooa aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7db70-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7db70-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7db70-114">What you need</span></span>

<span data-ttu-id="7db70-115">O Azure IoT Edge foi instalado no computador host.</span><span class="sxs-lookup"><span data-stu-id="7db70-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="7db70-116">Estrutura de pastas</span><span class="sxs-lookup"><span data-stu-id="7db70-116">Folder structure</span></span>

<span data-ttu-id="7db70-117">Na subpasta Olá lição 5 do código de exemplo hello que você clonou na lição 1, há um `module` pasta e um `sample` pasta.</span><span class="sxs-lookup"><span data-stu-id="7db70-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="7db70-119">Olá `module/my_module` pasta contém Olá código e script toobuild Olá módulo de fonte.</span><span class="sxs-lookup"><span data-stu-id="7db70-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="7db70-120">Olá `sample` pasta contém Olá fonte código e script toobuild Olá aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7db70-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="7db70-121">Compilar e executar o aplicativo de exemplo hello hello_world no Intel NUC</span><span class="sxs-lookup"><span data-stu-id="7db70-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="7db70-122">Olá `hello_world` exemplo cria um gateway com base em Olá `hello_world.json` arquivo que especifica Olá dois módulos predefinidos associados ao aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7db70-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="7db70-123">logs do gateway do Hello um arquivo de tooa de mensagem "hello world" a cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="7db70-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="7db70-124">Nesta seção, você pode compilar e executar Olá `hello_world` aplicativo com o seu módulo padrão.</span><span class="sxs-lookup"><span data-stu-id="7db70-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="7db70-125">Olá toocompile e execute `hello_world` aplicativo, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="7db70-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="7db70-126">Inicialize os arquivos de configuração Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="7db70-127">Atualize o arquivo de configuração do gateway de saudação com hello endereço MAC de NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="7db70-128">Ignore esta etapa se você tiver feito por meio da lição Olá muito[configurar e executar um aplicativo de exemplo Bilitar][config_ble].</span><span class="sxs-lookup"><span data-stu-id="7db70-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="7db70-129">Abra o arquivo de configuração do gateway de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="7db70-130">Do gateway da saudação de atualização endereços MAC quando você [configurar NUC Intel como um gateway IoT][setup_nuc]e, em seguida, salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="7db70-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="7db70-131">Compile o código-fonte exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="7db70-132">Olá comando transfere Olá exemplo fonte código tooIntel NUC e executa `build.sh` toocompile-lo.</span><span class="sxs-lookup"><span data-stu-id="7db70-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="7db70-133">Executar Olá `hello_world` aplicativo no Intel NUC executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="7db70-134">Olá a execução do comando `../Tools/run-hello-world.js` especificada na `config.json` toostart aplicativo de exemplo hello em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="7db70-136">Crie um novo módulo e compilá-lo na Intel NUC</span><span class="sxs-lookup"><span data-stu-id="7db70-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="7db70-137">etapas de saudação abaixo orientarão-lo a criar um novo módulo e compilação-lo em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="7db70-138">módulo de saudação imprime mensagens com um carimbo de hora após recebê-los.</span><span class="sxs-lookup"><span data-stu-id="7db70-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="7db70-139">Você irá criar o primeiro módulo gateway personalizado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7db70-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="7db70-140">Qualquer módulo do Azure IoT borda deve implementar Olá interfaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="7db70-141">Opcionalmente, você pode implementar Olá interface a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="7db70-142">Olá diagrama a seguir mostra os caminhos de estado importantes de saudação de um módulo.</span><span class="sxs-lookup"><span data-stu-id="7db70-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="7db70-143">retângulos quadrado Olá representam métodos implementar operações tooperform quando o módulo de saudação se move entre estados.</span><span class="sxs-lookup"><span data-stu-id="7db70-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="7db70-144">elipses Olá são principais estados Olá módulo pode ser no.</span><span class="sxs-lookup"><span data-stu-id="7db70-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="7db70-146">Agora vamos criar um módulo com base no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="7db70-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="7db70-147">Abra a pasta de modelo de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="7db70-149">`src/my_module.c`serve como um modelo que facilita a criação de saudação de um módulo.</span><span class="sxs-lookup"><span data-stu-id="7db70-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="7db70-150">modelo de saudação declara interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="7db70-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="7db70-151">Você só precisa toodo é tooadd lógica toohello `MyModule_Receive` função.</span><span class="sxs-lookup"><span data-stu-id="7db70-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="7db70-152">`build.sh`é Olá compilação script toocompile Olá módulo em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="7db70-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="7db70-153">Olá abrir `src/my_module.c` de arquivo e incluir os dois arquivos de cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="7db70-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="7db70-154">Adicionar Olá toohello de código a seguir `MyModule_Receive` função:</span><span class="sxs-lookup"><span data-stu-id="7db70-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="7db70-155">Saudação de atualização `config.json` saudação do arquivo toospecify `workspace` pasta no seu computador e hello implantação caminho do host no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="7db70-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="7db70-156">Durante a compilação, Olá arquivos Olá `workspace` pasta será transferido toohello caminho de implantação.</span><span class="sxs-lookup"><span data-stu-id="7db70-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="7db70-157">Olá abrir `config.json` arquivo executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="7db70-158">Atualização `config.json` com hello a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="7db70-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="7db70-160">Compile o módulo Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="7db70-161">Olá comando transfere Olá fonte código tooIntel NUC e executa `build.sh` toocompile módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db70-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="7db70-162">Adicionar o aplicativo de exemplo hello módulo toohello hello_world e executar o aplicativo hello no Intel NUC</span><span class="sxs-lookup"><span data-stu-id="7db70-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="7db70-163">tooperform tarefas, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="7db70-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="7db70-164">Lista todos os binários de módulo de saudação (arquivos. SO) Intel NUC executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="7db70-165">caminho binário de saudação do `my_module` que é compilado deve ser listado abaixo:</span><span class="sxs-lookup"><span data-stu-id="7db70-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="7db70-166">Se você alterar o nome de usuário de logon padrão de saudação em `config-gateway.json`, caminho binário Olá iniciará com `home/<your username>` em vez de `root`.</span><span class="sxs-lookup"><span data-stu-id="7db70-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="7db70-167">Adicionar `my_module` toohello `hello_world` aplicativo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7db70-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="7db70-168">Olá abrir `hello_world.json` arquivo executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="7db70-169">Adicionar Olá toohello de código a seguir `modules` seção:</span><span class="sxs-lookup"><span data-stu-id="7db70-169">Add hello following code toohello `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="7db70-170">Olá valor `module.path` devem ser `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="7db70-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="7db70-171">Olá código declara `my_module` toobe associado gateway hello, bem como o local de saudação de binários de módulo Olá especificado em `module.path`.</span><span class="sxs-lookup"><span data-stu-id="7db70-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="7db70-172">Adicionar Olá toohello de código a seguir `links` seção:</span><span class="sxs-lookup"><span data-stu-id="7db70-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="7db70-173">Esse código especifica que as mensagens são transferidas da saudação `hello_world` módulo muito`my_module`.</span><span class="sxs-lookup"><span data-stu-id="7db70-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="7db70-175">Executar Olá `hello_world` amostra de aplicativo executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db70-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="7db70-176">Olá `--config` parâmetro força Olá `run-hello-world.js` script toorun usando Olá `hello_world.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="7db70-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="7db70-178">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="7db70-178">Congratulations.</span></span> <span data-ttu-id="7db70-179">Agora você pode ver o comportamento de saudação do novo módulo, simplesmente exibe mensagens de "hello world" com um carimbo de hora, um resultado diferente do módulo do hello original "hello_world".</span><span class="sxs-lookup"><span data-stu-id="7db70-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7db70-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7db70-180">Next Steps</span></span>

<span data-ttu-id="7db70-181">Você já criou um novo módulo, adicionado toohello hello_world exemplo e get hello exemplo aplicativo toorun com o novo módulo de saudação no gateway.</span><span class="sxs-lookup"><span data-stu-id="7db70-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="7db70-182">Se você quiser toolearn mais sobre os módulos de gateway IoT do Azure, você pode encontrar mais amostras de módulo: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="7db70-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
