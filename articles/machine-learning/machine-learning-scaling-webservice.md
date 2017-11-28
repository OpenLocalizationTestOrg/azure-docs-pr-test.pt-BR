---
title: "Como aumentar a simultaneidade de um serviço Web do Azure Machine Learning | Microsoft Docs"
description: "Como aumentar a simultaneidade de um serviço Web do Azure Machine Learning adicionando mais pontos de extremidade."
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
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="7a80d-104">Dimensionando um serviço Web do Azure Machine Learning adicionando mais pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="7a80d-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="7a80d-105">Este tópico descreve técnicas aplicáveis a um serviço Web do Machine Learning **clássico**.</span><span class="sxs-lookup"><span data-stu-id="7a80d-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="7a80d-106">Por padrão, cada serviço Web publicado é configurado para oferecer suporte a 20 solicitações simultâneas, podendo chegar a 200.</span><span class="sxs-lookup"><span data-stu-id="7a80d-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="7a80d-107">Embora o portal clássico do Azure forneça uma maneira de definir esse valor, o Azure Machine Learning otimiza essa configuração automaticamente para fornecer o melhor desempenho ao serviço Web e o valor do portal é ignorado.</span><span class="sxs-lookup"><span data-stu-id="7a80d-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="7a80d-108">Se você planeja chamar a API com uma carga maior que o valor suportado de 200 para o Máximo de Chamadas Simultâneas, é preciso criar vários pontos de extremidade no mesmo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7a80d-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="7a80d-109">Você pode, então, distribuir a carga aleatoriamente entre todos eles.</span><span class="sxs-lookup"><span data-stu-id="7a80d-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="7a80d-110">O dimensionamento de um serviço Web é uma tarefa comum.</span><span class="sxs-lookup"><span data-stu-id="7a80d-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="7a80d-111">Entre os motivos para dimensionar estão oferecer suporte a mais de 200 solicitações simultâneas, aumentar a disponibilidade por meio de vários pontos de extremidade ou fornecer pontos de extremidade separados ao serviço Web.</span><span class="sxs-lookup"><span data-stu-id="7a80d-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="7a80d-112">Você pode aumentar a escala adicionando mais pontos de extremidade para o serviço Web por meio do [portal clássico do Azure](https://manage.windowsazure.com/) ou pelo portal do [serviço Web do Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="7a80d-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="7a80d-113">Para saber mais sobre a adição de novos pontos de extremidade, consulte [Criando pontos de extremidade](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="7a80d-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="7a80d-114">Tenha em mente que usar uma contagem de simultaneidade alta pode ser prejudicial se você não estiver chamando a API com uma taxa correspondentemente alta.</span><span class="sxs-lookup"><span data-stu-id="7a80d-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="7a80d-115">Você pode ver tempos limite esporádicos e/ou picos na latência se colocar uma carga relativamente baixa em uma API configurada para alta carga.</span><span class="sxs-lookup"><span data-stu-id="7a80d-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="7a80d-116">As APIs síncronas são normalmente usadas em situações onde uma baixa latência é desejada.</span><span class="sxs-lookup"><span data-stu-id="7a80d-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="7a80d-117">A latência aqui indica o tempo necessário para a API concluir uma solicitação e não se responsabiliza por quaisquer atrasos na rede.</span><span class="sxs-lookup"><span data-stu-id="7a80d-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="7a80d-118">Digamos que você tenha uma API com uma latência de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="7a80d-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="7a80d-119">Para consumir totalmente a capacidade disponível com alto nível de limitação e o Máximo de Chamadas Simultâneas = 20, você precisa chamar esta API 20 * 1000 / 50 = 400 vezes por segundo.</span><span class="sxs-lookup"><span data-stu-id="7a80d-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="7a80d-120">Estendendo isso ainda mais, um Máximo de Chamadas Simultâneas de 200 permite que você chame a API 4000 vezes por segundo, supondo que a latência seja de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="7a80d-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
