---
title: "soluções pré-configuradas de aaaCustomizing | Microsoft Docs"
description: "Fornece orientação sobre como o toocustomize hello Azure IoT Suite soluções pré-configuradas."
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
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="d6ec2-103">Personalizar uma solução pré-configurada</span><span class="sxs-lookup"><span data-stu-id="d6ec2-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="d6ec2-104">soluções de saudação pré-configurado fornecidas com hello Azure IoT Suite demonstram serviços Olá Olá suite trabalhar juntos toodeliver uma solução de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="d6ec2-105">Do ponto de partida, há vários locais em que você pode estender e personalizar Olá solução para cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="d6ec2-106">Olá seções a seguir descreve esses pontos comuns de personalização.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="d6ec2-107">Localizar o código-fonte Olá</span><span class="sxs-lookup"><span data-stu-id="d6ec2-107">Find hello source code</span></span>

<span data-ttu-id="d6ec2-108">código-fonte para soluções de saudação pré-configurado Hello está disponível no GitHub no hello repositórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="d6ec2-109">Monitoramento remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="d6ec2-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="d6ec2-110">Manutenção preditiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="d6ec2-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="d6ec2-111">Fábrica conectada: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="d6ec2-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="d6ec2-112">código-fonte Olá para soluções de saudação pré-configurado é fornecido práticas e padrões de saudação toodemonstrate usou a funcionalidade de ponta a ponta de saudação do tooimplement de uma solução de IoT usando Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="d6ec2-113">Você pode encontrar mais informações sobre como toobuild e implantar soluções de saudação em repositórios de GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="d6ec2-114">Altere as regras de saudação pré-configurado</span><span class="sxs-lookup"><span data-stu-id="d6ec2-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="d6ec2-115">Olá solução de monitoramento remota inclui três [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) informações do dispositivo toohandle, telemetria e lógica de regras na solução de saudação de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="d6ec2-116">Olá três fluxo trabalhos de análise e sua sintaxe são descritos em detalhes no hello [monitoramento remoto pré-configurado passo a passo de solução](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d6ec2-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="d6ec2-117">Você pode editar esses trabalhos diretamente tooalter Olá lógica ou adicionar lógica específica tooyour cenário.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="d6ec2-118">Você pode encontrar hello trabalhos do Stream Analytics da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="d6ec2-119">Vá muito[portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6ec2-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6ec2-120">Navegue toohello o grupo de recursos com o mesmo nome como sua solução de IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="d6ec2-121">Selecione hello Azure Stream Analytics trabalho você gostaria que toomodify.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="d6ec2-122">Interromper o trabalho de saudação selecionando **parar** no conjunto de saudação de comandos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="d6ec2-123">Edite entradas hello, consulta e saídas.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="d6ec2-124">Uma simples modificação é toochange consultar Olá Olá **regras** toouse trabalho um **"<"** em vez de um **">"**.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="d6ec2-125">portal de solução Olá ainda mostra **">"** quando você editar uma regra, mas observe como o comportamento de saudação é invertido devido toohello alteração no hello subjacente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="d6ec2-126">Iniciar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="d6ec2-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="d6ec2-127">Painel de monitoramento remoto Olá depende de dados específicos, isso alterar trabalhos Olá pode provocar Olá painel toofail.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="d6ec2-128">Adicionar suas próprias regras</span><span class="sxs-lookup"><span data-stu-id="d6ec2-128">Add your own rules</span></span>

<span data-ttu-id="d6ec2-129">Além disso, Olá toochanging pré-configurado trabalhos do Stream Analytics do Azure, você pode usar novos trabalhos do hello tooadd portal do Azure ou adicionar novos trabalhos de tooexisting de consultas.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="d6ec2-130">Personalizar dispositivos</span><span class="sxs-lookup"><span data-stu-id="d6ec2-130">Customize devices</span></span>

<span data-ttu-id="d6ec2-131">Uma das atividades mais comuns de extensão hello está trabalhando com cenário de tooyour específicos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="d6ec2-132">Há vários métodos para trabalhar com dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-132">There are several methods for working with devices.</span></span> <span data-ttu-id="d6ec2-133">Esses métodos incluem alterando seu cenário de um dispositivo simulado toomatch ou usando Olá [SDK de dispositivo IoT] [ IoT Device SDK] tooconnect sua solução de toohello do dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="d6ec2-134">Para dispositivos de tooadding um guia passo a passo, consulte Olá [dispositivos de conexão do Iot Suite](iot-suite-connecting-devices.md) artigo e hello [C amostra do SDK de monitoramento remoto](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="d6ec2-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="d6ec2-135">Este exemplo é projetado toowork com hello solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="d6ec2-136">Criar seu próprio dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="d6ec2-136">Create your own simulated device</span></span>

<span data-ttu-id="d6ec2-137">Incluído no hello [código fonte da solução de monitoramento remoto](https://github.com/Azure/azure-iot-remote-monitoring), é um simulador de .NET.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="d6ec2-138">Este simulador é hello um provisionado como parte da solução de saudação e você pode alterá-la toosend diferentes metadados, telemetria e responder métodos e comandos toodifferent.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="d6ec2-139">simulador pré-configurado de saudação na solução pré-configurada de monitoramento remoto de saudação simula um dispositivo cooler que emite a telemetria de temperatura e umidade.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="d6ec2-140">Você pode modificar o simulador Olá no hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) quando você bifurcada repositório GitHub de saudação do projeto.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="d6ec2-141">Locais disponíveis para dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="d6ec2-141">Available locations for simulated devices</span></span>

<span data-ttu-id="d6ec2-142">conjunto de locais padrão de saudação está em Seattle/Redmond, Washington, Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="d6ec2-143">É possível alterar esses locais em [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="d6ec2-144">Adicionar um simulador toohello de manipulador de atualização de propriedade desejada</span><span class="sxs-lookup"><span data-stu-id="d6ec2-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="d6ec2-145">Você pode definir um valor para uma propriedade desejada para um dispositivo no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="d6ec2-146">É responsabilidade do hello de solicitação de alteração de propriedade Olá dispositivo toohandle hello quando o dispositivo Olá recupera o valor da propriedade Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="d6ec2-147">suporte de tooadd para uma alteração de valor de propriedade por meio de uma propriedade desejada, você precisa tooadd um simulador de toohello do manipulador.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="d6ec2-148">simulador Olá contém manipuladores para Olá **SetPointTemp** e **TelemetryInterval** desejado de propriedades que você pode atualizar definindo valores no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="d6ec2-149">Olá, exemplo a seguir mostra manipulador Olá Olá **SetPointTemp** desejado propriedade Olá **CoolerDevice** classe:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="d6ec2-150">Este método atualizará o ponto de telemetria Olá temperatura e, em seguida, Olá relatórios alterar tooIoT back Hub definindo uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="d6ec2-151">Você pode adicionar seus próprios manipuladores para suas próprias propriedades pelo seguinte padrão de Olá Olá anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="d6ec2-152">Você também deve vincular o manipulador de toohello de propriedade desejados Olá conforme Olá seguinte exemplo de hello **CoolerDevice** construtor:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="d6ec2-153">Observe que **SetPointTempPropertyName** é uma constante definida como "Config.SetPointTemp".</span><span class="sxs-lookup"><span data-stu-id="d6ec2-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="d6ec2-154">Adicionar suporte para um simulador de toohello novo método</span><span class="sxs-lookup"><span data-stu-id="d6ec2-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="d6ec2-155">Você pode personalizar Olá simulador tooadd suporte para um novo [método (método direto)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="d6ec2-156">Há duas etapas principais necessárias:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-156">There are two key steps required:</span></span>

- <span data-ttu-id="d6ec2-157">simulador Olá deve notificar o hub IoT de saudação na solução Olá pré-configurados com detalhes do método hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="d6ec2-158">simulador Olá deve incluir a chamada de método do código toohandle Olá ao invocá-lo da saudação **detalhes do dispositivo** painel no Gerenciador de soluções hello, ou por meio de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="d6ec2-159">Olá monitoramento remoto pré-configurado solução usa *relatado propriedades* toosend detalhes do hub de tooIoT métodos com suporte.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="d6ec2-160">back-end de solução Olá mantém uma lista de todos os métodos de saudação suportados por cada dispositivo junto com um histórico de invocações do método.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="d6ec2-161">Você pode exibir essas informações sobre dispositivos e chamar métodos no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="d6ec2-162">hub IoT da saudação de toonotify que um dispositivo oferece suporte a um método, dispositivo Olá deve adicionar detalhes da saudação método toohello **SupportedMethods** nó Olá relatado propriedades:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="d6ec2-163">assinatura do método Hello tem Olá formato a seguir: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="d6ec2-164">Por exemplo, toospecify Olá **InitiateFirmwareUpdate** método espera um parâmetro de cadeia de caracteres chamado **FwPackageURI**, use Olá a assinatura do método a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="d6ec2-165">Para obter uma lista dos tipos de parâmetro com suporte, consulte Olá **CommandTypes** classe no projeto de infra-estrutura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="d6ec2-166">toodelete um método, defina a assinatura do método hello muito`null` no hello reportada propriedades.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="d6ec2-167">Olá back-end solução atualiza somente informações sobre os métodos com suporte quando ele recebe um *informações do dispositivo* mensagem do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="d6ec2-168">Olá seguinte exemplo de código da saudação **SampleDeviceFactory** classe Olá comuns de projeto mostra como tooadd uma lista de toohello do método de **SupportedMethods** no hello reportada propriedades enviadas pelo Olá dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="d6ec2-169">Este trecho de código adiciona detalhes de saudação **InitiateFirmwareUpdate** método incluindo texto toodisplay no portal de solução de saudação e detalhes de saudação necessários parâmetros de método.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="d6ec2-170">simulador Olá envia relatadas propriedades, incluindo lista Olá dos métodos com suporte, tooIoT Hub quando o simulador Olá inicia.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="d6ec2-171">Adicione um código do manipulador toohello simulador para cada método que oferece suporte a ele.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="d6ec2-172">Você pode ver manipuladores existente Olá Olá **CoolerDevice** classe no projeto de Simulator.WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="d6ec2-173">Olá, exemplo a seguir mostra o manipulador de saudação para **InitiateFirmwareUpdate** método:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="d6ec2-174">Nomes de manipulador de método devem começar com `On` seguido pelo nome de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="d6ec2-175">Olá **methodRequest** parâmetro contém todos os parâmetros passados com a invocação de método hello de back-end de arquivo de solução hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="d6ec2-176">Olá valor de retorno deve ser do tipo **tarefa&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="d6ec2-177">Olá **BuildMethodResponse** método utilitário o ajuda a criar o valor de retorno de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="d6ec2-178">Dentro do manipulador de método hello, você pode:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="d6ec2-179">iniciar uma tarefa assíncrona.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="d6ec2-180">Recuperar propriedades desejadas de saudação *duas dispositivo* no IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="d6ec2-181">Atualizar uma única propriedade relatada usando Olá **SetReportedPropertyAsync** método hello **CoolerDevice** classe.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="d6ec2-182">Atualizar várias propriedades relatadas, criando um **TwinCollection** instância e hello chamada **Transport.UpdateReportedPropertiesAsync** método.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="d6ec2-183">Olá, exemplo anterior de atualização de firmware executa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="d6ec2-184">Verificações de saudação dispositivo é tooaccept capaz de solicitação de atualização de firmware de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="d6ec2-185">Inicia a operação de atualização de firmware hello e redefine a telemetria hello quando Olá operação é concluída de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="d6ec2-186">Imediatamente retorna hello "FirmwareUpdate aceitada" solicitação de saudação tooindicate mensagem foi aceita pelo dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="d6ec2-187">Compilar e usar seu próprio dispositivo (físico)</span><span class="sxs-lookup"><span data-stu-id="d6ec2-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="d6ec2-188">Olá [SDKs do Azure IoT](https://github.com/Azure/azure-iot-sdks) fornecem bibliotecas para se conectar a vários tipos de dispositivo (idiomas e sistemas operacionais) em soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="d6ec2-189">Modificar os limites do painel</span><span class="sxs-lookup"><span data-stu-id="d6ec2-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="d6ec2-190">Número de dispositivos exibida na lista suspensa do painel</span><span class="sxs-lookup"><span data-stu-id="d6ec2-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="d6ec2-191">saudação padrão é 200.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-191">hello default is 200.</span></span> <span data-ttu-id="d6ec2-192">É possível alterar esse número em [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="d6ec2-193">Número de pins toodisplay no controle de mapa do Bing</span><span class="sxs-lookup"><span data-stu-id="d6ec2-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="d6ec2-194">saudação padrão é 200.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-194">hello default is 200.</span></span> <span data-ttu-id="d6ec2-195">É possível alterar esse número em [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="d6ec2-196">Período do gráfico de telemetria</span><span class="sxs-lookup"><span data-stu-id="d6ec2-196">Time period of telemetry graph</span></span>

<span data-ttu-id="d6ec2-197">padrão de saudação é de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-197">hello default is 10 minutes.</span></span> <span data-ttu-id="d6ec2-198">É possível alterar esse valor em [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="d6ec2-199">Configurar manualmente as funções do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d6ec2-199">Manually set up application roles</span></span>

<span data-ttu-id="d6ec2-200">Olá procedimento a seguir descreve como tooadd **Admin** e **ReadOnly** tooa de funções de aplicativo pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="d6ec2-201">Observe que soluções pré-configuradas provisionadas de site de azureiotsuite.com Olá já incluem Olá **Admin** e **ReadOnly** funções.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="d6ec2-202">Membros da saudação **ReadOnly** função pode ver o painel de saudação e lista de dispositivos hello, mas não são permitidas tooadd dispositivos, alterar atributos de dispositivo ou comandos de envio.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="d6ec2-203">Membros da saudação **Admin** função tem funcionalidade de acesso completo a saudação tooall na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="d6ec2-204">Vá toohello [portal clássico do Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="d6ec2-205">Selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="d6ec2-206">Clique em nome de saudação do locatário do AAD Olá usado quando você provisionou sua solução.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="d6ec2-207">Clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-207">Click **Applications**.</span></span>
5. <span data-ttu-id="d6ec2-208">Clique em nome de saudação do aplicativo hello que coincide com o nome de solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="d6ec2-209">Se você não vir o aplicativo na lista de saudação, selecione **aplicativos que minha empresa possui** em Olá **Mostrar** Olá a lista suspensa e clique em marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="d6ec2-210">Final Olá Olá página, clique em **gerenciar manifesto** e **baixar manifesto**.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="d6ec2-211">Esse procedimento baixa uma máquina local do arquivo tooyour. JSON.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="d6ec2-212">Abra esse arquivo para edição em um editor de texto de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="d6ec2-213">Na terceira linha do arquivo. JSON de Olá Olá, você pode ver:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="d6ec2-214">Substitua esta linha hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="d6ec2-215">Salve o arquivo. JSON atualizado de saudação (você pode substituir o arquivo existente Olá).</span><span class="sxs-lookup"><span data-stu-id="d6ec2-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="d6ec2-216">No hello portal clássico do Azure, na parte inferior da saudação da página hello, selecione **gerenciar manifesto** , em seguida, **carregar manifesto** . JSON arquivo tooupload Olá que você salvou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="d6ec2-217">Agora você adicionou Olá **Admin** e **ReadOnly** aplicativo tooyour de funções.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="d6ec2-218">tooassign um usuário de tooa essas funções em seu diretório, consulte [permissões no site do hello azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="d6ec2-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="d6ec2-219">Comentários</span><span class="sxs-lookup"><span data-stu-id="d6ec2-219">Feedback</span></span>

<span data-ttu-id="d6ec2-220">Você tem uma personalização que você gostaria que toosee abordado neste documento?</span><span class="sxs-lookup"><span data-stu-id="d6ec2-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="d6ec2-221">Adicionar sugestões de recursos muito[User Voice](https://feedback.azure.com/forums/321918-azure-iot), ou comentário sobre este artigo.</span><span class="sxs-lookup"><span data-stu-id="d6ec2-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d6ec2-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6ec2-222">Next steps</span></span>

<span data-ttu-id="d6ec2-223">toolearn mais sobre opções de saudação para personalizar soluções Olá pré-configurado, consulte:</span><span class="sxs-lookup"><span data-stu-id="d6ec2-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="d6ec2-224">[Conecte-se a solução de monitoramento do Azure IoT Suite remoto pré-configurado do aplicativo lógico tooyour][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="d6ec2-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="d6ec2-225">[Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="d6ec2-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="d6ec2-226">[Metadados de informações de dispositivo no hello solução pré-configurada de monitoramento remoto][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="d6ec2-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="d6ec2-227">[Personalizar como Olá conectadas fábrica solução exibe dados de seus servidores de OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="d6ec2-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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