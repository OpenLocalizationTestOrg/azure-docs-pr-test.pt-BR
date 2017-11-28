---
title: aaaUse Power BI com o SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="51ead-103">Usar o Power BI com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="51ead-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="51ead-104">Como com o banco de dados SQL Azure, a conexão direta do SQL Data Warehouse permite que usuário tooleverage poderoso lógico aplicação juntamente com recursos analíticos de saudação do Power BI.</span><span class="sxs-lookup"><span data-stu-id="51ead-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="51ead-105">Com conexão direta, consultas são enviadas tooyour back Azure SQL Data Warehouse em tempo real conforme você explora dados hello.</span><span class="sxs-lookup"><span data-stu-id="51ead-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="51ead-106">Isso, combinado com escala de saudação do SQL Data Warehouse, permite que os usuários de relatórios dinâmicos toocreate em minutos em terabytes de dados.</span><span class="sxs-lookup"><span data-stu-id="51ead-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="51ead-107">Além disso, a introdução de saudação do hello aberto no botão Power BI permite que os usuários toodirectly conectar o Power BI tootheir SQL Data Warehouse sem coletar informações de outras partes do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ead-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="51ead-108">Ao usar a Conexão Direta:</span><span class="sxs-lookup"><span data-stu-id="51ead-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="51ead-109">Especifique o nome totalmente qualificado do servidor de saudação durante a conexão (consulte abaixo para obter mais detalhes)</span><span class="sxs-lookup"><span data-stu-id="51ead-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="51ead-110">Certifique-se de que as regras de firewall para o banco de dados de saudação são configuradas muito "permitem acesso tooAzure serviços".</span><span class="sxs-lookup"><span data-stu-id="51ead-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="51ead-111">Toda ação, como selecionar uma coluna ou adicionar um filtro, consultará diretamente data warehouse de saudação</span><span class="sxs-lookup"><span data-stu-id="51ead-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="51ead-112">Blocos são atualizados aproximadamente a cada 15 minutos (a atualização não é necessário toobe agendado)</span><span class="sxs-lookup"><span data-stu-id="51ead-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="51ead-113">Perguntas e respostas não estão disponíveis para conjuntos de dados de Conexão Direta</span><span class="sxs-lookup"><span data-stu-id="51ead-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="51ead-114">As alterações no esquema não são selecionadas automaticamente</span><span class="sxs-lookup"><span data-stu-id="51ead-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="51ead-115">Todas as consultas de Conexão Direta atingirão o tempo limite após 2 minutos</span><span class="sxs-lookup"><span data-stu-id="51ead-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="51ead-116">Essas restrições e observações podem mudar conforme continuamos tooimprove Olá experiências ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="51ead-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="51ead-117">Olá etapas tooconnect são detalhadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="51ead-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="51ead-118">Usando o botão 'Abrir no Power BI' hello</span><span class="sxs-lookup"><span data-stu-id="51ead-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="51ead-119">Olá toomove de maneira mais fácil entre o SQL Data Warehouse e o Power BI é com hello aberto no botão Power BI.</span><span class="sxs-lookup"><span data-stu-id="51ead-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="51ead-120">Esse botão permite tooseamlessly começar a criar novos painéis no Power BI.</span><span class="sxs-lookup"><span data-stu-id="51ead-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="51ead-121">tooget iniciado navegue tooyour instância de SQL Data Warehouse em Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ead-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="51ead-122">Clique o botão 'Abrir no Power BI' hello.</span><span class="sxs-lookup"><span data-stu-id="51ead-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="51ead-123">Se não for capaz de toosign no diretamente, ou se você não tiver uma conta do Power BI, você precisará toosign-in.</span><span class="sxs-lookup"><span data-stu-id="51ead-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="51ead-124">Você será direcionado pré-preenchidos toohello página de conexão do SQL Data Warehouse, com informações de saudação do Data Warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="51ead-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="51ead-125">Depois de inserir suas credenciais, você será totalmente conectada tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="51ead-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="51ead-126">Conectando por meio do portal do Power BI Olá</span><span class="sxs-lookup"><span data-stu-id="51ead-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="51ead-127">Saudação de toousing de adição aberto no botão Power BI, os usuários também podem conectar tootheir SQL Data Warehouse por meio de saudação Portal do Power BI.</span><span class="sxs-lookup"><span data-stu-id="51ead-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="51ead-128">Clique em 'Obter dados' na parte inferior de Olá Olá do painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="51ead-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="51ead-129">Selecione 'Bancos de dados'.</span><span class="sxs-lookup"><span data-stu-id="51ead-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="51ead-130">Uma vez na página de bancos de dados hello, selecione 'Azure SQL Data Warehouse' e, em seguida, clique em 'Conectar'.</span><span class="sxs-lookup"><span data-stu-id="51ead-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="51ead-131">Insira as informações de conexão necessárias hello.</span><span class="sxs-lookup"><span data-stu-id="51ead-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="51ead-132">Seu nome de servidor e o nome do banco de dados podem ser encontrados no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ead-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="51ead-133">Você será direcionado volta toohello o página principal do Power BI e depois que a conexão é feita uma nova entrada em 'Conjuntos de dados' aparecerá com o nome de saudação da sua instância.</span><span class="sxs-lookup"><span data-stu-id="51ead-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="51ead-134">Você pode clicar em Olá novo conjunto de dados tooexplore todas as tabelas de saudação e exibições no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="51ead-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="51ead-135">Selecionando uma coluna enviará uma fonte de back toohello consulta, criando dinamicamente seu visual.</span><span class="sxs-lookup"><span data-stu-id="51ead-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="51ead-136">Esses elementos visuais podem ser salvas em um novo relatório e fixados de volta tooyour painel.</span><span class="sxs-lookup"><span data-stu-id="51ead-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
