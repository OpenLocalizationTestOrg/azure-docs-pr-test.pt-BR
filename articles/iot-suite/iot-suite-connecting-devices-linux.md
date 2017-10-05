---
title: Conectar um dispositivo usando o C no Linux | Microsoft Docs
description: "Descreve como conectar um dispositivo à solução pré-configurada de monitoramento remoto do Azure IoT Suite usando um aplicativo escrito em C em execução no Linux."
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
ms.openlocfilehash: 9adbc9cc13f0b4cafa3a3a7703c46f8085b15232
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="10829-103">Conectar seu dispositivo à solução pré-configurada de monitoramento remoto (Linux)</span><span class="sxs-lookup"><span data-stu-id="10829-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="10829-104">Criar e executar um cliente C de exemplo Linux</span><span class="sxs-lookup"><span data-stu-id="10829-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="10829-105">As etapas a seguir mostram como criar um aplicativo cliente que se comunica com a solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="10829-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="10829-106">Esse aplicativo é escrito em C e compilado e executado no Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="10829-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="10829-107">Para concluir essas etapas, você precisa de um dispositivo em execução na versão 15.04 ou 15.10 do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="10829-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="10829-108">Antes de continuar, instale os pacotes de pré-requisitos no seu dispositivo Ubuntu usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="10829-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="10829-109">Instalar as bibliotecas de cliente no dispositivo</span><span class="sxs-lookup"><span data-stu-id="10829-109">Install the client libraries on your device</span></span>
<span data-ttu-id="10829-110">As bibliotecas de cliente do Hub IoT do Azure estão disponíveis como um pacote que você pode instalar em seu dispositivo Ubuntu usando o comando **apt-get** .</span><span class="sxs-lookup"><span data-stu-id="10829-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="10829-111">Conclua as seguintes etapas para instalar o pacote que contém os arquivos de biblioteca e cabeçalho do cliente Hub IoT em seu computador Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="10829-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="10829-112">Em um shell, adicione o repositório AzureIoT ao computador:</span><span class="sxs-lookup"><span data-stu-id="10829-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="10829-113">Instale o pacote azure-iot-sdk-c-dev</span><span class="sxs-lookup"><span data-stu-id="10829-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="10829-114">Instalar o analisador JSON Parson</span><span class="sxs-lookup"><span data-stu-id="10829-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="10829-115">As bibliotecas de cliente do Hub IoT usam o analisador JSON Parson para analisar cargas de mensagem.</span><span class="sxs-lookup"><span data-stu-id="10829-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="10829-116">Em uma pasta adequada no computador, clone o repositório Parson GitHub usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="10829-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="10829-117">Preparar seu projeto</span><span class="sxs-lookup"><span data-stu-id="10829-117">Prepare your project</span></span>
<span data-ttu-id="10829-118">No computador Ubuntu, crie uma pasta chamada **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="10829-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="10829-119">Na pasta **remote\_monitoring**:</span><span class="sxs-lookup"><span data-stu-id="10829-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="10829-120">Crie os quatro arquivos **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h** e **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="10829-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="10829-121">Crie uma pasta chamada **parson**.</span><span class="sxs-lookup"><span data-stu-id="10829-121">Create folder called **parson**.</span></span>

<span data-ttu-id="10829-122">Copie os arquivos **parson.c** e **parson.h** de sua cópia local do repositório Parson para a pasta **remote\_monitoring/parson**.</span><span class="sxs-lookup"><span data-stu-id="10829-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="10829-123">Em um editor de texto, abra o arquivo **remote\_monitoring.c**.</span><span class="sxs-lookup"><span data-stu-id="10829-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="10829-124">Adicione as seguintes declarações de `#include` :</span><span class="sxs-lookup"><span data-stu-id="10829-124">Add the following `#include` statements:</span></span>
   
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

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="10829-125">Chamar a função remote\_monitoring\_run</span><span class="sxs-lookup"><span data-stu-id="10829-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="10829-126">Em um editor de texto, abra o arquivo **remote_monitoring.h**.</span><span class="sxs-lookup"><span data-stu-id="10829-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="10829-127">Adicione os códigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="10829-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="10829-128">Em um editor de texto, abra o arquivo **main.c** .</span><span class="sxs-lookup"><span data-stu-id="10829-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="10829-129">Adicione os códigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="10829-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="10829-130">Compile e execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="10829-130">Build and run the application</span></span>
<span data-ttu-id="10829-131">As etapas a seguir descrevem como usar *CMake* para compilar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="10829-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="10829-132">Em um editor de texto, abra o arquivo **CMakeLists.txt** na pasta **remote_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="10829-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="10829-133">Adicione as seguintes instruções para definir como criar o aplicativo cliente:</span><span class="sxs-lookup"><span data-stu-id="10829-133">Add the following instructions to define how to build your client application:</span></span>
   
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
1. <span data-ttu-id="10829-134">Na pasta **remote_monitoring**, crie uma pasta para armazenar os arquivos *make* que CMake gera e execute os comandos **cmake** e **make** como se segue:</span><span class="sxs-lookup"><span data-stu-id="10829-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="10829-135">Execute o aplicativo cliente e envie telemetria ao Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="10829-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

