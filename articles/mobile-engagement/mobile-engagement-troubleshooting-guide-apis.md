---
title: aaaAzure Mobile Engagement Troubleshooting Guide - APIs
description: "Guias de solução de problemas para o Azure Mobile Engagement - APIs"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="486a9-103">Guia de solução de problemas de API</span><span class="sxs-lookup"><span data-stu-id="486a9-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="486a9-104">Olá seguem possíveis problemas que podem ser encontrados em como os administradores interagem com o Azure Mobile Engagement por meio de APIs de saudação.</span><span class="sxs-lookup"><span data-stu-id="486a9-104">hello following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via hello APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="486a9-105">Problemas de sintaxe</span><span class="sxs-lookup"><span data-stu-id="486a9-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="486a9-106">Problema</span><span class="sxs-lookup"><span data-stu-id="486a9-106">Issue</span></span>
* <span data-ttu-id="486a9-107">Erros de sintaxe usando Olá API (ou um comportamento inesperado).</span><span class="sxs-lookup"><span data-stu-id="486a9-107">Syntax Errors using hello API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="486a9-108">Causas</span><span class="sxs-lookup"><span data-stu-id="486a9-108">Causes</span></span>
* <span data-ttu-id="486a9-109">Problemas de sintaxe:</span><span class="sxs-lookup"><span data-stu-id="486a9-109">Syntax issues:</span></span>
  * <span data-ttu-id="486a9-110">Certifique-se de que toocheck Olá Olá API específica que você está usando sintaxe tooconfirm que Olá opção está disponível.</span><span class="sxs-lookup"><span data-stu-id="486a9-110">Make sure toocheck hello Syntax of hello specific API you are using tooconfirm that hello option is available.</span></span>
  * <span data-ttu-id="486a9-111">Um problema comum com o uso da API é tooconfuse Olá alcance API e hello API Push (a maioria das tarefas deve ser executada com hello API de alcance em vez da saudação API Push).</span><span class="sxs-lookup"><span data-stu-id="486a9-111">A common issue with API usage is tooconfuse hello Reach API and hello Push API (most tasks should be performed with hello Reach API instead of hello Push API).</span></span> 
  * <span data-ttu-id="486a9-112">Outro problema comum com integração SDK e o uso da API é tooconfuse hello chave SDK e Olá chave de API.</span><span class="sxs-lookup"><span data-stu-id="486a9-112">Another common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>
  * <span data-ttu-id="486a9-113">Scripts que se conectam toohello APIs precisam dados toosend pelo menos a cada 10 minutos ou conexão Olá atingirá o tempo limite (especialmente comum em scripts de API do Monitor escutando dados).</span><span class="sxs-lookup"><span data-stu-id="486a9-113">Scripts that connect toohello APIs need toosend data at least every 10 minutes or hello connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="486a9-114">tempos limite de tooprevent, tem seu envio script um ping XMPP cada sessão de atividade com o servidor de saudação Olá do tookeep de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="486a9-114">tooprevent timeouts, have your script send an XMPP ping every 10 minutes tookeep hello session alive with hello server.</span></span>

### <a name="see-also"></a><span data-ttu-id="486a9-115">Consulte também</span><span class="sxs-lookup"><span data-stu-id="486a9-115">See also</span></span>
* <span data-ttu-id="486a9-116">[Documentação da API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="486a9-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="486a9-117">Informações do protocolo XMPP</span><span class="sxs-lookup"><span data-stu-id="486a9-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a><span data-ttu-id="486a9-118">Não é possível toouse Olá API tooperform Olá mesma ação disponível em Olá interface de usuário do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="486a9-118">Unable toouse hello API tooperform hello same action available in hello Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="486a9-119">Problema</span><span class="sxs-lookup"><span data-stu-id="486a9-119">Issue</span></span>
* <span data-ttu-id="486a9-120">Uma ação que funciona da saudação de que interface de usuário do Azure Mobile Engagement não funcionar da saudação relacionadas a API do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="486a9-120">An action that works from hello Azure Mobile Engagement UI doesn't work from hello related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="486a9-121">Causas</span><span class="sxs-lookup"><span data-stu-id="486a9-121">Causes</span></span>
* <span data-ttu-id="486a9-122">Confirmar que você pode realizar Olá mesma ação de saudação do Azure Mobile Engagement UI mostra corretamente integraram esse recurso do Azure Mobile Engagement com hello SDK.</span><span class="sxs-lookup"><span data-stu-id="486a9-122">Confirming that you can perform hello same action from hello Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with hello SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="486a9-123">Consulte também</span><span class="sxs-lookup"><span data-stu-id="486a9-123">See also</span></span>
* <span data-ttu-id="486a9-124">[Documentação da Interface do Usuário][Link 1]</span><span class="sxs-lookup"><span data-stu-id="486a9-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="486a9-125">Mensagens de erro</span><span class="sxs-lookup"><span data-stu-id="486a9-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="486a9-126">Problema</span><span class="sxs-lookup"><span data-stu-id="486a9-126">Issue</span></span>
* <span data-ttu-id="486a9-127">Códigos de erro usando a API de saudação exibido em tempo de execução ou nos logs.</span><span class="sxs-lookup"><span data-stu-id="486a9-127">Error codes using hello API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="486a9-128">Causas</span><span class="sxs-lookup"><span data-stu-id="486a9-128">Causes</span></span>
* <span data-ttu-id="486a9-129">Veja uma lista composta de números de códigos de status comuns da API para referência e a solução de problemas preliminar:</span><span class="sxs-lookup"><span data-stu-id="486a9-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a><span data-ttu-id="486a9-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="486a9-130">See also</span></span>
* <span data-ttu-id="486a9-131">[Documentação da API – para erros detalhados sobre cada API específica][Link 4]</span><span class="sxs-lookup"><span data-stu-id="486a9-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="486a9-132">Falhas silenciosas</span><span class="sxs-lookup"><span data-stu-id="486a9-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="486a9-133">Problema</span><span class="sxs-lookup"><span data-stu-id="486a9-133">Issue</span></span>
* <span data-ttu-id="486a9-134">A ação da API falha sem nenhuma mensagem de erro exibida em tempo de execução ou nos logs.</span><span class="sxs-lookup"><span data-stu-id="486a9-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="486a9-135">Causas</span><span class="sxs-lookup"><span data-stu-id="486a9-135">Causes</span></span>
* <span data-ttu-id="486a9-136">Número de itens será desabilitado Olá interface de usuário do Azure Mobile Engagement se não estiver integrados corretamente, mas falhará em modo silencioso da saudação API, portanto Lembre-se tootest Olá a mesma funcionalidade de saudação da interface do usuário toosee se ele funciona.</span><span class="sxs-lookup"><span data-stu-id="486a9-136">Many items will be disabled in hello Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from hello API, so remember tootest hello same functionality from hello UI toosee if it works.</span></span>
* <span data-ttu-id="486a9-137">O Azure Mobile Engagement e vários recursos avançados do Azure Mobile Engagement, você está tentando executar toouse, toobe necessidade individualmente integrado ao seu aplicativo com o SDK do hello como etapas separadas antes de você pode usá-los.</span><span class="sxs-lookup"><span data-stu-id="486a9-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting toouse, need toobe individually integrated into your app with hello SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="486a9-138">Consulte também</span><span class="sxs-lookup"><span data-stu-id="486a9-138">See also</span></span>
* <span data-ttu-id="486a9-139">[Guia de Solução de Problemas ‑ SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="486a9-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

