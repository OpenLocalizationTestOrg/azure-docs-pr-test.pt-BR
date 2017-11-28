---
title: "Notas de versão do Gateway de Gerenciamento de Dados | Microsoft Docs"
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
ms.openlocfilehash: c052d7e9f757164429ce867201b96305e405dce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="3fdf9-103">Notas de versão para o Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="3fdf9-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="3fdf9-104">Um dos desafios da integração de dados moderna é mover dados entre o local e a nuvem.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-104">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span></span> <span data-ttu-id="3fdf9-105">O Data Factory faz essa integração com o Gateway de Gerenciamento de Dados, que é um agente que você pode instalar localmente para habilitar a movimentação de dados híbridos.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="3fdf9-106">Veja os artigos a seguir para obter informações detalhadas sobre o Gateway de Gerenciamento de Dados e como usá-lo:</span><span class="sxs-lookup"><span data-stu-id="3fdf9-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span>

*  [<span data-ttu-id="3fdf9-107">Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="3fdf9-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="3fdf9-108">Mover dados entre o local e a nuvem usando a Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="3fdf9-109">VERSÃO ATUAL (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="3fdf9-110">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="3fdf9-110">Enhancements-</span></span>
- <span data-ttu-id="3fdf9-111">Adicione as entradas DNS à lista de permissões do barramento de serviço, em vez de colocar na lista de permissões todos os endereços IP do Azure do firewall (se necessário).</span><span class="sxs-lookup"><span data-stu-id="3fdf9-111">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="3fdf9-112">Você pode encontrar a entrada DNS respectiva no Portal do Azure (Data Factory -> 'Criar e Implantar' -> 'Gateways' -> "serviceUrls" (no JSON)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="3fdf9-113">Agora, o conector HDFS dá suporte ao certificado público autoassinado, permitindo que você ignore a validação de SSL.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="3fdf9-114">Corrigido: problema com gateway offline durante a atualização (devido à distorção do relógio)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-114">Fixed: Issue with gateway offline during update (due to clock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="3fdf9-115">Versões anteriores</span><span class="sxs-lookup"><span data-stu-id="3fdf9-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="3fdf9-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="3fdf9-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="3fdf9-117">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="3fdf9-117">Enhancements-</span></span>
-   <span data-ttu-id="3fdf9-118">Adicione as entradas DNS à lista de permissões do Barramento de Serviço, em vez de colocar na lista de permissões todos os endereços IP do Azure do firewall (se necessário).</span><span class="sxs-lookup"><span data-stu-id="3fdf9-118">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="3fdf9-119">Mais detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-119">More details here.</span></span>
-   <span data-ttu-id="3fdf9-120">Agora você pode copiar dados de/para um único blob de blocos de até 4,75 TB, que é o tamanho máximo com suporte no blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-120">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span></span> <span data-ttu-id="3fdf9-121">(o limite anterior era de 195 GB).</span><span class="sxs-lookup"><span data-stu-id="3fdf9-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="3fdf9-122">Correção: problema de memória insuficiente ao descompactar vários arquivos pequenos durante a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="3fdf9-123">Correção: problema de índice fora do intervalo durante a cópia do DocumentDB para o SQL Server local com o recurso de idempotência.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-123">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="3fdf9-124">Correção: o script de limpeza do SQL não funcionava no SQL Server local no Assistente de Cópia.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="3fdf9-125">Correção: um nome de coluna com espaço no final não funcionava na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-125">Fixed: Column name with space at the end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="3fdf9-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="3fdf9-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="3fdf9-127">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="3fdf9-127">Enhancements-</span></span>
- <span data-ttu-id="3fdf9-128">Correção: problema com credenciais ausentes na reinicialização do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="3fdf9-129">Correção: problema com o registro durante a restauração do gateway usando um arquivo de backup.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="3fdf9-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="3fdf9-131">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="3fdf9-131">Enhancements-</span></span>
- <span data-ttu-id="3fdf9-132">Correção: leitura incorreta do valor nulo Decimal do Oracle como fonte.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="3fdf9-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="3fdf9-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="3fdf9-134">O que há de novo</span><span class="sxs-lookup"><span data-stu-id="3fdf9-134">What’s new</span></span>
- <span data-ttu-id="3fdf9-135">Os clientes podem fornecer comentários sobre a experiência de registro de gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="3fdf9-136">Suporte a um novo formato de compactação: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="3fdf9-137">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="3fdf9-137">Enhancements-</span></span>
- <span data-ttu-id="3fdf9-138">Melhoria de desempenho para o coletor Oracle, fonte HDFS.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="3fdf9-139">Correção de bug para atualização automática do gateway, capacidade de processamento paralelo do gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="3fdf9-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="3fdf9-141">Melhorias</span><span class="sxs-lookup"><span data-stu-id="3fdf9-141">Enhancements</span></span>
- <span data-ttu-id="3fdf9-142">Experiência de registro de gateway melhor e mais robusta – agora você pode acompanhar o status do progresso durante o processo de registro de gateway, o que torna a experiência de registro mais dinâmica.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-142">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="3fdf9-143">Melhoria no Processo de Restauração de Gateway – você ainda poderá recuperar o gateway, mesmo que não tenha o arquivo de backup do gateway com essa atualização.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="3fdf9-144">Isso exigiria a redefinição das credenciais de Serviço Vinculado no Portal.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-144">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="3fdf9-145">Correção de bug.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="3fdf9-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="3fdf9-147">O que há de novo</span><span class="sxs-lookup"><span data-stu-id="3fdf9-147">What’s new</span></span>

- <span data-ttu-id="3fdf9-148">Agora você pode armazenar credenciais de fonte de dados localmente.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="3fdf9-149">As credenciais são criptografadas.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-149">The credentials are encrypted.</span></span> <span data-ttu-id="3fdf9-150">As credenciais da fonte de dados podem ser recuperadas e restauradas usando o arquivo de backup que pode ser exportado do Gateway existente, tudo localmente.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-150">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="3fdf9-151">Melhorias-</span><span class="sxs-lookup"><span data-stu-id="3fdf9-151">Enhancements-</span></span>

- <span data-ttu-id="3fdf9-152">Experiência de registro de Gateway melhorada e mais robusta.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="3fdf9-153">Suporte à detecção automática da configuração de QuoteChar para formato de Texto no assistente de cópia e melhoria da precisão de detecção do formato geral.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="3fdf9-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="3fdf9-154">2.3.6100.2</span></span>

- <span data-ttu-id="3fdf9-155">Suporte à detecção automática de firstRowAsHeader e SkipLineCount no assistente de cópia para arquivos de texto em HDFS e no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="3fdf9-156">Melhoria da estabilidade da conexão de rede entre o gateway e o Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="3fdf9-156">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="3fdf9-157">Algumas correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="3fdf9-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-158">2.2.6072.1</span></span>

*  <span data-ttu-id="3fdf9-159">Permite a configuração do proxy HTTP para o gateway usando o Gerenciador de Configurações do Gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-159">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="3fdf9-160">Se configurado, o Blob do Azure, a Tabela do Azure, o Azure Data Lake e o DocumentDB serão acessados por meio do proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="3fdf9-161">Dá suporte ao tratamento de cabeçalho para TextFormat na cópia de dados dentro e fora do Blob do Azure, Azure Data Lake Store, Sistema de Arquivos Local e HDFS local.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-161">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="3fdf9-162">Dá suporte à cópia de dados do Blob de Acréscimos e Blob de Páginas com o Blob de Blocos já com suporte.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-162">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="3fdf9-163">Introduz um novo status de gateway **Online (Limitado)**, que indica se a funcionalidade principal do gateway funciona, com exceção do suporte à operação interativa do Assistente de Cópia.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-163">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="3fdf9-164">Aprimora a robustez do registro de gateway usando a chave do Registro.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-164">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="3fdf9-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-165">2.1.6040.</span></span>

*  <span data-ttu-id="3fdf9-166">O driver DB2 agora está incluído no pacote de instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-166">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="3fdf9-167">Você não precisa instalá-lo separadamente.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-167">You do not need to install it separately.</span></span>
*  <span data-ttu-id="3fdf9-168">O driver DB2 agora oferece suporte ao z/OS e DB2 para i (AS/400) junto com as plataformas já suportadas (Linux, Unix e Windows).</span><span class="sxs-lookup"><span data-stu-id="3fdf9-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="3fdf9-169">Dá suporte ao uso do Azure Cosmos DB como uma origem ou um destino para armazenamentos de dados locais</span><span class="sxs-lookup"><span data-stu-id="3fdf9-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="3fdf9-170">Dá suporte à cópia dos dados de/para o armazenamento de blobs quente/frio junto com a conta de armazenamento de uso geral já com suporte.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-170">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="3fdf9-171">Permite que você conecte o SQL Server local por meio do gateway com privilégios de logon remoto.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-171">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="3fdf9-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-172">2.0.6013.1</span></span>

*  <span data-ttu-id="3fdf9-173">Você pode selecionar o idioma/cultura a ser usada por um gateway durante a instalação manual.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-173">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="3fdf9-174">Quando o gateway não funcionar conforme o esperado, você poderá optar por enviar logs de gateway dos últimos sete dias à Microsoft para facilitar a solução do problema.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-174">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="3fdf9-175">Se gateway não estiver conectado ao serviço de nuvem, você poderá optar por salvar e arquivar logs de gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-175">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="3fdf9-176">Aprimoramentos na interface do usuário para o gerenciador de configuração de gateway:</span><span class="sxs-lookup"><span data-stu-id="3fdf9-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="3fdf9-177">Torne o status do gateway mais visível na guia Página Inicial.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-177">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="3fdf9-178">Controles reorganizados e simplificados.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="3fdf9-179">Você pode copiar dados de um armazenamento usando a [ferramenta de visualização de cópia sem código](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3fdf9-179">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="3fdf9-180">Confira [Cópia em Etapas](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes gerais sobre esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="3fdf9-181">Você pode aproveitar o Gateway de Gerenciamento de Dados para inserir dados diretamente de um banco de dados SQL Server local no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-181">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="3fdf9-182">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-182">Performance improvements</span></span>

    * <span data-ttu-id="3fdf9-183">Melhore o desempenho de exibição de Esquema/Visualização no SQL Server na ferramenta de visualização de cópia sem código.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="3fdf9-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-184">1.12.5953.1</span></span>

*  <span data-ttu-id="3fdf9-185">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="3fdf9-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-186">1.11.5918.1</span></span>

*  <span data-ttu-id="3fdf9-187">O tamanho máximo do log de eventos do gateway foi aumentado de 1 MB para 40 MB.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-187">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="3fdf9-188">Uma caixa de diálogo de aviso é exibida caso uma reinicialização seja necessária durante a atualização automática do gateway.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="3fdf9-189">Você pode optar por reiniciar logo em seguida ou mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-189">You can choose to restart right then or later.</span></span>

*  <span data-ttu-id="3fdf9-190">Em caso de falha da atualização automática, o instalador do gateway recupera a atualização automática três vezes no máximo.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="3fdf9-191">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-191">Performance improvements</span></span>

    * <span data-ttu-id="3fdf9-192">Melhora no desempenho do carregamento de grandes tabelas de servidor local no cenário de cópia sem código.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="3fdf9-193">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="3fdf9-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-194">1.10.5892.1</span></span>

*  <span data-ttu-id="3fdf9-195">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-195">Performance improvements</span></span>

*  <span data-ttu-id="3fdf9-196">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="3fdf9-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="3fdf9-197">1.9.5865.2</span></span>

*  <span data-ttu-id="3fdf9-198">Capacidade de atualização automática zero touch</span><span class="sxs-lookup"><span data-stu-id="3fdf9-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="3fdf9-199">Novo ícone de bandeja com indicadores de status do gateway</span><span class="sxs-lookup"><span data-stu-id="3fdf9-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="3fdf9-200">Capacidade de "Atualizar agora" do cliente</span><span class="sxs-lookup"><span data-stu-id="3fdf9-200">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="3fdf9-201">Capacidade de definir o horário da agenda de atualização</span><span class="sxs-lookup"><span data-stu-id="3fdf9-201">Ability to set update schedule time</span></span>
*  <span data-ttu-id="3fdf9-202">Script do PowerShell para ativar/desativar a atualização automática</span><span class="sxs-lookup"><span data-stu-id="3fdf9-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="3fdf9-203">Suporte para o formato JSON</span><span class="sxs-lookup"><span data-stu-id="3fdf9-203">Support for JSON format</span></span>  
*  <span data-ttu-id="3fdf9-204">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-204">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-205">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="3fdf9-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-206">1.8.5822.1</span></span>

*  <span data-ttu-id="3fdf9-207">Melhorar a experiência de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="3fdf9-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="3fdf9-208">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-208">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-209">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="3fdf9-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-210">1.7.5795.1</span></span>

*  <span data-ttu-id="3fdf9-211">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-211">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-212">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="3fdf9-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-213">1.7.5764.1</span></span>

*  <span data-ttu-id="3fdf9-214">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-214">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-215">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="3fdf9-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-216">1.6.5735.1</span></span>

*  <span data-ttu-id="3fdf9-217">Suporte à fonte/coletor do HDFS local</span><span class="sxs-lookup"><span data-stu-id="3fdf9-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="3fdf9-218">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-218">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-219">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="3fdf9-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-220">1.6.5696.1</span></span>

*  <span data-ttu-id="3fdf9-221">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-221">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-222">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="3fdf9-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-223">1.6.5676.1</span></span>

*  <span data-ttu-id="3fdf9-224">Suporte a ferramentas de diagnóstico no Gerenciador de Configurações</span><span class="sxs-lookup"><span data-stu-id="3fdf9-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="3fdf9-225">Suporte a colunas de tabela para fontes de dados tabulares do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-226">Suporte a SQL DW para Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-227">Suporte Reclusivo em BlobSource e FileSource para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-228">Suporte a CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy em BlobSink e FileSink com Cópia Binária para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-229">Suporte a relatórios de andamento de Atividade de Cópia do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-230">Suporte a Validação de Conectividade de Fonte de Dados para Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-231">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="3fdf9-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-232">1.6.5672.1</span></span>

*  <span data-ttu-id="3fdf9-233">Suporte a nome de tabela para  fonte de dados ODBC para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-234">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-234">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-235">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="3fdf9-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-236">1.6.5658.1</span></span>

*  <span data-ttu-id="3fdf9-237">Suporte a Coletor de Arquivo para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-238">Suporte à preservação de hierarquia na cópia binária para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-239">Suporte a Idempotência de Atividade de Cópia para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-240">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="3fdf9-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-241">1.6.5640.1</span></span>

*  <span data-ttu-id="3fdf9-242">Suporte a três ou mais fontes de dados para o Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="3fdf9-243">Suporte ao caractere de aspas no analisador de csv para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-244">Suporte à compactação (BZip2)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="3fdf9-245">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="3fdf9-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-246">1.5.5612.1</span></span>

*  <span data-ttu-id="3fdf9-247">Suporte a cinco bancos de dados relacionais do Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata e Sybase)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="3fdf9-248">Suporte à compactação (Gzip e Deflate)</span><span class="sxs-lookup"><span data-stu-id="3fdf9-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="3fdf9-249">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-249">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-250">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="3fdf9-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-251">1.4.5549.1</span></span>

*  <span data-ttu-id="3fdf9-252">Adicionar suporte a fonte de dados Oracle para o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3fdf9-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="3fdf9-253">Aprimoramentos de desempenho</span><span class="sxs-lookup"><span data-stu-id="3fdf9-253">Performance improvements</span></span>
*  <span data-ttu-id="3fdf9-254">Correções de bug</span><span class="sxs-lookup"><span data-stu-id="3fdf9-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="3fdf9-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-255">1.4.5492.1</span></span>

*  <span data-ttu-id="3fdf9-256">Binário unificado que dá suporte aos serviços Microsoft Azure Data Factory e Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="3fdf9-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="3fdf9-257">Refinar a interface do usuário de Configuração e o processo de registro</span><span class="sxs-lookup"><span data-stu-id="3fdf9-257">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="3fdf9-258">Azure Data Factory – suporte a Ingresso e Egresso do Azure para fonte de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="3fdf9-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="3fdf9-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="3fdf9-259">1.2.5303.1</span></span>

*  <span data-ttu-id="3fdf9-260">Correção do problema de tempo limite para dar suporte a conexões de fontes de dados mais demoradas.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-260">Fix timeout issue to support more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="3fdf9-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="3fdf9-261">1.1.5526.8</span></span>

*  <span data-ttu-id="3fdf9-262">Requer o .NET Framework 4.5.1 como pré-requisito durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="3fdf9-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="3fdf9-263">1.0.5144.2</span></span>

*  <span data-ttu-id="3fdf9-264">Nenhuma alteração que afeta os cenários do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3fdf9-264">No changes that affect Azure Data Factory scenarios.</span></span>
