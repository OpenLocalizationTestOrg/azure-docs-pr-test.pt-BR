---
title: "Telemetria dinâmico aaaUse | Microsoft Docs"
description: "Siga este tutorial toolearn como toouse a telemetria dinâmico com monitoramento remoto hello Azure IoT Suite pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="5a5b8-103">Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="5a5b8-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="5a5b8-104">Telemetria dinâmica permite que você toovisualize qualquer toohello telemetria enviada solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5a5b8-105">dispositivos Olá simulada que implantar solução Olá pré-configurado enviam telemetria de temperatura e umidade, que você pode visualizar no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="5a5b8-106">Se você personalizar dispositivos simulados existentes, criar novos dispositivos simulados ou conectar dispositivos físicos toohello pré-configurado solução pode enviar outros valores de telemetria como temperatura externa hello, RPM ou windspeed.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="5a5b8-107">Em seguida, você pode visualizar essa telemetria adicional no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="5a5b8-108">Este tutorial usa um dispositivo simulado Node. js simples que você pode modificar facilmente tooexperiment com a telemetria dinâmica.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="5a5b8-109">toocomplete neste tutorial, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="5a5b8-110">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-110">An active Azure subscription.</span></span> <span data-ttu-id="5a5b8-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5a5b8-112">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="5a5b8-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="5a5b8-113">[Node.js][lnk-node] versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="5a5b8-114">Você pode concluir este tutorial em qualquer sistema operacional, como Windows ou Linux, onde é possível instalar o Node.js.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="5a5b8-115">Adicionar um tipo de telemetria</span><span class="sxs-lookup"><span data-stu-id="5a5b8-115">Add a telemetry type</span></span>

<span data-ttu-id="5a5b8-116">Olá próxima etapa é a telemetria de saudação tooreplace gerada pelo dispositivo simulado do Node. js Olá com um novo conjunto de valores:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="5a5b8-117">Parar Olá Node. js dispositivo simulado digitando **Ctrl + C** no prompt de comando ou o shell.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="5a5b8-118">No arquivo de remote_monitoring.js Olá, você pode ver os valores de base de dados de saudação de temperatura existente hello, umidade e telemetria temperatura externa.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="5a5b8-119">Adicione um valor de dados base para **rpm** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="5a5b8-120">dispositivo simulado do Node. js Olá usa Olá **generateRandomIncrement** funcionar em Olá remote_monitoring.js arquivo tooadd toohello um incremento aleatório valores de base de dados.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="5a5b8-121">Tornar aleatório Olá **rpm** valor, adicionando uma linha de código após randomizations existente Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="5a5b8-122">Adicione Olá novo rpm valor toohello JSON carga Olá dispositivo envia tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="5a5b8-123">Execute o dispositivo simulado do Node. js hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="5a5b8-124">Observe Olá novo RPM telemetria tipo que será exibido no gráfico de saudação no painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Adicionar RPM toohello painel][image3]

> [!NOTE]
> <span data-ttu-id="5a5b8-126">Você pode precisar toodisable e, em seguida, habilitar o dispositivo Node. js Olá Olá **dispositivos** página na alteração de saudação do hello painel toosee imediatamente.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="5a5b8-127">Personalizar a exibição de painel Olá</span><span class="sxs-lookup"><span data-stu-id="5a5b8-127">Customize hello dashboard display</span></span>

<span data-ttu-id="5a5b8-128">Olá **informações do dispositivo** mensagem pode incluir metadados sobre a telemetria Olá dispositivo Olá pode enviar tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="5a5b8-129">Esses metadados podem especificar os tipos de telemetria Olá Olá dispositivo envia.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="5a5b8-130">Modificar Olá **deviceMetaData** valor Olá remote_monitoring.js arquivo tooinclude um **telemetria** definição após Olá **comandos** definição.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="5a5b8-131">Olá, trecho de código a seguir mostra Olá **comandos** definição (ser tooadd se um `,` após Olá **comandos** definição):</span><span class="sxs-lookup"><span data-stu-id="5a5b8-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="5a5b8-132">solução de monitoramento remoto Olá usa uma definição de metadados de saudação do correspondência diferencia maiusculas de minúsculas toocompare com dados no fluxo de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="5a5b8-133">Adicionando um **telemetria** definição conforme mostrado na saudação anterior trecho de código não altera o comportamento de saudação do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="5a5b8-134">No entanto, a saudação metadados também podem incluir um **DisplayName** toocustomize Olá exibição no painel de saudação do atributo.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="5a5b8-135">Saudação de atualização **telemetria** definição de metadados, como mostrado na Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="5a5b8-136">Olá seguinte captura de tela mostra como essa alteração modifica a legenda do gráfico de saudação no painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Personalizar a legenda do gráfico Olá][image4]

> [!NOTE]
> <span data-ttu-id="5a5b8-138">Você pode precisar toodisable e, em seguida, habilitar o dispositivo Node. js Olá Olá **dispositivos** página na alteração de saudação do hello painel toosee imediatamente.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="5a5b8-139">Tipos de telemetria de saudação de filtro</span><span class="sxs-lookup"><span data-stu-id="5a5b8-139">Filter hello telemetry types</span></span>

<span data-ttu-id="5a5b8-140">Por padrão, o gráfico de saudação no painel de saudação mostra cada série de dados no fluxo de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="5a5b8-141">Você pode usar o hello **informações do dispositivo** toosuppress metadados Olá exibição dos tipos de telemetria específica no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="5a5b8-142">gráfico de saudação toomake Mostrar apenas telemetria de temperatura e umidade, omita **ExternalTemperature** de saudação **informações do dispositivo** **telemetria** metadados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="5a5b8-143">Olá **temperatura externa** não é mais exibido no gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="5a5b8-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Telemetria de saudação de filtro no painel de saudação][image5]

<span data-ttu-id="5a5b8-145">Essa alteração afeta somente a exibição de gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-145">This change only affects hello chart display.</span></span> <span data-ttu-id="5a5b8-146">Olá **ExternalTemperature** valores de dados ainda são armazenados e disponibilizados para qualquer processamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="5a5b8-147">Você pode precisar toodisable e, em seguida, habilitar o dispositivo Node. js Olá Olá **dispositivos** página na alteração de saudação do hello painel toosee imediatamente.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="5a5b8-148">Tratar erros</span><span class="sxs-lookup"><span data-stu-id="5a5b8-148">Handle errors</span></span>

<span data-ttu-id="5a5b8-149">Para um toodisplay de fluxo de dados no gráfico de saudação, seu **tipo** em Olá **informações do dispositivo** metadados devem corresponder o tipo de dados de saudação de valores de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="5a5b8-150">Por exemplo, se hello metadados especificam que Olá **tipo** dos umidade estiver **int** e um **duplo** foi encontrado no fluxo de telemetria Olá então telemetria de umidade Olá não exiba no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="5a5b8-151">No entanto, Olá **umidade** valores ainda são armazenados e disponibilizados para qualquer processamento de back-end.</span><span class="sxs-lookup"><span data-stu-id="5a5b8-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a5b8-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a5b8-152">Next steps</span></span>

<span data-ttu-id="5a5b8-153">Agora que você viu como toouse a telemetria dinâmico, você pode aprender mais sobre como o hello soluções pré-configuradas usam informações do dispositivo: [metadados de informações de dispositivo no monitoramento remoto de saudação pré-configurado solução] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="5a5b8-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
