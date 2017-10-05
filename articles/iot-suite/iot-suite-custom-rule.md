---
title: Criar uma regra personalizada no Azure IoT Suite | Microsoft Docs
description: "Como criar uma regra personalizada em uma solução pré-configurada do IoT Suite."
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
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="df406-103">Criar uma regra personalizada na solução pré-configurada de monitoramento remota</span><span class="sxs-lookup"><span data-stu-id="df406-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="df406-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="df406-104">Introduction</span></span>

<span data-ttu-id="df406-105">Nas soluções pré-configuradas, você pode configurar [regras que serão disparadas quando um valor de telemetria de um dispositivo atingir um limite específico][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="df406-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="df406-106">[Usar telemetria dinâmica com a solução pré-configurada de monitoramento remoto][lnk-dynamic-telemetry] descreve como você pode adicionar valores personalizados de telemetria, como *ExternalTemperature*, à sua solução.</span><span class="sxs-lookup"><span data-stu-id="df406-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="df406-107">Este artigo mostra como criar uma regra personalizada para tipos de telemetria dinâmicos na sua solução.</span><span class="sxs-lookup"><span data-stu-id="df406-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="df406-108">Este tutorial usa um dispositivo simulado Node.js simples para gerar telemetria dinâmica a ser enviada ao back-end da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="df406-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="df406-109">Você então adiciona regras personalizadas à solução **RemoteMonitoring** do Visual Studio e implanta esse back-end personalizado na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="df406-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="df406-110">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="df406-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="df406-111">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="df406-111">An active Azure subscription.</span></span> <span data-ttu-id="df406-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="df406-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="df406-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="df406-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="df406-114">[Node.js][lnk-node] versão 0.12.x ou posterior para criar um dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="df406-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="df406-115">Visual Studio 2015 ou Visual Studio 2017 para modificar o back-end da solução pré-configurada com suas novas regras.</span><span class="sxs-lookup"><span data-stu-id="df406-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="df406-116">Faça uma anotação com o nome da solução que você escolheu para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="df406-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="df406-117">Você precisará do nome dessa solução mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="df406-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="df406-118">Você pode interromper o aplicativo de console do Node.js quando tiver confirmado que ele está enviando a telemetria de **ExternalTemperature** para a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="df406-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="df406-119">Mantenha a janela do console aberta, porque você executará o aplicativo de console do Node.js novamente depois de adicionar a regra personalizada à solução.</span><span class="sxs-lookup"><span data-stu-id="df406-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="df406-120">Locais de armazenamento de regras</span><span class="sxs-lookup"><span data-stu-id="df406-120">Rule storage locations</span></span>

<span data-ttu-id="df406-121">As informações sobre as regras são mantidas em dois locais:</span><span class="sxs-lookup"><span data-stu-id="df406-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="df406-122">Tabela **DeviceRulesNormalizedTable** – essa tabela armazena uma referência normalizada para as regras definidas pelo portal de solução.</span><span class="sxs-lookup"><span data-stu-id="df406-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="df406-123">Quando o portal de solução exibe as regras do dispositivo, ele consulta esta tabela para obter as definições de regras.</span><span class="sxs-lookup"><span data-stu-id="df406-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="df406-124">Blob de **DeviceRules** – esse blob armazena todas as regras definidas para todos os dispositivos registrados e é definido como uma entrada de referência para os trabalhos do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="df406-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="df406-125">Quando você atualiza uma regra existente ou define uma nova regra no portal de solução, a tabela e o blob são atualizados para refletirem as alterações.</span><span class="sxs-lookup"><span data-stu-id="df406-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="df406-126">A definição de regra exibida no portal vem do armazenamento da tabela e a definição da regra referenciada pelos trabalhos do Stream Analytics vem do blob.</span><span class="sxs-lookup"><span data-stu-id="df406-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="df406-127">Atualizar a solução RemoteMonitoring do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df406-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="df406-128">As etapas a seguir mostram como modificar a solução RemoteMonitoring do Visual Studio para incluir uma nova regra que usa a telemetria de **ExternalTemperature** enviada do dispositivo simulado:</span><span class="sxs-lookup"><span data-stu-id="df406-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="df406-129">Caso ainda não o tenha feito, faça um clone do repositório **azure-iot-remote-monitoring** em um local adequado na sua máquina local usando o seguinte comando Git:</span><span class="sxs-lookup"><span data-stu-id="df406-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="df406-130">No Visual Studio, abra o arquivo RemoteMonitoring.sln da sua cópia local do repositório **azure-iot-remote-monitoring**.</span><span class="sxs-lookup"><span data-stu-id="df406-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="df406-131">Abra o arquivo Infrastructure\Models\DeviceRuleBlobEntity.cs e adicione uma propriedade **ExternalTemperature** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="df406-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="df406-132">No mesmo arquivo, adicione uma propriedade **ExternalTemperatureRuleOutput** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="df406-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="df406-133">Abra o arquivo Infrastructure\Models\DeviceRuleDataFields.cs e adicione a seguinte propriedade **ExternalTemperature** após a propriedade **Humidity** existente:</span><span class="sxs-lookup"><span data-stu-id="df406-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="df406-134">No mesmo arquivo, atualize o método **_availableDataFields** para incluir **ExternalTemperature** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="df406-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="df406-135">Abra o arquivo Infrastructure\Repository\DeviceRulesRepository.cs e modifique o método **BuildBlobEntityListFromTableRows** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="df406-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="df406-136">Recompile e reimplante a solução.</span><span class="sxs-lookup"><span data-stu-id="df406-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="df406-137">Agora, você pode implantar a solução atualizada para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="df406-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="df406-138">Abra um prompt de comando elevado e navegue até a raiz da sua cópia local do repositório azure-iot-remote-monitoring.</span><span class="sxs-lookup"><span data-stu-id="df406-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="df406-139">Para implantar a solução atualizada, execute o seguinte comando, substituindo **{nome da implantação}** pelo nome da implantação de solução pré-configurada que você anotou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="df406-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="df406-140">Atualizar o trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="df406-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="df406-141">Quando a implantação for concluída, você poderá atualizar o trabalho do Stream Analytics para usar novas definições de regras.</span><span class="sxs-lookup"><span data-stu-id="df406-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="df406-142">No Portal do Azure, navegue até o grupo de recursos que contém os recursos de solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="df406-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="df406-143">Esse grupo de recursos tem o mesmo nome que você especificou para a solução durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="df406-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="df406-144">Navegue até o trabalho do Stream Analytics {nome da implantação}-Rules.</span><span class="sxs-lookup"><span data-stu-id="df406-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="df406-145">Clique em **Parar** para interromper a execução do trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="df406-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="df406-146">(Você deve aguardar a interrupção do trabalho para editar a consulta).</span><span class="sxs-lookup"><span data-stu-id="df406-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="df406-147">Clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="df406-147">Click **Query**.</span></span> <span data-ttu-id="df406-148">Edite a consulta para incluir a instrução **SELECT** para **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="df406-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="df406-149">O exemplo a seguir mostra a consulta completa com a nova instrução **SELECT**:</span><span class="sxs-lookup"><span data-stu-id="df406-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="df406-150">Clique em **Salvar** para alterar a consulta de regra atualizada.</span><span class="sxs-lookup"><span data-stu-id="df406-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="df406-151">Clique em **Iniciar** para iniciar a execução do trabalho do Stream Analytics novamente.</span><span class="sxs-lookup"><span data-stu-id="df406-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="df406-152">Adicionar sua nova regra no painel de controle</span><span class="sxs-lookup"><span data-stu-id="df406-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="df406-153">Agora, você pode adicionar a regra **ExternalTemperature** a um dispositivo no painel de solução.</span><span class="sxs-lookup"><span data-stu-id="df406-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="df406-154">Navegue até o portal de solução.</span><span class="sxs-lookup"><span data-stu-id="df406-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="df406-155">Navegue até o painel **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="df406-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="df406-156">Localize o dispositivo personalizado que você criou que envia a telemetria de **ExternalTemperature** e, no painel **Detalhes do Dispositivo**, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="df406-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="df406-157">Selecione **ExternalTemperature** no **Campo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="df406-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="df406-158">Defina o **Limite** como 56.</span><span class="sxs-lookup"><span data-stu-id="df406-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="df406-159">Em seguida, clique em **Salvar e exibir regras**.</span><span class="sxs-lookup"><span data-stu-id="df406-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="df406-160">Retorne ao painel para visualizar o histórico de alarme.</span><span class="sxs-lookup"><span data-stu-id="df406-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="df406-161">Na janela do console que você deixou aberta, inicie o aplicativo de console do Node.js para começar a enviar os dados de telemetria de **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="df406-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="df406-162">Observe que a tabela **Histórico do Alarme** mostra novos alarmes quando a nova regra é acionada.</span><span class="sxs-lookup"><span data-stu-id="df406-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="df406-163">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="df406-163">Additional information</span></span>

<span data-ttu-id="df406-164">Alterar o operador **>** é mais complexo e vai além das etapas descritas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="df406-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="df406-165">Embora você possa alterar o trabalho do Stream Analytics para usar qualquer operador que você queira, refletir esse operador no portal de solução é uma tarefa mais complexa.</span><span class="sxs-lookup"><span data-stu-id="df406-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="df406-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df406-166">Next steps</span></span>
<span data-ttu-id="df406-167">Agora que você já viu como criar regras personalizadas, você pode saber mais sobre as soluções pré-configuradas:</span><span class="sxs-lookup"><span data-stu-id="df406-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="df406-168">[Conectar um aplicativo lógico à solução pré-configurada de monitoramento remoto do Azure IoT Suite][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="df406-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="df406-169">[Metadados de informações de dispositivo na solução pré-configurada de monitoramento remoto][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="df406-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md