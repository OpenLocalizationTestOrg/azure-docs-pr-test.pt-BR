---
title: "aaaFailover grupos e replicação geográfica ativa - banco de dados do SQL Azure | Microsoft Docs"
description: "Grupos de failover automático com replicação geográfica permite toosetup 4 réplicas de banco de dados em qualquer um dos Olá datacenters do Azure e failover autoomatically no evento de saudação de uma interrupção."
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Visão geral: grupos de failover e replicação geográfica ativa
Replicação geográfica permite tooconfigure backup toofour legível bancos de dados secundários em Olá mesmo ou em diferentes data centers locais (regiões). Bancos de dados secundários estão disponíveis para consulta e para o failover no caso de saudação do data center interrupção ou hello dificuldades tooconnect toohello banco de dados primário. saudação failover deve ser iniciada manualmente pelo aplicativo de saudação do usuário hello. Após o failover, o novo primário de saudação tem um ponto de extremidade de conexão diferente. 

> [!NOTE]
> A replicação geográfica ativa agora está disponível para todos os bancos de dados em todas as camadas de serviço e em todas as regiões.
>  

Grupos de failover automático do banco de dados SQL do Azure (em visualização) é tooautomatically de recurso criado um banco de dados SQL gerenciar a relação de replicação geográfica, a conectividade e o failover em escala. Com ele, Olá clientes ganho olá capacidade tooautomatically recuperar vários bancos de dados relacionados na região secundária Olá após falhas catastróficas de regionais ou outros eventos não planejados que resultam na perda completa ou parcial de saudação do serviço de banco de dados SQL disponibilidade na região primária hello. Além disso, eles podem usar Olá bancos de dados secundários legíveis toooffload somente leitura cargas de trabalho.  Como os grupos de failover automático envolvem vários bancos de dados que devem ser configurados no servidor primário hello. Servidores primários e secundários devem estar no hello mesma assinatura. Grupos de failover automático oferecem suporte a replicação de todos os bancos de dados em Olá grupo tooonly em um servidor secundário em uma região diferente. Replicação geográfica ativa, sem grupos de failover automático, permite que até too4 secundários em qualquer região.

Se você estiver usando replicação geográfica ativa e por qualquer motivo que seu banco de dados primário falha, ou simplesmente toobe necessidades colocado offline, você pode iniciar failover tooany dos seus bancos de dados secundários. Quando o failover for ativado tooone dos bancos de dados secundários hello, todos os outros secundários são automaticamente vinculado toohello novo primário. Se você estiver usando o failover automático e grupos de recuperação de banco de dados (em visualização) toomanage qualquer interrupção que afeta um ou vários bancos de dados de saudação nos resultados de grupo Olá no failover automático. Você pode configurar a política de failover automático de saudação que melhor atenda às necessidades do seu aplicativo, ou você pode recusá-lo e usar a ativação manual. Além disso, os grupos de failover automático (em versão prévia) fornecem pontos de extremidade de ouvinte de leitura/gravação e somente leitura que permanecem inalterados durante failovers. Se você usar a ativação de failover manual ou automático, failover alterna todos os bancos de dados secundários em Olá tooprimary de grupo. Após a conclusão do failover de banco de dados hello, o registro de DNS do hello é automaticamente atualizada tooredirect Olá pontos de extremidade toohello nova região.

