---
title: Criar seu primeiro banco de dados SQL do Azure - C# | Microsoft Docs
description: "Aprenda a criar seu primeiro banco de dados SQL do Azure e conectá-lo a um programa em C# usando o ADO.NET."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: d9731cf5399cce6f103129ccda521f2867bd8da6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="ded96-103">Criar um banco de dados SQL do Azure e conectar-se com C&#x23 e o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ded96-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="ded96-104">O Banco de Dados SQL do Azure é um DBaaS (banco de dados como serviço) no Microsoft Cloud (“Azure”).</span><span class="sxs-lookup"><span data-stu-id="ded96-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="ded96-105">Neste tutorial, você aprenderá a usar o portal do Azure e o ADO.NET com o Visual Studio para:</span><span class="sxs-lookup"><span data-stu-id="ded96-105">In this tutorial, you learn how to use the Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ded96-106">Criar um banco de dados no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ded96-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="ded96-107">Configurar uma regra de firewall de nível de servidor no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ded96-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="ded96-108">Conecte-se ao banco de dados com o ADO.NET e o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ded96-108">Connect to the database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="ded96-109">Criar tabelas com o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ded96-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="ded96-110">Inserir, atualizar e excluir dados com o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ded96-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="ded96-111">Consultar ADO.NET de dados</span><span class="sxs-lookup"><span data-stu-id="ded96-111">Query data ADO.NET</span></span>

<span data-ttu-id="ded96-112">Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="ded96-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ded96-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ded96-113">Prerequisites</span></span>

<span data-ttu-id="ded96-114">Uma instalação do [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ded96-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- The following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- The following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="ded96-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ded96-115">Next steps</span></span>

<span data-ttu-id="ded96-116">Neste tutorial, você aprendeu as tarefas básicas de banco de dados, como criar um banco de dados e tabelas, carregar e consultar dados e restaurar o banco de dados para um ponto anterior no tempo.</span><span class="sxs-lookup"><span data-stu-id="ded96-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="ded96-117">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="ded96-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ded96-118">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="ded96-118">Create a database</span></span>
> * <span data-ttu-id="ded96-119">Configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="ded96-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="ded96-120">Conectar-se ao banco de dados com o [Visual Studio e C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ded96-120">Connect to the database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="ded96-121">Criar tabelas</span><span class="sxs-lookup"><span data-stu-id="ded96-121">Create tables</span></span>
> * <span data-ttu-id="ded96-122">Inserir, atualizar e excluir dados</span><span class="sxs-lookup"><span data-stu-id="ded96-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="ded96-123">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="ded96-123">Query data</span></span>

<span data-ttu-id="ded96-124">Avance para o próximo tutorial para saber mais sobre como migrar seus dados.</span><span class="sxs-lookup"><span data-stu-id="ded96-124">Advance to the next tutorial to learn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="ded96-125">Migrar seu banco de dados do SQL Server para o banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ded96-125">Migrate your SQL Server database to Azure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

