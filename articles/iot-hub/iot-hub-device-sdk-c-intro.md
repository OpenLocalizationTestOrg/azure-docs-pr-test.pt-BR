---
title: O SDK do dispositivo IoT do Azure para C | Microsoft Docs
description: Como usar o SDK do dispositivo IoT do Azure para C e saiba como criar aplicativos de dispositivos que se comunicam com um Hub IoT.
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
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="400a3-103">SDK do dispositivo IoT do Azure para C</span><span class="sxs-lookup"><span data-stu-id="400a3-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="400a3-104">O **SDK do dispositivo IoT do Azure** é um conjunto de bibliotecas projetadas para simplificar o processo de envio e o recebimento de mensagens do serviço **Hub IoT do Azure**.</span><span class="sxs-lookup"><span data-stu-id="400a3-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="400a3-105">Existem diferentes variações do SDK, cada uma visando uma plataforma específica, mas este artigo descreve o **SDK do dispositivo IoT do Azure para C**.</span><span class="sxs-lookup"><span data-stu-id="400a3-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="400a3-106">O SDK do dispositivo IoT do Azure para C foi escrito em ANSI (C99) para maximizar a portabilidade.</span><span class="sxs-lookup"><span data-stu-id="400a3-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="400a3-107">Esse recurso torna as bibliotecas bastante adequado para a operação em vários dispositivos e plataformas, especialmente quando a minimização do volume de disco e de memória for uma prioridade.</span><span class="sxs-lookup"><span data-stu-id="400a3-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="400a3-108">Há uma ampla variedade de plataformas nas quais o SDK foi testado (confira o [Catálogo de dispositivos certificados pelo Azure para IoT](https://catalog.azureiotsuite.com/) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="400a3-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="400a3-109">Embora este artigo inclua explicações de exemplo de código em execução na plataforma Windows, o código descrito neste artigo é idêntico entre as várias plataformas com suporte.</span><span class="sxs-lookup"><span data-stu-id="400a3-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="400a3-110">Este artigo apresenta a arquitetura do SDK do dispositivo IoT do Azure para C. Ele demonstra como inicializar a biblioteca de dispositivo, enviar dados para o Hub IoT e receber mensagens dele.</span><span class="sxs-lookup"><span data-stu-id="400a3-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="400a3-111">As informações neste artigo devem ser suficientes para começar a usar o SDK, mas também há indicações para se saber mais sobre as bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="400a3-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="400a3-112">Arquitetura do SDK</span><span class="sxs-lookup"><span data-stu-id="400a3-112">SDK architecture</span></span>

