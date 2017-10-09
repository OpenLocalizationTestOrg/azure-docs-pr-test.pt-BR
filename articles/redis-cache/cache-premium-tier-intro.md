---
title: camada do aaaIntroduction toohello Premium do Cache Redis do Azure | Microsoft Docs
description: "Saiba como toocreate e gerenciar persistência Redis, clustering do Redis e suporte de rede virtual para suas instâncias de Cache Redis do Azure Premium da camada"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Camada de Azure Redis Cache Premium toohello Introdução
Cache Redis do Azure é um cache distribuído gerenciado que ajuda você a criar aplicativos altamente dimensionáveis e ágeis fornecendo acesso extremamente rápido tooyour dados. 

Olá que nova camada Premium é uma camada pronta Enterprise, que inclui todos os recursos da camada Standard hello e muito mais, como um melhor desempenho, cargas de trabalho maiores, recuperação de desastres, importação/exportação e segurança aprimorada. Continue lendo toolearn mais sobre os recursos adicionais de saudação da camada de cache Premium Olá.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Melhor desempenho em comparação com tooStandard ou básica
**Melhor desempenho em relação às camadas Standard ou Básica.** Os caches na camada de Premium Olá são implantados no hardware que tem processadores mais rápidos e fornece melhor toohello de desempenho em comparação comparado básica ou a camada padrão. Os Caches da camada Premium têm a taxa de transferência mais alta e as latências mais baixas. 

**Taxa de transferência para Olá mesmo tamanho de Cache é maior no Premium como camada tooStandard comparados.** Por exemplo, taxa de transferência de saudação de um 53 GB P4 cache (Premium) é 250 mil solicitações por segundo de too150K comparados para C6 (padrão).

