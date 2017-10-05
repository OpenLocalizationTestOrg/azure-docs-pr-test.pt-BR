---
title: "Como abrir as portas de firewall necessárias para um aplicativo de Application Proxy | Microsoft Docs"
description: Descubra quais portas abrir para o Application Proxy do Azure AD funcionar corretamente
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="13bd7-103">Como abrir as portas de firewall necessárias para um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="13bd7-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="13bd7-104">Para ver uma lista completa das portas necessárias e a função de cada porta, consulte a seção pré-requisitos da [documentação de Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="13bd7-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="13bd7-105">observe que o Application Proxy usa apenas as portas de saída.</span><span class="sxs-lookup"><span data-stu-id="13bd7-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="13bd7-106">Você também pode verificar se você tem todas as portas abertas necessárias, abrindo a [ferramenta de teste de portas do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) de sua rede local.</span><span class="sxs-lookup"><span data-stu-id="13bd7-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="13bd7-107">Mais marcas de seleção verde significa maior resiliência.</span><span class="sxs-lookup"><span data-stu-id="13bd7-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="13bd7-108">Regiões de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="13bd7-108">App Proxy regions</span></span>

<span data-ttu-id="13bd7-109">Estamos trabalhando em uma maneira para que você saiba que essas regiões precisam estar verdes para você.</span><span class="sxs-lookup"><span data-stu-id="13bd7-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="13bd7-110">Por enquanto, certifique-se de que todas estão verdes.</span><span class="sxs-lookup"><span data-stu-id="13bd7-110">For now, make sure they all are.</span></span> <span data-ttu-id="13bd7-111">EUA Central também é necessária, independentemente de qual região você está.</span><span class="sxs-lookup"><span data-stu-id="13bd7-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="13bd7-112">Para certificar-se de que a ferramenta oferece os resultados certos, certifique-se de:</span><span class="sxs-lookup"><span data-stu-id="13bd7-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="13bd7-113">Abrir a ferramenta em um navegador do servidor na qual você instalou o conector.</span><span class="sxs-lookup"><span data-stu-id="13bd7-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="13bd7-114">Certifique-se de que quaisquer proxies ou firewalls aplicáveis a seu conector também estejam aplicados a esta página.</span><span class="sxs-lookup"><span data-stu-id="13bd7-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="13bd7-115">Isso pode ser feito no Internet Explorer, vá para **Configurações** -&gt;**Opções da Internet** -&gt;**Conexões** -&gt;**Configurações da Lan**.</span><span class="sxs-lookup"><span data-stu-id="13bd7-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="13bd7-116">Nessa página, você vê o campo "Use um Servidor Proxy para sua LAN".</span><span class="sxs-lookup"><span data-stu-id="13bd7-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="13bd7-117">Marque essa caixa e coloque o endereço do proxy no campo "Endereço".</span><span class="sxs-lookup"><span data-stu-id="13bd7-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13bd7-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13bd7-118">Next steps</span></span>
[<span data-ttu-id="13bd7-119">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bd7-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
