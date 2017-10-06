---
title: "continuidade de negócios aaaCloud - recuperação de banco de dados - banco de dados SQL | Microsoft Docs"
description: "Saiba como o Banco de Dados SQL do Azure dá suporte para a continuidade dos negócios em nuvem e para a recuperação de banco de dados, além de ajudar a manter os aplicativos em nuvem críticos em execução."
keywords: "continuidade dos negócios, continuidade dos negócios em nuvem, recuperação de desastre do banco de dados, recuperação de banco de dados"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Visão geral da continuidade dos negócios com o Banco de Dados SQL do Azure

Esta visão geral descreve recursos Olá que o banco de dados do SQL Azure fornece continuidade dos negócios e recuperação de desastres. Saiba mais sobre as opções, recomendações e tutoriais para a recuperação de eventos de interrupção que podem causar perda de dados ou toobecome seu banco de dados e o aplicativo não está disponível. Saiba quais toodo quando um erro de usuário ou aplicativo afeta a integridade dos dados, uma região do Azure tem uma interrupção ou manutenção do seu aplicativo requer.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Recursos de banco de dados SQL que você pode usar tooprovide continuidade de negócios

O Banco de Dados SQL fornece vários recursos de continuidade dos negócios, incluindo backups automatizados e replicação opcional do banco de dados. Cada um deles tem características diferentes para o ERT (tempo de recuperação estimado) e para a perda potencial de dados em transações recentes. Depois de compreender essas opções, você poderá escolher entre elas e, na maioria dos cenários, usá-las simultaneamente em cenários diferentes. À medida que desenvolve seu plano de continuidade de negócios, você precisa toounderstand Olá tempo máximo aceitável para o aplicativo hello totalmente recupera após o evento de interrupção Olá - esse é o objetivo de tempo de recuperação (RTO). Você também precisa toounderstand quantidade máxima de saudação do aplicativo de saudação de atualizações (intervalo) de dados recente pode tolerar perda durante a recuperação após o evento de interrupção Olá - esse é o objetivo de ponto de recuperação (RPO).

Olá a seguinte tabela compara hello ERTER e RPO para cenários mais comuns de saudação três.

| Recurso | Camada básica | Camada padrão | Camada premium |
| --- | --- | --- | --- |
| Recuperação Pontual do backup |Qualquer ponto de restauração dentro de 7 dias |Qualquer ponto de restauração dentro de 35 dias |Qualquer ponto de restauração dentro de 35 dias |
| Restauração geográfica de backups replicados geograficamente |ERT < 12h, RPO < 1h |ERT < 12h, RPO < 1h |ERT < 12h, RPO < 1h |
| Restaurar Cofre de Backup do Azure |ERT < 12h, RPO < 1 semana |ERT < 12h, RPO < 1 semana |ERT < 12h, RPO < 1 semana |
| Replicação geográfica ativa |ERT < 30s, RPO < 5s |ERT < 30s, RPO < 5s |ERT < 30s, RPO < 5s |

### <a name="use-database-backups-toorecover-a-database"></a>Usar backups de banco de dados toorecover um banco de dados

Banco de dados SQL executa automaticamente uma combinação de backups de banco de dados completo semanalmente, backups de banco de dados diferencial por hora e a transação de backups de log a cada cinco-dez minutos tooprotect sua empresa contra perda de dados. Esses backups são armazenados no armazenamento com redundância geográfica para 35 dias para bancos de dados em camadas de serviço Standard e Premium Olá e 7 dias para bancos de dados na camada de serviço básico de saudação. Para saber mais, consulte [Camadas de serviço](sql-database-service-tiers.md). Se o período de retenção Olá para a camada de serviço não atender a seus requisitos de negócios, você pode aumentar o período de retenção Olá [alterar a camada de serviço Olá](sql-database-service-tiers.md). Olá backups completo e diferencial de banco de dados também são replicado tooa [Datacenter emparelhado](../best-practices-availability-paired-regions.md) para proteção contra uma paralisação do data center. Para saber mais, consulte [backups de banco de dados automáticos](sql-database-automated-backups.md).

Se o período de retenção internas de saudação não é suficiente para o seu aplicativo, você pode estendê-lo ao configurar uma política de retenção de longo prazo de banco de dados. Para saber mais, confira [Retenção de longo prazo](sql-database-long-term-retention.md).

Você pode usar esses backups de automático do banco de dados toorecover um banco de dados de vários eventos de interrupção, tanto no seu data center e o Centro de dados tooanother. Usando backups de banco de dados automática, Olá estimado tempo de recuperação depende de vários fatores, incluindo o número total de saudação de bancos de dados de recuperação da saudação mesmo região em Olá ao mesmo tempo, Olá tamanho do banco de dados, tamanho do log de transações Olá e largura de banda de rede. tempo de recuperação de saudação normalmente é menor que 12 horas. Ao recuperar a região de dados de tooanother, Olá perda de dados é hora de too1 limitado pelo armazenamento com redundância geográfica de saudação de backups de banco de dados diferencial por hora.

