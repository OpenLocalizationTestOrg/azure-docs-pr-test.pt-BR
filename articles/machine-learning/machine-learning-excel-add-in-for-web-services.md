---
title: "Suplemento do Excel para serviços Web do Machine Learning | Microsoft Docs"
description: "Como usar os serviços Web do Azure Machine Learning diretamente no Excel sem escrever nenhum código."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="4d1d7-103">Suplemento do Excel para serviços Web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4d1d7-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="4d1d7-104">O Excel torna fácil chamar serviços Web diretamente, sem a necessidade de escrever nenhum código.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="4d1d7-105">Etapas para usar um serviço Web existente na pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="4d1d7-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="4d1d7-106">Abra o [arquivo de exemplo do Excel](http://aka.ms/amlexcel-sample-2), que contém o suplemento do Excel e os dados sobre passageiros do Titanic.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="4d1d7-107">Escolha o serviço Web clicando nele - "Titanic Survivor Predictor (exemplo de suplemento do Excel) [Pontuação]" neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Selecionar o serviço Web][01]
3. <span data-ttu-id="4d1d7-109">Isso levará você à seção **Prever**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="4d1d7-110">Esta pasta de trabalho já contém dados de exemplo, mas para uma pasta de trabalho em branco você pode selecionar uma célula no Excel e clicar em **Usar dados de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="4d1d7-111">Selecione os dados com cabeçalhos e clique no ícone de intervalo de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="4d1d7-112">Verifique se a caixa "Meus dados contêm cabeçalhos" está marcada.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="4d1d7-113">Em **Saída**, insira o número da célula em que você deseja colocar a saída, por exemplo, "H1" aqui.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="4d1d7-114">Clique em **Prever**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-114">Click **Predict**.</span></span>
   
    ![Seção Prever][02]

<span data-ttu-id="4d1d7-116">Implante um serviço Web ou use um serviço Web existente.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="4d1d7-117">Para obter mais informações sobre como implantar um serviço Web, consulte [Passo a passo – Etapa 5: Implantar o serviço Web do Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4d1d7-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="4d1d7-118">Obtenha a chave de API para o seu serviço Web.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-118">Get the API key for your web service.</span></span> <span data-ttu-id="4d1d7-119">O local em que você executa essa ação depende se você publicou um serviço Web Clássico do Machine Learning ou um Novo serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="4d1d7-120">**Usar um serviço Web Clássico**</span><span class="sxs-lookup"><span data-stu-id="4d1d7-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="4d1d7-121">No Machine Learning Studio, clique na seção **SERVIÇOS WEB** no painel esquerdo e selecione o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Selecione um serviço Web do Studio][04]
2. <span data-ttu-id="4d1d7-123">Copie a chave de API para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-123">Copy the API key for the web service.</span></span>
   
    ![Chave de API do Studio][05]
3. <span data-ttu-id="4d1d7-125">Na guia **PAINEL** do serviço Web, clique no link **SOLICITAÇÃO/RESPOSTA**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="4d1d7-126">Procure a seção **URI da solicitação** .</span><span class="sxs-lookup"><span data-stu-id="4d1d7-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="4d1d7-127">Copie e salve a URL.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="4d1d7-128">Agora é possível entrar no portal dos [Serviços Web do Azure Machine Learning](https://services.azureml.net) para obter a chave de API para um serviço Web Clássico do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="4d1d7-129">**Usar um Novo serviço Web**</span><span class="sxs-lookup"><span data-stu-id="4d1d7-129">**Use a New web service**</span></span>

1. <span data-ttu-id="4d1d7-130">No portal dos [Serviços Web do Azure Machine Learning](https://services.azureml.net), clique em **Serviços Web** e selecione o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="4d1d7-131">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-131">Click **Consume**.</span></span>
3. <span data-ttu-id="4d1d7-132">Procure a seção **Informações básicas de consumo** .</span><span class="sxs-lookup"><span data-stu-id="4d1d7-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="4d1d7-133">Copie e salve a **Chave primária** e a URL de **solicitação-resposta**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="4d1d7-134">Etapas para adicionar um Novo serviço Web</span><span class="sxs-lookup"><span data-stu-id="4d1d7-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="4d1d7-135">Implante um serviço Web ou use um serviço Web existente.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="4d1d7-136">Para obter mais informações sobre como implantar um serviço Web, consulte [Passo a passo – Etapa 5: Implantar o serviço Web do Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4d1d7-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="4d1d7-137">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-137">Click **Consume**.</span></span>
3. <span data-ttu-id="4d1d7-138">Procure a seção **Informações básicas de consumo** .</span><span class="sxs-lookup"><span data-stu-id="4d1d7-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="4d1d7-139">Copie e salve a **Chave primária** e a URL de **solicitação-resposta**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="4d1d7-140">No Excel, vá para a seção **Serviços Web** (se você estiver na seção **Prever**, clique na seta para voltar para ir para a lista de serviços Web).</span><span class="sxs-lookup"><span data-stu-id="4d1d7-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Vá para a seleção de serviço Web][03]
5. <span data-ttu-id="4d1d7-142">Clique em **Adicionar Serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="4d1d7-143">Cole a URL na caixa de texto do complemento do Excel chamada **URL**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="4d1d7-144">Cole a chave de API/primária na caixa de texto chamada **Chave de API**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="4d1d7-145">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-145">Click **Add**.</span></span>
   
    ![URL e chave de API para um serviço Web clássico.][06]
9. <span data-ttu-id="4d1d7-147">Para usar o serviço Web, siga as instruções anteriores de “Etapas para usar um serviço Web existente”.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="4d1d7-148">Compartilhar sua pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="4d1d7-148">Sharing Your Workbook</span></span>
<span data-ttu-id="4d1d7-149">Se você salvar sua pasta de trabalho, as chaves de API/primária dos serviços Web adicionados também serão salvas.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="4d1d7-150">Isso significa que você só deve compartilhar a pasta de trabalho com pessoas confiáveis.</span><span class="sxs-lookup"><span data-stu-id="4d1d7-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="4d1d7-151">Faça suas perguntas na seção de comentário abaixo ou em nosso [fórum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4d1d7-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
