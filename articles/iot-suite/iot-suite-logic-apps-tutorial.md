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
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="97f0e-103">Tutorial: Conectar-se a solução de monitoramento do Azure IoT Suite remoto pré-configurado do aplicativo lógico tooyour</span><span class="sxs-lookup"><span data-stu-id="97f0e-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="97f0e-104">Olá [Microsoft Azure IoT Suite] [ lnk-internetofthings] solução pré-configurada de monitoramento remoto é uma ótima maneira tooget iniciado rapidamente com um conjunto de recursos de ponta a ponta que um exemplo de uma solução de IoT.</span><span class="sxs-lookup"><span data-stu-id="97f0e-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="97f0e-105">Este tutorial o orienta como monitoramento remoto de tooadd aplicativo lógico tooyour Microsoft Azure IoT Suite pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="97f0e-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="97f0e-106">Essas etapas demonstram como você pode tirar ainda mais sua solução de IoT conectando-se o processo de negócios tooa.</span><span class="sxs-lookup"><span data-stu-id="97f0e-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="97f0e-107">*Se você estiver procurando uma passo a passo sobre como tooprovision um monitoramento remoto pré-configurado solução, consulte [Tutorial: Introdução com soluções de IoT pré-configurado Olá][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="97f0e-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="97f0e-108">Antes de iniciar este tutorial, você deve:</span><span class="sxs-lookup"><span data-stu-id="97f0e-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="97f0e-109">Saudação de provisionar uma solução pré-configurada em sua assinatura do Azure de monitoramento remota.</span><span class="sxs-lookup"><span data-stu-id="97f0e-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="97f0e-110">Criar um tooenable de conta do SendGrid toosend um email que dispara o processo de negócios.</span><span class="sxs-lookup"><span data-stu-id="97f0e-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="97f0e-111">Você pode se inscrever para uma conta de avaliação gratuita no [SendGrid](https://sendgrid.com/) clicando em **Teste gratuitamente**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="97f0e-112">Depois que você registrou para sua conta de avaliação gratuita, você precisa toocreate um [chave API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) em SendGrid que concede permissões toosend mail.</span><span class="sxs-lookup"><span data-stu-id="97f0e-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="97f0e-113">Você precisa esta chave de API mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="97f0e-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="97f0e-114">toocomplete neste tutorial, você precisa que o Visual Studio 2015 ou Visual Studio de 2017 ações de saudação toomodify no back-end de solução pré-configurada hello.</span><span class="sxs-lookup"><span data-stu-id="97f0e-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="97f0e-115">Supondo que você já tiver provisionado o monitoramento remoto pré-configurado solução, navegue até toohello o grupo de recursos para a solução em Olá [portal do Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="97f0e-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="97f0e-116">grupo de recursos de saudação tem Olá mesmo nome como hello solução o nome que você escolheu quando você provisionou sua solução de monitoramento remota.</span><span class="sxs-lookup"><span data-stu-id="97f0e-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="97f0e-117">No grupo de recursos hello, você pode ver provisionado de saudação todos os recursos do Azure para sua solução, exceto Olá aplicativo do Active Directory do Azure que você pode encontrar no hello Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="97f0e-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="97f0e-118">Olá, seguinte captura de tela mostra um exemplo **grupo de recursos** folha de um monitoramento remoto pré-configurado solução:</span><span class="sxs-lookup"><span data-stu-id="97f0e-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="97f0e-119">toobegin, configurar Olá lógica aplicativo toouse com hello pré-configurado a solução.</span><span class="sxs-lookup"><span data-stu-id="97f0e-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="97f0e-120">Configurar Olá lógica de aplicativo</span><span class="sxs-lookup"><span data-stu-id="97f0e-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="97f0e-121">Clique em **adicionar** na parte superior de saudação da sua folha de grupo de recursos no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="97f0e-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="97f0e-122">Procure o **Aplicativo Lógico**, selecione-o e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="97f0e-123">Preencha Olá **nome** e use Olá mesmo **assinatura** e **grupo de recursos** que você usou ao provisionar sua solução de monitoramento remota.</span><span class="sxs-lookup"><span data-stu-id="97f0e-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="97f0e-124">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="97f0e-125">Quando a implantação for concluída, você pode ver Olá que aplicativo lógico é listado como um recurso em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="97f0e-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="97f0e-126">Clique Olá aplicativo lógico toonavigate toohello folha do aplicativo lógico, selecione Olá **aplicativo lógica em branco** saudação do modelo tooopen **lógica aplicativos Designer**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="97f0e-127">Escolha **Solicitar**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-127">Select **Request**.</span></span> <span data-ttu-id="97f0e-128">Essa ação especifica que uma solicitação HTTP de entrada com um carga no formato JSON específico atua como um gatilho.</span><span class="sxs-lookup"><span data-stu-id="97f0e-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="97f0e-129">Cole Olá código a seguir em Olá esquema de JSON de corpo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="97f0e-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="97f0e-130">Você pode copiar a URL de saudação POST Olá HTTP após você salva o aplicativo de lógica de saudação, mas primeiro você deve adicionar uma ação.</span><span class="sxs-lookup"><span data-stu-id="97f0e-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="97f0e-131">Clique em **+ Nova etapa** no gatilho manual.</span><span class="sxs-lookup"><span data-stu-id="97f0e-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="97f0e-132">Em seguida, clique em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="97f0e-133">Procure **SendGrid – Enviar email** e clique nele.</span><span class="sxs-lookup"><span data-stu-id="97f0e-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="97f0e-134">Insira um nome para a conexão de saudação, como **SendGridConnection**, digite Olá **chave de API do SendGrid** você criou quando configurou sua conta do SendGrid e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="97f0e-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="97f0e-135">Adicionar endereços de email você Olá próprio tooboth **de** e **para** campos.</span><span class="sxs-lookup"><span data-stu-id="97f0e-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="97f0e-136">Adicionar **alerta de monitoramento remota [DeviceId]** toohello **assunto** campo.</span><span class="sxs-lookup"><span data-stu-id="97f0e-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="97f0e-137">Em Olá **corpo do Email** campo, adicione **[DeviceId] reportou [measurementName] com valor [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="97f0e-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="97f0e-138">Você pode adicionar **[DeviceId]**, **[measurementName]**, e **[measuredValue]** clicando em Olá **você pode inserir dados de etapas anteriores**seção.</span><span class="sxs-lookup"><span data-stu-id="97f0e-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="97f0e-139">Clique em **salvar** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="97f0e-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="97f0e-140">Clique em Olá **solicitação** Olá gatilho e cópia **Http Post toothis URL** valor.</span><span class="sxs-lookup"><span data-stu-id="97f0e-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="97f0e-141">Você precisará dessa URL mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="97f0e-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="97f0e-142">Aplicativos lógicos habilitar toorun [muitos tipos diferentes de ação] [ lnk-logic-apps-actions] incluindo ações no Office 365.</span><span class="sxs-lookup"><span data-stu-id="97f0e-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="97f0e-143">Configurar Olá EventProcessor Web trabalho</span><span class="sxs-lookup"><span data-stu-id="97f0e-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="97f0e-144">Nesta seção, você pode se conectar toohello sua solução pré-configurada lógica de aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="97f0e-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="97f0e-145">toocomplete nesta tarefa, você adiciona Olá tootrigger Olá aplicativo lógico toohello ação de URL que é acionado quando um valor do sensor de dispositivo excede um limite.</span><span class="sxs-lookup"><span data-stu-id="97f0e-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="97f0e-146">Usar o git cliente tooclone Olá versão mais recente do hello [azure-iot-monitoramento remoto repositório github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="97f0e-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="97f0e-147">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="97f0e-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="97f0e-148">No Visual Studio, abra Olá **RemoteMonitoring.sln** de cópia local de saudação do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="97f0e-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="97f0e-149">Olá abrir **ActionRepository.cs** arquivo hello **infraestrutura\\repositório** pasta.</span><span class="sxs-lookup"><span data-stu-id="97f0e-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="97f0e-150">Saudação de atualização **actionIds** dicionário com hello **Http Post toothis URL** você anotou do seu aplicativo lógico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="97f0e-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="97f0e-151">Salvar alterações de saudação na solução e sair do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97f0e-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="97f0e-152">Implantar na linha de comando Olá</span><span class="sxs-lookup"><span data-stu-id="97f0e-152">Deploy from hello command line</span></span>
<span data-ttu-id="97f0e-153">Nesta seção, você deve implantar a versão atualizada de saudação remoto monitoramento tooreplace Olá versão da solução atualmente em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="97f0e-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="97f0e-154">A seguir Olá [configuração de desenvolvimento] [ lnk-devsetup] tooset instruções seu ambiente para implantação.</span><span class="sxs-lookup"><span data-stu-id="97f0e-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="97f0e-155">toodeploy localmente, siga Olá [implantação local] [ lnk-localdeploy] instruções.</span><span class="sxs-lookup"><span data-stu-id="97f0e-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="97f0e-156">toodeploy toohello de nuvem e atualizar sua implantação de nuvem existente, siga Olá [implantação de nuvem] [ lnk-clouddeploy] instruções.</span><span class="sxs-lookup"><span data-stu-id="97f0e-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="97f0e-157">Use o nome da sua implantação original como o nome da implantação Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="97f0e-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="97f0e-158">Por exemplo, se a implantação original Olá foi chamada **demologicapp**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="97f0e-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="97f0e-159">Quando Olá compilar o script será executado, certifique-se de que toouse Olá mesmo instância do Active Directory que você usou ao provisionar solução hello, assinatura, região e conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="97f0e-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="97f0e-160">Ver seu aplicativo lógico em ação</span><span class="sxs-lookup"><span data-stu-id="97f0e-160">See your Logic App in action</span></span>
<span data-ttu-id="97f0e-161">Olá solução pré-configurada de monitoramento remoto tem duas regras definidas por padrão quando você provisiona uma solução.</span><span class="sxs-lookup"><span data-stu-id="97f0e-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="97f0e-162">As regras são em Olá **SampleDevice001** dispositivo:</span><span class="sxs-lookup"><span data-stu-id="97f0e-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="97f0e-163">Temperatura > 38,00</span><span class="sxs-lookup"><span data-stu-id="97f0e-163">Temperature > 38.00</span></span>
* <span data-ttu-id="97f0e-164">Umidade > 48,00</span><span class="sxs-lookup"><span data-stu-id="97f0e-164">Humidity > 48.00</span></span>

<span data-ttu-id="97f0e-165">regra de temperatura Olá dispara Olá **gerar alarme** regra de umidade de ação e hello dispara Olá **SendMessage** ação.</span><span class="sxs-lookup"><span data-stu-id="97f0e-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="97f0e-166">Supondo que você usou Olá a mesma URL para ambos os Olá ações **ActionRepository** classe seus gatilhos de aplicativo lógica para a regra.</span><span class="sxs-lookup"><span data-stu-id="97f0e-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="97f0e-167">As regras de usam o SendGrid toosend toohello um email **para** endereço com detalhes de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="97f0e-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="97f0e-168">Olá lógica de aplicativo continua tootrigger sempre Olá limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="97f0e-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="97f0e-169">emails de desnecessários tooavoid, você pode desabilitar regras de saudação em sua solução portal ou desabilitar Olá lógica de aplicativo no hello [portal do Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="97f0e-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="97f0e-170">Além disso tooreceiving emails, você também pode ver quando Olá lógica de aplicativo é executado no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="97f0e-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="97f0e-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97f0e-171">Next steps</span></span>
<span data-ttu-id="97f0e-172">Agora que você usou um processo de negócios do aplicativo lógico tooconnect Olá pré-configurado solução tooa, você pode saber mais sobre opções de saudação para personalizar soluções Olá pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="97f0e-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="97f0e-173">[Usar a telemetria dinâmica com hello solução pré-configurada de monitoramento remoto][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="97f0e-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="97f0e-174">[Metadados de informações de dispositivo no hello solução pré-configurada de monitoramento remoto][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="97f0e-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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
