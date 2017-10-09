---
title: Notas de aaaRelease do Gateway de gerenciamento de dados | Microsoft Docs
description: "Notas de versão do Gateway de Gerenciamento de Dados"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="9b9d2-103">Notas de versão para o Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="9b9d2-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="9b9d2-104">Um dos desafios Olá para integração de dados modernos é toomove dados tooand de toocloud local.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="9b9d2-105">Fábrica de dados torna essa integração com o Gateway de gerenciamento de dados, que é um agente que você pode instalar o movimento de dados local tooenable híbrida.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="9b9d2-106">Consulte Olá seguintes artigos para obter informações detalhadas sobre o Gateway de gerenciamento de dados e como toouse-lo:</span><span class="sxs-lookup"><span data-stu-id="9b9d2-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="9b9d2-107">Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="9b9d2-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="9b9d2-108">Mover dados entre o local e a nuvem usando a Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="9b9d2-109">VERSÃO ATUAL (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="9b9d2-110">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="9b9d2-110">Enhancements-</span></span>
- <span data-ttu-id="9b9d2-111">Você pode adicionar o barramento de serviço do DNS entradas toowhitelist em vez de lista branca de todos os endereços IP do Azure do seu firewall (se necessário).</span><span class="sxs-lookup"><span data-stu-id="9b9d2-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="9b9d2-112">Você pode encontrar a entrada DNS respectiva no Portal do Azure (Data Factory -> 'Criar e Implantar' -> 'Gateways' -> "serviceUrls" (no JSON)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="9b9d2-113">Agora, o conector HDFS dá suporte ao certificado público autoassinado, permitindo que você ignore a validação de SSL.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="9b9d2-114">Corrigido: Problema com gateway offline durante a atualização (devido a distorção tooclock)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="9b9d2-115">Versões anteriores</span><span class="sxs-lookup"><span data-stu-id="9b9d2-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="9b9d2-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="9b9d2-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="9b9d2-117">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="9b9d2-117">Enhancements-</span></span>
-   <span data-ttu-id="9b9d2-118">Você pode adicionar entradas DNS toowhitelist barramento de serviço em vez de lista branca de todos os endereços IP do Azure do seu firewall (se necessário).</span><span class="sxs-lookup"><span data-stu-id="9b9d2-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="9b9d2-119">Mais detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-119">More details here.</span></span>
-   <span data-ttu-id="9b9d2-120">Agora você pode copiar dados para/de um blob de bloco único backup too4.75 TB, que é o tamanho de saudação máximo com suporte de blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="9b9d2-121">(o limite anterior era de 195 GB).</span><span class="sxs-lookup"><span data-stu-id="9b9d2-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="9b9d2-122">Correção: problema de memória insuficiente ao descompactar vários arquivos pequenos durante a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="9b9d2-123">Correção: Índice fora do problema de intervalo durante a cópia do banco de dados de documento tooan local do SQL Server com o recurso idempotência.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="9b9d2-124">Correção: o script de limpeza do SQL não funcionava no SQL Server local no Assistente de Cópia.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="9b9d2-125">Correção: Nome da coluna espaço Olá final não funciona na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="9b9d2-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="9b9d2-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="9b9d2-127">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="9b9d2-127">Enhancements-</span></span>
- <span data-ttu-id="9b9d2-128">Correção: problema com credenciais ausentes na reinicialização do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="9b9d2-129">Correção: problema com o registro durante a restauração do gateway usando um arquivo de backup.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="9b9d2-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="9b9d2-131">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="9b9d2-131">Enhancements-</span></span>
- <span data-ttu-id="9b9d2-132">Correção: leitura incorreta do valor nulo Decimal do Oracle como fonte.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="9b9d2-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="9b9d2-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="9b9d2-134">O que há de novo</span><span class="sxs-lookup"><span data-stu-id="9b9d2-134">What’s new</span></span>
- <span data-ttu-id="9b9d2-135">Os clientes podem fornecer comentários sobre a experiência de registro de gateway.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="9b9d2-136">Suporte a um novo formato de compactação: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="9b9d2-137">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="9b9d2-137">Enhancements-</span></span>
- <span data-ttu-id="9b9d2-138">Melhoria de desempenho para o coletor Oracle, fonte HDFS.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="9b9d2-139">Correção de bug para atualização automática do gateway, capacidade de processamento paralelo do gateway.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="9b9d2-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="9b9d2-141">Melhorias</span><span class="sxs-lookup"><span data-stu-id="9b9d2-141">Enhancements</span></span>
- <span data-ttu-id="9b9d2-142">Melhor e mais robusta Gateway registro experiência-agora você pode acompanhar o status do andamento durante o processo de registro de Gateway hello, que torna a experiência de registro hello mais ágil na resposta.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="9b9d2-143">Melhoria no Gateway restaurar processo - você ainda poderá recuperar o gateway mesmo se você não tiver o arquivo de backup Olá gateway com essa atualização.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="9b9d2-144">Isso exigiria tooreset credenciais de serviço vinculado no Portal.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="9b9d2-145">Correção de bug.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="9b9d2-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="9b9d2-147">O que há de novo</span><span class="sxs-lookup"><span data-stu-id="9b9d2-147">What’s new</span></span>

