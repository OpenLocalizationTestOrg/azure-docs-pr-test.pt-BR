---
title: "Padrões e práticas recomendadas de segurança do Azure | Microsoft Docs"
description: "O artigo fornece uma introdução sobre padrões e práticas recomendadas de segurança do Azure e uma lista selecionada de práticas recomendadas de segurança para diferentes recursos do Azure."
services: azure-security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1cbbf8dc-ea94-4a7e-8fa0-c2cb198956c5
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: terrylan
ms.openlocfilehash: 1cc0d2d1e9a62ff8531f963413ff573713d508ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="13241-103">Padrões e práticas recomendadas de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="13241-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="13241-104">No momento, temos os artigos de padrões e práticas recomendadas de segurança do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="13241-104">We currently have the following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="13241-105">Não deixe de visitar este site periodicamente para ver as atualizações para nossa lista crescente de padrões e práticas recomendadas de segurança do Azure:</span><span class="sxs-lookup"><span data-stu-id="13241-105">Make sure to visit this site periodically to see updates to our growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="13241-106">Práticas recomendadas de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="13241-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="13241-107">Práticas recomendadas de segurança de dados e criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="13241-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="13241-108">Práticas recomendadas de gerenciamento de identidade e segurança de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="13241-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="13241-109">Práticas recomendadas de segurança de Internet das Coisas</span><span class="sxs-lookup"><span data-stu-id="13241-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="13241-110">[Práticas recomendadas de segurança do IaaS do Azure] (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="13241-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="13241-111">Práticas recomendadas de segurança de limites do Azure</span><span class="sxs-lookup"><span data-stu-id="13241-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="13241-112">Implementar uma arquitetura de rede híbrida segura no Azure</span><span class="sxs-lookup"><span data-stu-id="13241-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="13241-113">[Melhores Práticas de PaaS do Azure] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="13241-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="13241-114">O Azure fornece uma plataforma segura na qual você pode criar suas soluções.</span><span class="sxs-lookup"><span data-stu-id="13241-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="13241-115">Também fornecemos serviços e tecnologias para tornar as suas soluções no Azure mais seguras.</span><span class="sxs-lookup"><span data-stu-id="13241-115">We also provide services and technologies to make your solutions on Azure more secure.</span></span> <span data-ttu-id="13241-116">Devido às muitas opções disponíveis, muitos de vocês expressaram interesse no que a Microsoft aconselha como práticas recomendadas e padrões para aprimorar a segurança.</span><span class="sxs-lookup"><span data-stu-id="13241-116">Because of the many options available to you, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="13241-117">Compreendemos seu interesse e criamos uma coleção de documentos que descrevem o que você pode fazer, levando em conta o contexto certo, para melhorar a segurança de implantações do Azure.</span><span class="sxs-lookup"><span data-stu-id="13241-117">We understand your interest and have created a collection of documents that describe things you can do, given the right context, to improve the security of Azure deployments.</span></span>

<span data-ttu-id="13241-118">Nesses artigos sobre práticas recomendadas e padrões, discutimos uma coleção de práticas recomendadas e padrões úteis para tópicos específicos.</span><span class="sxs-lookup"><span data-stu-id="13241-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="13241-119">Essas práticas recomendadas e padrões derivam das nossas experiências com essas tecnologias e da experiência de clientes como você.</span><span class="sxs-lookup"><span data-stu-id="13241-119">These best practices and patterns are derived from our experiences with these technologies and the experiences of customers like yourself.</span></span>

<span data-ttu-id="13241-120">Para cada prática recomendada, buscamos explicar:</span><span class="sxs-lookup"><span data-stu-id="13241-120">For each best practice we strive to explain:</span></span>

* <span data-ttu-id="13241-121">O que é a prática recomendada</span><span class="sxs-lookup"><span data-stu-id="13241-121">What the best practice is</span></span>
* <span data-ttu-id="13241-122">Por que é ideal habilitar essa prática recomendada</span><span class="sxs-lookup"><span data-stu-id="13241-122">Why you want to enable that best practice</span></span>
* <span data-ttu-id="13241-123">O que poderá acontecer se você não habilitar a prática recomendada</span><span class="sxs-lookup"><span data-stu-id="13241-123">What might be the result if you fail to enable the best practice</span></span>
* <span data-ttu-id="13241-124">Possíveis alternativas à prática recomendada</span><span class="sxs-lookup"><span data-stu-id="13241-124">Possible alternatives to the best practice</span></span>
* <span data-ttu-id="13241-125">Como você pode aprender a habilitar a prática recomendada</span><span class="sxs-lookup"><span data-stu-id="13241-125">How you can learn to enable the best practice</span></span>

<span data-ttu-id="13241-126">Estamos ansiosos para incluir muito mais artigos sobre arquitetura de segurança do Azure e práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="13241-126">We look forward to including many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="13241-127">Se houver tópicos que você deseja que incluamos, avise-nos na área de discussão na parte inferior desta página.</span><span class="sxs-lookup"><span data-stu-id="13241-127">If there are topics that you'd like us to include, let us know in the discussion area at the bottom of this page.</span></span>
