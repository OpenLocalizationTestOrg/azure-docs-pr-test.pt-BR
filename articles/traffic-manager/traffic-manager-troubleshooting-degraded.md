---
title: "Solucionando problemas de status degradado do Gerenciador de Tráfego"
description: "Como solucionar problemas de perfis do Gerenciador de Tráfego quando ele aparece com status de degradado."
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
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="5a5e8-103">Solucionando problemas de status degradado do Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="5a5e8-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="5a5e8-104">Este artigo descreve como solucionar problemas de um perfil do Gerenciador de Tráfego do Azure que mostra um estado degradado.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="5a5e8-105">Para esse cenário, considere a possibilidade de que você configurou um perfil do Gerenciador de Tráfego apontando para alguns dos serviços hospedados do cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="5a5e8-106">Se a integridade do seu Gerenciador de Tráfego exibe um status **Degradado**, o status de um ou mais pontos de extremidade pode ser **Degradado**:</span><span class="sxs-lookup"><span data-stu-id="5a5e8-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![status do ponto de extremidade degradado](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="5a5e8-108">Se a integridade do seu Gerenciador de Tráfego exibe um status **Inativo**, ambos os pontos de extremidade podem ser **Desabilitado**:</span><span class="sxs-lookup"><span data-stu-id="5a5e8-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Status do Gerenciador de Tráfego Inativo](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="5a5e8-110">Noções básicas sobre as investigações do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="5a5e8-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="5a5e8-111">O Gerenciador de Tráfego considera um ponto de extremidade como estando ONLINE somente quando a investigação recebe uma resposta HTTP 200 do caminho de investigação.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="5a5e8-112">Qualquer outra resposta diferente de 200 é uma falha.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="5a5e8-113">Um redirecionamento 30x falha, mesmo se a URL redirecionada retorna uma resposta 200.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="5a5e8-114">Para investigações de HTTPs, os erros de certificado são ignorados.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="5a5e8-115">O conteúdo real do caminho de investigação não importa, contanto que uma resposta 200 seja retornada.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="5a5e8-116">A investigação de uma URL para algum conteúdo estático como “/favicon.ico” é uma técnica comum.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="5a5e8-117">O conteúdo dinâmico, como as páginas ASP, nem sempre poderá retornar a resposta 200, mesmo quando o aplicativo estiver íntegro.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="5a5e8-118">Uma prática recomendada é definir o caminho de Investigação como algo que tenha lógica suficiente para determinar se o site está ativo ou inativo.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="5a5e8-119">No exemplo anterior, ao configurar o caminho como “/favicon.ico”, você está apenas testando se w3wp.exe está respondendo.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="5a5e8-120">Essa investigação pode não indicar que o aplicativo Web está íntegro.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="5a5e8-121">Uma opção melhor seria definir um caminho para algo como “/Probe.aspx”, que tem lógica para determinar a integridade do site.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="5a5e8-122">Por exemplo, você poderá usar contadores de desempenho para a utilização da CPU ou medir o número de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="5a5e8-123">Se preferir, você poderá tentar acessar os recursos de banco de dados ou o estado de sessão para verificar se o aplicativo Web está funcionando.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="5a5e8-124">Se todos os pontos de extremidade em um perfil estiverem degradados, o Gerenciador de Tráfego tratará todos os pontos de extremidade como íntegros e encaminhará o tráfego para todos eles.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="5a5e8-125">Esse comportamento garante que os problemas com o mecanismo de investigação não resultam em uma interrupção completa do serviço.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5a5e8-126">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="5a5e8-126">Troubleshooting</span></span>

<span data-ttu-id="5a5e8-127">Para solucionar uma falha de investigação, você precisa de uma ferramenta que mostra o retorno de código de status HTTP da URL de investigação.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="5a5e8-128">Há várias ferramentas disponíveis que mostram a resposta HTTP bruta.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="5a5e8-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="5a5e8-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="5a5e8-130">curl</span><span class="sxs-lookup"><span data-stu-id="5a5e8-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="5a5e8-131">wget</span><span class="sxs-lookup"><span data-stu-id="5a5e8-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="5a5e8-132">Além disso, você pode usar a guia Rede das Ferramentas de Depuração F12 no Internet Explorer para exibir as respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="5a5e8-133">Neste exemplo, queremos ver a resposta de nossa URL de investigação: http://watestsdp2008r2.cloudapp.net:80/Probe.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="5a5e8-134">O exemplo do PowerShell a seguir ilustra o problema.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="5a5e8-135">Saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="5a5e8-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="5a5e8-136">Observe que recebemos uma resposta de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="5a5e8-137">Como mencionamos anteriormente, qualquer StatusCode diferente de 200 é considerado uma falha.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="5a5e8-138">O Gerenciador de Tráfego altera o status do ponto de extremidade para Offline.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="5a5e8-139">Para resolver o problema, verifique a configuração do site para garantir que o StatusCode apropriado pode ser retornado do caminho de investigação.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="5a5e8-140">Reconfigure a investigação do Gerenciador de Tráfego para que ela aponte para um caminho que retorna uma resposta 200.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="5a5e8-141">Se a investigação estiver usando o protocolo HTTPS, talvez seja necessário desabilitar a verificação de certificado, para evitar erros de SSL/TLS durante o teste.</span><span class="sxs-lookup"><span data-stu-id="5a5e8-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="5a5e8-142">As seguintes instruções do PowerShell desabilitam a validação de certificado na sessão atual do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5a5e8-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5a5e8-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a5e8-143">Next Steps</span></span>

[<span data-ttu-id="5a5e8-144">Sobre os métodos de roteamento de tráfego do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="5a5e8-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="5a5e8-145">O que é o Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="5a5e8-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="5a5e8-146">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="5a5e8-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="5a5e8-147">Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="5a5e8-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="5a5e8-148">Operações no Gerenciador de Tráfego (referência de API REST)</span><span class="sxs-lookup"><span data-stu-id="5a5e8-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="5a5e8-149">[Cmdlets do Gerenciador de Tráfego do Azure][1]</span><span class="sxs-lookup"><span data-stu-id="5a5e8-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
