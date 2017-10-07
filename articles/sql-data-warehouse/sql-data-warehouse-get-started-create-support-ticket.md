---
title: "aaaHow toocreate um tíquete de suporte para o SQL Data Warehouse | Microsoft Docs"
description: "Como toocreate suporte um tíquete no Azure SQL Data Warehouse."
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
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="8b494-103">Como toocreate suporte um tíquete para SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8b494-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="8b494-104">Caso você tenha problemas com o SQL Data Warehouse, crie um tíquete de suporte para que nossa equipe de engenharia possa ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="8b494-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="8b494-105">A partir de 20/12/2016, não é precisa Olá verificação de integridade de recursos no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b494-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="8b494-106">Estamos trabalhando ativamente toofix esse problema.</span><span class="sxs-lookup"><span data-stu-id="8b494-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="8b494-107">Criar um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="8b494-107">Create a support ticket</span></span>
1. <span data-ttu-id="8b494-108">Olá abrir [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="8b494-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="8b494-109">Na tela de início de saudação, clique em Olá **ajuda + suporte** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="8b494-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Ajuda + suporte](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="8b494-111">No Olá ajuda + suporte folha, clique em **criar solicitação de suporte**.</span><span class="sxs-lookup"><span data-stu-id="8b494-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Nova solicitação de suporte](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="8b494-113">Selecione Olá **tipo de solicitação**.</span><span class="sxs-lookup"><span data-stu-id="8b494-113">Select hello **Request Type**.</span></span>
   
    ![Tipo de Solicitação](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="8b494-115">Por padrão, cada SQL Server (por exemplo, myserver.database.windows.net) tem uma **Cota de DTU** de 45.000.</span><span class="sxs-lookup"><span data-stu-id="8b494-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="8b494-116">Essa cota é simplesmente um limite de segurança.</span><span class="sxs-lookup"><span data-stu-id="8b494-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="8b494-117">Você pode aumentar a cota, crie um tíquete de suporte e selecione *cota* como tipo de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b494-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="8b494-118">toocalculate precisa, multiplique o DTU Olá 7.5 por Olá total [DWU] [ DWU] necessário.</span><span class="sxs-lookup"><span data-stu-id="8b494-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="8b494-119">Por exemplo, você gostaria que toohost duas DW6000s em um SQL server, você deve solicitar uma cota DTU de 90.000.</span><span class="sxs-lookup"><span data-stu-id="8b494-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="8b494-120">Você pode exibir seu consumo de DTU atual da folha de saudação SQL server no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b494-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="8b494-121">Bancos de dados em pausa e retomados contam para a cota de DTU de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b494-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="8b494-122">Selecione Olá **assinatura** hosts Olá banco de dados com problema Olá você está se comunicando.</span><span class="sxs-lookup"><span data-stu-id="8b494-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Assinatura](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="8b494-124">Selecione **SQL Data Warehouse** como Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="8b494-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Recurso](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="8b494-126">Selecione seu [Plano de suporte do Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="8b494-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="8b494-127">**gerenciamento de assinaturas, cobrança e cotas** está disponível em todos os níveis de suporte.</span><span class="sxs-lookup"><span data-stu-id="8b494-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="8b494-128">O suporte do **reparo** é fornecido por meio do suporte do [Desenvolvedor][Developer], [Standard][Standard], [Professional Direct][Professional Direct] ou [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="8b494-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="8b494-129">Problemas são problemas enfrentados pelos clientes durante o uso do Azure onde há uma expectativa razoável problema Olá Microsoft causada.</span><span class="sxs-lookup"><span data-stu-id="8b494-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="8b494-130">**Desenvolvedor aconselhamento** e **os serviços de consultoria** estão disponíveis em Olá [Professional Direct] [ Professional Direct] e [Premier] [ Premier] níveis de suporte.</span><span class="sxs-lookup"><span data-stu-id="8b494-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="8b494-131">Se você tiver um Premier plano de suporte, você também pode relatar SQL Data Warehouse relacionados a problemas de saudação [portal online da Microsoft Premier][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="8b494-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="8b494-132">Consulte [planos de suporte do Azure] [ Azure support plan] toolearn mais sobre Olá vários oferecem suporte a planos, incluindo o escopo, tempos de resposta, preços, etc.  Para ver as perguntas frequentes sobre o suporte do Azure, consulte [Perguntas frequentes do suporte do Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="8b494-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Plano de suporte](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="8b494-134">Selecione Olá **tipo de problema** e **categoria**.</span><span class="sxs-lookup"><span data-stu-id="8b494-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="8b494-135">Neste exemplo, escolhemos como tipo de problema de hello "ferramentas" e "Ferramentas de cliente" como categoria da saudação.</span><span class="sxs-lookup"><span data-stu-id="8b494-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Categoria de tipo de problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="8b494-137">Descreva o problema de saudação e escolha Olá nível de impacto nos negócios.</span><span class="sxs-lookup"><span data-stu-id="8b494-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Descrição do problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="8b494-139">Suas **informações de contato** para esse tíquete de suporte serão preenchidas previamente.</span><span class="sxs-lookup"><span data-stu-id="8b494-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="8b494-140">Atualize-as se necessário.</span><span class="sxs-lookup"><span data-stu-id="8b494-140">Update this if necessary.</span></span>
    
    ![Informações de contato](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="8b494-142">Clique em **criar** toosubmit Olá o suporte da solicitação.</span><span class="sxs-lookup"><span data-stu-id="8b494-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="8b494-143">Monitorar um tíquete de suporte</span><span class="sxs-lookup"><span data-stu-id="8b494-143">Monitor a support ticket</span></span>
<span data-ttu-id="8b494-144">Depois que você enviou a solicitação de suporte Olá, equipe de suporte do Azure Olá entrará em contato com você.</span><span class="sxs-lookup"><span data-stu-id="8b494-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="8b494-145">toocheck seu status de solicitação e os detalhes, clique em **gerenciar solicitações de suporte** no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b494-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Verificar o status](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="8b494-147">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="8b494-147">Other Resources</span></span>
<span data-ttu-id="8b494-148">Além disso, você pode se conectar com hello da comunidade do SQL Data Warehouse em [estouro de pilha] [ Stack Overflow] ou em Olá [Fórum do MSDN do Azure SQL Data Warehouse] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="8b494-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

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