- <span data-ttu-id="9b9d2-148">Agora você pode armazenar credenciais de fonte de dados localmente.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="9b9d2-149">Olá credenciais são criptografadas.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-149">hello credentials are encrypted.</span></span> <span data-ttu-id="9b9d2-150">credenciais de fonte de dados Olá podem ser recuperadas e restaurados usando o arquivo de backup de saudação que pode ser exportado do hello existente Gateway, todos os locais.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="9b9d2-151">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="9b9d2-151">Enhancements-</span></span>

- <span data-ttu-id="9b9d2-152">Experiência de registro de Gateway melhorada e mais robusta.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="9b9d2-153">Suporte a detecção automática da configuração de QuoteChar para formato de texto no Assistente para copiar e melhorar Olá formato geral a precisão da detecção.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="9b9d2-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="9b9d2-154">2.3.6100.2</span></span>

- <span data-ttu-id="9b9d2-155">Suporte à detecção automática de firstRowAsHeader e SkipLineCount no assistente de cópia para arquivos de texto em HDFS e no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="9b9d2-156">Aprimorar a estabilidade de saudação da conexão de rede entre o gateway e o barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="9b9d2-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="9b9d2-157">Algumas correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="9b9d2-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-158">2.2.6072.1</span></span>

*  <span data-ttu-id="9b9d2-159">Oferece suporte ao configurar o proxy HTTP para usar o gateway Olá Olá Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="9b9d2-160">Se configurado, o Blob do Azure, a Tabela do Azure, o Azure Data Lake e o DocumentDB serão acessados por meio do proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="9b9d2-161">Cabeçalho dá suporte ao tratamento de TextFormat ao copiar dados do sistema de arquivos local e HDFS local tooAzure Blob, repositório Azure Data Lake,.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="9b9d2-162">Oferece suporte à cópia de dados de Blob de acréscimo e blobs de página juntamente com hello já suporte para o Blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="9b9d2-163">Apresenta um novo status do gateway **Online (limitado)**, que indica que essa funcionalidade principal de saudação do gateway de saudação funciona exceto o suporte da operação interativa Olá para o Assistente para cópia.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="9b9d2-164">Melhora a robustez de saudação do registro de gateway usando a chave de registro.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="9b9d2-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-165">2.1.6040.</span></span>

*  <span data-ttu-id="9b9d2-166">Driver do DB2 está incluído no pacote de instalação do gateway Olá agora.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="9b9d2-167">Não é necessário tooinstall-lo separadamente.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="9b9d2-168">Driver de DB2 agora dá suporte a z/OS e DB2 para i (AS / 400) junto com hello plataformas já com suporte (Linux, Unix e Windows).</span><span class="sxs-lookup"><span data-stu-id="9b9d2-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="9b9d2-169">Dá suporte ao uso do Azure Cosmos DB como uma origem ou um destino para armazenamentos de dados locais</span><span class="sxs-lookup"><span data-stu-id="9b9d2-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="9b9d2-170">Dá suporte ao copiar o armazenamento de blob do/toocold/hot dados junto com hello já suporte para a conta de armazenamento de uso geral.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="9b9d2-171">Permite que você tooconnect tooon-local do SQL Server por meio do gateway com privilégios de logon remoto.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="9b9d2-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-172">2.0.6013.1</span></span>

