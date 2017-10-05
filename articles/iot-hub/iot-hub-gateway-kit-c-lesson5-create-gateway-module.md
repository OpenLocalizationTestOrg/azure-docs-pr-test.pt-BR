---
title: "Criar seu primeiro módulo Azure IoT Gateway | Microsoft Docs"
description: "Crie um módulo e adicioná-la a um aplicativo de exemplo para personalizar os comportamentos de módulo."
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="4df31-103">Lição 5: Criar o primeiro módulo de Gateway de IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="4df31-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="4df31-104">Embora o Azure IoT Edge permita que você crie módulos escritos em Java, .NET ou Node.js, este tutorial explica as etapas para criar um módulo em C.</span><span class="sxs-lookup"><span data-stu-id="4df31-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4df31-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="4df31-105">What you will do</span></span>

- <span data-ttu-id="4df31-106">Compile e execute o aplicativo de exemplo hello_world no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="4df31-107">Crie um módulo e o compile no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="4df31-108">Adicione o novo módulo ao aplicativo de exemplo hello_world e então execute a amostra no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="4df31-109">O novo módulo imprime mensagens de "hello_world" com um carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="4df31-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4df31-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4df31-110">What you will learn</span></span>

- <span data-ttu-id="4df31-111">Como compilar e executar um aplicativo de exemplo no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="4df31-112">Como criar um módulo.</span><span class="sxs-lookup"><span data-stu-id="4df31-112">How to create a module.</span></span>
- <span data-ttu-id="4df31-113">Como adicionar o módulo para um aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="4df31-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4df31-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="4df31-114">What you need</span></span>

<span data-ttu-id="4df31-115">O Azure IoT Edge foi instalado no computador host.</span><span class="sxs-lookup"><span data-stu-id="4df31-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="4df31-116">Estrutura de pastas</span><span class="sxs-lookup"><span data-stu-id="4df31-116">Folder structure</span></span>

