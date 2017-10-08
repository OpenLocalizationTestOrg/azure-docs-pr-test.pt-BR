---
title: suporte a aaaHTTP/2 no Azure CDN | Microsoft Docs
description: Saiba mais sobre o suporte a HTTP/2 e CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="ce768-103">Suporte a HTTP/2 na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ce768-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="ce768-104">HTTP/2 é tooHTTP/1.1\ uma revisão principal.</span><span class="sxs-lookup"><span data-stu-id="ce768-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="ce768-105">Fornece mais rapidamente o desempenho da web, tempo de resposta reduzida e usuário aprimorada experiência, mantendo Olá familiares métodos HTTP, códigos de status e semântica.</span><span class="sxs-lookup"><span data-stu-id="ce768-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="ce768-106">Embora HTTP/2 toowork projetado com HTTP e HTTPS, muitos navegadores da web de cliente suportam apenas HTTP/2 por TLS.</span><span class="sxs-lookup"><span data-stu-id="ce768-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="ce768-107">Benefícios do HTTP/2</span><span class="sxs-lookup"><span data-stu-id="ce768-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="ce768-108">saudação de HTTP/2 benefícios:</span><span class="sxs-lookup"><span data-stu-id="ce768-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="ce768-109">**Multiplexação e simultaneidade**</span><span class="sxs-lookup"><span data-stu-id="ce768-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="ce768-110">Usando o HTTP 1.1, fazer várias solicitações de recursos requer várias conexões TCP, sendo que cada conexão tem uma sobrecarga de desempenho associada a ela.</span><span class="sxs-lookup"><span data-stu-id="ce768-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="ce768-111">2/HTTP permite que vários toobe recursos solicitado em uma única conexão de TCP.</span><span class="sxs-lookup"><span data-stu-id="ce768-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="ce768-112">**Compactação de cabeçalho**</span><span class="sxs-lookup"><span data-stu-id="ce768-112">**Header compression**</span></span>

    <span data-ttu-id="ce768-113">Compactando cabeçalhos Olá HTTP para recursos atendidos, tempo de transmissão de saudação é reduzido significativamente.</span><span class="sxs-lookup"><span data-stu-id="ce768-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="ce768-114">**Dependências de fluxo**</span><span class="sxs-lookup"><span data-stu-id="ce768-114">**Stream dependencies**</span></span>

    <span data-ttu-id="ce768-115">Dependências de fluxo permitir que o cliente Olá tooindicate toohello server quais recursos têm prioridade.</span><span class="sxs-lookup"><span data-stu-id="ce768-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="ce768-116">Suporte a Navegador HTTP/2</span><span class="sxs-lookup"><span data-stu-id="ce768-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="ce768-117">Todos os principais navegadores de saudação implementou o suporte HTTP/2 em suas versões atuais.</span><span class="sxs-lookup"><span data-stu-id="ce768-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="ce768-118">Navegadores com suporte não serão automaticamente fallback tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="ce768-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="ce768-119">Navegador</span><span class="sxs-lookup"><span data-stu-id="ce768-119">Browser</span></span>|<span data-ttu-id="ce768-120">Versão Mínima</span><span class="sxs-lookup"><span data-stu-id="ce768-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="ce768-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="ce768-121">Microsoft Edge</span></span>| <span data-ttu-id="ce768-122">12</span><span class="sxs-lookup"><span data-stu-id="ce768-122">12</span></span>|
|<span data-ttu-id="ce768-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="ce768-123">Google Chrome</span></span>| <span data-ttu-id="ce768-124">43</span><span class="sxs-lookup"><span data-stu-id="ce768-124">43</span></span>|
|<span data-ttu-id="ce768-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="ce768-125">Mozilla Firefox</span></span>| <span data-ttu-id="ce768-126">38</span><span class="sxs-lookup"><span data-stu-id="ce768-126">38</span></span>|
|<span data-ttu-id="ce768-127">Opera</span><span class="sxs-lookup"><span data-stu-id="ce768-127">Opera</span></span>| <span data-ttu-id="ce768-128">32</span><span class="sxs-lookup"><span data-stu-id="ce768-128">32</span></span>|
|<span data-ttu-id="ce768-129">Safari</span><span class="sxs-lookup"><span data-stu-id="ce768-129">Safari</span></span>| <span data-ttu-id="ce768-130">9</span><span class="sxs-lookup"><span data-stu-id="ce768-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="ce768-131">Habilitar o Suporte a HTTP/2 na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ce768-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="ce768-132">No momento, o suporte a HTTP/2 está ativo para os perfis **CDN do Azure do Akamai** e **CDN do Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="ce768-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="ce768-133">Nenhuma ação adicional dos clientes é necessária.</span><span class="sxs-lookup"><span data-stu-id="ce768-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="ce768-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce768-134">Next Steps</span></span>

<span data-ttu-id="ce768-135">benefícios de saudação toosee de HTTP/2 em ação, consulte [esta demonstração do Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="ce768-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="ce768-136">toolearn mais sobre HTTP/2, visite Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce768-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="ce768-137">Home page de especificação HTTP/2</span><span class="sxs-lookup"><span data-stu-id="ce768-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="ce768-138">Perguntas Frequentes Oficiais do HTTP/2</span><span class="sxs-lookup"><span data-stu-id="ce768-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="ce768-139">Informações de HTTP/2 do Akamai</span><span class="sxs-lookup"><span data-stu-id="ce768-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="ce768-140">toolearn mais sobre os recursos disponíveis do Azure CDN, consulte Olá [visão geral do Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="ce768-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