*  <span data-ttu-id="9b9d2-173">Você pode selecionar Olá toobe de cultura do idioma usado por um gateway durante a instalação manual.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="9b9d2-174">Quando o gateway não funciona conforme o esperado, você pode escolher toosend logs do gateway de últimos sete dias tooMicrosoft toofacilitate solução do problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="9b9d2-175">Se o gateway não está conectado toohello serviço de nuvem, você pode escolher toosave e arquivar os logs do gateway.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="9b9d2-176">Aprimoramentos na interface do usuário para o gerenciador de configuração de gateway:</span><span class="sxs-lookup"><span data-stu-id="9b9d2-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="9b9d2-177">Verifique o status do gateway mais visível na guia de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="9b9d2-178">Controles reorganizados e simplificados.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="9b9d2-179">Você pode copiar dados de um armazenamento usando Olá [ferramenta de visualização de cópia sem código](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9b9d2-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="9b9d2-180">Confira [Cópia em Etapas](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes gerais sobre esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="9b9d2-181">Você pode usar dados de tooingress de Gateway de gerenciamento de dados diretamente de um banco de dados do SQL Server local no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="9b9d2-182">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-182">Performance improvements</span></span>

    * <span data-ttu-id="9b9d2-183">Melhore o desempenho de exibição de Esquema/Visualização no SQL Server na ferramenta de visualização de cópia sem código.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="9b9d2-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-184">1.12.5953.1</span></span>

*  <span data-ttu-id="9b9d2-185">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="9b9d2-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-186">1.11.5918.1</span></span>

*  <span data-ttu-id="9b9d2-187">Tamanho máximo do log de eventos do gateway Olá foi aumentado de 1 MB too40 MB.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="9b9d2-188">Uma caixa de diálogo de aviso é exibida caso uma reinicialização seja necessária durante a atualização automática do gateway.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="9b9d2-189">Você pode escolher toorestart direita, em seguida, ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="9b9d2-190">Em caso de falha da atualização automática, o instalador do gateway recupera a atualização automática três vezes no máximo.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="9b9d2-191">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-191">Performance improvements</span></span>

    * <span data-ttu-id="9b9d2-192">Melhora no desempenho do carregamento de grandes tabelas de servidor local no cenário de cópia sem código.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="9b9d2-193">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="9b9d2-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-194">1.10.5892.1</span></span>

*  <span data-ttu-id="9b9d2-195">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-195">Performance improvements</span></span>

*  <span data-ttu-id="9b9d2-196">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="9b9d2-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="9b9d2-197">1.9.5865.2</span></span>

*  <span data-ttu-id="9b9d2-198">Capacidade de atualização automática zero touch</span><span class="sxs-lookup"><span data-stu-id="9b9d2-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="9b9d2-199">Novo ícone de bandeja com indicadores de status do gateway</span><span class="sxs-lookup"><span data-stu-id="9b9d2-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="9b9d2-200">Capacidade muito "Atualizar agora" de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="9b9d2-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="9b9d2-201">Hora de agendamento de atualização de tooset de capacidade</span><span class="sxs-lookup"><span data-stu-id="9b9d2-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="9b9d2-202">Script do PowerShell para ativar/desativar a atualização automática</span><span class="sxs-lookup"><span data-stu-id="9b9d2-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="9b9d2-203">Suporte para o formato JSON</span><span class="sxs-lookup"><span data-stu-id="9b9d2-203">Support for JSON format</span></span>  
*  <span data-ttu-id="9b9d2-204">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-204">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-205">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="9b9d2-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-206">1.8.5822.1</span></span>

*  <span data-ttu-id="9b9d2-207">Melhorar a experiência de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="9b9d2-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="9b9d2-208">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-208">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-209">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="9b9d2-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-210">1.7.5795.1</span></span>

