---
title: "aaaHow tooconfigure replicação geográfica para Cache Redis do Azure | Microsoft Docs"
description: "Saiba como tooreplicate seu Cache Redis do Azure instâncias regiões geográficas."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>Como tooconfigure replicação geográfica para Cache Redis do Azure

A Replicação geográfica fornece um mecanismo para vincular duas instâncias de Cache Redis do Azure de camada Premium. Um cache é designado como o cache de vinculado primário hello e hello como cache de vinculado secundário hello. cache de vinculado secundário Olá se torna somente leitura e dados cache primário toohello escrito é replicada toohello cache secundário de vinculado. Essa funcionalidade pode ser usado tooreplicate um cache em regiões do Azure. Este artigo fornece uma tooconfiguring guia replicação geográfica para suas instâncias de Cache Redis do Azure da camada Premium.

## <a name="geo-replication-prerequisites"></a>Pré-requisitos de replicação geográfica

tooconfigure replicação geográfica entre dois caches, Olá pré-requisitos a seguir deve ser atendido:

- Ambos os caches devem ser de [camada Premium](cache-premium-tier-intro.md).
- Ambos os caches devem estar no hello mesma assinatura do Azure.
- cache de vinculado secundário Olá deve ser ou Olá mesmo preço camada ou um preço maior que o cache de vinculado primário hello.
- Se cache primário de vinculado Olá cluster habilitado, o cache de vinculado secundário Olá deve ter de cluster habilitado com hello mesmo número de fragmentos de cache de vinculado primário hello.
- Ambos os caches devem ser criados em um estado de execução.
- A persistência não deve ser habilitada em nenhum dos caches.
- Replicação geográfica entre os caches hello, há suporte para a mesma rede virtual. A replicação geográfica entre os caches diferentes VNETs também é suportada, como Olá dois VNETs são configurados de forma que recursos em VNETs Olá estejam tooreach capaz de uns aos outros por meio de conexões TCP.

Depois de configurar a replicação geográfica, hello seguintes restrições se aplicam tooyour par de cache vinculado:

