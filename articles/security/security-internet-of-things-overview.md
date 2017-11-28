---
title: Proteger a Internet das Coisas (IoT) no Azure | Microsoft Docs
description: " Os serviços de IoT (Internet das Coisas) do Azure oferecem uma ampla variedade de funcionalidades. Este artigo ajuda você a entender como proteger suas soluções de IoT no Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="adab2-104">Visão geral da segurança da Internet das Coisas</span><span class="sxs-lookup"><span data-stu-id="adab2-104">Internet of Things security overview</span></span>
<span data-ttu-id="adab2-105">Os serviços de IoT (Internet das Coisas) do Azure oferecem uma ampla variedade de funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="adab2-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="adab2-106">Esses serviços de nível corporativo permitem que você:</span><span class="sxs-lookup"><span data-stu-id="adab2-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="adab2-107">Colete dados de dispositivos</span><span class="sxs-lookup"><span data-stu-id="adab2-107">Collect data from devices</span></span>
* <span data-ttu-id="adab2-108">Analise fluxos de dados em movimento</span><span class="sxs-lookup"><span data-stu-id="adab2-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="adab2-109">Armazene e consulte grandes conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="adab2-109">Store and query large data sets</span></span>
* <span data-ttu-id="adab2-110">Visualize dados históricos e em tempo real</span><span class="sxs-lookup"><span data-stu-id="adab2-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="adab2-111">Realize a integração com sistemas de back-office</span><span class="sxs-lookup"><span data-stu-id="adab2-111">Integrate with back-office systems</span></span>

<span data-ttu-id="adab2-112">Para fornecer essas funcionalidades, o Azure IoT Suite reúne diversos serviços do Azure com extensões personalizadas como soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="adab2-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="adab2-113">Essas soluções pré-configuradas são implementações básicas dos padrões comuns de solução de IoT que ajudam a reduzir o tempo necessário para entregar suas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="adab2-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="adab2-114">Usando os kits de desenvolvimento de software de IoT, você pode personalizar e estender essas soluções para atender aos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="adab2-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="adab2-115">Você também pode usar essas soluções como exemplos ou modelos no desenvolvimento de novas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="adab2-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="adab2-116">O Azure IoT Suite é uma solução poderosa para suas necessidades de IoT.</span><span class="sxs-lookup"><span data-stu-id="adab2-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="adab2-117">No entanto, é de máxima importância que suas soluções de IoT sejam criadas com a segurança em mente desde o início.</span><span class="sxs-lookup"><span data-stu-id="adab2-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="adab2-118">Devido ao grande número de dispositivos IoT, qualquer incidente de segurança pode se tornar rapidamente um evento difundido com consequências significativas.</span><span class="sxs-lookup"><span data-stu-id="adab2-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="adab2-119">Para ajudá-lo a entender como proteger suas soluções de IoT, temos as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="adab2-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="adab2-120">Arquitetura de segurança</span><span class="sxs-lookup"><span data-stu-id="adab2-120">Security architecture</span></span>
<span data-ttu-id="adab2-121">Durante a criação de um sistema, é importante compreender as ameaças potenciais para esse sistema e adicionar as defesas apropriadas da mesma forma, conforme o sistema é projetado e desenvolvido.</span><span class="sxs-lookup"><span data-stu-id="adab2-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="adab2-122">É importante projetar o produto desde o início com a segurança em mente porque a compreensão de como um invasor pode conseguir comprometer um sistema ajuda a garantir que as mitigações adequadas estão em vigor desde o início.</span><span class="sxs-lookup"><span data-stu-id="adab2-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="adab2-123">Você pode aprender sobre a arquitetura de segurança da IoT lendo o artigo [Arquitetura de segurança da Internet das Coisas](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="adab2-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="adab2-124">Este artigo discute os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="adab2-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="adab2-125">A segurança começa com um modelo de risco</span><span class="sxs-lookup"><span data-stu-id="adab2-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="adab2-126">Segurança na IoT</span><span class="sxs-lookup"><span data-stu-id="adab2-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="adab2-127">Fazendo a modelagem de risco da arquitetura de referência de IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="adab2-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="adab2-128">Segurança desde o início</span><span class="sxs-lookup"><span data-stu-id="adab2-128">Security from the ground up</span></span>
<span data-ttu-id="adab2-129">A IoT apresenta desafios específicos de segurança, privacidade e conformidade para empresas em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="adab2-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="adab2-130">Ao contrário da tecnologia cibernética tradicional, na qual esses problemas giram em torno do software e de como ele é implementado, a IoT se preocupa com o que acontece quando os mundos físico e cibernético convergem.</span><span class="sxs-lookup"><span data-stu-id="adab2-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="adab2-131">Proteger as soluções da IoT exige a garantia de provisionamento seguro dos dispositivos, a conectividade segura entre eles e a nuvem e a proteção garantida dos dados na nuvem durante o processamento e o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="adab2-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="adab2-132">No entanto, trabalhando contra essa funcionalidade estão os dispositivos com recursos limitados, a distribuição geográfica das implantações e vários dispositivos em uma solução.</span><span class="sxs-lookup"><span data-stu-id="adab2-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="adab2-133">Você pode aprender como lidar com a segurança nessas áreas lendo o artigo [Protegendo sua Internet das Coisas desde o princípio](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="adab2-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="adab2-134">O artigo discute os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="adab2-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="adab2-135">Infraestrutura segura desde o princípio</span><span class="sxs-lookup"><span data-stu-id="adab2-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="adab2-136">Microsoft Azure - infraestrutura segura da IoT para os seus negócios</span><span class="sxs-lookup"><span data-stu-id="adab2-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="adab2-137">Práticas Recomendadas</span><span class="sxs-lookup"><span data-stu-id="adab2-137">Best Practices</span></span>
<span data-ttu-id="adab2-138">Proteger uma infraestrutura de IoT requer uma estratégia de segurança em camadas rigorosa.</span><span class="sxs-lookup"><span data-stu-id="adab2-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="adab2-139">Desde proteger os dados na nuvem até proteger a integridade dos dados em trânsito na Internet pública até provisionar dispositivos com segurança, cada camada agrega maior garantia de segurança à infraestrutura total.</span><span class="sxs-lookup"><span data-stu-id="adab2-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="adab2-140">Você pode aprender sobre as práticas recomendadas de segurança da Internet das Coisas lendo o artigo [Práticas recomendadas de segurança de Internet das Coisas](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="adab2-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="adab2-141">O artigo discute os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="adab2-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="adab2-142">Fabricante/integrador de hardware de IoT</span><span class="sxs-lookup"><span data-stu-id="adab2-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="adab2-143">Desenvolvedor de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="adab2-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="adab2-144">Implantador de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="adab2-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="adab2-145">Operador de solução IoT</span><span class="sxs-lookup"><span data-stu-id="adab2-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
