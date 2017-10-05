---
title: Migrar seus dados para o SQL Data Warehouse | Microsoft Docs
description: "Dicas para migrar seus dados para o SQL Data Warehouse do Azure para desenvolvimento de soluções."
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
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="6eb9f-103">Migrar seus dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-103">Migrate Your Data</span></span>
<span data-ttu-id="6eb9f-104">Os dados podem ser movidos de diferentes origens no SQL Data Warehouse com uma variedade de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="6eb9f-105">A cópia do ADF, o SSIS e o bcp podem ser usados para cumprir essa meta.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="6eb9f-106">No entanto, à medida que o volume de dados aumenta, uma boa prática é dividir em etapas o processo de migração de dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="6eb9f-107">Isso possibilita a otimização de cada etapa quanto ao desempenho e à resiliência para garantir uma migração de dados tranquila.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="6eb9f-108">Em primeiro lugar, este artigo descreve os cenários de migração simples por Cópia do ADF, SSIS e bcp.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="6eb9f-109">Em seguida, o artigo se aprofunda um pouco em como a migração pode ser otimizada.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="6eb9f-110">Cópia do ADF (Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="6eb9f-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="6eb9f-111">A [Cópia do ADF][ADF Copy] faz parte do [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="6eb9f-112">Você pode usar a Cópia do ADF para exportar dados para arquivos simples que residem no armazenamento local, arquivos simples remotos mantidos no armazenamento de blob do Azure ou diretamente no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="6eb9f-113">Se seus dados começarem em arquivos simples, você precisará transferi-los para o Azure Storage Blob antes de carregá-los no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="6eb9f-114">Depois que os dados forem transferidos para o armazenamento de blobs do Azure, você poderá optar por usar a [Cópia do ADF][ADF Copy] novamente para enviar os dados por push ao SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="6eb9f-115">O PolyBase também fornece uma opção de desempenho alto para carregamento dos dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="6eb9f-116">No entanto, isso significa usar duas ferramentas em vez de uma.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="6eb9f-117">Se precisar de melhor desempenho, use o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="6eb9f-118">Se deseja uma experiência de ferramenta única (e os dados não forem pesados), o ADF é a melhor opção.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="6eb9f-119">Acesse o artigo a seguir para ver algumas ótimas [amostras de ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="6eb9f-120">Serviços de integração</span><span class="sxs-lookup"><span data-stu-id="6eb9f-120">Integration Services</span></span>
<span data-ttu-id="6eb9f-121">O SSIS (SQL Server Integration Services) é uma ferramenta de ETL (Extração, Transformação e Carregamento) avançada e flexível que oferece suporte a fluxos de trabalho complexos, transformação de dados e várias opções de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="6eb9f-122">Use o SSIS para simplificar a transferência de dados para o Azure ou como parte de uma migração mais ampla.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="6eb9f-123">O SSIS pode exportar para UTF-8 sem a marca de ordem de byte no arquivo.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="6eb9f-124">Para configurar isso, primeiramente você deve usar o componente de coluna derivada para converter os dados de caractere no fluxo de dados para usar a página de código 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="6eb9f-125">Depois que as colunas forem convertidas, grave os dados no adaptador de destino do arquivo simples, garantindo que 65001 também tenha sido selecionado como a página de código para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="6eb9f-126">O SSIS conecta-se ao SQL Data Warehouse da mesma forma que se conecta a uma implantação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="6eb9f-127">No entanto, suas conexões precisarão usar um gerenciador de conexão ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="6eb9f-128">Você também deve ter cuidado para definir a configuração "Usar inserção em massa quando disponível" para maximizar a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="6eb9f-129">Consulte o artigo [Adaptador de destino ADO.NET][ADO.NET destination adapter] para saber mais sobre essa propriedade</span><span class="sxs-lookup"><span data-stu-id="6eb9f-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="6eb9f-130">Não há suporte para a conexão com o SQL Data Warehouse usando o OLEDB.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="6eb9f-131">Além disso, sempre há a possibilidade de que um pacote possa falhar devido a problemas de limitação ou rede.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="6eb9f-132">Crie pacotes que possam ser retomados do ponto de falha, sem precisar refazer o trabalho concluído antes da falha.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="6eb9f-133">Para obter mais informações, consulte a [documentação do SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="6eb9f-134">bcp</span><span class="sxs-lookup"><span data-stu-id="6eb9f-134">bcp</span></span>
<span data-ttu-id="6eb9f-135">O bcp é um utilitário de linha de comando desenvolvido para importação e exportação de dados de arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="6eb9f-136">Algumas transformações podem ocorrer durante a exportação de dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="6eb9f-137">Para executar transformações simples, use uma consulta para selecionar e transformar os dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="6eb9f-138">Depois de exportados, os arquivos simples podem ser carregados diretamente no banco de dados do SQL Data Warehouse de destino.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="6eb9f-139">Uma boa prática recomendada é encapsular as transformações usadas durante a exportação de dados em uma exibição no sistema de origem.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="6eb9f-140">Isso garante que a lógica seja mantida e o processo possa ser repetido.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="6eb9f-141">As vantagens do bcp são:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="6eb9f-142">Simplicidade.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-142">Simplicity.</span></span> <span data-ttu-id="6eb9f-143">A criação e a execução dos comandos do bcp são simples</span><span class="sxs-lookup"><span data-stu-id="6eb9f-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="6eb9f-144">Processo de carregamento reinicializável.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-144">Re-startable load process.</span></span> <span data-ttu-id="6eb9f-145">Depois de exportada, a carga pode ser executada várias vezes</span><span class="sxs-lookup"><span data-stu-id="6eb9f-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="6eb9f-146">As limitações do bcp são:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="6eb9f-147">O bcp funciona somente com arquivo simples tabulados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="6eb9f-148">Ele não funciona com arquivos xml ou JSON, por exemplo</span><span class="sxs-lookup"><span data-stu-id="6eb9f-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="6eb9f-149">Os recursos de transformação de dados são limitados apenas à fase de exportação e são inerentemente simples</span><span class="sxs-lookup"><span data-stu-id="6eb9f-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="6eb9f-150">O bcp não foi adaptado para ser robusto ao carregar dados pela Internet.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="6eb9f-151">Qualquer instabilidade de rede pode causar um erro de carregamento.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="6eb9f-152">O bcp depende do esquema presente no banco de dados de destino antes do carregamento</span><span class="sxs-lookup"><span data-stu-id="6eb9f-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="6eb9f-153">Para obter mais informações, consulte [Usar o bcp para carregar dados no SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="6eb9f-154">Otimizando a migração de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-154">Optimizing data migration</span></span>
<span data-ttu-id="6eb9f-155">Um processo de migração de dados SQLDW pode ser dividido efetivamente em três etapas distintas:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="6eb9f-156">Exportação dos dados de origem</span><span class="sxs-lookup"><span data-stu-id="6eb9f-156">Export of source data</span></span>
2. <span data-ttu-id="6eb9f-157">Transferência de dados para o Azure</span><span class="sxs-lookup"><span data-stu-id="6eb9f-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="6eb9f-158">Carregamento no banco de dados do SQLDW de destino</span><span class="sxs-lookup"><span data-stu-id="6eb9f-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="6eb9f-159">Cada etapa pode ser otimizada individualmente para criar um processo de migração robusto, reinicializável e flexível que maximize o desempenho em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="6eb9f-160">Otimizando o carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-160">Optimizing data load</span></span>
<span data-ttu-id="6eb9f-161">Observando-as na ordem inversa por um momento, a maneira mais rápida de carregar dados é pelo PolyBase.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="6eb9f-162">A otimização de um processo de carregamento do PolyBase impõe pré-requisitos nas etapas anteriores, de modo que é melhor entendê-los de antemão.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="6eb9f-163">Eles são:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-163">They are:</span></span>

1. <span data-ttu-id="6eb9f-164">Codificação dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-164">Encoding of data files</span></span>
2. <span data-ttu-id="6eb9f-165">Formatação dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-165">Format of data files</span></span>
3. <span data-ttu-id="6eb9f-166">Localização dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="6eb9f-167">Codificação</span><span class="sxs-lookup"><span data-stu-id="6eb9f-167">Encoding</span></span>
<span data-ttu-id="6eb9f-168">O PolyBase exige que os arquivos de dados sejam codificados em UTF-8 ou UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="6eb9f-169">Formatação dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-169">Format of data files</span></span>
<span data-ttu-id="6eb9f-170">O PolyBase exige um terminador de linha fixo de \n ou uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="6eb9f-171">Os arquivos de dados devem estar de acordo com esse padrão.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="6eb9f-172">Não existem restrições quanto a terminadores de coluna ou de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="6eb9f-173">Você precisará definir todas as colunas no arquivo como parte de sua tabela externa no PolyBase.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="6eb9f-174">Certifique-se de que todas as colunas exportadas sejam necessárias e que os tipos estejam em conformidade com os padrões exigidos.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="6eb9f-175">Consulte novamente o artigo [migrar seu esquema] para obter detalhes sobre os tipos de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="6eb9f-176">Localização dos arquivos de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-176">Location of data files</span></span>
<span data-ttu-id="6eb9f-177">O SQL Data Warehouse usa o PolyBase para carregar dados com exclusividade do Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="6eb9f-178">Consequentemente, os dados devem ser sido transferidos primeiro para o armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="6eb9f-179">Otimizando a transferência de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-179">Optimizing data transfer</span></span>
<span data-ttu-id="6eb9f-180">Uma das partes mais lentas da migração de dados é a transferência dos dados para o Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="6eb9f-181">Não só a largura de banda da rede pode ser um problema; a confiabilidade também pode atrapalhar seriamente o progresso.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="6eb9f-182">Por padrão, a migração de dados para o Azure é pela Internet, de modo que as chances de erros de transferência são razoáveis.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="6eb9f-183">No entanto, esses erros podem exigir que os dados sejam reenviados no todo ou em parte.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="6eb9f-184">Felizmente, você tem várias opções para melhorar a velocidade e a resiliência desse processo:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="6eb9f-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="6eb9f-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="6eb9f-186">Talvez você deseje considerar o uso do [ExpressRoute][ExpressRoute] para acelerar a transferência.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="6eb9f-187">O [ExpressRoute][ExpressRoute] fornece uma conexão privada estabelecida com o Azure, para que a conexão não passe pela Internet pública.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="6eb9f-188">Essa não é uma etapa obrigatória.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="6eb9f-189">No entanto, ela melhora a taxa de transferência ao enviar dados para o Azure de uma instalação local ou colocalizada.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="6eb9f-190">Os benefícios de usar o [ExpressRoute][ExpressRoute] são:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="6eb9f-191">Maior confiabilidade</span><span class="sxs-lookup"><span data-stu-id="6eb9f-191">Increased reliability</span></span>
2. <span data-ttu-id="6eb9f-192">Rede mais rápida</span><span class="sxs-lookup"><span data-stu-id="6eb9f-192">Faster network speed</span></span>
3. <span data-ttu-id="6eb9f-193">Menor latência da rede</span><span class="sxs-lookup"><span data-stu-id="6eb9f-193">Lower network latency</span></span>
4. <span data-ttu-id="6eb9f-194">Mais segurança de rede</span><span class="sxs-lookup"><span data-stu-id="6eb9f-194">higher network security</span></span>

<span data-ttu-id="6eb9f-195">O [ExpressRoute][ExpressRoute] é vantajoso em muitos cenários; não apenas na migração.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="6eb9f-196">Interessado?</span><span class="sxs-lookup"><span data-stu-id="6eb9f-196">Interested?</span></span> <span data-ttu-id="6eb9f-197">Para obter informações e os preço, acesse a [documentação do ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="6eb9f-198">Serviço de Importação e Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="6eb9f-198">Azure Import and Export Service</span></span>
<span data-ttu-id="6eb9f-199">O Serviço de Importação e Exportação do Azure é um processo de transferência de dados desenvolvido para transferências de volumes de dados grandes (GB++) e em massa (TB++) para o Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="6eb9f-200">Ele envolve gravar os dados em discos e enviá-los a um data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="6eb9f-201">O conteúdo do disco é carregado nos Blobs de Armazenamento do Azure em seu nome.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="6eb9f-202">Exibição de alto nível do processo de importação/exportação:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="6eb9f-203">Configurar um contêiner de Armazenamento de Blob do Azure para receber os dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="6eb9f-204">Exportar dados para o armazenamento local</span><span class="sxs-lookup"><span data-stu-id="6eb9f-204">Export your data to local storage</span></span>
3. <span data-ttu-id="6eb9f-205">Copiar dados em unidades de disco rígido SATA II/III de 3,5 polegadas usando a [Ferramenta de Importação/Exportação do Azure].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="6eb9f-206">Criar um Trabalho de Importação usando o Serviço de Importação e Exportação do Azure fornecendo os arquivos de diário gerados pela [Ferramenta de Importação/Exportação do Azure].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="6eb9f-207">Enviar os discos para o data center do Azure indicado</span><span class="sxs-lookup"><span data-stu-id="6eb9f-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="6eb9f-208">Seus dados são transferidos para o contêiner de Armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="6eb9f-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="6eb9f-209">Carregar os dados no SQLDW usando o PolyBase</span><span class="sxs-lookup"><span data-stu-id="6eb9f-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="6eb9f-210">Utilitário [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="6eb9f-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="6eb9f-211">O utilitário [AZCopy][AZCopy] é uma excelente ferramenta para transferir dados para os Blobs de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="6eb9f-212">Ele foi desenvolvido para transferências de volumes de dados pequenos (MB++) a muito grandes (GB++).</span><span class="sxs-lookup"><span data-stu-id="6eb9f-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="6eb9f-213">[AZCopy] também foi projetado para fornecer boa taxa de transferência resiliente ao transferir dados para o Azure e, portanto, é uma excelente opção para a etapa de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="6eb9f-214">Depois de transferidos, você pode carregar os dados no SQL Data Warehouse usando o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="6eb9f-215">Também é possível incorporar o AZCopy aos seus pacotes do SSIS usando uma tarefa “Executar Processo”.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="6eb9f-216">Para usar o AZCopy, primeiramente é preciso baixá-lo e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="6eb9f-217">Uma [versão de produção][production version] e uma [versão prévia][preview version] estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="6eb9f-218">Para carregar um arquivo do seu sistema de arquivos, será necessário um comando como o mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="6eb9f-219">Exemplo do resumo de um processo de alto nível:</span><span class="sxs-lookup"><span data-stu-id="6eb9f-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="6eb9f-220">Configurar um contêiner de blob de armazenamento do Azure para receber os dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="6eb9f-221">Exportar dados para o armazenamento local</span><span class="sxs-lookup"><span data-stu-id="6eb9f-221">Export your data to local storage</span></span>
3. <span data-ttu-id="6eb9f-222">Copiar os dados no contêiner de Armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="6eb9f-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="6eb9f-223">Carregar os dados no SQL Data Warehouse usando PolyBase</span><span class="sxs-lookup"><span data-stu-id="6eb9f-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="6eb9f-224">Documentação completa disponível: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="6eb9f-225">Otimizando a exportação de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-225">Optimizing data export</span></span>
<span data-ttu-id="6eb9f-226">Além de assegurar que a exportação está em conformidade com os requisitos apresentados pelo PolyBase, você também pode otimizar a exportação dos dados para melhorar ainda mais o processo.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="6eb9f-227">Compactação de dados</span><span class="sxs-lookup"><span data-stu-id="6eb9f-227">Data compression</span></span>
<span data-ttu-id="6eb9f-228">O PolyBase pode ler dados compactados em gzip.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="6eb9f-229">Se for possível compactar os dados em arquivos gzip, você minimizará o volume de dados que é enviado pela rede.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="6eb9f-230">Vários arquivos</span><span class="sxs-lookup"><span data-stu-id="6eb9f-230">Multiple files</span></span>
<span data-ttu-id="6eb9f-231">Dividir tabelas grandes em vários arquivos ajuda a aumentar a velocidade da exportação, bem como ajuda na capacidade de reinicialização da transferência e na capacidade de gerenciamento geral dos dados quando eles estiverem no armazenamento de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="6eb9f-232">Um dos muitos recursos interessantes do PolyBase é que ele lê todos os arquivos dentro de uma pasta e os trata como uma tabela.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="6eb9f-233">Desse modo, é uma boa ideia isolar os arquivos de cada tabela em sua própria pasta.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="6eb9f-234">O PolyBase também oferece suporte a um recurso conhecido como "passagem de pasta recursiva".</span><span class="sxs-lookup"><span data-stu-id="6eb9f-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="6eb9f-235">Você pode usar esse recurso para aprimorar ainda mais a organização dos seus dados exportados, melhorando o gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6eb9f-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="6eb9f-236">Para saber mais sobre como carregar dados com o PolyBase, consulte [Usar o PolyBase para carregar dados no SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eb9f-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6eb9f-237">Next steps</span></span>
<span data-ttu-id="6eb9f-238">Para saber mais sobre a migração, consulte [Migrar sua solução para o SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="6eb9f-239">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="6eb9f-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
