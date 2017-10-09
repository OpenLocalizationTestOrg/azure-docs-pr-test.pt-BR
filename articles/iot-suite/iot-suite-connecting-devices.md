---
title: aaaConnect um dispositivo usando o C no Windows | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurados de solução de monitoramento remota usando um aplicativo escrito em C em execução no Windows."
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
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="1c75c-103">Conecte-se a toohello do dispositivo remoto monitoramento solução pré-configurada (Windows)</span><span class="sxs-lookup"><span data-stu-id="1c75c-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="1c75c-104">Criar um exemplo de solução C no Windows</span><span class="sxs-lookup"><span data-stu-id="1c75c-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="1c75c-105">Olá etapas a seguir mostra como toocreate um aplicativo cliente que se comunica com o monitoramento remoto Olá pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="1c75c-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="1c75c-106">Esse aplicativo é escrito em C e compilado e executado no Windows.</span><span class="sxs-lookup"><span data-stu-id="1c75c-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="1c75c-107">Criar um projeto de starter no Visual Studio 2015 ou 2017 do Visual Studio e adicione pacotes NuGet do hello Hub IoT dispositivo cliente:</span><span class="sxs-lookup"><span data-stu-id="1c75c-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="1c75c-108">No Visual Studio, crie um aplicativo de console C usando Olá Visual C++ **aplicativo do Console Win32** modelo.</span><span class="sxs-lookup"><span data-stu-id="1c75c-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="1c75c-109">Projeto de saudação do nome **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="1c75c-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="1c75c-110">Em Olá **configurações do aplicativo** página Olá **Assistente de aplicativo Win32**, certifique-se de que **aplicativo de Console** está selecionado e desmarque **pré-compilado cabeçalho** e **Security Development Lifecycle (SDL) verifica**.</span><span class="sxs-lookup"><span data-stu-id="1c75c-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="1c75c-111">Em **Solution Explorer**, excluir arquivos de saudação Stdafx. h, targetver.h e Stdafx.</span><span class="sxs-lookup"><span data-stu-id="1c75c-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="1c75c-112">Em **Solution Explorer**, renomear Olá arquivo RMDevice.cpp tooRMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="1c75c-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="1c75c-113">Em **Solution Explorer**, clique duas vezes em Olá **RMDevice** do projeto e, em seguida, clique em **gerenciar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1c75c-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="1c75c-114">Clique em **procurar**, em seguida, procurar e instalar Olá pacotes do NuGet a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c75c-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="1c75c-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="1c75c-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="1c75c-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="1c75c-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="1c75c-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="1c75c-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="1c75c-118">Em **Solution Explorer**, com o botão direito em Olá **RMDevice** do projeto e, em seguida, clique em **propriedades** do projeto de saudação tooopen **páginas de propriedade**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c75c-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="1c75c-119">Para obter detalhes, confira [Configurando as propriedades do projeto no Visual C++][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="1c75c-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="1c75c-120">Clique Olá **vinculador** pasta, em seguida, clique em Olá **entrada** página de propriedades.</span><span class="sxs-lookup"><span data-stu-id="1c75c-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="1c75c-121">Adicionar **crypt32.lib** toohello **dependências adicionais** propriedade.</span><span class="sxs-lookup"><span data-stu-id="1c75c-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="1c75c-122">Clique em **Okey** e **Okey** novamente toosave Olá projeto valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="1c75c-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="1c75c-123">Adicionar Olá JSON Parson biblioteca toohello **RMDevice** do projeto e adicionar Olá necessário `#include` instruções:</span><span class="sxs-lookup"><span data-stu-id="1c75c-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="1c75c-124">Em uma pasta adequada no seu computador, clone repositório do GitHub Parson hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c75c-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="1c75c-125">Copie os arquivos de parson.h e parson.c Olá da cópia local de saudação do hello Parson repositório tooyour **RMDevice** pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="1c75c-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="1c75c-126">No Visual Studio, clique com botão direito Olá **RMDevice** de projeto, clique em **adicionar**e, em seguida, clique em **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="1c75c-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="1c75c-127">Em Olá **Add Existing Item** caixa de diálogo, parson.h e parson.c arquivos em Olá Olá selecione **RMDevice** pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="1c75c-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="1c75c-128">Em seguida, clique em **adicionar** tooadd esses dois arquivos projeto de tooyour.</span><span class="sxs-lookup"><span data-stu-id="1c75c-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="1c75c-129">No Visual Studio, abra o arquivo de RMDevice.c de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c75c-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="1c75c-130">Substituir saudação `#include` instruções com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c75c-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="1c75c-131">Agora você pode verificar que o projeto tem dependências corretas de saudação configuradas pelo compilá-lo.</span><span class="sxs-lookup"><span data-stu-id="1c75c-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="1c75c-132">Compilar e executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="1c75c-132">Build and run hello sample</span></span>

<span data-ttu-id="1c75c-133">Adicionar saudação do código tooinvoke **remoto\_monitoramento\_executar** de função e, em seguida, compilar e executar o aplicativo de dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="1c75c-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="1c75c-134">Substituir saudação **principal** função com o seguinte Olá tooinvoke de código **remoto\_monitoramento\_executar** função:</span><span class="sxs-lookup"><span data-stu-id="1c75c-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="1c75c-135">Clique em **criar** e **compilar solução** aplicativo de dispositivo toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="1c75c-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="1c75c-136">Em **Solution Explorer**, Olá com o botão direito **RMDevice** de projeto, clique em **depurar**e, em seguida, clique em **iniciar nova instância** toorun Olá exemplo.</span><span class="sxs-lookup"><span data-stu-id="1c75c-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="1c75c-137">console de saudação exibe mensagens como hello aplicativo envia exemplo telemetria toohello pré-configurado solução, recebe os valores de propriedade desejados definidos no painel de solução hello e responde toomethods invocada a partir do painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c75c-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
