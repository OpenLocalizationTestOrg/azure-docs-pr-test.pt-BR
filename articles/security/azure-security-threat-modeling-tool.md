---
title: "aaaMicrosoft ferramenta de modelagem de ameaças - Azure | Microsoft Docs"
description: "página principal de saudação Microsoft Threat modelagem ferramenta, que contém informações sobre como iniciar a ferramenta hello, incluindo o processo de modelagem de ameaça Olá"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="18ad8-103">Ferramenta de modelagem de ameaças do Microsoft</span><span class="sxs-lookup"><span data-stu-id="18ad8-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="18ad8-104">Olá, ferramenta de modelagem de ameaça é um elemento de núcleo do hello Microsoft Security Development Lifecycle (SDL).</span><span class="sxs-lookup"><span data-stu-id="18ad8-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="18ad8-105">Ele permite que o software arquitetos tooidentify e atenuar problemas potenciais de segurança no início, quando eles são tooresolve relativamente fácil e econômica.</span><span class="sxs-lookup"><span data-stu-id="18ad8-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="18ad8-106">Como resultado, ele reduz significativamente o custo total de desenvolvimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="18ad8-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="18ad8-107">Além disso, projetamos ferramenta Olá com especialistas de segurança não em mente, facilitando a modelagem de ameaças para todos os desenvolvedores, fornecendo uma orientação clara sobre como criar e analisar os modelos de risco.</span><span class="sxs-lookup"><span data-stu-id="18ad8-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="18ad8-108">ferramenta de saudação permite que qualquer pessoa:</span><span class="sxs-lookup"><span data-stu-id="18ad8-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="18ad8-109">Se comunicar sobre design de segurança de saudação de seus sistemas</span><span class="sxs-lookup"><span data-stu-id="18ad8-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="18ad8-110">Analisar esses designs para problemas potenciais de segurança usando uma metodologia comprovada</span><span class="sxs-lookup"><span data-stu-id="18ad8-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="18ad8-111">Sugerir e gerenciar atenuações para problemas de segurança</span><span class="sxs-lookup"><span data-stu-id="18ad8-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="18ad8-112">Aqui estão alguns recursos de ferramentas e inovações, tooname apenas algumas:</span><span class="sxs-lookup"><span data-stu-id="18ad8-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="18ad8-113">**Automação:** orientação e comentários em um modelo de desenho</span><span class="sxs-lookup"><span data-stu-id="18ad8-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="18ad8-114">**STRIDE por elemento:** interativa de análise de ameaças e atenuações</span><span class="sxs-lookup"><span data-stu-id="18ad8-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="18ad8-115">**Emissão de relatórios:** atividades de segurança e testes em fase de verificação Olá</span><span class="sxs-lookup"><span data-stu-id="18ad8-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="18ad8-116">**Metodologia exclusiva:** permite que os usuários toobetter visualizar e compreender as ameaças</span><span class="sxs-lookup"><span data-stu-id="18ad8-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="18ad8-117">**Projetado para desenvolvedores e centralizado no Software:** muitas abordagens são centralizadas em ativos ou invasores.</span><span class="sxs-lookup"><span data-stu-id="18ad8-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="18ad8-118">Nós são centralizados em software.</span><span class="sxs-lookup"><span data-stu-id="18ad8-118">We are centered on software.</span></span> <span data-ttu-id="18ad8-119">Criamos em atividades que todos os arquitetos e desenvolvedores de software estão familiarizados com-- como o desenho de imagens para sua arquitetura de software</span><span class="sxs-lookup"><span data-stu-id="18ad8-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="18ad8-120">**Se concentra na análise de Design:** Olá termo "modelagem de ameaças" pode referir-se tooeither um requisitos ou uma técnica de análise de design.</span><span class="sxs-lookup"><span data-stu-id="18ad8-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="18ad8-121">Às vezes, ele se refere mistura complexa de tooa de Olá dois.</span><span class="sxs-lookup"><span data-stu-id="18ad8-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="18ad8-122">modelagem de toothreat Olá Microsoft SDL abordagem é uma técnica de análise de design focada</span><span class="sxs-lookup"><span data-stu-id="18ad8-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="18ad8-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="18ad8-123">Next steps</span></span>

<span data-ttu-id="18ad8-124">tabela de saudação abaixo contém links importantes tooget iniciado com a ferramenta de modelagem de ameaça de saudação:</span><span class="sxs-lookup"><span data-stu-id="18ad8-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="18ad8-125">Etapa</span><span class="sxs-lookup"><span data-stu-id="18ad8-125">Step</span></span>  | <span data-ttu-id="18ad8-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="18ad8-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="18ad8-127">**1**</span><span class="sxs-lookup"><span data-stu-id="18ad8-127">**1**</span></span> | [<span data-ttu-id="18ad8-128">Baixar a ferramenta de modelagem de ameaça de saudação</span><span class="sxs-lookup"><span data-stu-id="18ad8-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="18ad8-129">**2**</span><span class="sxs-lookup"><span data-stu-id="18ad8-129">**2**</span></span> | [<span data-ttu-id="18ad8-130">Leia nosso guia de introdução</span><span class="sxs-lookup"><span data-stu-id="18ad8-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="18ad8-131">**3**</span><span class="sxs-lookup"><span data-stu-id="18ad8-131">**3**</span></span> | [<span data-ttu-id="18ad8-132">Familiarize-se com os recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="18ad8-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="18ad8-133">**4**</span><span class="sxs-lookup"><span data-stu-id="18ad8-133">**4**</span></span> | [<span data-ttu-id="18ad8-134">Saiba mais sobre categorias de ameaça gerada</span><span class="sxs-lookup"><span data-stu-id="18ad8-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="18ad8-135">**5**</span><span class="sxs-lookup"><span data-stu-id="18ad8-135">**5**</span></span> | [<span data-ttu-id="18ad8-136">Localizar atenuações toogenerated ameaças</span><span class="sxs-lookup"><span data-stu-id="18ad8-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="18ad8-137">Recursos</span><span class="sxs-lookup"><span data-stu-id="18ad8-137">Resources</span></span>

<span data-ttu-id="18ad8-138">Aqui estão alguns antigos artigos toothreat ainda relevante de modelagem hoje:</span><span class="sxs-lookup"><span data-stu-id="18ad8-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="18ad8-139">Olá importância da modelagem de ameaça de artigo</span><span class="sxs-lookup"><span data-stu-id="18ad8-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="18ad8-140">Treinamento publicado pela Trustworthy Computing</span><span class="sxs-lookup"><span data-stu-id="18ad8-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="18ad8-141">Confira o que alguns especialistas em Ferramenta de modelagem de ameaças têm feito:</span><span class="sxs-lookup"><span data-stu-id="18ad8-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="18ad8-142">Gerenciador de ameaças</span><span class="sxs-lookup"><span data-stu-id="18ad8-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="18ad8-143">Blog de segurança Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="18ad8-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)