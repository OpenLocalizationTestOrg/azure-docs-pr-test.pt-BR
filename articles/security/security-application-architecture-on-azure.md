---
title: "segurança aaaIntegrate em seus projetos arquitetônicos do Azure | Microsoft Docs"
description: " Este artigo o ajudará a entender a arquitetura de aplicativos e serviços de saudação no Azure toomake-lo mais fácil segurança toointegrate no design e implementação. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="cb756-103">Arquitetura de aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="cb756-103">Application architecture on Azure</span></span>
<span data-ttu-id="cb756-104">toohelp proteger suas soluções baseadas em nuvem no Microsoft Azure, uma base sólida de arquitetura é crítica.</span><span class="sxs-lookup"><span data-stu-id="cb756-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="cb756-105">Arquitetos, designers e implementadores se beneficiam de um conhecimento sólido sobre a arquitetura de aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="cb756-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="cb756-106">Esse conhecimento básico ajuda você a entender todos os componentes de saudação do suas soluções baseadas em nuvem e torná-lo mais fácil de segurança toointegrate todos os aspectos do seu design e implementação.</span><span class="sxs-lookup"><span data-stu-id="cb756-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="cb756-107">Podemos ter Olá seguintes toohelp você com designs e sua arquitetura investigações:</span><span class="sxs-lookup"><span data-stu-id="cb756-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="cb756-108">Infográficos de arquitetura</span><span class="sxs-lookup"><span data-stu-id="cb756-108">Architectural infographics</span></span>
* <span data-ttu-id="cb756-109">Plantas de arquitetura</span><span class="sxs-lookup"><span data-stu-id="cb756-109">Architectural blueprints</span></span>
* <span data-ttu-id="cb756-110">Conjunto de símbolos de nuvem e empresariais</span><span class="sxs-lookup"><span data-stu-id="cb756-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="cb756-111">Modelo de planta 3D do Visio</span><span class="sxs-lookup"><span data-stu-id="cb756-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="cb756-112">Infográficos de arquitetura</span><span class="sxs-lookup"><span data-stu-id="cb756-112">Architectural infographics</span></span>
<span data-ttu-id="cb756-113">A Microsoft publica diversos infográficos/pôsteres relacionados à arquitetura.</span><span class="sxs-lookup"><span data-stu-id="cb756-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="cb756-114">Elas incluem:</span><span class="sxs-lookup"><span data-stu-id="cb756-114">They include:</span></span>

* [<span data-ttu-id="cb756-115">Compilação de aplicativos reais na nuvem</span><span class="sxs-lookup"><span data-stu-id="cb756-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="cb756-116">Escala com Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="cb756-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="cb756-117">Plantas de arquitetura</span><span class="sxs-lookup"><span data-stu-id="cb756-117">Architectural blueprints</span></span>
<span data-ttu-id="cb756-118">A Microsoft publica um conjunto de alto nível [plantas de arquitetura](http://aka.ms/azblueprints) mostrando como toobuild a tipos específicos de sistemas que usam os produtos da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb756-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="cb756-119">Cada planta inclui um:</span><span class="sxs-lookup"><span data-stu-id="cb756-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="cb756-120">Arquivo simples baseado em Visio 2003 2D que você pode baixar e modificar</span><span class="sxs-lookup"><span data-stu-id="cb756-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="cb756-121">Perspectiva 3D coloridos PDF arquivo toointroduce Olá planta tooless público técnico</span><span class="sxs-lookup"><span data-stu-id="cb756-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="cb756-122">Vídeo orienta na versão 3D Olá</span><span class="sxs-lookup"><span data-stu-id="cb756-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="cb756-123">Conjunto de símbolos de nuvem e empresariais</span><span class="sxs-lookup"><span data-stu-id="cb756-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="cb756-124">[Exibir hello Visio e símbolos de vídeo de treinamento](http://aka.ms/CnESymbolsVideo) e [baixar o conjunto de nuvem e Enterprise símbolo Olá](http://aka.ms/CnESymbols) toohelp criar material técnico que descrevem o Azure, Windows Server, SQL Server e muito mais.</span><span class="sxs-lookup"><span data-stu-id="cb756-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="cb756-125">Você pode usar os símbolos de saudação em diagramas de arquitetura, materiais de treinamento, apresentações, folhas de dados, infográficos, white papers e até mesmo os livros de terceiros se Olá catálogo treina pessoas toouse produtos da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb756-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="cb756-126">No entanto, eles não se destinam ao uso em interfaces do usuário.</span><span class="sxs-lookup"><span data-stu-id="cb756-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="cb756-127">Modelo de planta 3D do Visio</span><span class="sxs-lookup"><span data-stu-id="cb756-127">3D blueprint Visio template</span></span>
<span data-ttu-id="cb756-128">Olá 3D versões do hello [plantas de arquitetura do Microsoft](http://aka.ms/azblueprints) criados inicialmente em uma ferramenta de terceiros.</span><span class="sxs-lookup"><span data-stu-id="cb756-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="cb756-129">Um novo modelo do Visio 2013 (e posterior) foi enviado em 5 de agosto de 2015 como parte de um [Curso de certificação de arquitetura da Microsoft distribuído em EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="cb756-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="cb756-130">modelo de saudação também está disponível fora Olá curso.</span><span class="sxs-lookup"><span data-stu-id="cb756-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="cb756-131">[Exibir vídeo de treinamento Olá](http://aka.ms/3dBlueprintTemplateVideo) primeiro para que você saiba o que pode fazer</span><span class="sxs-lookup"><span data-stu-id="cb756-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="cb756-132">Baixar Olá [Microsoft modelo de Visio plano gráfico 3d](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="cb756-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="cb756-133">Baixar Olá [nuvem e Enterprise símbolos](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse com modelo 3D Olá</span><span class="sxs-lookup"><span data-stu-id="cb756-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
