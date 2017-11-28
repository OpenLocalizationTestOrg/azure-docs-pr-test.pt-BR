---
title: "Visualização de dados em tempo real de dados de sensor do seu Hub IoT do Azure – aplicativos Web | Microsoft Docs"
description: "Use a funcionalidade do aplicativo Web do Serviço de Aplicativo do Microsoft Azure para visualizar dados de temperatura e umidade que são coletados do sensor e enviados para o seu Hub IoT."
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
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="6af68-104">Visualizar dados do sensor em tempo real de seu Hub IoT do Azure usando a funcionalidade de aplicativos Web do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="6af68-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="6af68-106">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="6af68-106">What you learn</span></span>

<span data-ttu-id="6af68-107">Neste tutorial, você aprenderá como visualizar dados de sensor em tempo real que o seu Hub IoT recebe por meio da execução de um aplicativo Web hospedado em um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6af68-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="6af68-108">Se você quiser tentar visualizar os dados em seu Hub IoT usando o Power BI, consulte [Usar o Power BI para visualizar dados de sensor em tempo real do Hub IoT do Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6af68-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6af68-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="6af68-109">What you do</span></span>

- <span data-ttu-id="6af68-110">Criar um aplicativo Web no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6af68-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="6af68-111">Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="6af68-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="6af68-112">Configurar o aplicativo Web para ler dados de sensor de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6af68-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="6af68-113">Carregar um aplicativo Web a ser hospedado pelo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6af68-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="6af68-114">Abrir o aplicativo Web para ver os dados de temperatura e umidade em tempo real de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6af68-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6af68-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="6af68-115">What you need</span></span>

- <span data-ttu-id="6af68-116">[Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) que aborda os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="6af68-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="6af68-117">Uma assinatura ativa do Azure</span><span class="sxs-lookup"><span data-stu-id="6af68-117">An active Azure subscription</span></span>
  - <span data-ttu-id="6af68-118">Um Hub IoT em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="6af68-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="6af68-119">Um aplicativo cliente que envia mensagens para o seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="6af68-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="6af68-120">Baixar Git</span><span class="sxs-lookup"><span data-stu-id="6af68-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="6af68-121">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="6af68-121">Create a web app</span></span>

1. <span data-ttu-id="6af68-122">No [Portal do Azure](https://ms.portal.azure.com/), clique em **Novo** > **Web + Móvel** > **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="6af68-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="6af68-123">Insira um nome de trabalho exclusivo, verifique a assinatura, especifique um grupo de recursos e um local, selecione **Fixar no painel** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6af68-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="6af68-124">Recomendamos que você selecione o mesmo local do seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6af68-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="6af68-125">Isso ajuda a aumentar a velocidade de processamento e reduzir os custos de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="6af68-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![Criar um aplicativo Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="6af68-127">Configurar o aplicativo Web para ler dados de sensor de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="6af68-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="6af68-128">Abra o aplicativo Web que você acabou de provisionar.</span><span class="sxs-lookup"><span data-stu-id="6af68-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="6af68-129">Clique em **Configurações do aplicativo** e, em seguida, adicione os seguintes pares chave/valor em **Configurações do aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="6af68-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="6af68-130">Chave</span><span class="sxs-lookup"><span data-stu-id="6af68-130">Key</span></span>                                   | <span data-ttu-id="6af68-131">Valor</span><span class="sxs-lookup"><span data-stu-id="6af68-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="6af68-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="6af68-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="6af68-133">Obtido de iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="6af68-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="6af68-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="6af68-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="6af68-135">O nome do grupo de consumidores que você adiciona ao seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="6af68-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![Adicionar configurações ao seu aplicativo Web com pares chave/valor](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="6af68-137">Clique em **Configurações do aplicativo**, em **Configurações gerais**, alternar a opção de **soquetes da Web** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6af68-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![Alternar a opção de soquetes da Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="6af68-139">Carregar um aplicativo Web a ser hospedado pelo aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="6af68-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="6af68-140">No GitHub, foi disponibilizado um aplicativo Web que exibe dados de sensor em tempo real obtidos do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6af68-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="6af68-141">Tudo que você precisa fazer é configurar o aplicativo Web para trabalhar com um repositório Git, baixar o aplicativo Web do GitHub e carregá-lo no Azure para ser hospedado pelo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6af68-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="6af68-142">No aplicativo Web, clique em **Opções de Implantação** > **Escolher Fonte** > **Repositório Git Local**, e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6af68-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurar a implantação do seu aplicativo Web para usar o repositório Git local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="6af68-144">Clique em **Credenciais de Implantação**, crie um nome de usuário e senha que serão usados para conexão ao repositório Git no Azure e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6af68-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="6af68-145">Clique em **Visão geral** e anote o valor de **URL de clone do Git**.</span><span class="sxs-lookup"><span data-stu-id="6af68-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![Obter a URL de clone do Git de seu aplicativo Web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="6af68-147">Abra uma janela de terminal ou de comando no computador local.</span><span class="sxs-lookup"><span data-stu-id="6af68-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="6af68-148">Baixe o aplicativo Web do GitHub e carregue-o no Azure para ser hospedado pelo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6af68-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="6af68-149">Para fazer isso, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6af68-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="6af68-150">\<URL de clone do Git\> é a URL do repositório Git encontrado na página **Visão geral** do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6af68-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="6af68-151">Abrir o aplicativo Web para ver os dados de temperatura e umidade em tempo real de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="6af68-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="6af68-152">Na página **Visão geral** do seu aplicativo Web, clique na URL para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="6af68-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![Obter a URL do seu aplicativo web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="6af68-154">Você deve ver os dados de temperatura e umidade em tempo real de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6af68-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![Página de aplicativo Web mostrando a umidade e a temperatura em tempo real](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="6af68-156">Verifique se o aplicativo de exemplo está em execução em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6af68-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="6af68-157">Se não, você receberá um gráfico em branco, você pode consultar os tutoriais em [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6af68-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6af68-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6af68-158">Next steps</span></span>
<span data-ttu-id="6af68-159">Você usou com êxito seu aplicativo Web para visualizar dados do sensor em tempo real do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6af68-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="6af68-160">Para obter um modo alternativo para visualizar os dados de Hub IoT do Azure, consulte [Usar o Power BI para visualizar dados de sensor em tempo real do seu Hub IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6af68-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
