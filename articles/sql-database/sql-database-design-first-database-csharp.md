---
title: aaaDesign primeiro Azure banco de dados SQL - c# | Microsoft Docs
description: Saiba toodesign seu primeiro banco de dados do SQL Azure e conecte-se tooit com um programa c# usando o ADO.NET.
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
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="76fa2-103">Criar um banco de dados SQL do Azure e conectar-se com C&#x23 e o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="76fa2-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="76fa2-104">Banco de dados do SQL Azure é um relacional banco de dados como um serviço (DBaaS) no hello Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="76fa2-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="76fa2-105">Neste tutorial, você aprenderá como toouse Olá portal do Azure e o ADO.NET com o Visual Studio para:</span><span class="sxs-lookup"><span data-stu-id="76fa2-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="76fa2-106">Criar um banco de dados Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="76fa2-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="76fa2-107">Configurar uma regra de firewall de nível de servidor em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="76fa2-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="76fa2-108">Conectar o banco de dados de toohello com o ADO.NET e o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="76fa2-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="76fa2-109">Criar tabelas com o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="76fa2-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="76fa2-110">Inserir, atualizar e excluir dados com o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="76fa2-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="76fa2-111">Consultar ADO.NET de dados</span><span class="sxs-lookup"><span data-stu-id="76fa2-111">Query data ADO.NET</span></span>

<span data-ttu-id="76fa2-112">Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="76fa2-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76fa2-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76fa2-113">Prerequisites</span></span>

<span data-ttu-id="76fa2-114">Uma instalação do [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="76fa2-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="76fa2-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76fa2-115">Next steps</span></span>

<span data-ttu-id="76fa2-116">Neste tutorial, você aprendeu a tarefas básicas de banco de dados, como criam um banco de dados e tabelas, carregar e consultar dados e Olá banco de dados tooa anterior ponto de restauração pontual.</span><span class="sxs-lookup"><span data-stu-id="76fa2-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="76fa2-117">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="76fa2-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="76fa2-118">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="76fa2-118">Create a database</span></span>
> * <span data-ttu-id="76fa2-119">Configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="76fa2-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="76fa2-120">Conecte-se o banco de dados toohello com [Visual Studio e C#.](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="76fa2-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="76fa2-121">Criar tabelas</span><span class="sxs-lookup"><span data-stu-id="76fa2-121">Create tables</span></span>
> * <span data-ttu-id="76fa2-122">Inserir, atualizar e excluir dados</span><span class="sxs-lookup"><span data-stu-id="76fa2-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="76fa2-123">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="76fa2-123">Query data</span></span>

<span data-ttu-id="76fa2-124">Avançar toohello toolearn próximo de tutorial sobre como migrar seus dados.</span><span class="sxs-lookup"><span data-stu-id="76fa2-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="76fa2-125">Migrar seu banco de dados de SQL Server tooAzure banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="76fa2-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

