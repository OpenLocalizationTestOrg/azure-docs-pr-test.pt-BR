---
title: aaaAzure SQL Data Warehouse perguntas frequentes | Microsoft Docs
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="4e74a-103">Perguntas frequentes sobre o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4e74a-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="4e74a-104">Geral</span><span class="sxs-lookup"><span data-stu-id="4e74a-104">General</span></span>

<span data-ttu-id="4e74a-105">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-105">Q.</span></span> <span data-ttu-id="4e74a-106">O que o SQL DW oferece em relação à segurança de dados?</span><span class="sxs-lookup"><span data-stu-id="4e74a-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="4e74a-107">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-107">A.</span></span> <span data-ttu-id="4e74a-108">O SQL DW oferece diversas soluções para proteger dados como TDE e auditoria.</span><span class="sxs-lookup"><span data-stu-id="4e74a-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="4e74a-109">Para saber mais, consulte [Segurança].</span><span class="sxs-lookup"><span data-stu-id="4e74a-109">For more information, see [Security].</span></span>

<span data-ttu-id="4e74a-110">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-110">Q.</span></span> <span data-ttu-id="4e74a-111">Em que local posso encontrar os padrões legais ou comerciais com os quais o SQL DW está em conformidade?</span><span class="sxs-lookup"><span data-stu-id="4e74a-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="4e74a-112">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-112">A.</span></span> <span data-ttu-id="4e74a-113">Visite Olá [Microsoft Compliance] página para várias ofertas de conformidade por produto como SOC e ISO.</span><span class="sxs-lookup"><span data-stu-id="4e74a-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="4e74a-114">Primeiro escolha por título de conformidade, e então expanda Azure na seção de serviços de nuvem Olá Microsoft em escopo no lado direito de saudação do hello página toosee quais serviços são os serviços do Azure é compatíveis.</span><span class="sxs-lookup"><span data-stu-id="4e74a-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="4e74a-115">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-115">Q.</span></span> <span data-ttu-id="4e74a-116">Posso conectar o Power BI?</span><span class="sxs-lookup"><span data-stu-id="4e74a-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="4e74a-117">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-117">A.</span></span> <span data-ttu-id="4e74a-118">Sim!</span><span class="sxs-lookup"><span data-stu-id="4e74a-118">Yes!</span></span> <span data-ttu-id="4e74a-119">Embora o Power BI dê suporte à consulta direta com o SQL DW, ele não se destina a um grande número de usuários nem a dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="4e74a-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="4e74a-120">Para o uso em produção do Power BI, recomendamos usar o Power BI no Azure Analysis Services ou no IaaS do Analysis Service.</span><span class="sxs-lookup"><span data-stu-id="4e74a-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="4e74a-121">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-121">Q.</span></span> <span data-ttu-id="4e74a-122">Quais são os limites de capacidade do SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="4e74a-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="4e74a-123">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-123">A.</span></span> <span data-ttu-id="4e74a-124">Consulte nossa página de [limites de capacidade] atuais.</span><span class="sxs-lookup"><span data-stu-id="4e74a-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="4e74a-125">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-125">Q.</span></span> <span data-ttu-id="4e74a-126">Por que Escalar/Pausar/Retomar está demorando tanto para mim?</span><span class="sxs-lookup"><span data-stu-id="4e74a-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="4e74a-127">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-127">A.</span></span> <span data-ttu-id="4e74a-128">Uma variedade de fatores pode influenciar o tempo de saudação para operações de gerenciamento de computação.</span><span class="sxs-lookup"><span data-stu-id="4e74a-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="4e74a-129">Um caso comum para operações de execução longa é a reversão transacional.</span><span class="sxs-lookup"><span data-stu-id="4e74a-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="4e74a-130">Quando uma operação de escala ou pausa é iniciada, todas as sessões de entrada são bloqueadas e as consultas são esvaziadas.</span><span class="sxs-lookup"><span data-stu-id="4e74a-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="4e74a-131">No sistema de saudação ordem tooleave em um estado estável, transações devem ser revertidas antes de uma operação pode começar.</span><span class="sxs-lookup"><span data-stu-id="4e74a-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="4e74a-132">Olá maior número de saudação e tamanho de log Olá maior de transações, mais longa operação de Olá Olá será ser parado e restaurar o estado estável da saudação sistema tooa.</span><span class="sxs-lookup"><span data-stu-id="4e74a-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="4e74a-133">Suporte ao usuário</span><span class="sxs-lookup"><span data-stu-id="4e74a-133">User support</span></span>

<span data-ttu-id="4e74a-134">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-134">Q.</span></span> <span data-ttu-id="4e74a-135">Tenho uma solicitação de recurso. Para qual local devo enviá-la?</span><span class="sxs-lookup"><span data-stu-id="4e74a-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="4e74a-136">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-136">A.</span></span> <span data-ttu-id="4e74a-137">Caso tenha uma solicitação de recurso, envie-a para nossa página do [UserVoice]</span><span class="sxs-lookup"><span data-stu-id="4e74a-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="4e74a-138">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-138">Q.</span></span> <span data-ttu-id="4e74a-139">Como posso fazer?</span><span class="sxs-lookup"><span data-stu-id="4e74a-139">How can I do x?</span></span>

<span data-ttu-id="4e74a-140">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-140">A.</span></span> <span data-ttu-id="4e74a-141">Para obter ajuda no desenvolvimento com o SQL Data Warehouse, faça perguntas em nossa página do [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="4e74a-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="4e74a-142">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-142">Q.</span></span> <span data-ttu-id="4e74a-143">Como fazer para enviar um tíquete de suporte?</span><span class="sxs-lookup"><span data-stu-id="4e74a-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="4e74a-144">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-144">A.</span></span> <span data-ttu-id="4e74a-145">Os [Tíquetes de Suporte] podem ser apresentados por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e74a-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="4e74a-146">Suporte a linguagem/recurso do SQL</span><span class="sxs-lookup"><span data-stu-id="4e74a-146">SQL language/feature support</span></span> 

