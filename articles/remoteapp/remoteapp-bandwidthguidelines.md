---
title: aaaAzure RemoteApp de largura de banda - diretrizes gerais | Microsoft Docs
description: "Compreenda algumas diretrizes básicas de largura de banda de rede para as coleções e aplicativos do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="037f1-103">Largura de banda de rede do Azure RemoteApp - diretrizes gerais (se não puder testar a sua)</span><span class="sxs-lookup"><span data-stu-id="037f1-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="037f1-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="037f1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="037f1-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="037f1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="037f1-106">Se você não tiver Olá tempo ou a funcionalidade de toorun Olá [testes de largura de banda de rede](remoteapp-bandwidthtests.md) do Azure RemoteApp, aqui estão algumas diretrizes razoavelmente genéricas que podem ajudá-lo a estimar a largura de banda de rede por usuário.</span><span class="sxs-lookup"><span data-stu-id="037f1-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="037f1-107">Se você tiver uma combinação desses cenários, não recomendamos nada menor que (ou igual a) 10 MB/s como Olá largura de banda mínima para aplicativos modernos conectados à Internet, em um ambiente remoto.</span><span class="sxs-lookup"><span data-stu-id="037f1-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="037f1-108">(Embora, conforme discutido, isso não assegure uma experiência de usuário acima da média.)</span><span class="sxs-lookup"><span data-stu-id="037f1-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="037f1-109">PowerPoint complexo, PowerPoint simples</span><span class="sxs-lookup"><span data-stu-id="037f1-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="037f1-110">O Azure RemoteApp funciona melhor em LAN de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="037f1-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="037f1-111">Em Olá 10 MB/perfil de rede % s, quando mais de 5% usuário Olá tremulação acima 120 ms verá uma experiência média.</span><span class="sxs-lookup"><span data-stu-id="037f1-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="037f1-112">No hello de 1 MB/s diferentes é evidente - por exemplo, em uma apresentação de slides, usuário Olá talvez não veja transições animadas em todos os porque quadros são ignorados.</span><span class="sxs-lookup"><span data-stu-id="037f1-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="037f1-113">Internet Explorer, PDF misto, PDF, Texto</span><span class="sxs-lookup"><span data-stu-id="037f1-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="037f1-114">Perfil de 10 MB/s de rede é fechar tooLAN na maioria dos aspectos.</span><span class="sxs-lookup"><span data-stu-id="037f1-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="037f1-115">1 MB/s fornecem uma experiência de Okey, embora possa haver algumas tremulação quando um usuário rola enquanto há imagens na tela hello.</span><span class="sxs-lookup"><span data-stu-id="037f1-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="037f1-116">Vídeo em Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="037f1-116">Flash video (YouTube)</span></span>
<span data-ttu-id="037f1-117">100 MB/s LAN fornece melhor experiência de hello, enquanto 10 MB/s é aceitável (que significa acompanhar a taxa de quadros hello, mas tremulação aumenta).</span><span class="sxs-lookup"><span data-stu-id="037f1-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="037f1-118">A 1 MB/s, a tremulação é muito alta e perceptível.</span><span class="sxs-lookup"><span data-stu-id="037f1-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="037f1-119">Digitação de palavras (entrada remota do Word)</span><span class="sxs-lookup"><span data-stu-id="037f1-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="037f1-120">Esse é um cenário de uso de baixa largura de banda.</span><span class="sxs-lookup"><span data-stu-id="037f1-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="037f1-121">A 256 KB/s fornecemos uma experiência tão boa quanto aquela obtida com LAN.</span><span class="sxs-lookup"><span data-stu-id="037f1-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="037f1-122">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="037f1-122">Learn more</span></span>
* [<span data-ttu-id="037f1-123">Estimar o uso de largura de banda de rede do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="037f1-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="037f1-124">Azure RemoteApp - como a largura de banda de rede e a qualidade da experiência funcionam juntas?</span><span class="sxs-lookup"><span data-stu-id="037f1-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="037f1-125">Azure RemoteApp - testando o uso da largura de banda de sua rede com alguns cenários comuns</span><span class="sxs-lookup"><span data-stu-id="037f1-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

