---
title: "políticas de acesso aaaData no Azure Insights de série de tempo | Microsoft Docs"
description: "Neste tutorial, você aprenderá toomanage políticas de acesso de dados em informações da série de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="e5ccf-103">Ambiente Grant dados access tooa Insights de série de tempo usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5ccf-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="e5ccf-104">Os ambientes de Análise de Séries Temporais possuem dois tipos independentes de políticas de acesso:</span><span class="sxs-lookup"><span data-stu-id="e5ccf-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="e5ccf-105">Políticas de acesso de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e5ccf-105">Management access policies</span></span>
* <span data-ttu-id="e5ccf-106">Políticas de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="e5ccf-106">Data access policies</span></span>

<span data-ttu-id="e5ccf-107">Os dois tipos de políticas concedem às entidades de segurança (usuários e aplicativos) do Azure Active Directory várias permissões em um ambiente específico.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="e5ccf-108">Olá entidades (usuários e aplicativos) devem pertencer toohello active directory (ou "Locatário do Azure") associado à assinatura Olá que contém o ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="e5ccf-109">Políticas de gerenciamento de acesso concederem a configuração de permissões de toohello relacionados de ambiente hello, como</span><span class="sxs-lookup"><span data-stu-id="e5ccf-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="e5ccf-110">Conjuntos de dados de referência de criação e exclusão de ambiente hello, fontes de evento, e</span><span class="sxs-lookup"><span data-stu-id="e5ccf-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="e5ccf-111">Gerenciamento de políticas de acesso de dados hello.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-111">Management of hello data access policies.</span></span>

<span data-ttu-id="e5ccf-112">Políticas de acesso de dados conceder permissões em consultas de dados tooissue, manipulam dados de referência de ambiente hello e compartilham consultas salvas e perspectivas associadas ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="e5ccf-113">dois tipos de saudação de políticas permitem separação clara entre gerenciamento de acesso à toohello do ambiente de saudação e acessar os dados toohello no ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="e5ccf-114">Por exemplo, é possível toosetup um ambiente que Olá proprietário/criador do ambiente de saudação é removido do acesso a dados hello.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="e5ccf-115">Bem como usuários e serviços que são permitidos dados tooread do ambiente Olá não pode ser concedido nenhuma configuração de toohello de acesso do ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="e5ccf-116">Conceder acesso a dados</span><span class="sxs-lookup"><span data-stu-id="e5ccf-116">Grant data access</span></span>
<span data-ttu-id="e5ccf-117">Olá etapas a seguir mostram como acesso a dados de toogrant para uma entidade de segurança do usuário:</span><span class="sxs-lookup"><span data-stu-id="e5ccf-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="e5ccf-118">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5ccf-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="e5ccf-119">Clique em "Todos os recursos" no menu de saudação no lado esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="e5ccf-120">Selecione o seu ambiente de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-120">Select your Time Series Insights environment.</span></span>

  ![Gerenciar Olá fonte de informações da série de tempo - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="e5ccf-122">Selecione "Acesso ao plano de dados", clique em "Adicionar"</span><span class="sxs-lookup"><span data-stu-id="e5ccf-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Gerenciar a fonte de informações da série de tempo de saudação - adicionar](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="e5ccf-124">Clique em “Selecionar usuário”.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="e5ccf-125">A pesquisa e selecione o usuário por email hello.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="e5ccf-126">Clique em "Selecionar" na folha "Selecionar usuário".</span><span class="sxs-lookup"><span data-stu-id="e5ccf-126">Click “Select” in “Select User” blade.</span></span>

  ![Gerenciar Olá fonte de informações da série de tempo - selecione o usuário](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="e5ccf-128">Clique em “Selecionar função”.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="e5ccf-129">Selecione "Colaborador" Se você deseja que os dados de referência do tooallow usuário toochange e compartilha consultas salvas e perspectivas com outros usuários do ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="e5ccf-130">Caso contrário, selecione dados de consulta de usuário "Leitor" tooallow no ambiente de saudação e salve pessoais consultas (não compartilhadas) no ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5ccf-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="e5ccf-131">Clique em "Okey" na folha do hello "Selecionar função".</span><span class="sxs-lookup"><span data-stu-id="e5ccf-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Gerenciar Olá fonte de informações da série de tempo - função select](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="e5ccf-133">Clique em "Okey" na folha do hello "Selecionar a função de usuário".</span><span class="sxs-lookup"><span data-stu-id="e5ccf-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="e5ccf-134">Você deverá ver:</span><span class="sxs-lookup"><span data-stu-id="e5ccf-134">You should see:</span></span>

  ![Gerenciar Olá fonte de informações da série de tempo - resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="e5ccf-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5ccf-136">Next steps</span></span>

* [<span data-ttu-id="e5ccf-137">Criar uma fonte de eventos</span><span class="sxs-lookup"><span data-stu-id="e5ccf-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="e5ccf-138">[Enviar eventos](time-series-insights-send-events.md) toohello origem do evento</span><span class="sxs-lookup"><span data-stu-id="e5ccf-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="e5ccf-139">Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="e5ccf-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
