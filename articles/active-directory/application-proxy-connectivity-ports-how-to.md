---
title: "as portas de firewall Olá tooopen aaaHow necessárias para um aplicativo de Proxy de aplicativo | Microsoft Docs"
description: "Descubra quais tooopen portas para toowork de Proxy de aplicativo de saudação do AD do Azure corretamente"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="79528-103">Como tooopen Olá portas de firewall necessárias para um aplicativo de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="79528-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="79528-104">toosee uma lista completa de portas Olá necessários e a função de saudação de cada porta, consulte a seção pré-requisitos Olá Olá [documentação do Proxy de aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="79528-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="79528-105">observe que o Application Proxy usa apenas as portas de saída.</span><span class="sxs-lookup"><span data-stu-id="79528-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="79528-106">Você também pode verificar se há todas Olá necessárias portas abertas, abrindo Olá [ferramenta de teste de portas do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) da sua rede local.</span><span class="sxs-lookup"><span data-stu-id="79528-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="79528-107">Mais marcas de seleção verde significa maior resiliência.</span><span class="sxs-lookup"><span data-stu-id="79528-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="79528-108">Regiões de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="79528-108">App Proxy regions</span></span>

<span data-ttu-id="79528-109">Estamos trabalhando em um modo toolet você sabe que essas regiões precisa toobe verde para você.</span><span class="sxs-lookup"><span data-stu-id="79528-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="79528-110">Por enquanto, certifique-se de que todas estão verdes.</span><span class="sxs-lookup"><span data-stu-id="79528-110">For now, make sure they all are.</span></span> <span data-ttu-id="79528-111">EUA Central também é necessária, independentemente de qual região você está.</span><span class="sxs-lookup"><span data-stu-id="79528-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="79528-112">toomake se Olá ferramenta oferece Olá resultados à direita, ser-se:</span><span class="sxs-lookup"><span data-stu-id="79528-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="79528-113">Abra a ferramenta de saudação em um navegador do servidor de saudação onde você instalou Olá conector.</span><span class="sxs-lookup"><span data-stu-id="79528-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="79528-114">Certifique-se de que qualquer tooyour aplicável proxies ou firewalls conector também são aplicadas toothis página.</span><span class="sxs-lookup"><span data-stu-id="79528-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="79528-115">Isso pode ser feito no Internet Explorer indo muito**configurações**  - &gt; **opções da Internet**  - &gt; **conexões**  - &gt; **Configurações da Lan**.</span><span class="sxs-lookup"><span data-stu-id="79528-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="79528-116">Nessa página, você deve ver campo hello "Usar um Proxy do servidor para sua LAN".</span><span class="sxs-lookup"><span data-stu-id="79528-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="79528-117">Marque esta caixa e coloque o endereço de proxy de saudação no campo de "Address" hello.</span><span class="sxs-lookup"><span data-stu-id="79528-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79528-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79528-118">Next steps</span></span>
[<span data-ttu-id="79528-119">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79528-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
