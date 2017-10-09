---
title: "soluções de recuperação de desastres aaaDesign - banco de dados do SQL Azure | Microsoft Docs"
description: "Saiba como toodesign sua solução de nuvem para recuperação de desastres por escolhendo Olá failover direito padrão."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Estratégias de recuperação de desastres para aplicativos que usam o Pool Elástico do banco de dados SQL
Ao longo de anos de saudação aprendemos que os serviços de nuvem não são à prova de falhas e incidentes catastróficos acontecem. Banco de dados SQL fornece vários tooprovide de recursos Olá para continuidade de negócios do seu aplicativo quando esses incidentes ocorrem. [Pools Elásticos](sql-database-elastic-pool.md) e suportam a bancos de dados único Olá mesmo tipo de recursos de recuperação de desastres. Este artigo descreve diversas estratégias de recuperação de desastres para pools elásticos que aproveitam esses recursos de continuidade de negócios do Banco de Dados SQL.

Este artigo usa o saudação padrão de aplicativo SaaS ISV canônico a seguir:

<i>Um aplicativo web baseado em nuvem modernos provisiona um banco de dados do SQL para cada usuário final. Olá ISV tem muitos clientes e, portanto, usa muitos bancos de dados, conhecidos como bancos de dados de locatário. Como bancos de dados de locatário Olá normalmente têm os padrões de atividade imprevisíveis, Olá ISV usa um pool Elástico toomake Olá banco de dados custo muito previsível por longos períodos de tempo. pool Elástico Olá também simplifica o gerenciamento de desempenho de saudação quando houver picos de atividade de usuário hello. Além do aplicativo hello do toohello locatário bancos de dados também usa vários bancos de dados toomanage perfis de usuário, segurança, coletam padrões de uso etc. Disponibilidade de locatários individuais Olá não afeta a disponibilidade do aplicativo hello como todo. No entanto, hello disponibilidade e o desempenho de bancos de dados de gerenciamento é essenciais para a função do aplicativo hello e se bancos de dados de gerenciamento Olá todo o aplicativo hello offline está offline.</i>  

Este artigo discute estratégias de recuperação de desastres que abrangem uma variedade de cenários de custo inicialização confidenciais aplicativos tooones com requisitos rigorosos de disponibilidade.

## <a name="scenario-1-cost-sensitive-startup"></a>Cenário 1. Inicialização econômica
<i>Sou uma startup e dependo muito do custo das coisas.  Desejo toosimplify implantação e gerenciamento de aplicativo hello e tenho um SLA limitado para clientes individuais. Mas aplicativo hello de tooensure como um todo nunca está offline.</i>

requisito de simplicidade de saudação toosatisfy, implantar todos os bancos de dados de locatário em um pool Elástico em Olá região do Azure de sua escolha e implantar bancos de dados de gerenciamento como o único banco de dados replicada geograficamente. Olá para recuperação de desastres de locatários, use a restauração geográfica, que é fornecido sem custo adicional. disponibilidade de saudação tooensure de Olá bancos de dados de gerenciamento, replicar geograficamente-los região tooanother usando um grupo de failover automático (em visualização) (etapa 1). custos contínuos Olá configuração de recuperação de desastres Olá neste cenário é igual toohello o custo total de bancos de dados secundários hello. Essa configuração é ilustrada no próximo diagrama de saudação.

