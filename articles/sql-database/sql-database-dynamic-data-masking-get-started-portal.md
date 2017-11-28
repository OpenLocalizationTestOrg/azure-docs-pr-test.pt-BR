---
title: "Portal do Azure: máscara de dados dinâmicos do Banco de Dados SQL | Microsoft Docs"
description: "Como começar a usar a máscara de dados dinâmicos do Banco de Dados SQL no Portal do Azure"
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
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="60133-103">Introdução à máscara de dados dinâmicos do Banco de Dados SQL com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60133-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="60133-104">Este tópico mostra como implementar a [máscara de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md) com o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60133-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="60133-105">Você também pode implementar a máscara de dados dinâmicos usando [cmdlets de Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou a [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="60133-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="60133-106">Configurar dados dinâmicos de mascaramento para o banco de dados usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60133-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="60133-107">Inicie o Portal do Azure em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60133-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="60133-108">Navegue até a folha de configurações do banco de dados que contém os dados confidenciais que você deseja mascarar.</span><span class="sxs-lookup"><span data-stu-id="60133-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="60133-109">Clique no bloco **Máscara de Dados Dinâmicos** que inicia a folha de configuração **Máscara de Dados Dinâmicos**.</span><span class="sxs-lookup"><span data-stu-id="60133-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="60133-110">Como alternativa, role para baixo até a seção **Operações** e clique em **Máscara de Dados Dinâmicos**.</span><span class="sxs-lookup"><span data-stu-id="60133-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="60133-112">Na folha de configuração **Mascaramento de Dados Dinâmicos** , você poderá ver algumas colunas de banco de dados que o mecanismo de recomendações sinalizou para mascaramento.</span><span class="sxs-lookup"><span data-stu-id="60133-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="60133-113">Para aceitar as recomendações, basta clicar em **Adicionar Máscara** para uma ou mais colunas e uma máscara será criada com base no tipo padrão para essa coluna.</span><span class="sxs-lookup"><span data-stu-id="60133-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="60133-114">Você pode alterar a função de mascaramento clicando na regra de mascaramento e editando o formato do campo de mascaramento para um formato diferente à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="60133-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="60133-115">Clique em **Salvar** para salvar suas configurações.</span><span class="sxs-lookup"><span data-stu-id="60133-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="60133-117">Para adicionar uma máscara a uma coluna do banco de dados, na parte superior da folha de configuração **Máscara de Dados Dinâmicos**, clique em **Adicionar Máscara** para abrir a folha de configuração **Adicionar Regra de Mascaramento**</span><span class="sxs-lookup"><span data-stu-id="60133-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="60133-119">Selecione o **Esquema**, a **Tabela** e a **Coluna** para definir o campo designado que será mascarado.</span><span class="sxs-lookup"><span data-stu-id="60133-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="60133-120">Escolha um **Formato do Campo de Máscara** na lista de categorias de mascaramento dos dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="60133-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="60133-122">Clique em **Salvar** na folha da regra de mascaramento de dados para atualizar o conjunto de regras de mascaramento na política de máscara de dados dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="60133-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="60133-123">Digite os usuários do SQL ou as identidades AAD que devem ser excluídos da máscara e têm acesso aos dados confidenciais sem máscara.</span><span class="sxs-lookup"><span data-stu-id="60133-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="60133-124">Deve ser uma lista de usuários separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="60133-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="60133-125">Observe que os usuários com privilégios de administrador sempre terão acesso aos dados sem máscara originais.</span><span class="sxs-lookup"><span data-stu-id="60133-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="60133-127">Para fazer isso de forma que a camada de aplicativo possa exibir dados confidenciais para usuários com privilégios de aplicativo, adicione o usuário do SQL ou a identidade do AAD usados pelo aplicativo para consultar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60133-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="60133-128">É altamente recomendável que essa lista contenha um número mínimo de usuários privilegiados para minimizar a exposição de dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="60133-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="60133-129">Clique em **Salvar** na folha de configuração de mascaramento de dados para salvar a política de mascaramento nova ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="60133-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="60133-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60133-130">Next steps</span></span>

* <span data-ttu-id="60133-131">Para obter uma visão geral da máscara de dados dinâmicos, consulte [máscara de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="60133-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="60133-132">Você também pode implementar a máscara de dados dinâmicos usando [cmdlets de Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou a [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="60133-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>