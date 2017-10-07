---
title: "persistência de dados de tooconfigure aaaHow para um Premium do Azure Redis Cache"
description: "Saiba como tooconfigure e gerenciar suas instâncias de Cache Redis do Azure Premium da camada de persistência de dados"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>Como tooconfigure a persistência de dados para um Premium do Azure Redis Cache
Cache Redis do Azure tem diferentes ofertas de cache que fornecem flexibilidade na escolha de saudação do tamanho do cache e recursos, incluindo recursos de camada Premium, como clustering, persistência e suporte de rede virtual. Este artigo descreve como tooconfigure persistência em uma premium do Azure Redis Cache de instância.

Para obter informações sobre outros recursos de cache premium, consulte [camada de Azure Redis Cache Premium Introdução toohello](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>O que é a persistência de dados?
[Persistência de redis](https://redis.io/topics/persistence) permite que dados toopersist armazenados no Redis. Você também pode tirar instantâneos e fazer backup de dados hello, que é possível carregar em caso de falha de hardware. Isso é uma enorme vantagem sobre Basic ou camada padrão, onde todos os Olá dados é armazenada na memória e pode haver perda de dados em caso de falha quando os nós de Cache são para baixo. 

Cache Redis do Azure oferece a persistência de Redis usando Olá modelos a seguir:

* **Persistência RDB** -persistência quando RDB (banco de dados Redis) é configurado, o Cache Redis do Azure persistir um instantâneo de cache do Redis Olá em um formato binário toodisk com base em uma frequência de backup configurável de Redis. Se um desastre ocorrer que desabilita Olá primário e o cache de réplica, cache Olá é reconstruído usando o instantâneo mais recente hello. Saiba mais sobre Olá [vantagens](https://redis.io/topics/persistence#rdb-advantages) e [desvantagens](https://redis.io/topics/persistence#rdb-disadvantages) de persistência RDB.
* **Persistência de AOF** -persistência quando AOF (arquivo somente de acréscimo) estiver configurada, o Cache Redis do Azure salva cada log de tooa de operação de gravação que é salvo pelo menos uma vez por segundo em uma conta de armazenamento do Azure. Se um desastre ocorrer que desabilita Olá primário e o cache de réplica, cache Olá será reconstruída usando operações de gravação da saudação armazenada. Saiba mais sobre Olá [vantagens](https://redis.io/topics/persistence#aof-advantages) e [desvantagens](https://redis.io/topics/persistence#aof-disadvantages) de persistência de AOF.

Persistência é configurada da saudação **novo Cache Redis** folha durante a criação do cache e em Olá **menu recursos** para premium existente armazena em cache.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Depois de selecionar um tipo de preço premium, clique em **Persistência do Redis**.

![Persistência do Redis][redis-cache-persistence]

Olá etapas na próxima seção, Olá descrevem como tooconfigure Redis persistência em seu novo cache premium. Após configurar a persistência do Redis, clique em **criar** toocreate premium seu novo cache com a persistência de Redis.

## <a name="enable-redis-persistence"></a>Habilitar a persistência de Redis

Redis persistência está ativada Olá **Redis a persistência de dados** folha escolhendo um **RDB** ou **AOF** persistência. Para novos caches, esta folha é acessada durante o processo de criação do cache hello, conforme descrito na seção anterior hello. Para caches existentes, Olá **Redis a persistência de dados** folha é acessada de saudação **menu recursos** para seu cache.

![Configurações do Redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>Configurar a persistência de RDB

persistência de RDB tooenable, clique em **RDB**. persistência de RDB toodisable em um cache premium habilitado anteriormente, clique em **desabilitado**.

![Persistência de RDB Redis][redis-cache-rdb-persistence]

tooconfigure Olá intervalo de backup, selecione um **frequência de Backup** da lista suspensa de saudação. As opções incluem **15 minutos**, **30 minutos**, **60 minutos**, **6 horas**, **12 horas** e **24 horas**. Esse intervalo inicia a contagem regressiva após a conclusão bem-sucedida da operação de backup anterior hello e quando ele expira, um novo backup é iniciado.

Clique em **conta de armazenamento** tooselect Olá toouse da conta de armazenamento e escolha qualquer Olá **chave primária** ou **chave secundária** toouse de saudação **armazenamento Chave** lista suspensa. Você deve escolher uma conta de armazenamento no hello mesma região que o cache de Olá e um **armazenamento Premium** conta é recomendada porque o armazenamento premium tem maior taxa de transferência. 

> [!IMPORTANT]
> Se a chave de armazenamento de saudação para sua conta de persistência é regenerada, reconfigure a tecla desejada Olá de saudação **chave de armazenamento** lista suspensa.
> 
> 

Clique em **Okey** toosave configuração de persistência de saudação.

próximo backup Hello (ou primeiro backup para novos caches) é iniciado depois que o intervalo de frequência de backup de saudação expira.

## <a name="configure-aof-persistence"></a>Configurar a persistência de AOF

persistência de AOF tooenable, clique em **AOF**. persistência de AOF toodisable em um cache premium habilitado anteriormente, clique em **desabilitado**.

![Persistência de AOF de Redis][redis-cache-aof-persistence]

persistência de AOF tooconfigure, especifique um **primeira conta de armazenamento**. Esta conta de armazenamento deve estar no hello mesma região que o cache de Olá e um **armazenamento Premium** conta é recomendada porque o armazenamento premium tem maior taxa de transferência. Como opção, você pode configurar uma conta de armazenamento adicional denominada **Segunda Conta de Armazenamento**. Se uma segunda conta de armazenamento é configurada, hello gravações toohello réplica cache são gravados toothis segunda conta de armazenamento. Para cada conta de armazenamento configurado, escolher o hello **chave primária** ou **chave secundária** toouse de saudação **chave de armazenamento** lista suspensa. 

> [!IMPORTANT]
> Se a chave de armazenamento de saudação para sua conta de persistência é regenerada, reconfigure a tecla desejada Olá de saudação **chave de armazenamento** lista suspensa.
> 
> 

Quando a persistência de AOF está habilitada, grave o cache de toohello operações são salvos toohello designado a conta de armazenamento (ou contas, se você tiver configurado uma segunda conta de armazenamento). No evento de saudação de uma falha catastrófica que leva para baixo ambos Olá primário e cache de réplica, hello armazenado AOF log é usado toorebuild cache de saudação.

## <a name="persistence-faq"></a>Perguntas frequentes sobre persistência
Olá lista a seguir contém as respostas toocommonly perguntas frequentes sobre a persistência de Cache Redis do Azure.

* [Posso habilitar a persistência em um cache criado anteriormente?](#can-i-enable-persistence-on-a-previously-created-cache)
* [Posso habilitar persistência AOF e RDB em Olá simultaneamente?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Qual modelo de persistência eu devo escolher?](#which-persistence-model-should-i-choose)
* [O que acontece se eu tiver dimensionado tooa um tamanho diferente e um backup é restaurado que foi feita antes da operação de dimensionamento de Olá?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>Persistência de RDB
* [Pode alterar o frequência de backup Olá RDB depois de criar cache Olá?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Por que quando eu tenho uma frequência de backup de RDB de 60 minutos há mais de 60 minutos entre os backups?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [O que acontece toohello backups RDB antigos, quando um novo backup é feito?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>Persistência de AOF
* [Quando devo usar uma segunda conta de armazenamento?](#when-should-i-use-a-second-storage-account)
* [A persistência de AOF afeta a taxa de transferência, latência ou desempenho de meu cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Como remover a segunda conta de armazenamento Olá?](#how-can-i-remove-the-second-storage-account)
* [O que é uma regravação e como ela afeta meu cache?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [O que devo esperar ao dimensionar um cache com o AOF habilitado?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [Como os dados de AOF são organizados no armazenamento?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>Posso habilitar a persistência em um cache criado anteriormente?
Sim, a persistência do Redis pode ser configurada na criação do cache e em caches premium existentes.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>Posso habilitar persistência AOF e RDB em Olá simultaneamente?

Não, você pode habilitar apenas RDB ou AOF, mas não ambos ao Olá simultaneamente.

### <a name="which-persistence-model-should-i-choose"></a>Qual modelo de persistência eu devo escolher?

Persistência de AOF salva cada gravação tooa log, que tem algum impacto na taxa de transferência, em comparação com RDB persistência que salva os backups com base no hello configurado intervalo de backup, com impacto mínimo no desempenho. Escolha persistência AOF se seu principal objetivo é toominimize perda de dados, e você pode manipular uma diminuição na taxa de transferência para seu cache. Escolha persistência RDB se você deseja que a taxa de transferência ideal toomaintain em seu cache, mas ainda deseja um mecanismo de recuperação de dados.

* Saiba mais sobre Olá [vantagens](https://redis.io/topics/persistence#rdb-advantages) e [desvantagens](https://redis.io/topics/persistence#rdb-disadvantages) de persistência RDB.
* Saiba mais sobre Olá [vantagens](https://redis.io/topics/persistence#aof-advantages) e [desvantagens](https://redis.io/topics/persistence#aof-disadvantages) de persistência de AOF.

Para saber mais sobre o desempenho ao usar a persistência de AOF, veja [A persistência de AOF afeta a taxa de transferência, latência ou desempenho de meu cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>O que acontece se eu tiver dimensionado tooa um tamanho diferente e um backup é restaurado que foi feita antes da operação de dimensionamento de Olá?

Para a persistência de RDB e AOF:

* Se você tiver dimensionado tooa maior tamanho, não há nenhum impacto.
* Se tiver dimensionado tooa menor e você tem um personalizado [bancos de dados](cache-configure.md#databases) configuração é maior do que Olá [limite de bancos de dados](cache-configure.md#databases) para o novo tamanho, os dados nesses bancos de dados não for restaurados. Para obter mais informações, consulte [A configuração dos meus bancos de dados personalizados é afetada durante o dimensionamento?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Se tiver dimensionado tooa menor e não há espaço suficiente no hello menor tamanho toohold todos os dados de saudação de chaves de backup, última Olá serão removidos durante o processo de restauração hello, normalmente usando Olá [allkeys lru](http://redis.io/topics/lru-cache) remoção diretiva.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>Pode alterar o frequência de backup Olá RDB depois de criar cache Olá?
Sim, você pode alterar a frequência de backup de saudação de persistência RDB Olá **Redis a persistência de dados** folha. Para obter instruções, consulte [Configurar persistência do Redis](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Por que quando eu tenho uma frequência de backup de RDB de 60 minutos há mais de 60 minutos entre os backups?
intervalo de frequência de backup de persistência de RDB saudação não inicia até que o processo de backup anterior Olá foi concluída com êxito. Se frequência de backup Olá é 60 minutos e leva um toosuccessfully de 15 minutos do processo de backup completo, o próximo backup de saudação não iniciará até 75 minutos após Olá hora de início do backup anterior de saudação.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>O que acontece toohello backups RDB antigos, quando um novo backup é feito?
Todos os backups de persistência RDB exceto hello mais recente são excluídos automaticamente. Essa exclusão pode não acontecer imediatamente, mas os backups mais antigos não são persistidos por tempo indeterminado.


### <a name="when-should-i-use-a-second-storage-account"></a>Quando devo usar uma segunda conta de armazenamento?

Você deve usar uma segunda conta de armazenamento para a persistência de AOF quando você acreditar que você tem maior do que as operações de conjunto esperado no cache de saudação.  Configurar conta de armazenamento secundário Olá ajuda a garantir que o cache não atinja os limites de largura de banda de armazenamento.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>A persistência de AOF afeta a taxa de transferência, latência ou desempenho de meu cache?

Persistência AOF afeta a taxa de transferência por aproximadamente 15 a 20% ao cache hello está abaixo de carga máxima (CPU e carga do servidor ambos em 90%). Não deve haver problemas de latência quando cache Olá estiver dentro desses limites. No entanto, o cache de saudação alcançará esses limites mais cedo com AOF habilitado.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Como remover a segunda conta de armazenamento Olá?

Você pode remover a conta de armazenamento secundário Olá AOF persistência definindo a conta de armazenamento segundo Olá toobe Olá mesmo como conta de armazenamento primeiro hello. Para obter instruções, veja [Configurar a persistência de AOF](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>O que é uma regravação e como ela afeta meu cache?

Quando o arquivo AOF Olá se torna grande o suficiente, uma reescrita é automaticamente em fila em cache hello. Olá reconfiguração redimensiona Olá AOF arquivo com o conjunto mínimo de saudação operações necessárias toocreate Olá atual do conjunto de dados. Durante a recriação, espere tooreach limites de desempenho mais cedo, especialmente ao lidar com grandes conjuntos de dados. Regravações menor ocorrerem com frequência como arquivo AOF Olá fica maior, mas terá uma quantidade significativa de tempo quando isso acontece.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>O que devo esperar ao dimensionar um cache com o AOF habilitado?

Se o arquivo AOF Olá no tempo de saudação do dimensionamento é muito grande, em seguida, espere hello mais do que o esperado, pois será ele ser recarregar arquivo hello após dimensionamento de tootake de operação de escala.

Para obter mais informações sobre dimensionamento, consulte [o que acontece se eu tiver dimensionado tooa um tamanho diferente e um backup é restaurado que foi feita antes da operação de dimensionamento de Olá?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>Como os dados de AOF são organizados no armazenamento?

Dados armazenados em arquivos AOF são divididos em vários blobs de página por desempenho tooincrease de salvar Olá dados toostorage. Olá seguinte tabela exibe quantos blobs de página são usados para cada tipo de preço:

| Camada premium | Blobs |
|--------------|-------|
| P1           | 4 por fragmento    |
| P2           | 8 por fragmento    |
| P3           | 16 por fragmento   |
| P4           | 20 por fragmento   |

Quando o cluster estiver habilitado, cada fragmento no cache de saudação tem seu próprio conjunto de blobs de página, conforme indicado na tabela anterior hello. Por exemplo, um cache de P2 com três fragmentos distribui seu arquivo AOF em 24 blobs de páginas (oito blobs por fragmento, com três fragmentos).

Após uma regeneração, dois conjuntos de arquivos AOF existirão no armazenamento. Regravações ocorrem no plano de fundo hello e acrescente toohello primeiro conjunto de arquivos, enquanto as operações de conjunto que são enviadas toohello cache durante a regravação da saudação acrescentam toohello segundo conjunto. Um backup é armazenado temporariamente durante regenerações no caso de falha, mas é excluída imediatamente após a conclusão de uma regeneração.


## <a name="next-steps"></a>Próximas etapas
Saiba como toouse premium mais recursos de cache.

* [Camada de Azure Redis Cache Premium toohello Introdução](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
