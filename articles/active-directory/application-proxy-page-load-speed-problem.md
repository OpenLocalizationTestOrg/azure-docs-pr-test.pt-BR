---
title: Um aplicativo de Proxy de Aplicativo demora muito para carregar | Microsoft Docs
description: "Solucionar problemas de desempenho de carregamento de página com o Proxy de Aplicativo do Azure AD"
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
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="d3302-103">Um aplicativo de Proxy de Aplicativo demora muito para carregar</span><span class="sxs-lookup"><span data-stu-id="d3302-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="d3302-104">Este artigo ajuda-o a entender porque um aplicativo de Proxy de Aplicativo do Azure AD pode demorar muito tempo para carregar e o que pode ser feito para resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="d3302-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="d3302-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d3302-105">Overview</span></span>
<span data-ttu-id="d3302-106">Se seus aplicativos estão funcionando, mas você percebe uma longa latência, pode haver alguns pequenos ajustes na sua topologia de rede que podem ser considerados para melhorar a velocidade.</span><span class="sxs-lookup"><span data-stu-id="d3302-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="d3302-107">Para uma avaliação de diferentes topologias, consulte o [documento de considerações de rede](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="d3302-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="d3302-108">Se essas considerações não ajudarem, infelizmente nós não temos atualmente outras recomendações para ajuste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="d3302-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="d3302-109">À medida que o serviço de Proxy de Aplicativo se expande para mais data centers que podem estar mais próximos a você, será possível começar a perceber a latência melhorada diretamente.</span><span class="sxs-lookup"><span data-stu-id="d3302-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="d3302-110">Para ver a lista completa de data centers do Azure, você pode consultar a [página de teste de latência](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="d3302-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="d3302-111">Os data centers com o serviço de Proxy de Aplicativo podem ser localizados com a [Ferramenta de Teste de Portas do Conector](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="d3302-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="d3302-112">Comentários sobre locais de data centers do Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d3302-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="d3302-113">Pode existir data centers do Azure que ainda não incluem Proxy de Aplicativo, mas poderiam conduzi-lo a uma grande melhoria de latência.</span><span class="sxs-lookup"><span data-stu-id="d3302-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="d3302-114">Locais de data center em <aadapfeedback@microsoft.com>, desse modo, podemos usar seu comentário para planejar conforme expandimos.</span><span class="sxs-lookup"><span data-stu-id="d3302-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="d3302-115">Nós estamos trabalhando em alguns recursos adicionais que ajudam a melhorar a latência para locatários que atualmente percebem latências longas e, assegure-se de compartilhar a documentação disponível.</span><span class="sxs-lookup"><span data-stu-id="d3302-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3302-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3302-116">Next steps</span></span>
[<span data-ttu-id="d3302-117">Trabalhar com servidores proxy locais existentes</span><span class="sxs-lookup"><span data-stu-id="d3302-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