Você pode gerenciar a replicação e o failover de um banco de dados individual ou de um conjunto de bancos de dados em um servidor ou em um pool elástico usando a replicação geográfica ativa. Você pode fazer essa usando Olá [portal do Azure](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [Transact-SQL](sql-database-geo-replication-transact-sql.md), ou hello [API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). Após o failover, certifique-se de requisitos de autenticação de saudação de seu servidor e banco de dados são definidos no novo primário de saudação. Para obter detalhes, consulte [Segurança do Banco de Dados SQL do Azure após a recuperação de desastre](sql-database-geo-replication-security-config.md). Isso se aplica a ambos os tooactive replicação geográfica e o failover automático grupos (em visualização).

Saudação de aproveita a replicação geográfica ativa [AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) tecnologia do SQL Server tooasynchronously replicar as transações confirmadas em Olá banco de dados primário tooa banco de dados secundário usando o isolamento de instantâneo de leitura confirmada (RCSI). Os grupos de failover automático fornecem semântica de grupo Olá sobre replicação geográfica ativa, mas Olá mesmo mecanismo de replicação assíncrona é usado. Em qualquer momento determinado, banco de dados secundário Olá pode ficar um pouco atrás do banco de dados primário hello, dados secundários Olá toonever têm transações parciais. A redundância entre regiões permite recuperar tooquickly de aplicativos da perda permanente de um datacenter inteiro ou partes de um datacenter causada por desastres naturais, falhas humanas catastróficas ou crimes. dados específicos de RPO Olá podem ser encontrados em [visão geral da continuidade de negócios](sql-database-business-continuity.md).

Olá figura a seguir mostra um exemplo de replicação geográfica ativa secundária e configurado com um principal na região do hello Centro Norte dos EUA na região do hello Centro Sul dos EUA.

![relacionamento de replicação geográfica](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Como os bancos de dados secundários Olá são legíveis, eles podem ser usados toooffload somente leitura cargas de trabalho como trabalhos de relatório. Se você estiver usando replicação geográfica ativa, é banco de dados secundário toocreate possíveis Olá Olá mesma região com hello primário, mas não aumenta falhas de toocatastrophic de resiliência do aplicativo hello. Se você estiver usando grupos de failover automático (em versão prévia), seus bancos de dados secundários serão criados sempre em uma região diferente.

Além disso, toodisaster recuperação replicação geográfica pode ser usada em Olá os seguintes cenários:

* **Migração de banco de dados**: você pode usar um banco de dados de um servidor tooanother on-line de toomigrate de replicação geográfica ativa com tempo de inatividade mínimo.
* **Atualizações de aplicativos**: você pode criar um secundário extra como uma cópia de failback durante as atualizações de aplicativos.

continuidade de negócios tooachieve, adicionar redundância de banco de dados entre data centers é apenas parte da solução de saudação. Recuperando um aplicativo (serviço) a-ponta após uma falha catastrófica exige a recuperação de todos os componentes que constituem o serviço hello e todos os serviços dependentes. Exemplos desses componentes incluem software de cliente da saudação (por exemplo, um navegador com JavaScript personalizado), front-ends da web, armazenamento e DNS. É fundamental que todos os componentes são resiliente toohello mesmas falhas e fiquem disponíveis dentro do objetivo de tempo de recuperação hello (RTO) do seu aplicativo. Portanto, você precisa tooidentify todos os serviços dependentes e entende as garantias de saudação e os recursos que eles fornecem. Em seguida, você deve tomar as etapas adequadas tooensure que seu serviço funcione durante Olá failover dos serviços de saudação do qual ele depende. Para obter mais informações sobre como criar soluções para a recuperação de desastre, veja [Criando soluções de nuvem para a recuperação de desastre usando a replicação geográfica ativa](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Recursos da replicação geográfica ativa
recurso de replicação geográfica ativa Olá fornece Olá recursos essenciais a seguir:
* **Replicação assíncrona automática**: você só pode criar um banco de dados secundário, adicionando tooan banco de dados existente. Olá secundário pode ser criado em qualquer servidor de banco de dados SQL. Depois de criado, banco de dados secundário Olá é preenchido com dados de saudação copiados do banco de dados primário hello. Este processo é conhecido como propagação. Depois que o banco de dados secundário foi criado e propagado, atualizações de banco de dados primário toohello assincronamente são replicados automaticamente toohello banco de dados secundário. Replicação assíncrona significa que as transações são confirmadas no banco de dados primário Olá antes que eles sejam replicados toohello banco de dados secundário. 
* **Bancos de dados secundários legíveis**: um aplicativo pode acessar um banco de dados secundário para operações somente leitura usando Olá iguais ou diferentes elementos de segurança usado para acessar o banco de dados primário hello. Olá bancos de dados secundários operam em isolamento de instantâneo modo tooensure a replicação de atualizações de saudação do hello primário (repetição de log) não é atrasada por consultas executadas no hello secundário.

   > [!NOTE]
   > a repetição do log Hello está atrasada no banco de dados secundário Olá se há atualizações de esquema que está recebendo do hello primário que exigem um bloqueio de esquema no banco de dados secundário hello. 
   > 

* **Vários secundários legíveis**: dois ou mais bancos de dados secundários aumentam a redundância e o nível de proteção para o banco de dados primário hello e aplicativo. Se existirem vários bancos de dados secundários, aplicativo hello permanece protegido, mesmo se um dos bancos de dados secundários Olá falhar. Se houver apenas um banco de dados secundário, e ele falhar, o aplicativo hello é exposto toohigher risco até que um novo banco de dados secundário é criado.

   > [!NOTE]
   > Se você estiver usando replicação geográfica ativa toobuild um aplicativo distribuído globalmente e precisa tooprovide somente leitura acessar toodata em mais de 4 regiões, você pode criar secundário de um secundário (um processo conhecido como encadeamento). Dessa forma, que você pode obter uma escala praticamente ilimitada de replicação de banco de dados. Além disso, o encadeamento reduz a sobrecarga de Olá de replicação do banco de dados primário hello. compensação de saudação é latência de replicação maior Olá bancos de dados secundários hello mais folha. . 
   >

* **Suporte para bancos de dados do pool elástico**: a replicação geográfica ativa pode ser configurada para qualquer banco de dados em qualquer pool elástico. banco de dados secundário Olá pode ser em outro pool Elástico. Para bancos de dados regulares, Olá secundário pode ser um pool Elástico e vice-versa como são camadas de serviço Olá Olá mesmo. 
* **Nível de desempenho configurável do banco de dados secundário Olá**: um banco de dados secundário pode ser criado com o nível de desempenho inferior Olá primário. Bancos de dados primários e secundários são necessários toohave Olá mesma camada de serviço. Essa opção não é recomendada para aplicativos com atividade de gravação do banco de dados de alta porque a latência de replicação maior Olá aumenta o risco de saudação de perda significativa de dados após um failover. Além disso, depois que o desempenho do aplicativo de saudação do failover é afetado até Olá novo primário é atualizado tooa maior desempenho nível. Olá, gráfico de porcentagem de e/s de log no portal do Azure fornece uma boa maneira tooestimate Olá mínimo nível de desempenho do hello secundária que é necessário toosustain Olá replicação load. Por exemplo, se o banco de dados primário é P6 (1000 DTU) e seu percentual de e/s de log é 50% Olá secundário precisa toobe pelo menos P4 (500 DTU). Você também pode recuperar dados de e/s de log de hello usando [sys. resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) ou [sys.DM db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) modos de exibição de banco de dados.  Para obter mais informações sobre níveis de desempenho do banco de dados SQL hello, consulte [opções de banco de dados SQL e desempenho](sql-database-service-tiers.md). 
* **Controlado pelo usuário failover e failback**: um banco de dados secundário pode ser explicitamente função primária desligados toohello a qualquer momento pelo aplicativo hello ou usuário de saudação. Durante uma saudação interrupção real opção "não planejada" deve ser usada, que promove imediatamente toobe secundário Olá primário. Quando primário falha Olá recupera e está disponível novamente, sistema Olá automaticamente marcas hello recuperado primário como um secundário e colocá-lo atualizado com o novo primário de saudação. Devido a toohello natureza assíncrona de replicação, uma pequena quantidade de dados pode ser perdida durante failovers não planejados se primário falhar antes que ele replica hello mais recentes alterações toohello secundário. Quando um principal com vários secundários Falha, sistema Olá reconfigura automaticamente as relações de replicação hello e Olá links restantes secundários toohello recentemente promovido primário sem a necessidade de intervenção do usuário. Após a interrupção de saudação que causou o failover de saudação é reduzida, pode ser região primária do toohello tooreturn desejável Olá aplicativo. toodo que, o comando de failover Olá deve ser chamado com hello "planejado" opção. 
* **Manter as credenciais e as regras de firewall em sincronia**: É recomendável usar [regras de firewall de banco de dados](sql-database-firewall-configure.md) para bancos de dados replicada geograficamente para essas regras podem ser replicadas com hello tooensure de banco de dados todos os bancos de dados secundários têm Olá as mesmas regras de firewall que Olá primário. Essa abordagem elimina a necessidade de saudação para clientes toomanually configurar e manter as regras de firewall nos servidores que hospedam os bancos de dados primários e secundários hello. Da mesma forma, usando [usuários de banco de dados independente](sql-database-manage-logins.md) de dados acesso garante que bancos de dados primários e secundários sempre têm Olá as credenciais do usuário mesmo durante um failover, não há nenhum interrupções toomismatches devido aos logons e senhas. Com a adição de saudação do [Active Directory do Azure](../active-directory/active-directory-whatis.md), os clientes podem gerenciar usuários acesso tooboth primários e secundários bancos de dados e eliminar Olá necessário para o gerenciamento de credenciais em bancos de dados completamente.

## <a name="auto-failover-group-capabilities"></a>Recursos de grupo de failover automático

O recurso grupos de failover automático fornece uma abstração eficaz de replicação geográfica ativa, dando suporte à replicação em nível de grupo e o failover automático. Além disso, remove cadeia de conexão de SQL Olá Olá necessidade toochange após o failover, fornecendo pontos de extremidade do hello ouvinte adicional. 

* **Grupo de failover**: Um ou mais grupos de failover podem ser criados entre dois servidores em regiões diferentes (servidores primário e secundário). Cada grupo pode conter um ou vários bancos de dados são recuperados como uma unidade no caso de alguns ou todos os bancos de dados principais fique indisponíveis devido tooan interrupção na região primária hello.  
* **Servidor primário**: um servidor que hospeda os bancos de dados primários no grupo de failover Olá Olá.
* **Servidor secundário**: um servidor que hospeda os bancos de dados secundários no grupo de failover Olá Olá. servidor secundário Olá não pode estar em Olá mesma região que o servidor primário hello.
* **Adicionar grupo de toofailover de bancos de dados**: você pode colocar vários bancos de dados dentro de um servidor ou em uma elástica pool em Olá mesmo grupo de failover. Se você adicionar um grupo de toohello de banco de dados autônomo, ele cria automaticamente um banco de dados secundário usando Olá a mesma edição e nível de desempenho. Se o banco de dados primário hello está em um pool Elástico, Olá secundário é criado automaticamente no pool Elástico Olá com hello mesmo nome. Se você adicionar um banco de dados que já tenha um banco de dados secundário no servidor secundário hello, que a replicação geográfica é herdada por grupo de saudação.

   > [!NOTE]
   > Ao adicionar um banco de dados que já tenha um banco de dados secundário em um servidor que não faz parte do grupo de saudação de failover, um novo secundário é criado no servidor secundário hello. 
   >

* **Ouvinte de leitura / gravação do grupo de failover**: registro de um DNS CNAME formado como  **&lt;nome do grupo de failover&gt;. t** que aponte toohello URL de servidor primário atual. Permite aplicativos de SQL de leitura-gravação Olá tootransparently reconectar toohello banco de dados primário quando Olá primário é alterado após o failover. 
* **Ouvinte do grupo de failover somente leitura**: registro de um DNS CNAME formado como  **&lt;nome do grupo de failover&gt;. secondary.database.windows.net** que aponta o URL do servidor secundário toohello. Permite Olá aplicativos SQL somente leitura, conectar tootransparently toohello banco de dados secundário usando Olá especificado de regras de balanceamento de carga. Opcionalmente, você pode especificar se deseja Olá somente leitura tráfego toobe automaticamente redirecionados servidor primário toohello quando o servidor secundário Olá não está disponível.
* **Política de failover automático**: por padrão, o grupo de saudação de failover é configurado com uma política de failover automático. Olá sistema dispara o failover, assim como Olá falha é detectada. Se desejar que o fluxo de trabalho do toocontrol Olá failover de aplicativo hello, você pode desativar o failover automático. 
* **Failover manual**: você pode iniciar o failover manualmente a qualquer momento, independentemente da configuração de failover automático de saudação. Se a política de failover automático não é configurado o failover manual é necessário toorecover bancos de dados no grupo de saudação de failover. Você pode iniciar um failover forçado ou amigável (com sincronização total de dados). Olá este último pode ser região primária do toohello toorelocate usado Olá servidor ativo. Quando concluir o failover registros DNS de saudação são atualizadas automaticamente tooensure conectividade toohello correto do servidor.
* **Período de cortesia com perda de dados**: bancos de dados primários e secundários Olá estão sincronizados usando replicação assíncrona Olá failover pode resultar em perda de dados. Você pode personalizar tooreflect de política de failover automático Olá perda de toodata tolerância do seu aplicativo. Configurando **GracePeriodWithDataLossHours**, você pode controlar quanto tempo o sistema Olá aguarda antes de iniciar o failover de saudação que provavelmente tooresult perda de dados. 

   > [!NOTE]
   > Quando o sistema detectar que bancos de dados Olá no grupo Olá ainda estão online (por exemplo, interrupção Olá somente impacto plano de controle de serviço Olá), ele ativa o failover de saudação à sincronização de dados completo (amigável failover), independentemente do valor de saudação imediatamente definido por **GracePeriodWithDataLossHours**. Esse comportamento garante que não há nenhuma perda de dados durante a recuperação de saudação. período de cortesia Olá entra em vigor somente quando um failover amigável não é possível. Se a interrupção de saudação mitigada antes de expirar o período de cortesia Olá, Olá failover não está ativado.
   >

* **Vários grupos de failover**: você pode configurar vários grupos de failover para Olá mesmo par de servidores toocontrol Olá de escala de failovers. Cada grupo sofre failover de forma independente. Se seu aplicativo multilocatário usa pools Elásticos, você pode usar esse recurso toomix primários e secundários os bancos de dados em cada pool. Dessa forma, você pode reduzir o impacto de Olá de uma interrupção tooonly metade dos locatários hello.

## <a name="best-practices-of-building-highly-available-service"></a>Práticas recomendadas para a criação de serviço altamente disponível

toobuild um serviço altamente disponível que usa clientes de saudação do banco de dados SQL do Azure deve seguir estas diretrizes:
- **Usar grupo de failover**: Um ou mais grupos de failover podem ser criados entre dois servidores em regiões diferentes (servidores primário e secundário). Cada grupo pode conter um ou vários bancos de dados são recuperados como uma unidade no caso de alguns ou todos os bancos de dados principais fique indisponíveis devido tooan interrupção na região primária hello. grupo de failover de saudação cria o banco de dados de replicação geográfica secundária com hello mesmo objetivo como Olá principal de serviço. Se você adicionar que um replicação geográfica relação toohello failover grupo Certifique-se de que Olá geográfica-secundário existente é configurado com Olá mesmo como objetivo de nível de serviço Olá primário.
- **Use o ouvinte de leitura / gravação para a carga de trabalho OLTP**: ao executar o uso de operações OLTP  **&lt;nome do grupo de failover&gt;. t** como URL do servidor de saudação e conexões Olá será primário toohello direcionado automaticamente. Essa URL não será alterado após o failover de saudação.  
Observação Olá failover envolve a atualização Olá registro DNS para que conexões de cliente Olá seja redirecionado toohello novo primário após o cliente Olá cache DNS é atualizado.
- **Use o ouvinte de somente leitura para cargas de trabalho somente leitura**: se você tiver uma logicamente isolada somente leitura carga de trabalho toocertain tolerante a deterioração dos dados, você pode usar o banco de dados secundário Olá no aplicativo hello. Para usam sessões somente leitura  **&lt;nome do grupo de failover&gt;. secondary.database.windows.net** como URL do servidor de saudação e conexão Olá será direcionado automaticamente toohello secundário. Também recomendamos que você indique na cadeia de conexão a intenção de leitura usando **ApplicationIntent=ReadOnly**. 
- **Esteja preparado para a degradação do desempenho**: decisão de failover do SQL é independente do restante de saudação do aplicativo hello ou outros serviços usados. aplicativo Hello pode ser "mixed" com alguns componentes em uma região e alguns em outro. degradação de saudação tooavoid, certifique-se de implantação de aplicativo redundantes de saudação na região Olá DR e siga as orientações de saudação neste artigo.  
Observação Olá aplicativo na região de DR Olá não tem toouse uma cadeia de caracteres de conexão diferente.  
- **Preparar para perda de dados**: se for detectada uma interrupção, SQL acionará automaticamente o failover de leitura / gravação se zero toohello de perda de dados é melhor de nossos dados de Conhecimento. Caso contrário, ele aguarda o período de saudação especificado por **GracePeriodWithDataLossHours**. Se você tiver especificado **GracePeriodWithDataLossHours**, esteja preparado para eventual perda de dados. Em geral, durante interrupções, o Azure favorece a disponibilidade. Se você não puder perda de dados, verifique se tooset **GracePeriodWithDataLossHours** tooa suficientemente grande número, como 24 horas. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Atualizar ou fazer downgrade de um banco de dados primário
Você pode atualizar ou fazer downgrade de um nível de desempenho diferente do banco de dados primário tooa (dentro de saudação mesma camada de serviço) sem desconectar qualquer banco de dados secundário. Durante a atualização, é recomendável que você atualiza o banco de dados secundário Olá primeiro e, em seguida, atualiza Olá primário. Ao fazer o downgrade, inverta a ordem de saudação: downgrade Olá primário primeiro e, em seguida, fazer o downgrade Olá secundário. Quando você atualiza ou fazer downgrade da camada de serviço diferente de tooa de banco de dados Olá essa recomendação é imposta. 

> [!NOTE]
> Se você criou o banco de dados secundário como parte da configuração de grupo de failover Olá não é banco de dados secundário do hello toodowngrade recomendado. Isso é tooensure sua camada de dados tem tooprocess de capacidade suficiente sua carga de trabalho normal após o failover está ativado. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Impedir a perda de saudação de dados críticos
Devido a toohello alta latência de redes de longa distância, a cópia contínua usa um mecanismo de replicação assíncrona. A replicação assíncrona tornará a perda de alguns dados inevitável se ocorrer uma falha. No entanto, alguns aplicativos podem exigir nenhuma perda de dados. tooprotect essas atualizações críticas, um desenvolvedor de aplicativos podem chamar hello [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) procedimento de sistema imediatamente após a confirmação de transação de saudação. Chamando **sp_wait_for_database_copy_sync** Olá blocos thread de chamada até que a última transação confirmada de saudação foi transmitida toohello banco de dados secundário. No entanto, ela não espera por Olá transmitido transações toobe repetidos e confirmada no hello secundário. **sp_wait_for_database_copy_sync** tooa escopo link de cópia contínua específico. Qualquer usuário com hello conexão direitos toohello banco de dados primário pode chamar esse procedimento.

> [!NOTE]
> **sp_wait_for_database_copy_sync** prevenirá perda de dados depois de um failover, mas não garantirá a sincronização completa para acesso de leitura. Olá atraso causado por uma **sp_wait_for_database_copy_sync** chamada de procedimento pode ser significativa e depende do tamanho de Olá Olá do log de transações em tempo de saudação da chamada de saudação. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Gerenciar grupos de failover e a replicação geográfica ativa programaticamente
Como discutido anteriormente, grupos de failover automático (em visualização) e ativar replicação geográfica também pode ser gerenciada programaticamente usando o PowerShell do Azure e Olá API REST. Olá tabelas seguintes descreve o conjunto de saudação de comandos disponíveis.

**API do Gerenciador de recursos do Azure e segurança baseada em função**: replicação geográfica ativa inclui um conjunto de APIs do Gerenciador de recursos do Azure para gerenciamento, incluindo Olá [API de REST de banco de dados SQL do Azure](https://docs.microsoft.com/rest/api/sql/) e [Azure Cmdlets do PowerShell](https://docs.microsoft.com/powershell/azure/overview). Essas APIs exigem o uso de saudação de grupos de recursos e suporte à segurança baseada em função (RBAC). Para obter mais informações sobre como acessar as funções tooimplement, consulte [o controle de acesso](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Muitos dos novos recursos de replicação geográfica ativa só têm suporte usando a [API REST do Azure SQL](../azure-resource-manager/resource-group-overview.md) e [cmdlets do PowerShell do Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt163571.aspx) baseados no [Azure Resource Manager](https://msdn.microsoft.com/library/azure/mt574084.aspx). Olá [(clássico) API de REST](https://msdn.microsoft.com/library/azure/dn505719.aspx) e [cmdlets de banco de dados do SQL do Azure (clássica)](https://msdn.microsoft.com/library/azure/dn546723.aspx) têm suporte para compatibilidade com versões anteriores, usando Olá APIs com base em Gerenciador de recursos do Azure são recomendadas. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>Gerenciar SQL database failover usando Transact-SQL

| Command | Descrição |
| --- | --- |
| [ALTER DATABASE (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Use Adicionar SECUNDÁRIO ON SERVER argumento toocreate um banco de dados secundário para um banco de dados existente e inicia a replicação de dados |
| [ALTER DATABASE (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Usar o FAILOVER ou FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch um failover do banco de dados secundário toobe tooinitiate primário |
| [ALTER DATABASE (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Use remover SECUNDÁRIO ON SERVER tooterminate uma replicação de dados entre um banco de dados SQL e hello especificado banco de dados secundário. |
| [sys.geo_replication_links (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt575501.aspx) |Retorna informações sobre todos os links de replicação existente para cada banco de dados no servidor lógico do hello Azure SQL Database. |
| [sys.dm_geo_replication_link_status (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/mt575504.aspx) |Obtém Olá último horário de duplicação, última latência de replicação e outras informações sobre o link de replicação Olá para um determinado banco de dados SQL. |
| [sys.dm_operation_status (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/dn270022.aspx) |Mostra o status de saudação para todas as operações de banco de dados, incluindo status Olá Olá dos links de replicação. |
| [sp_wait_for_database_copy_sync (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/dn467644.aspx) |faz com que Olá aplicativo toowait até que todas as transações confirmadas sejam replicadas e reconhecidas pelo Olá banco de dados secundário. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>Gerenciar SQL database failover usando PowerShell

| Cmdlet | Descrição |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Obtém um ou mais bancos de dados. |
| [New-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Cria um banco de dados secundário para um banco de dados existente e inicia a replicação de dados. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Alterna um failover do banco de dados secundário toobe tooinitiate primário. |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Encerra a replicação de dados entre um banco de dados SQL e Olá secundário banco de dados especificado. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Obtém os links de replicação geográfica Olá entre um banco de dados do SQL Azure e um grupo de recursos ou do SQL Server. |
| [New-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Esse comando cria um grupo de failover e registra-o nos servidores primário e secundário|
| [Remove-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Remove o grupo de failover de saudação do servidor de saudação e exclui todos os bancos de dados secundários incluídos Olá grupo |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Recupera a configuração do grupo de failover Olá |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Modifica a configuração de saudação do grupo de saudação de failover |
| [Switch-AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | Dispara o failover de servidor secundário do hello failover grupo toohello |
|  | |

> [!IMPORTANT]
> Para scripts de exemplo, consulte [Configurar e realizar o failover de um banco de dados individual usando a replicação geográfica ativa](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [Configurar e realizar o failover de um banco de dados em pool usando a replicação geográfica ativa](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md) e [Configurar e realizar o failover de um grupo de failover para um banco de dados individual (versão prévia)] (scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>Gerenciar usando a API REST de saudação de failover do banco de dados SQL
| API | Descrição |
| --- | --- |
| [Criar ou atualizar banco de dados (createMode=Restore)](/rest/api/sql/Databases/CreateOrUpdate) |Cria, atualiza ou restaura um banco de dados primário ou secundário. |
| [Obter, Criar ou Atualizar o Status de um Banco de Dados](/rest/api/sql/Databases/CreateOrUpdate) |Retorna o status de saudação durante uma operação de criação. |
| [Definir o banco de dados secundário como primário (Failover planejado)](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Define qual banco de dados de réplica é primário efetuando failover do banco de dados de réplica primária atual hello. |
| [Definir o banco de dados secundário como primário r (Failover não planejado)](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Define qual banco de dados de réplica é primário efetuando failover do banco de dados de réplica primária atual hello. Esta operação pode resultar em perda de dados. |
| [Obter link de replicação](/rest/api/sql/replicationlinks/get) |Obtém um link de replicação específico para um determinado Banco de Dados SQL em uma parceria de replicação geográfica. Recupera informações de saudação visíveis na exibição de catálogo sys.geo_replication_links hello. |
| [Links de Replicação - Listar pelo Banco de Dados](/rest/api/sql/replicationlinks/listbydatabase) | Obtém todos os links de replicação para um determinado Banco de Dados SQL em uma parceria de replicação geográfica. Recupera informações de saudação visíveis na exibição de catálogo sys.geo_replication_links hello. |
| [Excluir links de replicação](/rest/api/sql/databases/delete) | Exclui um link de replicação do banco de dados. Não pode ser feito durante o failover. |
| [Criar ou atualizar um grupo de failover] / rest/api/sql/failovergroups/createorupdate) | Criar ou atualizar grupo de failover |
| [Excluir grupo de failover](/rest/api/sql/failovergroups/delete) | Remove o grupo de failover de saudação do servidor de saudação |
| [Failover (planejado)](/rest/api/sql/failovergroups/failover) | O failover do servidor de toothis de servidor principal atual hello. |
| [O Failover forçado permite a perda de dados](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |aflições através do servidor de toothis de servidor principal atual hello. Esta operação pode resultar em perda de dados. |
| [Obter grupo de failover](/rest/api/sql/failovergroups/get) | Obtém um grupo de failover. |
| [Listar grupos de failover pelo servidor](/rest/api/sql/failovergroups/listbyserver) | Lista os grupos de failover de saudação em um servidor. |
| [Atualizar grupo de failover](/rest/api/sql/failovergroups/update) | Atualiza um grupo de failover. |
|  | |

## <a name="next-steps"></a>Próximas etapas
* Para exemplos de scripts, consulte:
   - [Configurar e fazer failover de um banco de dados individual usando replicação geográfica ativa](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Configurar e fazer failover de um banco de dados em pool usando replicação geográfica ativa](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Configurar e realizar o failover de um grupo de failover para um banco de dados individual (versão prévia)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* Para obter uma visão geral e os cenários de continuidade dos negócios, confira [Visão geral da continuidade dos negócios](sql-database-business-continuity.md)
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md).
* toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups de iniciadas pelo serviço de saudação](sql-database-recovery-using-backups.md).
* toolearn sobre os requisitos de autenticação para um novo servidor primário e o banco de dados, consulte [segurança de banco de dados SQL após a recuperação de desastres](sql-database-geo-replication-security-config.md).

