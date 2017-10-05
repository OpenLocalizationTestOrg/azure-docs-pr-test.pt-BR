---
title: "Saiba mais sobre a Limitação nos Serviços BizTalk | Microsoft Docs"
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
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="f4a6b-105">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="f4a6b-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="f4a6b-106">Os Serviços BizTalk do Azure implementam a limitação do serviço com base em duas condições: uso de memória e número de mensagens simultâneas em processamento.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="f4a6b-107">Este tópico lista as limitações e descreve o comportamento da Execução quando ocorre uma condição de limitação.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="f4a6b-108">Limites da limitação</span><span class="sxs-lookup"><span data-stu-id="f4a6b-108">Throttling Thresholds</span></span>
<span data-ttu-id="f4a6b-109">A tabela a seguir lista os limites e origem da limitação:</span><span class="sxs-lookup"><span data-stu-id="f4a6b-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="f4a6b-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="f4a6b-110">Description</span></span> | <span data-ttu-id="f4a6b-111">Limite baixo</span><span class="sxs-lookup"><span data-stu-id="f4a6b-111">Low Threshold</span></span> | <span data-ttu-id="f4a6b-112">Limite alto</span><span class="sxs-lookup"><span data-stu-id="f4a6b-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f4a6b-113">Memória</span><span class="sxs-lookup"><span data-stu-id="f4a6b-113">Memory</span></span> |<span data-ttu-id="f4a6b-114">% de memória total de sistema disponível/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="f4a6b-115">O total de PageFileBytes disponível é aproximadamente 2 vezes a RAM do sistema.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="f4a6b-116">60%</span><span class="sxs-lookup"><span data-stu-id="f4a6b-116">60%</span></span> |<span data-ttu-id="f4a6b-117">70%</span><span class="sxs-lookup"><span data-stu-id="f4a6b-117">70%</span></span> |
| <span data-ttu-id="f4a6b-118">Processamento de mensagem</span><span class="sxs-lookup"><span data-stu-id="f4a6b-118">Message Processing</span></span> |<span data-ttu-id="f4a6b-119">Número de processamento de mensagens simultaneamente</span><span class="sxs-lookup"><span data-stu-id="f4a6b-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="f4a6b-120">40 vezes o número de núcleos</span><span class="sxs-lookup"><span data-stu-id="f4a6b-120">40 * number of cores</span></span> |<span data-ttu-id="f4a6b-121">100 vezes o número de núcleos</span><span class="sxs-lookup"><span data-stu-id="f4a6b-121">100 * number of cores</span></span> |

<span data-ttu-id="f4a6b-122">Quando um limite alto é atingido, os Serviços BizTalk do Azure começam a ser limitados.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="f4a6b-123">A limitação é interrompida quando um limite baixo é atingido.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="f4a6b-124">Por exemplo, seu serviço estiver usando 65% da memória do sistema.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="f4a6b-125">Nesta situação, o serviço não sofre limitação.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="f4a6b-126">Seu serviço começa usando 70% da memória do sistema.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="f4a6b-127">Nessa situação, o serviço começa a ser limitado e continua até que o serviço use 60% da memória do sistema (limite baixo).</span><span class="sxs-lookup"><span data-stu-id="f4a6b-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="f4a6b-128">Os Serviços BizTalk do Azure acompanham o status da limitação (estado normal versus limitado) e a duração da limitação.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="f4a6b-129">Comportamento do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="f4a6b-129">Runtime Behavior</span></span>
<span data-ttu-id="f4a6b-130">Quando os Serviços BizTalk do Azure entram em estado de limitação, o seguinte ocorre:</span><span class="sxs-lookup"><span data-stu-id="f4a6b-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="f4a6b-131">A limitação ocorre por instância de função.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-131">Throttling is per role instance.</span></span> <span data-ttu-id="f4a6b-132">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f4a6b-132">For example:</span></span><br/>
  <span data-ttu-id="f4a6b-133">A InstânciadeFunçãoA está limitada.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="f4a6b-134">A InstânciadeFunçãoB não está limitada.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="f4a6b-135">Nesta situação, as mensagens da InstânciadeFunçãoB são processadas conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="f4a6b-136">As mensagens na RoleInstanceA são descartadas e ocorre uma falha com o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="f4a6b-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="f4a6b-137">
  **O servidor está ocupado. Tente novamente.**</span><span class="sxs-lookup"><span data-stu-id="f4a6b-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="f4a6b-138">Nenhuma origem de pull pode pesquisar ou baixar uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="f4a6b-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f4a6b-139">For example:</span></span><br/>
  <span data-ttu-id="f4a6b-140">um pipeline puxa as mensagens de uma origem de FTP externa.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="f4a6b-141">A instância de função que faz puxa entra em estado de limitação.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="f4a6b-142">Nessa situação, o pipeline interrompe o download de mensagens adicionais até que a instância de função saia da limitação.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="f4a6b-143">Uma resposta é enviada ao cliente para que ele reenvie a mensagem.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="f4a6b-144">Você deve aguardar até que a limitação seja resolvida.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="f4a6b-145">Especificamente, você deve aguardar até que o limite baixo seja atingido.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="f4a6b-146">Observações importantes</span><span class="sxs-lookup"><span data-stu-id="f4a6b-146">Important notes</span></span>
* <span data-ttu-id="f4a6b-147">A limitação não pode ser desabilitada.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="f4a6b-148">Os limites de limitação não podem ser modificados.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="f4a6b-149">A limitação é implementada em todo o sistema.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="f4a6b-150">O Servidor de Banco de Dados SQL do Azure também tem uma limitação interna.</span><span class="sxs-lookup"><span data-stu-id="f4a6b-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="f4a6b-151">Tópicos adicionais dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a6b-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="f4a6b-152">Instalando o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a6b-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="f4a6b-153">Tutoriais: Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a6b-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="f4a6b-154">Como começar a usar o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a6b-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="f4a6b-155">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a6b-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="f4a6b-156">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f4a6b-156">See Also</span></span>
* [<span data-ttu-id="f4a6b-157">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="f4a6b-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="f4a6b-158">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a6b-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="f4a6b-159">Serviços BizTalk: gráfico do status do provisionamento</span><span class="sxs-lookup"><span data-stu-id="f4a6b-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="f4a6b-160">Serviços BizTalk: guias Painel, Monitor e Escala</span><span class="sxs-lookup"><span data-stu-id="f4a6b-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="f4a6b-161">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="f4a6b-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="f4a6b-162">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="f4a6b-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

