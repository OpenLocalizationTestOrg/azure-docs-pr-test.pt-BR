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
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Criar uma regra personalizada no hello solução pré-configurada de monitoramento remoto

## <a name="introduction"></a>Introdução

Em soluções de saudação pré-configurados, você pode configurar [regras disparam quando uma telemetria de valor para um dispositivo atinge um limite específico][lnk-builtin-rule]. [Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto] [ lnk-dynamic-telemetry] descreve como você pode adicionar valores de telemetria personalizada, como *ExternalTemperature* tooyour solução. Este artigo mostra como os tipos de regra personalizada de toocreate de telemetria dinâmica em sua solução.

Este tutorial usa um simples Node. js dispositivo simulado toogenerate telemetria dinâmico toosend toohello solução pré-configurada back-end. Adicione regras personalizadas no hello **RemoteMonitoring** solução do Visual Studio e implantar esse tooyour de back-end personalizado assinatura do Azure.

toocomplete neste tutorial, você precisa:

* Uma assinatura ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].
* [Node.js] [ lnk-node] versão 0.12.x ou posterior toocreate um dispositivo simulado.
* Visual Studio 2015 ou Visual Studio de 2017 toomodify Olá pré-configurado solução novamente terminar com as regras de novo.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Anote Olá solução nome escolhido para sua implantação. Você precisará do nome dessa solução mais tarde neste tutorial.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Você pode interromper o aplicativo de console do Node. js hello quando você tiver verificado que está enviando **ExternalTemperature** toohello telemetria pré-configurado solução. Janela de console Olá mantenha aberta porque você executa esse aplicativo de console do Node. js novamente depois que você adicionar Olá regra personalizada toohello solução.

## <a name="rule-storage-locations"></a>Locais de armazenamento de regras

As informações sobre as regras são mantidas em dois locais:

* **DeviceRulesNormalizedTable** tabela – esta tabela armazena um normalizado toohello regras definidas pelo portal de solução de saudação de referência. Quando o portal de solução de saudação exibe as regras de dispositivo, ele consulta esta tabela para definições de regra de saudação.
* **DeviceRules** blob – esse blob armazena todas as regras de saudação definidas para todos os dispositivos registrados e são definidos como trabalhos referência toohello entrada Stream Analytics do Azure.
 
Quando você atualiza uma regra existente ou define uma nova regra no portal de solução de hello, tabela hello e blob são atualizados tooreflect Olá alterações. regra Olá definição exibido no portal de saudação vem do repositório de tabela hello e regra Olá definição referenciada por trabalhos do Stream Analytics Olá vem do blob de saudação. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Atualizar solução de RemoteMonitoring Visual Studio Olá

Olá etapas a seguir mostram como toomodify Olá RemoteMonitoring Visual Studio solução tooinclude uma nova regra que usa Olá **ExternalTemperature** telemetria enviada do dispositivo simulado hello:

1. Se você ainda não tiver feito isso, Olá clone **azure-iot-monitoramento remoto** local do repositório tooa adequado em seu computador local usando Olá Git comando a seguir:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. No Visual Studio, abra o arquivo de RemoteMonitoring.sln de saudação da sua cópia local da saudação **azure-iot-monitoramento remoto** repositório.

3. Abra o arquivo hello Infrastructure\Models\DeviceRuleBlobEntity.cs e adicione um **ExternalTemperature** propriedade da seguinte maneira:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. Em Olá mesmo arquivo, adicione uma **ExternalTemperatureRuleOutput** propriedade da seguinte maneira:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Abra o arquivo de saudação Infrastructure\Models\DeviceRuleDataFields.cs e adicione o seguinte Olá **ExternalTemperature** propriedade após Olá existente **umidade** propriedade:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. No hello mesmo arquivo, atualizar Olá **_availableDataFields** método tooinclude **ExternalTemperature** da seguinte maneira:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Abra o arquivo hello Infrastructure\Repository\DeviceRulesRepository.cs e modifique Olá **BuildBlobEntityListFromTableRows** método da seguinte maneira:

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

## <a name="rebuild-and-redeploy-hello-solution"></a>Recompilar e reimplantar a solução de saudação.

Agora você pode implantar Olá atualizado solução tooyour assinatura do Azure.

1. Abra um prompt de comando com privilégios elevados e navegue toohello raiz de sua cópia local do repositório de monitoramento do azure-iot-remoto Olá.

2. toodeploy sua solução atualizada, execute Olá a seguir de comando substituindo **{nome da implantação}** com nome de saudação da sua implantação de solução pré-configurada que você anotou anteriormente:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Atualizar o trabalho de análise de fluxo de saudação

Quando Olá implantação estiver concluída, você pode atualizar Olá Stream Analytics trabalho toouse Olá novas definições de regra.

1. No portal do Azure de Olá, navegue toohello grupo de recursos que contém seus recursos de solução pré-configurada. Este grupo de recursos tem Olá mesmo nome que você especificou para Olá solução durante a implantação de saudação.

2. Navegue toohello {nome da implantação}-trabalho de análise de fluxo de regras. 

3. Clique em **parar** trabalho de análise de fluxo de Olá toostop seja executado. (Você deve aguardar Olá toostop de trabalho de streaming antes de poder editar consulta Olá).

4. Clique em **Consulta**. Editar saudação do hello consulta tooinclude **selecione** instrução **ExternalTemperature**. Olá exemplo a seguir mostra a consulta completa Olá com hello novo **selecione** instrução:

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

5. Clique em **salvar** toochange Olá atualizar pesquisa de regra.

6. Clique em **iniciar** toostart trabalho de análise de fluxo de saudação executando novamente.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Adicionar nova regra no painel de saudação

Agora você pode adicionar Olá **ExternalTemperature** dispositivo de tooa de regra no painel de solução de saudação.

1. Navegue toohello portal de solução.

2. Navegue toohello **dispositivos** painel.

3. Localizar dispositivo personalizado do hello criado que envia **ExternalTemperature** telemetria e Olá **detalhes do dispositivo** do painel, clique em **Adicionar regra**.

4. Selecione **ExternalTemperature** no **Campo de Dados**.

5. Definir **limite** too56. Em seguida, clique em **Salvar e exibir regras**.

6. Retorna o histórico de alarme toohello painel tooview hello.

7. Na janela de console Olá é deixada aberta, iniciar o envio do aplicativo toobegin do hello Node. js console **ExternalTemperature** os dados de telemetria.

8. Observe que Olá **histórico de alarme** tabela mostra alarmes novo quando a nova regra de saudação é disparada.
 
## <a name="additional-information"></a>Informações adicionais

Operador de saudação alteração  **>**  é mais complexa e vai além da saudação etapas descritas neste tutorial. Embora seja possível alterar toouse de trabalho do Stream Analytics Olá qualquer operador que você deseja, refletir esse operador no portal de solução de saudação é uma tarefa mais complexa. 

## <a name="next-steps"></a>Próximas etapas
Agora que você viu como toocreate de regras personalizadas, você pode aprender mais sobre as soluções de saudação pré-configurados:

- [Conecte-se a solução de monitoramento do Azure IoT Suite remoto pré-configurado do aplicativo lógico tooyour][lnk-logic-app]
- [Metadados de informações de dispositivo no monitoramento remoto de saudação pré-configurado solução][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md