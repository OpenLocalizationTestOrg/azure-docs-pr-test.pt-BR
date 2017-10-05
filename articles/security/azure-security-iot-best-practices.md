---
title: "Práticas recomendadas de segurança de Internet das Coisas | Microsoft Docs"
description: "O artigo fornece uma lista selecionada de práticas recomendadas e recomendações gerais do Internet das Coisas da Microsoft."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 8efc0053458e338ac1afe98d9ce970c1d5cbfa81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="a9f0f-103">Práticas recomendadas de segurança de Internet das Coisas</span><span class="sxs-lookup"><span data-stu-id="a9f0f-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="a9f0f-104">Proteger a infraestrutura de IoT (Internet das Coisas) é uma tarefa crítica para qualquer pessoa envolvida com soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-104">Securing the Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="a9f0f-105">Por causa do número de dispositivos envolvidos e da natureza distribuída desses dispositivos, o impacto de um evento de segurança relacionado ao comprometimento de milhões de dispositivos IoT não é trivial, e pode ter impacto generalizado.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-105">Because of the number of devices involved and the distributed nature of these devices, the impact a security event related to compromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="a9f0f-106">Por esse motivo, a segurança do IoT precisa de uma abordagem de segurança detalhada.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="a9f0f-107">Os dados devem ser protegidos na nuvem e conforme eles se movem por redes públicas e privadas.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-107">Data needs to be secure in the cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="a9f0f-108">É preciso que métodos estejam em vigor para provisionar, com segurança, os dispositivos IoT em si.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-108">Methods need to be in place to securely provision the IoT devices themselves.</span></span> <span data-ttu-id="a9f0f-109">Cada camada, desde dispositivo, passando pela rede, até o back-end de nuvem, precisa de garantias fortes de segurança.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-109">Each layer, from device, to network, to cloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="a9f0f-110">As práticas recomendadas de IoT podem ser categorizadas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a9f0f-110">IoT best practices can be categorized in the following way:</span></span>

* <span data-ttu-id="a9f0f-111">Fabricante ou integrador de hardware de IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="a9f0f-112">Desenvolvedor de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-112">IoT solution developer</span></span>
* <span data-ttu-id="a9f0f-113">Implantador de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-113">IoT solution deployer</span></span>
* <span data-ttu-id="a9f0f-114">Operador de solução IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-114">IoT solution operator</span></span>

