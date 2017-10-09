---
title: aaaConnect um dispositivo usando C no Linux | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurados de solução de monitoramento remota usando um aplicativo escrito em C em execução no Linux."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Conecte-se a sua solução pré-configurada (Linux) de monitoramento remoto de toohello de dispositivo
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Criar e executar um cliente C de exemplo Linux
Olá etapas a seguir mostra como toocreate um aplicativo cliente que se comunica com o monitoramento remoto Olá pré-configurado solução. Esse aplicativo é escrito em C e compilado e executado no Ubuntu Linux.

toocomplete essas etapas, você precisa de um dispositivo executando Ubuntu 15.04 ou 15.10 de versão. Antes de prosseguir, instale pacotes de pré-requisitos de saudação no dispositivo Ubuntu usando Olá comando a seguir:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Instalar bibliotecas de saudação do cliente no dispositivo
Olá bibliotecas de cliente do Azure IoT Hub estão disponíveis como um pacote pode ser instalado no dispositivo Ubuntu usando Olá **apt get** comando. Olá concluída após o pacote de saudação de tooinstall de etapas que contém hello biblioteca de cliente de IoT Hub e arquivos de cabeçalho no seu computador Ubuntu:

1. Um shell, adicione Olá AzureIoT repositório tooyour:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Instalar o pacote do azure-iot-sdk-c-dev Olá
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Instalar Olá analisador JSON Parson
Olá usam bibliotecas de cliente de IoT Hub Olá cargas de mensagem JSON Parson analisador tooparse. Em uma pasta adequada no seu computador, clone repositório do GitHub Parson hello usando Olá comando a seguir:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Preparar seu projeto
No computador Ubuntu, crie uma pasta chamada **remote\_monitoring**. Em Olá **remoto\_monitoramento** pasta:

- Crie quatro arquivos de saudação **main.c**, **remoto\_monitoring.c**, **remoto\_monitoring.h**, e **CMakeLists.txt**.
- Crie uma pasta chamada **parson**.

Copiar arquivos Olá **parson.c** e **parson.h** da sua cópia local do repositório de Parson Olá em Olá **remoto\_monitoramento/parson** pasta.

Em um editor de texto, abra Olá **remoto\_monitoring.c** arquivo. Adicione o seguinte Olá `#include` instruções:
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a>Chamar hello remoto\_monitoramento\_executar a função
Em um editor de texto, abra Olá **remote_monitoring.h** arquivo. Adicione Olá código a seguir:

```
void remote_monitoring_run(void);
```

Em um editor de texto, abra Olá **main.c** arquivo. Adicione Olá código a seguir:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Compilar e executar o aplicativo hello
Olá etapas a seguir descrevem como toouse *CMake* toobuild seu aplicativo cliente.

1. Em um editor de texto, abra Olá **CMakeLists.txt** arquivo hello **remote_monitoring** pasta.

1. Adicionar Olá toodefine instruções a seguir como toobuild seu aplicativo cliente:
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. Em hello **remote_monitoring** pasta, crie uma saudação de toostore pasta *fazer* arquivos que CMake gera e, em seguida, executar Olá **cmake** e **fazer** comandos da seguinte maneira:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Execute o aplicativo de cliente hello e enviar telemetria tooIoT Hub:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

