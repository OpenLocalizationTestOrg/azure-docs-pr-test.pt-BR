---
title: "Identificar cenários de análise avançada para Azure Machine Learning | Microsoft Docs"
description: "Escolha os cenários apropriados para realizar a análise preditiva avançada com o Processo de Ciência de Dados de Equipe."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="47ffc-103">Cenários para análises avançadas no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="47ffc-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="47ffc-104">Este artigo descreve as diversas fontes de dados de exemplo e os cenários de destino que podem ser manipulados pelo [TDSP (Processo de Ciência de Dados de Equipe)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="47ffc-105">O TDSP fornece uma abordagem sistemática para que as equipes colaborem na criação de aplicativos inteligentes.</span><span class="sxs-lookup"><span data-stu-id="47ffc-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="47ffc-106">Os cenários apresentados aqui ilustram as opções disponíveis no fluxo de trabalho de processamento de dados que dependem das características de dados, de locais de origem e de repositórios de destino no Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="47ffc-107">A **árvore de decisão** para selecionar os cenários de exemplo apropriados para seus dados e objetivo é apresentada na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="47ffc-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="47ffc-108">Cada uma das seções a seguir apresenta um cenário de exemplo.</span><span class="sxs-lookup"><span data-stu-id="47ffc-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="47ffc-109">Para cada cenário, são listados uma possível ciência de dados ou fluxo de análise avançada e os recursos de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="47ffc-110">**Para todos os cenários a seguir, você precisa:**
> </span><span class="sxs-lookup"><span data-stu-id="47ffc-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="47ffc-111">[Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="47ffc-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * <span data-ttu-id="47ffc-112">
            [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="47ffc-112">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md)</span></span>
> 
> 

