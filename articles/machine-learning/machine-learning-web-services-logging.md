---
title: "Registro em log de serviços Web do Machine Learning | Microsoft Azure"
description: "Saiba como habilitar o registro em log de serviços Web de Machine Learning. O registro em log fornece informações adicionais para ajudar a solucionar problemas com as APIs."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="41f34-104">Habilitar o log de serviços Web de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="41f34-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="41f34-105">Este documento fornece informações sobre o recurso de logs de serviços Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="41f34-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="41f34-106">Os logs fornecem informações adicionais, além de apenas um número de erro e uma mensagem, o que pode ajudar a solucionar suas chamadas para as APIs de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="41f34-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="41f34-107">Como habilitar o registro em log para um serviço Web</span><span class="sxs-lookup"><span data-stu-id="41f34-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="41f34-108">Você hara habilita os logs no portal de [serviços Web do Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="41f34-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="41f34-109">Entre no portal de Serviços Web do Azure Machine Learning em [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="41f34-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="41f34-110">Para um serviço Web Clássico, você também pode acessar o portal clicando em **Nova Experiência de Serviços Web** na página de Serviços Web do Machine Learning no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="41f34-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Novo link de Experiência dos Serviços Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="41f34-112">Na barra de menus superior, clique em **Serviços Web** para um novo serviço Web ou clique em **Serviços Web Clássicos** para um serviço Web Clássico.</span><span class="sxs-lookup"><span data-stu-id="41f34-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selecione serviços Web Novos ou Clássicos](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="41f34-114">Para um novo serviço Web, clique no nome de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="41f34-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="41f34-115">Para um serviço Web Clássico, clique no nome do serviço Web e clique no ponto de extremidade apropriado na próxima página.</span><span class="sxs-lookup"><span data-stu-id="41f34-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="41f34-116">Na barra de menus superior, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="41f34-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="41f34-117">Defina a opção **Habilitar Log** como *Erro* (para registrar somente erros) ou *Todos* (para registro em log completo).</span><span class="sxs-lookup"><span data-stu-id="41f34-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Selecionar o nível de log](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="41f34-119">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="41f34-119">Click **Save**.</span></span>

7. <span data-ttu-id="41f34-120">Para os serviços Web Clássicos, crie o contêiner **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="41f34-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="41f34-121">Todos os logs de serviço Web são mantidos em um contêiner de blob denominado **ml diagnóstico** na conta de armazenamento associada ao serviço Web.</span><span class="sxs-lookup"><span data-stu-id="41f34-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="41f34-122">Para novos serviços Web, esse contêiner é criado na primeira vez que você acessa o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="41f34-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="41f34-123">Para serviços Web Clássico, você precisa criar o contêiner, se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="41f34-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="41f34-124">No [portal do Azure](https://portal.azure.com), vá para a conta de armazenamento associada ao serviço Web.</span><span class="sxs-lookup"><span data-stu-id="41f34-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="41f34-125">Em **Serviço Blob**, clique em **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="41f34-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="41f34-126">Se o contêiner **ml-diagnostics** não existir, clique em **+Contêiner**, dê ao contêiner o nome "ml-diagnostics" e selecione o **Tipo de acesso** como "Blob".</span><span class="sxs-lookup"><span data-stu-id="41f34-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="41f34-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41f34-127">Click **OK**.</span></span>

      ![Selecionar o nível de log](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="41f34-129">Para um serviço Web Clássico, o Painel de Serviços Web no Machine Learning Studio também tem uma opção para habilitar o log.</span><span class="sxs-lookup"><span data-stu-id="41f34-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="41f34-130">No entanto, como os logs são gerenciados por meio do portal de serviços Web, você precisa habilitar os logs por meio do portal, conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="41f34-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="41f34-131">Se você tiver habilitado os logs no Studio, no Portal de Serviços Web, desabilite os logs e habilite-os novamente.</span><span class="sxs-lookup"><span data-stu-id="41f34-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="41f34-132">Os efeitos de habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="41f34-132">The effects of enabling logging</span></span>
<span data-ttu-id="41f34-133">Quando o log estiver habilitado, os diagnósticos e erros do ponto de extremidade de serviço Web serão registrados no contêiner de blobs **ml-diagnostics** na Conta de Armazenamento do Azure vinculada ao espaço de trabalho do usuário.</span><span class="sxs-lookup"><span data-stu-id="41f34-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="41f34-134">Esse contêiner armazena todas as informações de diagnóstico para todos os pontos de extremidade do serviço da Web para todos os espaços de trabalho associados a esta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="41f34-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="41f34-135">Os logs podem ser exibidos usando qualquer uma das várias ferramentas disponíveis para explorar uma Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="41f34-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="41f34-136">A maneira mais fácil possível de navegar para a conta de armazenamento no portal do Azure: clique em **Contêineres** e clique no contêiner **ml diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="41f34-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="41f34-137">Informações detalhadas do log blob</span><span class="sxs-lookup"><span data-stu-id="41f34-137">Log blob detail information</span></span>
<span data-ttu-id="41f34-138">Cada blob no contêiner contém as informações de diagnóstico para um das seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="41f34-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="41f34-139">Uma execução do método Batch-Execution</span><span class="sxs-lookup"><span data-stu-id="41f34-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="41f34-140">Uma execução do método Request-Response</span><span class="sxs-lookup"><span data-stu-id="41f34-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="41f34-141">Inicialização de um contêiner de Request-Response</span><span class="sxs-lookup"><span data-stu-id="41f34-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="41f34-142">O nome de cada blob tem um prefixo da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="41f34-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="41f34-143">Sendo que _Tipo de log_ assume um dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="41f34-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="41f34-144">lote</span><span class="sxs-lookup"><span data-stu-id="41f34-144">batch</span></span>  
* <span data-ttu-id="41f34-145">pontuação/solicitações</span><span class="sxs-lookup"><span data-stu-id="41f34-145">score/requests</span></span>  
* <span data-ttu-id="41f34-146">pontuação/init</span><span class="sxs-lookup"><span data-stu-id="41f34-146">score/init</span></span>  

