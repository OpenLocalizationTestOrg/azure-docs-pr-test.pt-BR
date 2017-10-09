---
title: "aaaAzure IoT Suite e os aplicativos lógicos | Microsoft Docs"
description: "Um tutorial sobre como toohook a aplicativos lógicos tooAzure IoT Suite para processo de negócios."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Tutorial: Conectar-se a solução de monitoramento do Azure IoT Suite remoto pré-configurado do aplicativo lógico tooyour
Olá [Microsoft Azure IoT Suite] [ lnk-internetofthings] solução pré-configurada de monitoramento remoto é uma ótima maneira tooget iniciado rapidamente com um conjunto de recursos de ponta a ponta que um exemplo de uma solução de IoT. Este tutorial o orienta como monitoramento remoto de tooadd aplicativo lógico tooyour Microsoft Azure IoT Suite pré-configurado solução. Essas etapas demonstram como você pode tirar ainda mais sua solução de IoT conectando-se o processo de negócios tooa.

*Se você estiver procurando uma passo a passo sobre como tooprovision um monitoramento remoto pré-configurado solução, consulte [Tutorial: Introdução com soluções de IoT pré-configurado Olá][lnk-getstarted].*

Antes de iniciar este tutorial, você deve:

* Saudação de provisionar uma solução pré-configurada em sua assinatura do Azure de monitoramento remota.
* Criar um tooenable de conta do SendGrid toosend um email que dispara o processo de negócios. Você pode se inscrever para uma conta de avaliação gratuita no [SendGrid](https://sendgrid.com/) clicando em **Teste gratuitamente**. Depois que você registrou para sua conta de avaliação gratuita, você precisa toocreate um [chave API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) em SendGrid que concede permissões toosend mail. Você precisa esta chave de API mais tarde no tutorial de saudação.

toocomplete neste tutorial, você precisa que o Visual Studio 2015 ou Visual Studio de 2017 ações de saudação toomodify no back-end de solução pré-configurada hello.

Supondo que você já tiver provisionado o monitoramento remoto pré-configurado solução, navegue até toohello o grupo de recursos para a solução em Olá [portal do Azure][lnk-azureportal]. grupo de recursos de saudação tem Olá mesmo nome como hello solução o nome que você escolheu quando você provisionou sua solução de monitoramento remota. No grupo de recursos hello, você pode ver provisionado de saudação todos os recursos do Azure para sua solução, exceto Olá aplicativo do Active Directory do Azure que você pode encontrar no hello Portal clássico do Azure. Olá, seguinte captura de tela mostra um exemplo **grupo de recursos** folha de um monitoramento remoto pré-configurado solução:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, configurar Olá lógica aplicativo toouse com hello pré-configurado a solução.

## <a name="set-up-hello-logic-app"></a>Configurar Olá lógica de aplicativo
1. Clique em **adicionar** na parte superior de saudação da sua folha de grupo de recursos no hello portal do Azure.
2. Procure o **Aplicativo Lógico**, selecione-o e clique em **Criar**.
3. Preencha Olá **nome** e use Olá mesmo **assinatura** e **grupo de recursos** que você usou ao provisionar sua solução de monitoramento remota. Clique em **Criar**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Quando a implantação for concluída, você pode ver Olá que aplicativo lógico é listado como um recurso em seu grupo de recursos.
5. Clique Olá aplicativo lógico toonavigate toohello folha do aplicativo lógico, selecione Olá **aplicativo lógica em branco** saudação do modelo tooopen **lógica aplicativos Designer**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Escolha **Solicitar**. Essa ação especifica que uma solicitação HTTP de entrada com um carga no formato JSON específico atua como um gatilho.
7. Cole Olá código a seguir em Olá esquema de JSON de corpo de solicitação:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Você pode copiar a URL de saudação POST Olá HTTP após você salva o aplicativo de lógica de saudação, mas primeiro você deve adicionar uma ação.
   > 
   > 
8. Clique em **+ Nova etapa** no gatilho manual. Em seguida, clique em **Adicionar uma ação**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Procure **SendGrid – Enviar email** e clique nele.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Insira um nome para a conexão de saudação, como **SendGridConnection**, digite Olá **chave de API do SendGrid** você criou quando configurou sua conta do SendGrid e clique em **criar**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Adicionar endereços de email você Olá próprio tooboth **de** e **para** campos. Adicionar **alerta de monitoramento remota [DeviceId]** toohello **assunto** campo. Em Olá **corpo do Email** campo, adicione **[DeviceId] reportou [measurementName] com valor [measuredValue].** Você pode adicionar **[DeviceId]**, **[measurementName]**, e **[measuredValue]** clicando em Olá **você pode inserir dados de etapas anteriores**seção.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Clique em **salvar** no menu superior hello.
13. Clique em Olá **solicitação** Olá gatilho e cópia **Http Post toothis URL** valor. Você precisará dessa URL mais tarde neste tutorial.

> [!NOTE]
> Aplicativos lógicos habilitar toorun [muitos tipos diferentes de ação] [ lnk-logic-apps-actions] incluindo ações no Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Configurar Olá EventProcessor Web trabalho
Nesta seção, você pode se conectar toohello sua solução pré-configurada lógica de aplicativo que você criou. toocomplete nesta tarefa, você adiciona Olá tootrigger Olá aplicativo lógico toohello ação de URL que é acionado quando um valor do sensor de dispositivo excede um limite.

1. Usar o git cliente tooclone Olá versão mais recente do hello [azure-iot-monitoramento remoto repositório github][lnk-rmgithub]. Por exemplo:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. No Visual Studio, abra Olá **RemoteMonitoring.sln** de cópia local de saudação do repositório de saudação.
3. Olá abrir **ActionRepository.cs** arquivo hello **infraestrutura\\repositório** pasta.
4. Saudação de atualização **actionIds** dicionário com hello **Http Post toothis URL** você anotou do seu aplicativo lógico da seguinte maneira:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Salvar alterações de saudação na solução e sair do Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Implantar na linha de comando Olá
Nesta seção, você deve implantar a versão atualizada de saudação remoto monitoramento tooreplace Olá versão da solução atualmente em execução no Azure.

1. A seguir Olá [configuração de desenvolvimento] [ lnk-devsetup] tooset instruções seu ambiente para implantação.
2. toodeploy localmente, siga Olá [implantação local] [ lnk-localdeploy] instruções.
3. toodeploy toohello de nuvem e atualizar sua implantação de nuvem existente, siga Olá [implantação de nuvem] [ lnk-clouddeploy] instruções. Use o nome da sua implantação original como o nome da implantação Olá Olá. Por exemplo, se a implantação original Olá foi chamada **demologicapp**, use Olá comando a seguir:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Quando Olá compilar o script será executado, certifique-se de que toouse Olá mesmo instância do Active Directory que você usou ao provisionar solução hello, assinatura, região e conta do Azure.

## <a name="see-your-logic-app-in-action"></a>Ver seu aplicativo lógico em ação
Olá solução pré-configurada de monitoramento remoto tem duas regras definidas por padrão quando você provisiona uma solução. As regras são em Olá **SampleDevice001** dispositivo:

* Temperatura > 38,00
* Umidade > 48,00

regra de temperatura Olá dispara Olá **gerar alarme** regra de umidade de ação e hello dispara Olá **SendMessage** ação. Supondo que você usou Olá a mesma URL para ambos os Olá ações **ActionRepository** classe seus gatilhos de aplicativo lógica para a regra. As regras de usam o SendGrid toosend toohello um email **para** endereço com detalhes de alerta de saudação.

> [!NOTE]
> Olá lógica de aplicativo continua tootrigger sempre Olá limite é atingido. emails de desnecessários tooavoid, você pode desabilitar regras de saudação em sua solução portal ou desabilitar Olá lógica de aplicativo no hello [portal do Azure][lnk-azureportal].
> 
> 

Além disso tooreceiving emails, você também pode ver quando Olá lógica de aplicativo é executado no portal de saudação:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Próximas etapas
Agora que você usou um processo de negócios do aplicativo lógico tooconnect Olá pré-configurado solução tooa, você pode saber mais sobre opções de saudação para personalizar soluções Olá pré-configurados:

* [Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto][lnk-dynamic]
* [Metadados de informações de dispositivo no hello solução pré-configurada de monitoramento remoto][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