<span data-ttu-id="a9f0f-115">Este artigo resume as [Práticas recomendadas de segurança de Internet das Coisas](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="a9f0f-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="a9f0f-116">Consulte esse artigo para obter informações mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-116">Please refer to that article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="a9f0f-117">Fabricante ou integrador de hardware de IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="a9f0f-118">Siga as práticas recomendadas a seguir se você for um fabricante ou integrador de hardware de IoT:</span><span class="sxs-lookup"><span data-stu-id="a9f0f-118">Follow the best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="a9f0f-119">**Escopo de hardware para requisitos mínimos**: o design de hardware deve incluir o mínimo de recursos necessários para a operação de hardware e nada mais.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-119">**Scope hardware to minimum requirements**: the hardware design should include minimum features required for operation of the hardware, and nothing more.</span></span> 
* <span data-ttu-id="a9f0f-120">**Tornar o hardware à prova de adulteração**: crie mecanismos para detectar a violação física do hardware, tal como a abertura da tampa do dispositivo, remoção de parte do dispositivo, etc.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-120">**Make hardware tamper proof**: build in mechanisms to detect physical tampering of hardware, such as opening the device cover, removing a part of the device, etc.</span></span> 
* <span data-ttu-id="a9f0f-121">**Criar em hardware seguro**: se o [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permitir, crie recursos de segurança, como as funcionalidades de inicialização baseadas no armazenamento seguro e criptografado e no TPM (Trusted Platform Module).</span><span class="sxs-lookup"><span data-stu-id="a9f0f-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="a9f0f-122">**Tornar as atualizações seguras**: atualizar o firmware durante o tempo de vida do dispositivo é inevitável.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-122">**Make upgrades secure**: upgrading firmware during lifetime of the device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="a9f0f-123">Desenvolvedor de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-123">IoT solution developer</span></span>
<span data-ttu-id="a9f0f-124">Siga as práticas recomendadas a seguir se você for um desenvolvedor de solução IoT:</span><span class="sxs-lookup"><span data-stu-id="a9f0f-124">Follow the best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="a9f0f-125">**Seguir a metodologia de desenvolvimento de software seguro**: desenvolver software seguro requer uma consideração inicial desde a concepção do projeto até sua implementação, teste e implantação.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from the inception of the project all the way to its implementation, testing, and deployment.</span></span>
* <span data-ttu-id="a9f0f-126">**Escolher software livre com cuidado**: software livre fornece uma oportunidade o rápido desenvolvimento de soluções.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-126">**Choose open source software with care**: open source software provides an opportunity to quickly develop solutions.</span></span>
* <span data-ttu-id="a9f0f-127">**Integrar com cuidado**: há muitas das falhas de segurança de software no limite de bibliotecas e APIs.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-127">**Integrate with care**: many of the software security flaws exist at the boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="a9f0f-128">Implantador de soluções IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-128">IoT solution deployer</span></span>
<span data-ttu-id="a9f0f-129">Siga as práticas recomendadas a seguir se você for um implantador de solução IoT:</span><span class="sxs-lookup"><span data-stu-id="a9f0f-129">Follow the best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="a9f0f-130">**Implantar o hardware com segurança**: implantações de IoT podem exigir que o hardware seja implantado em locais não seguros, como espaços públicos ou localidades sem supervisão.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-130">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="a9f0f-131">**Manter as chaves de autenticação em segurança**: durante a implantação, cada dispositivo requer IDs de dispositivo e chaves de autenticação associadas geradas pelo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span></span> <span data-ttu-id="a9f0f-132">Mantenha essas chaves fisicamente seguras mesmo após a implantação.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-132">Keep these keys physically safe even after the deployment.</span></span> <span data-ttu-id="a9f0f-133">Qualquer chave comprometida pode ser usada por um dispositivo mal-intencionado passando-se por um dispositivo existente.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-133">Any compromised key can be used by a malicious device to masquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="a9f0f-134">Operador de solução IoT</span><span class="sxs-lookup"><span data-stu-id="a9f0f-134">IoT solution operator</span></span>
<span data-ttu-id="a9f0f-135">Siga as práticas recomendadas a seguir se você for um operador de solução IoT:</span><span class="sxs-lookup"><span data-stu-id="a9f0f-135">Follow the best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="a9f0f-136">**Manter sistemas atualizados**: verifique se todos os sistemas operacionais e drivers do dispositivo estão atualizados para as versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-136">**Keep systems up to date**: ensure device operating systems and all device drivers are updated to the latest versions.</span></span> 
* <span data-ttu-id="a9f0f-137">**Proteger contra atividades mal-intencionadas**: se o sistema operacional permitir, aplique as funcionalidades antivírus e antimalware mais recentes em cada sistema operacional do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-137">**Protect against malicious activity**: if the operating system permits, place the latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="a9f0f-138">**Auditar frequentemente**: auditar problemas relacionados à infraestrutura de IoT é essencial ao responder a incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding to security incidents.</span></span>
* <span data-ttu-id="a9f0f-139">**Proteger fisicamente a infraestrutura de IoT**: os pior ataques de segurança contra infraestrutura de são iniciados usando o acesso físico aos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-139">**Physically protect the IoT infrastructure**: the worst security attacks against IoT infrastructure are launched using physical access to devices.</span></span>
* <span data-ttu-id="a9f0f-140">**Proteger credenciais da nuvem**: credenciais de autenticação da nuvem usadas para configurar e operar uma implantação de IoT são possivelmente a maneira mais fácil para acessar e comprometer um sistema de IoT.</span><span class="sxs-lookup"><span data-stu-id="a9f0f-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span></span> 

