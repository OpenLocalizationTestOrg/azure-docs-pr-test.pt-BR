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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Lição 5: Criar o primeiro módulo de Gateway de IoT do Azure
Enquanto o Azure IoT borda permite toobuild módulos escritos em Java, .NET ou Node. js, este tutorial orienta você pelas etapas de saudação para a criação de um módulo em C.

## <a name="what-you-will-do"></a>O que você fará

- Compile e execute o aplicativo de exemplo hello hello_world em NUC Intel.
- Crie um módulo e o compile no Intel NUC.
- Adicionar Olá novo módulo toohello hello_world aplicativo de exemplo e, em seguida, executar o exemplo hello em NUC Intel. novo módulo de saudação imprime mensagens de "hello_world" com um carimbo de hora.

## <a name="what-you-will-learn"></a>O que você aprenderá

- Como toocompile e executar um aplicativo de exemplo em NUC Intel.
- Como toocreate um módulo.
- Como tooadd módulo tooa aplicativo de exemplo.

## <a name="what-you-need"></a>O que você precisa

O Azure IoT Edge foi instalado no computador host.

## <a name="folder-structure"></a>Estrutura de pastas

Na subpasta Olá lição 5 do código de exemplo hello que você clonou na lição 1, há um `module` pasta e um `sample` pasta.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Olá `module/my_module` pasta contém Olá código e script toobuild Olá módulo de fonte.
- Olá `sample` pasta contém Olá fonte código e script toobuild Olá aplicativo de exemplo.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Compilar e executar o aplicativo de exemplo hello hello_world no Intel NUC

Olá `hello_world` exemplo cria um gateway com base em Olá `hello_world.json` arquivo que especifica Olá dois módulos predefinidos associados ao aplicativo hello. logs do gateway do Hello um arquivo de tooa de mensagem "hello world" a cada 5 segundos. Nesta seção, você pode compilar e executar Olá `hello_world` aplicativo com o seu módulo padrão.

Olá toocompile e execute `hello_world` aplicativo, siga estas etapas no computador host:

1. Inicialize os arquivos de configuração Olá executando Olá comandos a seguir:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Atualize o arquivo de configuração do gateway de saudação com hello endereço MAC de NUC Intel. Ignore esta etapa se você tiver feito por meio da lição Olá muito[configurar e executar um aplicativo de exemplo Bilitar][config_ble].

   1. Abra o arquivo de configuração do gateway de saudação executando Olá comando a seguir:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Do gateway da saudação de atualização endereços MAC quando você [configurar NUC Intel como um gateway IoT][setup_nuc]e, em seguida, salve o arquivo hello.

1. Compile o código-fonte exemplo hello executando Olá comando a seguir:

   ```bash
   gulp compile
   ```

   Olá comando transfere Olá exemplo fonte código tooIntel NUC e executa `build.sh` toocompile-lo.

1. Executar Olá `hello_world` aplicativo no Intel NUC executando Olá comando a seguir:

   ```bash
   gulp run
   ```

   Olá a execução do comando `../Tools/run-hello-world.js` especificada na `config.json` toostart aplicativo de exemplo hello em NUC Intel.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Crie um novo módulo e compilá-lo na Intel NUC

etapas de saudação abaixo orientarão-lo a criar um novo módulo e compilação-lo em NUC Intel. módulo de saudação imprime mensagens com um carimbo de hora após recebê-los. Você irá criar o primeiro módulo gateway personalizado nesta seção.

Qualquer módulo do Azure IoT borda deve implementar Olá interfaces a seguir:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

Opcionalmente, você pode implementar Olá interface a seguir:

   ```C
   pfModule_Start Module_Start
   ```

Olá diagrama a seguir mostra os caminhos de estado importantes de saudação de um módulo. retângulos quadrado Olá representam métodos implementar operações tooperform quando o módulo de saudação se move entre estados. elipses Olá são principais estados Olá módulo pode ser no.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Agora vamos criar um módulo com base no modelo de saudação:

1. Abra a pasta de modelo de saudação executando Olá comando a seguir:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`serve como um modelo que facilita a criação de saudação de um módulo. modelo de saudação declara interfaces hello. Você só precisa toodo é tooadd lógica toohello `MyModule_Receive` função.
   - `build.sh`é Olá compilação script toocompile Olá módulo em NUC Intel.
1. Olá abrir `src/my_module.c` de arquivo e incluir os dois arquivos de cabeçalho:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Adicionar Olá toohello de código a seguir `MyModule_Receive` função:

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

1. Saudação de atualização `config.json` saudação do arquivo toospecify `workspace` pasta no seu computador e hello implantação caminho do host no Intel NUC. Durante a compilação, Olá arquivos Olá `workspace` pasta será transferido toohello caminho de implantação.

   1. Olá abrir `config.json` arquivo executando Olá comando a seguir:

      ```bash
      code config.json
      ```

   1. Atualização `config.json` com hello a seguinte configuração:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Compile o módulo Olá executando Olá comando a seguir:

   ```bash
   gulp compile
   ```

   Olá comando transfere Olá fonte código tooIntel NUC e executa `build.sh` toocompile módulo de saudação.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Adicionar o aplicativo de exemplo hello módulo toohello hello_world e executar o aplicativo hello no Intel NUC

tooperform tarefas, siga estas etapas:

1. Lista todos os binários de módulo de saudação (arquivos. SO) Intel NUC executando Olá comando a seguir:

   ```bash
   gulp modules --list
   ```

   caminho binário de saudação do `my_module` que é compilado deve ser listado abaixo:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Se você alterar o nome de usuário de logon padrão de saudação em `config-gateway.json`, caminho binário Olá iniciará com `home/<your username>` em vez de `root`.

1. Adicionar `my_module` toohello `hello_world` aplicativo de exemplo:

   1. Olá abrir `hello_world.json` arquivo executando Olá comando a seguir:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Adicionar Olá toohello de código a seguir `modules` seção:

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

      Olá valor `module.path` devem ser `/root/gateway_sample/module/my_module/build/libmy_module.so`. Olá código declara `my_module` toobe associado gateway hello, bem como o local de saudação de binários de módulo Olá especificado em `module.path`.
   1. Adicionar Olá toohello de código a seguir `links` seção:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Esse código especifica que as mensagens são transferidas da saudação `hello_world` módulo muito`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Executar Olá `hello_world` amostra de aplicativo executando Olá comando a seguir:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Olá `--config` parâmetro força Olá `run-hello-world.js` script toorun usando Olá `hello_world.json` arquivo.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Parabéns. Agora você pode ver o comportamento de saudação do novo módulo, simplesmente exibe mensagens de "hello world" com um carimbo de hora, um resultado diferente do módulo do hello original "hello_world".

## <a name="next-steps"></a>Próximas etapas

Você já criou um novo módulo, adicionado toohello hello_world exemplo e get hello exemplo aplicativo toorun com o novo módulo de saudação no gateway. Se você quiser toolearn mais sobre os módulos de gateway IoT do Azure, você pode encontrar mais amostras de módulo: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
