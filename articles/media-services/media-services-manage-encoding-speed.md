---
title: "velocidade de gerenciar AAA e a simultaneidade de sua codificação com os serviços de mídia do Azure | Microsoft Docs"
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
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="3e3c4-103">Gerenciar a velocidade e a simultaneidade de sua codificação</span><span class="sxs-lookup"><span data-stu-id="3e3c4-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="3e3c4-104">Este artigo fornece uma visão geral de como você pode gerenciar a velocidade e a simultaneidade de seus trabalhos/tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="3e3c4-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3e3c4-105">Overview</span></span>

<span data-ttu-id="3e3c4-106">Nos serviços de mídia, um **o tipo de unidade reservada** determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="3e3c4-107">Você pode escolher entre os seguintes Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="3e3c4-108">Por exemplo, Olá mesmo trabalho de codificação é executada mais rapidamente ao usar o hello **S2** tipo de unidade reservada comparar toohello **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="3e3c4-109">Olá [dimensionamento unidades de codificação](media-services-scale-media-processing-overview.md) tópico mostra uma tabela que ajuda a tomar decisões ao escolher entre diferentes velocidades de codificação.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="3e3c4-110">Além disso, toospecifying Olá reservado tipo de unidade, você pode especificar tooprovision sua conta com **unidades reservadas**.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="3e3c4-111">número de saudação de unidades reservadas provisionadas determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma determinada conta.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="3e3c4-112">Por exemplo, se sua conta tiver cinco unidades reservadas, tarefas de cinco mídia serão executados simultaneamente desde pois há tarefas toobe processado.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="3e3c4-113">as tarefas restantes Olá aguardarão na fila hello e serão escolhidas para processamento sequencialmente quando uma tarefa em execução for concluída.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="3e3c4-114">Se uma conta não tiver nenhuma unidade reservada provisionada, as tarefas serão selecionadas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="3e3c4-115">Nesse caso, Olá aguardar o tempo entre a conclusão de uma tarefa e hello seguir dependerá disponibilidade Olá dos recursos no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="3e3c4-116">Para obter informações detalhadas e exemplos que mostram como unidades de codificação tooscale, consulte [isso](media-services-scale-media-processing-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="3e3c4-117">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="3e3c4-117">Next step</span></span>

[<span data-ttu-id="3e3c4-118">Dimensionamento de unidades de codificação</span><span class="sxs-lookup"><span data-stu-id="3e3c4-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="3e3c4-119">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="3e3c4-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3e3c4-120">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="3e3c4-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

