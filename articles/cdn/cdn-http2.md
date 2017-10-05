---
title: Suporte a HTTP/2 na CDN do Azure | Microsoft Docs
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
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="fd538-103">Suporte a HTTP/2 na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="fd538-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="fd538-104">HTTP/2 é uma revisão principal HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="fd538-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="fd538-105">Ele fornece mais rápido do desempenho da web, tempo de reposta reduzido e melhor experiência de usuário, mantendo os métodos HTTP familiares, códigos de status e semântica.</span><span class="sxs-lookup"><span data-stu-id="fd538-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="fd538-106">Embora o HTTP/2 seja projetado para trabalhar com HTTP e HTTPS, muitos navegadores da Web de cliente somente dão suporte a HTTP/2 por TLS.</span><span class="sxs-lookup"><span data-stu-id="fd538-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="fd538-107">Benefícios do HTTP/2</span><span class="sxs-lookup"><span data-stu-id="fd538-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="fd538-108">Os benefícios do HTTP/2 incluem:</span><span class="sxs-lookup"><span data-stu-id="fd538-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="fd538-109">**Multiplexação e simultaneidade**</span><span class="sxs-lookup"><span data-stu-id="fd538-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="fd538-110">Usando o HTTP 1.1, fazer várias solicitações de recursos requer várias conexões TCP, sendo que cada conexão tem uma sobrecarga de desempenho associada a ela.</span><span class="sxs-lookup"><span data-stu-id="fd538-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="fd538-111">O HTTP/2 permite que vários recursos sejam solicitados em uma única conexão TCP.</span><span class="sxs-lookup"><span data-stu-id="fd538-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="fd538-112">**Compactação de cabeçalho**</span><span class="sxs-lookup"><span data-stu-id="fd538-112">**Header compression**</span></span>

    <span data-ttu-id="fd538-113">Compactando cabeçalhos HTTP para recursos fornecidos, o tempo de transmissão é reduzido significativamente.</span><span class="sxs-lookup"><span data-stu-id="fd538-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="fd538-114">**Dependências de fluxo**</span><span class="sxs-lookup"><span data-stu-id="fd538-114">**Stream dependencies**</span></span>

    <span data-ttu-id="fd538-115">Dependências de fluxo permitem que o cliente indique ao servidor quais recursos têm prioridade.</span><span class="sxs-lookup"><span data-stu-id="fd538-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="fd538-116">Suporte a Navegador HTTP/2</span><span class="sxs-lookup"><span data-stu-id="fd538-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="fd538-117">Todos os principais navegadores implementaram o suporte a HTTP/2 em suas versões atuais.</span><span class="sxs-lookup"><span data-stu-id="fd538-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="fd538-118">O fallback de navegadores sem suporte para HTTP/1.1 ocorrerá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fd538-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="fd538-119">Navegador</span><span class="sxs-lookup"><span data-stu-id="fd538-119">Browser</span></span>|<span data-ttu-id="fd538-120">Versão Mínima</span><span class="sxs-lookup"><span data-stu-id="fd538-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="fd538-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="fd538-121">Microsoft Edge</span></span>| <span data-ttu-id="fd538-122">12</span><span class="sxs-lookup"><span data-stu-id="fd538-122">12</span></span>|
|<span data-ttu-id="fd538-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="fd538-123">Google Chrome</span></span>| <span data-ttu-id="fd538-124">43</span><span class="sxs-lookup"><span data-stu-id="fd538-124">43</span></span>|
|<span data-ttu-id="fd538-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="fd538-125">Mozilla Firefox</span></span>| <span data-ttu-id="fd538-126">38</span><span class="sxs-lookup"><span data-stu-id="fd538-126">38</span></span>|
|<span data-ttu-id="fd538-127">Opera</span><span class="sxs-lookup"><span data-stu-id="fd538-127">Opera</span></span>| <span data-ttu-id="fd538-128">32</span><span class="sxs-lookup"><span data-stu-id="fd538-128">32</span></span>|
|<span data-ttu-id="fd538-129">Safari</span><span class="sxs-lookup"><span data-stu-id="fd538-129">Safari</span></span>| <span data-ttu-id="fd538-130">9</span><span class="sxs-lookup"><span data-stu-id="fd538-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="fd538-131">Habilitar o Suporte a HTTP/2 na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="fd538-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="fd538-132">No momento, o suporte a HTTP/2 está ativo para os perfis **CDN do Azure do Akamai** e **CDN do Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="fd538-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="fd538-133">Nenhuma ação adicional dos clientes é necessária.</span><span class="sxs-lookup"><span data-stu-id="fd538-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="fd538-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd538-134">Next Steps</span></span>

<span data-ttu-id="fd538-135">Para ver os benefícios do HTTP/2 em ação, consulte [esta demonstração do Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="fd538-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="fd538-136">Para saber mais sobre o HTTP/2, visite os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="fd538-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="fd538-137">Home page de especificação HTTP/2</span><span class="sxs-lookup"><span data-stu-id="fd538-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="fd538-138">Perguntas Frequentes Oficiais do HTTP/2</span><span class="sxs-lookup"><span data-stu-id="fd538-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="fd538-139">Informações de HTTP/2 do Akamai</span><span class="sxs-lookup"><span data-stu-id="fd538-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="fd538-140">Para saber mais sobre os recursos disponíveis da CDN do Azure, consulte a [Visão geral da CDN do Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="fd538-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>