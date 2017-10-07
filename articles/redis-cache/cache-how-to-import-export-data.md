---
title: aaaImport e exportar dados em Cache Redis do Azure | Microsoft Docs
description: "Saiba como tooimport e exportar tooand de dados do armazenamento de blob com suas instâncias de Cache Redis do Azure premium"
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
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Importar e Exportar dados no Cache Redis do Azure
Importação/exportação é uma operação de gerenciamento de dados do Cache Redis do Azure, que permite que você tooimport dados em Cache Redis do Azure ou exportar dados do Cache Redis do Azure importando e exportando um instantâneo de banco de dados de Cache Redis (RDB) de um blob de tooa de cache premium em um Azure Conta de armazenamento. 

- **Exportar** -você pode exportar seu tooa de instantâneos do Azure Redis Cache RDB Blob de páginas.
- **Importação**: você pode importar instantâneos do RDB do Cache Redis de um Blob de Páginas ou de um Blob de Blocos.

Importação/exportação permite toomigrate entre instâncias diferentes do Cache Redis do Azure ou popular Olá cache com os dados antes do uso.

Este artigo fornece um guia de importação e exportação de dados com o Cache Redis do Azure e fornece respostas Olá toocommonly perguntas frequentes.

> [!IMPORTANT]
> Importação/Exportação está em preview e está disponível somente para caches da [camada premium](cache-premium-tier-intro.md) .
>
>

## <a name="import"></a>Importar
Importação pode ser usado toobring Redis compatível RDB arquivos de qualquer servidor Redis em execução em qualquer nuvem ou o ambiente, incluindo o Redis em execução no Linux, Windows ou em qualquer provedor de nuvem como Amazon Web Services e outros. Importação de dados é uma maneira fácil de toocreate um cache com dados preenchidos previamente. Durante o processo de importação hello, Cache Redis do Azure carrega arquivos RDB saudação do armazenamento do Azure na memória e insere chaves Olá cache hello.