*  <span data-ttu-id="9b9d2-211">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-211">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-212">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="9b9d2-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-213">1.7.5764.1</span></span>

*  <span data-ttu-id="9b9d2-214">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-214">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-215">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="9b9d2-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-216">1.6.5735.1</span></span>

*  <span data-ttu-id="9b9d2-217">Suporte à fonte/coletor do HDFS local</span><span class="sxs-lookup"><span data-stu-id="9b9d2-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="9b9d2-218">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-218">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-219">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="9b9d2-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-220">1.6.5696.1</span></span>

*  <span data-ttu-id="9b9d2-221">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-221">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-222">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="9b9d2-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-223">1.6.5676.1</span></span>

*  <span data-ttu-id="9b9d2-224">Suporte a ferramentas de diagnóstico no Gerenciador de Configurações</span><span class="sxs-lookup"><span data-stu-id="9b9d2-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="9b9d2-225">Suporte a colunas de tabela para fontes de dados tabulares do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-226">Suporte a SQL DW para Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-227">Suporte Reclusivo em BlobSource e FileSource para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-228">Suporte a CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy em BlobSink e FileSink com Cópia Binária para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-229">Suporte a relatórios de andamento de Atividade de Cópia do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-230">Suporte a Validação de Conectividade de Fonte de Dados para Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-231">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="9b9d2-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-232">1.6.5672.1</span></span>

*  <span data-ttu-id="9b9d2-233">Suporte a nome de tabela para  fonte de dados ODBC para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-234">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-234">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-235">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="9b9d2-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-236">1.6.5658.1</span></span>

*  <span data-ttu-id="9b9d2-237">Suporte a Coletor de Arquivo para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-238">Suporte à preservação de hierarquia na cópia binária para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-239">Suporte a Idempotência de Atividade de Cópia para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-240">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="9b9d2-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-241">1.6.5640.1</span></span>

*  <span data-ttu-id="9b9d2-242">Suporte a três ou mais fontes de dados para o Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="9b9d2-243">Suporte ao caractere de aspas no analisador de csv para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-244">Suporte à compactação (BZip2)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="9b9d2-245">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="9b9d2-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-246">1.5.5612.1</span></span>

*  <span data-ttu-id="9b9d2-247">Suporte a cinco bancos de dados relacionais do Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata e Sybase)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="9b9d2-248">Suporte à compactação (Gzip e Deflate)</span><span class="sxs-lookup"><span data-stu-id="9b9d2-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="9b9d2-249">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-249">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-250">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="9b9d2-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-251">1.4.5549.1</span></span>

*  <span data-ttu-id="9b9d2-252">Adicionar suporte a fonte de dados Oracle para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9b9d2-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="9b9d2-253">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="9b9d2-253">Performance improvements</span></span>
*  <span data-ttu-id="9b9d2-254">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="9b9d2-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="9b9d2-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-255">1.4.5492.1</span></span>

*  <span data-ttu-id="9b9d2-256">Binário unificado que dá suporte aos serviços Microsoft Azure Data Factory e Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="9b9d2-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="9b9d2-257">Refinar o processo de configuração da interface do usuário e o registro de saudação</span><span class="sxs-lookup"><span data-stu-id="9b9d2-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="9b9d2-258">Azure Data Factory – suporte a Ingresso e Egresso do Azure para fonte de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="9b9d2-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="9b9d2-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="9b9d2-259">1.2.5303.1</span></span>

*  <span data-ttu-id="9b9d2-260">Corrigi toosupport de problema de tempo limite mais demorado conexões de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="9b9d2-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="9b9d2-261">1.1.5526.8</span></span>

*  <span data-ttu-id="9b9d2-262">Requer o .NET Framework 4.5.1 como pré-requisito durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="9b9d2-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="9b9d2-263">1.0.5144.2</span></span>

*  <span data-ttu-id="9b9d2-264">Nenhuma alteração que afeta os cenários do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9b9d2-264">No changes that affect Azure Data Factory scenarios.</span></span>
