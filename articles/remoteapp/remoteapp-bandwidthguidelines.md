---
title: Largura de banda de rede do Azure RemoteApp - diretrizes gerais | Microsoft Docs
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
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="609d9-103">Largura de banda de rede do Azure RemoteApp - diretrizes gerais (se não puder testar a sua)</span><span class="sxs-lookup"><span data-stu-id="609d9-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="609d9-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="609d9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="609d9-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="609d9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="609d9-106">Caso você não tenha tempo nem capacidade de executar os [testes de largura de banda de rede](remoteapp-bandwidthtests.md) para o Azure RemoteApp, aqui estão algumas diretrizes bastante genéricas que poderão ajudá-lo a estimar a largura de banda de rede por usuário.</span><span class="sxs-lookup"><span data-stu-id="609d9-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="609d9-107">Caso você tenha uma combinação desses cenários, nós não recomendamos nada menor que (ou igual a) 10 MB/s, como a largura de banda de rede MÍNIMA para aplicativos modernos conectados à Internet em um ambiente remoto.</span><span class="sxs-lookup"><span data-stu-id="609d9-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="609d9-108">(Embora, conforme discutido, isso não assegure uma experiência de usuário acima da média.)</span><span class="sxs-lookup"><span data-stu-id="609d9-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="609d9-109">PowerPoint complexo, PowerPoint simples</span><span class="sxs-lookup"><span data-stu-id="609d9-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="609d9-110">O Azure RemoteApp funciona melhor em LAN de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="609d9-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="609d9-111">No perfil de rede 10 MB/s, quando a tremulação acima de 120 ms é superior a 5%, o usuário verá uma experiência média.</span><span class="sxs-lookup"><span data-stu-id="609d9-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="609d9-112">A 1 MB/s, a diferença é evidente - por exemplo, em uma apresentação de slides, o usuário talvez não veja transição animada nenhuma porque os quadros são ignorados.</span><span class="sxs-lookup"><span data-stu-id="609d9-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="609d9-113">Internet Explorer, PDF misto, PDF, Texto</span><span class="sxs-lookup"><span data-stu-id="609d9-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="609d9-114">O perfil de rede de 10 MB/s se aproxima de LAN na maioria dos aspectos.</span><span class="sxs-lookup"><span data-stu-id="609d9-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="609d9-115">1 MB/s fornecerá uma experiência OK, embora possa haver alguma tremulação quando o usuário rola enquanto há imagens na tela.</span><span class="sxs-lookup"><span data-stu-id="609d9-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="609d9-116">Vídeo em Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="609d9-116">Flash video (YouTube)</span></span>
<span data-ttu-id="609d9-117">LAN de 100 MB/s fornece a melhor experiência, enquanto 10 MB/s é aceitável (que significa acompanhar a taxa de quadros, mas com aumento da tremulação).</span><span class="sxs-lookup"><span data-stu-id="609d9-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="609d9-118">A 1 MB/s, a tremulação é muito alta e perceptível.</span><span class="sxs-lookup"><span data-stu-id="609d9-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="609d9-119">Digitação de palavras (entrada remota do Word)</span><span class="sxs-lookup"><span data-stu-id="609d9-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="609d9-120">Esse é um cenário de uso de baixa largura de banda.</span><span class="sxs-lookup"><span data-stu-id="609d9-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="609d9-121">A 256 KB/s fornecemos uma experiência tão boa quanto aquela obtida com LAN.</span><span class="sxs-lookup"><span data-stu-id="609d9-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="609d9-122">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="609d9-122">Learn more</span></span>
* [<span data-ttu-id="609d9-123">Estimar o uso de largura de banda de rede do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="609d9-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="609d9-124">Azure RemoteApp - como a largura de banda de rede e a qualidade da experiência funcionam juntas?</span><span class="sxs-lookup"><span data-stu-id="609d9-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="609d9-125">Azure RemoteApp - testando o uso da largura de banda de sua rede com alguns cenários comuns</span><span class="sxs-lookup"><span data-stu-id="609d9-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

