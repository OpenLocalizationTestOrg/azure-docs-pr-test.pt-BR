---
title: "Portal do Azure: máscara de dados dinâmicos do Banco de Dados SQL | Microsoft Docs"
description: "Como tooget iniciada com hello Portal do Azure de mascaramento de dados dinâmicos do banco de dados SQL"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="6c601-103">Introdução ao mascaramento com hello Azure Portal de dados dinâmicos do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="6c601-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="6c601-104">Este tópico mostra como tooimplement [mascaramento de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md) com hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c601-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="6c601-105">Você também pode implementar o mascaramento de dados dinâmicos usando [cmdlets do Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c601-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="6c601-106">Configurar o mascaramento de dados dinâmicos para seu banco de dados usando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6c601-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="6c601-107">Iniciar Olá Portal do Azure em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c601-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c601-108">Navegue toohello folha de configurações de banco de dados de saudação que inclui dados confidenciais hello, você deseja toomask.</span><span class="sxs-lookup"><span data-stu-id="6c601-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="6c601-109">Clique em Olá **mascaramento de dados dinâmicos** lado a lado que inicia Olá **mascaramento de dados dinâmicos** folha de configuração.</span><span class="sxs-lookup"><span data-stu-id="6c601-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="6c601-110">Como alternativa, você pode rolar para baixo toohello **operações** seção e clique em **mascaramento de dados dinâmicos**.</span><span class="sxs-lookup"><span data-stu-id="6c601-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="6c601-112">Em Olá **mascaramento de dados dinâmicos** folha de configuração, você pode ver algumas colunas de banco de dados esse mecanismo de recomendações Olá foi sinalizada para mascaramento.</span><span class="sxs-lookup"><span data-stu-id="6c601-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="6c601-113">Em ordem tooaccept recomendações hello, basta clicar em **Adicionar máscara** para uma ou mais colunas e uma máscara serão criados com base no tipo de padrão de saudação para essa coluna.</span><span class="sxs-lookup"><span data-stu-id="6c601-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="6c601-114">Você pode alterar Olá função de máscara clicando na regra de mascaramento hello e editando Olá mascaramento campo tooa outro formato de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="6c601-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="6c601-115">Ser tooclick se **salvar** toosave suas configurações.</span><span class="sxs-lookup"><span data-stu-id="6c601-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="6c601-117">tooadd uma máscara para qualquer coluna em seu banco de dados, na parte superior de saudação do hello **mascaramento de dados dinâmicos** configuração folha, clique em **Adicionar máscara** tooopen Olá **Adicionar regra de mascaramento** folha de configuração</span><span class="sxs-lookup"><span data-stu-id="6c601-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="6c601-119">Selecione Olá **esquema**, **tabela** e **coluna** toodefine Olá designado campo será mascarado.</span><span class="sxs-lookup"><span data-stu-id="6c601-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="6c601-120">Escolha um **máscara de formato de campo** de lista de saudação de categorias de mascaramento de dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="6c601-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="6c601-122">Clique em **salvar** nos dados Olá regra folha tooupdate Olá conjunto de regras de política de mascaramento de dados dinâmico Olá de mascaramento de mascaramento.</span><span class="sxs-lookup"><span data-stu-id="6c601-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="6c601-123">Os usuários do tipo hello SQL ou identidades do AAD que devem ser excluídas do mascaramento e possui dados confidenciais de toohello sem máscara de acesso.</span><span class="sxs-lookup"><span data-stu-id="6c601-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="6c601-124">Deve ser uma lista de usuários separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="6c601-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="6c601-125">Observe que os usuários com privilégios de administrador sempre têm acesso toohello dados não mascarados original.</span><span class="sxs-lookup"><span data-stu-id="6c601-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="6c601-127">toomake-Olá para camada de aplicativo pode exibir dados confidenciais para os usuários com privilégios de aplicativo, adicione Olá usuário do SQL ou o aplicativo de saudação do AAD identidade usa o banco de dados do tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="6c601-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="6c601-128">É altamente recomendável que essa lista contém um número mínimo de exposição a usuários privilegiados toominimize dados confidenciais hello.</span><span class="sxs-lookup"><span data-stu-id="6c601-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="6c601-129">Clique em **salvar** nos dados Olá configuração folha toosave Olá mascaramento novos ou atualizados política de mascaramento.</span><span class="sxs-lookup"><span data-stu-id="6c601-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6c601-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c601-130">Next steps</span></span>

* <span data-ttu-id="6c601-131">Para obter uma visão geral da máscara de dados dinâmicos, consulte [máscara de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6c601-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="6c601-132">Você também pode implementar o mascaramento de dados dinâmicos usando [cmdlets do Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c601-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
