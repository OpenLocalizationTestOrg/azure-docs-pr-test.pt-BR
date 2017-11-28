---
ms.assetid: 
title: "diretrizes de limitação de Cofre de chaves de aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="e7464-102">Diretrizes de limitação do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e7464-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="e7464-103">Limitação é um processo que você iniciar o que limita o número de saudação de superutilização de tooprevent de serviço do Azure chamadas simultâneas toohello de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7464-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="e7464-104">Cofre de chave do Azure (AKV) é projetado toohandle um alto volume de solicitações.</span><span class="sxs-lookup"><span data-stu-id="e7464-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="e7464-105">Se ocorrer um número excessivo de solicitações, a limitação de solicitações do cliente ajuda a manter o desempenho ideal e a confiabilidade do hello serviço AKV.</span><span class="sxs-lookup"><span data-stu-id="e7464-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="e7464-106">Limites de limitação variam com base no cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7464-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="e7464-107">Por exemplo, se você estiver executando um grande volume de gravações, possibilidade de saudação para limitação é maior do que se você estiver executando apenas leituras.</span><span class="sxs-lookup"><span data-stu-id="e7464-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="e7464-108">Como o Key Vault trata os próprios limites?</span><span class="sxs-lookup"><span data-stu-id="e7464-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="e7464-109">Limites de serviço no cofre de chaves há uso indevido de tooprevent de recursos e certifique-se de qualidade de serviço para todos os clientes do cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="e7464-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="e7464-110">Quando um limite de serviço é excedido, o Key Vault limita quaisquer solicitações adicionais desse cliente por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e7464-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="e7464-111">Quando isso acontece, o Cofre de chaves retorna o código de status HTTP 429 (muito muitas solicitações), e Olá solicitações falhas.</span><span class="sxs-lookup"><span data-stu-id="e7464-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="e7464-112">Além disso, solicitações com falha que retornam uma contagem 429 para limites Olá controladas pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e7464-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="e7464-113">Se você tiver um caso comercial válido para restrições mais altas, entre em contato conosco.</span><span class="sxs-lookup"><span data-stu-id="e7464-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="e7464-114">Como toothrottle seu aplicativo na resposta tooservice limita</span><span class="sxs-lookup"><span data-stu-id="e7464-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="e7464-115">Olá seguem **práticas recomendadas** para seu aplicativo de limitação:</span><span class="sxs-lookup"><span data-stu-id="e7464-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="e7464-116">Reduza o número de saudação de operações por solicitação.</span><span class="sxs-lookup"><span data-stu-id="e7464-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="e7464-117">Reduza a frequência de saudação de solicitações.</span><span class="sxs-lookup"><span data-stu-id="e7464-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="e7464-118">Evite tentativas imediatas.</span><span class="sxs-lookup"><span data-stu-id="e7464-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="e7464-119">Todas as solicitações se acumulam em relação a seus limites de uso.</span><span class="sxs-lookup"><span data-stu-id="e7464-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="e7464-120">Quando você implementa o tratamento de erros do aplicativo, use Olá HTTP Erro código 429 toodetect Olá necessário para limitação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="e7464-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="e7464-121">Se a solicitação de saudação falhar novamente com um código de erro HTTP 429, você ainda está encontrando um limite de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7464-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="e7464-122">Continue Olá toouse recomendado o método limitação do lado do cliente, tentar novamente a solicitação de saudação até obter êxito.</span><span class="sxs-lookup"><span data-stu-id="e7464-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="e7464-123">Método recomendado de limitação do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="e7464-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="e7464-124">No código de erro HTTP 429, inicie a limitação do cliente usando uma abordagem de retirada exponencial:</span><span class="sxs-lookup"><span data-stu-id="e7464-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="e7464-125">Aguarde 1 segundo, tente solicitar novamente</span><span class="sxs-lookup"><span data-stu-id="e7464-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="e7464-126">Se ainda estiver limitado, aguarde 2 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="e7464-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="e7464-127">Se ainda estiver limitado, aguarde 4 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="e7464-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="e7464-128">Se ainda estiver limitado, aguarde 8 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="e7464-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="e7464-129">Se ainda estiver limitado, aguarde 16 segundos e tente a solicitação novamente</span><span class="sxs-lookup"><span data-stu-id="e7464-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="e7464-130">Neste ponto, você não deve estar obtendo códigos de resposta HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="e7464-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7464-131">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e7464-131">See also</span></span>

<span data-ttu-id="e7464-132">Para obter uma orientação mais profunda do limitação em Olá Microsoft Cloud, consulte [limitação padrão](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="e7464-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

