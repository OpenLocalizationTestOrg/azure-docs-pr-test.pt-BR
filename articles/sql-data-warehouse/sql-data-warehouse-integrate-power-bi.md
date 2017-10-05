---
title: Usar o Power BI com o SQL Data Warehouse | Microsoft Docs
description: "Dicas para usar o Power BI com o SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="9e6a0-103">Usar o Power BI com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9e6a0-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="9e6a0-104">Assim como o Banco de Dados SQL do Azure, a Conexão Direta do SQL Data Warehouse permite ao usuário aproveitar a aplicação lógica ao longo dos recursos analíticos do Power BI.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="9e6a0-105">Com a Conexão Direta, as consultas são enviadas de volta ao SQL Data Warehouse do Azure em tempo real enquanto você explora os dados.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="9e6a0-106">Esse recurso, combinado com a escala do SQL Data Warehouse, permite aos usuários criar relatórios dinâmicos dos terabytes de dados em questão de minutos.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="9e6a0-107">Além disso, a introdução do botão Abrir no Power BI permite que os usuários conectem o Power BI diretamente ao respectivo SQL Data Warehouse sem coletar informações de outras partes do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="9e6a0-108">Ao usar a Conexão Direta:</span><span class="sxs-lookup"><span data-stu-id="9e6a0-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="9e6a0-109">Especifique o nome de servidor totalmente qualificado ao conectar (veja mais detalhes abaixo)</span><span class="sxs-lookup"><span data-stu-id="9e6a0-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="9e6a0-110">Certifique-se de que as regras de firewall estejam configuradas como “Permitir acesso aos serviços do Azure”.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="9e6a0-111">Cada ação, como selecionar uma coluna ou adicionar um filtro, consultará diretamente o data warehouse</span><span class="sxs-lookup"><span data-stu-id="9e6a0-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="9e6a0-112">Os blocos são atualizados aproximadamente a cada 15 minutos (a atualização não precisa ser agendada)</span><span class="sxs-lookup"><span data-stu-id="9e6a0-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="9e6a0-113">Perguntas e respostas não estão disponíveis para conjuntos de dados de Conexão Direta</span><span class="sxs-lookup"><span data-stu-id="9e6a0-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="9e6a0-114">As alterações no esquema não são selecionadas automaticamente</span><span class="sxs-lookup"><span data-stu-id="9e6a0-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="9e6a0-115">Todas as consultas de Conexão Direta atingirão o tempo limite após 2 minutos</span><span class="sxs-lookup"><span data-stu-id="9e6a0-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="9e6a0-116">Essas restrições e observações podem mudar à medida que aprimoramos as experiências.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="9e6a0-117">As etapas para conexão estão detalhadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="9e6a0-118">Usando o botão ‘Abrir no Power BI’</span><span class="sxs-lookup"><span data-stu-id="9e6a0-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="9e6a0-119">A maneira mais fácil de mover entre o SQL Data Warehouse e o Power BI é usando o botão Abrir no Power BI.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="9e6a0-120">Esse botão permite que você comece a criar novos painéis diretamente no Power BI.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="9e6a0-121">Para começar, navegue até sua instância do SQL Data Warehouse no Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="9e6a0-122">Clique no botão “Abrir no Power BI”.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="9e6a0-123">Se não pudermos conectar você diretamente ou se você não tiver uma conta do Power BI, será preciso se conectar.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="9e6a0-124">Você será direcionado para a página de conexão do SQL Data Warehouse, com as informações do seu SQL Data Warehouse previamente populadas.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="9e6a0-125">Depois de inserir suas credenciais, você será totalmente conectado ao SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="9e6a0-126">Conectando-se pelo portal do Power BI</span><span class="sxs-lookup"><span data-stu-id="9e6a0-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="9e6a0-127">Além de usar o botão Abrir no Power BI, os usuários também podem se conectar ao respectivo SQL Data Warehouse pelo Portal do Power BI.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="9e6a0-128">Clique em 'Obter dados' na parte inferior do painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="9e6a0-129">Selecione 'Bancos de dados'.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="9e6a0-130">Uma vez na página Bancos de dados, selecione 'SQL Data Warehouse do Azure' e, em seguida, clique em 'Conectar'.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="9e6a0-131">Insira as informações de conexão necessárias.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="9e6a0-132">O nome do servidor e o nome do banco de dados podem ser encontrados no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="9e6a0-133">Você será direcionado para a página principal do Power BI e, depois que a conexão é feita, uma nova entrada em 'Conjuntos de dados' aparecerá com o nome da sua instância.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="9e6a0-134">Você pode clicar no novo conjunto de dados para explorar todas as tabelas e exibições no seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="9e6a0-135">Selecionar uma coluna enviará uma consulta de volta à origem, criando dinamicamente seu visual.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="9e6a0-136">Esses visuais podem ser salvos em um novo relatório e fixados de volta no seu painel.</span><span class="sxs-lookup"><span data-stu-id="9e6a0-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
