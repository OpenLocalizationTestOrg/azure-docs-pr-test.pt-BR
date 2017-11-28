---
title: "aaaLogging para serviços web do aprendizado de máquina | Microsoft Docs"
description: "Saiba como serviços da web de registro em log tooenable para aprendizado de máquina. Registro em log informações adicionais toohelp Olá APIs de solução de problemas."
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
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="d5c30-104">Habilitar o log de serviços Web de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d5c30-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="d5c30-105">Este documento fornece informações sobre Olá log capacidade de serviços web do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d5c30-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="d5c30-106">Registro em log informações adicionais, além de um número de erro e uma mensagem, que pode ajudá-lo a solucionar problemas de seu toohello chama APIs de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d5c30-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="d5c30-107">Como o log tooenable para um serviço Web</span><span class="sxs-lookup"><span data-stu-id="d5c30-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="d5c30-108">Habilitar o registro de saudação [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="d5c30-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="d5c30-109">Entrar no portal de serviços de Web de aprendizado de máquina do Azure toohello em [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="d5c30-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="d5c30-110">Para um serviço web clássico, você também pode obter toohello portal clicando **nova experiência de serviços Web** na página de serviços de Web do aprendizado de máquina Olá no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d5c30-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Novo link de Experiência dos Serviços Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="d5c30-112">Na barra de menus superior hello, clique em **serviços Web** para um novo serviço da web, ou clique em **Web Services clássico** para um clássico de serviço web.</span><span class="sxs-lookup"><span data-stu-id="d5c30-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selecione serviços Web Novos ou Clássicos](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="d5c30-114">Para um novo serviço da web, clique em nome do serviço web hello.</span><span class="sxs-lookup"><span data-stu-id="d5c30-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="d5c30-115">Para um serviço web clássico, clique em nome do serviço web hello e clique em ponto de extremidade apropriado Olá na próxima página de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5c30-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="d5c30-116">Na barra de menus superior hello, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="d5c30-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="d5c30-117">Saudação de conjunto **Habilitar log** opção muito*erro* (toolog somente erros) ou *todas as* (para registro em log completo).</span><span class="sxs-lookup"><span data-stu-id="d5c30-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Selecionar o nível de log](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="d5c30-119">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d5c30-119">Click **Save**.</span></span>

7. <span data-ttu-id="d5c30-120">Para serviços da web de clássico, criar hello **ml diagnóstico** contêiner.</span><span class="sxs-lookup"><span data-stu-id="d5c30-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="d5c30-121">Todos os logs de serviço web são mantidos em um contêiner de blob denominado **ml diagnóstico** na conta de armazenamento Olá associada ao serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5c30-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="d5c30-122">Para novos serviços da web, esse contêiner é criado Olá primeira vez que você acessar o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5c30-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="d5c30-123">Para serviços da web de clássico, você precisar de toocreate Olá contêiner se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="d5c30-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="d5c30-124">Em Olá [portal do Azure](https://portal.azure.com), vá toohello conta de armazenamento associada ao serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5c30-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="d5c30-125">Em **Serviço Blob**, clique em **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="d5c30-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="d5c30-126">Se contêiner Olá **ml diagnóstico** não existe, clique em **+ contêiner**, dê a saudação contêiner Olá nome "ml de diagnóstico" e selecione Olá **tipo de acesso** como "Blob".</span><span class="sxs-lookup"><span data-stu-id="d5c30-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="d5c30-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5c30-127">Click **OK**.</span></span>

      ![Selecionar o nível de log](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="d5c30-129">Para um serviço web clássico, Olá painel de serviços Web no estúdio de aprendizado de máquina também tem um registro em log do comutador tooenable.</span><span class="sxs-lookup"><span data-stu-id="d5c30-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="d5c30-130">No entanto, como log agora é gerenciado por meio do portal de serviços Web hello, é necessário tooenable log por meio do portal Olá conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d5c30-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="d5c30-131">Se você tiver habilitado o log no Studio, em seguida, no Portal de serviços da Web de Olá, desabilite o log e habilitá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="d5c30-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="d5c30-132">efeitos de saudação de habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="d5c30-132">hello effects of enabling logging</span></span>
<span data-ttu-id="d5c30-133">Quando o log está habilitado, diagnóstico hello e erros de ponto de extremidade do serviço Olá web são registrados em Olá **ml diagnóstico** contêiner de blob em Olá conta de armazenamento do Azure vinculada ao espaço de trabalho do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="d5c30-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="d5c30-134">Este contêiner contém todas as informações de diagnóstico Olá para todos os pontos de serviço web Olá para todos os espaços de trabalho Olá associados a esta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d5c30-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="d5c30-135">Olá logs podem ser exibidos usando qualquer um dos Olá várias ferramentas tooexplore disponível uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c30-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="d5c30-136">Olá mais fácil pode ser toonavigate toohello conta de armazenamento Olá portal do Azure, clique em **contêineres**e, em seguida, clique em contêiner Olá **ml diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="d5c30-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="d5c30-137">Informações detalhadas do log blob</span><span class="sxs-lookup"><span data-stu-id="d5c30-137">Log blob detail information</span></span>
<span data-ttu-id="d5c30-138">Cada blob no contêiner de saudação contém informações de diagnóstico de saudação para exatamente um Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5c30-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="d5c30-139">A execução do método hello execução em lotes</span><span class="sxs-lookup"><span data-stu-id="d5c30-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="d5c30-140">A execução do método hello solicitação-resposta</span><span class="sxs-lookup"><span data-stu-id="d5c30-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="d5c30-141">Inicialização de um contêiner de Request-Response</span><span class="sxs-lookup"><span data-stu-id="d5c30-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="d5c30-142">nome de saudação de cada blob tem um prefixo de saudação formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5c30-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="d5c30-143">Onde _tipo de Log_ é uma saudação valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5c30-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="d5c30-144">lote</span><span class="sxs-lookup"><span data-stu-id="d5c30-144">batch</span></span>  
* <span data-ttu-id="d5c30-145">pontuação/solicitações</span><span class="sxs-lookup"><span data-stu-id="d5c30-145">score/requests</span></span>  
* <span data-ttu-id="d5c30-146">pontuação/init</span><span class="sxs-lookup"><span data-stu-id="d5c30-146">score/init</span></span>  