- cache de vinculado secundário Olá é somente leitura; Você pode lê-lo, mas você não pode gravar qualquer tooit de dados. 
- Todos os dados que estava no cache de vinculado secundário Olá antes da saudação link foi adicionado são removidos. Se hello replicação geográfica é subsequentemente removida no entanto, Olá replicado dados permanecem no cache de vinculado secundário hello.
- Não é possível iniciar um [a operação de dimensionamento](cache-how-to-scale.md) em um cache ou [alterar Olá número de fragmentos](cache-how-to-premium-clustering.md) se cache Olá cluster habilitado.
- Você não pode habilitar a persistência em nenhum dos caches.
- Você pode usar [exportar](cache-how-to-import-export-data.md#export) com o cache, mas você só pode [importação](cache-how-to-import-export-data.md#import) em Olá primário vinculado cache.
- Não é possível excluir o cache vinculado ou grupo de recursos de saudação que os contém, até que você remova o link de replicação geográfica hello. Para obter mais informações, consulte [por que Olá operação falhar quando tentei toodelete meu cache vinculado?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Se dois caches de saudação em regiões diferentes, os custos de egresso de rede aplicará toohello dados replicados entre regiões toohello vinculado o cache secundário. Para obter mais informações, consulte [quanto o custo tooreplicate meus dados entre regiões do Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- Não existe o failover automático toohello secundário vinculado cache se cache primário hello (e sua réplica) ficarem inativos. Em aplicativos de cliente toofailover ordem, você precisaria de link de replicação geográfica do toomanually remover hello e ponto Olá toohello de aplicativos de cliente de cache que anteriormente era o cache Olá secundário vinculado. Para obter mais informações, consulte [como funciona o failover no cache de vinculado secundário toohello?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Adicionar um link de replicação geográfica

1. toolink premium dois caches juntos para replicação geográfica, clique em **georeplicação** menu Olá recursos de cache Olá planejado como Olá primário vinculado de cache e, em seguida, clique em **Adicionar link de replicação de cache**de saudação **georeplicação** folha.

    ![Adicionar Link](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Clique em nome de saudação do cache secundário de Olá desejado de saudação **caches compatíveis** lista. Se seu cache desejado não for exibido na lista de saudação, verifique se esse Olá [pré-requisitos de replicação geográfica](#geo-replication-prerequisites) para Olá desejado cache secundário são atendidos. toofilter Olá caches por região, clique na região desejada Olá no hello mapa toodisplay somente os caches Olá **caches compatíveis** lista.

    ![Caches compatíveis de replicação geográfica](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    Você também pode iniciar Olá vinculação processo ou exibir detalhes sobre cache secundário hello usando o menu de contexto de saudação.

    ![Menu de contexto de replicação geográfica](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Clique em **Link** toolink Olá dois caches juntos e começar o processo de replicação de saudação.

    ![Vincular caches](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. Você pode exibir o progresso de saudação do processo de replicação de saudação em Olá **georeplicação** folha.

    ![Status da vinculação](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    Você também pode exibir hello vinculação status Olá **visão geral** folha para ambos os caches de saudação primários e secundários.

    ![Status do cache](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Após a conclusão do processo de replicação hello, Olá **Link status** muda muito**êxito**.

    ![Status do cache](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Durante a saudação vinculação de processo, Olá cache de vinculado primário permanece disponível para uso mas Olá cache de vinculado secundário não está disponível até que Olá vinculando o processo seja concluído.

## <a name="remove-a-geo-replication-link"></a>Remover um vínculo de replicação geográfica

1. tooremove Olá link entre dois caches e parar a replicação geográfica, clique em **desvincular caches** de saudação **georeplicação** folha.
    
    ![Desvincular caches](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Quando a conclusão do processo de desvinculação Olá, cache secundário hello está disponível para ambas as leituras e gravações.

>[!NOTE]
>Quando o link de replicação geográfica de saudação é removido, Olá dos dados replicados de saudação cache vinculado primário permanece no cache secundário hello.
>
>

## <a name="geo-replication-faq"></a>Perguntas frequentes de replicação geográfica

- [Posso usar a replicação geográfica com um cache de camada Standard ou Basic?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [O cache está disponível para uso durante a vinculação de saudação ou desvincular?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [Posso vincular mais de dois caches juntos?](#can-i-link-more-than-two-caches-together)
- [Posso vincular dois caches de assinaturas do Azure diferentes?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [Posso vincular dois caches com tamanhos diferentes?](#can-i-link-two-caches-with-different-sizes)
- [Posso usar a replicação geográfica com o clustering habilitado?](#can-i-use-geo-replication-with-clustering-enabled)
- [Posso usar a replicação geográfica com meus caches em uma VNET?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [Posso usar o PowerShell ou CLI do Azure toomanage replicação geográfica?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [Quanto custa tooreplicate meus dados entre regiões do Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [Por operação de saudação que falhou quando tentei toodelete meu cache vinculado?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [Qual região devo usar para meu cache vinculado secundário?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [Como funciona o failover no cache de vinculado secundário toohello?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>Posso usar a replicação geográfica com um cache de camada Standard ou Basic?

Não, a replicação geográfica está disponível somente para caches de camada Premium.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>O cache está disponível para uso durante a vinculação de saudação ou desvincular?

- Ao vincular dois caches em conjunto para a replicação geográfica, cache de vinculado primário Olá permanece disponível para uso mas Olá cache de vinculado secundário não está disponível até que Olá vinculando o processo seja concluído.
- Ao remover o link de replicação geográfica de saudação entre dois caches, ambos os caches permanecem disponíveis para uso.

### <a name="can-i-link-more-than-two-caches-together"></a>Posso vincular mais de dois caches juntos?

Não. Ao usar a replicação geográfica, só é possível vincular dois caches juntos.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>Posso vincular dois caches de assinaturas do Azure diferentes?

Não, os dois caches devem estar no hello mesma assinatura do Azure.

### <a name="can-i-link-two-caches-with-different-sizes"></a>Posso vincular dois caches com tamanhos diferentes?

Sim, como Olá secundário vinculado cache é maior que o cache primário de vinculado hello.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>Posso usar a replicação geográfica com o clustering habilitado?

Sim, contanto que os dois caches tem Olá mesmo número de fragmentos.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>Posso usar a replicação geográfica com meus caches em uma VNET?

Sim, há suporte para replicação geográfica de caches em redes virtuais. 

- Replicação geográfica entre os caches hello, há suporte para a mesma rede virtual.
- A replicação geográfica entre os caches diferentes VNETs também é suportada, como Olá dois VNETs são configurados de forma que recursos em VNETs Olá estejam tooreach capaz de uns aos outros por meio de conexões TCP.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>Posso usar o PowerShell ou CLI do Azure toomanage replicação geográfica?

Neste momento, você só pode gerenciar a replicação geográfica usando Olá portal do Azure.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>Quanto custa tooreplicate meus dados entre regiões do Azure?

Ao usar a replicação geográfica, dados do cache de vinculado primário Olá são cache replicado toohello secundário vinculado. Se vinculado Olá dois caches estão em Olá mesma região do Azure, não há nenhum encargo Olá para transferência de dados. Se hello dois vinculado caches estão em diferentes regiões do Azure, hello, taxa de transferência de dados de replicação geográfica é Olá custo de largura de banda de replicação que toohello dados de outra região do Azure. Para obter mais informações, consulte [Detalhes de preço de largura de banda](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>Por operação de saudação que falhou quando tentei toodelete meu cache vinculado?

Quando dois caches são vinculados, você não pode excluir grupo de recursos de cache ou hello que os contém até que você remova o link de replicação geográfica hello. Se você tentar toodelete grupo de recursos de saudação que contém uma ou ambas Olá vinculado caches, hello outros recursos no grupo de recursos de saudação são excluídos, mas o grupo de recursos Olá permanece no hello `deleting` estado e qualquer vinculados caches no grupo de recursos de saudação permanecem no hello `running` estado. a exclusão do grupo de recursos de saudação e hello Olá toocomplete vinculado caches dentro dele, o link de replicação geográfica de saudação quebra conforme descrito em [remover um link de replicação geográfica](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>Qual região devo usar para meu cache vinculado secundário?

Em geral, é recomendável para tooexist seu cache em Olá mesma região do Azure como o aplicativo hello que acessa-lo. Se seu aplicativo tiver uma região primária e uma de fallback, seus caches primário e secundário devem existir nessas mesmas regiões. Para obter mais informações sobre regiões emparelhadas, consulte [Melhores práticas – regiões emparelhadas do Azure](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>Como funciona o failover no cache de vinculado secundário toohello?

Na versão inicial do hello da replicação geográfica, Cache Redis do Azure não oferece suporte a failover automático em regiões do Azure. A replicação geográfica é usada principalmente em um cenário de recuperação de desastre. Em um cenário de recuperação distater, os clientes devem abrir pilha de todo o aplicativo hello em uma região de backup em uma maneira coordenada em vez de permitir que os componentes de aplicativos individuais decidir quando tooswitch tootheir backups por conta própria. Isso é especialmente relevante tooRedis. Um dos principais benefícios de saudação do Redis é um repositório de baixa latência. Se Redis usado por um aplicativo falhar em uma região do Azure diferente tooa mas camada de computação Olá não, Olá adicionado round tempo de viagem teria um impacto significativo no desempenho. Por esse motivo, gostaríamos tooavoid Redis falha em automaticamente devido a problemas de disponibilidade de tootransient.

Atualmente, tooinitiate Olá failover, você precisa tooremove Olá replicação geográfica link no portal do Azure de saudação e, em seguida, alterar o ponto de extremidade de conexão de saudação no cliente Redis de saudação de secundário do hello cache vinculado primário toohello (anteriormente vinculado) cache. Quando Olá dois caches são desassociados, réplica Olá se torna um regular leitura-gravação cache novamente e aceita solicitações diretamente de clientes Redis.


## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre Olá [camada Premium do Azure Redis Cache](cache-premium-tier-intro.md).

