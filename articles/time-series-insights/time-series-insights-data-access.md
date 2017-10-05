---
title: "Políticas de acesso de dados nas Análise de Séries Temporais do Azure | Microsoft Docs"
description: "Neste tutorial, você aprenderá a gerenciar políticas de acesso de dados nas Análise de Séries Temporais"
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
ms.openlocfilehash: e975c6d8f217bc73948c0c046204b16b1a742bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="6f81c-103">Conceder acesso a dados em um ambiente de Análise de Séries Temporais usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6f81c-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="6f81c-104">Os ambientes de Análise de Séries Temporais possuem dois tipos independentes de políticas de acesso:</span><span class="sxs-lookup"><span data-stu-id="6f81c-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="6f81c-105">Políticas de acesso de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6f81c-105">Management access policies</span></span>
* <span data-ttu-id="6f81c-106">Políticas de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="6f81c-106">Data access policies</span></span>

<span data-ttu-id="6f81c-107">Os dois tipos de políticas concedem às entidades de segurança (usuários e aplicativos) do Azure Active Directory várias permissões em um ambiente específico.</span><span class="sxs-lookup"><span data-stu-id="6f81c-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="6f81c-108">As entidades de segurança (usuários e aplicativos) devem pertencer ao active directory (ou "Azure locatário") associado à assinatura que contém o ambiente.</span><span class="sxs-lookup"><span data-stu-id="6f81c-108">The principals (users and apps) must belong to the active directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="6f81c-109">As políticas de acesso de gerenciamento concedem permissões relacionadas à configuração do ambiente, como</span><span class="sxs-lookup"><span data-stu-id="6f81c-109">Management access policies grant permissions related to the configuration of the environment, such as</span></span>
*   <span data-ttu-id="6f81c-110">Criação e exclusão do ambiente, origens de evento, conjuntos de dados de referência e</span><span class="sxs-lookup"><span data-stu-id="6f81c-110">Creation and deletion of the environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="6f81c-111">Gerenciamento das políticas de acesso de dados.</span><span class="sxs-lookup"><span data-stu-id="6f81c-111">Management of the data access policies.</span></span>

<span data-ttu-id="6f81c-112">As políticas de acesso a dados concedem permissões para emitir consultas de dados, manipular dados de referência no ambiente e salvar consultas compartilhadas e perspectivas associadas ao ambiente.</span><span class="sxs-lookup"><span data-stu-id="6f81c-112">Data access policies grant permissions to issue data queries, manipulate reference data in the environment, and share saved queries and perspectives associated with the environment.</span></span>

<span data-ttu-id="6f81c-113">Os dois tipos de políticas permitem uma separação clara entre o acesso ao gerenciamento do ambiente e o acesso aos dados dentro do ambiente.</span><span class="sxs-lookup"><span data-stu-id="6f81c-113">The two kinds of policies allow clear separation between access to the management of the environment and access to the data inside the environment.</span></span> <span data-ttu-id="6f81c-114">Por exemplo, é possível configurar um ambiente de modo que o proprietário/criador do ambiente é removido do acesso aos dados.</span><span class="sxs-lookup"><span data-stu-id="6f81c-114">For example, it is possible to setup an environment such that the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="6f81c-115">Assim como usuários e serviços que têm permissão para ler dados do ambiente podem não receber permissão de acesso à configuração do ambiente.</span><span class="sxs-lookup"><span data-stu-id="6f81c-115">As well as users and services that are allowed to read data from the environment may be granted no access to the configuration of the environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="6f81c-116">Conceder acesso a dados</span><span class="sxs-lookup"><span data-stu-id="6f81c-116">Grant data access</span></span>
<span data-ttu-id="6f81c-117">As etapas a seguir mostram como conceder acesso a dados para uma entidade de usuário:</span><span class="sxs-lookup"><span data-stu-id="6f81c-117">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="6f81c-118">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f81c-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="6f81c-119">Clique em "Todos os recursos" no menu à esquerda do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f81c-119">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="6f81c-120">Selecione o seu ambiente de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="6f81c-120">Select your Time Series Insights environment.</span></span>

  ![Gerenciar a fonte das Análise de Séries Temporais - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="6f81c-122">Selecione "Acesso ao plano de dados", clique em "Adicionar"</span><span class="sxs-lookup"><span data-stu-id="6f81c-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Gerenciar a fonte das Análise de Séries Temporais - adicionar](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="6f81c-124">Clique em “Selecionar usuário”.</span><span class="sxs-lookup"><span data-stu-id="6f81c-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="6f81c-125">Procure e selecione o usuário por email.</span><span class="sxs-lookup"><span data-stu-id="6f81c-125">Search and select user by the email.</span></span>
7.  <span data-ttu-id="6f81c-126">Clique em "Selecionar" na folha "Selecionar usuário".</span><span class="sxs-lookup"><span data-stu-id="6f81c-126">Click “Select” in “Select User” blade.</span></span>

  ![Gerenciar a fonte das Análise de Séries Temporais - selecionar usuário](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="6f81c-128">Clique em “Selecionar função”.</span><span class="sxs-lookup"><span data-stu-id="6f81c-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="6f81c-129">Selecione "Colaborador" se quiser permitir que o usuário altere os dados de referência e compartilhe consultas salvas e perspectivas com outros usuários do ambiente.</span><span class="sxs-lookup"><span data-stu-id="6f81c-129">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="6f81c-130">Caso contrário, selecione "Leitor" para permitir que o usuário consulte os dados no ambiente e salve as consultas (não compartilhadas) pessoais no ambiente.</span><span class="sxs-lookup"><span data-stu-id="6f81c-130">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="6f81c-131">Clique em "Ok" na folha "Selecionar função".</span><span class="sxs-lookup"><span data-stu-id="6f81c-131">Click “Ok” in the “Select Role” blade.</span></span>

  ![Gerenciar a fonte das Análise de Séries Temporais - selecionar função](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="6f81c-133">Clique em "Ok" na folha "Selecionar função do usuário".</span><span class="sxs-lookup"><span data-stu-id="6f81c-133">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="6f81c-134">Você deverá ver:</span><span class="sxs-lookup"><span data-stu-id="6f81c-134">You should see:</span></span>

  ![Gerenciar a fonte das Análise de Séries Temporais - resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="6f81c-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f81c-136">Next steps</span></span>

* [<span data-ttu-id="6f81c-137">Criar uma origem de evento</span><span class="sxs-lookup"><span data-stu-id="6f81c-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="6f81c-138">[Enviar eventos](time-series-insights-send-events.md) para a origem do evento</span><span class="sxs-lookup"><span data-stu-id="6f81c-138">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="6f81c-139">Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6f81c-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