Para obter mais informações sobre tamanho, taxa de transferência e largura de banda com caches premium, veja [Perguntas frequentes sobre o Cache Redis do Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Persistência de dados do Redis
camada de Premium Olá permite que dados de cache de saudação toopersist em uma conta de armazenamento do Azure. Em um cache Basic/Standard todos os dados de saudação é armazenado somente na memória. Em caso de problemas de infraestrutura subjacente, pode haver uma possível perda de dados. É recomendável usar o recurso de persistência de dados do Redis Olá em Olá Premium camada tooincrease garantir a resiliência contra perda de dados. O Cache Redis do Azure oferece opções de RDB e AOF (em breve) na [persistência do Redis](http://redis.io/topics/persistence). 

Para obter instruções sobre como configurar persistência, consulte [como tooconfigure persistência para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Cluster Redis
Se você deseja toocreate caches maiores que 53 GB ou tooshard dados em vários nós de Redis, você pode usar o Redis cluster que está disponível na camada de Premium Olá. Cada nó consiste em um par de cache primário/de réplica gerenciado pelo Azure para alta disponibilidade. 

**O clustering do Redis fornece uma produtividade e escala máximas.** Taxa de transferência aumenta linearmente conforme você aumenta o número de saudação de fragmentos (nós) no cluster hello. Por exemplo, Se você criar um cluster P4 de 10 fragmentos, taxa de transferência disponível Olá é 250K * 10 = 2,5 milhões de solicitações por segundo. Consulte Olá [perguntas Frequentes de Cache Redis do Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obter mais detalhes sobre o tamanho, a taxa de transferência e a largura de banda com caches premium.

tooget de Introdução ao clustering, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Isolamento e segurança avançados
Caches criados no nível básico ou padrão de Olá estão acessíveis no hello internet pública. Acesso toohello de que cache é restrito com base na chave de acesso de saudação. Com a camada de Premium Olá pode mais garantir que somente os clientes em uma rede especificada podem acessar Olá Cache. É possível implantar o Cache Redis em uma [VNet (Rede Virtual) do Azure](https://azure.microsoft.com/services/virtual-network/). Você pode usar todos os recursos de saudação do VNet, como sub-redes, políticas de controle de acesso e outros recursos toofurther restringem acesso tooRedis.

Para obter mais informações, consulte [como suporte a tooconfigure rede Virtual para um Premium do Azure Redis Cache](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Importar/exportar
Importação/exportação é uma operação de gerenciamento de dados de Cache Redis do Azure que permite que você tooimport dados em Cache Redis do Azure ou exportar dados do Cache Redis do Azure importando e exportando um instantâneo de banco de dados de Cache Redis (RDB) de um blob de páginas de tooa de cache premium em um Azure Conta de armazenamento. Isso permite que você toomigrate entre instâncias diferentes do Cache Redis do Azure ou popular Olá cache com os dados antes do uso.

Importação pode ser usado toobring Redis compatível RDB (s) de qualquer servidor Redis em execução em qualquer nuvem ou o ambiente, incluindo o Redis em execução no Linux, Windows ou em qualquer provedor de nuvem como Amazon Web Services e outros. Importação de dados é uma maneira fácil de toocreate um cache com dados preenchidos previamente. Durante o processo de importação hello, Cache Redis do Azure carrega arquivos RDB saudação do armazenamento do Azure na memória e insere chaves Olá cache hello.

Exportação permite que dados de saudação tooexport armazenados em Cache Redis do Azure tooRedis compatível RDB (s). Você pode usar esses dados de toomove do recurso de um Cache Redis do Azure instância tooanother ou servidor do Redis tooanother. Durante o processo de exportação hello, um arquivo temporário é criado no hello VM que hospeda Olá instância de servidor de Cache Redis do Azure e arquivo hello é carregado toohello designado a conta de armazenamento. Quando a operação de exportação Olá for concluído com o status de êxito ou falha, o arquivo temporário de saudação é excluído.

Para obter mais informações, consulte [como tooimport dados e exportar dados do Cache Redis do Azure](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Reboot
camada de premium Olá permite que você tooreboot um ou mais nós de seu cache sob demanda. Isso permite tootest seu aplicativo para garantir a resiliência no evento de saudação de uma falha. Você pode reinicializar Olá nós a seguir.

* Nó mestre do cache
* Nó subordinado do cache
* Nós mestre e subordinado do cache
* Ao usar um cache premium com clustering, você pode reinicializar Olá mestre, Escravo ou ambos os nós para os fragmentos individuais no cache de saudação

Para obter mais informações, consulte [Reinicializar](cache-administration.md#reboot) e [Perguntas frequentes sobre reinicialização](cache-administration.md#reboot-faq).

>[!NOTE]
>A funcionalidade de reinicialização agora está habilitada para todas as camadas do Cache Redis do Azure.
>
>

## <a name="schedule-updates"></a>Agende atualizações
recurso de atualizações agendadas Olá permite toodesignate uma janela de manutenção para seu cache. Quando a janela de manutenção de saudação for especificada, as atualizações de servidor do Redis são feitas durante essa janela. toodesignate uma janela de manutenção, selecione os dias de saudação desejado e especifique a hora de início de janela de manutenção de saudação para cada dia. Observe que o tempo de janela de manutenção de saudação é em UTC. 

Para obter mais informações, consulte [Agendar atualizações](cache-administration.md#schedule-updates) e [Perguntas frequentes sobre agendamento de atualizações](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Redis somente as atualizações são feitas durante a janela de manutenção agendada de saudação do servidor. janela de manutenção de saudação não se aplica a atualizações de tooAzure ou atualiza o sistema de operacional VM toohello.
> 
> 

## <a name="geo-replication"></a>Replicação geográfica

A **Replicação geográfica** fornece um mecanismo para vincular duas instâncias de Cache Redis do Azure de camada Premium. Um cache é designado como o cache de vinculado primário hello e hello como cache de vinculado secundário hello. cache de vinculado secundário Olá se torna somente leitura e dados cache primário toohello escrito é replicada toohello cache secundário de vinculado. Essa funcionalidade pode ser usado tooreplicate um cache em regiões do Azure.

Para obter mais informações, consulte [como tooconfigure replicação geográfica para Cache Redis do Azure](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>camada do tooscale toohello premium
camada de premium toohello tooscale, basta escolher uma das camadas de premium Olá Olá **alterações de preço** folha. Você também pode dimensionar o cache toohello da camada premium usando o PowerShell e CLI. Para obter instruções passo a passo, consulte [como tooScale Cache Redis do Azure](cache-how-to-scale.md) e [como uma operação de dimensionamento de tooautomate](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Próximas etapas
Criar um cache e explorar os novos recursos de camada premium Olá.

* [Como tooconfigure persistência para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md)
* [Como o suporte a tooconfigure rede Virtual para um Premium do Azure Redis Cache](cache-how-to-premium-vnet.md)
* [Como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md)
* [Como tooimport dados e exportar dados do Cache Redis do Azure](cache-how-to-import-export-data.md)
* [Como tooadminister Cache Redis do Azure](cache-administration.md)

