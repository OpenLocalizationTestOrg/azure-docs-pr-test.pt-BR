---
title: Conectar um dispositivo usando C no Windows | Microsoft Docs
description: "Descreve como conectar um dispositivo à solução pré-configurada de monitoramento remoto do Azure IoT Suite usando um aplicativo escrito em C em execução no Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="fb981-103">Conectar seu dispositivo à solução pré-configurada de monitoramento remoto (Windows)</span><span class="sxs-lookup"><span data-stu-id="fb981-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="fb981-104">Criar um exemplo de solução C no Windows</span><span class="sxs-lookup"><span data-stu-id="fb981-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="fb981-105">As etapas a seguir mostram como criar um aplicativo cliente que se comunica com a solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="fb981-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="fb981-106">Esse aplicativo é escrito em C e compilado e executado no Windows.</span><span class="sxs-lookup"><span data-stu-id="fb981-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="fb981-107">Crie um projeto inicial no Visual Studio 2015 ou Visual Studio 2017 e adicione os pacotes NuGet de cliente do dispositivo Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="fb981-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="fb981-108">No Visual Studio, crie um aplicativo de console C usando o modelo **Aplicativo do Console Win32** do Visual C++.</span><span class="sxs-lookup"><span data-stu-id="fb981-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="fb981-109">Dê o nome de **RMDevice**ao projeto.</span><span class="sxs-lookup"><span data-stu-id="fb981-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="fb981-110">Na página **Configurações de Aplicativos** no **Assistente do Aplicativo Win32**, verifique se **Aplicativo do Console** está selecionado e desmarque **Cabeçalho pré-compilado** e **Verificações do Security Development Lifecycle (SDL)**.</span><span class="sxs-lookup"><span data-stu-id="fb981-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="fb981-111">No **Gerenciador de Soluções**, exclua os arquivos stdafx.h, targetver.h e stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="fb981-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="fb981-112">No **Gerenciador de Soluções**, renomeie o arquivo RMDevice.cpp para RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="fb981-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="fb981-113">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **RMDevice** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fb981-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="fb981-114">Clique em **Procurar**, para encontrar e instalar os seguintes pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="fb981-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="fb981-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="fb981-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="fb981-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="fb981-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="fb981-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="fb981-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="fb981-118">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **RMDevice** e clique em **Propriedades** para abrir a caixa de diálogo **Páginas de Propriedade**.</span><span class="sxs-lookup"><span data-stu-id="fb981-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="fb981-119">Para obter detalhes, confira [Configurando as propriedades do projeto no Visual C++][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="fb981-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="fb981-120">Clique na pasta **Vinculador** e clique na página de propriedade **Entrada**.</span><span class="sxs-lookup"><span data-stu-id="fb981-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="fb981-121">Adicione **crypt32.lib** à propriedade **Dependências Adicionais**.</span><span class="sxs-lookup"><span data-stu-id="fb981-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="fb981-122">Clique em **OK** e **OK** novamente para salvar os valores da propriedade do projeto.</span><span class="sxs-lookup"><span data-stu-id="fb981-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="fb981-123">Adicione a biblioteca Parson JSON ao projeto **RMDevice** e adicione as instruções `#include` necessárias:</span><span class="sxs-lookup"><span data-stu-id="fb981-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="fb981-124">Em uma pasta adequada no computador, clone o repositório Parson GitHub usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="fb981-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="fb981-125">Copie os arquivos parson.h e parson.c da cópia local do repositório Parson para a pasta **RMDevice** do projeto.</span><span class="sxs-lookup"><span data-stu-id="fb981-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="fb981-126">No Visual Studio, clique com o botão direito do mouse no projeto **RMDevice**, clique em **Adicionar** e em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="fb981-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="fb981-127">Na caixa de diálogo **Adicionar Item Existente**, selecione os arquivos parson.h e parson.c na pasta do projeto **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="fb981-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="fb981-128">Em seguida, clique em **Adicionar** para adicionar esses dois arquivos ao projeto.</span><span class="sxs-lookup"><span data-stu-id="fb981-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="fb981-129">No Visual Studio, abra o arquivo RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="fb981-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="fb981-130">Substitua as instruções `#include` existentes pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="fb981-130">Replace the existing `#include` statements with the following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="fb981-131">Agora você pode verificar se o projeto tem as dependências corretas configuradas compilando-o.</span><span class="sxs-lookup"><span data-stu-id="fb981-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="fb981-132">Criar e executar a amostra</span><span class="sxs-lookup"><span data-stu-id="fb981-132">Build and run the sample</span></span>

<span data-ttu-id="fb981-133">Adicione código para invocar a função **remote\_monitoring\_run** e compile e execute o aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fb981-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="fb981-134">Substitua a função **main** pelo seguinte código para invocar a função **remote\_monitoring\_run**:</span><span class="sxs-lookup"><span data-stu-id="fb981-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="fb981-135">Clique em **Compilar** e em **Compilar Solução** para compilar o aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fb981-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="fb981-136">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **RMDevice**, clique em **Depurar** e em **Iniciar nova instância** para executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="fb981-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="fb981-137">O console exibe mensagens quando o aplicativo envia a telemetria de exemplo para a solução pré-configurada, recebe os valores de propriedade desejados definidos no painel de solução e responde aos métodos invocados por meio do painel de solução.</span><span class="sxs-lookup"><span data-stu-id="fb981-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
