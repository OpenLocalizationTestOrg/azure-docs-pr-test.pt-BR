---
title: "Linha de base de solução de Segurança e Auditoria do Operations Management Suite | Microsoft Docs"
description: "Este documento explica como usar a solução de Segurança e Auditoria do OMS para realizar uma avaliação de linha de base de Web de todos os servidores Web para fins de conformidade e segurança."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="36683-103">Avaliação de linha de base de Web na Solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="36683-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="36683-104">Este documento o ajuda a usar os recursos de avaliação da linha de base da Web da [Solução de Segurança e Auditoria do Operations Management Suite (OMS)](operations-management-suite-overview.md) para acessar o estado de segurança de seus recursos monitorados.</span><span class="sxs-lookup"><span data-stu-id="36683-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="36683-105">O que é a Avaliação de Linha de Base da Web?</span><span class="sxs-lookup"><span data-stu-id="36683-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="36683-106">Atualmente a Segurança do OMS oferece uma avaliação de linha de base para os sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="36683-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="36683-107">Ele examina as configurações de sistema operacional dos servidores a cada 24 horas e fornece uma exibição para configurações potencialmente vulneráveis.</span><span class="sxs-lookup"><span data-stu-id="36683-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="36683-108">Leia [Avaliação de Linha de Base na Solução de Segurança e Auditoria do Operations Management Suite](oms-security-baseline.md) para saber mais informações sobre esta opção.</span><span class="sxs-lookup"><span data-stu-id="36683-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="36683-109">O objetivo da avaliação de linha de base da Web é localizar as configurações de servidor Web vulneráveis.</span><span class="sxs-lookup"><span data-stu-id="36683-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="36683-110">As três fontes principais para as configurações de linha de base da Web são: configuração do .NET, ASP.NET e IIS.</span><span class="sxs-lookup"><span data-stu-id="36683-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="36683-111">Assim como a avaliação de linha de base do sistema operacional, a Segurança do OMS vai verificar os seus servidores Web a cada 24 horas e fornecer uma exibição do estado de segurança deles.</span><span class="sxs-lookup"><span data-stu-id="36683-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="36683-112">No Serviço de Informações da Internet (IIS), as configurações são altamente personalizáveis, o que permite que vários níveis de aplicativo e site sejam substituídos.</span><span class="sxs-lookup"><span data-stu-id="36683-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="36683-113">O scanner verifica as configurações em cada nível de site/aplicativo além do nível de raiz padrão.</span><span class="sxs-lookup"><span data-stu-id="36683-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="36683-114">Isso ajuda a identificar os locais das potenciais vulnerabilidades das configurações e corrigi-las rapidamente.</span><span class="sxs-lookup"><span data-stu-id="36683-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="36683-115">Avaliação de Linha de Base de Segurança da Web</span><span class="sxs-lookup"><span data-stu-id="36683-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="36683-116">Para essa visualização esse recurso está prestes a ser acessado usando a opção de Pesquisa do OMS.</span><span class="sxs-lookup"><span data-stu-id="36683-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="36683-117">Siga as etapas abaixo para executar a consulta adequada:</span><span class="sxs-lookup"><span data-stu-id="36683-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="36683-118">No painel principal do **Microsoft Operations Management Suite**, clique no bloco **Segurança e Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="36683-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="36683-119">No painel **Segurança e Auditoria**, clique no botão **Pesquisa de Log**.</span><span class="sxs-lookup"><span data-stu-id="36683-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="36683-120">A primeira consulta que você pode usar é o **Resumo da avaliação de linha de base da Web**.</span><span class="sxs-lookup"><span data-stu-id="36683-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="36683-121">No campo **Iniciar pesquisa aqui**, digite esta consulta: Type*=SecurityBaselineSummary BaselineType=web*.</span><span class="sxs-lookup"><span data-stu-id="36683-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="36683-122">A tela a seguir tem um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="36683-122">The following screen has an output sample:</span></span>

![Avaliação de linha de base da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="36683-124">Nesta consulta, cada registro indica o resumo da avaliação em um único servidor.</span><span class="sxs-lookup"><span data-stu-id="36683-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="36683-125">Quando você estiver na **Pesquisa de Log**, você pode digitar diferentes consultas para obter mais informações sobre a avaliação de linha de base da web.</span><span class="sxs-lookup"><span data-stu-id="36683-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="36683-126">Além da consulta anterior, você também pode usar as seguintes nesta exibição.</span><span class="sxs-lookup"><span data-stu-id="36683-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="36683-127">**Avaliação da regra de linha de base de Web**: Cada registro representa uma avaliação da regra de linha de base única Web em um único servidor.</span><span class="sxs-lookup"><span data-stu-id="36683-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="36683-128">Ele inclui todos os dados para a regra, local, o resultado esperado e o resultado real.</span><span class="sxs-lookup"><span data-stu-id="36683-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="36683-129">**Consulta**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="36683-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Avaliação de regra de linha de base da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="36683-131">**Mostrar todos os resultados para um servidor específico**: Esta consulta mostra como ver os resultados de um servidor específico.</span><span class="sxs-lookup"><span data-stu-id="36683-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="36683-132">**Consulta**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="36683-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Todos os resultados](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="36683-134">Você também pode usar esses registros/consultas para criar seus próprios painéis, relatórios ou alertas.</span><span class="sxs-lookup"><span data-stu-id="36683-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="36683-135">A tela a seguir tem um controle de interface do usuário de exemplo que você pode adicionar ao seu painel.</span><span class="sxs-lookup"><span data-stu-id="36683-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="36683-136">Você pode aprender como visualizar os seus dados usando o Designer de Exibição do OMS [aqui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="36683-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="36683-137">A tela a seguir é um exemplo de como o bloco parecerá após fazer essa personalização.</span><span class="sxs-lookup"><span data-stu-id="36683-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![Interface de usuário de exemplo](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="36683-139">Se você gostaria de saber as configurações que são verificadas para a avaliação de linha de base, você pode baixar [essa planilha do Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) que contém essas configurações.</span><span class="sxs-lookup"><span data-stu-id="36683-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="36683-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="36683-140">See also</span></span>
<span data-ttu-id="36683-141">Neste documento, você aprendeu sobre a avaliação de linha de base de Web da Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="36683-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="36683-142">Para saber mais sobre a Segurança do OMS, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="36683-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="36683-143">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="36683-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="36683-144">Monitorando e respondendo a alertas de segurança na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="36683-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="36683-145">Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="36683-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

