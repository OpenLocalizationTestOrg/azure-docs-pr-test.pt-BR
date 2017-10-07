---
title: aaaMigrate tooSQL seus dados do Data Warehouse | Microsoft Docs
description: "Dicas para migrar sua tooAzure de dados SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="f4687-103">Migrar seus dados</span><span class="sxs-lookup"><span data-stu-id="f4687-103">Migrate Your Data</span></span>
<span data-ttu-id="f4687-104">Os dados podem ser movidos de diferentes origens no SQL Data Warehouse com uma variedade de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="f4687-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="f4687-105">Cópia de ADF, SSIS e todos os bcp pode ser usado tooachieve essa meta.</span><span class="sxs-lookup"><span data-stu-id="f4687-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="f4687-106">No entanto, como Olá quantidade de dados aumenta, deve pensar dividindo o processo de migração de dados de saudação em etapas.</span><span class="sxs-lookup"><span data-stu-id="f4687-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="f4687-107">Isso lhe dá a você Olá oportunidade toooptimize cada etapa para desempenho e resiliência tooensure uma migração de dados sem problemas.</span><span class="sxs-lookup"><span data-stu-id="f4687-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="f4687-108">Primeiro, este artigo descreve os cenários de migração simples de saudação de cópia do ADF, SSIS e bcp.</span><span class="sxs-lookup"><span data-stu-id="f4687-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="f4687-109">Em seguida, procure um pouco mais em como migração Olá pode ser otimizada.</span><span class="sxs-lookup"><span data-stu-id="f4687-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="f4687-110">Cópia do ADF (Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="f4687-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="f4687-111">A [Cópia do ADF][ADF Copy] faz parte do [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="f4687-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="f4687-112">Você pode usar a cópia ADF tooexport tooflat arquivos de dados do que reside no armazenamento local, arquivos simples tooremote mantidos no armazenamento de BLOBs do Azure ou diretamente no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4687-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="f4687-113">Se seus dados começam em arquivos simples, você precisará primeiro tootransfer-tooAzure blob de armazenamento antes de iniciar um carregamento no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4687-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="f4687-114">Quando dados saudação for transferidos para o armazenamento de BLOBs do Azure, você pode escolher toouse [cópia ADF] [ ADF Copy] toopush dados de saudação novamente no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4687-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="f4687-115">PolyBase também fornece uma opção de alto desempenho para carregar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4687-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="f4687-116">No entanto, isso significa usar duas ferramentas em vez de uma.</span><span class="sxs-lookup"><span data-stu-id="f4687-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="f4687-117">Se você precisa obter um melhor desempenho hello, usa o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f4687-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="f4687-118">Se você quiser uma experiência única ferramenta (e dados de saudação não são grandes) ADF é sua resposta.</span><span class="sxs-lookup"><span data-stu-id="f4687-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="f4687-119">Principal sobre toohello após o artigo para alguns ótimo [exemplos ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="f4687-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="f4687-120">Serviços de integração</span><span class="sxs-lookup"><span data-stu-id="f4687-120">Integration Services</span></span>
<span data-ttu-id="f4687-121">O SSIS (SQL Server Integration Services) é uma ferramenta de ETL (Extração, Transformação e Carregamento) avançada e flexível que oferece suporte a fluxos de trabalho complexos, transformação de dados e várias opções de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f4687-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="f4687-122">Usar o SSIS toosimply transferência dados tooAzure ou como parte de uma migração mais ampla.</span><span class="sxs-lookup"><span data-stu-id="f4687-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="f4687-123">O SSIS pode exportar tooUTF-8 sem Olá marca de ordem de bytes no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f4687-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="f4687-124">tooconfigure isso primeiro você deve usar Olá derivado coluna componente tooconvert Olá dados de caracteres hello dados fluxo toouse Olá 65001 UTF-8 página de código.</span><span class="sxs-lookup"><span data-stu-id="f4687-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="f4687-125">Quando colunas Olá tem sido convertidas, escreva Olá dados toohello arquivo simples destino adaptador garantindo que 65001 também foi selecionada como a página de código Olá para o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f4687-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="f4687-126">SSIS tooSQL Data Warehouse conecta-se exatamente como ele se conectaria tooa implantação de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4687-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="f4687-127">No entanto, as conexões precisará toobe usando um Gerenciador de conexão ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="f4687-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="f4687-128">Você também deve ter cuidado tooconfigure hello "Usar o inserção em massa quando disponível" taxa de transferência de toomaximize de configuração.</span><span class="sxs-lookup"><span data-stu-id="f4687-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="f4687-129">Consulte toohello [adaptador de destino ADO.NET] [ ADO.NET destination adapter] artigo toolearn mais sobre essa propriedade</span><span class="sxs-lookup"><span data-stu-id="f4687-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="f4687-130">Não há suporte para a conexão tooAzure SQL Data Warehouse usando OLEDB.</span><span class="sxs-lookup"><span data-stu-id="f4687-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="f4687-131">Além disso, sempre há possibilidade de saudação que um pacote pode falhar devido a problemas de rede ou toothrottling.</span><span class="sxs-lookup"><span data-stu-id="f4687-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="f4687-132">Design de pacotes para que eles possam ser retomados no ponto de saudação de falha, sem refazer o trabalho concluído antes de falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4687-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="f4687-133">Para obter mais informações, consulte Olá [documentação SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="f4687-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="f4687-134">bcp</span><span class="sxs-lookup"><span data-stu-id="f4687-134">bcp</span></span>
<span data-ttu-id="f4687-135">O bcp é um utilitário de linha de comando desenvolvido para importação e exportação de dados de arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="f4687-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="f4687-136">Algumas transformações podem ocorrer durante a exportação de dados.</span><span class="sxs-lookup"><span data-stu-id="f4687-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="f4687-137">transformações de tooperform simples usam uma consulta tooselect e transform dados de hello.</span><span class="sxs-lookup"><span data-stu-id="f4687-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="f4687-138">Uma vez exportado, arquivos simples hello, em seguida, podem ser carregados diretamente no banco de dados do SQL Data Warehouse Olá Olá destino.</span><span class="sxs-lookup"><span data-stu-id="f4687-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="f4687-139">Geralmente é Olá de tooencapsulate uma boa ideia exportar transformações usadas durante a dados em uma exibição no sistema de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4687-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="f4687-140">Isso garante que lógica Olá é retida e o processo de saudação é repetido.</span><span class="sxs-lookup"><span data-stu-id="f4687-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="f4687-141">As vantagens do bcp são:</span><span class="sxs-lookup"><span data-stu-id="f4687-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="f4687-142">Simplicidade.</span><span class="sxs-lookup"><span data-stu-id="f4687-142">Simplicity.</span></span> <span data-ttu-id="f4687-143">comandos de BCP são toobuild simple e executar</span><span class="sxs-lookup"><span data-stu-id="f4687-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="f4687-144">Processo de carregamento reinicializável.</span><span class="sxs-lookup"><span data-stu-id="f4687-144">Re-startable load process.</span></span> <span data-ttu-id="f4687-145">Uma vez exportado Olá carga pode ser executado várias vezes</span><span class="sxs-lookup"><span data-stu-id="f4687-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="f4687-146">As limitações do bcp são:</span><span class="sxs-lookup"><span data-stu-id="f4687-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="f4687-147">O bcp funciona somente com arquivo simples tabulados.</span><span class="sxs-lookup"><span data-stu-id="f4687-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="f4687-148">Ele não funciona com arquivos xml ou JSON, por exemplo</span><span class="sxs-lookup"><span data-stu-id="f4687-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="f4687-149">Recursos de transformação de dados são toohello limitado somente estágio de exportação e são simples de natureza</span><span class="sxs-lookup"><span data-stu-id="f4687-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="f4687-150">BCP não foi adaptada toobe robusto ao carregar dados sobre Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="f4687-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="f4687-151">Qualquer instabilidade de rede pode causar um erro de carregamento.</span><span class="sxs-lookup"><span data-stu-id="f4687-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="f4687-152">BCP depende do esquema Olá presente na carga de toohello anterior de banco de dados de destino Olá</span><span class="sxs-lookup"><span data-stu-id="f4687-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="f4687-153">Para obter mais informações, consulte [usar dados do bcp tooload no SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4687-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="f4687-154">Otimizando a migração de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-154">Optimizing data migration</span></span>
<span data-ttu-id="f4687-155">Um processo de migração de dados SQLDW pode ser dividido efetivamente em três etapas distintas:</span><span class="sxs-lookup"><span data-stu-id="f4687-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="f4687-156">Exportação dos dados de origem</span><span class="sxs-lookup"><span data-stu-id="f4687-156">Export of source data</span></span>
2. <span data-ttu-id="f4687-157">Transferência de dados tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4687-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="f4687-158">Carregar no banco de dados do hello destino SQLDW</span><span class="sxs-lookup"><span data-stu-id="f4687-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="f4687-159">Cada etapa pode ser otimizado individualmente toocreate um processo de migração robusta, reinicializável e resiliente que maximiza o desempenho em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="f4687-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="f4687-160">Otimizando o carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-160">Optimizing data load</span></span>
<span data-ttu-id="f4687-161">Olhando na ordem inversa para um momento; dados de tooload de maneira mais rápidos de saudação são por meio do PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f4687-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="f4687-162">Otimização para um processo de carregamento do PolyBase exige pré-requisitos de Olá etapas anteriores é melhor toounderstand isso inicial.</span><span class="sxs-lookup"><span data-stu-id="f4687-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="f4687-163">Eles são:</span><span class="sxs-lookup"><span data-stu-id="f4687-163">They are:</span></span>

1. <span data-ttu-id="f4687-164">Codificação dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-164">Encoding of data files</span></span>
2. <span data-ttu-id="f4687-165">Formatação dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-165">Format of data files</span></span>
3. <span data-ttu-id="f4687-166">Localização dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="f4687-167">Codificação</span><span class="sxs-lookup"><span data-stu-id="f4687-167">Encoding</span></span>
<span data-ttu-id="f4687-168">O PolyBase requer toobe de arquivos de dados UTF-8 ou UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="f4687-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="f4687-169">Formatação dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-169">Format of data files</span></span>
<span data-ttu-id="f4687-170">O PolyBase exige um terminador de linha fixo de \n ou uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="f4687-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="f4687-171">Os arquivos de dados devem estar de acordo com toothis padrão.</span><span class="sxs-lookup"><span data-stu-id="f4687-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="f4687-172">Não existem restrições quanto a terminadores de coluna ou de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f4687-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="f4687-173">Você terá toodefine todas as colunas no arquivo hello como parte da tabela externa no PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f4687-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="f4687-174">Certifique-se de que todas as colunas exportadas são necessárias e que tipos de saudação em conformidade com padrões toohello necessário.</span><span class="sxs-lookup"><span data-stu-id="f4687-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="f4687-175">Consulte novamente toohello [migrar seu esquema] artigo para obter detalhes sobre os tipos de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="f4687-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="f4687-176">Localização dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-176">Location of data files</span></span>
<span data-ttu-id="f4687-177">SQL Data Warehouse usa dados do armazenamento de BLOBs do Azure tooload exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="f4687-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="f4687-178">Consequentemente, dados saudação devem foram primeiro transferidos no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="f4687-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="f4687-179">Otimizando a transferência de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-179">Optimizing data transfer</span></span>
<span data-ttu-id="f4687-180">Uma das partes de hello mais lentos de migração de dados é a transferência de saudação de saudação tooAzure de dados.</span><span class="sxs-lookup"><span data-stu-id="f4687-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="f4687-181">Não só a largura de banda da rede pode ser um problema; a confiabilidade também pode atrapalhar seriamente o progresso.</span><span class="sxs-lookup"><span data-stu-id="f4687-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="f4687-182">Por padrão tooAzure migração de dados é Olá internet assim Olá possibilidades de erros de transferência ocorrendo razoavelmente provavelmente.</span><span class="sxs-lookup"><span data-stu-id="f4687-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="f4687-183">No entanto, esses erros podem exigir dados toobe enviada novamente no todo ou em parte.</span><span class="sxs-lookup"><span data-stu-id="f4687-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="f4687-184">Felizmente, você tem várias velocidade de saudação tooimprove opções e resiliência desse processo:</span><span class="sxs-lookup"><span data-stu-id="f4687-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="f4687-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="f4687-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="f4687-186">Convém usar tooconsider [ExpressRoute] [ ExpressRoute] toospeed transferência hello.</span><span class="sxs-lookup"><span data-stu-id="f4687-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="f4687-187">[Rota expressa] [ ExpressRoute] fornece a você com um tooAzure estabelecida conexão privada para a conexão de saudação não passa pelo Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="f4687-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="f4687-188">Essa não é uma etapa obrigatória.</span><span class="sxs-lookup"><span data-stu-id="f4687-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="f4687-189">No entanto, isso melhorará taxa de transferência ao enviar dados tooAzure de um local ou instalação de colocalização.</span><span class="sxs-lookup"><span data-stu-id="f4687-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="f4687-190">benefícios do uso de Olá [ExpressRoute] [ ExpressRoute] são:</span><span class="sxs-lookup"><span data-stu-id="f4687-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="f4687-191">Maior confiabilidade</span><span class="sxs-lookup"><span data-stu-id="f4687-191">Increased reliability</span></span>
2. <span data-ttu-id="f4687-192">Rede mais rápida</span><span class="sxs-lookup"><span data-stu-id="f4687-192">Faster network speed</span></span>
3. <span data-ttu-id="f4687-193">Menor latência da rede</span><span class="sxs-lookup"><span data-stu-id="f4687-193">Lower network latency</span></span>
4. <span data-ttu-id="f4687-194">Mais segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f4687-194">higher network security</span></span>

<span data-ttu-id="f4687-195">[Rota expressa] [ ExpressRoute] é benéfico para diversos cenários; Olá não apenas a migração.</span><span class="sxs-lookup"><span data-stu-id="f4687-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="f4687-196">Interessado?</span><span class="sxs-lookup"><span data-stu-id="f4687-196">Interested?</span></span> <span data-ttu-id="f4687-197">Para obter mais informações e preços, visite Olá [documentação de rota expressa][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="f4687-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="f4687-198">Serviço de Importação e Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="f4687-198">Azure Import and Export Service</span></span>
<span data-ttu-id="f4687-199">Hello Azure serviço de importação e exportação é um processo de transferência de dados grandes (GB + +) toomassive (TB + +) para transferências de dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="f4687-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="f4687-200">Ela envolve a gravar sua toodisks de dados e enviá-los tooan data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4687-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="f4687-201">conteúdo do disco Hello será carregado em Blobs de armazenamento do Azure em seu nome.</span><span class="sxs-lookup"><span data-stu-id="f4687-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="f4687-202">Uma visão geral do processo de exportação de importação de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f4687-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="f4687-203">Configurar um contêiner de armazenamento de BLOBs do Azure tooreceive Olá dados</span><span class="sxs-lookup"><span data-stu-id="f4687-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="f4687-204">Exportar seu armazenamento de dados toolocal</span><span class="sxs-lookup"><span data-stu-id="f4687-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="f4687-205">Copiar Olá dados too3.5 polegadas SATA II ou III unidades de disco rígido usando Olá [ferramenta de importação/exportação do Azure]</span><span class="sxs-lookup"><span data-stu-id="f4687-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="f4687-206">Criar um trabalho de importação usando hello importação do Azure e o serviço de exportação fornecer arquivos de diário Olá produzidos pelo Olá [ferramenta de importação/exportação do Azure]</span><span class="sxs-lookup"><span data-stu-id="f4687-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="f4687-207">Enviar os discos de saudação seu indicado data center do Azure</span><span class="sxs-lookup"><span data-stu-id="f4687-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="f4687-208">Seus dados são transferidos tooyour contêiner de armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="f4687-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="f4687-209">Carregar dados de saudação em SQLDW usando PolyBase</span><span class="sxs-lookup"><span data-stu-id="f4687-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="f4687-210">Utilitário [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="f4687-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="f4687-211">Olá [AZCopy][AZCopy] utilitário é uma excelente ferramenta para obter os dados transferidos para Blobs de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4687-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="f4687-212">Ele foi projetado para pequenos (MB + +) toovery grande (GB + +) transferências de dados.</span><span class="sxs-lookup"><span data-stu-id="f4687-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="f4687-213">[AZCopy] também foi projetado tooprovide bom throughput resiliente quando a transferência de dados tooAzure e, portanto é uma ótima opção para a etapa de transferência de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4687-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="f4687-214">Uma vez transferidos, você pode carregar dados hello usando PolyBase no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f4687-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="f4687-215">Também é possível incorporar o AZCopy aos seus pacotes do SSIS usando uma tarefa “Executar Processo”.</span><span class="sxs-lookup"><span data-stu-id="f4687-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="f4687-216">toouse AZCopy primeiro será necessário toodownload e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="f4687-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="f4687-217">Uma [versão de produção][production version] e uma [versão prévia][preview version] estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f4687-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="f4687-218">tooupload um arquivo do sistema de arquivos, que você precisará de um comando como Olá um abaixo:</span><span class="sxs-lookup"><span data-stu-id="f4687-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="f4687-219">Exemplo do resumo de um processo de alto nível:</span><span class="sxs-lookup"><span data-stu-id="f4687-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="f4687-220">Configurar um blob de armazenamento do Azure contêiner tooreceive Olá dados</span><span class="sxs-lookup"><span data-stu-id="f4687-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="f4687-221">Exportar seu armazenamento de dados toolocal</span><span class="sxs-lookup"><span data-stu-id="f4687-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="f4687-222">AZCopy seus dados no contêiner de armazenamento de BLOBs do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="f4687-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="f4687-223">Saudação de carregar dados no SQL Data Warehouse usando PolyBase</span><span class="sxs-lookup"><span data-stu-id="f4687-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="f4687-224">Documentação completa disponível: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="f4687-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="f4687-225">Otimizando a exportação de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-225">Optimizing data export</span></span>
<span data-ttu-id="f4687-226">Além disso tooensuring que exportação hello está de acordo com requisitos de toohello dispostos pelo PolyBase você também pode pesquisar toooptimize exportação de Olá Olá tooimprove saudação do processo de dados ainda mais.</span><span class="sxs-lookup"><span data-stu-id="f4687-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="f4687-227">Compactação de dados</span><span class="sxs-lookup"><span data-stu-id="f4687-227">Data compression</span></span>
<span data-ttu-id="f4687-228">O PolyBase pode ler dados compactados em gzip.</span><span class="sxs-lookup"><span data-stu-id="f4687-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="f4687-229">Se você é capaz de toocompress que toogzip dos arquivos de dados, em seguida, você minimizará a quantidade de saudação de dados sendo enviados pela rede hello.</span><span class="sxs-lookup"><span data-stu-id="f4687-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="f4687-230">Vários arquivos</span><span class="sxs-lookup"><span data-stu-id="f4687-230">Multiple files</span></span>
<span data-ttu-id="f4687-231">Dividir tabelas grandes em vários arquivos de Ajuda não só a tooimprove exportar velocidade, como também ajuda com reinicialização de transferência e Olá a capacidade de gerenciamento geral de dados Olá uma vez no armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f4687-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="f4687-232">Um dos Olá há muitos recursos de PolyBase é que ele lerá todos os arquivos de saudação dentro de uma pasta e tratá-lo como uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f4687-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="f4687-233">Portanto, é um arquivos de saudação tooisolate boa ideia para cada tabela em sua própria pasta.</span><span class="sxs-lookup"><span data-stu-id="f4687-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="f4687-234">O PolyBase também oferece suporte a um recurso conhecido como "passagem de pasta recursiva".</span><span class="sxs-lookup"><span data-stu-id="f4687-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="f4687-235">Você pode usar esse recurso toofurther melhorar a organização de saudação do seu tooimprove dados exportados o gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f4687-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="f4687-236">toolearn mais sobre o carregamento de dados com o PolyBase, consulte [Use tooload dados no SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4687-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4687-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4687-237">Next steps</span></span>
<span data-ttu-id="f4687-238">Para obter mais informações sobre migração, consulte [migrar tooSQL sua solução do Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="f4687-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="f4687-239">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="f4687-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