<span data-ttu-id="4df31-117">Na subpasta Lesson 5 do código de exemplo que você clonou na lição 1, há uma pasta `module` e uma pasta `sample`.</span><span class="sxs-lookup"><span data-stu-id="4df31-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="4df31-119">A pasta `module/my_module` contém o código-fonte e o script para criar o módulo.</span><span class="sxs-lookup"><span data-stu-id="4df31-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="4df31-120">A pasta `sample` contém o código-fonte e o script para criar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="4df31-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="4df31-121">Compile e execute o aplicativo de exemplo hello_world em Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4df31-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="4df31-122">O exemplo `hello_world` cria um gateway com base no arquivo `hello_world.json` que especifica os dois módulos predefinidos associados ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4df31-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="4df31-123">O gateway registra uma mensagem "hello world" em um arquivo de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="4df31-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="4df31-124">Nesta seção, você pode compilar e executar o aplicativo `hello_world` com seu módulo padrão.</span><span class="sxs-lookup"><span data-stu-id="4df31-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="4df31-125">Para compilar e executar o aplicativo `hello_world`, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="4df31-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="4df31-126">Inicialize os arquivos de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4df31-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="4df31-127">Atualize o arquivo de configuração do gateway com o endereço MAC do Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="4df31-128">Ignore esta etapa se você visto a lição para [configurar e executar um aplicativo de exemplo BLE][config_ble].</span><span class="sxs-lookup"><span data-stu-id="4df31-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="4df31-129">Abra o arquivo de configuração do gateway executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="4df31-130">Atualize o endereço MAC do gateway quando [configurar o Intel NUC como um gateway IoT][setup_nuc] e então salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="4df31-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="4df31-131">Compile o código-fonte, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="4df31-132">O comando transfere o código-fonte para Intel NUC e executa `build.sh` para compilá-lo.</span><span class="sxs-lookup"><span data-stu-id="4df31-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="4df31-133">Execute o aplicativo `hello_world` no Intel NUC executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="4df31-134">O comando executa `../Tools/run-hello-world.js`, que é especificado em `config.json` para iniciar o aplicativo de exemplo no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="4df31-136">Crie um novo módulo e compilá-lo na Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4df31-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="4df31-137">As etapas a seguir orientam você durante a criação de um novo módulo e compile-o no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="4df31-138">O módulo imprime mensagens com um carimbo de hora após recebê-los.</span><span class="sxs-lookup"><span data-stu-id="4df31-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="4df31-139">Você irá criar o primeiro módulo gateway personalizado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="4df31-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="4df31-140">Qualquer módulo do Azure IoT Edge deve implementar as seguintes interfaces:</span><span class="sxs-lookup"><span data-stu-id="4df31-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="4df31-141">Opcionalmente, você pode implementar a interface a seguir:</span><span class="sxs-lookup"><span data-stu-id="4df31-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="4df31-142">O diagrama a seguir mostra os caminhos de estado importantes de um módulo.</span><span class="sxs-lookup"><span data-stu-id="4df31-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="4df31-143">Os retângulos quadrados representam métodos que implementar para executar operações quando o módulo se movem entre estados.</span><span class="sxs-lookup"><span data-stu-id="4df31-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="4df31-144">Os ovais são principais estados que de módulo pode ser no.</span><span class="sxs-lookup"><span data-stu-id="4df31-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="4df31-146">Agora vamos criar um módulo com base no modelo:</span><span class="sxs-lookup"><span data-stu-id="4df31-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="4df31-147">Abra a pasta de modelos, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="4df31-149">`src/my_module.c` serve como um modelo que facilita a criação de um módulo.</span><span class="sxs-lookup"><span data-stu-id="4df31-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="4df31-150">O modelo declara as interfaces.</span><span class="sxs-lookup"><span data-stu-id="4df31-150">The template declares the interfaces.</span></span> <span data-ttu-id="4df31-151">Tudo o que você precisa fazer é adicionar lógica à função `MyModule_Receive`.</span><span class="sxs-lookup"><span data-stu-id="4df31-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="4df31-152">`build.sh` é o script de compilação para compilar o módulo no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="4df31-153">Abra o `src/my_module.c` de arquivo e inclui dois arquivos de cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="4df31-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="4df31-154">Adicione o seguinte código à função `MyModule_Receive`:</span><span class="sxs-lookup"><span data-stu-id="4df31-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="4df31-155">Atualize o arquivo `config.json` para especificar a pasta `workspace` no computador host e o caminho de implantação no Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4df31-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="4df31-156">Durante a compilação, os arquivos na pasta `workspace` serão transferidos para o caminho de implantação.</span><span class="sxs-lookup"><span data-stu-id="4df31-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="4df31-157">Abra o arquivo `config.json` executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="4df31-158">Atualize `config.json` com a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="4df31-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="4df31-160">Compile o módulo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="4df31-161">O comando transfere o código-fonte para Intel NUC e executa `build.sh` para compilar o módulo.</span><span class="sxs-lookup"><span data-stu-id="4df31-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="4df31-162">Adicionar o módulo para o aplicativo de exemplo hello_world e execute o aplicativo em Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4df31-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="4df31-163">Para executar essa tarefa, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4df31-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="4df31-164">Liste todos os módulo binários (arquivos .so) no Intel NUC executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="4df31-165">O caminho binário do `my_module` que você compilou deve estar listado como abaixo:</span><span class="sxs-lookup"><span data-stu-id="4df31-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="4df31-166">Se você alterar o nome de usuário de logon padrão em `config-gateway.json`, o caminho binário será iniciado com `home/<your username>` em vez de `root`.</span><span class="sxs-lookup"><span data-stu-id="4df31-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="4df31-167">Adicione `my_module` ao aplicativo e exemplo `hello_world`:</span><span class="sxs-lookup"><span data-stu-id="4df31-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="4df31-168">Abra o arquivo `hello_world.json` executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="4df31-169">Adicione o seguinte código à seção `modules`:</span><span class="sxs-lookup"><span data-stu-id="4df31-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="4df31-170">O valor de `module.path` deve ser `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="4df31-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="4df31-171">O código declara `my_module` a ser associado com o gateway, bem como o local do módulo binário especificado em `module.path`.</span><span class="sxs-lookup"><span data-stu-id="4df31-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="4df31-172">Adicione o seguinte código à seção `links`:</span><span class="sxs-lookup"><span data-stu-id="4df31-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="4df31-173">Esse código especifica que as mensagens são transferidas do `hello_world` módulo `my_module`.</span><span class="sxs-lookup"><span data-stu-id="4df31-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="4df31-175">Execute o `hello_world` aplicativo de exemplo, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4df31-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="4df31-176">O `--config` parâmetro força o `run-hello-world.js` script a ser executado usando o `hello_world.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="4df31-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="4df31-178">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="4df31-178">Congratulations.</span></span> <span data-ttu-id="4df31-179">Agora você pode ver o comportamento do novo módulo, ele simplesmente imprime mensagens de "hello world" com um carimbo de hora, um resultado diferente do módulo "hello_world" original.</span><span class="sxs-lookup"><span data-stu-id="4df31-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4df31-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4df31-180">Next Steps</span></span>

<span data-ttu-id="4df31-181">Você já criou um novo módulo, adicionou à hello_world exemplo e obter o aplicativo de exemplo para executar com o novo módulo no gateway.</span><span class="sxs-lookup"><span data-stu-id="4df31-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="4df31-182">Se você quiser saber mais sobre os módulos de gateway IoT do Azure, você pode encontrar mais exemplos de módulo: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="4df31-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
