---
title: Habilitando o SSL de ponta a ponta no Gateway de Aplicativo do Azure | Microsoft Docs
description: "Esta página oferece uma visão geral do suporte a SSL de ponta a ponta do Gateway de Aplicativo."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: 689ee54dc1db2ea371b08270718278fd98c65bb5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-end-to-end-ssl-with-application-gateway"></a><span data-ttu-id="1e29f-103">Visão geral do SSL de ponta a ponta com um Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e29f-103">Overview of end to end SSL with Application Gateway</span></span>

<span data-ttu-id="1e29f-104">O gateway de aplicativo dá suporte a terminação SSL no gateway, pelo qual o tráfego flui geralmente descriptografado até os servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e29f-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="1e29f-105">Esse recurso permite que os servidores Web fiquem livres da sobrecarga da criptografia e descriptografia dispendiosa.</span><span class="sxs-lookup"><span data-stu-id="1e29f-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="1e29f-106">No entanto, para alguns clientes, a comunicação descriptografada com os servidores de back-end não é uma opção aceitável.</span><span class="sxs-lookup"><span data-stu-id="1e29f-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="1e29f-107">Essa comunicação não criptografada pode ocorrer devido a requisitos de segurança e conformidade ou o aplicativo só pode aceitar uma conexão segura.</span><span class="sxs-lookup"><span data-stu-id="1e29f-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="1e29f-108">Para tais aplicativos, o gateway de aplicativo dá suporte à criptografia SSL de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="1e29f-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="1e29f-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1e29f-109">Overview</span></span>

<span data-ttu-id="1e29f-110">O SSL de ponta a ponta permite transmitir com segurança dados confidenciais para o back-end criptografado aproveitando as vantagens dos recursos de balanceamento de carga da Camada 7 que o gateway de aplicativo fornece.</span><span class="sxs-lookup"><span data-stu-id="1e29f-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="1e29f-111">Alguns desses recursos têm uma afinidade de sessão baseada em cookies, um roteamento baseado em URL, suporte para o roteamento com base em sites ou a capacidade de injetar cabeçalhos X-Forwarded-*.</span><span class="sxs-lookup"><span data-stu-id="1e29f-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.</span></span>

<span data-ttu-id="1e29f-112">Quando configurado com o modo de comunicação SSL de ponta a ponta, o gateway de aplicativo encerra as sessões SSL no gateway e descriptografa o tráfego do usuário.</span><span class="sxs-lookup"><span data-stu-id="1e29f-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="1e29f-113">Ele aplica as regras configuradas para selecionar uma instância de pool de back-end apropriada para rotear o tráfego.</span><span class="sxs-lookup"><span data-stu-id="1e29f-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="1e29f-114">Depois, o gateway de aplicativo inicia uma nova conexão SSL com o servidor de back-end e criptografa novamente os dados usando o certificado de chave pública do servidor de back-end antes de transmitir a solicitação ao back-end.</span><span class="sxs-lookup"><span data-stu-id="1e29f-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="1e29f-115">O SSL de ponta a ponta é habilitado definindo a configuração de protocolo em BackendHTTPSetting para HTTPS, que é então aplicado a um pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="1e29f-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="1e29f-116">Cada servidor de back-end no pool de back-end com SSL de ponta a ponta habilitado deve ser configurado com um certificado para permitir uma comunicação segura.</span><span class="sxs-lookup"><span data-stu-id="1e29f-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![cenário do ssl de ponta a ponta][1]

<span data-ttu-id="1e29f-118">Neste exemplo, as solicitações que usam o TLS1.2 são roteadas para os servidores de back-end no Pool1 usando o SSL de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="1e29f-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="1e29f-119">SSL de ponta a ponta e lista de exceções de certificados</span><span class="sxs-lookup"><span data-stu-id="1e29f-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="1e29f-120">O gateway de aplicativo se comunica somente com as instâncias de back-end conhecidas que têm o certificado na lista de exceções do gateway.</span><span class="sxs-lookup"><span data-stu-id="1e29f-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="1e29f-121">Para habilitar a lista de exceções dos certificados, você precisa carregar a chave pública dos certificados do servidor de back-end no gateway de aplicativo (não no certificado-raiz).</span><span class="sxs-lookup"><span data-stu-id="1e29f-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="1e29f-122">Somente as conexões com os back-ends conhecidos e na lista de exceções são permitidas.</span><span class="sxs-lookup"><span data-stu-id="1e29f-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="1e29f-123">O back-ends restantes resultam em um erro de gateway.</span><span class="sxs-lookup"><span data-stu-id="1e29f-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="1e29f-124">Os certificados autoassinados servem somente para teste e não são recomendados para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="1e29f-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="1e29f-125">Esses certificados devem estar na lista de exceções do gateway de aplicativo, conforme descrito nas etapas acima, antes de poder ser usados.</span><span class="sxs-lookup"><span data-stu-id="1e29f-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e29f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e29f-126">Next steps</span></span>

<span data-ttu-id="1e29f-127">Depois de aprender sobre o SSL de ponta a ponta, vá e [habilite o SSL de ponta a ponta no gateway de aplicativo](application-gateway-end-to-end-ssl-powershell.md) para criar um gateway de aplicativo usando esse SSL.</span><span class="sxs-lookup"><span data-stu-id="1e29f-127">After learning about end to end SSL, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
