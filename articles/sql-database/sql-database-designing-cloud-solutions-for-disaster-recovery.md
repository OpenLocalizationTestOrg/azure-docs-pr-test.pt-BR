---
title: "aaaDesign serviço altamente disponível usando o banco de dados do SQL Azure | Microsoft Docs"
description: "Saiba mais sobre a criação de um aplicativo para serviços altamente disponíveis usando o Banco de Dados SQL do Azure."
keywords: "recuperação de desastre em nuvem, soluções de recuperação de desastre, backup de dados de aplicativo, replicação geográfica, planejamento de continuidade de negócios"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Criar serviços altamente disponíveis usando o Banco de Dados SQL do Azure

Ao criar e implantar serviços altamente disponíveis no banco de dados do SQL Azure, você usar [failover grupos e replicação geográfica ativa](sql-database-geo-replication-overview.md) tooprovide falhas de tooregional de resiliência e falhas catastróficas e habilitar recuperação rápida toohello bancos de dados secundários. Este artigo enfoca os padrões de aplicativo comuns e descreve benefícios hello e vantagens e desvantagens de cada opção, dependendo dos requisitos de implantação de aplicativo hello, contrato de nível de serviço do hello estiver direcionando, latência de tráfego e os custos. Para obter informações sobre o uso da replicação geográfica ativa com Pools elásticos, confira [Estratégias de recuperação de desastres do pool elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Padrão de design 1: Implantação ativa-passiva para recuperação de desastre em nuvem com banco de dados colocalizado
Essa opção é mais adequada para aplicativos com hello características a seguir:

* Instância ativa em uma única região do Azure
* Dependência forte de leitura / gravação (RW) acesso toodata
* Conectividade entre regiões entre o aplicativo da web hello e banco de dados de saudação não é aceitável devido a custos de tráfego e toolatency    

Nesse caso, a topologia de implantação de aplicativo hello é otimizada para lidar com desastres regionais quando todos os componentes de aplicativos são afetados e necessário toofailover como uma unidade. Para redundância geográfica, a lógica do aplicativo hello e Olá são replicados tooanother região, mas não são usados para cargas de trabalho de aplicativo de saudação em condições normais de saudação. o aplicativo Hello na região secundária Olá deve ser configurado toouse SQL conexão cadeia de caracteres toohello banco de dados secundário. Gerenciador de tráfego é configurar toouse [método de roteamento de failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> O [gerenciador de tráfego do ](../traffic-manager/traffic-manager-overview.md) é usado em todo este artigo apenas para fins ilustrativos. Você pode usar qualquer solução de balanceamento de carga que dê suporte ao método de roteamento de failover.    
>

Olá diagrama a seguir mostra essa configuração antes de uma interrupção.

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Após uma interrupção na região primária hello, o serviço de banco de dados SQL do hello detecta banco de dados primário Olá não está acessível e disparar um failover toohello banco de dados secundário com base em parâmetros de saudação da política de failover automático de saudação. Dependendo de seu SLA de aplicativo, você pode decidir tooconfigure um período de cortesia entre detecção de saudação de interrupção hello e failover de saudação em si. Configurar um período de cortesia reduz o risco de saudação de casos de toohello de perda de dados onde interrupção Olá é grave e disponibilidade em Olá região não pode ser restaurada rapidamente. Se o failover do ponto de extremidade de saudação é iniciado pelo Gerenciador de tráfego de saudação antes dos gatilhos de failover do grupo Olá Olá failover de banco de dados Olá, aplicativo hello não é capaz de tooreconnect toohello. tooreconnect de tentativa do aplicativo Hello terá êxito automaticamente assim que a conclusão do failover de banco de dados de saudação. 

> [!NOTE]
> tooachieve totalmente coordenada failover de aplicativo hello e bancos de dados hello, você deve criar seu próprio método de monitoramento e usar o failover manual de pontos de extremidade de aplicativo de web hello e bancos de dados de saudação.
>

Após a conclusão do failover de saudação de pontos de extremidade do aplicativo hello e banco de dados de saudação, aplicativo hello novamente iniciar o processamento de solicitações do usuário Olá na região Olá B e permanecerá localizado no mesmo banco de dados de saudação porque o banco de dados primário Olá agora está em região B. Neste cenário é ilustrado no diagrama a seguir de saudação. Em todos os diagramas, linhas sólidas indicam conexões ativas, linhas pontilhadas indicam conexões suspensas e pontos indicam gatilhos de ação.

![Replicação geográfica: Banco de dados Failover toosecondary. Backup de dados do aplicativo.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Se ocorrer uma interrupção na região secundária hello, Olá link de replicação entre hello primário e o banco de dados secundário Olá será suspenso, mas Olá failover não será disparado porque o banco de dados primário Olá não é afetado. disponibilidade do aplicativo Hello nesse caso, não é alterada mas aplicativo hello opera exposto e, portanto, ambas as regiões corre risco em caso de falham em sucessão.

> [!NOTE]
> Para recuperação de desastres, é recomendável configuração Olá com regiões de tootwo de limitado de implantação do aplicativo. Isso ocorre porque a maioria de saudação regiões do Azure tem apenas duas regiões. Essa configuração não protegerá seu aplicativo contra uma falha catastrófica simultânea nas duas regiões.  Caso ocorra essa falha improvável, você poderá recuperar seus bancos de dados em uma terceira região usando a [operação de restauração geográfica](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Depois que a interrupção de saudação é reduzida, banco de dados secundário Olá automaticamente serão sincronizados novamente com hello primário. Durante a sincronização, o desempenho de saudação primária pode ser afetado ligeiramente dependendo da quantidade de saudação de dados que precisa toobe sincronizado. Olá diagrama a seguir ilustra uma interrupção na região secundária hello.

![Banco de dados secundário sincronizado com o primário. Recuperação de desastre em nuvem.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

chave de saudação **vantagens** de padrão de design são:

* Olá, mesmo aplicativo da web é implantado tooboth regiões sem qualquer configuração específica de região e failover de toohello de tooreact nenhuma lógica adicional. 
* desempenho do aplicativo Hello não é afetado por failover como aplicativo da web hello e banco de dados de saudação sempre estão localizados.

Olá principal **compensação** é que o aplicativo redundantes hello instância na região secundária Olá só é usada para recuperação de desastres.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Padrão de design 2: implantação ativa-ativa para balanceamento de carga de aplicativo
Essa opção de recuperação de desastres de nuvem é ideal para aplicativos com hello características a seguir:

* Alta taxa de banco de dados lê toowrites
* Banco de dados de latência de leitura é mais importante para a experiência do usuário final de saudação latência de gravação da saudação 
* A lógica somente leitura pode ser separada da lógica de leitura/gravação usando uma cadeia de conexão diferente
* Lógica de somente leitura não dependem de dados sendo totalmente sincronizados com as atualizações mais recentes de saudação  

Se seus aplicativos tenham essas características, balanceamento de carga conexões de usuário final Olá entre várias instâncias do aplicativo em diferentes regiões pode melhorar significativamente Olá experiência geral do usuário final. Duas das regiões Olá devem ser selecionada como Olá par de recuperação de desastres e grupo de saudação de failover deve incluir bancos de dados de saudação nessas regiões. tooimplement balanceamento de carga, cada região deve ter uma instância ativa do aplicativo hello com ponto de extremidade do hello leitura-gravação (RW) lógica conectada toohello ouvinte de leitura / gravação do grupo de failover de saudação. Ele garantirá que o failover Olá será iniciado automaticamente se o banco de dados primário Olá é afetado por uma interrupção. Olá somente leitura lógica (RO) no aplicativo da web hello deve se conectar diretamente toohello banco de dados nessa região. Gerenciador de tráfego deve ser configurado toouse [desempenho roteamento](../traffic-manager/traffic-manager-configure-performance-routing-method.md) com [monitoramento de ponto de extremidade](../traffic-manager/traffic-manager-monitoring.md) habilitado para cada instância do aplicativo.

Como no padrão 1, considere a implantação de um aplicativo de monitoramento semelhante. Mas, diferente do padrão #1, Olá monitoramento do aplicativo não será responsável por disparar um failover do ponto de extremidade de saudação.

> [!NOTE]
> Enquanto esse padrão usa mais de um banco de dados secundário, somente Olá secundário na região B deve ser usado para failover e deve fazer parte do grupo de saudação de failover.
>

Gerenciador de tráfego deve ser configurado para a localização geográfica do desempenho roteamento toodirect Olá usuário conexões toohello instância mais próxima toohello do usuário do aplicativo. Olá diagrama a seguir ilustra essa configuração antes de uma interrupção.

![Nenhuma interrupção: aplicativo toonearest roteamento de desempenho. Replicação geográfica.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Se uma interrupção de banco de dados for detectada em uma região de hello, grupo de failover Olá iniciará automaticamente o failover de banco de dados primário no toohello região um secundário na região B. Olá Atualizará automaticamente tooregion de ponto de extremidade de escuta de leitura-gravação Olá B para que conexões de leitura / gravação no aplicativo web de saudação não serão afetados. Gerenciador de tráfego Olá excluirá o ponto de extremidade offline Olá da tabela de roteamento hello, mas continuará roteamento saudação do usuário final tráfego toohello online instâncias restantes. Olá cadeias de conexão SQL somente leitura não serão afetadas como eles sempre ponto toohello banco de dados na Olá mesma região. 

Olá diagrama a seguir ilustra a nova configuração Olá após o failover de saudação.

![Configuração após o failover. Recuperação de desastre em nuvem.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

No caso de uma interrupção em uma das regiões secundário Olá, Gerenciador de tráfego Olá removerá automaticamente pontos de extremidade offline Olá nessa região da tabela de roteamento de saudação. Olá replicação canal toohello banco de dados secundário nessa região será suspenso. Porque regiões restantes Olá receber tráfego de usuário adicionais neste cenário, o desempenho do aplicativo hello será afetado durante a interrupção de saudação. Depois que a interrupção de saudação é reduzida, hello banco de dados secundário na região afetada hello serão imediatamente sincronizado com hello primário. Durante a saudação desempenho da sincronização de saudação primária pode ser afetado ligeiramente dependendo da quantidade de saudação de dados que precisa toobe sincronizado. Olá diagrama a seguir ilustra uma interrupção na região B.

![Interrupção na região secundária. Recuperação de desastre em nuvem – replicação geográfica.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

chave de saudação **vantagem** desse design padrão é que você pode dimensionar a carga de trabalho de aplicativo hello entre vários desempenho de usuário final ideal secundários tooachieve Olá. Olá **compensações** dessa opção são:

* Conexões de leitura / gravação entre instâncias do aplicativo hello e banco de dados têm diferentes latência e custo
* Desempenho do aplicativo é afetado durante a interrupção de saudação

> [!NOTE]
> Uma abordagem semelhante pode ser usada toooffload especializado cargas de trabalho como trabalhos, ferramentas de business intelligence ou backups de emissão de relatórios. Normalmente, essas cargas de trabalho consumam recursos significativos do banco de dados, portanto, é recomendável que você designar uma saudação bancos de dados secundários para eles com hello desempenho toohello correspondentes nível carga de trabalho prevista.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Padrão de design 3: implantação ativa-passiva para preservação dos dados
Essa opção é mais adequada para aplicativos com hello características a seguir:

* Qualquer perda de dados é um risco comercial elevado. Olá failover de banco de dados só pode ser usado como um último recurso se a interrupção de saudação for catastrófica.
* aplicativo Hello dá suporte aos modos de somente leitura e leitura / gravação de operações e pode operar em "modo somente leitura" por um período de tempo.

Nesse padrão, o aplicativo hello Alterna modo somente tooread quando conexões de leitura / gravação da saudação comece a obter erros de tempo limite. Olá aplicativo Web é implantado tooboth regiões e incluir um ponto de extremidade de escuta de leitura-gravação de toohello conexão e um ponto de extremidade de escuta de somente leitura de toohello conexão diferente. Gerenciador de tráfego Olá deve ser configurado toouse [failover roteamento](../traffic-manager/traffic-manager-configure-failover-routing-method.md) com [monitoramento de ponto de extremidade](../traffic-manager/traffic-manager-monitoring.md) habilitado para o ponto de extremidade de aplicativo de saudação em cada região.

Olá diagrama a seguir ilustra essa configuração antes de uma interrupção.

![Implantação ativo-passivo antes do failover. Recuperação de desastre em nuvem.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Quando o Gerenciador de tráfego Olá detecta uma falha de conectividade tooregion um, ele alternará automaticamente uma instância de aplicativo do usuário tráfego toohello na região B. Com esse padrão, é importante definir período de cortesia de saudação com um valor suficientemente alto do tooa do perda de dados, por exemplo, 24 horas. Ele garantirá que a perda de dados é evitada se interrupção Olá mitigada nesse período. Quando Olá aplicativo Web na região Olá B é ativado operações de leitura / gravação da saudação começam a falhar. Nesse ponto, ele deverá alternar toohello o modo somente leitura. Olá esse modo solicitações será automaticamente roteado toohello banco de dados secundário. No caso de saudação de saudação uma falha catastrófica interrupção não será atenuada dentro do período de cortesia hello e grupo de failover Olá irá disparar Olá failover. Depois que Olá ouvinte de leitura-gravação ficará disponível e Olá chamadas tooit parará falhando. Isso é ilustrado pela Olá diagrama a seguir.

![Interrupção: aplicativo em modo somente leitura. Recuperação de desastre em nuvem.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Se a interrupção de saudação na região primária Olá mitigada dentro do período de cortesia Olá, traffic manager detecta restauração Olá de conectividade na região primária hello e alterna a instância de aplicativo do usuário tráfego toohello Voltar na região A. Essa instância de aplicativo reinicia e opera no modo de leitura / gravação usando o banco de dados primário Olá na região A.

No caso de uma interrupção na região Olá B, Gerenciador de tráfego Olá detecta a falha de saudação do ponto de extremidade de aplicativo hello na região B e Olá failover grupo comutadores Olá ouvinte somente leitura tooregion A. Essa interrupção não afeta a experiência do usuário final de saudação mas o banco de dados primário hello será exposto durante a interrupção de saudação. Isso é ilustrado pela Olá diagrama a seguir.

![Interrupção: banco de dados secundário. Recuperação de desastre em nuvem.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Depois que a interrupção de saudação é reduzida, hello banco de dados secundário é imediatamente sincronizado com hello primário e ouvinte Olá de somente leitura é comutada toohello back o banco de dados secundário na região B. Durante a sincronização, desempenho de saudação primária pode ser afetado ligeiramente dependendo da quantidade de saudação de dados que precisa toobe sincronizado.

Esse padrão de design apresenta várias **vantagens**:

* Isso evita a perda de dados durante interrupções temporárias hello.
* Tempo de inatividade depende apenas rapidez do traffic manager detecta a falha de conectividade hello, que é configurável.

Olá **compensação** é:

* Aplicativo deve ser capaz de toooperate no modo somente leitura.

> [!NOTE]
> No caso de uma interrupção de serviço permanente na região hello, manualmente ativar o failover de banco de dados e perda de dados de saudação. aplicativo Hello estará funcional em região secundária do hello com banco de dados de toohello de acesso de leitura-gravação.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Planejamento de continuidade de negócios: escolher um design de aplicativo para recuperação de desastre em nuvem
Sua estratégia de recuperação de desastres de nuvem específica pode combinar ou estender esses padrões de design necessidades de saudação atender toobest de seu aplicativo.  Como mencionado anteriormente, estratégia Olá que você escolher baseia Olá SLA desejado toooffer tooyour clientes e Olá topologia de implantação do aplicativo. toohelp orientar sua decisão, Olá a tabela a seguir compara opções de saudação com base em Olá dados estimada perda ou recuperação objetivo de ponto (RPO) e o tempo de recuperação estimado (ERTER).

| Padrão | RPO | ERT |
|:--- |:--- |:--- |
| Implantação ativa-passiva para recuperação de desastres com acesso de banco de dados colocalizado |Acesso de leitura/gravação < 5 s |Tempo de detecção de falha + TTL do DNS |
| Implantação ativa-ativa para balanceamento de carga de aplicativo |Acesso de leitura/gravação < 5 s |Tempo de detecção de falha + TTL do DNS |
| Implantação ativa-passiva para preservação de dados |Acesso somente leitura < 5 seg | Acesso somente leitura = 0 |
||Acesso de leitura/gravação = zero | Acesso de leitura/gravação = Tempo de detecção de falha + período de carência de perda de dados |
|||

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md)
* Para obter uma visão geral e os cenários de continuidade dos negócios, confira [Visão geral da continuidade dos negócios](sql-database-business-continuity.md)
* toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups de iniciadas pelo serviço de saudação](sql-database-recovery-using-backups.md)
* toolearn sobre as opções de recuperação mais rápidas, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md)  
* toolearn sobre como usar backups automatizados para arquivamento, consulte [cópia de banco de dados](sql-database-copy.md)
* Para obter informações sobre o uso da replicação geográfica ativa com Pools elásticos, confira [Estratégias de recuperação de desastres do pool elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
