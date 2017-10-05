---
ms.assetid: 
title: "Diretrizes de limitação do Azure Key Vault | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="eb3ec-102">Diretrizes de limitação do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="eb3ec-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="eb3ec-103">A limitação é o processo que você iniciar para limitar o número de chamadas simultâneas para o serviço do Azure a fim de evitar o uso excessivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="eb3ec-104">O AKV (Azure Key Vault) foi projetado para lidar com um grande volume de solicitações.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="eb3ec-105">No caso de ocorrer um grande número de solicitações, limitar as solicitações do seu cliente ajuda a manter o desempenho ideal e a confiabilidade do serviço AKV.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="eb3ec-106">Limites de limitação variam de acordo com o cenário.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="eb3ec-107">Por exemplo, se você estiver executando um grande volume de gravação, a possibilidade de limitação será maior do que se você estiver apenas executando leituras.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="eb3ec-108">Como o Key Vault trata os próprios limites?</span><span class="sxs-lookup"><span data-stu-id="eb3ec-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="eb3ec-109">Os limites de serviço no Key Vault existem para impedir o uso incorreto de recursos e assegurar a qualidade de serviço para todos os clientes do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="eb3ec-110">Quando um limite de serviço é excedido, o Key Vault limita quaisquer solicitações adicionais desse cliente por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="eb3ec-111">Quando isso acontece, o Key Vault retorna o código de status HTTP 429 (Número excessivo de solicitações) e as solicitações falham.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="eb3ec-112">Além disso, solicitações com falha que retornam um 429 contam para as restrições acompanhadas pelo Key Vault.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="eb3ec-113">Se você tiver um caso comercial válido para restrições mais altas, entre em contato conosco.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="eb3ec-114">Como restringir o seu aplicativo em resposta aos limites de serviço</span><span class="sxs-lookup"><span data-stu-id="eb3ec-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="eb3ec-115">A seguir estão as **práticas recomendadas** para limitar seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="eb3ec-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="eb3ec-116">Reduza o número de operações por solicitação.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="eb3ec-117">Reduza a frequência de solicitações.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="eb3ec-118">Evite tentativas imediatas.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="eb3ec-119">Todas as solicitações se acumulam em relação a seus limites de uso.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="eb3ec-120">Quando você implementa o tratamento de erro do aplicativo, use o código de erro HTTP 429 para detectar a necessidade de limitação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="eb3ec-121">Se a solicitação falha novamente com um código de erro HTTP 429, você ainda está encontrando um limite de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="eb3ec-122">Continue a usar o método de limitação do lado do cliente recomendado, tentando realizar a solicitação novamente até que ela tenha êxito.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="eb3ec-123">Método recomendado de limitação do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="eb3ec-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="eb3ec-124">No código de erro HTTP 429, inicie a limitação do cliente usando uma abordagem de retirada exponencial:</span><span class="sxs-lookup"><span data-stu-id="eb3ec-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="eb3ec-125">Aguarde 1 segundo, tente solicitar novamente</span><span class="sxs-lookup"><span data-stu-id="eb3ec-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="eb3ec-126">Se ainda estiver limitado, aguarde 2 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="eb3ec-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="eb3ec-127">Se ainda estiver limitado, aguarde 4 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="eb3ec-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="eb3ec-128">Se ainda estiver limitado, aguarde 8 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="eb3ec-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="eb3ec-129">Se ainda estiver limitado, aguarde 16 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="eb3ec-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="eb3ec-130">Neste ponto, você não deve estar obtendo códigos de resposta HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="eb3ec-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="eb3ec-131">Consulte também</span><span class="sxs-lookup"><span data-stu-id="eb3ec-131">See also</span></span>

<span data-ttu-id="eb3ec-132">Para obter uma orientação mais profunda de limitação no Microsoft Cloud, consulte [Padrão de Limitação](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="eb3ec-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

