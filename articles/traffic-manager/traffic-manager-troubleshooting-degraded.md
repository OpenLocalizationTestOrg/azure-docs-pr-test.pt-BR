---
title: status de aaaTroubleshooting degradado no Azure Traffic Manager
description: "Como perfis de Gerenciador de tráfego tootroubleshoot quando ele aparece como status degradado."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="7bc2b-103">Solucionando problemas de status degradado do Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="7bc2b-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="7bc2b-104">Este artigo descreve como tootroubleshoot um perfil do Gerenciador de tráfego do Azure que está mostrando um estado degradado.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="7bc2b-105">Para este cenário, considere a possibilidade de que você tenha configurado um perfil do Gerenciador de tráfego apontando toosome de seus serviços hospedados de cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="7bc2b-106">Se a integridade de saudação do seu Traffic Manager exibe um **degradado** status e status de saudação de um ou mais pontos de extremidade podem ser **degradado**:</span><span class="sxs-lookup"><span data-stu-id="7bc2b-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![status do ponto de extremidade degradado](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="7bc2b-108">Se a integridade de saudação do seu Traffic Manager exibe um **inativo** status e, em seguida, os dois pontos de extremidade podem ser **desabilitado**:</span><span class="sxs-lookup"><span data-stu-id="7bc2b-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Status do Gerenciador de Tráfego Inativo](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="7bc2b-110">Noções básicas sobre as investigações do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="7bc2b-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="7bc2b-111">Gerenciador de tráfego considera um toobe de ponto de extremidade ONLINE somente quando o teste de saudação recebe uma resposta HTTP 200 fazer do caminho de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="7bc2b-112">Qualquer outra resposta diferente de 200 é uma falha.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="7bc2b-113">Um redirecionamento 30 x falha, mesmo se Olá redirecionado URL retorna uma resposta 200.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="7bc2b-114">Para investigações de HTTPs, os erros de certificado são ignorados.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="7bc2b-115">conteúdo real de saudação do caminho de investigação de saudação não importa, desde que uma resposta 200 é retornado.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="7bc2b-116">Um tipo de conteúdo estático do toosome URL de investigação "/ favicon.ico" é uma técnica comum.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="7bc2b-117">Conteúdo dinâmico, como as páginas ASP hello, talvez nem sempre retorna 200, mesmo quando o aplicativo hello está íntegro.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="7bc2b-118">Uma prática recomendada é tooset Olá investigação toosomething de caminho que tem suficiente toodetermine lógica que Olá site está ativa ou inativa.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="7bc2b-119">Em Olá exemplo anterior, definindo Olá caminho too"/favicon.ico", você está apenas testar essa w3wp.exe está respondendo.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="7bc2b-120">Essa investigação pode não indicar que o aplicativo Web está íntegro.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="7bc2b-121">Uma opção melhor seria tooset tooa um caminho algo como "/ Probe.aspx" que tem lógica de integridade de saudação de toodetermine do site de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="7bc2b-122">Por exemplo, você pode usar a utilização de tooCPU de contadores de desempenho ou medida Olá número de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="7bc2b-123">Ou, você poderá tentar tooaccess recursos de banco de dados ou toomake de estado de sessão-se de que o aplicativo da web hello está funcionando.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="7bc2b-124">Se todos os pontos de extremidade em um perfil estão degradados, o Traffic Manager tratará todos os pontos de extremidade como íntegro e rotas tráfego tooall pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="7bc2b-125">Esse comportamento garante que problemas com hello mecanismo de sondagem não resultam em uma falha completa do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7bc2b-126">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="7bc2b-126">Troubleshooting</span></span>

<span data-ttu-id="7bc2b-127">tootroubleshoot uma falha de teste, você precisa de uma ferramenta que mostra o código de status HTTP Olá retorno da URL de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="7bc2b-128">Há muitas ferramentas disponíveis que mostram Olá bruta resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="7bc2b-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="7bc2b-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="7bc2b-130">curl</span><span class="sxs-lookup"><span data-stu-id="7bc2b-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="7bc2b-131">wget</span><span class="sxs-lookup"><span data-stu-id="7bc2b-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="7bc2b-132">Além disso, você pode usar o guia de rede de saudação do hello F12 ferramentas de depuração em respostas HTTP do Internet Explorer tooview hello.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="7bc2b-133">Neste exemplo, queremos toosee resposta de saudação do nosso URL de investigação: http://watestsdp2008r2.cloudapp.net:80/investigação.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="7bc2b-134">Olá PowerShell de exemplo a seguir ilustra o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="7bc2b-135">Saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7bc2b-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="7bc2b-136">Observe que recebemos uma resposta de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="7bc2b-137">Como mencionamos anteriormente, qualquer StatusCode diferente de 200 é considerado uma falha.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="7bc2b-138">Alterações de Gerenciador de tráfego Olá tooOffline de status do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="7bc2b-139">problema de saudação tooresolve, seleção Olá site configuração tooensure que Olá StatusCode adequada pode ser retornado do caminho de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="7bc2b-140">Reconfigure Olá Traffic Manager investigação toopoint tooa caminho que retorna uma resposta 200.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="7bc2b-141">Se o teste é usando Olá protocolo HTTPS, talvez seja necessário certificado toodisable verificação de erros SSL/TLS tooavoid durante o teste.</span><span class="sxs-lookup"><span data-stu-id="7bc2b-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="7bc2b-142">Olá, instruções a seguir do PowerShell desabilitar validação de certificado para a sessão atual do PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="7bc2b-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="7bc2b-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7bc2b-143">Next Steps</span></span>

[<span data-ttu-id="7bc2b-144">Sobre os métodos de roteamento de tráfego do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="7bc2b-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="7bc2b-145">O que é o Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="7bc2b-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="7bc2b-146">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="7bc2b-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="7bc2b-147">Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="7bc2b-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="7bc2b-148">Operações no Gerenciador de Tráfego (referência de API REST)</span><span class="sxs-lookup"><span data-stu-id="7bc2b-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="7bc2b-149">[Cmdlets do Gerenciador de Tráfego do Azure][1]</span><span class="sxs-lookup"><span data-stu-id="7bc2b-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
