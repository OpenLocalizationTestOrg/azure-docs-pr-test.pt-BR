---
title: "tempo de aaaReal visualização de dados de sensor do seu hub IoT do Azure – aplicativos Web | Microsoft Docs"
description: "Use o recurso de aplicativos Web de saudação do serviço de aplicativo do Microsoft Azure toovisualize temperatura e umidade dados coletados de sensor hello e enviados tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualização de dados em tempo real, visualização de dados dinâmicos, visualização de dados de sensor"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="7311c-104">Visualizar os dados de sensor em tempo real de seu hub IoT do Azure usando o recurso de aplicativos Web de saudação do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7311c-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="7311c-106">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7311c-106">What you learn</span></span>

<span data-ttu-id="7311c-107">Neste tutorial, você aprenderá como dados de sensor em tempo real toovisualize que recebe o hub IoT executando um aplicativo web que são hospedados em um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="7311c-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="7311c-108">Se quiser tootry toovisualize Olá dados em seu hub IoT usando o Power BI, consulte [dados de sensor em tempo real de toovisualize usar o Power BI do Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="7311c-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7311c-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="7311c-109">What you do</span></span>

- <span data-ttu-id="7311c-110">Crie um aplicativo web no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7311c-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="7311c-111">Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="7311c-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="7311c-112">Configure dados do sensor Olá web aplicativo tooread do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7311c-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="7311c-113">Carregar um toobe de aplicativo web hospedado pelo aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="7311c-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="7311c-114">Abra Olá web toosee em tempo real temperatura e umidade dados de aplicativo do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7311c-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7311c-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7311c-115">What you need</span></span>

- <span data-ttu-id="7311c-116">[Configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), que abrange Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7311c-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="7311c-117">Uma assinatura ativa do Azure</span><span class="sxs-lookup"><span data-stu-id="7311c-117">An active Azure subscription</span></span>
  - <span data-ttu-id="7311c-118">Um Hub IoT em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="7311c-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="7311c-119">Um aplicativo cliente que envia o hub de Iot tooyour mensagens</span><span class="sxs-lookup"><span data-stu-id="7311c-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="7311c-120">Baixar Git</span><span class="sxs-lookup"><span data-stu-id="7311c-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="7311c-121">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="7311c-121">Create a web app</span></span>

1. <span data-ttu-id="7311c-122">Em Olá [portal do Azure](https://ms.portal.azure.com/), clique em **novo** > **Web + móvel** > **aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="7311c-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="7311c-123">Insira um nome exclusivo do trabalho, verifique se a assinatura de saudação, especifique um grupo de recursos e um local, selecione **Pin toodashboard**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="7311c-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="7311c-124">Recomendamos que você selecione Olá mesmo local que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7311c-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="7311c-125">Isso ajuda a velocidade de processamento e reduz o custo de saudação de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="7311c-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Criar um aplicativo Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="7311c-127">Configurar Olá web aplicativo tooread dados do seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="7311c-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="7311c-128">Abra o aplicativo de web de saudação que tiver acabado de provisionar.</span><span class="sxs-lookup"><span data-stu-id="7311c-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="7311c-129">Clique em **configurações do aplicativo**e, em seguida, em **configurações do aplicativo**, adicionar Olá pares chave/valor a seguir:</span><span class="sxs-lookup"><span data-stu-id="7311c-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="7311c-130">Chave</span><span class="sxs-lookup"><span data-stu-id="7311c-130">Key</span></span>                                   | <span data-ttu-id="7311c-131">Valor</span><span class="sxs-lookup"><span data-stu-id="7311c-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="7311c-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="7311c-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="7311c-133">Obtido de iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="7311c-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="7311c-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="7311c-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="7311c-135">nome de saudação do grupo de consumidores Olá que você adicione tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="7311c-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Adicionar configurações tooyour web app com pares chave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="7311c-137">Clique em **configurações do aplicativo**, em **configurações gerais**, Olá alternância **Web sockets** opção e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7311c-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Saudação de ativar/desativar opção de soquetes da Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="7311c-139">Carregar um toobe de aplicativo web hospedado pelo aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="7311c-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="7311c-140">No GitHub, foi disponibilizado um aplicativo Web que exibe dados de sensor em tempo real obtidos do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7311c-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="7311c-141">Você só precisa toodo é configurar Olá web aplicativo toowork com um repositório Git, baixar o aplicativo da web de saudação do GitHub e, em seguida, carregá-lo tooAzure para toohost de aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="7311c-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="7311c-142">No aplicativo da web de saudação, clique em **opções de implantação** > **Escolher fonte** > **repositório Git Local**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="7311c-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurar o repositório do Git web app implantação toouse Olá local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="7311c-144">Clique em **credenciais de implantação**, crie um usuário nome e senha toouse tooconnect toohello repositório Git no Azure e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7311c-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="7311c-145">Clique em **visão geral**e observe o valor de saudação do **url de clone de Git**.</span><span class="sxs-lookup"><span data-stu-id="7311c-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Obter URL de clone de Git de saudação do seu aplicativo web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="7311c-147">Abra uma janela de terminal ou de comando no computador local.</span><span class="sxs-lookup"><span data-stu-id="7311c-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="7311c-148">Baixar o aplicativo da web de saudação do GitHub e carregá-lo tooAzure para toohost de aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="7311c-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="7311c-149">toodo caso, execute hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7311c-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="7311c-150">\<URL de clone de Git\> é Olá URL do repositório do Git Olá encontrado no hello **visão geral** página do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="7311c-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="7311c-151">Abrir Olá web toosee em tempo real temperatura e umidade dados de aplicativo do seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="7311c-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="7311c-152">Em Olá **visão geral** página do seu aplicativo web, clique em Olá URL tooopen Olá web app.</span><span class="sxs-lookup"><span data-stu-id="7311c-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Obter URL de saudação do seu aplicativo web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="7311c-154">Você deve ver dados de umidade e temperatura de saudação em tempo real do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7311c-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Página de aplicativo Web mostrando a umidade e a temperatura em tempo real](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="7311c-156">Certifique-se de que o aplicativo de exemplo hello está em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7311c-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="7311c-157">Se não, você receberá um gráfico em branco, você poderá consultar toohello tutoriais em [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7311c-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7311c-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7311c-158">Next steps</span></span>
<span data-ttu-id="7311c-159">Você usou com êxito seus dados de sensor em tempo real de toovisualize de aplicativo da web do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7311c-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="7311c-160">Para um modo alternativo toovisualize de dados do Azure IoT Hub, consulte [dados de sensor em tempo real de toovisualize usar o Power BI de seu hub IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="7311c-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
