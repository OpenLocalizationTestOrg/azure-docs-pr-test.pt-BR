---
title: aaaEnabling final tooend SSL no Gateway de aplicativo do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral da saudação Application Gateway final tooend suporte para SSL."
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
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="d9626-103">Visão geral do fim tooend SSL com o Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d9626-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="d9626-104">Gateway de aplicativo oferece suporte a terminação SSL no gateway hello, depois que o tráfego que flui geralmente descriptografados toohello servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="d9626-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="d9626-105">Esse recurso permite toobe de servidores de web unburdened da sobrecarga de criptografia e descriptografia cara.</span><span class="sxs-lookup"><span data-stu-id="d9626-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="d9626-106">No entanto para alguns clientes a servidores de back-end de toohello de comunicação não criptografada não é uma opção aceitável.</span><span class="sxs-lookup"><span data-stu-id="d9626-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="d9626-107">Essa comunicação não criptografada pode ser devido a requisitos de toosecurity, requisitos de conformidade, ou o aplicativo hello só pode aceitar uma conexão segura.</span><span class="sxs-lookup"><span data-stu-id="d9626-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="d9626-108">Para tais aplicativos, o gateway de aplicativo oferece suporte a tooend final SSL criptografia.</span><span class="sxs-lookup"><span data-stu-id="d9626-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="d9626-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d9626-109">Overview</span></span>

<span data-ttu-id="d9626-110">Final tooend SSL permite que você toosecurely transmitir dados confidenciais toohello back-end criptografado enquanto ainda tirar proveito dos benefícios de saudação de recursos de balanceamento de carga de camada 7 qual gateway de aplicativo fornece.</span><span class="sxs-lookup"><span data-stu-id="d9626-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="d9626-111">Alguns desses recursos são a afinidade de sessão baseada em cookie, roteamento baseado em URL, o suporte para roteamento baseado em sites ou capacidade tooinject X - encaminhado-* cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="d9626-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="d9626-112">Quando configurado com o modo de comunicação do end tooend SSL, o gateway de aplicativo encerra as sessões SSL Olá no gateway hello e descriptografa o tráfego do usuário.</span><span class="sxs-lookup"><span data-stu-id="d9626-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="d9626-113">Ele aplica Olá configurado regras tooselect um back-end apropriado pool instância tooroute tráfego.</span><span class="sxs-lookup"><span data-stu-id="d9626-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="d9626-114">Gateway de aplicativo, em seguida, inicia um novo servidor de back-end de toohello de conexão SSL e criptografa novamente dados usando o certificado de chave pública do servidor de back-end Olá antes de transmitir o back-end do hello solicitação toohello.</span><span class="sxs-lookup"><span data-stu-id="d9626-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="d9626-115">Tooend final que SSL está habilitado, definindo a configuração de protocolo no BackendHTTPSetting tooHTTPS, que é então aplicado tooa pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="d9626-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="d9626-116">Cada servidor de back-end no pool de back-end de saudação com tooend final que SSL habilitado deve ser configurado com uma certificado tooallow uma comunicação segura.</span><span class="sxs-lookup"><span data-stu-id="d9626-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![cenário de ssl tooend final][1]

<span data-ttu-id="d9626-118">Neste exemplo, solicitações que usam o TLS 1.2 são servidores toobackend roteadas em Pool1 usando tooend final SSL.</span><span class="sxs-lookup"><span data-stu-id="d9626-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="d9626-119">Encerrar tooend SSL e a lista branca de certificados</span><span class="sxs-lookup"><span data-stu-id="d9626-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="d9626-120">Gateway de aplicativo se comunica somente com instâncias de back-end conhecidos que têm o certificado com o gateway de aplicativo hello de na lista de permissões.</span><span class="sxs-lookup"><span data-stu-id="d9626-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="d9626-121">tooenable lista branca de certificados, você deve carregar a chave pública de saudação do gateway de aplicativo de toohello para certificados de servidor back-end (não o certificado raiz de saudação).</span><span class="sxs-lookup"><span data-stu-id="d9626-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="d9626-122">Somente back-ends conexões tooknown e na lista de permissões, em seguida, são permitidas.</span><span class="sxs-lookup"><span data-stu-id="d9626-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="d9626-123">Olá restantes back-ends resulta em um erro de gateway.</span><span class="sxs-lookup"><span data-stu-id="d9626-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="d9626-124">Os certificados autoassinados servem somente para teste e não são recomendados para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="d9626-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="d9626-125">Esses certificados tem toobe na lista de permissões com hello application gateway conforme descrito nas etapas anteriores para que possam ser usados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9626-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9626-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9626-126">Next steps</span></span>

<span data-ttu-id="d9626-127">Depois de conhecer final tooend SSL, vá muito[habilitar final tooend SSL no gateway do aplicativo](application-gateway-end-to-end-ssl-powershell.md) toocreate um gateway de aplicativo usando finalizar tooend SSL.</span><span class="sxs-lookup"><span data-stu-id="d9626-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