## <span data-ttu-id="47ffc-113"><a name="smalllocal"></a>Cenário\#1: conjunto de dados tabular pequeno a médio em arquivos locais</span><span class="sxs-lookup"><span data-stu-id="47ffc-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Arquivos locais pequenos a médios][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="47ffc-115">Recursos adicionais do Azure: nenhum</span><span class="sxs-lookup"><span data-stu-id="47ffc-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="47ffc-116">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="47ffc-117">Carregue um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-117">Upload a dataset.</span></span>
3. <span data-ttu-id="47ffc-118">Crie um fluxo experimental do Azure Machine Learning começando com os conjuntos de dados carregados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="47ffc-119"><a name="smalllocalprocess"></a>Cenário \#2: conjunto de dados pequeno a médio em arquivos locais, que exige processamento</span><span class="sxs-lookup"><span data-stu-id="47ffc-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Arquivos locais pequenos a médios com processamento][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="47ffc-121">Recursos adicionais do Azure: Máquina Virtual do Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="47ffc-122">Crie uma Máquina Virtual do Azure que executa o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="47ffc-123">Carregue dados para um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="47ffc-124">Pré-processe e limpe dados no IPython Notebook, acessando dados no contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="47ffc-125">Transforme os dados para o formato limpo e em tabela.</span><span class="sxs-lookup"><span data-stu-id="47ffc-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="47ffc-126">Salve os dados transformados nos blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="47ffc-127">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="47ffc-128">Leia os dados dos blobs do Azure usando o módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="47ffc-129">Crie um fluxo experimental do Azure Machine Learning começando com os conjuntos de dados ingeridos.</span><span class="sxs-lookup"><span data-stu-id="47ffc-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="47ffc-130"><a name="largelocal"></a>Cenário \#3: conjunto de dados grande em arquivos locais, com blobs do Azure como destino</span><span class="sxs-lookup"><span data-stu-id="47ffc-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Arquivos locais grandes][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="47ffc-132">Recursos adicionais do Azure: Máquina Virtual do Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="47ffc-133">Crie uma Máquina Virtual do Azure que executa o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="47ffc-134">Carregue dados para um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="47ffc-135">Pré-processe e limpe dados no IPython Notebook, acessando dados nos blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="47ffc-136">Transforme os dados para o formato limpo e em tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="47ffc-137">Explore dados e crie recursos conforme for necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="47ffc-138">Extraia um exemplo de dados de pequeno a médio porte.</span><span class="sxs-lookup"><span data-stu-id="47ffc-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="47ffc-139">Salve os dados do exemplo nos blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="47ffc-140">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="47ffc-141">Leia os dados dos blobs do Azure usando o módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="47ffc-142">Crie um fluxo experimental do Azure Machine Learning, começando com os conjuntos de dados ingeridos.</span><span class="sxs-lookup"><span data-stu-id="47ffc-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="47ffc-143"><a name="smalllocaltodb"></a>Cenário \#4: conjunto de dados pequeno a médio em arquivos locais, com o SQL Server na Máquina Virtual do Azure como destino</span><span class="sxs-lookup"><span data-stu-id="47ffc-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Arquivos locais pequenos a médios para o Banco de Dados SQL no Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="47ffc-145">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="47ffc-146">Crie uma Máquina Virtual do Azure que executa SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="47ffc-147">Carregue dados para um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="47ffc-148">Pré-processe e limpe dados no contêiner de armazenamento do Azure usando o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="47ffc-149">Transforme os dados para o formato limpo e em tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="47ffc-150">Salve dados em arquivos locais da VM (o IPython Notebook está em execução na VM, as unidades locais se referem às unidades da VM).</span><span class="sxs-lookup"><span data-stu-id="47ffc-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="47ffc-151">Carregue dados para o banco de dados do SQL Server em execução em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="47ffc-152">Opção \#1: usar o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="47ffc-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="47ffc-153">Faça logon na VM do SQL Server</span><span class="sxs-lookup"><span data-stu-id="47ffc-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="47ffc-154">Execute o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="47ffc-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="47ffc-155">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="47ffc-155">Create database and target tables.</span></span>
   * <span data-ttu-id="47ffc-156">Use um dos métodos de importação em massa para carregar os dados dos arquivos locais da VM.</span><span class="sxs-lookup"><span data-stu-id="47ffc-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="47ffc-157">Opção \#2: usar o IPython Notebook – não é aconselhável para conjuntos de dados médios e maiores</span><span class="sxs-lookup"><span data-stu-id="47ffc-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="47ffc-158">Use uma cadeia de conexão ODBC para acessar o SQL Server na VM.</span><span class="sxs-lookup"><span data-stu-id="47ffc-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="47ffc-159">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="47ffc-159">Create database and target tables.</span></span>
   * <span data-ttu-id="47ffc-160">Use um dos métodos de importação em massa para carregar os dados dos arquivos locais da VM.</span><span class="sxs-lookup"><span data-stu-id="47ffc-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="47ffc-161">Explore dados e crie recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-161">Explore data, create features as needed.</span></span> <span data-ttu-id="47ffc-162">Observe que os recursos não precisam ser materializado nas tabelas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="47ffc-163">Anote somente a consulta necessária para criá-los.</span><span class="sxs-lookup"><span data-stu-id="47ffc-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="47ffc-164">Escolha um tamanho de amostra de dados, se necessário e/ou desejado.</span><span class="sxs-lookup"><span data-stu-id="47ffc-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="47ffc-165">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="47ffc-166">Leia os dados diretamente do SQL Server usando o módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="47ffc-167">Cole a consulta necessária que extrai os campos, cria recursos e amostras de dados, se necessário, diretamente na consulta [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="47ffc-168">Crie um fluxo experimental do Azure Machine Learning, começando com os conjuntos de dados ingeridos.</span><span class="sxs-lookup"><span data-stu-id="47ffc-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="47ffc-169"><a name="largelocaltodb"></a>Cenário \#5: conjunto de dados grande em arquivos locais, com o SQL Server na VM do Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Arquivos locais grandes para o Banco de Dados SQL no Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="47ffc-171">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="47ffc-172">Crie uma Máquina Virtual do Azure que executa SQL Server e o servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="47ffc-173">Carregue dados para um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="47ffc-174">(Opcional) Pré-processe e limpe os dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="47ffc-175">a.</span><span class="sxs-lookup"><span data-stu-id="47ffc-175">a.</span></span>  <span data-ttu-id="47ffc-176">Pré-processe e limpe dados no IPython Notebook, acessando dados do Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="47ffc-177">b.</span><span class="sxs-lookup"><span data-stu-id="47ffc-177">b.</span></span>  <span data-ttu-id="47ffc-178">Transforme os dados para o formato limpo e em tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="47ffc-179">c.</span><span class="sxs-lookup"><span data-stu-id="47ffc-179">c.</span></span>  <span data-ttu-id="47ffc-180">Salve dados em arquivos locais da VM (o IPython Notebook está em execução na VM, as unidades locais se referem às unidades da VM).</span><span class="sxs-lookup"><span data-stu-id="47ffc-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="47ffc-181">Carregue dados para o banco de dados do SQL Server em execução em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="47ffc-182">a.</span><span class="sxs-lookup"><span data-stu-id="47ffc-182">a.</span></span>  <span data-ttu-id="47ffc-183">Faça logon na VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47ffc-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="47ffc-184">b.</span><span class="sxs-lookup"><span data-stu-id="47ffc-184">b.</span></span>  <span data-ttu-id="47ffc-185">Se os dados já não estiverem salvos, baixe arquivos de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="47ffc-186">c.</span><span class="sxs-lookup"><span data-stu-id="47ffc-186">c.</span></span>  <span data-ttu-id="47ffc-187">Execute o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="47ffc-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="47ffc-188">d.</span><span class="sxs-lookup"><span data-stu-id="47ffc-188">d.</span></span>  <span data-ttu-id="47ffc-189">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="47ffc-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="47ffc-190">e.</span><span class="sxs-lookup"><span data-stu-id="47ffc-190">e.</span></span>  <span data-ttu-id="47ffc-191">Use um dos métodos de importação em massa para carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="47ffc-192">f.</span><span class="sxs-lookup"><span data-stu-id="47ffc-192">f.</span></span>  <span data-ttu-id="47ffc-193">Se junções de tabelas forem necessárias, crie índices para agilizá-las.</span><span class="sxs-lookup"><span data-stu-id="47ffc-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47ffc-194">Para um carregamento mais rápido de grandes quantidades de dados, é recomendável criar tabelas particionadas e importar em massa os dados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="47ffc-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="47ffc-195">Para saber mais, consulte [Importação de Dados em Paralelo para Tabelas Particionadas do SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="47ffc-196">Explore dados e crie recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-196">Explore data, create features as needed.</span></span> <span data-ttu-id="47ffc-197">Observe que os recursos não precisam ser materializado nas tabelas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="47ffc-198">Anote somente a consulta necessária para criá-los.</span><span class="sxs-lookup"><span data-stu-id="47ffc-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="47ffc-199">Escolha um tamanho de amostra de dados, se necessário e/ou desejado.</span><span class="sxs-lookup"><span data-stu-id="47ffc-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="47ffc-200">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="47ffc-201">Leia os dados diretamente do SQL Server usando o módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="47ffc-202">Cole a consulta necessária que extrai os campos, cria recursos e amostras de dados, se necessário, diretamente na consulta [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="47ffc-203">Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado</span><span class="sxs-lookup"><span data-stu-id="47ffc-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="47ffc-204"><a name="largedbtodb"></a>Cenário \#6: conjunto de dados grande em um banco de dados do SQL Server local, com o SQL Server em uma Máquina Virtual do Azure como destino</span><span class="sxs-lookup"><span data-stu-id="47ffc-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Banco de Dados SQL local grande para o Banco de Dados SQL no Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="47ffc-206">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="47ffc-207">Crie uma Máquina Virtual do Azure que executa SQL Server e o servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="47ffc-208">Use um dos métodos de exportação de dados para exportar os dados do SQL Server para arquivos de despejo.</span><span class="sxs-lookup"><span data-stu-id="47ffc-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47ffc-209">Caso você decida mover todos os dados do banco de dados local, há um método alternativo (mais rápido) para mover o banco de dados completo para a instância do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="47ffc-210">Ignore as etapas para exportar dados, criar o banco de dados e carregar/importar dados para o banco de dados de destino e execute o método alternativo.</span><span class="sxs-lookup"><span data-stu-id="47ffc-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="47ffc-211">Carregue os arquivos de despejo no contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="47ffc-212">Carregue os dados para um banco de dados do SQL Server em execução em uma Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="47ffc-213">a.</span><span class="sxs-lookup"><span data-stu-id="47ffc-213">a.</span></span>  <span data-ttu-id="47ffc-214">Faça logon na VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47ffc-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="47ffc-215">b.</span><span class="sxs-lookup"><span data-stu-id="47ffc-215">b.</span></span>  <span data-ttu-id="47ffc-216">Baixe os arquivos de dados de um contêiner de armazenamento do Azure para a pasta da VM local.</span><span class="sxs-lookup"><span data-stu-id="47ffc-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="47ffc-217">c.</span><span class="sxs-lookup"><span data-stu-id="47ffc-217">c.</span></span>  <span data-ttu-id="47ffc-218">Execute o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="47ffc-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="47ffc-219">d.</span><span class="sxs-lookup"><span data-stu-id="47ffc-219">d.</span></span>  <span data-ttu-id="47ffc-220">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="47ffc-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="47ffc-221">e.</span><span class="sxs-lookup"><span data-stu-id="47ffc-221">e.</span></span>  <span data-ttu-id="47ffc-222">Use um dos métodos de importação em massa para carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="47ffc-223">f.</span><span class="sxs-lookup"><span data-stu-id="47ffc-223">f.</span></span>  <span data-ttu-id="47ffc-224">Se junções de tabelas forem necessárias, crie índices para agilizá-las.</span><span class="sxs-lookup"><span data-stu-id="47ffc-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47ffc-225">Para um carregamento mais rápido de grandes quantidades de dados, crie tabelas particionadas e importe em massa os dados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="47ffc-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="47ffc-226">Para saber mais, consulte [Importação de Dados em Paralelo para Tabelas Particionadas do SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="47ffc-227">Explore dados e crie recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-227">Explore data, create features as needed.</span></span> <span data-ttu-id="47ffc-228">Observe que os recursos não precisam ser materializado nas tabelas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="47ffc-229">Anote somente a consulta necessária para criá-los.</span><span class="sxs-lookup"><span data-stu-id="47ffc-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="47ffc-230">Escolha um tamanho de amostra de dados, se necessário e/ou desejado.</span><span class="sxs-lookup"><span data-stu-id="47ffc-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="47ffc-231">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="47ffc-232">Leia os dados diretamente do SQL Server usando o módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="47ffc-233">Cole a consulta necessária que extrai os campos, cria recursos e amostras de dados, se necessário, diretamente na consulta [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="47ffc-234">Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado.</span><span class="sxs-lookup"><span data-stu-id="47ffc-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="47ffc-235">Método alternativo para copiar um banco de dados completo de um SQL Server local para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Desanexar o banco de dados local e anexar ao Banco de Dados SQL no Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="47ffc-237">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="47ffc-238">Para replicar todo o banco de dados do SQL Server na sua VM do SQL Server, você deve copiar um banco de dados de um local/servidor para outro, supondo que o banco de dados possa ficar offline temporariamente.</span><span class="sxs-lookup"><span data-stu-id="47ffc-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="47ffc-239">Você pode fazer isso no Pesquisador de Objetos do SQL Server Management Studio ou usando os comandos Transact-SQL equivalentes.</span><span class="sxs-lookup"><span data-stu-id="47ffc-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="47ffc-240">Desanexe o banco de dados no local de origem.</span><span class="sxs-lookup"><span data-stu-id="47ffc-240">Detach the database at the source location.</span></span> <span data-ttu-id="47ffc-241">Para saber mais, veja [Desanexar um banco de dados](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="47ffc-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="47ffc-242">Na janela de prompt de comando do Windows Explorer ou Windows, copie os arquivos do banco de dados e os arquivos de log desanexados para o local de destino na VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="47ffc-243">Anexe os arquivos copiados à instância de destino do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47ffc-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="47ffc-244">Para saber mais, veja [Anexar um banco de dados](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="47ffc-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="47ffc-245">[Mover um Banco de Dados utilizando Desanexar e Anexar (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="47ffc-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="47ffc-246"><a name="largedbtohive"></a>Cenário \#7: Big Data em arquivos locais, com um banco de dados Hive em clusters Hadoop do Azure HDInsight como destino</span><span class="sxs-lookup"><span data-stu-id="47ffc-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Big Data no Hive local de destino][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="47ffc-248">Recursos adicionais do Azure: cluster Hadoop do Azure HDInsight e Máquina Virtual do Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="47ffc-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="47ffc-249">Crie uma Máquina Virtual do Azure que executa o servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="47ffc-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="47ffc-250">Personalize um cluster Hadoop do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47ffc-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="47ffc-251">(Opcional) Pré-processe e limpe os dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="47ffc-252">a.</span><span class="sxs-lookup"><span data-stu-id="47ffc-252">a.</span></span>  <span data-ttu-id="47ffc-253">Pré-processe e limpe dados no IPython Notebook, acessando dados do Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="47ffc-254">b.</span><span class="sxs-lookup"><span data-stu-id="47ffc-254">b.</span></span>  <span data-ttu-id="47ffc-255">Transforme os dados para o formato limpo e em tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="47ffc-256">c.</span><span class="sxs-lookup"><span data-stu-id="47ffc-256">c.</span></span>  <span data-ttu-id="47ffc-257">Salve dados em arquivos locais da VM (o IPython Notebook está em execução na VM, as unidades locais se referem às unidades da VM).</span><span class="sxs-lookup"><span data-stu-id="47ffc-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="47ffc-258">Carregue dados no contêiner padrão do cluster Hadoop selecionado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="47ffc-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="47ffc-259">Carregue dados para o banco de dados Hive no cluster Hadoop do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47ffc-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="47ffc-260">a.</span><span class="sxs-lookup"><span data-stu-id="47ffc-260">a.</span></span>  <span data-ttu-id="47ffc-261">Faça logon no nó principal do cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="47ffc-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="47ffc-262">b.</span><span class="sxs-lookup"><span data-stu-id="47ffc-262">b.</span></span>  <span data-ttu-id="47ffc-263">Abra a linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47ffc-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="47ffc-264">c.</span><span class="sxs-lookup"><span data-stu-id="47ffc-264">c.</span></span>  <span data-ttu-id="47ffc-265">Insira o diretório raiz do Hive pelo comando `cd %hive_home%\bin` na linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47ffc-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="47ffc-266">d.</span><span class="sxs-lookup"><span data-stu-id="47ffc-266">d.</span></span>  <span data-ttu-id="47ffc-267">Execute as consultas do Hive para criar o banco de dados e tabelas e carregue dados do armazenamento de blob para as tabelas do Hive.</span><span class="sxs-lookup"><span data-stu-id="47ffc-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47ffc-268">Se o volume de dados for grande, os usuários podem criar a tabela do Hive com partições.</span><span class="sxs-lookup"><span data-stu-id="47ffc-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="47ffc-269">Em seguida, os usuários podem usar um loop `for` na linha de comando do Hadoop no nó principal para carregar dados na tabela do Hive particionada, por partição.</span><span class="sxs-lookup"><span data-stu-id="47ffc-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="47ffc-270">Explore dados e crie recursos conforme necessário na linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47ffc-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="47ffc-271">Observe que os recursos não precisam ser materializado nas tabelas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="47ffc-272">Anote somente a consulta necessária para criá-los.</span><span class="sxs-lookup"><span data-stu-id="47ffc-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="47ffc-273">a.</span><span class="sxs-lookup"><span data-stu-id="47ffc-273">a.</span></span>  <span data-ttu-id="47ffc-274">Faça logon no nó principal do cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="47ffc-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="47ffc-275">b.</span><span class="sxs-lookup"><span data-stu-id="47ffc-275">b.</span></span>  <span data-ttu-id="47ffc-276">Abra a linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47ffc-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="47ffc-277">c.</span><span class="sxs-lookup"><span data-stu-id="47ffc-277">c.</span></span>  <span data-ttu-id="47ffc-278">Insira o diretório raiz do Hive pelo comando `cd %hive_home%\bin` na linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47ffc-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="47ffc-279">d.</span><span class="sxs-lookup"><span data-stu-id="47ffc-279">d.</span></span>  <span data-ttu-id="47ffc-280">Execute as consultas do Hive na linha de comando do Hadoop no nó principal do cluster do Hadoop para explorar os dados e criar recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="47ffc-281">Se necessário e/ou desejado, faça amostras dos dados para que eles caibam no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="47ffc-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="47ffc-282">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="47ffc-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="47ffc-283">Leia os dados diretamente do `Hive Queries` usando o módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="47ffc-284">Cole a consulta necessária que extrai os campos, cria recursos e amostras de dados, se necessário, diretamente na consulta [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="47ffc-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="47ffc-285">Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado.</span><span class="sxs-lookup"><span data-stu-id="47ffc-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="47ffc-286"><a name="decisiontree"></a>Árvore de decisão para a seleção do cenário</span><span class="sxs-lookup"><span data-stu-id="47ffc-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="47ffc-287">O diagrama a seguir resume os cenários descritos acima e as opções do Processo e Tecnologia de Análise Avançada selecionadas que o levam a cada um dos cenários detalhados.</span><span class="sxs-lookup"><span data-stu-id="47ffc-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="47ffc-288">Observe que o processamento de dados, exploração, engenharia de recursos e amostragem podem ocorrer em um ou mais métodos/ambientes – nos ambientes de origem, intermediário e/ou de destino – e podem continuar iterativamente conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="47ffc-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="47ffc-289">O diagrama só serve para ilustrar alguns dos fluxos de possíveis e não fornece uma enumeração completa.</span><span class="sxs-lookup"><span data-stu-id="47ffc-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Cenários de passo a passo de exemplo do processo de Ciência de Dados][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="47ffc-291">Exemplos de análise avançada em ação</span><span class="sxs-lookup"><span data-stu-id="47ffc-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="47ffc-292">Para obter um passo a passo do Azure Machine Learning que emprega o Processo e Tecnologia de Análise Avançada usando conjuntos de dados públicos, consulte:</span><span class="sxs-lookup"><span data-stu-id="47ffc-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="47ffc-293">[Processo de Ciência de Dados de Equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="47ffc-294">[Processo de Ciência de Dados de Equipe em ação: usando clusters Hadoop do HDInsight](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
