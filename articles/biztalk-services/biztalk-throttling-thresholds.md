---
title: "aaaLearn sobre limitação nos Serviços BizTalk | Microsoft Docs"
description: "Saiba mais sobre os limites de limitação e comportamentos de tempo de execução resultantes para os serviços BizTalk. A limitação é baseada no uso de memória e número de mensagens. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="dfcc6-105">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="dfcc6-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="dfcc6-106">Serviços BizTalk do Azure implementa o serviço com base em duas condições de limitação: número de hello e uso de memória de processamento de mensagens simultâneas.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="dfcc6-107">Este tópico lista Olá limitação limites e descreve o comportamento de tempo de execução de saudação quando ocorre uma condição de limitação.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="dfcc6-108">Limites da limitação</span><span class="sxs-lookup"><span data-stu-id="dfcc6-108">Throttling Thresholds</span></span>
<span data-ttu-id="dfcc6-109">Olá a tabela a seguir lista Olá limitação de origem e de limites:</span><span class="sxs-lookup"><span data-stu-id="dfcc6-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="dfcc6-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="dfcc6-110">Description</span></span> | <span data-ttu-id="dfcc6-111">Limite baixo</span><span class="sxs-lookup"><span data-stu-id="dfcc6-111">Low Threshold</span></span> | <span data-ttu-id="dfcc6-112">Limite alto</span><span class="sxs-lookup"><span data-stu-id="dfcc6-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dfcc6-113">Memória</span><span class="sxs-lookup"><span data-stu-id="dfcc6-113">Memory</span></span> |<span data-ttu-id="dfcc6-114">% de memória total de sistema disponível/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="dfcc6-115">Total PageFileBytes disponível é de aproximadamente 2 vezes Olá RAM do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="dfcc6-116">60%</span><span class="sxs-lookup"><span data-stu-id="dfcc6-116">60%</span></span> |<span data-ttu-id="dfcc6-117">70%</span><span class="sxs-lookup"><span data-stu-id="dfcc6-117">70%</span></span> |
| <span data-ttu-id="dfcc6-118">Processamento de mensagem</span><span class="sxs-lookup"><span data-stu-id="dfcc6-118">Message Processing</span></span> |<span data-ttu-id="dfcc6-119">Número de processamento de mensagens simultaneamente</span><span class="sxs-lookup"><span data-stu-id="dfcc6-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="dfcc6-120">40 vezes o número de núcleos</span><span class="sxs-lookup"><span data-stu-id="dfcc6-120">40 * number of cores</span></span> |<span data-ttu-id="dfcc6-121">100 vezes o número de núcleos</span><span class="sxs-lookup"><span data-stu-id="dfcc6-121">100 * number of cores</span></span> |

<span data-ttu-id="dfcc6-122">Quando um limite máximo for atingido, os Serviços BizTalk do Azure inicia toothrottle.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="dfcc6-123">Limitação será interrompido quando o limite mínimo de saudação é atingido.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="dfcc6-124">Por exemplo, seu serviço estiver usando 65% da memória do sistema.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="dfcc6-125">Nessa situação, o serviço de saudação não acelerador.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="dfcc6-126">Seu serviço começa usando 70% da memória do sistema.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="dfcc6-127">Nessa situação, o serviço Olá limita e continua toothrottle até que o serviço de saudação usa a memória do sistema 60% (limite inferior).</span><span class="sxs-lookup"><span data-stu-id="dfcc6-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="dfcc6-128">Serviços BizTalk do Azure controla Olá limitação status (estado normal versus estado limitado) e hello limitação duração.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="dfcc6-129">Comportamento do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="dfcc6-129">Runtime Behavior</span></span>
<span data-ttu-id="dfcc6-130">Quando os Serviços BizTalk do Azure entrará em um estado de limitação, ocorre a seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="dfcc6-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="dfcc6-131">A limitação ocorre por instância de função.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-131">Throttling is per role instance.</span></span> <span data-ttu-id="dfcc6-132">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcc6-132">For example:</span></span><br/>
  <span data-ttu-id="dfcc6-133">A InstânciadeFunçãoA está limitada.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="dfcc6-134">A InstânciadeFunçãoB não está limitada.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="dfcc6-135">Nesta situação, as mensagens da InstânciadeFunçãoB são processadas conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="dfcc6-136">Mensagens de RoleInstanceA são descartadas e falharem com hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfcc6-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="dfcc6-137">
  **O servidor está ocupado. Tente novamente.**</span><span class="sxs-lookup"><span data-stu-id="dfcc6-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="dfcc6-138">Nenhuma origem de pull pode pesquisar ou baixar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="dfcc6-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dfcc6-139">For example:</span></span><br/>
  <span data-ttu-id="dfcc6-140">um pipeline puxa as mensagens de uma origem de FTP externa.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="dfcc6-141">instância de função Hello fazer pull Olá obtém em um estado de limitação.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="dfcc6-142">Nessa situação, pipeline Olá para baixar mensagens adicionais até que a instância de função hello para de limitação.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="dfcc6-143">Uma resposta é enviada toohello cliente cliente Olá pode enviar novamente a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="dfcc6-144">Você deve aguardar até que a limitação de saudação seja resolvido.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="dfcc6-145">Especificamente, você deve aguardar até que o limite mínimo de saudação é atingido.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="dfcc6-146">Observações importantes</span><span class="sxs-lookup"><span data-stu-id="dfcc6-146">Important notes</span></span>
* <span data-ttu-id="dfcc6-147">A limitação não pode ser desabilitada.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="dfcc6-148">Os limites de limitação não podem ser modificados.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="dfcc6-149">A limitação é implementada em todo o sistema.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="dfcc6-150">Olá servidor de banco de dados do SQL Azure também tem uma limitação interna.</span><span class="sxs-lookup"><span data-stu-id="dfcc6-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="dfcc6-151">Tópicos adicionais dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="dfcc6-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="dfcc6-152">Instalando Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="dfcc6-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="dfcc6-153">Tutoriais: Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="dfcc6-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="dfcc6-154">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="dfcc6-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="dfcc6-155">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="dfcc6-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="dfcc6-156">Consulte também</span><span class="sxs-lookup"><span data-stu-id="dfcc6-156">See Also</span></span>
* [<span data-ttu-id="dfcc6-157">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="dfcc6-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="dfcc6-158">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="dfcc6-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="dfcc6-159">Serviços BizTalk: gráfico do status do provisionamento</span><span class="sxs-lookup"><span data-stu-id="dfcc6-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="dfcc6-160">Serviços BizTalk: guias Painel, Monitor e Escala</span><span class="sxs-lookup"><span data-stu-id="dfcc6-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="dfcc6-161">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="dfcc6-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="dfcc6-162">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="dfcc6-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

