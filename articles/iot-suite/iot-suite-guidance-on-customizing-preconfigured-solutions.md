---
title: "Personalizando soluções pré-configuradas | Microsoft Docs"
description: "Fornece orientação sobre como personalizar as soluções pré-configuradas do Pacote IoT do Azure."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="e3c6a-103">Personalizar uma solução pré-configurada</span><span class="sxs-lookup"><span data-stu-id="e3c6a-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="e3c6a-104">As soluções pré-configuradas fornecidas com o Pacote IoT do Azure demonstram os serviços no pacote trabalhando juntos para fornecer uma solução de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="e3c6a-105">Do ponto de partida, há diversos lugares nos quais você pode estender e personalizar a solução para cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="e3c6a-106">As seções a seguir descrevem esses pontos comuns de personalização.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="e3c6a-107">Localizar o código-fonte</span><span class="sxs-lookup"><span data-stu-id="e3c6a-107">Find the source code</span></span>

<span data-ttu-id="e3c6a-108">O código-fonte para a solução pré-configurada está disponível no GitHub nos seguintes repositórios:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="e3c6a-109">Monitoramento remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="e3c6a-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="e3c6a-110">Manutenção preditiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="e3c6a-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="e3c6a-111">Fábrica conectada: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="e3c6a-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="e3c6a-112">O código-fonte para as soluções pré-configuradas é fornecido para demonstrar os padrões e as práticas usadas para implementar a funcionalidade de ponta a ponta de uma solução IoT usando o Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="e3c6a-113">Você pode encontrar mais informações sobre como compilar e implantar as soluções em repositórios GitHub.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="e3c6a-114">Alterar as regras pré-configuradas</span><span class="sxs-lookup"><span data-stu-id="e3c6a-114">Change the preconfigured rules</span></span>

