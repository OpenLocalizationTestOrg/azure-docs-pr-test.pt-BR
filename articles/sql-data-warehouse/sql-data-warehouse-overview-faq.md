---
title: Perguntas frequentes sobre o Azure SQL Data Warehouse | Microsoft Docs
description: Este artigo lista as perguntas frequentes sobre o Azure SQL Data Warehouse de clientes e desenvolvedores
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="2c106-103">Perguntas frequentes sobre o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2c106-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="2c106-104">Geral</span><span class="sxs-lookup"><span data-stu-id="2c106-104">General</span></span>

<span data-ttu-id="2c106-105">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-105">Q.</span></span> <span data-ttu-id="2c106-106">O que o SQL DW oferece em relação à segurança de dados?</span><span class="sxs-lookup"><span data-stu-id="2c106-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="2c106-107">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-107">A.</span></span> <span data-ttu-id="2c106-108">O SQL DW oferece diversas soluções para proteger dados como TDE e auditoria.</span><span class="sxs-lookup"><span data-stu-id="2c106-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="2c106-109">Para saber mais, consulte [Segurança].</span><span class="sxs-lookup"><span data-stu-id="2c106-109">For more information, see [Security].</span></span>

<span data-ttu-id="2c106-110">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-110">Q.</span></span> <span data-ttu-id="2c106-111">Em que local posso encontrar os padrões legais ou comerciais com os quais o SQL DW está em conformidade?</span><span class="sxs-lookup"><span data-stu-id="2c106-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="2c106-112">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-112">A.</span></span> <span data-ttu-id="2c106-113">Visite a página [Conformidade da Microsoft] para ver várias ofertas de conformidade por produto, como SOC e ISO.</span><span class="sxs-lookup"><span data-stu-id="2c106-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="2c106-114">Primeiro escolha pelo título Conformidade e, em seguida, expanda Azure na seção de serviços de nuvem no escopo da Microsoft no lado direito da página para ver quais serviços do Azure estão em conformidade.</span><span class="sxs-lookup"><span data-stu-id="2c106-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="2c106-115">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-115">Q.</span></span> <span data-ttu-id="2c106-116">Posso conectar o Power BI?</span><span class="sxs-lookup"><span data-stu-id="2c106-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="2c106-117">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-117">A.</span></span> <span data-ttu-id="2c106-118">Sim!</span><span class="sxs-lookup"><span data-stu-id="2c106-118">Yes!</span></span> <span data-ttu-id="2c106-119">Embora o Power BI dê suporte à consulta direta com o SQL DW, ele não se destina a um grande número de usuários nem a dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="2c106-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="2c106-120">Para o uso em produção do Power BI, recomendamos usar o Power BI no Azure Analysis Services ou no IaaS do Analysis Service.</span><span class="sxs-lookup"><span data-stu-id="2c106-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="2c106-121">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-121">Q.</span></span> <span data-ttu-id="2c106-122">Quais são os limites de capacidade do SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="2c106-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="2c106-123">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-123">A.</span></span> <span data-ttu-id="2c106-124">Consulte nossa página de [limites de capacidade] atuais.</span><span class="sxs-lookup"><span data-stu-id="2c106-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="2c106-125">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-125">Q.</span></span> <span data-ttu-id="2c106-126">Por que Escalar/Pausar/Retomar está demorando tanto para mim?</span><span class="sxs-lookup"><span data-stu-id="2c106-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="2c106-127">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-127">A.</span></span> <span data-ttu-id="2c106-128">Uma variedade de fatores pode influenciar o tempo de computação das operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="2c106-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="2c106-129">Um caso comum para operações de execução longa é a reversão transacional.</span><span class="sxs-lookup"><span data-stu-id="2c106-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="2c106-130">Quando uma operação de escala ou pausa é iniciada, todas as sessões de entrada são bloqueadas e as consultas são esvaziadas.</span><span class="sxs-lookup"><span data-stu-id="2c106-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="2c106-131">Para deixar o sistema em um estado estável, as transações devem ser revertidas antes do início de uma operação.</span><span class="sxs-lookup"><span data-stu-id="2c106-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="2c106-132">Quanto maior o número e maior o tamanho do log de transações, por mais tempo a operação ficará interrompida na restauração do sistema para um estado estável.</span><span class="sxs-lookup"><span data-stu-id="2c106-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="2c106-133">Suporte ao usuário</span><span class="sxs-lookup"><span data-stu-id="2c106-133">User support</span></span>

<span data-ttu-id="2c106-134">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-134">Q.</span></span> <span data-ttu-id="2c106-135">Tenho uma solicitação de recurso. Para qual local devo enviá-la?</span><span class="sxs-lookup"><span data-stu-id="2c106-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="2c106-136">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-136">A.</span></span> <span data-ttu-id="2c106-137">Caso tenha uma solicitação de recurso, envie-a para nossa página do [UserVoice]</span><span class="sxs-lookup"><span data-stu-id="2c106-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="2c106-138">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-138">Q.</span></span> <span data-ttu-id="2c106-139">Como posso fazer?</span><span class="sxs-lookup"><span data-stu-id="2c106-139">How can I do x?</span></span>

<span data-ttu-id="2c106-140">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-140">A.</span></span> <span data-ttu-id="2c106-141">Para obter ajuda no desenvolvimento com o SQL Data Warehouse, faça perguntas em nossa página do [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="2c106-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="2c106-142">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-142">Q.</span></span> <span data-ttu-id="2c106-143">Como fazer para enviar um tíquete de suporte?</span><span class="sxs-lookup"><span data-stu-id="2c106-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="2c106-144">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-144">A.</span></span> <span data-ttu-id="2c106-145">Os [Tíquetes de Suporte] podem ser apresentados por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c106-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="2c106-146">Suporte a linguagem/recurso do SQL</span><span class="sxs-lookup"><span data-stu-id="2c106-146">SQL language/feature support</span></span> 