> [!IMPORTANT]
> toorecover usando backups automáticos, você deve ser um membro da função de Colaborador do SQL Server de saudação ou proprietário da assinatura Olá - consulte [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md). Você pode recuperar usando Olá portal do Azure, PowerShell ou Olá API REST. Você não pode usar o Transact-SQL.
>

Use os backups automatizados como o mecanismo de continuidade e recuperação dos negócios se seu aplicativo:

* Não for considerado crítico.
* Não tem um SLA associado - um tempo de inatividade de 24 horas ou mais não resulta em responsabilidade financeira.
* Tem uma baixa taxa de alteração de dados (baixas transações por hora) e a perda de tooan hora de alteração é uma perda de dados aceitável.
* Seja suscetível aos custos.

Se você precisar de uma recuperação mais rápida, use a [replicação geográfica ativa](sql-database-geo-replication-overview.md) (discutida a seguir). Se você precisar toobe toorecover capaz de dados de um período mais de 35 dias, use [retenção de backup de longo prazo](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Use active replicação geográfica e o failover automático grupos (em visualização) tooreduce recuperação tempo e o limite de perda de dados associada a uma recuperação

Além disso toousing backups de banco de dados para recuperação banco de dados se ocorrer uma interrupção dos negócios, você pode usar [replicação geográfica ativa](sql-database-geo-replication-overview.md) tooconfigure toohave um banco de dados para cima toofour legível bancos de dados secundários em regiões de saudação do seu Escolha. Esses bancos de dados secundários são mantidos em sincronizado com o banco de dados primário hello usando um mecanismo de replicação assíncrona. Esse recurso é usado tooprotect contra interrupção dos negócios se ocorrer uma paralisação do data center ou durante uma atualização do aplicativo. Replicação geográfica ativa também pode ser usado tooprovide melhor desempenho de consulta para consultas somente leitura toogeographically distribuído usuários.

tooenable automatizada e failover transparente, você deve organizar seus bancos de dados replicada geograficamente em grupos usando Olá [failover automático grupo](sql-database-geo-replication-overview.md) recurso do banco de dados do SQL (na visualização).

Se o banco de dados primário Olá fica offline inesperadamente ou se precisar tootake offline para atividades de manutenção, você pode promover um principal de saudação toobecome secundário (também chamado de um failover) e configurar rapidamente primário do aplicativos tooconnect toohello promovido. Se seu aplicativo estiver se conectando a bancos de dados toohello usando Olá ouvinte de grupo de failover, configuração de cadeia de caracteres de conexão toochange Olá SQL após o failover não é necessário. Com um failover planejado, não há nenhuma perda de dados. Com um failover não planejado, pode haver alguns pequena quantidade de perda de dados muito recente transações devido a natureza toohello de replicação assíncrona. Usando grupos de failover automático (em visualização), você pode personalizar Olá failover política toominimize Olá potencial perda de dados. Após um failover, você pode posteriormente failback - plano acordo de tooa ou quando Olá Datacenter volta a ficar online. Em todos os casos, os usuários enfrentar uma pequena quantidade de tempo de inatividade e precisam tooreconnect.

> [!IMPORTANT]
> toouse replicação geográfica e grupos de failover automático (em visualização), você deve ser proprietário da assinatura de hello ou ter permissões administrativas no SQL Server. Você pode configurar e fazer failover usando Olá portal do Azure, o PowerShell ou Olá API REST usando permissões de assinatura do Azure ou usando o Transact-SQL com permissões do SQL Server.
> 

Use a replicação geográfica ativa e os grupos de failover automático (em versão prévia), caso seu aplicativo atenda a qualquer um desses critérios:

* Seja crítico.
* Tenha um SLA (Contrato de Nível de Serviço) que não permita um tempo de inatividade de 24 horas ou superior.
* O tempo de inatividade pode resultar em responsabilidade financeira.
* Tenha uma alta taxa de alteração de dados e que a perda de uma hora de dados não seja aceitável.
* custo adicional de saudação de replicação geográfica é inferior a responsabilidade de financeiro potencial Olá e perda associada de negócios.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Recuperar um banco de dados após um erro de usuário ou de aplicativo
*Ninguém é perfeito! Um usuário pode acidentalmente excluir alguns dados, remover uma tabela importante inadvertidamente ou até mesmo um banco de dados inteiro. Ou, um aplicativo pode substituir os dados bons acidentalmente com dados incorretos devido a falhas de aplicativo tooan.

Neste cenário, estas são as opções de recuperação.

### <a name="perform-a-point-in-time-restore"></a>Executar uma recuperação pontual
Você pode usar o hello automatizada backups toorecover uma cópia do seu tooa de banco de dados conhecido bom ponto no tempo, desde que a hora está no período de retenção do banco de dados de saudação. Depois de restaurar banco de dados de Olá, você pode substituir o banco de dados original do hello com banco de dados restaurado de saudação ou copiar dados saudação necessário dos dados de Olá restaurado no banco de dados original Olá. Se o banco de dados de saudação usa replicação geográfica ativa, é recomendável copiar dados de Olá necessário de cópia Olá restaurado no banco de dados original hello. Se você substituir o banco de dados original Olá com banco de dados de saudação restaurado, você precisa tooreconfigure e ressincronizar a replicação geográfica (que pode levar algum tempo para um banco de dados grande).

Para obter mais informações e para obter etapas detalhadas para a restauração de um ponto de tooa do banco de dados no momento usando Olá portal do Azure ou usando o PowerShell, consulte [restauração point-in-time](sql-database-recovery-using-backups.md#point-in-time-restore). Você não pode recuperar usando o Transact-SQL.

### <a name="restore-a-deleted-database"></a>Restaurar um banco de dados excluído
Se o banco de dados de saudação é excluído, mas servidor lógico Olá não foi excluído, você pode ponto de restauração Olá excluído banco de dados toohello em que ele foi excluído. Isso restaura um toohello de backup do banco de dados mesmo lógico do SQL server do qual ele foi excluído. Você pode restaurá-lo usando o nome original da saudação ou fornecer um novo nome ou o banco de dados de saudação restaurado.

Para obter mais informações e para obter etapas detalhadas para restaurar um banco de dados excluído usando Olá portal do Azure ou usando o PowerShell, consulte [restaurar um banco de dados excluído](sql-database-recovery-using-backups.md#deleted-database-restore). Você não pode restaurar usando o Transact-SQL.

> [!IMPORTANT]
> Se o servidor lógico Olá for excluído, você não pode recuperar um banco de dados excluído.
>
>

### <a name="restore-from-azure-backup-vault"></a>Restaurar Cofre de Backup do Azure
Se a perda de dados Olá ocorreu fora do período de retenção atual Olá para backups automatizados e seu banco de dados está configurado para retenção de longo prazo, você pode restaurar de um backup semanal no novo banco de dados do Cofre de Backup do Azure tooa. Neste ponto, você pode substituir o banco de dados original do hello com banco de dados restaurado de saudação ou copiar dados de Olá necessário do banco de dados de saudação restaurado no banco de dados original hello. Se você precisar tooretrieve uma versão antiga do que a atualização do banco de dados anterior tooa aplicativo principal, atender uma solicitação de auditores ou uma ordem legal, que você pode criar um banco de dados usando um backup completo salvo em Olá Cofre de Backup do Azure.  Para obter mais informações, consulte [Retenção de longo prazo](sql-database-long-term-retention.md).

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Recuperar uma região de tooanother do banco de dados de uma paralisação de centro de dados regional do Azure
<!-- Explain this scenario -->

Embora seja raro, um data center do Azure pode ter uma interrupção. Quando uma interrupção ocorre, ela causa uma parada nos negócios, que pode durar alguns minutos ou horas.

* Uma opção é toowait para sua toocome de banco de dados online novamente quando sobre Olá paralisação do data center. Isso funciona para aplicativos que podem toohave Olá banco de dados offline. Por exemplo, um projeto de desenvolvimento ou avaliação gratuita não é necessário toowork em constantemente. Quando um data center tem uma interrupção, você não souber quanto tempo pode durar interrupção hello, portanto essa opção só funcionará se seu banco de dados não é necessário para um pouco.
* Outra opção é tooeither falha em região de dados de tooanother se você estiver usando replicação geográfica ativa ou Olá recuperar um banco de dados usando backups de banco de dados com redundância geográfica (restauração geográfica). O failover demora apenas alguns segundos, enquanto a recuperação de banco de dados de backups demora horas.

Quando você executa uma ação, quanto tempo você leva toorecover e quanto a perda de dados incorre em depende de como você decidir toouse esses recursos de continuidade de negócios em seu aplicativo. Na verdade, você pode escolher toouse uma combinação de backups de banco de dados e replicação geográfica dependendo dos seus requisitos de aplicativo. Para uma discussão sobre as considerações de design do aplicativo para bancos de dados independentes e pools elásticos que usam esses recursos de continuidade de negócios, consulte [Criar um aplicativo para recuperação de desastre na nuvem](sql-database-designing-cloud-solutions-for-disaster-recovery.md) e [Estratégias de recuperação de desastre para Pool Elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

Olá seções a seguir fornecem uma visão geral da saudação etapas toorecover usando backups de banco de dados ou de replicação geográfica ativa. Para etapas detalhadas, incluindo o planejamento de requisitos, etapas de recuperação de postagem e obter informações sobre como toosimulate tooperform uma interrupção uma recuperação de desastres detalhada, consulte [recuperar um banco de dados SQL de uma paralisação](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Prepare-se para uma interrupção
Independentemente do recurso de continuidade de negócios Olá que você usar, você deve:

* Identifique e prepare o servidor de destino hello, incluindo as regras de firewall de nível de servidor, logons e permissões em nível de banco de dados mestre.
* Determinar como tooredirect clientes e aplicativos de cliente toohello servidor novo
* Documentar outras dependências, como as configurações e alertas de auditoria

Se você não se preparar corretamente, colocar seus aplicativos online após um failover ou uma recuperação de banco de dados exigirá um tempo adicional e, provavelmente, a solução de problemas também será exigida em um momento de estresse, ou seja, uma combinação ruim.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Failover tooa replicado geograficamente banco de dados secundário
Se você estiver usando a replicação geográfica ativa e os grupos de failover automático (em versão prévia) como mecanismos de recuperação, você poderá configurar uma política de failover automático ou usar o [failover manual](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Uma vez iniciada, Olá failover causas Olá secundário toobecome Olá novo primário e pronto toorecord novas transações e responder tooqueries - com perda mínima de dados para dados Olá ainda não foram replicadas. Para obter informações sobre como criar o processo de failover hello, consulte [criar um aplicativo de nuvem para recuperação de desastres](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Quando o Datacenter Olá volta a ficar online primárias antigo Olá automaticamente reconectar toohello novo primário e se tornam bancos de dados secundários. Se você precisar região original do toorelocate Olá toohello back primário, você pode iniciar um failover planejado manualmente (failback). 
> 

### <a name="perform-a-geo-restore"></a>Executar uma restauração geográfica
Se você estiver usando backups automatizados com a replicação de armazenamento com redundância geográfica como o mecanismo de recuperação, [inicie uma recuperação de banco de dados usando a restauração geográfica](sql-database-disaster-recovery.md#recover-using-geo-restore). Recuperação geralmente ocorre dentro de 12 horas - com perda de dados de backup tooone hora determinada por quando hello última hora backup diferencial feito e replicado. Até concluir a recuperação de Olá, Olá banco de dados toorecord não é possível nenhuma transação ou responde a consultas de tooany. Enquanto isso restaura um banco de dados toohello último disponível ponto no tempo, restaurar Olá geográfica secundário tooany ponto no tempo não há atualmente suporte.

> [!NOTE]
> Se o Datacenter Olá volta a ficar online antes de alternar o aplicativo de banco de dados recuperado toohello, você pode cancelar a recuperação hello.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Executar pós-failover / tarefas de recuperação
Após a recuperação de um dos mecanismos de recuperação, você deve executar Olá tarefas adicionais a seguir antes dos usuários e aplicativos de backup e em execução:

* Clientes de redirecionamento de cliente aplicativos toohello novo servidor e banco de dados restaurado
* Certifique-se de que as regras de firewall de nível de servidor apropriado estão em vigor para os usuários tooconnect (ou use [firewalls de nível de banco de dados](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* Verificar se os logons apropriados e as permissões nível de banco de dados mestre estão em vigor (ou usar os [usuários independentes](https://msdn.microsoft.com/library/ff929188.aspx))
* Configurar a auditoria, conforme apropriado
* Configurar os alertas, conforme apropriado

## <a name="upgrade-an-application-with-minimal-downtime"></a>Atualize um aplicativo com tempo de inatividade mínimo
Às vezes, um aplicativo deve ser colocado offline devido à manutenção planejada, como uma atualização do aplicativo. [Gerenciar atualizações de aplicativo](sql-database-manage-application-rolling-upgrade.md) descreve como toouse tooenable de replicação geográfica ativa sem interrupção atualizações do tempo de inatividade sua nuvem aplicativo toominimize durante as atualizações e fornecer um caminho de recuperação se algo der errado. 

## <a name="next-steps"></a>Próximas etapas
Para uma discussão sobre as considerações de design de aplicativo para bancos de dados independentes em pools elásticos, confira [Criar um aplicativo para recuperação de desastre na nuvem](sql-database-designing-cloud-solutions-for-disaster-recovery.md) e [Estratégias de recuperação de desastre para Pool Elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
