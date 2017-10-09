---
title: "aaaOperations linha de base de Web de solução de auditoria e de segurança do pacote de gerenciamento | Microsoft Docs"
description: "Este documento explica como toouse solução de segurança da OMS e auditoria tooperform uma avaliação de linha de base da web de todos os servidores da web monitorados para fins de conformidade e segurança."
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
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="ebf9a-103">Avaliação de linha de base de Web na Solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="ebf9a-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="ebf9a-104">Este documento ajuda toouse [Operations Management Suite (OMS) solução de segurança e auditoria](operations-management-suite-overview.md) web tooaccess recursos Olá estado seguro de seus recursos monitorados de avaliação de linha de base.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="ebf9a-105">O que é a Avaliação de Linha de Base da Web?</span><span class="sxs-lookup"><span data-stu-id="ebf9a-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="ebf9a-106">Atualmente a Segurança do OMS oferece uma avaliação de linha de base para os sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="ebf9a-107">Ele examina as configurações de sistema operacional Olá dos servidores a cada 24 horas e fornece um modo de exibição para configurações potencialmente vulneráveis.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="ebf9a-108">Leia [Avaliação de Linha de Base na Solução de Segurança e Auditoria do Operations Management Suite](oms-security-baseline.md) para saber mais informações sobre esta opção.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="ebf9a-109">meta de saudação da avaliação de linha de base de web hello é configurações do servidor web vulnerável toofind.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="ebf9a-110">Olá três fontes principais para as configurações de linha de base de web hello: configuração do .NET, ASP.NET e IIS.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="ebf9a-111">Apenas como hello avaliação de linha de base do sistema operacional, o OMS segurança será tooscan seus servidores web todas as próximas 24 horas e fornecer uma exibição de estado de segurança-los.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="ebf9a-112">No serviço de informações da Internet (IIS), as configurações são altamente personalizáveis, que permite que vários toobe níveis site e aplicativo substituído.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="ebf9a-113">o scanner Olá verifica as configurações de saudação em cada nível de site do aplicativo no nível de raiz adição toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="ebf9a-114">Isso ajuda você a locais de configurações de vulnerabilidade potencial tooidentify e corrigir rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="ebf9a-115">Avaliação de Linha de Base de Segurança da Web</span><span class="sxs-lookup"><span data-stu-id="ebf9a-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="ebf9a-116">Para essa visualização, este recurso será toobe acessado usando a opção de pesquisa do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="ebf9a-117">Siga as próximas etapas, Olá tooperform consulta de saudação apropriada:</span><span class="sxs-lookup"><span data-stu-id="ebf9a-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="ebf9a-118">Em Olá **Microsoft Operations Management Suite** clique de painel principal **segurança e auditoria** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="ebf9a-119">Em Olá **segurança e auditoria** painel, clique em **pesquisa de Log** botão.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="ebf9a-120">Olá primeira consulta que você pode usar é Olá **Resumo da avaliação da linha de base**.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="ebf9a-121">Em Olá **Iniciar pesquisa aqui** , digite esta consulta: tipo*= SecurityBaselineSummary BaselineType = web*.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="ebf9a-122">saudação de tela a seguir tem um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="ebf9a-122">hello following screen has an output sample:</span></span>

![Avaliação de linha de base da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="ebf9a-124">Nesta consulta, cada registro indica o resumo da avaliação em um único servidor.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="ebf9a-125">Quando estiver no hello **pesquisa de Log**, você pode digitar tooobtain consultas diferentes para obter mais informações sobre a avaliação de linha de base Olá web.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="ebf9a-126">Além disso toohello de consulta anterior, você também pode usar Olá aqueles nesta visualização a seguir.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="ebf9a-127">**Avaliação da regra de linha de base de Web**: Cada registro representa uma avaliação da regra de linha de base única Web em um único servidor.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="ebf9a-128">Ela inclui todos os dados de regra hello, local, resultado Olá esperado e resultado real hello.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="ebf9a-129">**Consulta**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="ebf9a-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Avaliação de regra de linha de base da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="ebf9a-131">**Mostrar todos os resultados para um servidor específico**: esta consulta mostra como toosee os resultados de um servidor específico.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="ebf9a-132">**Consulta**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="ebf9a-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Todos os resultados](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="ebf9a-134">Você também pode usar esses registros/consultas toocreate seus próprios painéis, relatórios ou alertas.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="ebf9a-135">tela Hello abaixo tem um controle de interface do usuário de exemplo que você pode adicionar tooyour painel.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="ebf9a-136">Você pode aprender como toovisualize os dados usando o Designer de exibição do OMS [aqui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="ebf9a-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="ebf9a-137">tela Hello abaixo é um exemplo de como Olá bloco se parecerá com depois de fazer essa personalização.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Interface de usuário de exemplo](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="ebf9a-139">Se você quiser que as configurações de saudação tooknow marcados para avaliação de linha de base de saudação, você pode baixar [essa planilha do Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) que contenha essas configurações.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="ebf9a-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ebf9a-140">See also</span></span>
<span data-ttu-id="ebf9a-141">Neste documento, você aprendeu sobre a avaliação de linha de base de Web da Segurança e Auditoria do OMS.</span><span class="sxs-lookup"><span data-stu-id="ebf9a-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="ebf9a-142">toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebf9a-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="ebf9a-143">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="ebf9a-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="ebf9a-144">Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria</span><span class="sxs-lookup"><span data-stu-id="ebf9a-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="ebf9a-145">Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="ebf9a-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

