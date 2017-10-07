---
title: aaaHow tooScale Cache Redis do Azure | Microsoft Docs
description: "Saiba como tooscale do Azure Redis Cache instâncias"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>Como tooScale Cache Redis do Azure
Cache Redis do Azure tem diferentes ofertas de cache, que fornecem flexibilidade na escolha de saudação do tamanho do cache e recursos. Depois que um cache é criado, você pode dimensionar tamanho hello e hello preço do cache de saudação se alterarem de requisitos de saudação do seu aplicativo. Este artigo mostra como tooscale seu cache Olá portal do Azure e o uso de ferramentas como o PowerShell do Azure e a CLI do Azure.

## <a name="when-tooscale"></a>Quando tooscale
Você pode usar o hello [monitoramento](cache-how-to-monitor.md) recursos do Cache Redis do Azure toomonitor Olá integridade e desempenho do cache e ajudar a determinar quando tooscale Olá cache. 

Você pode monitorar a seguir Olá métricas toohelp determinar se é necessário tooscale.

* Carga do Servidor Redis
* Uso de Memória
* Largura de Banda de Rede
* Uso da CPU

Se você determinar que o cache não está atendendo aos requisitos do aplicativo, você pode dimensionar tooa cache maior ou menor preço é adequada para seu aplicativo. Para obter mais informações sobre como determinar qual cache toouse de camada de preços, consulte [qual oferta de Cache do Redis e tamanho devo usar](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Dimensionar um cache
tooscale seu cache, [procurar cache toohello](cache-configure.md#configure-redis-cache-settings) em Olá [portal do Azure](https://portal.azure.com) e clique em **escala** de saudação **menu recursos**.

![Escala](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Selecione Olá desejado de preços de saudação **selecione preço** folha e clique em **selecione**.

![Tipo de preço ][redis-cache-pricing-tier-blade]


Você pode dimensionar tooa diferente preços com hello restrições a seguir:

* Não é possível redimensionar de um maior preço camada tooa menor preço.
  * Você não pode ser dimensionada de um **Premium** cache para baixo tooa **padrão** ou um **básica** cache.
  * Você não pode ser dimensionada de um **padrão** cache para baixo tooa **básica** cache.
* Pode ser dimensionada de um **básica** cache tooa **padrão** cache, mas você não pode alterar o tamanho de saudação em Olá simultaneamente. Se você precisar de um tamanho diferente, você pode fazer um tamanho de toohello desejado escala operação subsequente.
* Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache. Deve ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em uma escala subsequentes operação.
* Não é possível redimensionar de um tamanho maior para baixo toohello **C0 (250 MB)** tamanho.
 
Enquanto está dimensionamento do cache de saudação toohello novo preço, uma **Scaling** status é exibido no hello **Redis Cache** folha.

![Dimensionamento][redis-cache-scaling]

Quando o dimensionamento for concluído, o status de Olá muda de **Scaling** muito**executando**.

## <a name="how-tooautomate-a-scaling-operation"></a>Como tooautomate uma operação de dimensionamento
Em adição tooscaling suas instâncias de cache em Olá portal do Azure, você pode dimensionar usando cmdlets do PowerShell, CLI do Azure e usando Olá Microsoft Azure Management bibliotecas (MAML). 

* [Dimensionar usando o PowerShell](#scale-using-powershell)
* [Dimensionar usando a CLI do Azure](#scale-using-azure-cli)
* [Dimensionar usando MAML](#scale-using-maml)

### <a name="scale-using-powershell"></a>Dimensionar usando o PowerShell
Você pode dimensionar suas instâncias de Cache Redis do Azure com o PowerShell usando Olá [conjunto AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet quando hello `Size`, `Sku`, ou `ShardCount` propriedades são modificadas. Olá exemplo a seguir mostra como tooscale um cache nomeado `myCache` tooa 2,5 GB cache. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Para obter mais informações sobre a expansão com o PowerShell, consulte [tooscale um Redis cache usando o Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Dimensionar usando a CLI do Azure
tooscale suas instâncias de Cache Redis do Azure usando a CLI do Azure, chame Olá `azure rediscache set` comando e passe as alterações de configuração de saudação desejada que incluem um novo tamanho, o sku ou o tamanho do cluster, dependendo da saudação desejado a operação de escala.

Para obter mais informações sobre o dimensionamento com CLI do Azure, confira [Alterar as configurações de um Cache Redis existente](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Dimensionar usando MAML
tooscale suas instâncias de Cache Redis do Azure usando Olá [Microsoft Azure Management bibliotecas (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), chamada hello `IRedisOperations.CreateOrUpdate` método e passar no novo tamanho Olá Olá `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Para obter mais informações, consulte Olá [gerenciar Redis Cache usando MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) exemplo.

## <a name="scaling-faq"></a>Perguntas frequentes sobre dimensionamento
Olá lista a seguir contém as respostas toocommonly perguntas frequentes sobre o dimensionamento do Cache Redis do Azure.

* [Posso escalonar para um cache Premium, por meio dele ou nele?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Depois de escalar, é necessário toochange minhas chaves de acesso ou o nome do cache?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Como funciona o dimensionamento?](#how-does-scaling-work)
* [Perderei dados de meu cache durante o dimensionamento?](#will-i-lose-data-from-my-cache-during-scaling)
* [A configuração dos meus bancos de dados personalizados foi afetada durante o dimensionamento?](#is-my-custom-databases-setting-affected-during-scaling)
* [O cache estará disponível durante o dimensionamento?](#will-my-cache-be-available-during-scaling)
* [Operações que não têm suporte](#operations-that-are-not-supported)
* [Quanto tempo o dimensionamento leva?](#how-long-does-scaling-take)
* [Como saber quando o dimensionamento é concluído?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>Posso escalonar para um cache Premium, por meio dele ou nele?
* Você não pode ser dimensionada de um **Premium** cache para baixo tooa **básica** ou **padrão** preço.
* Você pode dimensionar uma **Premium** tooanother da camada de preço do cache.
* Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache. Você deve primeiro ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em um subsequente a operação de dimensionamento.
* Se você habilitou o cluster quando criou sua **Premium** cache, você pode [alterar o tamanho do cluster Olá](cache-how-to-premium-clustering.md#cluster-size). Se o cache foi criado sem clustering habilitado, não é possível configurar o clustering em um momento posterior.
  
  Para obter mais informações, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Depois de escalar, é necessário toochange minhas chaves de acesso ou o nome do cache?
Não, o nome do cache e as chaves permanecem inalterados durante uma operação de dimensionamento.

### <a name="how-does-scaling-work"></a>Como funciona o dimensionamento?
* Quando um **básica** cache for dimensionado tooa de tamanho diferente, ele é desligado e um novo cache é configurado usando o novo tamanho de saudação. Durante esse tempo, cache Olá não está disponível e todos os dados no cache de saudação serão perdidos.
* Quando um **básica** cache for dimensionado tooa **padrão** cache, um cache de réplica é provisionado e Olá dados são copiados do cache de réplica de toohello Olá cache primário. cache Olá permanece disponível durante a saudação dimensionamento de processo.
* Quando um **padrão** cache for dimensionado tooa um tamanho diferente ou tooa **Premium** cache, uma das réplicas de saudação é desligada e provisionado novamente toohello novo tamanho e hello dados transferidos por e, em seguida, Olá outros réplica executará um failover antes que ele seja provisionado novamente, o processo toohello semelhante que ocorre durante uma falha de um de nós de cache de saudação.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Perderei dados de meu cache durante o dimensionamento?
* Quando um **básica** cache é dimensionado tooa novo tamanho, todos os dados é perdido e cache Olá fica indisponível durante a operação de dimensionamento de saudação.
* Quando um **básica** cache for dimensionado tooa **padrão** do cache, hello dados no cache de saudação normalmente sejam preservados.
* Quando um **padrão** cache for dimensionado tooa maior tamanho ou camada, ou um **Premium** cache for dimensionado tooa maior tamanho, todos os dados normalmente é preservado. Ao dimensionar um **padrão** ou **Premium** cache inativo tooa menores, dados pode ser perdida dependendo de quantos dados estão no cache de saudação relacionadas toohello novo tamanho quando ela é dimensionada. Se os dados são perdidos na redução, as chaves são removidas usando Olá [allkeys lru](http://redis.io/topics/lru-cache) política de remoção. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>A configuração dos meus bancos de dados personalizados foi afetada durante o dimensionamento?
Alguns tipos de preço têm diferentes [limites de bancos de dados](cache-configure.md#databases), portanto, há algumas considerações ao dimensionamento se configurado um valor personalizado para Olá `databases` configuração durante a criação do cache.

* Dimensionamento quando tooa preço com baixo `databases` limite da camada atual de saudação de:
  * Se você estiver usando o número padrão de saudação do `databases` que é 16 para todas as camadas de preços, nenhum dado será perdido.
  * Se você estiver usando um número de `databases` que se enquadra dentro dos limites Olá para Olá camada toowhich dimensionará, isso `databases` configuração é mantida e nenhum dado será perdido.
  * Se você estiver usando um número de `databases` que excede os limites de saudação do novo nível de hello, hello `databases` configuração é reduzido toohello limites de nova camada de saudação e todos os dados em bancos de dados Olá removido é perdida.
* Dimensionamento quando tooa preço com hello igual ou superior `databases` limite da camada atual de saudação de seu `databases` configuração é mantida e nenhum dado será perdido.

Observe que, embora os caches Standard e Premium tenham um SLA de 99,9% de disponibilidade, não há SLA para perda de dados.

### <a name="will-my-cache-be-available-during-scaling"></a>O cache estará disponível durante o dimensionamento?
* **Padrão** e **Premium** caches permanecem disponíveis durante a operação de dimensionamento de saudação.
* **Básico** caches estão offline durante a escala de tamanho diferente de tooa de operações, mas permanecem disponíveis quando o dimensionamento de **básica** muito**padrão**.

### <a name="operations-that-are-not-supported"></a>Operações que não têm suporte
* Não é possível redimensionar de um maior preço camada tooa menor preço.
  * Você não pode ser dimensionada de um **Premium** cache para baixo tooa **padrão** ou um **básica** cache.
  * Você não pode ser dimensionada de um **padrão** cache para baixo tooa **básica** cache.
* Pode ser dimensionada de um **básica** cache tooa **padrão** cache, mas você não pode alterar o tamanho de saudação em Olá simultaneamente. Se você precisar de um tamanho diferente, você pode fazer um tamanho de toohello desejado escala operação subsequente.
* Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache. Você deve primeiro ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em um subsequente a operação de dimensionamento.
* Não é possível redimensionar de um tamanho maior para baixo toohello **C0 (250 MB)** tamanho.

Se uma operação de dimensionamento falhar, serviço Olá tentará operação de saudação do toorevert e cache Olá reverterá tamanho original toohello.

### <a name="how-long-does-scaling-take"></a>Quanto tempo o dimensionamento leva?
Dimensionamento leva aproximadamente 20 minutos, dependendo de quantos dados estão no cache de saudação.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Como saber quando o dimensionamento é concluído?
Olá portal do Azure, você verá Olá a operação de dimensionamento em andamento. Quando o dimensionamento for concluído, Olá status das alterações de cache Olá muito**executando**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