<span data-ttu-id="e3c6a-115">A solução de monitoramento remoto inclui três trabalhos do [Stream Analytics do Azure](https://azure.microsoft.com/services/stream-analytics/) para lidar com informações do dispositivo, telemetria e lógica de regras na solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="e3c6a-116">Os três trabalhos de Stream Analytics e sua sintaxe são descritos em detalhes na [Passo a passo da solução pré-configurada de monitoramento remoto](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e3c6a-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="e3c6a-117">Você pode editar esses trabalhos diretamente para alterar a lógica ou adicionar lógica específica para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="e3c6a-118">Você pode encontrar os trabalhos do Stream Analytics da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="e3c6a-119">Vá para o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3c6a-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e3c6a-120">Navegue até o grupo de recursos com o mesmo nome da sua solução IoT.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="e3c6a-121">Selecione o trabalho de Stream Analytics do Azure que você deseja modificar.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="e3c6a-122">Interrompa o trabalho selecionando **Parar**no conjunto de comandos.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="e3c6a-123">Edite as entradas, consulta e saídas.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="e3c6a-124">Uma modificação simples é alterar a consulta para o trabalho **Regras** para usar um **"<"**, em vez de um **">"**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="e3c6a-125">O portal de solução ainda mostra **">"** quando a regra for editada, mas percebe como o comportamento é invertido devido à alteração no trabalho subjacente.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="e3c6a-126">Iniciar o trabalho</span><span class="sxs-lookup"><span data-stu-id="e3c6a-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="e3c6a-127">O painel de monitoramento remoto depende de dados específicos, por isso, alterar os trabalhos pode fazer com que o painel falhe.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="e3c6a-128">Adicionar suas próprias regras</span><span class="sxs-lookup"><span data-stu-id="e3c6a-128">Add your own rules</span></span>

<span data-ttu-id="e3c6a-129">Além de alterar os trabalhos de Stream Analytics do Azure, você pode usar o portal do Azure para adicionar novos trabalhos ou adicionar novas consultas para trabalhos existentes.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="e3c6a-130">Personalizar dispositivos</span><span class="sxs-lookup"><span data-stu-id="e3c6a-130">Customize devices</span></span>

<span data-ttu-id="e3c6a-131">Uma das atividades mais comuns de extensão é o trabalho com dispositivos específicos ao seu cenário.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="e3c6a-132">Há vários métodos para trabalhar com dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-132">There are several methods for working with devices.</span></span> <span data-ttu-id="e3c6a-133">Esses métodos incluem alterar um dispositivo simulado de acordo com seu cenário ou usar o [SDK de Dispositivo IoT][IoT Device SDK] para conectar seu dispositivo físico à solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="e3c6a-134">Para obter um guia passo a passo para adicionar dispositivos, consulte o artigo [Dispositivos de Conexão do Iot Suite](iot-suite-connecting-devices.md) e o [Exemplo de SDK para o monitoramento remoto em C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="e3c6a-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="e3c6a-135">Este exemplo é projetado para trabalhar com a solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="e3c6a-136">Criar seu próprio dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="e3c6a-136">Create your own simulated device</span></span>

<span data-ttu-id="e3c6a-137">Incluído no [código-fonte da solução de monitoramento remota](https://github.com/Azure/azure-iot-remote-monitoring), é um simulador de .NET.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="e3c6a-138">Esse simulador é provisionado como parte da solução e pode ser alterado para enviar metadados diferentes, telemetria, e responder a comandos e métodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="e3c6a-139">O simulador pré-configurado na solução pré-configurada de monitoramento remoto simula um dispositivo mais frio que emite a temperatura e a telemetria da umidade.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="e3c6a-140">Você pode modificar o simulador no projeto [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) quando tiver dividido o repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="e3c6a-141">Locais disponíveis para dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="e3c6a-141">Available locations for simulated devices</span></span>

<span data-ttu-id="e3c6a-142">O conjunto padrão de locais fica em Seattle/Redmond, Washington, Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="e3c6a-143">É possível alterar esses locais em [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="e3c6a-144">Adicionar um manipulador de atualização da propriedade desejada ao simulador</span><span class="sxs-lookup"><span data-stu-id="e3c6a-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="e3c6a-145">Você pode definir um valor para uma propriedade desejada para um dispositivo no portal de solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="e3c6a-146">É responsabilidade do dispositivo lidar com a solicitação de alteração da propriedade quando o dispositivo recupera o valor da propriedade desejada.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="e3c6a-147">Para adicionar suporte para uma alteração de valor da propriedade por meio de uma propriedade desejada, você precisa adicionar um manipulador ao simulador.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="e3c6a-148">O simulador contém manipuladores para as propriedades **SetPointTemp** e **TelemetryInterval** que você pode atualizar definindo os valores desejados no portal da solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="e3c6a-149">O exemplo a seguir mostra o manipulador para a propriedade desejada **SetPointTemp** na classe **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="e3c6a-150">Esse método atualiza a temperatura do ponto de telemetria, em seguida, informa a alteração ao Hub IoT definindo uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="e3c6a-151">Você pode adicionar seus próprios manipuladores para suas próprias propriedades seguindo o padrão no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="e3c6a-152">Você também deve associar a propriedade desejada ao manipulador como mostrado no exemplo a seguir do construtor **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="e3c6a-153">Observe que **SetPointTempPropertyName** é uma constante definida como "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="e3c6a-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="e3c6a-154">Adicionar o suporte de um novo método ao simulador</span><span class="sxs-lookup"><span data-stu-id="e3c6a-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="e3c6a-155">Você pode personalizar o simulador para adicionar o suporte de um novo [método (método direto)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="e3c6a-156">Há duas etapas principais necessárias:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-156">There are two key steps required:</span></span>

- <span data-ttu-id="e3c6a-157">O simulador deve notificar o Hub IoT na solução pré-configurada com os detalhes do método.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="e3c6a-158">O simulador deve incluir o código para lidar com a chamada do método quando você o chama no painel **Detalhes do dispositivo** no Gerenciador de Soluções ou por meio de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="e3c6a-159">A solução pré-configurada de monitoramento remoto usa as *propriedades relatadas* para enviar os detalhes dos métodos com suporte para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="e3c6a-160">O back-end de solução mantém uma lista de todos os métodos suportados por cada dispositivo junto com um histórico de chamadas do método.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="e3c6a-161">Você pode exibir essas informações sobre os dispositivos e chamar os métodos no portal de solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="e3c6a-162">Para notificar o Hub IoT que um dispositivo oferece suporte a um método, o dispositivo deve adicionar os detalhes do método ao nó **SupportedMethods** nas propriedades relatadas:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="e3c6a-163">A assinatura do método tem o seguinte formato: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="e3c6a-164">Por exemplo, para especificar o método **InitiateFirmwareUpdate** que espera um parâmetro da cadeia de caracteres denominado **FwPackageURI**, use a assinatura do método a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="e3c6a-165">Para obter uma lista dos tipos de parâmetro com suporte, consulte a classe **CommandTypes** no projeto de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="e3c6a-166">Para excluir um método, defina a assinatura do método para `null` nas propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="e3c6a-167">O back-end de solução só atualiza as informações sobre os métodos com suporte quando ele recebe uma mensagem de *informações do dispositivo* a partir do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="e3c6a-168">O exemplo de código a seguir da classe **SampleDeviceFactory** no projeto Common mostra como adicionar um método à lista de **SupportedMethods** nas propriedades relatadas enviadas pelo dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="e3c6a-169">Esse trecho de código adiciona os detalhes do método **InitiateFirmwareUpdate**, incluindo o texto a exibir no portal de solução e os detalhes dos parâmetros do método necessários.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="e3c6a-170">O simulador envia as propriedades relatadas, incluindo a lista de métodos com suporte, ao Hub IoT quando o simulador inicia.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="e3c6a-171">Adicione um manipulador ao código do simulador para cada método com suporte.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="e3c6a-172">Você pode ver os manipuladores existentes na classe **CoolerDevice** no projeto Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="e3c6a-173">O exemplo a seguir mostra o manipulador do método **InitiateFirmwareUpdate**:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="e3c6a-174">Os nomes do manipulador do método devem começar com `On` seguido do nome do método.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="e3c6a-175">O parâmetro **methodRequest** contém todos os parâmetros passados com a chamada do método a partir do back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="e3c6a-176">O valor de retorno deve ser do tipo **Task&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="e3c6a-177">O método utilitário **BuildMethodResponse** ajuda a criar o valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="e3c6a-178">No manipulador do método, você pode:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="e3c6a-179">iniciar uma tarefa assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="e3c6a-180">recuperar as propriedades desejadas no *dispositivo gêmeo* no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="e3c6a-181">atualizar uma única propriedade relatada usando o método **SetReportedPropertyAsync** na classe **CoolerDevice**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="e3c6a-182">atualizar várias propriedades relatadas criando uma instância **TwinCollection** e chamar o método **Transport.UpdateReportedPropertiesAsync**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="e3c6a-183">O exemplo anterior de atualização do firmware executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="e3c6a-184">verifica se o dispositivo é capaz de aceitar a solicitação de atualização do firmware.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="e3c6a-185">inicia de forma assíncrona a operação de atualização do firmware e redefine a telemetria quando a operação é concluída.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="e3c6a-186">retorna imediatamente a mensagem "FirmwareUpdate aceito" para indicar que a solicitação foi aceita pelo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="e3c6a-187">Compilar e usar seu próprio dispositivo (físico)</span><span class="sxs-lookup"><span data-stu-id="e3c6a-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="e3c6a-188">Os [SDKs do Azure IoT](https://github.com/Azure/azure-iot-sdks) fornecem bibliotecas para conectar a vários tipos de dispositivo (linguagens e sistemas operacionais) em soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="e3c6a-189">Modificar os limites do painel</span><span class="sxs-lookup"><span data-stu-id="e3c6a-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="e3c6a-190">Número de dispositivos exibida na lista suspensa do painel</span><span class="sxs-lookup"><span data-stu-id="e3c6a-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="e3c6a-191">O padrão é 200.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-191">The default is 200.</span></span> <span data-ttu-id="e3c6a-192">É possível alterar esse número em [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="e3c6a-193">Número de marcações a serem exibidas no controle do Mapa do Bing</span><span class="sxs-lookup"><span data-stu-id="e3c6a-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="e3c6a-194">O padrão é 200.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-194">The default is 200.</span></span> <span data-ttu-id="e3c6a-195">É possível alterar esse número em [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="e3c6a-196">Período do gráfico de telemetria</span><span class="sxs-lookup"><span data-stu-id="e3c6a-196">Time period of telemetry graph</span></span>

<span data-ttu-id="e3c6a-197">O padrão é 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-197">The default is 10 minutes.</span></span> <span data-ttu-id="e3c6a-198">É possível alterar esse valor em [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="e3c6a-199">Configurar manualmente as funções do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e3c6a-199">Manually set up application roles</span></span>

<span data-ttu-id="e3c6a-200">O procedimento a seguir descreve como adicionar as funções de aplicativo **Admin** e **ReadOnly** a uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="e3c6a-201">Observe que as soluções pré-configuradas provisionadas no site azureiotsuite.com já incluem as funções **Admin** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="e3c6a-202">Membros da função **ReadOnly** podem ver o painel e a lista de dispositivos, mas não têm permissão para adicionar dispositivos, alterar os atributos do dispositivo ou enviar comandos.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="e3c6a-203">Membros da função **Admin** têm acesso total a todos os recursos da solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="e3c6a-204">Vá para o [Portal Clássico do Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="e3c6a-205">Selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="e3c6a-206">Clique no nome do locatário AAD que você usou ao provisionar a solução.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="e3c6a-207">Clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-207">Click **Applications**.</span></span>
5. <span data-ttu-id="e3c6a-208">Clique no nome do aplicativo que corresponda ao nome da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="e3c6a-209">Se você não vir seu aplicativo na lista, selecione **Aplicativos que minha empresa** possui na lista suspensa **Mostrar** e clique na marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="e3c6a-210">Na parte inferior da página, clique em **Gerenciar Manifesto** e em **Baixar Manifesto**.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="e3c6a-211">Este procedimento baixa um arquivo .json para seu computador local.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="e3c6a-212">Abra esse arquivo para edição em um editor de texto de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="e3c6a-213">Na terceira linha do arquivo .json, você pode ver:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="e3c6a-214">Substitua essa linha pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="e3c6a-215">Salve o arquivo .json atualizado (você pode substituir o arquivo existente).</span><span class="sxs-lookup"><span data-stu-id="e3c6a-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="e3c6a-216">No Portal Clássico do Azure, na parte inferior da página, selecione **Gerenciar Manifesto** e, em seguida, **Carregar Manifesto** para carregar o arquivo .json salvo na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="e3c6a-217">Agora você adicionou as funções **Admin** e **ReadOnly** ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="e3c6a-218">Para atribuir uma dessas funções a um usuário no diretório, consulte [Permissões no site azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="e3c6a-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="e3c6a-219">Comentários</span><span class="sxs-lookup"><span data-stu-id="e3c6a-219">Feedback</span></span>

<span data-ttu-id="e3c6a-220">Há alguma personalização que você gostaria que fosse abordada neste documento?</span><span class="sxs-lookup"><span data-stu-id="e3c6a-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="e3c6a-221">Adicione sugestões de recursos ao [User Voice](https://feedback.azure.com/forums/321918-azure-iot)ou faça comentários sobre este artigo.</span><span class="sxs-lookup"><span data-stu-id="e3c6a-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3c6a-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3c6a-222">Next steps</span></span>

<span data-ttu-id="e3c6a-223">Para saber mais sobre as opções para personalizar as soluções pré-configuradas, confira:</span><span class="sxs-lookup"><span data-stu-id="e3c6a-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="e3c6a-224">[Conectar um Aplicativo lógico à solução pré-configurada de monitoramento remoto do Azure IoT Suite][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="e3c6a-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="e3c6a-225">[Usar telemetria dinâmica com a solução pré-configurada de monitoramento remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="e3c6a-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="e3c6a-226">[Metadados de informações de dispositivo na solução pré-configurada de monitoramento remoto][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="e3c6a-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="e3c6a-227">[Personalizar como a solução de fábrica conectada exibe dados de seus servidores de agente do usuário OPC][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="e3c6a-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md