<span data-ttu-id="400a3-113">Você pode encontrar o [**SDK do dispositivo IoT do Azure para C**](https://github.com/Azure/azure-iot-sdk-c) no repositório GitHub e exibir os detalhes da API [na referência da API do C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="400a3-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="400a3-114">A versão mais recente das bibliotecas pode ser encontrada na ramificação **mestre** deste repositório:</span><span class="sxs-lookup"><span data-stu-id="400a3-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="400a3-115">A implementação principal do SDK fica na pasta **iothub\_client**, que contém a implementação da camada de API mais baixa no SDK: a biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="400a3-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="400a3-116">A biblioteca **IoTHubClient** contém APIs que implementam mensagens brutas para enviar mensagens para o Hub IoT, além de receber mensagens dele.</span><span class="sxs-lookup"><span data-stu-id="400a3-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="400a3-117">Ao usar essa biblioteca, você será o responsável por implementar a serialização de mensagens, mas outros detalhes de comunicação com o Hub IoT serão tratados para você.</span><span class="sxs-lookup"><span data-stu-id="400a3-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="400a3-118">A pasta **serializador** contém funções auxiliares e exemplos que mostram como serializar os dados antes de enviar para o Hub IoT do Azure usando a biblioteca de cliente.</span><span class="sxs-lookup"><span data-stu-id="400a3-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="400a3-119">O uso do serializador não é obrigatório e só é fornecido como uma conveniência.</span><span class="sxs-lookup"><span data-stu-id="400a3-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="400a3-120">Para usar a biblioteca **serializer**, defina um modelo que especifica os dados para envio ao Hub IoT e as mensagens que você espera receber dele.</span><span class="sxs-lookup"><span data-stu-id="400a3-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="400a3-121">Depois que o modelo é definido, o SDK fornece uma superfície de API que permite a você trabalhar facilmente com mensagens de dispositivo para nuvem e de nuvem para dispositivo sem se preocupar com os detalhes de serialização.</span><span class="sxs-lookup"><span data-stu-id="400a3-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="400a3-122">A biblioteca depende de outras bibliotecas de software livre que implementam o transporte usando protocolos como MQTT e AMQP.</span><span class="sxs-lookup"><span data-stu-id="400a3-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="400a3-123">A biblioteca **IoTHubClient** depende de outras bibliotecas de software livre:</span><span class="sxs-lookup"><span data-stu-id="400a3-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="400a3-124">A biblioteca de [utilitários compartilhados do Azure C](https://github.com/Azure/azure-c-shared-utility), que fornece funcionalidades comuns para tarefas básicas (como cadeia de caracteres, manipulação de listas e E/S) necessárias entre vários SDKs para C relacionados ao Azure.</span><span class="sxs-lookup"><span data-stu-id="400a3-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="400a3-125">A biblioteca [uAMQP do Azure](https://github.com/Azure/azure-uamqp-c) é uma implementação do lado do cliente do AMQP otimizada para dispositivos com restrição de recursos.</span><span class="sxs-lookup"><span data-stu-id="400a3-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="400a3-126">A biblioteca [uMQTT do Azure](https://github.com/Azure/azure-umqtt-c) , que é uma biblioteca de finalidade geral, com o protocolo MQTT implementado e otimizada para dispositivos com restrição de recursos.</span><span class="sxs-lookup"><span data-stu-id="400a3-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="400a3-127">O uso dessas bibliotecas fica mais fácil de entender examinando exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="400a3-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="400a3-128">As seções a seguir explicam alguns exemplos de aplicativo incluídos no SDK.</span><span class="sxs-lookup"><span data-stu-id="400a3-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="400a3-129">O passo a passo deve dar uma boa ideia dos vários recursos das camadas de arquitetura do SDK, bem como uma introdução ao funcionamento da API.</span><span class="sxs-lookup"><span data-stu-id="400a3-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="400a3-130">Antes de executar os exemplos</span><span class="sxs-lookup"><span data-stu-id="400a3-130">Before you run the samples</span></span>

<span data-ttu-id="400a3-131">Antes de executar os exemplos no SDK do dispositivo IoT do Azure para C, você deverá [criar uma instância do serviço Hub IoT](iot-hub-create-through-portal.md) em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="400a3-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="400a3-132">Em seguida, conclua as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="400a3-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="400a3-133">Preparar seu ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="400a3-133">Prepare your development environment</span></span>
* <span data-ttu-id="400a3-134">Obtenha as credenciais do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="400a3-135">Preparar seu ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="400a3-135">Prepare your development environment</span></span>

<span data-ttu-id="400a3-136">Os pacotes são fornecidos para plataformas comuns (como o NuGet para Windows ou apt_get para Debian e Ubuntu) e os exemplos usam esses pacotes, quando disponíveis.</span><span class="sxs-lookup"><span data-stu-id="400a3-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="400a3-137">Em alguns casos, você precisa compilar o SDK para ou em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="400a3-138">Se você precisa compilar o SDK, consulte [Preparar o ambiente de desenvolvimento](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) no repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="400a3-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="400a3-139">Para obter o código do aplicativo de exemplo, baixe uma cópia do SDK do GitHub.</span><span class="sxs-lookup"><span data-stu-id="400a3-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="400a3-140">Obtenha uma cópia da origem na ramificação **master** do [repositório GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="400a3-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="400a3-141">Obter credenciais do dispositivo</span><span class="sxs-lookup"><span data-stu-id="400a3-141">Obtain the device credentials</span></span>

<span data-ttu-id="400a3-142">Agora que você tem o código-fonte, a próxima coisa a fazer é obter um conjunto de credenciais do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="400a3-143">Para um dispositivo poder acessar um Hub IoT, primeiro você deverá adicionar o dispositivo ao registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="400a3-144">Quando você adiciona seu dispositivo, obtém um conjunto de credenciais de dispositivo necessário para que ele seja capaz de se conectar ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="400a3-145">Os aplicativos de exemplo abordados na próxima seção esperam essas credenciais na forma de uma **cadeia de conexão de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="400a3-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="400a3-146">Há várias ferramentas de código-fonte aberto para ajudá-lo a gerenciar seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="400a3-147">Um aplicativo do Windows chamado [Gerenciador de Dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="400a3-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="400a3-148">Uma ferramenta CLI de plataforma cruzada Node.js chamada [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="400a3-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="400a3-149">Este tutorial usa a ferramenta gráfica *Gerenciador de Dispositivos*.</span><span class="sxs-lookup"><span data-stu-id="400a3-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="400a3-150">Você também pode usar a ferramenta *iothub-explorer* se preferir usar uma ferramenta CLI.</span><span class="sxs-lookup"><span data-stu-id="400a3-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="400a3-151">A ferramenta Gerenciador de Dispositivos usa as bibliotecas de serviço IoT do Azure para executar várias funções no Hub IoT, incluindo a adição de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="400a3-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="400a3-152">Se você usar a ferramenta Gerenciador de Dispositivos para adicionar um dispositivo, você obterá uma cadeia de conexão para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="400a3-153">Você precisa dessa cadeia de conexão para executar os aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="400a3-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="400a3-154">Caso você não esteja familiarizado com a ferramenta Gerenciador de Dispositivos, o procedimento a seguir descreve como usá-la para adicionar um dispositivo e obter uma cadeia de conexão de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="400a3-155">Para instalar a ferramenta Gerenciador de Dispositivos, consulte [Como usar o Gerenciador de Dispositivos para dispositivos Hub IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="400a3-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="400a3-156">Ao executar o programa, você verá esta interface:</span><span class="sxs-lookup"><span data-stu-id="400a3-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="400a3-157">Insira a **Cadeia de Conexão do Hub IoT** no primeiro campo e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="400a3-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="400a3-158">Essa etapa configura a ferramenta para que ela possa se comunicar com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="400a3-159">Depois que a cadeia de conexão do Hub IoT for configurada, clique na guia **Gerenciamento**:</span><span class="sxs-lookup"><span data-stu-id="400a3-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="400a3-160">Essa guia é o local onde você gerencia os dispositivos registrados no seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="400a3-161">Crie um dispositivo clicando no botão **Criar** .</span><span class="sxs-lookup"><span data-stu-id="400a3-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="400a3-162">Um diálogo é exibido com um conjunto de chaves pré-populadas (primárias e secundárias).</span><span class="sxs-lookup"><span data-stu-id="400a3-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="400a3-163">Insira uma **ID de dispositivo** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="400a3-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="400a3-164">Depois que o dispositivo for criado, a lista Dispositivos será atualizada com todos os dispositivos registrados, incluindo o que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="400a3-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="400a3-165">Se você clicar com o botão direito do mouse no novo dispositivo, este menu será exibido:</span><span class="sxs-lookup"><span data-stu-id="400a3-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="400a3-166">Se você escolher **Copiar cadeia de conexão para o dispositivo selecionado**, a cadeia de conexão do dispositivo será copiada para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="400a3-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="400a3-167">Manter uma cópia da cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="400a3-168">Você precisará dela ao executar os aplicativos de exemplo descritos nas próximas seções.</span><span class="sxs-lookup"><span data-stu-id="400a3-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="400a3-169">Após concluir as etapas acima, você estará pronto para começar a executar códigos.</span><span class="sxs-lookup"><span data-stu-id="400a3-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="400a3-170">Ambos os exemplos têm uma constante na parte superior do arquivo de origem principal que permite inserir uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="400a3-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="400a3-171">Por exemplo, a linha correspondente do **iothub\_client\_sample\_mqtt** aparece da forma a seguir.</span><span class="sxs-lookup"><span data-stu-id="400a3-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="400a3-172">Usar a biblioteca IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="400a3-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="400a3-173">Na pasta **iothub\_client** no repositório [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c), há uma pasta **samples** que contém um aplicativo chamado **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="400a3-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="400a3-174">A versão do Windows do aplicativo **iothub\_client\_sample\_mqtt** inclui a seguinte solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="400a3-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="400a3-175">Se você abrir esse projeto no Visual Studio 2017, aceite os prompts a fim de redirecionar o projeto para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="400a3-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="400a3-176">Essa solução contém um único projeto.</span><span class="sxs-lookup"><span data-stu-id="400a3-176">This solution contains a single project.</span></span> <span data-ttu-id="400a3-177">Há quatro pacotes NuGet instalados na solução:</span><span class="sxs-lookup"><span data-stu-id="400a3-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="400a3-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="400a3-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="400a3-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="400a3-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="400a3-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="400a3-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="400a3-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="400a3-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="400a3-182">Você sempre precisará do pacote **Microsoft.Azure.C.SharedUtility** quando estiver trabalhando com o SDK.</span><span class="sxs-lookup"><span data-stu-id="400a3-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="400a3-183">Este exemplo usa o protocolo MQTT e, portanto, você deve incluir os pacotes **Microsoft.Azure.umqtt** e **Microsoft.Azure.IoTHub.MqttTransport** (há pacotes equivalentes para AMQP e HTTP).</span><span class="sxs-lookup"><span data-stu-id="400a3-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="400a3-184">Como o exemplo usa a biblioteca **IoTHubClient**, você também deverá incluir o pacote **Microsoft.Azure.IoTHub.IoTHubClient** em sua solução.</span><span class="sxs-lookup"><span data-stu-id="400a3-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="400a3-185">Você pode encontrar a implementação do aplicativo de exemplo no arquivo de origem **iothub\_client\_sample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="400a3-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="400a3-186">As etapas a seguir usam esse exemplo de aplicativo para explicar o que é necessário para usar a biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="400a3-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="400a3-187">Inicializar a biblioteca</span><span class="sxs-lookup"><span data-stu-id="400a3-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="400a3-188">Antes de começar a trabalhar com as bibliotecas, talvez seja necessário executar alguma inicialização específica de plataforma.</span><span class="sxs-lookup"><span data-stu-id="400a3-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="400a3-189">Por exemplo, se você planeja usar o AMQP no Linux, você deverá inicializar a biblioteca OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="400a3-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="400a3-190">Os exemplos de [repositório GitHub](https://github.com/Azure/azure-iot-sdk-c) chamam a função de utilitário **platform\_init** quando o cliente inicia, e chamam a função **platform\_deinit** antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="400a3-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="400a3-191">Essas funções são declaradas no arquivo de cabeçalho platform.h.</span><span class="sxs-lookup"><span data-stu-id="400a3-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="400a3-192">Examine as definições dessas funções para sua plataforma de destino no [repositório](https://github.com/Azure/azure-iot-sdk-c) para determinar se é necessário incluir algum código de inicialização específico de plataforma no seu cliente.</span><span class="sxs-lookup"><span data-stu-id="400a3-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="400a3-193">Para começar a trabalhar com as bibliotecas, primeiro aloque um identificador de cliente do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="400a3-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="400a3-194">Passe uma cópia da cadeia de conexão do dispositivo obtido da ferramenta Gerenciador de Dispositivos para essa função.</span><span class="sxs-lookup"><span data-stu-id="400a3-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="400a3-195">Você também pode designar o protocolo de comunicação a ser usado.</span><span class="sxs-lookup"><span data-stu-id="400a3-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="400a3-196">Este exemplo usa MQTT, mas AMQP e HTTP também são opções.</span><span class="sxs-lookup"><span data-stu-id="400a3-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="400a3-197">Quando você tiver um **IOTHUB\_CLIENT\_HANDLE** válido, será possível iniciar a chamada a APIs para enviar e receber mensagens do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="400a3-198">Enviar mensagens</span><span class="sxs-lookup"><span data-stu-id="400a3-198">Send messages</span></span>

<span data-ttu-id="400a3-199">O aplicativo de exemplo configura um loop para enviar mensagens para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="400a3-200">O seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="400a3-200">The following snippet:</span></span>

- <span data-ttu-id="400a3-201">Cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-201">Creates a message.</span></span>
- <span data-ttu-id="400a3-202">Adiciona uma propriedade à mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-202">Adds a property to the message.</span></span>
- <span data-ttu-id="400a3-203">Envia uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-203">Sends a message.</span></span>

<span data-ttu-id="400a3-204">Em primeiro lugar, crie uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="400a3-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="400a3-205">Sempre que você enviar uma mensagem, será possível especificar uma referência a uma função de retorno de chamada que é invocada quando os dados são enviados.</span><span class="sxs-lookup"><span data-stu-id="400a3-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="400a3-206">Neste exemplo, a função de retorno de chamada se chama **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="400a3-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="400a3-207">O trecho abaixo mostra essa função de retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="400a3-207">The following snippet shows this callback function:</span></span>

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

<span data-ttu-id="400a3-208">Observe a chamada à função **IoTHubMessage\_Destroy** quando terminar com a mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="400a3-209">Essa função libera os recursos alocados ao criar a mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="400a3-210">Receber mensagens</span><span class="sxs-lookup"><span data-stu-id="400a3-210">Receive messages</span></span>

<span data-ttu-id="400a3-211">O recebimento de uma mensagem é uma operação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="400a3-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="400a3-212">Primeiro, você registra o retorno de chamada a ser invocado quando o dispositivo recebe uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="400a3-212">First, you register the callback to invoke when the device receives a message:</span></span>

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

<span data-ttu-id="400a3-213">O último parâmetro é um ponteiro nulo para o que você quiser.</span><span class="sxs-lookup"><span data-stu-id="400a3-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="400a3-214">No exemplo, é um ponteiro para um inteiro, mas poderia ser um ponteiro para uma estrutura de dados mais complexa.</span><span class="sxs-lookup"><span data-stu-id="400a3-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="400a3-215">Esse parâmetro permite que a função de retorno de chamada opere em estado compartilhado com o chamador dessa função.</span><span class="sxs-lookup"><span data-stu-id="400a3-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="400a3-216">Quando o dispositivo receber uma mensagem, a função de retorno de chamada registrada será invocada.</span><span class="sxs-lookup"><span data-stu-id="400a3-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="400a3-217">Essa função de retorno de chamada recupera:</span><span class="sxs-lookup"><span data-stu-id="400a3-217">This callback function retrieves:</span></span>

* <span data-ttu-id="400a3-218">A ID da mensagem e a ID de correlação da mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="400a3-219">O conteúdo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-219">The message content.</span></span>
* <span data-ttu-id="400a3-220">Todas as propriedades personalizadas da mensagem.</span><span class="sxs-lookup"><span data-stu-id="400a3-220">Any custom properties from the message.</span></span>

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
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
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

<span data-ttu-id="400a3-221">Use a função **IoTHubMessage\_GetByteArray** para recuperar a mensagem que, neste exemplo, é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="400a3-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="400a3-222">Não inicializar a biblioteca</span><span class="sxs-lookup"><span data-stu-id="400a3-222">Uninitialize the library</span></span>

<span data-ttu-id="400a3-223">Quando acabar de enviar eventos e de receber mensagens, você poderá cancelar a inicialização da biblioteca IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="400a3-224">Para fazer isso, emita a seguinte chamada de função:</span><span class="sxs-lookup"><span data-stu-id="400a3-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="400a3-225">Essa chamada libera os recursos anteriormente alocados pela função **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="400a3-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="400a3-226">Como você pode ver, é fácil enviar e receber mensagens com a biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="400a3-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="400a3-227">A biblioteca lida com os detalhes de comunicação com o Hub IoT, incluindo o protocolo a ser usado (da perspectiva do desenvolvedor, isso é uma opção de configuração simples).</span><span class="sxs-lookup"><span data-stu-id="400a3-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="400a3-228">A biblioteca **IoTHubClient** também fornece controle preciso sobre como serializar os dados que o seu dispositivo envia ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="400a3-229">Em alguns casos, esse nível de controle é uma vantagem, mas em outros, é um detalhe de implementação com que você não quer se preocupar.</span><span class="sxs-lookup"><span data-stu-id="400a3-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="400a3-230">Se for esse o caso, você poderá considerar usar a biblioteca **serializer** , que está descrita na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="400a3-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="400a3-231">Usar a biblioteca do serializador</span><span class="sxs-lookup"><span data-stu-id="400a3-231">Use the serializer library</span></span>

<span data-ttu-id="400a3-232">Conceitualmente, a biblioteca **serializer** fica acima da biblioteca **IoTHubClient** no SDK.</span><span class="sxs-lookup"><span data-stu-id="400a3-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="400a3-233">Ela usa a biblioteca **IoTHubClient** para a comunicação subjacente com o Hub IoT, mas adiciona recursos de modelagem que removem a sobrecarga de lidar com a serialização de mensagens do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="400a3-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="400a3-234">O funcionamento dessa biblioteca é mais bem demonstrado por um exemplo.</span><span class="sxs-lookup"><span data-stu-id="400a3-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="400a3-235">Na pasta **serializer** do [repositório azure-iot-sdk](https://github.com/Azure/azure-iot-sdk-c), há uma pasta **samples** que contém um aplicativo chamado **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="400a3-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="400a3-236">A versão para Windows deste exemplo inclui a seguinte solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="400a3-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="400a3-237">Se você abrir esse projeto no Visual Studio 2017, aceite os prompts a fim de redirecionar o projeto para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="400a3-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="400a3-238">Assim como no exemplo anterior, este inclui vários pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="400a3-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="400a3-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="400a3-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="400a3-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="400a3-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="400a3-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="400a3-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="400a3-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="400a3-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="400a3-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="400a3-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="400a3-244">Você viu a maior parte desses pacotes no exemplo anterior, mas **Microsoft.Azure.IoTHub.Serializer** é novo.</span><span class="sxs-lookup"><span data-stu-id="400a3-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="400a3-245">Este pacote é necessário quando você usa a biblioteca **serializer**.</span><span class="sxs-lookup"><span data-stu-id="400a3-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="400a3-246">A implementação do aplicativo de exemplo pode ser encontrada no arquivo **simplesample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="400a3-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="400a3-247">As seções a seguir explicam as principais partes desse exemplo.</span><span class="sxs-lookup"><span data-stu-id="400a3-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="400a3-248">Inicializar a biblioteca</span><span class="sxs-lookup"><span data-stu-id="400a3-248">Initialize the library</span></span>

<span data-ttu-id="400a3-249">Para começar a trabalhar com a biblioteca **serializer**, chame as APIs de inicialização:</span><span class="sxs-lookup"><span data-stu-id="400a3-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

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

<span data-ttu-id="400a3-250">A chamada à função **serializer\_init** é uma chamada única e inicializa a biblioteca subjacente.</span><span class="sxs-lookup"><span data-stu-id="400a3-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="400a3-251">Então, você chama a função **IoTHubClient\_LL\_CreateFromConnectionString**, que é a mesma API do exemplo **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="400a3-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="400a3-252">Essa chamada define a cadeia de conexão de dispositivo (ela é também onde você escolhe o protocolo que quer usar).</span><span class="sxs-lookup"><span data-stu-id="400a3-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="400a3-253">Este exemplo usa MQTT como transporte, mas pode usar AMQP ou HTTP.</span><span class="sxs-lookup"><span data-stu-id="400a3-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="400a3-254">Por fim, chame a função **CREATE\_MODEL\_INSTANCE**.</span><span class="sxs-lookup"><span data-stu-id="400a3-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="400a3-255">**WeatherStation** é o namespace do modelo e **ContosoAnemometer** é o nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="400a3-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="400a3-256">Depois que a instância do modelo for definida, você poderá usá-lo para começar a enviar e a receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="400a3-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="400a3-257">No entanto, em primeiro lugar, é importante entender o que é um modelo.</span><span class="sxs-lookup"><span data-stu-id="400a3-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="400a3-258">Definir o modelo</span><span class="sxs-lookup"><span data-stu-id="400a3-258">Define the model</span></span>

<span data-ttu-id="400a3-259">Um modelo na biblioteca **serializer** define as mensagens que seu dispositivo pode enviar ao Hub IoT e as mensagens, chamadas de *ações* na linguagem de modelagem, que ele pode receber.</span><span class="sxs-lookup"><span data-stu-id="400a3-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="400a3-260">Defina um modelo usando um conjunto de macros C, como no exemplo de aplicativo **simplesample\_mqtt**:</span><span class="sxs-lookup"><span data-stu-id="400a3-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="400a3-261">As macros **BEGIN\_NAMESPACE** e **END\_NAMESPACE** usam o namespace do modelo como um argumento.</span><span class="sxs-lookup"><span data-stu-id="400a3-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="400a3-262">Espera-se que qualquer coisa entre essas macros seja a definição de seus modelos e as estruturas de dados que os modelos usam.</span><span class="sxs-lookup"><span data-stu-id="400a3-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="400a3-263">Neste exemplo, há um único modelo chamado **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="400a3-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="400a3-264">Esse modelo define dois dados que o dispositivo pode enviar ao Hub IoT: **DeviceId** e **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="400a3-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="400a3-265">Ele também define três ações (mensagens) que o dispositivo pode receber: **TurnFanOn**, **TurnFanOff** e **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="400a3-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="400a3-266">Cada elemento de dados tem um tipo, e cada ação tem um nome (e, opcionalmente, um conjunto de parâmetros).</span><span class="sxs-lookup"><span data-stu-id="400a3-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="400a3-267">Os dados e ações definidos no modelo definem uma superfície de API que você pode usar para enviar mensagens ao Hub IoT, bem como para responder a mensagens enviadas ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="400a3-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="400a3-268">O uso desse modelo é compreendido melhor por meio de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="400a3-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="400a3-269">Enviar mensagens</span><span class="sxs-lookup"><span data-stu-id="400a3-269">Send messages</span></span>

<span data-ttu-id="400a3-270">O modelo define os dados que você pode enviar ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="400a3-271">Neste exemplo, isso significa um dos dois itens de dados definidos usando a macro **WITH_DATA**.</span><span class="sxs-lookup"><span data-stu-id="400a3-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="400a3-272">Há várias etapas necessárias para enviar os valores **DeviceId** e **WindSpeed** para um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="400a3-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="400a3-273">A primeira é definir os dados que deseja enviar:</span><span class="sxs-lookup"><span data-stu-id="400a3-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="400a3-274">O modelo que você definiu anteriormente permite que você defina os valores definindo membros de uma **struct**.</span><span class="sxs-lookup"><span data-stu-id="400a3-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="400a3-275">Em seguida, serialize a mensagem que deseja enviar:</span><span class="sxs-lookup"><span data-stu-id="400a3-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="400a3-276">Esse código serializa o dispositivo-para-nuvem em um buffer (conhecido como **destination**).</span><span class="sxs-lookup"><span data-stu-id="400a3-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="400a3-277">O código chama a função **sendMessage** para enviar a mensagem para o Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="400a3-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="400a3-278">Do segundo ao último parâmetro de **IoTHub\_LL\_ClientSendEventAsync** é uma referência a uma função de retorno de chamada que é chamada quando os dados são enviados com êxito.</span><span class="sxs-lookup"><span data-stu-id="400a3-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="400a3-279">Aqui está a função de retorno de chamada no exemplo:</span><span class="sxs-lookup"><span data-stu-id="400a3-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="400a3-280">O segundo parâmetro é um ponteiro para contexto do usuário, o mesmo ponteiro que passamos para **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="400a3-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="400a3-281">Nesse caso, esse contexto é um contador simples, mas ele pode ser o que você quiser.</span><span class="sxs-lookup"><span data-stu-id="400a3-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="400a3-282">Isso é tudo para enviar mensagens de dispositivo para nuvem.</span><span class="sxs-lookup"><span data-stu-id="400a3-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="400a3-283">Agora nos resta falar sobre o recebimento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="400a3-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="400a3-284">Receber mensagens</span><span class="sxs-lookup"><span data-stu-id="400a3-284">Receive messages</span></span>

<span data-ttu-id="400a3-285">O recebimento de uma mensagem funciona de forma semelhante a como as mensagens funcionam na biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="400a3-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="400a3-286">Primeiramente, você registra uma função de retorno de chamada de mensagem:</span><span class="sxs-lookup"><span data-stu-id="400a3-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="400a3-287">Em seguida, você grava a função de retorno de chamada que é invocada quando uma mensagem é recebida:</span><span class="sxs-lookup"><span data-stu-id="400a3-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="400a3-288">Esse código é clichê, é o mesmo para qualquer solução.</span><span class="sxs-lookup"><span data-stu-id="400a3-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="400a3-289">Essa função recebe a mensagem e cuida de encaminhá-la à função apropriada por meio da chamada a **EXECUTE\_COMMAND**.</span><span class="sxs-lookup"><span data-stu-id="400a3-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="400a3-290">A função chamada nesse ponto depende da definição das ações em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="400a3-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="400a3-291">Ao definir uma ação em seu modelo, você precisa implementar uma função que é chamada quando o dispositivo recebe a mensagem correspondente.</span><span class="sxs-lookup"><span data-stu-id="400a3-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="400a3-292">Por exemplo, se o seu modelo definir esta ação:</span><span class="sxs-lookup"><span data-stu-id="400a3-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="400a3-293">Defina uma função com esta assinatura:</span><span class="sxs-lookup"><span data-stu-id="400a3-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="400a3-294">Observe como o nome da função corresponde ao nome da ação no modelo e que os parâmetros da função correspondem aos parâmetros especificados para a ação.</span><span class="sxs-lookup"><span data-stu-id="400a3-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="400a3-295">O primeiro parâmetro é sempre obrigatório e contém um ponteiro para a instância do seu modelo.</span><span class="sxs-lookup"><span data-stu-id="400a3-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="400a3-296">Quando o dispositivo recebe uma mensagem que corresponde a essa assinatura, a função correspondente é chamada.</span><span class="sxs-lookup"><span data-stu-id="400a3-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="400a3-297">Portanto, além de ter que incluir o código clichê de **IoTHubMessage**, receber mensagens será apenas uma questão de definir uma função simples para cada ação definida no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="400a3-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="400a3-298">Não inicializar a biblioteca</span><span class="sxs-lookup"><span data-stu-id="400a3-298">Uninitialize the library</span></span>

<span data-ttu-id="400a3-299">Quando acabar de enviar dados e de receber mensagens, você poderá cancelar a inicialização da biblioteca IoT:</span><span class="sxs-lookup"><span data-stu-id="400a3-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="400a3-300">Cada uma dessas três funções se alinha às três funções de inicialização descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="400a3-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="400a3-301">Chamar essas APIs garante a liberação dos recursos alocados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="400a3-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="400a3-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="400a3-302">Next Steps</span></span>

<span data-ttu-id="400a3-303">Este artigo abordou os conceitos básicos de como usar as bibliotecas no **SDK do dispositivo IoT do Azure para C**. Ele forneceu informações suficientes para entender o que está incluído no SDK, sua arquitetura e como começar a trabalhar com os exemplos do Windows.</span><span class="sxs-lookup"><span data-stu-id="400a3-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="400a3-304">O próximo artigo continua a descrição do SDK, explicando [mais sobre a biblioteca IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="400a3-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="400a3-305">Para saber mais sobre como desenvolver para o Hub IoT, consulte os [SDKs do Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="400a3-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="400a3-306">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="400a3-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="400a3-307">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="400a3-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
