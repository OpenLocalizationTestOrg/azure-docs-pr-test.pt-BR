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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="3f2f0-103">Conecte-se a sua solução pré-configurada (Linux) de monitoramento remoto de toohello de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3f2f0-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="3f2f0-104">Criar e executar um cliente C de exemplo Linux</span><span class="sxs-lookup"><span data-stu-id="3f2f0-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="3f2f0-105">Olá etapas a seguir mostra como toocreate um aplicativo cliente que se comunica com o monitoramento remoto Olá pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="3f2f0-106">Esse aplicativo é escrito em C e compilado e executado no Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="3f2f0-107">toocomplete essas etapas, você precisa de um dispositivo executando Ubuntu 15.04 ou 15.10 de versão.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="3f2f0-108">Antes de prosseguir, instale pacotes de pré-requisitos de saudação no dispositivo Ubuntu usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="3f2f0-109">Instalar bibliotecas de saudação do cliente no dispositivo</span><span class="sxs-lookup"><span data-stu-id="3f2f0-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="3f2f0-110">Olá bibliotecas de cliente do Azure IoT Hub estão disponíveis como um pacote pode ser instalado no dispositivo Ubuntu usando Olá **apt get** comando.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="3f2f0-111">Olá concluída após o pacote de saudação de tooinstall de etapas que contém hello biblioteca de cliente de IoT Hub e arquivos de cabeçalho no seu computador Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="3f2f0-112">Um shell, adicione Olá AzureIoT repositório tooyour:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="3f2f0-113">Instalar o pacote do azure-iot-sdk-c-dev Olá</span><span class="sxs-lookup"><span data-stu-id="3f2f0-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="3f2f0-114">Instalar Olá analisador JSON Parson</span><span class="sxs-lookup"><span data-stu-id="3f2f0-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="3f2f0-115">Olá usam bibliotecas de cliente de IoT Hub Olá cargas de mensagem JSON Parson analisador tooparse.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="3f2f0-116">Em uma pasta adequada no seu computador, clone repositório do GitHub Parson hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="3f2f0-117">Preparar seu projeto</span><span class="sxs-lookup"><span data-stu-id="3f2f0-117">Prepare your project</span></span>
<span data-ttu-id="3f2f0-118">No computador Ubuntu, crie uma pasta chamada **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="3f2f0-119">Em Olá **remoto\_monitoramento** pasta:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="3f2f0-120">Crie quatro arquivos de saudação **main.c**, **remoto\_monitoring.c**, **remoto\_monitoring.h**, e **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="3f2f0-121">Crie uma pasta chamada **parson**.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-121">Create folder called **parson**.</span></span>

<span data-ttu-id="3f2f0-122">Copiar arquivos Olá **parson.c** e **parson.h** da sua cópia local do repositório de Parson Olá em Olá **remoto\_monitoramento/parson** pasta.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="3f2f0-123">Em um editor de texto, abra Olá **remoto\_monitoring.c** arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="3f2f0-124">Adicione o seguinte Olá `#include` instruções:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-124">Add hello following `#include` statements:</span></span>
   
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

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="3f2f0-125">Chamar hello remoto\_monitoramento\_executar a função</span><span class="sxs-lookup"><span data-stu-id="3f2f0-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="3f2f0-126">Em um editor de texto, abra Olá **remote_monitoring.h** arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="3f2f0-127">Adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="3f2f0-128">Em um editor de texto, abra Olá **main.c** arquivo.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="3f2f0-129">Adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="3f2f0-130">Compilar e executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="3f2f0-130">Build and run hello application</span></span>
<span data-ttu-id="3f2f0-131">Olá etapas a seguir descrevem como toouse *CMake* toobuild seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="3f2f0-132">Em um editor de texto, abra Olá **CMakeLists.txt** arquivo hello **remote_monitoring** pasta.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="3f2f0-133">Adicionar Olá toodefine instruções a seguir como toobuild seu aplicativo cliente:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
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
1. <span data-ttu-id="3f2f0-134">Em hello **remote_monitoring** pasta, crie uma saudação de toostore pasta *fazer* arquivos que CMake gera e, em seguida, executar Olá **cmake** e **fazer** comandos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="3f2f0-135">Execute o aplicativo de cliente hello e enviar telemetria tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

