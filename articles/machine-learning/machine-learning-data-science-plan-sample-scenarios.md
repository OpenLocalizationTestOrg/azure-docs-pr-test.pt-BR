---
title: "aaaIdentify avançado cenários de análise para o aprendizado de máquina do Azure | Microsoft Docs"
description: "Selecione os cenários de saudação apropriados para fazer avançadas de análise preditiva com hello processo de ciência de dados de equipe."
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
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="f7a9c-103">Cenários para análises avançadas no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f7a9c-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="f7a9c-104">Este artigo descreve vários Olá fontes de dados de exemplo e cenários de destino que podem ser tratados pelo Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="f7a9c-105">Olá TDSP fornece uma abordagem sistemática para equipes toocollaborate na criação de aplicativos inteligentes.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="f7a9c-106">Olá apresentadas aqui ilustram opções disponíveis no fluxo de trabalho de processamento de dados de saudação que dependem de características de dados hello, locais de origem e repositórios de destino no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="f7a9c-107">Olá **árvore de decisão** para selecionar os cenários de exemplo hello apropriado para seus dados e o objetivo é apresentada na última seção do hello.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="f7a9c-108">Cada uma das seguintes seções de saudação apresenta um cenário de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="f7a9c-109">Para cada cenário, são listados uma possível ciência de dados ou fluxo de análise avançada e os recursos de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="f7a9c-110">**Para todos os seguintes cenários de saudação, você precisa:**
> </span><span class="sxs-lookup"><span data-stu-id="f7a9c-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="f7a9c-111">[Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="f7a9c-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * <span data-ttu-id="f7a9c-112">
            [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-112">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md)</span></span>
> 
> 

## <span data-ttu-id="f7a9c-113"><a name="smalllocal"></a>Cenário \#1: pequeno toomedium o conjunto de dados tabulares em um local de arquivos</span><span class="sxs-lookup"><span data-stu-id="f7a9c-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Arquivos locais toomedium pequeno][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="f7a9c-115">Recursos adicionais do Azure: nenhum</span><span class="sxs-lookup"><span data-stu-id="f7a9c-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="f7a9c-116">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="f7a9c-117">Carregue um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-117">Upload a dataset.</span></span>
3. <span data-ttu-id="f7a9c-118">Crie um fluxo experimental do Azure Machine Learning começando com os conjuntos de dados carregados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="f7a9c-119"><a name="smalllocalprocess"></a>Cenário \#2: toomedium pequeno conjunto de dados de arquivos locais que exigem processamento</span><span class="sxs-lookup"><span data-stu-id="f7a9c-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Toomedium pequenos arquivos de locais com processamento][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="f7a9c-121">Recursos adicionais do Azure: Máquina Virtual do Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="f7a9c-122">Crie uma Máquina Virtual do Azure que executa o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="f7a9c-123">Carregar o contêiner de armazenamento do Azure de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="f7a9c-124">Pré-processe e limpe dados no IPython Notebook, acessando dados no contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="f7a9c-125">Transforme dados toocleaned, formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="f7a9c-126">Salve os dados transformados nos blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="f7a9c-127">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="f7a9c-128">Ler dados de saudação de blobs do Azure usando Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="f7a9c-129">Crie um fluxo experimental do Azure Machine Learning começando com os conjuntos de dados ingeridos.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="f7a9c-130"><a name="largelocal"></a>Cenário \#3: conjunto de dados grande em arquivos locais, com blobs do Azure como destino</span><span class="sxs-lookup"><span data-stu-id="f7a9c-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Arquivos locais grandes][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="f7a9c-132">Recursos adicionais do Azure: Máquina Virtual do Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="f7a9c-133">Crie uma Máquina Virtual do Azure que executa o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="f7a9c-134">Carregar o contêiner de armazenamento do Azure de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="f7a9c-135">Pré-processe e limpe dados no IPython Notebook, acessando dados nos blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="f7a9c-136">Transforme dados toocleaned, formato de tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="f7a9c-137">Explore dados e crie recursos conforme for necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="f7a9c-138">Extraia um exemplo de dados de pequeno a médio porte.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="f7a9c-139">Salve dados de amostra de saudação em blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="f7a9c-140">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="f7a9c-141">Ler dados de saudação de blobs do Azure usando Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="f7a9c-142">Crie um fluxo experimental do Azure Machine Learning, começando com os conjuntos de dados ingeridos.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="f7a9c-143"><a name="smalllocaltodb"></a>Cenário \#4: toomedium pequeno conjunto de dados de arquivos locais, voltados para o SQL Server em uma máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="f7a9c-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Toomedium pequenos arquivos locais tooSQL banco de dados no Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="f7a9c-145">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="f7a9c-146">Crie uma Máquina Virtual do Azure que executa SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="f7a9c-147">Carregar o contêiner de armazenamento do Azure de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="f7a9c-148">Pré-processe e limpe dados no contêiner de armazenamento do Azure usando o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="f7a9c-149">Transforme dados toocleaned, formato de tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="f7a9c-150">Salvar os arquivos de dados local tooVM (bloco de anotações do IPython está em execução na máquina virtual, unidades locais Consulte tooVM drives).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="f7a9c-151">Carrega dados tooSQL banco de dados Server em execução em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="f7a9c-152">Opção \#1: usar o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="f7a9c-153">Logon tooSQL VM do servidor</span><span class="sxs-lookup"><span data-stu-id="f7a9c-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="f7a9c-154">Execute o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="f7a9c-155">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-155">Create database and target tables.</span></span>
   * <span data-ttu-id="f7a9c-156">Use um em massa de saudação importar dados de saudação do tooload de métodos de arquivos de VM local.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="f7a9c-157">Opção \#2: usar o IPython Notebook – não é aconselhável para conjuntos de dados médios e maiores</span><span class="sxs-lookup"><span data-stu-id="f7a9c-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="f7a9c-158">Use tooaccess de cadeia de caracteres de conexão do ODBC SQL Server na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="f7a9c-159">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-159">Create database and target tables.</span></span>
   * <span data-ttu-id="f7a9c-160">Use um em massa de saudação importar dados de saudação do tooload de métodos de arquivos de VM local.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="f7a9c-161">Explore dados e crie recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-161">Explore data, create features as needed.</span></span> <span data-ttu-id="f7a9c-162">Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="f7a9c-163">Apenas Observe Olá consulta necessária toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="f7a9c-164">Escolha um tamanho de amostra de dados, se necessário e/ou desejado.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="f7a9c-165">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="f7a9c-166">Dados de leitura Olá diretamente do SQL Server usando Olá Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="f7a9c-167">Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="f7a9c-168">Crie um fluxo experimental do Azure Machine Learning, começando com os conjuntos de dados ingeridos.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="f7a9c-169"><a name="largelocaltodb"></a>Cenário \#5: conjunto de dados grande em arquivos locais, com o SQL Server na VM do Azure</span><span class="sxs-lookup"><span data-stu-id="f7a9c-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Locais de arquivos grandes tooSQL banco de dados no Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="f7a9c-171">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="f7a9c-172">Crie uma Máquina Virtual do Azure que executa SQL Server e o servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="f7a9c-173">Carregar o contêiner de armazenamento do Azure de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="f7a9c-174">(Opcional) Pré-processe e limpe os dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="f7a9c-175">a.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-175">a.</span></span>  <span data-ttu-id="f7a9c-176">Pré-processe e limpe dados no IPython Notebook, acessando dados do Azure</span><span class="sxs-lookup"><span data-stu-id="f7a9c-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="f7a9c-177">b.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-177">b.</span></span>  <span data-ttu-id="f7a9c-178">Transforme dados toocleaned, formato de tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="f7a9c-179">c.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-179">c.</span></span>  <span data-ttu-id="f7a9c-180">Salvar os arquivos de dados local tooVM (bloco de anotações do IPython está em execução na máquina virtual, unidades locais Consulte tooVM drives).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="f7a9c-181">Carrega dados tooSQL banco de dados Server em execução em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="f7a9c-182">a.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-182">a.</span></span>  <span data-ttu-id="f7a9c-183">Logon tooSQL VM do servidor.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="f7a9c-184">b.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-184">b.</span></span>  <span data-ttu-id="f7a9c-185">Se os dados já não estiverem salvos, baixe arquivos de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="f7a9c-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="f7a9c-186">c.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-186">c.</span></span>  <span data-ttu-id="f7a9c-187">Execute o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="f7a9c-188">d.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-188">d.</span></span>  <span data-ttu-id="f7a9c-189">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="f7a9c-190">e.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-190">e.</span></span>  <span data-ttu-id="f7a9c-191">Use um em massa de saudação importar dados de saudação do tooload de métodos.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="f7a9c-192">f.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-192">f.</span></span>  <span data-ttu-id="f7a9c-193">Se as junções de tabela são necessárias, crie índices tooexpedite junções.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f7a9c-194">Para carregamento mais rápido de tamanhos de dados grande, é recomendável que você crie tabelas particionadas e importar dados de saudação em paralelo em massa.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="f7a9c-195">Para obter mais informações, consulte [tooSQL de importação de dados paralela Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="f7a9c-196">Explore dados e crie recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-196">Explore data, create features as needed.</span></span> <span data-ttu-id="f7a9c-197">Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="f7a9c-198">Apenas Observe Olá consulta necessária toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="f7a9c-199">Escolha um tamanho de amostra de dados, se necessário e/ou desejado.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="f7a9c-200">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="f7a9c-201">Dados de leitura Olá diretamente do SQL Server usando Olá Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="f7a9c-202">Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="f7a9c-203">Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado</span><span class="sxs-lookup"><span data-stu-id="f7a9c-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="f7a9c-204"><a name="largedbtodb"></a>Cenário \#6: conjunto de dados grande em um banco de dados do SQL Server local, com o SQL Server em uma Máquina Virtual do Azure como destino</span><span class="sxs-lookup"><span data-stu-id="f7a9c-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Grande tooSQL de local de banco de dados SQL banco de dados no Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="f7a9c-206">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="f7a9c-207">Crie uma Máquina Virtual do Azure que executa SQL Server e o servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="f7a9c-208">Use um dos dados de saudação exportar dados de saudação do tooexport de métodos de arquivos de toodump do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f7a9c-209">Se você decidir toomove todos os dados do banco de dados de local de hello, uma alternativa (mais rápido) método toomove Olá banco de dados completo toothe instância do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="f7a9c-210">Ignorar dados de tooexport etapas hello, criar banco de dados e banco de dados de destino do carregamento/importar dados toohello e siga o método alternativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="f7a9c-211">Carregar o contêiner de armazenamento de tooAzure de arquivos de despejo de memória.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="f7a9c-212">Carregar Olá dados tooa de dados SQL Server em execução em uma máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="f7a9c-213">a.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-213">a.</span></span>  <span data-ttu-id="f7a9c-214">Logon toohello VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="f7a9c-215">b.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-215">b.</span></span>  <span data-ttu-id="f7a9c-216">Baixe arquivos de dados de uma pasta de VM local de toohello de contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="f7a9c-217">c.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-217">c.</span></span>  <span data-ttu-id="f7a9c-218">Execute o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="f7a9c-219">d.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-219">d.</span></span>  <span data-ttu-id="f7a9c-220">Crie o banco de dados e as tabelas de destino.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="f7a9c-221">e.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-221">e.</span></span>  <span data-ttu-id="f7a9c-222">Use um em massa de saudação importar dados de saudação do tooload de métodos.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="f7a9c-223">f.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-223">f.</span></span>  <span data-ttu-id="f7a9c-224">Se as junções de tabela são necessárias, crie índices tooexpedite junções.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f7a9c-225">Para carregamento mais rápido de tamanhos de dados grande, crie tabelas particionadas e toobulk importar Olá dados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="f7a9c-226">Para obter mais informações, consulte [tooSQL de importação de dados paralela Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="f7a9c-227">Explore dados e crie recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-227">Explore data, create features as needed.</span></span> <span data-ttu-id="f7a9c-228">Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="f7a9c-229">Apenas Observe Olá consulta necessária toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="f7a9c-230">Escolha um tamanho de amostra de dados, se necessário e/ou desejado.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="f7a9c-231">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="f7a9c-232">Dados de leitura Olá diretamente do SQL Server usando Olá Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="f7a9c-233">Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="f7a9c-234">Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="f7a9c-235">Método alternativo toocopy um banco de dados completo de um tooAzure do SQL Server local banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="f7a9c-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Desanexe o banco de dados local e anexar tooSQL banco de dados no Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="f7a9c-237">Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="f7a9c-238">tooreplicate Olá todo banco de dados SQL na VM do SQL Server, você deve copiar um banco de dados de tooanother de um servidor do local, supondo que esse banco de dados de saudação pode ficar temporariamente offline.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="f7a9c-239">Você pode fazer isso no hello Pesquisador de objetos do SQL Server Management Studio ou usando os comandos de Transact-SQL equivalentes hello.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="f7a9c-240">Desanexe o banco de dados de saudação no local de origem hello.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="f7a9c-241">Para saber mais, veja [Desanexar um banco de dados](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="f7a9c-242">Na janela do Windows Explorer ou Prompt de comando do Windows, a saudação de cópia desanexado arquivo de banco de dados ou arquivos e arquivo de log ou local de destino de toohello de arquivos no hello VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="f7a9c-243">Anexe a instância do SQL Server de destino do hello copiado arquivos toohello.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="f7a9c-244">Para saber mais, veja [Anexar um banco de dados](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="f7a9c-245">[Mover um Banco de Dados utilizando Desanexar e Anexar (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="f7a9c-246"><a name="largedbtohive"></a>Cenário \#7: Big Data em arquivos locais, com um banco de dados Hive em clusters Hadoop do Azure HDInsight como destino</span><span class="sxs-lookup"><span data-stu-id="f7a9c-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Big Data no Hive local de destino][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="f7a9c-248">Recursos adicionais do Azure: cluster Hadoop do Azure HDInsight e Máquina Virtual do Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="f7a9c-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="f7a9c-249">Crie uma Máquina Virtual do Azure que executa o servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="f7a9c-250">Personalize um cluster Hadoop do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="f7a9c-251">(Opcional) Pré-processe e limpe os dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="f7a9c-252">a.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-252">a.</span></span>  <span data-ttu-id="f7a9c-253">Pré-processe e limpe dados no IPython Notebook, acessando dados do Azure</span><span class="sxs-lookup"><span data-stu-id="f7a9c-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="f7a9c-254">b.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-254">b.</span></span>  <span data-ttu-id="f7a9c-255">Transforme dados toocleaned, formato de tabela, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="f7a9c-256">c.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-256">c.</span></span>  <span data-ttu-id="f7a9c-257">Salvar os arquivos de dados local tooVM (bloco de anotações do IPython está em execução na máquina virtual, unidades locais Consulte tooVM drives).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="f7a9c-258">Carregar o contêiner do cluster de Hadoop Olá selecionado na etapa 2 do hello padrão de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="f7a9c-259">Carregar o banco de dados do data tooHive no cluster Hadoop de HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="f7a9c-260">a.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-260">a.</span></span>  <span data-ttu-id="f7a9c-261">Faça logon no toohello o nó principal do cluster de Hadoop Olá</span><span class="sxs-lookup"><span data-stu-id="f7a9c-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="f7a9c-262">b.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-262">b.</span></span>  <span data-ttu-id="f7a9c-263">Abra Olá linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="f7a9c-264">c.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-264">c.</span></span>  <span data-ttu-id="f7a9c-265">Insira o diretório raiz da saudação Hive pelo comando `cd %hive_home%\bin` na linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="f7a9c-266">d.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-266">d.</span></span>  <span data-ttu-id="f7a9c-267">Executar o banco de dados do hello Hive consultas toocreate e tabelas e carregar dados de tabelas de tooHive de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f7a9c-268">Se dados saudação forem grandes, os usuários podem criar tabela de Hive Olá com partições.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="f7a9c-269">Em seguida, os usuários podem usar um `for` loop na saudação de linha de comando do Hadoop em dados de tooload de nó principal Olá Olá Hive tabela particionada por partição.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="f7a9c-270">Explore dados e crie recursos conforme necessário na linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="f7a9c-271">Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="f7a9c-272">Apenas Observe Olá consulta necessária toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="f7a9c-273">a.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-273">a.</span></span>  <span data-ttu-id="f7a9c-274">Faça logon no toohello o nó principal do cluster de Hadoop Olá</span><span class="sxs-lookup"><span data-stu-id="f7a9c-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="f7a9c-275">b.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-275">b.</span></span>  <span data-ttu-id="f7a9c-276">Abra Olá linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="f7a9c-277">c.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-277">c.</span></span>  <span data-ttu-id="f7a9c-278">Insira o diretório raiz da saudação Hive pelo comando `cd %hive_home%\bin` na linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="f7a9c-279">d.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-279">d.</span></span>  <span data-ttu-id="f7a9c-280">Executar consultas de Hive Olá na linha de comando do Hadoop no nó de cabeçalho Olá dos dados de Olá Olá Hadoop cluster tooexplore e criar recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="f7a9c-281">Se necessário e/ou desejado, exemplo hello dados toofit no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="f7a9c-282">Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="f7a9c-283">Ler dados saudação diretamente da saudação `Hive Queries` usando Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="f7a9c-284">Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="f7a9c-285">Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="f7a9c-286"><a name="decisiontree"></a>Árvore de decisão para a seleção do cenário</span><span class="sxs-lookup"><span data-stu-id="f7a9c-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="f7a9c-287">Olá diagrama a seguir resume cenários Olá descritos acima e escolhas processo de análise avançada e tecnologia de saudação feitas que levar tooeach dos cenários de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="f7a9c-288">Observe que podem levar o processamento de dados, exploração, engenharia de recurso e amostragem colocar em um ou mais método/ambiente – na fonte hello, intermediário, e/ou ambientes de destino e podem continuar iterativamente conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="f7a9c-289">diagrama de saudação só serve como uma ilustração de alguns fluxos de possíveis e não fornece uma enumeração completa.</span><span class="sxs-lookup"><span data-stu-id="f7a9c-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Cenários de passo a passo de exemplo do processo de Ciência de Dados][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="f7a9c-291">Exemplos de análise avançada em ação</span><span class="sxs-lookup"><span data-stu-id="f7a9c-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="f7a9c-292">Para orientações de aprendizado de máquina do Azure de ponta a ponta que empregam hello tecnologia e o processo de análise avançada usando conjuntos de dados públicos, consulte:</span><span class="sxs-lookup"><span data-stu-id="f7a9c-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="f7a9c-293">[Processo de Ciência de Dados de Equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="f7a9c-294">[Processo de Ciência de Dados de Equipe em ação: usando clusters Hadoop do HDInsight](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f7a9c-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
