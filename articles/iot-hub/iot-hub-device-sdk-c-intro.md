---
title: dispositivo SDK do Azure IoT aaaThe para C | Microsoft Docs
description: "Introdução ao dispositivo do hello IoT do Azure SDK para C e saiba como toocreate aplicativos de dispositivos que se comunicam com um hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="6fa82-103">SDK do dispositivo IoT do Azure para C</span><span class="sxs-lookup"><span data-stu-id="6fa82-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="6fa82-104">Olá **dispositivo IoT do Azure SDK** é um conjunto de bibliotecas projetou o processo de saudação do toosimplify de envio de mensagens tooand recebendo mensagens de saudação **Azure IoT Hub** serviço.</span><span class="sxs-lookup"><span data-stu-id="6fa82-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="6fa82-105">Há diferentes variações de saudação SDK, cada um direcionado para uma plataforma específica, mas este artigo descreve Olá **dispositivo IoT do Azure SDK para C**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="6fa82-106">dispositivo SDK do Azure IoT Olá para C é gravado em ANSI C (C99) toomaximize portabilidade.</span><span class="sxs-lookup"><span data-stu-id="6fa82-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="6fa82-107">Este recurso torna Olá bibliotecas adequado toooperate em várias plataformas e dispositivos, especialmente onde minimizando o disco e volume de memória é uma prioridade.</span><span class="sxs-lookup"><span data-stu-id="6fa82-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="6fa82-108">Há uma ampla variedade de plataformas na qual Olá SDK foi testado (consulte Olá [Azure Certified para catálogo de dispositivo IoT](https://catalog.azureiotsuite.com/) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="6fa82-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="6fa82-109">Embora este artigo inclui instruções passo a passo do código de exemplo em execução na plataforma do Windows hello, código de saudação descrito neste artigo é idêntico em intervalo de saudação de plataformas com suporte.</span><span class="sxs-lookup"><span data-stu-id="6fa82-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="6fa82-110">Este artigo apresenta toohello arquitetura do dispositivo do hello IoT do Azure SDK para C. Ele demonstra como enviar dados tooIoT Hub tooinitialize biblioteca de dispositivo Olá e receber mensagens dela.</span><span class="sxs-lookup"><span data-stu-id="6fa82-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="6fa82-111">informações de saudação neste artigo devem ser suficiente tooget iniciado usando Olá SDK, mas também fornece ponteiros tooadditional informações sobre as bibliotecas de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="6fa82-112">Arquitetura do SDK</span><span class="sxs-lookup"><span data-stu-id="6fa82-112">SDK architecture</span></span>

