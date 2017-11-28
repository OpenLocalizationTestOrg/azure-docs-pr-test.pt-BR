---
title: "pontos de extremidade de serviço Web de aaaCreating no aprendizado de máquina | Microsoft Docs"
description: "Criando pontos de extremidade de serviço Web no Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="d6eb4-103">Criando pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="d6eb4-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="d6eb4-104">Este tópico descreve tooa aplicável técnicas **clássico** serviço Web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="d6eb4-105">Quando você cria serviços Web que vende forward tooyour clientes, é necessário ao tooeach cliente tooprovide modelos treinados que são ainda vinculado toohello experimento de quais Olá Web serviço foi criado.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="d6eb4-106">Além disso, todas as atualizações experimento toohello deve ser aplicadas seletivamente tooan de ponto de extremidade sem substituir personalizações hello.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="d6eb4-107">tooaccomplish, aprendizado de máquina do Azure permite que você toocreate vários pontos de extremidade para um serviço Web implantado.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="d6eb4-108">Cada ponto de extremidade no hello serviço Web é abordado, limitado e gerenciado independentemente.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="d6eb4-109">Cada ponto de extremidade é uma chave exclusiva de autorização e a URL que você pode distribuir tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="d6eb4-110">Adicionando pontos de extremidade tooa Web serviço</span><span class="sxs-lookup"><span data-stu-id="d6eb4-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="d6eb4-111">Há três tooadd de maneiras tooa um ponto de extremidade serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="d6eb4-112">Programaticamente</span><span class="sxs-lookup"><span data-stu-id="d6eb4-112">Programmatically</span></span>
* <span data-ttu-id="d6eb4-113">Portal de serviços de Web de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="d6eb4-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="d6eb4-114">Embora Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="d6eb4-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="d6eb4-115">Depois que o ponto de extremidade de saudação é criado, você pode consumi-lo por meio de APIs síncrono, o lote APIs e planilhas do excel.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="d6eb4-116">Além disso tooadding pontos de extremidade por meio desta interface do usuário, você também pode usar Olá APIs de gerenciamento do ponto de extremidade tooprogrammatically adicionar pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="d6eb4-117">Se você adicionar mais pontos de extremidade toohello serviço da Web, você não pode excluir o ponto de extremidade do saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="d6eb4-118">Adicionando um ponto de extremidade programaticamente</span><span class="sxs-lookup"><span data-stu-id="d6eb4-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="d6eb4-119">Você pode adicionar um serviço Web de tooyour de ponto de extremidade programaticamente usando Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="d6eb4-120">Adicionar um ponto de extremidade usando o portal de serviços de Web de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="d6eb4-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="d6eb4-121">No estúdio de aprendizado de máquina, na coluna de navegação à esquerda do hello, clique em serviços da Web.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="d6eb4-122">Na parte inferior de saudação do painel de serviço Web hello, clique em **gerenciar pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="d6eb4-123">portal de serviços de Web de aprendizado de máquina do Azure Olá abre a página de pontos de extremidade de toohello de saudação serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="d6eb4-124">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-124">Click **New**.</span></span>
4. <span data-ttu-id="d6eb4-125">Digite um nome e uma descrição para o novo ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="d6eb4-126">Os nomes dos pontos de extremidade devem ter 24 caracteres ou menos e devem ser compostos de letras minúsculas ou números.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="d6eb4-127">Selecione o nível de log hello e se os dados de exemplo estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="d6eb4-128">Para obter mais informações sobre registro em log, veja [Habilitar o log de serviços Web de Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="d6eb4-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="d6eb4-129">Adicionar um ponto de extremidade usando Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="d6eb4-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="d6eb4-130">Entrar toohello [portal clássico do Azure](http://manage.windowsazure.com), clique em **aprendizado de máquina** na coluna esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="d6eb4-131">Clique em espaço de trabalho de saudação que contém o serviço Web de saudação no qual você está interessado.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Navegue tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="d6eb4-133">Clique em **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-133">Click **Web Services**.</span></span>
   
    ![Navegue tooWeb serviços](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="d6eb4-135">Clique em Olá Web service estiver interessado na lista de saudação toosee de pontos de extremidade disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Navegue tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="d6eb4-137">Final Olá Olá página, clique em **Adicionar ponto de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="d6eb4-138">Digite um nome e descrição, certifique-se de que não há nenhum outros pontos de extremidade com hello mesmo nome neste serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="d6eb4-139">Deixe o nível de limitação de saudação com seu valor padrão a menos que você tenha requisitos especiais.</span><span class="sxs-lookup"><span data-stu-id="d6eb4-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="d6eb4-140">toolearn mais sobre a limitação, consulte [pontos de extremidade de API de dimensionamento](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d6eb4-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Criar ponto de extremidade](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="d6eb4-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6eb4-142">Next Steps</span></span>
<span data-ttu-id="d6eb4-143">[Como um serviço Web de aprendizado de máquina do Azure de tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="d6eb4-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

