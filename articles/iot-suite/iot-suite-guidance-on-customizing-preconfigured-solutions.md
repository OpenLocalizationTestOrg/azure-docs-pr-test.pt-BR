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
# <a name="customize-a-preconfigured-solution"></a>Personalizar uma solução pré-configurada

soluções de saudação pré-configurado fornecidas com hello Azure IoT Suite demonstram serviços Olá Olá suite trabalhar juntos toodeliver uma solução de ponta a ponta. Do ponto de partida, há vários locais em que você pode estender e personalizar Olá solução para cenários específicos. Olá seções a seguir descreve esses pontos comuns de personalização.

## <a name="find-hello-source-code"></a>Localizar o código-fonte Olá

código-fonte para soluções de saudação pré-configurado Hello está disponível no GitHub no hello repositórios a seguir:

* Monitoramento remoto: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Manutenção preditiva: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Fábrica conectada: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

código-fonte Olá para soluções de saudação pré-configurado é fornecido práticas e padrões de saudação toodemonstrate usou a funcionalidade de ponta a ponta de saudação do tooimplement de uma solução de IoT usando Azure IoT Suite. Você pode encontrar mais informações sobre como toobuild e implantar soluções de saudação em repositórios de GitHub hello.

## <a name="change-hello-preconfigured-rules"></a>Altere as regras de saudação pré-configurado

Olá solução de monitoramento remota inclui três [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) informações do dispositivo toohandle, telemetria e lógica de regras na solução de saudação de trabalhos.

Olá três fluxo trabalhos de análise e sua sintaxe são descritos em detalhes no hello [monitoramento remoto pré-configurado passo a passo de solução](iot-suite-remote-monitoring-sample-walkthrough.md). 

Você pode editar esses trabalhos diretamente tooalter Olá lógica ou adicionar lógica específica tooyour cenário. Você pode encontrar hello trabalhos do Stream Analytics da seguinte maneira:

1. Vá muito[portal do Azure](https://portal.azure.com).
2. Navegue toohello o grupo de recursos com o mesmo nome como sua solução de IoT de saudação. 
3. Selecione hello Azure Stream Analytics trabalho você gostaria que toomodify. 
4. Interromper o trabalho de saudação selecionando **parar** no conjunto de saudação de comandos. 
5. Edite entradas hello, consulta e saídas.
   
    Uma simples modificação é toochange consultar Olá Olá **regras** toouse trabalho um **"<"** em vez de um **">"**. portal de solução Olá ainda mostra **">"** quando você editar uma regra, mas observe como o comportamento de saudação é invertido devido toohello alteração no hello subjacente de trabalho.
6. Iniciar trabalho Olá

> [!NOTE]
> Painel de monitoramento remoto Olá depende de dados específicos, isso alterar trabalhos Olá pode provocar Olá painel toofail.

## <a name="add-your-own-rules"></a>Adicionar suas próprias regras

Além disso, Olá toochanging pré-configurado trabalhos do Stream Analytics do Azure, você pode usar novos trabalhos do hello tooadd portal do Azure ou adicionar novos trabalhos de tooexisting de consultas.

## <a name="customize-devices"></a>Personalizar dispositivos

Uma das atividades mais comuns de extensão hello está trabalhando com cenário de tooyour específicos de dispositivos. Há vários métodos para trabalhar com dispositivos. Esses métodos incluem alterando seu cenário de um dispositivo simulado toomatch ou usando Olá [SDK de dispositivo IoT] [ IoT Device SDK] tooconnect sua solução de toohello do dispositivo físico.

Para dispositivos de tooadding um guia passo a passo, consulte Olá [dispositivos de conexão do Iot Suite](iot-suite-connecting-devices.md) artigo e hello [C amostra do SDK de monitoramento remoto](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Este exemplo é projetado toowork com hello solução pré-configurada de monitoramento remoto.

### <a name="create-your-own-simulated-device"></a>Criar seu próprio dispositivo simulado

Incluído no hello [código fonte da solução de monitoramento remoto](https://github.com/Azure/azure-iot-remote-monitoring), é um simulador de .NET. Este simulador é hello um provisionado como parte da solução de saudação e você pode alterá-la toosend diferentes metadados, telemetria e responder métodos e comandos toodifferent.

simulador pré-configurado de saudação na solução pré-configurada de monitoramento remoto de saudação simula um dispositivo cooler que emite a telemetria de temperatura e umidade. Você pode modificar o simulador Olá no hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) quando você bifurcada repositório GitHub de saudação do projeto.

### <a name="available-locations-for-simulated-devices"></a>Locais disponíveis para dispositivos simulados

conjunto de locais padrão de saudação está em Seattle/Redmond, Washington, Estados Unidos. É possível alterar esses locais em [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Adicionar um simulador toohello de manipulador de atualização de propriedade desejada

Você pode definir um valor para uma propriedade desejada para um dispositivo no portal de solução de saudação. É responsabilidade do hello de solicitação de alteração de propriedade Olá dispositivo toohandle hello quando o dispositivo Olá recupera o valor da propriedade Olá desejado. suporte de tooadd para uma alteração de valor de propriedade por meio de uma propriedade desejada, você precisa tooadd um simulador de toohello do manipulador.

simulador Olá contém manipuladores para Olá **SetPointTemp** e **TelemetryInterval** desejado de propriedades que você pode atualizar definindo valores no portal de solução de saudação.

Olá, exemplo a seguir mostra manipulador Olá Olá **SetPointTemp** desejado propriedade Olá **CoolerDevice** classe:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Este método atualizará o ponto de telemetria Olá temperatura e, em seguida, Olá relatórios alterar tooIoT back Hub definindo uma propriedade relatada.

Você pode adicionar seus próprios manipuladores para suas próprias propriedades pelo seguinte padrão de Olá Olá anterior de exemplo.

Você também deve vincular o manipulador de toohello de propriedade desejados Olá conforme Olá seguinte exemplo de hello **CoolerDevice** construtor:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Observe que **SetPointTempPropertyName** é uma constante definida como "Config.SetPointTemp".

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Adicionar suporte para um simulador de toohello novo método

Você pode personalizar Olá simulador tooadd suporte para um novo [método (método direto)][lnk-direct-methods]. Há duas etapas principais necessárias:

- simulador Olá deve notificar o hub IoT de saudação na solução Olá pré-configurados com detalhes do método hello.
- simulador Olá deve incluir a chamada de método do código toohandle Olá ao invocá-lo da saudação **detalhes do dispositivo** painel no Gerenciador de soluções hello, ou por meio de um trabalho.

Olá monitoramento remoto pré-configurado solução usa *relatado propriedades* toosend detalhes do hub de tooIoT métodos com suporte. back-end de solução Olá mantém uma lista de todos os métodos de saudação suportados por cada dispositivo junto com um histórico de invocações do método. Você pode exibir essas informações sobre dispositivos e chamar métodos no portal de solução de saudação.

hub IoT da saudação de toonotify que um dispositivo oferece suporte a um método, dispositivo Olá deve adicionar detalhes da saudação método toohello **SupportedMethods** nó Olá relatado propriedades:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

assinatura do método Hello tem Olá formato a seguir: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Por exemplo, toospecify Olá **InitiateFirmwareUpdate** método espera um parâmetro de cadeia de caracteres chamado **FwPackageURI**, use Olá a assinatura do método a seguir:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Para obter uma lista dos tipos de parâmetro com suporte, consulte Olá **CommandTypes** classe no projeto de infra-estrutura de saudação.

toodelete um método, defina a assinatura do método hello muito`null` no hello reportada propriedades.

> [!NOTE]
> Olá back-end solução atualiza somente informações sobre os métodos com suporte quando ele recebe um *informações do dispositivo* mensagem do dispositivo hello.

Olá seguinte exemplo de código da saudação **SampleDeviceFactory** classe Olá comuns de projeto mostra como tooadd uma lista de toohello do método de **SupportedMethods** no hello reportada propriedades enviadas pelo Olá dispositivo:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Este trecho de código adiciona detalhes de saudação **InitiateFirmwareUpdate** método incluindo texto toodisplay no portal de solução de saudação e detalhes de saudação necessários parâmetros de método.

simulador Olá envia relatadas propriedades, incluindo lista Olá dos métodos com suporte, tooIoT Hub quando o simulador Olá inicia.

Adicione um código do manipulador toohello simulador para cada método que oferece suporte a ele. Você pode ver manipuladores existente Olá Olá **CoolerDevice** classe no projeto de Simulator.WebJob hello. Olá, exemplo a seguir mostra o manipulador de saudação para **InitiateFirmwareUpdate** método:

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

Nomes de manipulador de método devem começar com `On` seguido pelo nome de saudação do método hello. Olá **methodRequest** parâmetro contém todos os parâmetros passados com a invocação de método hello de back-end de arquivo de solução hello. Olá valor de retorno deve ser do tipo **tarefa&lt;MethodResponse&gt;**. Olá **BuildMethodResponse** método utilitário o ajuda a criar o valor de retorno de saudação.

Dentro do manipulador de método hello, você pode:

- iniciar uma tarefa assíncrona.
- Recuperar propriedades desejadas de saudação *duas dispositivo* no IoT Hub.
- Atualizar uma única propriedade relatada usando Olá **SetReportedPropertyAsync** método hello **CoolerDevice** classe.
- Atualizar várias propriedades relatadas, criando um **TwinCollection** instância e hello chamada **Transport.UpdateReportedPropertiesAsync** método.

Olá, exemplo anterior de atualização de firmware executa Olá etapas a seguir:

- Verificações de saudação dispositivo é tooaccept capaz de solicitação de atualização de firmware de saudação.
- Inicia a operação de atualização de firmware hello e redefine a telemetria hello quando Olá operação é concluída de forma assíncrona.
- Imediatamente retorna hello "FirmwareUpdate aceitada" solicitação de saudação tooindicate mensagem foi aceita pelo dispositivo hello.

### <a name="build-and-use-your-own-physical-device"></a>Compilar e usar seu próprio dispositivo (físico)

Olá [SDKs do Azure IoT](https://github.com/Azure/azure-iot-sdks) fornecem bibliotecas para se conectar a vários tipos de dispositivo (idiomas e sistemas operacionais) em soluções de IoT.

## <a name="modify-dashboard-limits"></a>Modificar os limites do painel

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Número de dispositivos exibida na lista suspensa do painel

saudação padrão é 200. É possível alterar esse número em [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Número de pins toodisplay no controle de mapa do Bing

saudação padrão é 200. É possível alterar esse número em [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Período do gráfico de telemetria

padrão de saudação é de 10 minutos. É possível alterar esse valor em [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Configurar manualmente as funções do aplicativo

Olá procedimento a seguir descreve como tooadd **Admin** e **ReadOnly** tooa de funções de aplicativo pré-configurado solução. Observe que soluções pré-configuradas provisionadas de site de azureiotsuite.com Olá já incluem Olá **Admin** e **ReadOnly** funções.

Membros da saudação **ReadOnly** função pode ver o painel de saudação e lista de dispositivos hello, mas não são permitidas tooadd dispositivos, alterar atributos de dispositivo ou comandos de envio.  Membros da saudação **Admin** função tem funcionalidade de acesso completo a saudação tooall na solução de saudação.

1. Vá toohello [portal clássico do Azure][lnk-classic-portal].
2. Selecione **Active Directory**.
3. Clique em nome de saudação do locatário do AAD Olá usado quando você provisionou sua solução.
4. Clique em **Aplicativos**.
5. Clique em nome de saudação do aplicativo hello que coincide com o nome de solução pré-configurada. Se você não vir o aplicativo na lista de saudação, selecione **aplicativos que minha empresa possui** em Olá **Mostrar** Olá a lista suspensa e clique em marca de seleção.
6. Final Olá Olá página, clique em **gerenciar manifesto** e **baixar manifesto**.
7. Esse procedimento baixa uma máquina local do arquivo tooyour. JSON. Abra esse arquivo para edição em um editor de texto de sua escolha.
8. Na terceira linha do arquivo. JSON de Olá Olá, você pode ver:

   ```json
   "appRoles" : [],
   ```
   Substitua esta linha hello código a seguir:

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

9. Salve o arquivo. JSON atualizado de saudação (você pode substituir o arquivo existente Olá).
10. No hello portal clássico do Azure, na parte inferior da saudação da página hello, selecione **gerenciar manifesto** , em seguida, **carregar manifesto** . JSON arquivo tooupload Olá que você salvou na etapa anterior hello.
11. Agora você adicionou Olá **Admin** e **ReadOnly** aplicativo tooyour de funções.
12. tooassign um usuário de tooa essas funções em seu diretório, consulte [permissões no site do hello azureiotsuite.com][lnk-permissions].

## <a name="feedback"></a>Comentários

Você tem uma personalização que você gostaria que toosee abordado neste documento? Adicionar sugestões de recursos muito[User Voice](https://feedback.azure.com/forums/321918-azure-iot), ou comentário sobre este artigo. 

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre opções de saudação para personalizar soluções Olá pré-configurado, consulte:

* [Conecte-se a solução de monitoramento do Azure IoT Suite remoto pré-configurado do aplicativo lógico tooyour][lnk-logicapp]
* [Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto][lnk-dynamic]
* [Metadados de informações de dispositivo no hello solução pré-configurada de monitoramento remoto][lnk-devinfo]
* [Personalizar como Olá conectadas fábrica solução exibe dados de seus servidores de OPC UA][lnk-cf-customize]

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