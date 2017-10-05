---
title: Importar e exportar dados no Cache Redis do Azure | Microsoft Docs
description: "Saiba como importar e exportar dados de e para o armazenamento de blobs com as instâncias do Cache Redis do Azure premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: 5e6d731f0a1cecc1a191c74a45e37a9b94fd98ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="16aff-103">Importar e Exportar dados no Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="16aff-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="16aff-104">A Importação/Exportação é uma operação de gerenciamento de dados do Cache Redis do Azure que permite importar dados no Cache Redis do Azure ou exportar dados dele importando e exportando um instantâneo do RDB (Banco de Dados do Cache Redis) de um cache premium para um blob em uma Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-104">Import/Export is an Azure Redis Cache data management operation, which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="16aff-105">**Exportação**: você pode exportar instantâneos do RDB do Cache Redis do Azure para um Blob de Páginas.</span><span class="sxs-lookup"><span data-stu-id="16aff-105">**Export** - you can export your Azure Redis Cache RDB snapshots to a Page Blob.</span></span>
- <span data-ttu-id="16aff-106">**Importação**: você pode importar instantâneos do RDB do Cache Redis de um Blob de Páginas ou de um Blob de Blocos.</span><span class="sxs-lookup"><span data-stu-id="16aff-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="16aff-107">A Importação/Exportação permite migrar entre diferentes instâncias do Cache Redis do Azure ou popular o cache com os dados antes de usar.</span><span class="sxs-lookup"><span data-stu-id="16aff-107">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="16aff-108">Este artigo fornece um guia para importar e exportar dados com o Cache Redis do Azure, além de respostas para as perguntas mais frequentes.</span><span class="sxs-lookup"><span data-stu-id="16aff-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides the answers to commonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16aff-109">Importação/Exportação está em preview e está disponível somente para caches da [camada premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="16aff-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="16aff-110">Importar</span><span class="sxs-lookup"><span data-stu-id="16aff-110">Import</span></span>
<span data-ttu-id="16aff-111">A importação pode ser usada para trazer arquivos RDB compatíveis com o Redis de qualquer servidor Redis em execução em qualquer nuvem ou ambiente, incluindo o Redis em execução no Linux, Windows ou qualquer provedor de nuvem como Amazon Web Services e similares.</span><span class="sxs-lookup"><span data-stu-id="16aff-111">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="16aff-112">Importar os dados é uma maneira fácil de criar um cache com dados previamente populados.</span><span class="sxs-lookup"><span data-stu-id="16aff-112">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="16aff-113">Durante o processo de importação, o Cache Redis do Azure carrega os arquivos RDB do armazenamento do Azure para a memória e insere as chaves no cache.</span><span class="sxs-lookup"><span data-stu-id="16aff-113">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="16aff-114">Antes de iniciar a operação de importação, verifique se o upload dos arquivos RDB (Banco de Dados Redis) foi feito em blobs de páginas ou de blocos no armazenamento do Azure, na mesma região e assinatura que a instância do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-114">Before beginning the import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in the same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="16aff-115">Para saber mais, consulte [Introdução ao Armazenamento de Blobs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="16aff-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="16aff-116">Se você tiver exportado seu arquivo RDB usando o recurso de [Exportação do Cache Redis do Azure](#export) , seu arquivo RDB já estará armazenado em um blob de páginas, pronto para importação.</span><span class="sxs-lookup"><span data-stu-id="16aff-116">If you exported your RDB file using the [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="16aff-117">Para importar um ou mais blobs de cache exportados, [navegue até seu cache](cache-configure.md#configure-redis-cache-settings) no Portal do Azure e clique em **Importar dados** no menu **Recurso**.</span><span class="sxs-lookup"><span data-stu-id="16aff-117">To import one or more exported cache blobs, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Import data** from the **Resource menu**.</span></span>

    ![Importar dados][cache-import-data]
2. <span data-ttu-id="16aff-119">Clique em **Escolher Blob(s)** e selecione a conta de armazenamento que contém os dados a serem importados.</span><span class="sxs-lookup"><span data-stu-id="16aff-119">Click **Choose Blob(s)** and select the storage account that contains the data to import.</span></span>

    ![Escolher uma conta de armazenamento][cache-import-choose-storage-account]
3. <span data-ttu-id="16aff-121">Clique no contêiner que contém os dados a serem importados.</span><span class="sxs-lookup"><span data-stu-id="16aff-121">Click the container that contains the data to import.</span></span>

    ![Escolher um contêiner][cache-import-choose-container]
4. <span data-ttu-id="16aff-123">Selecione um ou mais blobs para importar clicando na área à esquerda do nome do blob e em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="16aff-123">Select one or more blobs to import by clicking the area to the left of the blob name, and then click **Select**.</span></span>

    ![Escolha os blobs][cache-import-choose-blobs]
5. <span data-ttu-id="16aff-125">Clique em **Importar** para iniciar o processo de importação.</span><span class="sxs-lookup"><span data-stu-id="16aff-125">Click **Import** to begin the import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="16aff-126">O cache não pode ser acessado pelos clientes do cache durante o processo de importação e todos os dados existentes no cache serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="16aff-126">The cache is not accessible by cache clients during the import process, and any existing data in the cache is deleted.</span></span>
   >
   >

    ![Importar][cache-import-blobs]

    <span data-ttu-id="16aff-128">Você pode monitorar o progresso da operação de importação seguindo as notificações do Portal do Azure ou exibindo os eventos no [log de auditoria](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="16aff-128">You can monitor the progress of the import operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Andamento da importação][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="16aff-130">Exportação</span><span class="sxs-lookup"><span data-stu-id="16aff-130">Export</span></span>
<span data-ttu-id="16aff-131">A exportação permite exportar os dados armazenados no Cache Redis do Azure para arquivos RDB compatíveis com Redis.</span><span class="sxs-lookup"><span data-stu-id="16aff-131">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span></span> <span data-ttu-id="16aff-132">Você pode usar esse recurso para mover dados de uma instância do Cache Redis do Azure para outro ou para outro servidor Redis.</span><span class="sxs-lookup"><span data-stu-id="16aff-132">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="16aff-133">Durante o processo de exportação, um arquivo temporário é criado na VM que hospeda a instância de servidor do Cache Redis do Azure e o arquivo é carregado para a conta de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="16aff-133">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="16aff-134">Após a operação de exportação ser concluída com um status de êxito ou de falha, o arquivo temporário é excluído.</span><span class="sxs-lookup"><span data-stu-id="16aff-134">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

1. <span data-ttu-id="16aff-135">Para exportar o conteúdo atual do cache para o armazenamento, [navegue até seu cache](cache-configure.md#configure-redis-cache-settings) no Portal do Azure e clique em **Exportar dados** no menu **Recurso**.</span><span class="sxs-lookup"><span data-stu-id="16aff-135">To export the current contents of the cache to storage, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Export data** from the **Resource menu**.</span></span>

    ![Escolher Contêiner de Armazenamento][cache-export-data-choose-storage-container]
2. <span data-ttu-id="16aff-137">Clique em **Escolher Contêiner de Armazenamento** e selecione a conta de armazenamento desejada.</span><span class="sxs-lookup"><span data-stu-id="16aff-137">Click **Choose Storage Container** and select the desired storage account.</span></span> <span data-ttu-id="16aff-138">A conta de armazenamento deve estar nas mesmas região e assinatura que seu cache.</span><span class="sxs-lookup"><span data-stu-id="16aff-138">The storage account must be in the same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="16aff-139">A Importação/Exportação funciona com blobs de páginas, que têm suporte em contas de armazenamento clássicas e do Resource Manager, mas que não têm suporte em [Contas de armazenamento de blobs](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) atualmente.</span><span class="sxs-lookup"><span data-stu-id="16aff-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Conta de armazenamento][cache-export-data-choose-account]
3. <span data-ttu-id="16aff-141">Escolha o contêiner de blob desejado e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="16aff-141">Choose the desired blob container and click **Select**.</span></span> <span data-ttu-id="16aff-142">Para usar um novo contêiner, clique em **Adicionar Contêiner** para adicioná-lo primeiramente e selecione-o na lista.</span><span class="sxs-lookup"><span data-stu-id="16aff-142">To use new a container, click **Add Container** to add it first and then select it from the list.</span></span>

    ![Escolher Contêiner de Armazenamento][cache-export-data-container]
4. <span data-ttu-id="16aff-144">Digite um **Prefixo do nome de blob** e clique em **Exportar** para iniciar o processo de exportação.</span><span class="sxs-lookup"><span data-stu-id="16aff-144">Type a **Blob name prefix** and click **Export** to start the export process.</span></span> <span data-ttu-id="16aff-145">O prefixo do nome de blob é usado para prefixar os nomes dos arquivos gerados por esta operação de exportação.</span><span class="sxs-lookup"><span data-stu-id="16aff-145">The blob name prefix is used to prefix the names of files generated by this export operation.</span></span>

    ![Exportação][cache-export-data]

    <span data-ttu-id="16aff-147">Você pode monitorar o progresso da operação de exportação seguindo as notificações do Portal do Azure ou exibindo os eventos no [log de auditoria](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="16aff-147">You can monitor the progress of the export operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Conclusão da exportação de dados][cache-export-data-export-complete]

    <span data-ttu-id="16aff-149">Os caches permanecem disponíveis para uso durante o processo de exportação.</span><span class="sxs-lookup"><span data-stu-id="16aff-149">Caches remain available for use during the export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="16aff-150">Perguntas frequentes de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="16aff-150">Import/Export FAQ</span></span>
<span data-ttu-id="16aff-151">Esta seção contém perguntas frequentes sobre o recurso de Importação/Exportação.</span><span class="sxs-lookup"><span data-stu-id="16aff-151">This section contains frequently asked questions about the Import/Export feature.</span></span>

* [<span data-ttu-id="16aff-152">Quais tipos de preço podem usar a Importação/Exportação?</span><span class="sxs-lookup"><span data-stu-id="16aff-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="16aff-153">Posso importar dados de qualquer servidor Redis?</span><span class="sxs-lookup"><span data-stu-id="16aff-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="16aff-154">Quais versões do RDB posso importar?</span><span class="sxs-lookup"><span data-stu-id="16aff-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="16aff-155">Meu cache está disponível durante uma operação de Importação/Exportação?</span><span class="sxs-lookup"><span data-stu-id="16aff-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="16aff-156">Posso usar a Importação/Exportação com o cluster Redis?</span><span class="sxs-lookup"><span data-stu-id="16aff-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="16aff-157">Como a Importação/Exportação funciona com uma configuração de bancos de dados personalizada?</span><span class="sxs-lookup"><span data-stu-id="16aff-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="16aff-158">De que forma a Importação/Exportação difere da persistência do Redis?</span><span class="sxs-lookup"><span data-stu-id="16aff-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="16aff-159">Posso automatizar a Importação/Exportação usando o PowerShell, CLI ou outros clientes de gerenciamento?</span><span class="sxs-lookup"><span data-stu-id="16aff-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="16aff-160">Recebi um erro de tempo limite durante minha operação de Importação/Exportação. O que isso significa?</span><span class="sxs-lookup"><span data-stu-id="16aff-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="16aff-161">Recebi um erro ao exportar meus dados para o Armazenamento de Blobs do Azure. O que aconteceu?</span><span class="sxs-lookup"><span data-stu-id="16aff-161">I got an error when exporting my data to Azure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="16aff-162">Quais tipos de preço podem usar a Importação/Exportação?</span><span class="sxs-lookup"><span data-stu-id="16aff-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="16aff-163">A Importação/Exportação está disponível apenas no tipo de preço premium.</span><span class="sxs-lookup"><span data-stu-id="16aff-163">Import/Export is available only in the premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="16aff-164">Posso importar dados de qualquer servidor Redis?</span><span class="sxs-lookup"><span data-stu-id="16aff-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="16aff-165">Sim, além de importar os dados exportados de instâncias de Cache Redis do Azure, você pode importar arquivos RDB de qualquer servidor Redis em execução em qualquer nuvem ou ambiente, como o Linux, Windows ou provedores de nuvem como o Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="16aff-165">Yes, in addition to importing data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="16aff-166">Para fazer isso, carregue o arquivo RDB do servidor Redis desejado em um blob de páginas ou de blocos em uma Conta de Armazenamento do Azure e importe-o para sua instância premium de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-166">To do this, upload the RDB file from the desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="16aff-167">Por exemplo, convém exportar os dados do cache de produção e importá-los para um cache usado como parte de um ambiente de preparo para testes ou migração.</span><span class="sxs-lookup"><span data-stu-id="16aff-167">For example, you may want to export the data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16aff-168">Para importar com êxito os dados exportados de servidores Redis, outros que não o Cache Redis do Azure ao usar um blob de páginas, o tamanho do blob de páginas deve ser alinhado com um limite de 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="16aff-168">To successfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, the page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="16aff-169">Para obter o código de exemplo a fim de executar o preenchimento de bytes necessários, confira [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload) (Exemplo de upload do blob de páginas).</span><span class="sxs-lookup"><span data-stu-id="16aff-169">For sample code to perform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="16aff-170">Quais versões do RDB posso importar?</span><span class="sxs-lookup"><span data-stu-id="16aff-170">What RDB versions can I import?</span></span>

<span data-ttu-id="16aff-171">O Cache Redis do Azure dá suporte à importação de RDB por meio da versão 7 do RDB.</span><span class="sxs-lookup"><span data-stu-id="16aff-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="16aff-172">Meu cache está disponível durante uma operação de Importação/Exportação?</span><span class="sxs-lookup"><span data-stu-id="16aff-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="16aff-173">**Exportação** - Os caches permanecem disponíveis e você pode continuar a usá-los durante uma operação de exportação.</span><span class="sxs-lookup"><span data-stu-id="16aff-173">**Export** - Caches remain available and you can continue to use your cache during an export operation.</span></span>
* <span data-ttu-id="16aff-174">**Importação** - Os caches ficam indisponíveis quando uma operação de importação é iniciada e ficam disponíveis para uso após ela ser concluída.</span><span class="sxs-lookup"><span data-stu-id="16aff-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when the import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="16aff-175">Posso usar a Importação/Exportação com o cluster Redis?</span><span class="sxs-lookup"><span data-stu-id="16aff-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="16aff-176">Sim, é possível importar/exportar entre um cache clusterizado e um não clusterizado.</span><span class="sxs-lookup"><span data-stu-id="16aff-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="16aff-177">Já que o cluster Redis [só dá suporte a banco de dados 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), quaisquer dados em bancos de dados diferentes de 0 não serão importados.</span><span class="sxs-lookup"><span data-stu-id="16aff-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="16aff-178">Quando os dados do cache clusterizados são importados, as chaves são redistribuídas entre os fragmentos do cluster.</span><span class="sxs-lookup"><span data-stu-id="16aff-178">When clustered cache data is imported, the keys are redistributed among the shards of the cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="16aff-179">Como a Importação/Exportação funciona com uma configuração de bancos de dados personalizada?</span><span class="sxs-lookup"><span data-stu-id="16aff-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="16aff-180">Alguns tipos de preço têm diferentes [limites de bancos de dados](cache-configure.md#databases), portanto, haverá algumas considerações a fazer ao importar se você tiver configurado um valor personalizado para a configuração `databases` durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="16aff-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="16aff-181">Ao importar para um tipo de preço com um limite de `databases` menor do que o tipo do qual você exportou:</span><span class="sxs-lookup"><span data-stu-id="16aff-181">When importing to a pricing tier with a lower `databases` limit than the tier from which you exported:</span></span>
  * <span data-ttu-id="16aff-182">Se você estiver usando o número padrão de `databases`, que é 16 para todos os tipos de preço, nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="16aff-182">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="16aff-183">Se você estiver usando um número personalizado de `databases` que se encaixar dentro dos limites para o tipo para o qual você está importando, nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="16aff-183">If you are using a custom number of `databases` that falls within the limits for the tier to which you are importing, no data is lost.</span></span>
  * <span data-ttu-id="16aff-184">Se os dados exportados continham dados em um banco de dados que excede os limites do novo tipo, os dados de um desses bancos de dados mais altos não serão importados.</span><span class="sxs-lookup"><span data-stu-id="16aff-184">If your exported data contained data in a database that exceeds the limits of the new tier, the data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="16aff-185">De que forma a Importação/Exportação difere da persistência do Redis?</span><span class="sxs-lookup"><span data-stu-id="16aff-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="16aff-186">A persistência do Cache Redis do Azure possibilita a persistência dos dados armazenados no Redis para o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-186">Azure Redis Cache persistence allows you to persist data stored in Redis to Azure Storage.</span></span> <span data-ttu-id="16aff-187">Quando a persistência é configurada, o Cache Redis do Azure persiste um instantâneo do cache Redis em um formato binário do Redis em disco com base em uma frequência de backup configurável.</span><span class="sxs-lookup"><span data-stu-id="16aff-187">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="16aff-188">Se ocorrer um desastre que desabilite os caches primário e de réplica, os dados do cache serão restaurados automaticamente usando o instantâneo mais recente.</span><span class="sxs-lookup"><span data-stu-id="16aff-188">If a catastrophic event occurs that disables both the primary and replica cache, the cache data is restored automatically using the most recent snapshot.</span></span> <span data-ttu-id="16aff-189">Para obter mais informações, consulte [Como configurar a persistência de dados para um Cache Redis do Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="16aff-189">For more information, see [How to configure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="16aff-190">A Importação/Exportação permite trazer dados ou exportá-los do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-190">Import/ Export allows you to bring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="16aff-191">Ele não configurar o backup e restauração usando a persistência do Redis.</span><span class="sxs-lookup"><span data-stu-id="16aff-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="16aff-192">Posso automatizar a Importação/Exportação usando o PowerShell, CLI ou outros clientes de gerenciamento?</span><span class="sxs-lookup"><span data-stu-id="16aff-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="16aff-193">Sim, para ver as instruções do PowerShell, confira [Para importar um cache Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) e [Para exportar um cache Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="16aff-193">Yes, for PowerShell instructions see [To import a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [To export a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="16aff-194">Recebi um erro de tempo limite durante minha operação de Importação/Exportação.</span><span class="sxs-lookup"><span data-stu-id="16aff-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="16aff-195">O que isso significa?</span><span class="sxs-lookup"><span data-stu-id="16aff-195">What does it mean?</span></span>
<span data-ttu-id="16aff-196">Se você permanecer na folha **Importar dados** ou **Exportar dados** por mais de 15 minutos antes de iniciar a operação, receberá um erro com uma mensagem semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="16aff-196">If you remain on the **Import data** or **Export data** blade for longer than 15 minutes before initiating the operation, you receive an error with an error message similar to the following example:</span></span>

    The request to import data into cache 'contoso55' failed with status 'error' and error 'One of the SAS URIs provided could not be used for the following reason: The SAS token end time (se) must be at least 1 hour from now and the start time (st), if given, must be at least 15 minutes in the past.

<span data-ttu-id="16aff-197">Para resolver esse problema, inicie a operação de importação ou exportação dentro do prazo de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="16aff-197">To resolve this, initiate the import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened"></a><span data-ttu-id="16aff-198">Recebi um erro ao exportar meus dados para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-198">I got an error when exporting my data to Azure Blob Storage.</span></span> <span data-ttu-id="16aff-199">O que aconteceu?</span><span class="sxs-lookup"><span data-stu-id="16aff-199">What happened?</span></span>
<span data-ttu-id="16aff-200">A exportação funciona somente com arquivos RDB armazenados como blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="16aff-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="16aff-201">Não há suporte para outros tipos de blobs no momento, incluindo contas de armazenamento de blobs com as camadas dinâmicas e estáticas.</span><span class="sxs-lookup"><span data-stu-id="16aff-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="16aff-202">Para saber mais, confira [Contas de armazenamento de blobs](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="16aff-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16aff-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16aff-203">Next steps</span></span>
<span data-ttu-id="16aff-204">Aprenda a usar mais recursos de cache premium.</span><span class="sxs-lookup"><span data-stu-id="16aff-204">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="16aff-205">Introdução à camada Premium do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="16aff-205">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
