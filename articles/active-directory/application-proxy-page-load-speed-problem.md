---
title: aaaAn aplicativo Proxy de aplicativo usa muito tooload | Microsoft Docs
description: "Solucionar problemas de desempenho de carregamento de página com hello Proxy de aplicativo do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="5088b-103">Um aplicativo de Proxy de aplicativo usa tooload muito longo</span><span class="sxs-lookup"><span data-stu-id="5088b-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="5088b-104">Este artigo ajuda toounderstand por que um aplicativo de Proxy de aplicativo do Azure AD pode levar um tooload muito tempo e o que você pode fazer tooresolve esse problema.</span><span class="sxs-lookup"><span data-stu-id="5088b-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="5088b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5088b-105">Overview</span></span>
<span data-ttu-id="5088b-106">Se os aplicativos estão funcionando, mas você verá uma longa latência, pode haver alguns ajustes secundários em sua topologia de rede que você pode considerar a velocidade de saudação tooimprove.</span><span class="sxs-lookup"><span data-stu-id="5088b-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="5088b-107">Para uma avaliação das diferentes topologias, consulte Olá [documento de considerações de rede](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="5088b-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="5088b-108">Se essas considerações não ajudarem, infelizmente nós não temos atualmente outras recomendações para ajuste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="5088b-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="5088b-109">Como Olá serviço Proxy de aplicativo expande toomore centros de dados que podem ser tooyou mais próximo, você pode iniciar toosee aprimorado latência diretamente.</span><span class="sxs-lookup"><span data-stu-id="5088b-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="5088b-110">centros de lista completa de saudação de toosee de dados do Azure, você pode ver Olá [página de teste de latência](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="5088b-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="5088b-111">Olá centros de dados com o serviço de Proxy de aplicativo hello podem ser encontrados com hello [ferramenta de teste de portas do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="5088b-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="5088b-112">Comentários sobre locais de data centers do Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5088b-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="5088b-113">Pode haver data centers do Azure que ainda não incluam o Proxy de aplicativo, mas levam tooa aperfeiçoamento de latência excelentes para você.</span><span class="sxs-lookup"><span data-stu-id="5088b-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="5088b-114">saudação de datacenter local < aadapfeedback@microsoft.com > para que possamos pode usar seu tooplan comentários como podemos expandir.</span><span class="sxs-lookup"><span data-stu-id="5088b-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="5088b-115">Estamos trabalhando em alguns recursos adicionais que ajudam a melhorar a latência de saudação para locatários que atualmente consulte latências de longo e ser documentação em tooshare-se de que quando estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="5088b-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5088b-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5088b-116">Next steps</span></span>
[<span data-ttu-id="5088b-117">Trabalhar com servidores proxy locais existentes</span><span class="sxs-lookup"><span data-stu-id="5088b-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