> [!NOTE]
> Antes de iniciar a operação de importação Olá, verifique se seu arquivo de banco de dados Redis (RDB) ou os arquivos são carregados na página ou blobs de bloco no armazenamento do Azure, em Olá mesmo região e assinatura como sua instância de Cache Redis do Azure. Para saber mais, consulte [Introdução ao Armazenamento de Blobs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Se você exportou o arquivo RDB usando Olá [exportar do Azure Redis Cache](#export) recurso, o arquivo RDB já esteja armazenado em um blob de página e está pronto para importação.
>
>

1. tooimport um ou mais exportado blobs de cache, [procurar cache tooyour](cache-configure.md#configure-redis-cache-settings) no hello portal do Azure e clique em **importar dados** de saudação **menu recursos**.

    ![Importar dados][cache-import-data]
2. Clique em **Blob(s) escolha** e selecione a conta de armazenamento Olá contém Olá tooimport de dados.

    ![Escolher uma conta de armazenamento][cache-import-choose-storage-account]
3. Clique em contêiner Olá que contém a saudação tooimport de dados.

    ![Escolher um contêiner][cache-import-choose-container]
4. Selecione tooimport de blobs de um ou mais clicando Olá área à esquerda da toohello do nome do blob hello e, em seguida, clique em **selecione**.

    ![Escolha os blobs][cache-import-choose-blobs]
5. Clique em **importar** toobegin processo de importação de saudação.

   > [!IMPORTANT]
   > Olá cache não está acessível pelos clientes de cache durante o processo de importação hello e quaisquer dados existentes no cache de saudação são excluídos.
   >
   >

    ![Importar][cache-import-blobs]

    Você pode monitorar o progresso de saudação da operação de importação de saudação seguintes notificações de saudação do hello portal do Azure, ou exibindo eventos Olá no hello [log de auditoria](../azure-resource-manager/resource-group-audit.md).

    ![Andamento da importação][cache-import-data-import-complete]

## <a name="export"></a>Exportação
Exportação permite que dados de saudação tooexport armazenados em Cache Redis do Azure tooRedis compatível RDB (s). Você pode usar esses dados de toomove do recurso de um Cache Redis do Azure instância tooanother ou servidor do Redis tooanother. Durante o processo de exportação hello, um arquivo temporário é criado no hello VM que hospeda Olá instância de servidor de Cache Redis do Azure e arquivo hello é carregado toohello designado a conta de armazenamento. Quando a operação de exportação Olá for concluído com o status de êxito ou falha, o arquivo temporário de saudação é excluído.

1. tooexport Olá conteúdo atual Olá cache toostorage, [procurar cache tooyour](cache-configure.md#configure-redis-cache-settings) no hello portal do Azure e clique em **exportar dados** de saudação **menu recursos**.

    ![Escolher Contêiner de Armazenamento][cache-export-data-choose-storage-container]
2. Clique em **escolher contêiner de armazenamento** e selecione a conta de armazenamento de saudação desejada. conta de armazenamento Olá deve estar no hello mesma assinatura e região que o cache.

   > [!IMPORTANT]
   > A Importação/Exportação funciona com blobs de páginas, que têm suporte em contas de armazenamento clássicas e do Resource Manager, mas que não têm suporte em [Contas de armazenamento de blobs](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) atualmente.
   >
   >

    ![Conta de armazenamento][cache-export-data-choose-account]
3. Escolha a saudação desejado contêiner de blob e clique em **selecione**. toouse um novo contêiner, clique em **adicionar contêiner** tooadd primeiro e, em seguida, selecione-o na lista de saudação.

    ![Escolher Contêiner de Armazenamento][cache-export-data-container]
4. Digite um **prefixo do nome do Blob** e clique em **exportar** toostart processo de exportação de saudação. prefixo do nome de blob de saudação é usado tooprefix Olá nomes dos arquivos gerados por essa operação de exportação.

    ![Exportação][cache-export-data]

    Você pode monitorar o progresso de saudação da operação de exportação de saudação seguintes notificações de saudação do hello portal do Azure, ou exibindo eventos Olá no hello [log de auditoria](../azure-resource-manager/resource-group-audit.md).

    ![Conclusão da exportação de dados][cache-export-data-export-complete]

    Caches permanecem disponíveis para uso durante o processo de exportação hello.

## <a name="importexport-faq"></a>Perguntas frequentes de Importação/Exportação
Esta seção contém perguntas frequentes sobre o recurso de importação/exportação de saudação.

* [Quais tipos de preço podem usar a Importação/Exportação?](#what-pricing-tiers-can-use-importexport)
* [Posso importar dados de qualquer servidor Redis?](#can-i-import-data-from-any-redis-server)
* [Quais versões do RDB posso importar?](#what-rdb-versions-can-i-import)
* [Meu cache está disponível durante uma operação de Importação/Exportação?](#is-my-cache-available-during-an-importexport-operation)
* [Posso usar a Importação/Exportação com o cluster Redis?](#can-i-use-importexport-with-redis-cluster)
* [Como a Importação/Exportação funciona com uma configuração de bancos de dados personalizada?](#how-does-importexport-work-with-a-custom-databases-setting)
* [De que forma a Importação/Exportação difere da persistência do Redis?](#how-is-importexport-different-from-redis-persistence)
* [Posso automatizar a Importação/Exportação usando o PowerShell, CLI ou outros clientes de gerenciamento?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [Recebi um erro de tempo limite durante minha operação de Importação/Exportação. O que isso significa?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [Recebi um erro ao exportar tooAzure meus dados armazenamento de Blob. O que aconteceu?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>Quais tipos de preço podem usar a Importação/Exportação?
Importação/exportação está disponível apenas no premium Olá preço.

### <a name="can-i-import-data-from-any-redis-server"></a>Posso importar dados de qualquer servidor Redis?
Sim, além de dados tooimporting exportados de instâncias de Cache Redis do Azure, você pode importar arquivos RDB de qualquer servidor Redis em execução em qualquer nuvem ou ambiente, como provedores de nuvem, como o Amazon Web Services, Windows ou Linux. toodo isso, carregamento Olá RDB o arquivo do servidor do Redis Olá desejado em um blob de página ou bloco em uma conta de armazenamento do Azure e então importá-lo em sua instância de Cache Redis do Azure premium. Por exemplo, você pode desejar tooexport dados de saudação do seu cache de produção e importá-lo para um cache usado como parte de um ambiente de preparo para teste ou migração.

> [!IMPORTANT]
> toosuccessfully importe dados exportados de servidores de Redis Cache Redis do Azure diferente de quando usar um blob de página, o tamanho do blob de página Olá deve estar alinhado em um limite de 512 bytes. Para tooperform de código de exemplo as necessárias preenchimento de byte, consulte [upload de blog da página de exemplo](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Quais versões do RDB posso importar?

O Cache Redis do Azure dá suporte à importação de RDB por meio da versão 7 do RDB.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>Meu cache está disponível durante uma operação de Importação/Exportação?
* **Exportar** - Caches permanecem disponíveis e você pode continuar toouse seu cache durante uma operação de exportação.
* **Importar** - Caches ficam indisponíveis quando inicia uma operação de importação e ficam disponíveis para uso quando a conclusão da operação de importação de saudação.

### <a name="can-i-use-importexport-with-redis-cluster"></a>Posso usar a Importação/Exportação com o cluster Redis?
Sim, é possível importar/exportar entre um cache clusterizado e um não clusterizado. Já que o cluster Redis [só dá suporte a banco de dados 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), quaisquer dados em bancos de dados diferentes de 0 não serão importados. Quando os dados de cluster de cache são importados, chaves de saudação são redistribuídas entre fragmentos de saudação do cluster hello.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>Como a Importação/Exportação funciona com uma configuração de bancos de dados personalizada?
Alguns tipos de preço têm diferentes [limites de bancos de dados](cache-configure.md#databases), portanto, há algumas considerações durante a importação se você tiver configurado um valor personalizado para Olá `databases` configuração durante a criação do cache.

* Ao importar o preço com menos de tooa `databases` limite da camada de saudação do qual você exportou de:
  * Se você estiver usando o número padrão de saudação de `databases`, que é 16 para todas as camadas de preços, nenhum dado será perdido.
  * Se você estiver usando um número de `databases` que fica dentro dos limites Olá para Olá camada toowhich que você está importando, nenhum dado será perdido.
  * Se os dados exportados continham dados em um banco de dados que excede os limites de saudação de nova camada de Olá, dados de saudação do superior desses bancos de dados não são importados.

### <a name="how-is-importexport-different-from-redis-persistence"></a>De que forma a Importação/Exportação difere da persistência do Redis?
Persistência de Cache Redis do Azure permite que você toopersist dados armazenados no armazenamento de tooAzure de Redis. Quando a persistência é configurada, Cache Redis do Azure mantém um instantâneo de cache do Redis Olá em um toodisk de formato binário do Redis com base em uma frequência de backup podem ser configurada. Se um desastre ocorrer que desabilita Olá primário e o cache de réplica, dados de cache de saudação são restaurados automaticamente usando o instantâneo mais recente hello. Para obter mais informações, consulte [como tooconfigure a persistência de dados para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md).

Importação / exportação permite que dados toobring ou exporte de Cache Redis do Azure. Ele não configurar o backup e restauração usando a persistência do Redis.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>Posso automatizar a Importação/Exportação usando o PowerShell, CLI ou outros clientes de gerenciamento?
Sim, para o PowerShell obter instruções, consulte [tooimport um cache Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) e [tooexport um cache Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>Recebi um erro de tempo limite durante minha operação de Importação/Exportação. O que isso significa?
Se você permanecer na Olá **importar dados** ou **exportar dados** folha por mais de 15 minutos antes de iniciar a operação de saudação, receberá um erro com um toohello semelhante da mensagem de erro exemplo a seguir:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve isso, inicie a importação hello ou operação de exportação antes de 15 minutos tiver decorrido.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>Recebi um erro ao exportar tooAzure meus dados armazenamento de Blob. O que aconteceu?
A exportação funciona somente com arquivos RDB armazenados como blobs de páginas. Não há suporte para outros tipos de blobs no momento, incluindo contas de armazenamento de blobs com as camadas dinâmicas e estáticas. Para saber mais, confira [Contas de armazenamento de blobs](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Próximas etapas
Saiba como toouse premium mais recursos de cache.

* [Camada de Azure Redis Cache Premium toohello Introdução](cache-premium-tier-intro.md)    

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
