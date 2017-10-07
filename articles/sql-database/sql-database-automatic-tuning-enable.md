---
title: "aaaEnable automático de ajuste de banco de dados do SQL Azure | Microsoft Docs"
description: "Habilite o ajuste automático do Banco de Dados SQL do Azure com facilidade."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="d12f5-103">Habilitar o ajuste automático</span><span class="sxs-lookup"><span data-stu-id="d12f5-103">Enable automatic tuning</span></span>

<span data-ttu-id="d12f5-104">Banco de dados do SQL Azure é um serviço de dados gerenciados automaticamente que constantemente monitora suas consultas e identifica Olá ação que você pode realizar tooimprove o desempenho da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d12f5-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="d12f5-105">Examine as recomendações e aplique-as manualmente ou permita que o Banco de Dados SQL do Azure aplique as ações corretivas automaticamente – isso é conhecido como **modo de ajuste automático**.</span><span class="sxs-lookup"><span data-stu-id="d12f5-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="d12f5-106">Ajuste automático pode ser habilitado no servidor de saudação ou nível de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d12f5-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="d12f5-107">Habilitar o ajuste automático no servidor</span><span class="sxs-lookup"><span data-stu-id="d12f5-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="d12f5-108">tooenable automático de ajuste no servidor de banco de dados SQL, navegar toohello server no Azure portal e, em seguida, selecione **ajuste automático** no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="d12f5-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="d12f5-109">Selecione Olá opções de ajuste automático, você deseja tooenable e selecione **aplicar**:</span><span class="sxs-lookup"><span data-stu-id="d12f5-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Servidor](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="d12f5-111">Automáticos de opções no servidor de ajuste são aplicadas tooall bancos de dados no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d12f5-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="d12f5-112">Por padrão, todos os bancos de dados herdam a configuração de saudação do seu servidor pai, mas isso pode ser substituído e especificado individualmente para cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d12f5-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="d12f5-113">Configurar o ajuste automático no banco de dados</span><span class="sxs-lookup"><span data-stu-id="d12f5-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="d12f5-114">Hello Azure portal permite que você tooindividually especificar a configuração de ajuste automático de saudação em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d12f5-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="d12f5-115">recomendação geral Olá é toomanage Olá ajuste a configuração automática no nível do servidor caso Olá mesmas definições de configuração podem ser aplicadas em cada banco de dados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d12f5-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="d12f5-116">Configure o ajuste automático em um banco de dados individual se a diferente que outras pessoas na Olá mesmo servidor do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d12f5-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="d12f5-117">tooenable automático de ajuste em um único banco de dados, navegue toohello banco de dados em Olá portal do Azure e, em seguida e selecione **ajuste automático**.</span><span class="sxs-lookup"><span data-stu-id="d12f5-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="d12f5-118">Você pode configurar um único banco de dados tooinherit saudação do banco de dados de saudação selecionando a caixa de seleção hello, ou você pode especificar a configuração de saudação para um banco de dados individualmente.</span><span class="sxs-lookup"><span data-stu-id="d12f5-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Banco de dados](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="d12f5-120">Depois de selecionar a configuração apropriada, clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d12f5-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d12f5-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d12f5-121">Next steps</span></span>
* <span data-ttu-id="d12f5-122">Saudação de leitura [artigo ajuste automático](sql-database-automatic-tuning.md) toolearn mais informações sobre o ajuste automático e como ele pode ajudar a melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d12f5-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="d12f5-123">Consulte [Recomendações de desempenho](sql-database-advisor.md) para obter uma visão geral das recomendações de desempenho do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="d12f5-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="d12f5-124">Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre como exibir o impacto no desempenho Olá as consultas principais.</span><span class="sxs-lookup"><span data-stu-id="d12f5-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
