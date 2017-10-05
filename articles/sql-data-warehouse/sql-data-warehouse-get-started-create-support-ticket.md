---
title: "Como criar um tíquete de suporte para o SQL Data Warehouse | Microsoft Docs"
description: "Como criar um tíquete de suporte no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 058ff1229acee5d03db7c0305c5565ae95a85758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="fdc06-103">Como criar um tíquete de suporte para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fdc06-103">How to create a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="fdc06-104">Caso você tenha problemas com o SQL Data Warehouse, crie um tíquete de suporte para que nossa equipe de engenharia possa ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="fdc06-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="fdc06-105">A partir de 20/12/2016, a verificação de integridade de recurso no portal do Azure não é precisa.</span><span class="sxs-lookup"><span data-stu-id="fdc06-105">As of 12/20/2016, the resource health check in the Azure portal is not accurate.</span></span> <span data-ttu-id="fdc06-106">Estamos trabalhando ativamente para corrigir esse problema.</span><span class="sxs-lookup"><span data-stu-id="fdc06-106">We are actively working to fix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="fdc06-107">Criar um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="fdc06-107">Create a support ticket</span></span>
1. <span data-ttu-id="fdc06-108">Abra o [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="fdc06-108">Open the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="fdc06-109">Na tela Inicial, clique no bloco **Ajuda + suporte** .</span><span class="sxs-lookup"><span data-stu-id="fdc06-109">On the Home screen, click the **Help + support** tile.</span></span>
   
    ![Ajuda + suporte](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="fdc06-111">Na folha Ajuda + Suporte, clique em **Criar solicitação de suporte**.</span><span class="sxs-lookup"><span data-stu-id="fdc06-111">On the Help + Support blade, click **Create support request**.</span></span>
   
    ![Nova solicitação de suporte](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="fdc06-113">Selecione o **Tipo de Solicitação**.</span><span class="sxs-lookup"><span data-stu-id="fdc06-113">Select the **Request Type**.</span></span>
   
    ![Tipo de Solicitação](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="fdc06-115">Por padrão, cada SQL Server (por exemplo, myserver.database.windows.net) tem uma **Cota de DTU** de 45.000.</span><span class="sxs-lookup"><span data-stu-id="fdc06-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="fdc06-116">Essa cota é simplesmente um limite de segurança.</span><span class="sxs-lookup"><span data-stu-id="fdc06-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="fdc06-117">Você pode aumentar sua cota criando um tíquete de suporte e selecionando *Cota* como o tipo de solicitação.</span><span class="sxs-lookup"><span data-stu-id="fdc06-117">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span></span> <span data-ttu-id="fdc06-118">Para calcular suas necessidades de DTU, multiplique 7,5 pelo total de [DWU][DWU] necessário.</span><span class="sxs-lookup"><span data-stu-id="fdc06-118">To calculate your DTU needs, multiply the 7.5 by the total [DWU][DWU] needed.</span></span> <span data-ttu-id="fdc06-119">Por exemplo, você gostaria de hospedar dois DW6000s em um SQL Server, então, deve solicitar uma cota DTU de 90.000.</span><span class="sxs-lookup"><span data-stu-id="fdc06-119">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="fdc06-120">Você pode exibir o consumo atual de DTU na folha do SQL Server no portal.</span><span class="sxs-lookup"><span data-stu-id="fdc06-120">You can view your current DTU consumption from the SQL server blade in the portal.</span></span> <span data-ttu-id="fdc06-121">Os bancos de dados em pausa e retomados contam como a cota de DTU.</span><span class="sxs-lookup"><span data-stu-id="fdc06-121">Both paused and un-paused databases count toward the DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="fdc06-122">Selecione a **Assinatura** que hospeda o banco de dados com o problema que você está relatando.</span><span class="sxs-lookup"><span data-stu-id="fdc06-122">Select the **Subscription** that hosts the database with the problem you are reporting.</span></span>
   
    ![Assinatura](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="fdc06-124">Selecione **SQL Data Warehouse** como o Recurso.</span><span class="sxs-lookup"><span data-stu-id="fdc06-124">Select **SQL Data Warehouse** as the Resource.</span></span>
   
    ![Recurso](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="fdc06-126">Selecione seu [Plano de suporte do Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="fdc06-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="fdc06-127">**gerenciamento de assinaturas, cobrança e cotas** está disponível em todos os níveis de suporte.</span><span class="sxs-lookup"><span data-stu-id="fdc06-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="fdc06-128">O suporte do **reparo** é fornecido por meio do suporte do [Desenvolvedor][Developer], [Standard][Standard], [Professional Direct][Professional Direct] ou [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="fdc06-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="fdc06-129">As questões que exigem reparos são problemas vivenciados pelo cliente ao usar o Azure, em que se espera que o problema tenha sido causado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fdc06-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span></span>
   * <span data-ttu-id="fdc06-130">O **aconselhamento de desenvolvedores** e os **serviços de consultoria** estão disponíveis nos níveis de suporte [Professional Direct][Professional Direct] e [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="fdc06-130">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="fdc06-131">Se tiver um plano de suporte Premier, você também poderá relatar problemas relacionados ao SQL Data Warehouse no [portal online Microsoft Premier][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="fdc06-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="fdc06-132">Consulte os [planos de suporte do Azure][Azure support plan] para saber mais sobre os vários planos de suporte, incluindo o escopo, tempos de resposta, preços etc.  Para ver as perguntas frequentes sobre o suporte do Azure, consulte [Perguntas frequentes do suporte do Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="fdc06-132">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Plano de suporte](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="fdc06-134">Selecione o **Tipo de Problema** e **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="fdc06-134">Select the **Problem Type** and **Category**.</span></span> <span data-ttu-id="fdc06-135">Neste exemplo, escolhemos "Ferramentas" como o tipo de problema e "Ferramentas de cliente", como a categoria.</span><span class="sxs-lookup"><span data-stu-id="fdc06-135">In this example, we have chosen "Tools" as the Problem type and "Client tools" as the category.</span></span> 
   
    ![Categoria de tipo de problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="fdc06-137">Descreva o problema e escolha o nível de impacto nos negócios.</span><span class="sxs-lookup"><span data-stu-id="fdc06-137">Describe the problem and choose the level of business impact.</span></span>
   
    ![Descrição do problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="fdc06-139">Suas **informações de contato** para esse tíquete de suporte serão preenchidas previamente.</span><span class="sxs-lookup"><span data-stu-id="fdc06-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="fdc06-140">Atualize-as se necessário.</span><span class="sxs-lookup"><span data-stu-id="fdc06-140">Update this if necessary.</span></span>
    
    ![Informações de contato](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="fdc06-142">Clique em **Criar** para enviar a solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="fdc06-142">Click **Create** to submit the support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="fdc06-143">Monitorar um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="fdc06-143">Monitor a support ticket</span></span>
<span data-ttu-id="fdc06-144">Depois que você enviar a solicitação de suporte, a equipe de suporte do Azure entrará em contato com você.</span><span class="sxs-lookup"><span data-stu-id="fdc06-144">After you have submitted the support request, the Azure support team will contact you.</span></span> <span data-ttu-id="fdc06-145">Para verificar o status e os detalhes da solicitação, clique em **Gerenciar solicitações de suporte** no painel.</span><span class="sxs-lookup"><span data-stu-id="fdc06-145">To check your request status and details, click **Manage support requests** on the dashboard.</span></span>

![Verificar o status](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="fdc06-147">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="fdc06-147">Other Resources</span></span>
<span data-ttu-id="fdc06-148">Além disso, você pode conectar a comunidade do SQL Data Warehouse no [Stack Overflow][Stack Overflow] ou no Fórum MSDN do [Azure SQL Data Warehouse][Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="fdc06-148">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

