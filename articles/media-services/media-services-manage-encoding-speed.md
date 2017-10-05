---
title: "Gerenciar a velocidade e a simultaneidade de sua codificação com os Serviços de Mídia do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral de como você pode gerenciar a velocidade e a simultaneidade de seus trabalhos/tarefas de codificação com os Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="8cd2e-103">Gerenciar a velocidade e a simultaneidade de sua codificação</span><span class="sxs-lookup"><span data-stu-id="8cd2e-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="8cd2e-104">Este artigo fornece uma visão geral de como você pode gerenciar a velocidade e a simultaneidade de seus trabalhos/tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="8cd2e-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8cd2e-105">Overview</span></span>

<span data-ttu-id="8cd2e-106">Nos Serviços de Mídia, um **Tipo de Unidade Reservada** que determina a velocidade com que as suas tarefas de processamento de mídia são processadas.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="8cd2e-107">Você pode escolher entre os seguintes tipos de unidade reservada: **S1**, **S2** ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="8cd2e-108">Por exemplo, o mesmo trabalho de codificação é executado mais rapidamente quando você usa o tipo de unidade reservada **S2** em comparação ao tipo **S1**.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="8cd2e-109">O tópico [dimensionamento de unidades de codificação](media-services-scale-media-processing-overview.md) mostra uma tabela que o ajuda a tomar uma decisão ao escolher entre diferentes velocidades de codificação.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="8cd2e-110">Além de especificar o tipo de unidade reservada, você pode especificar o provisionamento da sua conta com **Unidades Reservadas**.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="8cd2e-111">O número de unidades reservadas provisionadas determina o número de tarefas de mídia que podem ser processadas simultaneamente em uma determinada conta.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="8cd2e-112">Por exemplo, se sua conta tiver cinco unidades reservadas, as cinco tarefas de mídia serão executadas simultaneamente enquanto houver tarefas a serem processadas.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="8cd2e-113">As tarefas restantes irão aguardar na fila e serão selecionadas para processamento sequencialmente quando uma tarefa em execução for concluída.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="8cd2e-114">Se uma conta não tiver nenhuma unidade reservada provisionada, as tarefas serão selecionadas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="8cd2e-115">Nesse caso, o tempo de espera entre a conclusão de uma tarefa e o início da próxima dependerá da disponibilidade dos recursos do sistema.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="8cd2e-116">Para obter informações detalhadas e exemplos que mostram como dimensionar unidades de codificação, consulte [este](media-services-scale-media-processing-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="8cd2e-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="8cd2e-117">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="8cd2e-117">Next step</span></span>

[<span data-ttu-id="8cd2e-118">Dimensionamento de unidades de codificação</span><span class="sxs-lookup"><span data-stu-id="8cd2e-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="8cd2e-119">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="8cd2e-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8cd2e-120">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="8cd2e-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