<span data-ttu-id="2c106-147">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-147">Q.</span></span> <span data-ttu-id="2c106-148">Para quais tipos de dados o SQL Data Warehouse dá suporte?</span><span class="sxs-lookup"><span data-stu-id="2c106-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="2c106-149">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-149">A.</span></span> <span data-ttu-id="2c106-150">Consulte [tipos de dados] do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2c106-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="2c106-151">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-151">Q.</span></span> <span data-ttu-id="2c106-152">Para quais recursos de tabela há suporte?</span><span class="sxs-lookup"><span data-stu-id="2c106-152">What table features do you support?</span></span>

<span data-ttu-id="2c106-153">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-153">A.</span></span> <span data-ttu-id="2c106-154">Embora o SQL Data Warehouse dê suporte a vários recursos, não há suporte para alguns deles, que são documentados em [Recursos de tabela sem suporte].</span><span class="sxs-lookup"><span data-stu-id="2c106-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="2c106-155">Ferramentas e administração</span><span class="sxs-lookup"><span data-stu-id="2c106-155">Tooling and administration</span></span>

<span data-ttu-id="2c106-156">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-156">Q.</span></span> <span data-ttu-id="2c106-157">Há suporte para projetos de Banco de Dados no Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="2c106-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="2c106-158">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-158">A.</span></span> <span data-ttu-id="2c106-159">Atualmente, não há suporte para projetos de Banco de Dados no Visual Studio para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2c106-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="2c106-160">Se desejar votar para obter esse recurso, visite nossa [solicitação de recursos de projetos de Banco de Dados] do User Voice.</span><span class="sxs-lookup"><span data-stu-id="2c106-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="2c106-161">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-161">Q.</span></span> <span data-ttu-id="2c106-162">O SQL Data Warehouse dá suporte a APIs REST?</span><span class="sxs-lookup"><span data-stu-id="2c106-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="2c106-163">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-163">A.</span></span> <span data-ttu-id="2c106-164">Sim.</span><span class="sxs-lookup"><span data-stu-id="2c106-164">Yes.</span></span> <span data-ttu-id="2c106-165">A maioria das funcionalidades REST que pode ser usada com o Banco de Dados SQL também está disponível no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2c106-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="2c106-166">É possível encontrar informações sobre API nas páginas de documentação do REST ou no [MSDN].</span><span class="sxs-lookup"><span data-stu-id="2c106-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="2c106-167">Carregando</span><span class="sxs-lookup"><span data-stu-id="2c106-167">Loading</span></span>

<span data-ttu-id="2c106-168">P.</span><span class="sxs-lookup"><span data-stu-id="2c106-168">Q.</span></span> <span data-ttu-id="2c106-169">Para quais drivers de cliente há suporte?</span><span class="sxs-lookup"><span data-stu-id="2c106-169">What client drivers do you support?</span></span>

<span data-ttu-id="2c106-170">R.</span><span class="sxs-lookup"><span data-stu-id="2c106-170">A.</span></span> <span data-ttu-id="2c106-171">O suporte ao driver para o DW pode ser encontrado na página [Cadeias de conexão]</span><span class="sxs-lookup"><span data-stu-id="2c106-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="2c106-172">P: Para quais formatos de arquivo há suporte no PolyBase com o SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="2c106-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="2c106-173">R: Orc, RC, Parquet e texto simples delimitado</span><span class="sxs-lookup"><span data-stu-id="2c106-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="2c106-174">P: Ao que posso me conectar do SQL DW usando o PolyBase?</span><span class="sxs-lookup"><span data-stu-id="2c106-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="2c106-175">R: O [Azure Data Lake Store] e o [Azure Storage Blobs]</span><span class="sxs-lookup"><span data-stu-id="2c106-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="2c106-176">P: A aplicação de computação é possível ao conectar aos Azure Storage Blobs ou ao ADLS?</span><span class="sxs-lookup"><span data-stu-id="2c106-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="2c106-177">R: Não, o PolyBase do SQL DW interage apenas com os componentes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2c106-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="2c106-178">P: Posso me conectar ao HDI?</span><span class="sxs-lookup"><span data-stu-id="2c106-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="2c106-179">R: O HDI pode usar o ADLS ou o WASB como a camada HDFS.</span><span class="sxs-lookup"><span data-stu-id="2c106-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="2c106-180">Se você tiver como a camada HDFS, será possível carregar esse dados no SQL DW.</span><span class="sxs-lookup"><span data-stu-id="2c106-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="2c106-181">No entanto, não é possível gerar o cálculo de aplicação para a instância HDI.</span><span class="sxs-lookup"><span data-stu-id="2c106-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2c106-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c106-182">Next steps</span></span>
<span data-ttu-id="2c106-183">Para obter mais informações sobre o SQL Data Warehouse como um todo, consulte nossa página [Visão geral].</span><span class="sxs-lookup"><span data-stu-id="2c106-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="2c106-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="2c106-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="2c106-185">[Cadeias de conexão]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="2c106-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="2c106-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="2c106-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="2c106-187">[Tíquetes de Suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="2c106-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="2c106-188">[Segurança]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="2c106-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="2c106-189">[Conformidade da Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="2c106-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="2c106-190">[limites de capacidade]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="2c106-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="2c106-191">[tipos de dados]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="2c106-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="2c106-192">[Recursos de tabela sem suporte]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="2c106-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="2c106-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="2c106-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="2c106-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="2c106-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="2c106-195">[solicitação de recursos de projetos de Banco de Dados]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="2c106-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="2c106-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="2c106-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="2c106-197">[Visão geral]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="2c106-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>