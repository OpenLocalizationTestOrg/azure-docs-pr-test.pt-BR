---
title: "Saiba mais sobre a verificação em duas etapas no Azure MFA | Microsoft Docs"
description: "O que é a Autenticação Multifator do Azure (MFA, Multi-factor Authentication), por que usar MFA, mais informações sobre o cliente MFA e os diferentes métodos e versões disponíveis. "
keywords: "introdução ao MFA, visão do geral do mfa, o que é mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="e71dd-104">O que é o Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="e71dd-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="e71dd-105">A verificação em duas etapas é um método de autenticação que exige mais de um método de verificação e adiciona uma segunda camada crítica de segurança aos logons e às transações dos usuários.</span><span class="sxs-lookup"><span data-stu-id="e71dd-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="e71dd-106">Ela funciona, exigindo dois ou mais dos métodos de verificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="e71dd-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="e71dd-107">Algo que você sabe (normalmente, uma senha)</span><span class="sxs-lookup"><span data-stu-id="e71dd-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="e71dd-108">Algo que você tem (um dispositivo confiável que não pode ser facilmente clonado, como um telefone)</span><span class="sxs-lookup"><span data-stu-id="e71dd-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="e71dd-109">Algo seu (biometria)</span><span class="sxs-lookup"><span data-stu-id="e71dd-109">Something you are (biometrics)</span></span>

<span data-ttu-id="e71dd-110"><center>![Nome de usuário e senha](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Cartão inteligente](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Cartão inteligente virtual](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nome de usuário e senha](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="e71dd-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="e71dd-111">O Azure MFA é uma solução de verificação em duas etapas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e71dd-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="e71dd-112">O Azure MFA ajuda a proteger o acesso a dados e aplicativos, ao mesmo tempo que atende à demanda dos usuários por um processo de entrada simples.</span><span class="sxs-lookup"><span data-stu-id="e71dd-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="e71dd-113">Ele fornece autenticação forte por meio de uma variedade de métodos de verificação, incluindo chamada telefônica, mensagem de texto ou verificação de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="e71dd-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="e71dd-114">Por que usar o Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="e71dd-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="e71dd-115">Hoje, mais do que nunca, as pessoas estão cada vez mais conectadas.</span><span class="sxs-lookup"><span data-stu-id="e71dd-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="e71dd-116">Com os Smartphones, tablets, laptops e PCs, as pessoas têm várias opções diferentes para se conectar e se manterem conectadas.</span><span class="sxs-lookup"><span data-stu-id="e71dd-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="e71dd-117">As pessoas podem acessar suas contas e aplicativos de qualquer lugar, o que significa que elas podem concluir mais tarefas de trabalho e atender melhor os seus clientes.</span><span class="sxs-lookup"><span data-stu-id="e71dd-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="e71dd-118">O Azure Multi-Factor Authentication é uma solução fácil de usar, escalonável e confiável que fornece um segundo método de autenticação para que os usuários sempre estejam protegidos.</span><span class="sxs-lookup"><span data-stu-id="e71dd-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Fácil de usar](./media/multi-factor-authentication/simple.png) | ![Escalonável](./media/multi-factor-authentication/scalable.png) | ![Sempre protegidos](./media/multi-factor-authentication/protected.png) | ![Confiável](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="e71dd-123">**Fácil de usar**</span><span class="sxs-lookup"><span data-stu-id="e71dd-123">**Easy to use**</span></span> |<span data-ttu-id="e71dd-124">**Escalonável**</span><span class="sxs-lookup"><span data-stu-id="e71dd-124">**Scalable**</span></span> |<span data-ttu-id="e71dd-125">**Sempre protegidos**</span><span class="sxs-lookup"><span data-stu-id="e71dd-125">**Always Protected**</span></span> |<span data-ttu-id="e71dd-126">**Confiável**</span><span class="sxs-lookup"><span data-stu-id="e71dd-126">**Reliable**</span></span> |

* <span data-ttu-id="e71dd-127">**Fácil de usar** – a Autenticação Multifator do Azure é simples de configurar e usar.</span><span class="sxs-lookup"><span data-stu-id="e71dd-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="e71dd-128">A proteção extra que acompanha a Autenticação Multifator do Azure permite que os usuários gerenciem seus próprios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e71dd-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="e71dd-129">O melhor de tudo, em muitos casos ela pode ser configurada com apenas alguns cliques.</span><span class="sxs-lookup"><span data-stu-id="e71dd-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="e71dd-130">**Escalonável** – a Autenticação Multifator do Azure utiliza os recursos da nuvem e integra-se ao seu AD e a aplicativos personalizados locais.</span><span class="sxs-lookup"><span data-stu-id="e71dd-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="e71dd-131">Essa proteção ainda é estendida aos seus cenários essenciais de missão de alto volume.</span><span class="sxs-lookup"><span data-stu-id="e71dd-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="e71dd-132">**Sempre protegidos** - o Azure Multi-Factor Authentication fornece autenticação forte usando os mais altos padrões do setor.</span><span class="sxs-lookup"><span data-stu-id="e71dd-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="e71dd-133">**Confiável** - Garantimos 99,9% de disponibilidade do Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="e71dd-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="e71dd-134">O serviço é considerado indisponível quando não é possível receber ou processar solicitações de verificação para verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="e71dd-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="e71dd-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e71dd-135">Next steps</span></span>

- <span data-ttu-id="e71dd-136">Saiba mais sobre [Como funciona a Autenticação Multifator do Azure](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="e71dd-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="e71dd-137">Leia sobre os diferentes [métodos de consumo e versões para a Autenticação Multifator do Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="e71dd-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
