---
title: aaaSecure sua Internet das coisas (IoT) no Azure | Microsoft Docs
description: " Os serviços de IoT (Internet das Coisas) do Azure oferecem uma ampla variedade de funcionalidades. Este artigo ajuda você a entender como toosecure suas soluções IoT no Azure. "
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
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="a4145-104">Visão geral da segurança da Internet das Coisas</span><span class="sxs-lookup"><span data-stu-id="a4145-104">Internet of Things security overview</span></span>
<span data-ttu-id="a4145-105">Os serviços de IoT (Internet das Coisas) do Azure oferecem uma ampla variedade de funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="a4145-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="a4145-106">Esses serviços de nível corporativo permitem que você:</span><span class="sxs-lookup"><span data-stu-id="a4145-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="a4145-107">Colete dados de dispositivos</span><span class="sxs-lookup"><span data-stu-id="a4145-107">Collect data from devices</span></span>
* <span data-ttu-id="a4145-108">Analise fluxos de dados em movimento</span><span class="sxs-lookup"><span data-stu-id="a4145-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="a4145-109">Armazene e consulte grandes conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="a4145-109">Store and query large data sets</span></span>
* <span data-ttu-id="a4145-110">Visualize dados históricos e em tempo real</span><span class="sxs-lookup"><span data-stu-id="a4145-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="a4145-111">Realize a integração com sistemas de back-office</span><span class="sxs-lookup"><span data-stu-id="a4145-111">Integrate with back-office systems</span></span>

<span data-ttu-id="a4145-112">toodeliver esses recursos, o Azure IoT Suite pacotes juntos vários serviços do Azure com extensões personalizadas como soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="a4145-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="a4145-113">Essas soluções pré-configuradas são as implementações básicas dos padrões comuns de solução de IoT que ajudam a tooreduce Olá tempo você toodeliver suas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="a4145-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="a4145-114">Usando kits de desenvolvimento de software Olá IoT, você pode personalizar e estender essas soluções toomeet seus próprios requisitos.</span><span class="sxs-lookup"><span data-stu-id="a4145-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="a4145-115">Você também pode usar essas soluções como exemplos ou modelos no desenvolvimento de novas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="a4145-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="a4145-116">pacote do Azure IoT Olá é uma solução avançada para suas necessidades de IoT.</span><span class="sxs-lookup"><span data-stu-id="a4145-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="a4145-117">No entanto, é imprescindível que suas soluções IoT destinam-se com segurança em mente a partir do início da saudação.</span><span class="sxs-lookup"><span data-stu-id="a4145-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="a4145-118">Devido ao número absoluto de saudação de dispositivos IoT, qualquer incidente de segurança pode se tornar rapidamente um evento generalizado com consequências significativas.</span><span class="sxs-lookup"><span data-stu-id="a4145-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="a4145-119">toohelp você entender como toosecure suas soluções IoT, temos Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="a4145-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="a4145-120">Arquitetura de segurança</span><span class="sxs-lookup"><span data-stu-id="a4145-120">Security architecture</span></span>
<span data-ttu-id="a4145-121">Durante a criação de um sistema, é importante toounderstand ameaças em potencial Olá toothat sistema e adicionar defesas apropriadas da mesma forma, como sistema de saudação é desenvolvido e projetado.</span><span class="sxs-lookup"><span data-stu-id="a4145-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="a4145-122">É importante toodesign Olá produto a partir do início da saudação pensando na segurança porque a entender como um invasor pode ser capaz de toocompromise um sistema de ajuda a certificar-se de que as atenuações apropriadas estejam no local de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4145-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="a4145-123">Você pode aprender sobre a arquitetura de segurança da IoT lendo o artigo [Arquitetura de segurança da Internet das Coisas](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="a4145-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="a4145-124">Este artigo aborda Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="a4145-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="a4145-125">A segurança começa com um modelo de risco</span><span class="sxs-lookup"><span data-stu-id="a4145-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="a4145-126">Segurança na IoT</span><span class="sxs-lookup"><span data-stu-id="a4145-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="a4145-127">Saudação de modelagem de ameaça arquitetura de referência de IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="a4145-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="a4145-128">Segurança de saudação de plano de fundo para cima</span><span class="sxs-lookup"><span data-stu-id="a4145-128">Security from hello ground up</span></span>
<span data-ttu-id="a4145-129">Olá IoT representa exclusivo segurança, privacidade e conformidade desafios toobusinesses em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="a4145-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="a4145-130">Ao contrário da tecnologia tradicional cyber onde esses problemas giram em torno de software e como ele é implementado, IoT aborda o que acontece quando Olá cibernéticos e mundos físico Olá convergirem.</span><span class="sxs-lookup"><span data-stu-id="a4145-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="a4145-131">Proteger soluções IoT requer garantindo provisionamento seguro de dispositivos, a conectividade segura entre esses dispositivos e a nuvem hello e a proteção de dados seguros na nuvem Olá durante o processamento e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a4145-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="a4145-132">No entanto, trabalhando contra essa funcionalidade estão os dispositivos com recursos limitados, a distribuição geográfica das implantações e vários dispositivos em uma solução.</span><span class="sxs-lookup"><span data-stu-id="a4145-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="a4145-133">Você pode aprender como toohandle segurança nessas áreas lendo [segurança de Internet das coisas de saudação de plano de fundo](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="a4145-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="a4145-134">Olá artigo Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="a4145-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="a4145-135">Infraestrutura segura de saudação de plano de fundo para cima</span><span class="sxs-lookup"><span data-stu-id="a4145-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="a4145-136">Microsoft Azure - infraestrutura segura da IoT para os seus negócios</span><span class="sxs-lookup"><span data-stu-id="a4145-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="a4145-137">Práticas Recomendadas</span><span class="sxs-lookup"><span data-stu-id="a4145-137">Best Practices</span></span>
<span data-ttu-id="a4145-138">Proteger uma infraestrutura de IoT requer uma estratégia de segurança em camadas rigorosa.</span><span class="sxs-lookup"><span data-stu-id="a4145-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="a4145-139">Da proteção de dados na nuvem hello, proteger a integridade de dados em trânsito pela Olá internet pública, dispositivos de provisionamento de toosecurely, cada camada cria maior garantia de segurança de Olá infra-estrutura geral.</span><span class="sxs-lookup"><span data-stu-id="a4145-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="a4145-140">Você pode aprender sobre as práticas recomendadas de segurança da Internet das Coisas lendo o artigo [Práticas recomendadas de segurança de Internet das Coisas](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="a4145-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="a4145-141">Olá artigo Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="a4145-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="a4145-142">Fabricante/integrador de hardware de IoT</span><span class="sxs-lookup"><span data-stu-id="a4145-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="a4145-143">Desenvolvedor de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="a4145-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="a4145-144">Implantador de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="a4145-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="a4145-145">Operador de solução IoT</span><span class="sxs-lookup"><span data-stu-id="a4145-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