<span data-ttu-id="4e74a-147">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-147">Q.</span></span> <span data-ttu-id="4e74a-148">Para quais tipos de dados o SQL Data Warehouse dá suporte?</span><span class="sxs-lookup"><span data-stu-id="4e74a-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="4e74a-149">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-149">A.</span></span> <span data-ttu-id="4e74a-150">Consulte [tipos de dados] do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4e74a-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="4e74a-151">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-151">Q.</span></span> <span data-ttu-id="4e74a-152">Para quais recursos de tabela há suporte?</span><span class="sxs-lookup"><span data-stu-id="4e74a-152">What table features do you support?</span></span>

<span data-ttu-id="4e74a-153">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-153">A.</span></span> <span data-ttu-id="4e74a-154">Embora o SQL Data Warehouse dê suporte a vários recursos, não há suporte para alguns deles, que são documentados em [Recursos de tabela sem suporte].</span><span class="sxs-lookup"><span data-stu-id="4e74a-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="4e74a-155">Ferramentas e administração</span><span class="sxs-lookup"><span data-stu-id="4e74a-155">Tooling and administration</span></span>

<span data-ttu-id="4e74a-156">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-156">Q.</span></span> <span data-ttu-id="4e74a-157">Há suporte para projetos de Banco de Dados no Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="4e74a-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="4e74a-158">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-158">A.</span></span> <span data-ttu-id="4e74a-159">Atualmente, não há suporte para projetos de Banco de Dados no Visual Studio para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4e74a-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="4e74a-160">Se você quiser toocast tooget um voto que esse recurso, visite nosso User Voice [projetos de banco de dados de solicitação de recurso].</span><span class="sxs-lookup"><span data-stu-id="4e74a-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="4e74a-161">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-161">Q.</span></span> <span data-ttu-id="4e74a-162">O SQL Data Warehouse dá suporte a APIs REST?</span><span class="sxs-lookup"><span data-stu-id="4e74a-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="4e74a-163">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-163">A.</span></span> <span data-ttu-id="4e74a-164">Sim.</span><span class="sxs-lookup"><span data-stu-id="4e74a-164">Yes.</span></span> <span data-ttu-id="4e74a-165">A maioria das funcionalidades REST que pode ser usada com o Banco de Dados SQL também está disponível no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4e74a-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="4e74a-166">É possível encontrar informações sobre API nas páginas de documentação do REST ou no [MSDN].</span><span class="sxs-lookup"><span data-stu-id="4e74a-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="4e74a-167">Carregando</span><span class="sxs-lookup"><span data-stu-id="4e74a-167">Loading</span></span>

<span data-ttu-id="4e74a-168">P.</span><span class="sxs-lookup"><span data-stu-id="4e74a-168">Q.</span></span> <span data-ttu-id="4e74a-169">Para quais drivers de cliente há suporte?</span><span class="sxs-lookup"><span data-stu-id="4e74a-169">What client drivers do you support?</span></span>

<span data-ttu-id="4e74a-170">R.</span><span class="sxs-lookup"><span data-stu-id="4e74a-170">A.</span></span> <span data-ttu-id="4e74a-171">Suporte de driver para DW pode ser encontrado no hello [cadeias de caracteres de Conexão] página</span><span class="sxs-lookup"><span data-stu-id="4e74a-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="4e74a-172">P: Para quais formatos de arquivo há suporte no PolyBase com o SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="4e74a-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="4e74a-173">R: Orc, RC, Parquet e texto simples delimitado</span><span class="sxs-lookup"><span data-stu-id="4e74a-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="4e74a-174">P: o que pode conectar-se toofrom SQL DW usando PolyBase?</span><span class="sxs-lookup"><span data-stu-id="4e74a-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="4e74a-175">R: O [Azure Data Lake Store] e o [Azure Storage Blobs]</span><span class="sxs-lookup"><span data-stu-id="4e74a-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="4e74a-176">P: é possível a aplicação de computação, ao conectar-se tooAzure Blobs de armazenamento ou ADLS?</span><span class="sxs-lookup"><span data-stu-id="4e74a-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="4e74a-177">R: não, PolyBase do SQL DW interage somente os componentes de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="4e74a-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="4e74a-178">P: posso conectar tooHDI?</span><span class="sxs-lookup"><span data-stu-id="4e74a-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="4e74a-179">R: HDI pode usar ADLS ou WASB como camada HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="4e74a-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="4e74a-180">Se você tiver como a camada HDFS, será possível carregar esse dados no SQL DW.</span><span class="sxs-lookup"><span data-stu-id="4e74a-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="4e74a-181">No entanto, você não pode gerar a instância HDI de toohello de computação de aplicação.</span><span class="sxs-lookup"><span data-stu-id="4e74a-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4e74a-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e74a-182">Next steps</span></span>
<span data-ttu-id="4e74a-183">Para obter mais informações sobre o SQL Data Warehouse como um todo, consulte nossa página [Visão geral].</span><span class="sxs-lookup"><span data-stu-id="4e74a-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[cadeias de caracteres de Conexão]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Tíquetes de Suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Segurança]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[limites de capacidade]: ./sql-data-warehouse-service-capacity-limits.md
[tipos de dados]: ./sql-data-warehouse-tables-data-types.md
[Recursos de tabela sem suporte]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[projetos de banco de dados de solicitação de recurso]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Visão geral]: ./sql-data-warehouse-overview-faq.md