---
title: "Habilitar o ajuste automático para o Banco de Dados SQL do Azure | Microsoft Docs"
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
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="6254f-103">Habilitar o ajuste automático</span><span class="sxs-lookup"><span data-stu-id="6254f-103">Enable automatic tuning</span></span>

<span data-ttu-id="6254f-104">O Banco de Dados SQL do Azure é um serviço de dados gerenciados automaticamente que monitora as consultas constantemente e identifica a ação que pode ser executada para melhorar o desempenho da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6254f-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies the action that you can perform to improve performance of your workload.</span></span> <span data-ttu-id="6254f-105">Examine as recomendações e aplique-as manualmente ou permita que o Banco de Dados SQL do Azure aplique as ações corretivas automaticamente – isso é conhecido como **modo de ajuste automático**.</span><span class="sxs-lookup"><span data-stu-id="6254f-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="6254f-106">O ajuste automático pode ser habilitado no nível do servidor ou do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6254f-106">Automatic tuning can be enabled at the server or the database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="6254f-107">Habilitar o ajuste automático no servidor</span><span class="sxs-lookup"><span data-stu-id="6254f-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="6254f-108">Para habilitar o ajuste automático no servidor de Banco de Dados SQL do Azure, navegue para o servidor no portal do Azure e, em seguida, selecione **Ajuste automático** no menu.</span><span class="sxs-lookup"><span data-stu-id="6254f-108">To enable automatic tuning on Azure SQL Database server, navigate to the server in Azure portal and then select **Automatic tuning** in the menu.</span></span> <span data-ttu-id="6254f-109">Selecione as opções de ajuste automático que você deseja habilitar e selecione **Aplicar**:</span><span class="sxs-lookup"><span data-stu-id="6254f-109">Select the automatic tuning options you want to enable and select **Apply**:</span></span>

![Servidor](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="6254f-111">As opções de ajuste automático no servidor são aplicadas a todos os bancos de dados do servidor.</span><span class="sxs-lookup"><span data-stu-id="6254f-111">Automatic tuning options on server are applied to all databases on the server.</span></span> <span data-ttu-id="6254f-112">Por padrão, todos os bancos de dados herdam a configuração de seu servidor pai, mas isso pode ser substituído e especificado para cada banco de dados individualmente.</span><span class="sxs-lookup"><span data-stu-id="6254f-112">By default, all databases inherit the configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="6254f-113">Configurar o ajuste automático no banco de dados</span><span class="sxs-lookup"><span data-stu-id="6254f-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="6254f-114">O portal do Azure permite especificar a configuração de ajuste automático individualmente em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6254f-114">The Azure portal enables you to individually specify the automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="6254f-115">A recomendação geral é gerenciar a configuração de ajuste automático no nível de servidor, de forma que as mesmas definições de configuração possam ser aplicadas em cada banco de dados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6254f-115">The general recommendation is to manage the automatic tuning configuration at server level so the same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="6254f-116">Configure o ajuste automático em um banco de dados individual caso ele seja diferente dos outros no mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="6254f-116">Configure automatic tuning on an individual database if the database is different that others on the same server.</span></span>
>

<span data-ttu-id="6254f-117">Para habilitar o ajuste automático em um banco de dados individual, navegue para o banco de dados no portal do Azure e, em seguida, selecione **Ajuste automático**.</span><span class="sxs-lookup"><span data-stu-id="6254f-117">To enable automatic tuning on a single database, navigate to the database in the Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="6254f-118">Configure um banco de dados individual para herdar as configurações do banco de dados selecionando a caixa de seleção ou especifique a configuração de um banco de dados individualmente.</span><span class="sxs-lookup"><span data-stu-id="6254f-118">You can configure a single database to inherit the settings from the database by selecting the checkbox or you can specify the configuration for a database individually.</span></span>

![Banco de dados](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="6254f-120">Depois de selecionar a configuração apropriada, clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="6254f-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6254f-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6254f-121">Next steps</span></span>
* <span data-ttu-id="6254f-122">Leia o [artigo Ajuste automático](sql-database-automatic-tuning.md) para saber mais sobre o ajuste automático e como ele pode ajudar você a melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="6254f-122">Read the [Automatic tuning article](sql-database-automatic-tuning.md) to learn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="6254f-123">Consulte [Recomendações de desempenho](sql-database-advisor.md) para obter uma visão geral das recomendações de desempenho do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="6254f-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="6254f-124">Consulte [Análise de desempenho de consultas](sql-database-query-performance.md) para saber mais sobre como visualizar o impacto no desempenho de suas principais consultas.</span><span class="sxs-lookup"><span data-stu-id="6254f-124">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>
