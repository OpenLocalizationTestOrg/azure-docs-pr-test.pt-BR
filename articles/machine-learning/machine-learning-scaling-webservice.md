---
title: "simultaneidade de tooincrease aaaHow de um serviço web de aprendizado de máquina do Azure | Microsoft Docs"
description: "Saiba como tooincrease simultaneidade de um aprendizado de máquina do Azure de serviço web com a adição de pontos de extremidade adicionais."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "aprendizado de máquina do azure, serviços Web, operacionalização, dimensionamento, ponto de extremidade, simultaneidade"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="54d8f-104">Dimensionando um serviço Web do Azure Machine Learning adicionando mais pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="54d8f-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="54d8f-105">Este tópico descreve tooa aplicável técnicas **clássico** serviço Web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="54d8f-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="54d8f-106">Por padrão, cada serviço Web publicado é configurado toosupport 20 solicitações simultâneas e pode ser de até 200 solicitações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="54d8f-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="54d8f-107">Enquanto Olá portal clássico do Azure fornece uma maneira tooset esse valor, aprendizado de máquina do Azure automaticamente otimiza Olá configuração tooprovide Olá melhor desempenho para o serviço web e valor portal Olá será ignorado.</span><span class="sxs-lookup"><span data-stu-id="54d8f-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="54d8f-108">Se você planejar toocall Olá API com uma carga maior que dará suporte a um valor de chamadas simultâneas máx de 200, você deve criar vários pontos de extremidade em Olá mesmo serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="54d8f-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="54d8f-109">Você pode, então, distribuir a carga aleatoriamente entre todos eles.</span><span class="sxs-lookup"><span data-stu-id="54d8f-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="54d8f-110">Olá a expansão de um serviço Web é uma tarefa comum.</span><span class="sxs-lookup"><span data-stu-id="54d8f-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="54d8f-111">Alguns motivos tooscale são toosupport mais de 200 solicitações simultâneas, aumentar a disponibilidade por meio de vários pontos de extremidade ou fornecer pontos de extremidade separados para o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="54d8f-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="54d8f-112">Você pode aumentar a escala Olá adicionando pontos de extremidade adicionais para Olá mesmo serviço da Web por meio de [portal clássico do Azure](https://manage.windowsazure.com/) ou hello [serviço de Web de aprendizado de máquina do Azure](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="54d8f-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="54d8f-113">Para saber mais sobre a adição de novos pontos de extremidade, consulte [Criando pontos de extremidade](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="54d8f-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="54d8f-114">Tenha em mente que pode ser prejudicial, se você não estiver chamando Olá API com uma taxa alta de forma correspondente usando uma contagem de alta simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="54d8f-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="54d8f-115">Talvez você veja esporádica tempos limite de e/ou picos na latência Olá se você colocar uma carga relativamente baixa em uma API configurada para alta carga.</span><span class="sxs-lookup"><span data-stu-id="54d8f-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="54d8f-116">Olá que APIs síncronas são geralmente usados em situações onde uma baixa latência é desejada.</span><span class="sxs-lookup"><span data-stu-id="54d8f-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="54d8f-117">Latência aqui implica em tempo de saudação que demora para uma solicitação de toocomplete Olá API e não se responsabiliza por quaisquer atrasos de rede.</span><span class="sxs-lookup"><span data-stu-id="54d8f-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="54d8f-118">Digamos que você tenha uma API com uma latência de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="54d8f-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="54d8f-119">toofully consomem a capacidade disponível Olá com alto nível de limitação e chamadas simultâneas máx. = 20, você precisa toocall essa API 20 * 1000 / 400 = 50 vezes por segundo.</span><span class="sxs-lookup"><span data-stu-id="54d8f-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="54d8f-120">Um máximo de chamadas simultâneas de 200 estendendo isso ainda mais, permite que você toocall Olá API 4000 vezes por segundo, supondo que uma latência de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="54d8f-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