![A figura 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Se ocorrer uma interrupção na região primária hello, Olá toobring de etapas de recuperação online, seu aplicativo são ilustrado pelo diagrama Avançar hello.

* grupo de failover Olá iniciará o failover automático de região de DR de toohello do hello Gerenciamento banco de dados. aplicativo Hello é reconectada automaticamente toohello novas contas de principal e todos os novos e bancos de dados de locatário são criados na região de DR hello. os clientes existentes do Hello veem seus dados temporariamente indisponíveis.
* Criar o pool Elástico Olá com hello mesma configuração de pool original da saudação (2).
* Use a restauração geográfica toocreate cópias de bancos de dados de locatário de saudação (3). Você pode considerar disparo restaurações individuais Olá por conexões de usuário final hello ou usar outro esquema de prioridade específica do aplicativo.


Neste ponto o aplicativo está novamente online na região de DR Olá, mas alguns clientes observem atraso ao acessar seus dados.

![Figura 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Se interrupção Olá temporária, é possível que região primária Olá é recuperado do Azure antes de todas as restaurações de banco de dados de saudação completas na região Olá DR. Nesse caso, orquestra móvel Olá aplicativo back toohello região primária. processo de saudação leva etapas Olá ilustradas no diagrama seguinte hello.

* Cancele todas as solicitações de restauração geográfica pendentes.   
* Região de primária toohello (5) de bancos de dados de gerenciamento Olá o failover. Após a recuperação da região hello, primárias antigo Olá automaticamente tornaram secundários. Agora eles alternam funções novamente. 
* Altere conexão cadeia de caracteres toopoint toohello back principal de região do aplicativo hello. Agora todas as novas contas e bancos de dados de locatário são criados na região primária hello. Alguns clientes existentes verão seus dados como temporariamente indisponíveis.   
* Conjunto de todos os bancos de dados em Olá DR pool somente tooread tooensure que elas não podem ser modificadas na região de DR hello (6). 
* Para cada banco de dados Olá pool DR que foi alterado desde a recuperação hello, renomear ou excluir bancos de dados correspondentes no pool principal da saudação (7) hello. 
* Saudação de cópia atualizada bancos de dados de saudação pool principal de toohello pool da recuperação de desastres (8). 
* Excluir o pool de DR hello (9)

Agora seu aplicativo está online na região primária do hello com todos os locatários bancos de dados disponíveis no pool principal hello.

![A figura 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

chave de saudação **se beneficiar** dessa estratégia é baixo custo em andamento para a redundância de camada de dados. Os backups são obtidos automaticamente pelo Olá serviço de banco de dados SQL com nenhuma reconfiguração de aplicativos e sem nenhum custo adicional.  custo de saudação incorrido somente quando os bancos de dados Elástico Olá são restaurados. Olá **compensação** está completa de recuperação de todos os bancos de dados de locatário Olá leva um tempo significativo. Olá período de tempo depende Olá número total de restauração que você iniciar o hello DR região e o tamanho total da saudação bancos de dados de locatário. Mesmo que você pode priorizar restaurações alguns locatários por outras pessoas, estão competindo por hello todas as outras restaurações iniciadas no hello mesma região como serviço de saudação arbitra e limita toominimize Olá impacto geral nos bancos de dados dos clientes Olá existente. Além disso, recuperação de saudação de bancos de dados de locatário Olá não pode iniciar até que o novo pool Elástico Olá na região de DR Olá é criado.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Cenário 2: Aplicativo maduro com o serviço em camadas
<i>Tenho um aplicativo SaaS evoluído com ofertas de serviço em camadas e diferentes SLAs para clientes de avaliação e para clientes pagantes. Para clientes de avaliação hello, tenho tooreduce Olá custo tanto quanto possível. Clientes de teste podem levar um tempo de inatividade, mas quero tooreduce sua probabilidade. Para os clientes pagantes de Olá, nenhum tempo de inatividade é um risco de voo. Forma desejada toomake se clientes pagantes estão sempre tooaccess capaz de seus dados.</i> 

toosupport neste cenário, separado Olá locatários de avaliação de paga locatários colocando-os em pools Elásticos separados. os clientes de avaliação do Hello têm inferior eDTU por locatário e SLA inferior com um tempo de recuperação. clientes que pagam Olá estão em um pool com maior eDTU por locatário e um SLA mais alto. tempo de recuperação mais baixo saudação de tooguarantee, bancos de dados dos clientes pagantes Olá locatário são replicadas geograficamente. Essa configuração é ilustrada no próximo diagrama de saudação. 

![Figura 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Como o primeiro cenário de hello, bancos de dados de gerenciamento de saudação são muito ativos para usar um banco de dados único replicado geograficamente para (1). Isso garante um desempenho previsível Olá para novas assinaturas de clientes, atualizações de perfil e outras operações de gerenciamento. região na qual residem primários da saudação de bancos de dados de gerenciamento Olá Hello é região primária hello e Olá no qual residem secundários Olá de bancos de dados de gerenciamento Olá Olá DR a região é.

Olá locatário bancos de dados clientes pagantes têm bancos de dados ativos em hello "pago" pool provisionado na região primária hello. Provisione um pool secundário com hello mesmo nome na região Olá DR. Cada locatário é replicado geograficamente toohello secundário pool (2). Isso permite a recuperação rápida de todos os bancos de dados do locatário usando o failover. 

Se ocorrer uma interrupção na região primária hello, Olá toobring de etapas de recuperação online, seu aplicativo são ilustradas no diagrama de Avançar hello:

![Figura 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Failover imediatamente região Olá gerenciamento bancos de dados toohello DR (3).
* Altere conexão cadeia de caracteres toopoint toohello DR de região do aplicativo hello. Agora todas as novas contas e bancos de dados de locatário são criados na região de DR hello. clientes de teste existente Olá veem seus dados temporariamente indisponíveis.
* Failover Olá paga o pool de toohello de bancos de dados do locatário em Olá DR região tooimmediately restaurar sua disponibilidade (4). Como Olá failover é uma alteração do nível de metadados rápido, considere uma otimização onde failovers individuais Olá são disparadas sob demanda por conexões de usuário final hello. 
* Se o tamanho de eDTU do pool secundário era inferior a saudação primária porque os bancos de dados secundários Olá apenas Olá necessária capacidade tooprocess Olá alteração logs ao mesmo tempo em que eles foram secundários, imediatamente aumentar capacidade do pool de saudação agora tooaccommodate Olá completo carga de trabalho de todos os locatários (5). 
* Criar novo pool Elástico de saudação com hello mesmo nome e Olá mesmo configuração na região Olá recuperação de desastres para bancos de dados dos clientes avaliação hello (6). 
* Depois que o pool dos clientes Olá avaliação é criado, use bancos de dados de restauração geográfica toorestore Olá individuais de locatário de avaliação no novo pool de saudação (7). Considere disparo restaurações individuais Olá por conexões de usuário final hello ou use outro esquema de prioridade específica do aplicativo.

Agora seu aplicativo está novamente online na região de DR hello. Todos os clientes pagantes têm acesso tootheir dados enquanto os clientes de avaliação Olá experiência atraso ao acessar seus dados.

Quando a região primária Olá é recuperado pelo Azure *depois* você restaurou o aplicativo hello na região Olá DR que você pode continuar executando o aplicativo hello nessa região ou você pode decidir região primária do toofail toohello voltar. Se a região primária Olá é recuperado *antes de* Olá failover processo for concluído, considere com falha novamente imediatamente. Olá failback necessárias etapas de saudação ilustradas no diagrama seguinte hello: 

![Figura 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Cancele todas as solicitações de restauração geográfica pendentes.   
* Failover de bancos de dados de gerenciamento de saudação (8). Após a recuperação da região hello, hello antigo primário se torna automaticamente Olá secundário. Agora ele se torna Olá primário novamente.  
* Failover Olá paga bancos de dados do locatário (9). Da mesma forma, após a recuperação da região hello, primários antigo da saudação se torna automaticamente secundários hello. Agora eles se tornam primárias Olá novamente. 
* Olá conjunto restaurado avaliação bancos de dados que foram alterados na região de DR Olá somente tooread (10).
* Para cada banco de dados no pool de DR de clientes avaliação Olá que foram alteradas desde a recuperação hello, renomear ou excluir o banco de dados correspondente no pool principal de clientes de avaliações de saudação (11) hello. 
* Saudação de cópia atualizada bancos de dados de saudação pool principal de toohello pool da recuperação de desastres (12). 
* Excluir o pool de DR hello (13) 

> [!NOTE]
> a operação de failover Olá é assíncrona. tempo de recuperação de saudação toominimize é importante que você execute o comando de failover Olá locatário dos bancos de dados em lotes de pelo menos 20 bancos de dados. 
> 
> 

chave de saudação **se beneficiar** dessa estratégia é que ele fornece SLA mais alto Olá para Olá clientes pagantes. Ela também garante que avaliações novo Olá estiverem desbloqueadas, assim como Olá avaliação DR pool é criado. Olá **compensação** essa configuração aumenta Olá o custo total de bancos de dados de locatário Olá pelo custo de saudação do pool de DR secundário Olá para clientes pago. Além disso, se o pool secundário Olá tem um tamanho diferente, clientes pagantes Olá experiência menor desempenho depois do failover até hello pool na região Olá DR conclusão da atualização. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Cenário 3: Aplicativo distribuído geograficamente com o serviço em camadas
<i>Eu tenho um aplicativo SaaS evoluído com ofertas de serviço em camadas. Desejo toooffer um toomy SLA muito agressiva paga clientes e minimizar o risco de saudação do impacto quando ocorrem falhas porque o mesmo breves interrupções podem causar insatisfação dos clientes. É importante que os clientes pagantes de saudação sempre pode acessar seus dados. avaliações de saudação são gratuitas e um SLA não é oferecido durante o período de avaliação hello.</i> 

toosupport neste cenário, três pools Elásticos separado use. Dois pools de tamanho igual provisionar com alta eDTUs por banco de dados em dois Olá toocontain de regiões diferentes pagos, bancos de dados de locatário de clientes. pool de terceiro Olá contendo locatários de avaliação Olá pode ter eDTUs inferior por banco de dados e ser provisionado em uma das duas regiões de saudação.

tempo menor de recuperação durante interrupções da saudação tooguarantee, bancos de dados dos clientes pagantes Olá locatário são replicados geograficamente com 50% de bancos de dados primário em cada uma das regiões Olá dois hello. Da mesma forma, cada região tem 50% dos bancos de dados secundários hello. Dessa forma, se uma região estiver offline, somente 50% da saudação paga bancos de dados de clientes são afetados e têm toofail sobre. Olá a outros bancos de dados permanecem intactos. Essa configuração é ilustrada no diagrama a seguir de saudação:

![Figura 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Como em cenários de anterior hello, bancos de dados de gerenciamento de saudação são muito ativos para configurá-los como uma única replicado geograficamente bancos de dados (1). Isso garante um desempenho previsível Olá de novas assinaturas de cliente hello, atualizações de perfil e outras operações de gerenciamento. A saudação primário a região é para bancos de dados de gerenciamento hello e região Olá B é usado para recuperação de bancos de dados de gerenciamento de saudação.

bancos de dados dos clientes pagantes Olá locatário também são replicados geograficamente, mas com cores primárias e secundárias divididos entre regiões A e B (2). Dessa forma, Olá locatário bancos de dados primários afetados pela interrupção Olá failover toohello outra região e ficam disponíveis. Olá outros metade dos bancos de dados de locatário Olá não são afetados em todos os. 

Olá próximo diagrama ilustra Olá tootake de etapas de recuperação se ocorrer uma interrupção na região A.

![Figura 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Failover imediatamente tooregion de bancos de dados de gerenciamento Olá B (3).
* Alterar bancos de dados do aplicativo hello conexão cadeia de caracteres toopoint toohello gerenciamento na região B. modificar Olá gerenciamento bancos de dados toomake se Olá novas contas e bancos de dados de locatário são criados na região B e os bancos de dados do locatário existente Olá são encontrados como também. clientes de teste existente Olá veem seus dados temporariamente indisponíveis.
* Failover Olá paga toopool de bancos de dados do locatário 2 na região B tooimmediately restaurar sua disponibilidade (4). Como Olá failover é uma alteração do nível de metadados rápido, você pode considerar uma otimização onde failovers individuais Olá são disparadas sob demanda por conexões de usuário final hello. 
* Desde agora, pool 2 contém apenas bancos de dados primários, Olá a carga de trabalho total no hello pool aumenta e imediatamente pode aumentar o tamanho de eDTU (5). 
* Criar novo pool Elástico de saudação com hello mesmo nome e Olá mesmo configuração na região Olá B para bancos de dados dos clientes avaliação hello (6). 
* Depois que o pool de saudação é criado usar a restauração geográfica toorestore Olá locatário de avaliação individuais banco de dados no pool de saudação (7). Você pode considerar disparo restaurações individuais Olá por conexões de usuário final hello ou usar outro esquema de prioridade específica do aplicativo.

> [!NOTE]
> a operação de failover Olá é assíncrona. tempo de recuperação de saudação toominimize, é importante que você execute o comando de failover Olá locatário dos bancos de dados em lotes de pelo menos 20 bancos de dados. 
> 

Agora seu aplicativo esteja online novamente na região B. Todos os clientes pagantes têm acesso tootheir dados enquanto os clientes de avaliação Olá experiência atraso ao acessar seus dados.

Quando for recuperado região A precisar toodecide se você quiser região toouse B para clientes de avaliação ou pool de avaliação de clientes do failback toousing Olá na região A. Um critério pode ser Olá % de bancos de dados de locatário de avaliação modificado desde a recuperação de saudação. Independentemente dessa decisão, você precisa balancear toore Olá paga locatários entre dois pools de. Olá próximo diagrama ilustra o processo de saudação quando os bancos de dados de locatário de avaliação Olá falham a tooregion voltar.  

![Figura 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Cancele todas as pool de tootrial DR de solicitações pendentes de restauração geográfica.   
* Failover de banco de dados de gerenciamento de saudação (8). Após a recuperação da região hello, primário antigo Olá automaticamente se tornou Olá secundário. Agora ele se torna Olá primário novamente.  
* Selecione quais bancos de dados do locatário paga falharem toopool back 1 e iniciar failover tootheir secundários (9). Após a recuperação da região hello, todos os bancos de dados no pool de 1 automaticamente se tornou secundários. Agora, 50% deles se tornarão primários novamente. 
* Reduza o tamanho de saudação do eDTU do pool 2 toohello original (10).
* Conjunto de todos os restaurado avaliação bancos de dados na região Olá B somente tooread (11).
* Para cada banco de dados no pool DR avaliação Olá que foi alterado desde a recuperação hello, renomear ou excluir o banco de dados correspondente no pool (12) primário avaliação Olá Olá. 
* Saudação de cópia atualizada bancos de dados de saudação pool principal de toohello pool da recuperação de desastres (13). 
* Excluir o pool de DR hello (14) 

chave de saudação **benefícios** dessa estratégia são:

* Dá suporte à SLA mais agressivo Olá Olá clientes pagantes porque garante que uma interrupção não pode afetar mais de 50% dos bancos de dados de locatário hello. 
* Ela garante que avaliações novo Olá estiverem desbloqueadas como trilha Olá DR pool é criada durante a recuperação de saudação. 
* Permite um uso mais eficiente da capacidade de pool hello como 50% dos bancos de dados secundários no pool de 1 e 2 do pool são garantidas toobe menos ativas de bancos de dados primários hello.

Olá principal **compensações** são:

* as operações CRUD Olá em bancos de dados de gerenciamento de saudação tem menor latência de saudação usuários finais conectados tooregion A que para Olá usuários finais conectados tooregion B conforme elas são executadas em Olá primária dos bancos de dados de gerenciamento de saudação.
* Ele exige mais complexo do design de banco de dados de gerenciamento de saudação. Por exemplo, cada registro de Inquilino tem uma marca de local que precisa toobe alterado durante o failover e failback.  
* Olá clientes pagantes pode enfrentar desempenho mais baixo do que o usual até hello pool atualização na região B é concluída. 

## <a name="summary"></a>Resumo
Este artigo se concentra em estratégias de recuperação de desastres Olá para Olá da camada de banco de dados usado por um aplicativo do ISV SaaS multilocatário. Hello estratégia que você escolher é com base nas necessidades de saudação do aplicativo hello, como o modelo de negócios hello, Olá SLA toooffer tooyour clientes, orçamento restrição etc. Cada descrita estratégia contornos Olá benefícios e compensação para que você pode tomar uma decisão informada. Além disso, seu aplicativo específico provavelmente incluirá outros componentes do Azure. Para que você revise sua orientação de continuidade de negócios e coordenar a recuperação de saudação da camada de banco de dados de saudação com eles. toolearn mais sobre o gerenciamento de recuperação de aplicativos de banco de dados no Azure, consulte muito[criação de soluções de nuvem para recuperação de desastres](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md).
* Para obter uma visão geral e os cenários de continuidade dos negócios, consulte [Visão geral da continuidade dos negócios](sql-database-business-continuity.md).
* toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups de iniciadas pelo serviço de saudação](sql-database-recovery-using-backups.md).
* toolearn sobre as opções de recuperação mais rápidas, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md).
* toolearn sobre como usar backups automatizados para arquivamento, consulte [cópia de banco de dados](sql-database-copy.md).