<span data-ttu-id="6fa82-113">Você pode encontrar hello [ **dispositivo IoT do Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositório e exibir os detalhes de saudação API no hello [referência da API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="6fa82-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="6fa82-114">Olá a versão mais recente das bibliotecas de saudação pode ser encontrada Olá **mestre** ramificação do repositório de saudação:</span><span class="sxs-lookup"><span data-stu-id="6fa82-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="6fa82-115">Olá implementação básica do hello SDK está em Olá **hub IOT\_cliente** pasta que contém a implementação de saudação da camada de API mais baixa Olá no hello SDK: Olá **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6fa82-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="6fa82-116">Olá **IoTHubClient** biblioteca contém APIs implementando bruto de mensagens para enviar mensagens tooIoT Hub e receber mensagens de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="6fa82-117">Ao usar essa biblioteca, você será o responsável por implementar a serialização de mensagens, mas outros detalhes de comunicação com o Hub IoT serão tratados para você.</span><span class="sxs-lookup"><span data-stu-id="6fa82-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="6fa82-118">Olá **serializador** pasta contém exemplos que mostram como dados tooserialize antes de enviar tooAzure Hub IoT usando Olá biblioteca de cliente e funções auxiliares.</span><span class="sxs-lookup"><span data-stu-id="6fa82-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="6fa82-119">uso de saudação do serializador Olá não é obrigatório e é fornecido como uma conveniência.</span><span class="sxs-lookup"><span data-stu-id="6fa82-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="6fa82-120">Olá toouse **serializador** biblioteca, você define um modelo que especifica dados toosend tooIoT Hub e hello mensagens de saudação esperado tooreceive dele.</span><span class="sxs-lookup"><span data-stu-id="6fa82-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="6fa82-121">Após a definição de modelo hello, Olá SDK fornece uma superfície de API que permite que você tooeasily trabalham com o dispositivo para nuvem e mensagens de nuvem para dispositivo sem se preocupar Olá detalhes de serialização.</span><span class="sxs-lookup"><span data-stu-id="6fa82-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="6fa82-122">biblioteca de saudação depende de outras bibliotecas de código-fonte aberto que implementam o transporte usando protocolos como MQTT e AMQP.</span><span class="sxs-lookup"><span data-stu-id="6fa82-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="6fa82-123">Olá **IoTHubClient** biblioteca depende de outras bibliotecas de código-fonte aberto:</span><span class="sxs-lookup"><span data-stu-id="6fa82-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="6fa82-124">Olá [C Azure compartilhado utilitário](https://github.com/Azure/azure-c-shared-utility) library, que fornece a funcionalidade comum para as tarefas básicas (como cadeias de caracteres, manipulação de lista e e/s) necessária em vários SDKs de C relacionadas ao Azure.</span><span class="sxs-lookup"><span data-stu-id="6fa82-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="6fa82-125">Olá [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) biblioteca, que é uma implementação de cliente do AMQP otimizado para dispositivos de recurso restringido.</span><span class="sxs-lookup"><span data-stu-id="6fa82-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="6fa82-126">Olá [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) biblioteca, que é uma biblioteca de finalidade geral implementando Olá MQTT protocolo e otimizado para dispositivos de recurso restringido.</span><span class="sxs-lookup"><span data-stu-id="6fa82-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="6fa82-127">Uso dessas bibliotecas é mais fácil toounderstand examinando o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="6fa82-128">Olá seções a seguir orientam você durante vários aplicativos de exemplo hello que estão incluídos no SDK do hello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="6fa82-129">Este passo a passo deve fornecer uma boa sinta-se para Olá diversos recursos das camadas de arquitetura de saudação de hello SDK e uma saudação de toohow Introdução APIs funcionam.</span><span class="sxs-lookup"><span data-stu-id="6fa82-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="6fa82-130">Antes de executar os exemplos de saudação</span><span class="sxs-lookup"><span data-stu-id="6fa82-130">Before you run hello samples</span></span>

<span data-ttu-id="6fa82-131">Antes de executar os exemplos de saudação no dispositivo do hello IoT do Azure SDK para C, você deve [criar uma instância de serviço de IoT Hub de hello](iot-hub-create-through-portal.md) na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fa82-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="6fa82-132">Em seguida, conclua Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fa82-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="6fa82-133">Preparar seu ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="6fa82-133">Prepare your development environment</span></span>
* <span data-ttu-id="6fa82-134">Obtenha as credenciais do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="6fa82-135">Preparar seu ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="6fa82-135">Prepare your development environment</span></span>

<span data-ttu-id="6fa82-136">Os pacotes são fornecidos para plataformas comuns (como NuGet para Windows ou apt_get para Debian e Ubuntu) e exemplos de saudação usam esses pacotes, quando disponível.</span><span class="sxs-lookup"><span data-stu-id="6fa82-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="6fa82-137">Em alguns casos, você precisa toocompile Olá SDK para ou em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="6fa82-138">Se você precisar toocompile Olá SDK, consulte [preparar seu ambiente de desenvolvimento](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) no repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="6fa82-139">código de aplicativo de exemplo de hello tooobtain, baixar uma cópia da saudação SDK do GitHub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="6fa82-140">Obter sua cópia da fonte de saudação do hello **mestre** ramificação da saudação [repositório GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="6fa82-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="6fa82-141">Obter credenciais de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="6fa82-141">Obtain hello device credentials</span></span>

<span data-ttu-id="6fa82-142">Agora que você tem o código-fonte exemplo hello, Olá próxima coisa toodo é tooget um conjunto de credenciais do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="6fa82-143">Para um dispositivo toobe capaz de tooaccess um hub IoT, primeiro você deve adicionar Olá dispositivo toohello registro de identidade de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="6fa82-144">Quando você adiciona seu dispositivo, você pode obter um conjunto de credenciais de dispositivo necessários para o hub de IoT Olá dispositivo toobe capaz de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="6fa82-145">aplicativos de exemplo Hello discutidos na próxima seção, Olá esperam essas credenciais na forma de saudação de um **cadeia de caracteres de conexão de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="6fa82-146">Há várias toohelp de ferramentas de software livre gerenciar seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6fa82-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="6fa82-147">Um aplicativo do Windows chamado [Gerenciador de Dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="6fa82-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="6fa82-148">Uma ferramenta CLI de plataforma cruzada Node.js chamada [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="6fa82-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="6fa82-149">Este tutorial usa Olá gráfica *explorer dispositivo* ferramenta.</span><span class="sxs-lookup"><span data-stu-id="6fa82-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="6fa82-150">Você também pode usar o hello *Gerenciador de Hub IOT* ferramenta se você preferir toouse uma ferramenta CLI.</span><span class="sxs-lookup"><span data-stu-id="6fa82-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="6fa82-151">ferramenta de Gerenciador de dispositivo Olá usa hello Azure IoT serviço bibliotecas tooperform várias funções no IoT Hub, incluindo a adição de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6fa82-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="6fa82-152">Se você usar Olá dispositivo explorer ferramenta tooadd um dispositivo, você obtém uma cadeia de caracteres de conexão para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="6fa82-153">Você precisa de aplicativos de exemplo essa conexão cadeia de caracteres toorun hello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="6fa82-154">Se você não estiver familiarizado com a ferramenta de Gerenciador de dispositivo hello, Olá procedimento a seguir descreve como toouse-tooadd um dispositivo e obter uma cadeia de caracteres de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="6fa82-155">ferramenta de Gerenciador de dispositivo do tooinstall hello, consulte [como toouse Olá Gerenciador de dispositivo para dispositivos de IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="6fa82-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="6fa82-156">Quando você executar o programa de saudação, você verá essa interface:</span><span class="sxs-lookup"><span data-stu-id="6fa82-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="6fa82-157">Insira seu **cadeia de caracteres de Conexão de Hub IoT** no hello primeiro campo e clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="6fa82-158">Esta etapa configura a ferramenta de saudação para que ele possa se comunicar com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="6fa82-159">Quando Olá cadeia de caracteres de conexão de IoT Hub é configurado, clique em Olá **gerenciamento** guia:</span><span class="sxs-lookup"><span data-stu-id="6fa82-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="6fa82-160">Essa guia é onde você gerencia dispositivos Olá registrados em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6fa82-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="6fa82-161">Crie um dispositivo clicando Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="6fa82-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="6fa82-162">Um diálogo é exibido com um conjunto de chaves pré-populadas (primárias e secundárias).</span><span class="sxs-lookup"><span data-stu-id="6fa82-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="6fa82-163">Insira uma **ID de dispositivo** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="6fa82-164">Quando o dispositivo de saudação é criado, Olá dispositivos listam atualizações com todos os dispositivos de saudação registrado, incluindo Olá que aquele que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="6fa82-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="6fa82-165">Se você clicar com o botão direito do mouse no novo dispositivo, este menu será exibido:</span><span class="sxs-lookup"><span data-stu-id="6fa82-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="6fa82-166">Se você escolher **copiar a cadeia de caracteres de conexão para o dispositivo selecionado**, cadeia de caracteres de conexão de dispositivo Olá é toohello copiado na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="6fa82-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="6fa82-167">Manter uma cópia de cadeia de caracteres de conexão de dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="6fa82-168">É necessário ao executar aplicativos de exemplo hello descritos Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="6fa82-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="6fa82-169">Quando tiver concluído as etapas de saudação acima, você está pronto toostart executando algum código.</span><span class="sxs-lookup"><span data-stu-id="6fa82-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="6fa82-170">Os dois exemplos de tem uma constante na parte superior de Olá Olá principal do arquivo de origem que permite que você tooenter uma cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="6fa82-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="6fa82-171">Olá, por exemplo, a linha correspondente da saudação **hub IOT\_cliente\_exemplo\_mqtt** aplicativo aparece da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="6fa82-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="6fa82-172">Use a biblioteca de IoTHubClient Olá</span><span class="sxs-lookup"><span data-stu-id="6fa82-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="6fa82-173">Dentro de saudação **hub IOT\_cliente** pasta Olá [iot do azure-c sdk](https://github.com/azure/azure-iot-sdk-c) repositório, há um **exemplos** pasta que contém um aplicativo chamado **hub IOT\_cliente\_exemplo\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="6fa82-174">versão do Windows Hello de saudação **hub IOT\_cliente\_exemplo\_mqtt** aplicativo inclui Olá após a solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6fa82-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="6fa82-175">Se você abrir este projeto no Visual Studio de 2017, aceite Olá prompts tooretarget Olá toohello mais recente versão do projeto.</span><span class="sxs-lookup"><span data-stu-id="6fa82-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="6fa82-176">Essa solução contém um único projeto.</span><span class="sxs-lookup"><span data-stu-id="6fa82-176">This solution contains a single project.</span></span> <span data-ttu-id="6fa82-177">Há quatro pacotes NuGet instalados na solução:</span><span class="sxs-lookup"><span data-stu-id="6fa82-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="6fa82-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="6fa82-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="6fa82-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="6fa82-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="6fa82-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="6fa82-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="6fa82-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="6fa82-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="6fa82-182">Você sempre precisa Olá **Microsoft.Azure.C.SharedUtility** pacote quando você estiver trabalhando com hello SDK.</span><span class="sxs-lookup"><span data-stu-id="6fa82-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="6fa82-183">Este exemplo usa o protocolo MQTT de hello, portanto você deve incluir Olá **Microsoft.Azure.umqtt** e **Microsoft.Azure.IoTHub.MqttTransport** pacotes (há pacotes equivalentes para AMQP e HTTP ).</span><span class="sxs-lookup"><span data-stu-id="6fa82-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="6fa82-184">Como exemplo hello usa Olá **IoTHubClient** biblioteca, você também deve incluir Olá **Microsoft.Azure.IoTHub.IoTHubClient** pacote em sua solução.</span><span class="sxs-lookup"><span data-stu-id="6fa82-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="6fa82-185">Você pode encontrar a implementação Olá para o aplicativo de exemplo hello no hello **hub IOT\_cliente\_exemplo\_mqtt.c** arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="6fa82-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="6fa82-186">Olá, etapas a seguir usam esta toowalk do aplicativo de exemplo você durante o que é necessário Olá toouse **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6fa82-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="6fa82-187">Inicializar a biblioteca de saudação</span><span class="sxs-lookup"><span data-stu-id="6fa82-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="6fa82-188">Antes de começar a trabalhar com bibliotecas de saudação, talvez seja necessário tooperform alguns plataforma específica.</span><span class="sxs-lookup"><span data-stu-id="6fa82-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="6fa82-189">Por exemplo, se você planeja toouse AMQP Linux, você deverá inicializar biblioteca OpenSSL de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="6fa82-190">Olá amostras Olá [repositório GitHub](https://github.com/Azure/azure-iot-sdk-c) chamar a função de utilitário hello **plataforma\_init** quando Olá cliente inicia e chamar hello **plataforma\_deinit**  função antes de sair.</span><span class="sxs-lookup"><span data-stu-id="6fa82-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="6fa82-191">Essas funções são declaradas no arquivo de cabeçalho platform.h hello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="6fa82-192">Examine as definições de saudação dessas funções para sua plataforma de destino no hello [repositório](https://github.com/Azure/azure-iot-sdk-c) toodetermine se precisar tooinclude qualquer código de inicialização específico da plataforma no seu cliente.</span><span class="sxs-lookup"><span data-stu-id="6fa82-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="6fa82-193">toostart trabalhando com bibliotecas hello, primeiro alocar um identificador de cliente de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="6fa82-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="6fa82-194">Você passar uma cópia da cadeia de conexão do dispositivo Olá que você obteve da função de toothis hello dispositivo explorer ferramenta.</span><span class="sxs-lookup"><span data-stu-id="6fa82-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="6fa82-195">Você também pode designar Olá toouse de protocolo de comunicação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="6fa82-196">Este exemplo usa MQTT, mas AMQP e HTTP também são opções.</span><span class="sxs-lookup"><span data-stu-id="6fa82-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="6fa82-197">Quando você tem uma opção válida **hub IOT\_cliente\_tratar**, você pode iniciar uma chamada hello APIs toosend e receber mensagens tooand de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="6fa82-198">Enviar mensagens</span><span class="sxs-lookup"><span data-stu-id="6fa82-198">Send messages</span></span>

<span data-ttu-id="6fa82-199">aplicativo de exemplo Hello configura um hub IoT do loop toosend mensagens tooyour.</span><span class="sxs-lookup"><span data-stu-id="6fa82-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="6fa82-200">saudação de trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fa82-200">hello following snippet:</span></span>

- <span data-ttu-id="6fa82-201">Cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="6fa82-201">Creates a message.</span></span>
- <span data-ttu-id="6fa82-202">Adiciona uma mensagem de toohello de propriedade.</span><span class="sxs-lookup"><span data-stu-id="6fa82-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="6fa82-203">Envia uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="6fa82-203">Sends a message.</span></span>

<span data-ttu-id="6fa82-204">Em primeiro lugar, crie uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="6fa82-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="6fa82-205">Toda vez que você enviar uma mensagem, você pode especificar uma função de retorno de chamada de tooa de referência que é invocada quando dados saudação são enviados.</span><span class="sxs-lookup"><span data-stu-id="6fa82-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="6fa82-206">Neste exemplo, é chamada de função de retorno de chamada hello **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="6fa82-207">saudação de trecho de código a seguir mostra essa função de retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="6fa82-207">hello following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="6fa82-208">Observe Olá chamada toohello **IoTHubMessage\_destruir** funcionar quando você terminar com a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="6fa82-209">Essa função libera os recursos de saudação alocados ao criar mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="6fa82-210">Receber mensagens</span><span class="sxs-lookup"><span data-stu-id="6fa82-210">Receive messages</span></span>

<span data-ttu-id="6fa82-211">O recebimento de uma mensagem é uma operação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="6fa82-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="6fa82-212">Primeiro, é registrar Olá tooinvoke de retorno de chamada quando o dispositivo Olá recebe uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="6fa82-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="6fa82-213">Olá último parâmetro é um toowhatever de ponteiro nulo desejado.</span><span class="sxs-lookup"><span data-stu-id="6fa82-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="6fa82-214">No exemplo hello, é um número inteiro tooan de ponteiro, mas pode ser um ponteiro tooa a estrutura de dados mais complexa.</span><span class="sxs-lookup"><span data-stu-id="6fa82-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="6fa82-215">Este parâmetro permite Olá toooperate de função de retorno de chamada no estado compartilhado com chamador Olá dessa função.</span><span class="sxs-lookup"><span data-stu-id="6fa82-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="6fa82-216">Quando o dispositivo Olá recebe uma mensagem, hello função de retorno de chamada registrado é invocada.</span><span class="sxs-lookup"><span data-stu-id="6fa82-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="6fa82-217">Essa função de retorno de chamada recupera:</span><span class="sxs-lookup"><span data-stu-id="6fa82-217">This callback function retrieves:</span></span>

* <span data-ttu-id="6fa82-218">id de mensagem de saudação e id de correlação da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="6fa82-219">conteúdo da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-219">hello message content.</span></span>
* <span data-ttu-id="6fa82-220">Todas as propriedades personalizadas da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-220">Any custom properties from hello message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="6fa82-221">Saudação de uso **IoTHubMessage\_GetByteArray** mensagem de saudação do função tooretrieve, que neste exemplo é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6fa82-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="6fa82-222">Não inicializar a biblioteca de saudação</span><span class="sxs-lookup"><span data-stu-id="6fa82-222">Uninitialize hello library</span></span>

<span data-ttu-id="6fa82-223">Quando você terminar de enviar eventos e receber mensagens, você pode não inicializar Olá IoT biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6fa82-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="6fa82-224">toodo assim, emita Olá chamada de função a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fa82-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="6fa82-225">Essa chamada libera recursos Olá anteriormente alocados pelo Olá **IoTHubClient\_CreateFromConnectionString** função.</span><span class="sxs-lookup"><span data-stu-id="6fa82-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="6fa82-226">Como você pode ver, é fácil toosend e receber mensagens de saudação **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6fa82-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="6fa82-227">biblioteca Hello trata os detalhes de saudação de se comunicar com o IoT Hub, incluindo qual protocolo toouse (da perspectiva de saudação do desenvolvedor hello, essa é uma opção de configuração simples).</span><span class="sxs-lookup"><span data-stu-id="6fa82-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="6fa82-228">Olá **IoTHubClient** biblioteca também fornece um controle preciso sobre como dados de saudação tooserialize o dispositivo envia tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="6fa82-229">Em alguns casos, esse nível de controle é uma vantagem, mas em outros é um detalhe de implementação que você não deseja toobe preocupada com.</span><span class="sxs-lookup"><span data-stu-id="6fa82-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="6fa82-230">Se esse for o caso de Olá, você pode considerar o uso Olá **serializador** biblioteca, o que é descrita na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="6fa82-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="6fa82-231">Usar a biblioteca de serializador Olá</span><span class="sxs-lookup"><span data-stu-id="6fa82-231">Use hello serializer library</span></span>

<span data-ttu-id="6fa82-232">Olá conceitualmente **serializador** biblioteca fica na parte superior Olá **IoTHubClient** biblioteca no hello SDK.</span><span class="sxs-lookup"><span data-stu-id="6fa82-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="6fa82-233">Ele usa Olá **IoTHubClient** biblioteca para Olá subjacente a comunicação com o IoT Hub, mas ele adiciona recursos de modelagem que remove a carga de saudação de lidar com a serialização da mensagem de desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="6fa82-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="6fa82-234">O funcionamento dessa biblioteca é mais bem demonstrado por um exemplo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="6fa82-235">Olá interna **serializador** pasta Olá [repositório do azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), é um **exemplos** pasta que contém um aplicativo chamado **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="6fa82-236">versão do Windows Hello deste exemplo inclui Olá após a solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6fa82-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="6fa82-237">Se você abrir este projeto no Visual Studio de 2017, aceite Olá prompts tooretarget Olá toohello mais recente versão do projeto.</span><span class="sxs-lookup"><span data-stu-id="6fa82-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="6fa82-238">Como com o exemplo anterior de hello, este inclui vários pacotes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="6fa82-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="6fa82-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="6fa82-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="6fa82-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="6fa82-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="6fa82-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="6fa82-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="6fa82-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="6fa82-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="6fa82-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="6fa82-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="6fa82-244">Você viu a maioria desses pacotes no exemplo anterior de saudação, mas **Microsoft.Azure.IoTHub.Serializer** é novo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="6fa82-245">Este pacote é necessário quando você usar o hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6fa82-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="6fa82-246">Você pode encontrar a implementação de saudação do aplicativo de exemplo hello no hello **simplesample\_mqtt.c** arquivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="6fa82-247">Olá seções a seguir orientam você durante partes-chave Olá deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="6fa82-248">Inicializar a biblioteca de saudação</span><span class="sxs-lookup"><span data-stu-id="6fa82-248">Initialize hello library</span></span>

<span data-ttu-id="6fa82-249">toostart trabalhando com hello **serializador** biblioteca, chamada hello inicialização APIs:</span><span class="sxs-lookup"><span data-stu-id="6fa82-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="6fa82-250">Olá chamada toohello **serializador\_init** função é uma única chamada e inicializa Olá biblioteca subjacente.</span><span class="sxs-lookup"><span data-stu-id="6fa82-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="6fa82-251">Em seguida, você pode chamar hello **IoTHubClient\_LL\_CreateFromConnectionString** função, que é Olá a mesma API como Olá **IoTHubClient** exemplo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="6fa82-252">Essa chamada define a cadeia de caracteres de conexão do dispositivo (essa chamada também é onde você escolher o protocolo de saudação desejado toouse).</span><span class="sxs-lookup"><span data-stu-id="6fa82-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="6fa82-253">Este exemplo usa MQTT como transporte hello, mas pode usar AMQP ou HTTP.</span><span class="sxs-lookup"><span data-stu-id="6fa82-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="6fa82-254">Finalmente, chame Olá **criar\_modelo\_instância** função.</span><span class="sxs-lookup"><span data-stu-id="6fa82-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="6fa82-255">**WeatherStation** é o namespace de saudação do modelo de saudação e **ContosoAnemometer** é nome de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="6fa82-256">Depois de criar a instância de modelo hello, você pode usá-lo toostart enviando e recebendo mensagens.</span><span class="sxs-lookup"><span data-stu-id="6fa82-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="6fa82-257">No entanto, é importante toounderstand é que um modelo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="6fa82-258">Definir modelo Olá</span><span class="sxs-lookup"><span data-stu-id="6fa82-258">Define hello model</span></span>

<span data-ttu-id="6fa82-259">Um modelo no hello **serializador** biblioteca define as mensagens de saudação seu dispositivo pode enviar tooIoT mensagens de Hub e hello, chamadas *ações* em Olá linguagem, que pode receber de modelagem.</span><span class="sxs-lookup"><span data-stu-id="6fa82-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="6fa82-260">Definir um modelo usando um conjunto de macros C como Olá **simplesample\_mqtt** aplicativo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="6fa82-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="6fa82-261">Olá **começar\_NAMESPACE** e **final\_NAMESPACE** ambas as macros levar Olá namespace de modelo hello como um argumento.</span><span class="sxs-lookup"><span data-stu-id="6fa82-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="6fa82-262">Espera-se que qualquer coisa entre essas macros é a definição de saudação do seu modelo ou modelos e estruturas de dados de Olá Olá modelos usam.</span><span class="sxs-lookup"><span data-stu-id="6fa82-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="6fa82-263">Neste exemplo, há um único modelo chamado **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="6fa82-264">Esse modelo define duas partes de dados que o dispositivo pode enviar tooIoT Hub: **DeviceId** e **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="6fa82-265">Ele também define três ações (mensagens) que o dispositivo pode receber: **TurnFanOn**, **TurnFanOff** e **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="6fa82-266">Cada elemento de dados tem um tipo, e cada ação tem um nome (e, opcionalmente, um conjunto de parâmetros).</span><span class="sxs-lookup"><span data-stu-id="6fa82-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="6fa82-267">dados saudação e as ações definidas no modelo de saudação definem uma superfície de API que você pode usar toosend mensagens tooIoT Hub e responder toomessages enviados toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="6fa82-268">O uso desse modelo é compreendido melhor por meio de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="6fa82-269">Enviar mensagens</span><span class="sxs-lookup"><span data-stu-id="6fa82-269">Send messages</span></span>

<span data-ttu-id="6fa82-270">modelo de Olá define dados Olá pode enviar tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6fa82-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="6fa82-271">Neste exemplo, isso significa que uma saudação dois itens de dados definidos usando Olá **WITH_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="6fa82-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="6fa82-272">Há várias etapas e necessário toosend **DeviceId** e **WindSpeed** hub de IoT tooan valores.</span><span class="sxs-lookup"><span data-stu-id="6fa82-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="6fa82-273">Olá é primeiro tooset Olá dados toosend:</span><span class="sxs-lookup"><span data-stu-id="6fa82-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="6fa82-274">Olá modelo definido anteriormente permite que você os valores hello tooset definindo membros de um **struct**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="6fa82-275">Em seguida, serialize a mensagem de saudação desejado toosend:</span><span class="sxs-lookup"><span data-stu-id="6fa82-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="6fa82-276">Esse código serializa o buffer de dispositivo para nuvem tooa hello (referenciado por **destino**).</span><span class="sxs-lookup"><span data-stu-id="6fa82-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="6fa82-277">código de Hello, em seguida, invoca Olá **sendMessage** função tooIoT de mensagem de saudação toosend Hub:</span><span class="sxs-lookup"><span data-stu-id="6fa82-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="6fa82-278">Olá segundo parâmetro toolast de **IoTHubClient\_LL\_SendEventAsync** é uma função de retorno de chamada de tooa de referência que é chamada quando dados saudação são enviados com êxito.</span><span class="sxs-lookup"><span data-stu-id="6fa82-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="6fa82-279">Aqui está a função de retorno de chamada hello no exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="6fa82-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="6fa82-280">Olá segundo parâmetro é um contexto de toouser ponteiro; Olá ponteiro mesmo passado muito**IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="6fa82-281">Nesse caso, o contexto de saudação é um contador simple, mas pode ser qualquer coisa que você deseja.</span><span class="sxs-lookup"><span data-stu-id="6fa82-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="6fa82-282">Isso é tudo que há mensagens de dispositivo para nuvem toosending.</span><span class="sxs-lookup"><span data-stu-id="6fa82-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="6fa82-283">Olá somente coisa toocover é como tooreceive mensagens.</span><span class="sxs-lookup"><span data-stu-id="6fa82-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="6fa82-284">Receber mensagens</span><span class="sxs-lookup"><span data-stu-id="6fa82-284">Receive messages</span></span>

<span data-ttu-id="6fa82-285">Receber uma mensagem de funcionamento da mesma forma toohello mensagens funcionam no hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6fa82-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="6fa82-286">Primeiramente, você registra uma função de retorno de chamada de mensagem:</span><span class="sxs-lookup"><span data-stu-id="6fa82-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="6fa82-287">Em seguida, você escrever a função de retorno de chamada de saudação que é invocada quando uma mensagem é recebida:</span><span class="sxs-lookup"><span data-stu-id="6fa82-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="6fa82-288">Esse código é clichê - ele tem hello mesmo para qualquer solução.</span><span class="sxs-lookup"><span data-stu-id="6fa82-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="6fa82-289">Esta função recebe a mensagem de saudação e cuida de roteamento a função apropriada toohello por meio da chamada de saudação muito**EXECUTE\_comando**.</span><span class="sxs-lookup"><span data-stu-id="6fa82-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="6fa82-290">função Hello chamada neste ponto depende da definição Olá das ações de saudação em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="6fa82-291">Quando você define uma ação em seu modelo, será necessário tooimplement uma função que é chamada quando o dispositivo recebe a mensagem de saudação do correspondente.</span><span class="sxs-lookup"><span data-stu-id="6fa82-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="6fa82-292">Por exemplo, se o seu modelo definir esta ação:</span><span class="sxs-lookup"><span data-stu-id="6fa82-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="6fa82-293">Defina uma função com esta assinatura:</span><span class="sxs-lookup"><span data-stu-id="6fa82-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="6fa82-294">Observe como o nome de saudação do função hello corresponde o nome de Olá da ação Olá no modelo de saudação e que Olá da função hello correspondem Olá parâmetros especificados para a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa82-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="6fa82-295">Olá primeiro parâmetro é sempre necessário e contém uma instância de toohello ponteiro do seu modelo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="6fa82-296">Quando o dispositivo Olá recebe uma mensagem que corresponde a essa assinatura, função correspondente Olá é chamada.</span><span class="sxs-lookup"><span data-stu-id="6fa82-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="6fa82-297">Portanto, além de ter tooinclude Olá boilerplate código de **IoTHubMessage**, recebendo mensagens é apenas uma questão de definir uma função simples para cada ação definida no modelo.</span><span class="sxs-lookup"><span data-stu-id="6fa82-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="6fa82-298">Não inicializar a biblioteca de saudação</span><span class="sxs-lookup"><span data-stu-id="6fa82-298">Uninitialize hello library</span></span>

<span data-ttu-id="6fa82-299">Quando você terminar de envio de dados e receber mensagens, você pode não inicializar Olá IoT biblioteca:</span><span class="sxs-lookup"><span data-stu-id="6fa82-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="6fa82-300">Cada uma dessas três funções de acordo com hello três funções de inicialização descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6fa82-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="6fa82-301">Chamar essas APIs garante a liberação dos recursos alocados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6fa82-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fa82-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fa82-302">Next Steps</span></span>

<span data-ttu-id="6fa82-303">Este artigo coberto Noções básicas de saudação do uso de bibliotecas de saudação em Olá **dispositivo IoT do Azure SDK para C**. Ele acompanha suficiente toounderstand informações que está incluído na Olá SDK, sua arquitetura e como tooget começaram a funcionar com hello exemplos do Windows.</span><span class="sxs-lookup"><span data-stu-id="6fa82-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="6fa82-304">artigo Avançar Olá continua descrição Olá Olá SDK explicando [mais informações sobre a biblioteca de IoTHubClient Olá](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="6fa82-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="6fa82-305">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá [SDKs do Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="6fa82-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="6fa82-306">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="6fa82-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6fa82-307">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6fa82-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
