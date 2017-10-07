---
title: aaaCreate uma regra personalizada no Azure IoT Suite | Microsoft Docs
description: "Como toocreate uma regra personalizada em um conjunto de IoT pré-configurado solução."
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="eb6d1-103">Criar uma regra personalizada no hello solução pré-configurada de monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="eb6d1-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="eb6d1-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="eb6d1-104">Introduction</span></span>

<span data-ttu-id="eb6d1-105">Em soluções de saudação pré-configurados, você pode configurar [regras disparam quando uma telemetria de valor para um dispositivo atinge um limite específico][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="eb6d1-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="eb6d1-106">[Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto] [ lnk-dynamic-telemetry] descreve como você pode adicionar valores de telemetria personalizada, como *ExternalTemperature* tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="eb6d1-107">Este artigo mostra como os tipos de regra personalizada de toocreate de telemetria dinâmica em sua solução.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="eb6d1-108">Este tutorial usa um simples Node. js dispositivo simulado toogenerate telemetria dinâmico toosend toohello solução pré-configurada back-end.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="eb6d1-109">Adicione regras personalizadas no hello **RemoteMonitoring** solução do Visual Studio e implantar esse tooyour de back-end personalizado assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="eb6d1-110">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="eb6d1-111">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-111">An active Azure subscription.</span></span> <span data-ttu-id="eb6d1-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="eb6d1-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="eb6d1-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="eb6d1-114">[Node.js] [ lnk-node] versão 0.12.x ou posterior toocreate um dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="eb6d1-115">Visual Studio 2015 ou Visual Studio de 2017 toomodify Olá pré-configurado solução novamente terminar com as regras de novo.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="eb6d1-116">Anote Olá solução nome escolhido para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="eb6d1-117">Você precisará do nome dessa solução mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="eb6d1-118">Você pode interromper o aplicativo de console do Node. js hello quando você tiver verificado que está enviando **ExternalTemperature** toohello telemetria pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="eb6d1-119">Janela de console Olá mantenha aberta porque você executa esse aplicativo de console do Node. js novamente depois que você adicionar Olá regra personalizada toohello solução.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="eb6d1-120">Locais de armazenamento de regras</span><span class="sxs-lookup"><span data-stu-id="eb6d1-120">Rule storage locations</span></span>

<span data-ttu-id="eb6d1-121">As informações sobre as regras são mantidas em dois locais:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="eb6d1-122">**DeviceRulesNormalizedTable** tabela – esta tabela armazena um normalizado toohello regras definidas pelo portal de solução de saudação de referência.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="eb6d1-123">Quando o portal de solução de saudação exibe as regras de dispositivo, ele consulta esta tabela para definições de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="eb6d1-124">**DeviceRules** blob – esse blob armazena todas as regras de saudação definidas para todos os dispositivos registrados e são definidos como trabalhos referência toohello entrada Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="eb6d1-125">Quando você atualiza uma regra existente ou define uma nova regra no portal de solução de hello, tabela hello e blob são atualizados tooreflect Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="eb6d1-126">regra Olá definição exibido no portal de saudação vem do repositório de tabela hello e regra Olá definição referenciada por trabalhos do Stream Analytics Olá vem do blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="eb6d1-127">Atualizar solução de RemoteMonitoring Visual Studio Olá</span><span class="sxs-lookup"><span data-stu-id="eb6d1-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="eb6d1-128">Olá etapas a seguir mostram como toomodify Olá RemoteMonitoring Visual Studio solução tooinclude uma nova regra que usa Olá **ExternalTemperature** telemetria enviada do dispositivo simulado hello:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="eb6d1-129">Se você ainda não tiver feito isso, Olá clone **azure-iot-monitoramento remoto** local do repositório tooa adequado em seu computador local usando Olá Git comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="eb6d1-130">No Visual Studio, abra o arquivo de RemoteMonitoring.sln de saudação da sua cópia local da saudação **azure-iot-monitoramento remoto** repositório.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="eb6d1-131">Abra o arquivo hello Infrastructure\Models\DeviceRuleBlobEntity.cs e adicione um **ExternalTemperature** propriedade da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="eb6d1-132">Em Olá mesmo arquivo, adicione uma **ExternalTemperatureRuleOutput** propriedade da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="eb6d1-133">Abra o arquivo de saudação Infrastructure\Models\DeviceRuleDataFields.cs e adicione o seguinte Olá **ExternalTemperature** propriedade após Olá existente **umidade** propriedade:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="eb6d1-134">No hello mesmo arquivo, atualizar Olá **_availableDataFields** método tooinclude **ExternalTemperature** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="eb6d1-135">Abra o arquivo hello Infrastructure\Repository\DeviceRulesRepository.cs e modifique Olá **BuildBlobEntityListFromTableRows** método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="eb6d1-136">Recompilar e reimplantar a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="eb6d1-137">Agora você pode implantar Olá atualizado solução tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="eb6d1-138">Abra um prompt de comando com privilégios elevados e navegue toohello raiz de sua cópia local do repositório de monitoramento do azure-iot-remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="eb6d1-139">toodeploy sua solução atualizada, execute Olá a seguir de comando substituindo **{nome da implantação}** com nome de saudação da sua implantação de solução pré-configurada que você anotou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="eb6d1-140">Atualizar o trabalho de análise de fluxo de saudação</span><span class="sxs-lookup"><span data-stu-id="eb6d1-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="eb6d1-141">Quando Olá implantação estiver concluída, você pode atualizar Olá Stream Analytics trabalho toouse Olá novas definições de regra.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="eb6d1-142">No portal do Azure de Olá, navegue toohello grupo de recursos que contém seus recursos de solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="eb6d1-143">Este grupo de recursos tem Olá mesmo nome que você especificou para Olá solução durante a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="eb6d1-144">Navegue toohello {nome da implantação}-trabalho de análise de fluxo de regras.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="eb6d1-145">Clique em **parar** trabalho de análise de fluxo de Olá toostop seja executado.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="eb6d1-146">(Você deve aguardar Olá toostop de trabalho de streaming antes de poder editar consulta Olá).</span><span class="sxs-lookup"><span data-stu-id="eb6d1-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="eb6d1-147">Clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-147">Click **Query**.</span></span> <span data-ttu-id="eb6d1-148">Editar saudação do hello consulta tooinclude **selecione** instrução **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="eb6d1-149">Olá exemplo a seguir mostra a consulta completa Olá com hello novo **selecione** instrução:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="eb6d1-150">Clique em **salvar** toochange Olá atualizar pesquisa de regra.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="eb6d1-151">Clique em **iniciar** toostart trabalho de análise de fluxo de saudação executando novamente.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="eb6d1-152">Adicionar nova regra no painel de saudação</span><span class="sxs-lookup"><span data-stu-id="eb6d1-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="eb6d1-153">Agora você pode adicionar Olá **ExternalTemperature** dispositivo de tooa de regra no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="eb6d1-154">Navegue toohello portal de solução.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="eb6d1-155">Navegue toohello **dispositivos** painel.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="eb6d1-156">Localizar dispositivo personalizado do hello criado que envia **ExternalTemperature** telemetria e Olá **detalhes do dispositivo** do painel, clique em **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="eb6d1-157">Selecione **ExternalTemperature** no **Campo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="eb6d1-158">Definir **limite** too56.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-158">Set **Threshold** too56.</span></span> <span data-ttu-id="eb6d1-159">Em seguida, clique em **Salvar e exibir regras**.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="eb6d1-160">Retorna o histórico de alarme toohello painel tooview hello.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="eb6d1-161">Na janela de console Olá é deixada aberta, iniciar o envio do aplicativo toobegin do hello Node. js console **ExternalTemperature** os dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="eb6d1-162">Observe que Olá **histórico de alarme** tabela mostra alarmes novo quando a nova regra de saudação é disparada.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="eb6d1-163">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="eb6d1-163">Additional information</span></span>

<span data-ttu-id="eb6d1-164">Operador de saudação alteração  **>**  é mais complexa e vai além da saudação etapas descritas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="eb6d1-165">Embora seja possível alterar toouse de trabalho do Stream Analytics Olá qualquer operador que você deseja, refletir esse operador no portal de solução de saudação é uma tarefa mais complexa.</span><span class="sxs-lookup"><span data-stu-id="eb6d1-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eb6d1-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb6d1-166">Next steps</span></span>
<span data-ttu-id="eb6d1-167">Agora que você viu como toocreate de regras personalizadas, você pode aprender mais sobre as soluções de saudação pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="eb6d1-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="eb6d1-168">[Conecte-se a solução de monitoramento do Azure IoT Suite remoto pré-configurado do aplicativo lógico tooyour][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="eb6d1-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="eb6d1-169">[Metadados de informações de dispositivo no monitoramento remoto de saudação pré-configurado solução][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="eb6d1-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md