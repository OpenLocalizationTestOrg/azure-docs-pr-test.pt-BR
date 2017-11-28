---
title: "suplemento aaaExcel para serviços Web de aprendizado de máquina | Microsoft Docs"
description: "Como toouse da Web de aprendizado de máquina do Azure services diretamente no Excel sem gravar qualquer código."
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
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="0bd67-103">Suplemento do Excel para serviços Web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0bd67-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="0bd67-104">Excel torna fácil toocall os serviços da web diretamente sem Olá necessidade toowrite qualquer código.</span><span class="sxs-lookup"><span data-stu-id="0bd67-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="0bd67-105">Etapas tooUse um serviço da web existente na pasta de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="0bd67-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="0bd67-106">Olá abrir [arquivo do Excel de exemplo](http://aka.ms/amlexcel-sample-2), que contém Olá complemento do Excel e dados sobre em detrimento de passageiros Olá Titanic.</span><span class="sxs-lookup"><span data-stu-id="0bd67-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="0bd67-107">Escolha o serviço web de saudação clicando nele-"Titanic sobrevivente indicador (suplemento do Excel exemplo) [pontuação]" neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="0bd67-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Selecionar o serviço Web][01]
3. <span data-ttu-id="0bd67-109">Isso leva você toohello **prever** seção.</span><span class="sxs-lookup"><span data-stu-id="0bd67-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="0bd67-110">Esta pasta de trabalho já contém dados de exemplo, mas para uma pasta de trabalho em branco você pode selecionar uma célula no Excel e clicar em **Usar dados de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="0bd67-111">Selecionar dados de saudação com cabeçalhos e clique em ícone de intervalo de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="0bd67-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="0bd67-112">Certifique-se de hello "Meus dados têm cabeçalhos" caixa está marcada.</span><span class="sxs-lookup"><span data-stu-id="0bd67-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="0bd67-113">Em **saída**, insira o número de célula Olá onde você deseja Olá toobe de saída, por exemplo "H1" aqui.</span><span class="sxs-lookup"><span data-stu-id="0bd67-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="0bd67-114">Clique em **Prever**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-114">Click **Predict**.</span></span>
   
    ![Seção Prever][02]

<span data-ttu-id="0bd67-116">Implante um serviço Web ou use um serviço Web existente.</span><span class="sxs-lookup"><span data-stu-id="0bd67-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="0bd67-117">Para obter mais informações sobre como implantar um serviço web, consulte [passo a passo etapa 5: implantar o serviço de Web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0bd67-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="0bd67-118">Obter chave de API de saudação para o serviço web.</span><span class="sxs-lookup"><span data-stu-id="0bd67-118">Get hello API key for your web service.</span></span> <span data-ttu-id="0bd67-119">O local em que você executa essa ação depende se você publicou um serviço Web Clássico do Machine Learning ou um Novo serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0bd67-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="0bd67-120">**Usar um serviço Web Clássico**</span><span class="sxs-lookup"><span data-stu-id="0bd67-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="0bd67-121">No estúdio de aprendizado de máquina, clique em Olá **serviços WEB** seção no painel esquerdo do hello e, em seguida, selecione Olá web service.</span><span class="sxs-lookup"><span data-stu-id="0bd67-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Selecione um serviço Web do Studio][04]
2. <span data-ttu-id="0bd67-123">Copie a chave de API de Olá para o serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bd67-123">Copy hello API key for hello web service.</span></span>
   
    ![Chave de API do Studio][05]
3. <span data-ttu-id="0bd67-125">Em Olá **painel** para serviço web de saudação, clique em Olá **solicitação/resposta** link.</span><span class="sxs-lookup"><span data-stu-id="0bd67-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="0bd67-126">Procure Olá **URI da solicitação** seção.</span><span class="sxs-lookup"><span data-stu-id="0bd67-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="0bd67-127">Copie e salve a URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bd67-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="0bd67-128">Agora é possível toosign em Olá [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) tooobtain portal chave de API de saudação para um serviço web de aprendizado de máquina clássico.</span><span class="sxs-lookup"><span data-stu-id="0bd67-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="0bd67-129">**Usar um Novo serviço Web**</span><span class="sxs-lookup"><span data-stu-id="0bd67-129">**Use a New web service**</span></span>

1. <span data-ttu-id="0bd67-130">Em Olá [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) portal, clique **serviços Web**, em seguida, selecione o serviço da web.</span><span class="sxs-lookup"><span data-stu-id="0bd67-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="0bd67-131">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-131">Click **Consume**.</span></span>
3. <span data-ttu-id="0bd67-132">Procure Olá **informações básicas de consumo** seção.</span><span class="sxs-lookup"><span data-stu-id="0bd67-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="0bd67-133">Copie e salve Olá **chave primária** e hello **solicitação-resposta** URL.</span><span class="sxs-lookup"><span data-stu-id="0bd67-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="0bd67-134">Etapas tooAdd um novo serviço da web</span><span class="sxs-lookup"><span data-stu-id="0bd67-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="0bd67-135">Implante um serviço Web ou use um serviço Web existente.</span><span class="sxs-lookup"><span data-stu-id="0bd67-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="0bd67-136">Para obter mais informações sobre como implantar um serviço web, consulte [passo a passo etapa 5: implantar o serviço de Web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0bd67-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="0bd67-137">Clique em **Consumo**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-137">Click **Consume**.</span></span>
3. <span data-ttu-id="0bd67-138">Procure Olá **informações básicas de consumo** seção.</span><span class="sxs-lookup"><span data-stu-id="0bd67-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="0bd67-139">Copie e salve Olá **chave primária** e hello **solicitação-resposta** URL.</span><span class="sxs-lookup"><span data-stu-id="0bd67-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="0bd67-140">No Excel, vá toohello **serviços Web** seção (se você estiver no hello **prever** seção, clique em Olá seta Voltar toogo toohello lista de serviços da web).</span><span class="sxs-lookup"><span data-stu-id="0bd67-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Vá tooWeb seleção de serviço][03]
5. <span data-ttu-id="0bd67-142">Clique em **Adicionar Serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="0bd67-143">Cole URL Olá Olá rotulada de caixa de texto de suplemento do Excel **URL**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="0bd67-144">Chave de API/primário Olá colar na caixa de texto de saudação rotulada **chave API**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="0bd67-145">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0bd67-145">Click **Add**.</span></span>
   
    ![URL e chave de API para um serviço Web clássico.][06]
9. <span data-ttu-id="0bd67-147">toouse serviço de web Olá, siga Olá anterior direções, "Etapas tooUse um serviço da web do existente."</span><span class="sxs-lookup"><span data-stu-id="0bd67-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="0bd67-148">Compartilhar sua pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="0bd67-148">Sharing Your Workbook</span></span>
<span data-ttu-id="0bd67-149">Se você salvar sua pasta de trabalho, chave de API/primário Olá Olá serviços da web que você adicionou também serão salvos.</span><span class="sxs-lookup"><span data-stu-id="0bd67-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="0bd67-150">Isso significa que você somente deve compartilhar pasta de trabalho de saudação com pessoas que confiáveis.</span><span class="sxs-lookup"><span data-stu-id="0bd67-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="0bd67-151">Qualquer perguntas em Olá seguinte seção de comentários ou, no nosso [fórum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0bd67-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
