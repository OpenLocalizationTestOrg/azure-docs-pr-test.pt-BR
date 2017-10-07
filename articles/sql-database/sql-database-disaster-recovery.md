---
title: "recuperação de desastres de banco de dados de aaaSQL | Microsoft Docs"
description: "Saiba como toorecover um banco de dados de uma interrupção do datacenter regional ou a falha com hello Azure SQL Database replicação geográfica e recursos de restauração geográfica."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Restaurar um banco de dados do SQL Azure ou failover tooa secundário
Banco de dados do SQL Azure oferece Olá recursos para a recuperação de uma interrupção a seguir:

* [Replicação geográfica ativa](sql-database-geo-replication-overview.md)
* [Restauração geográfica](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn sobre cenários de continuidade de negócios e recursos de saudação dando suporte a esses cenários, consulte [continuidade dos negócios](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Preparar-se para eventos de saudação de uma interrupção
Para o êxito da região de dados tooanother de recuperação usando replicação geográfica ativa ou backups com redundância geográfica, você precisa tooprepare um servidor em outro data center interrupção toobecome Olá novo servidor primário deve Olá necessário surgir bem como ter etapas bem definidas testado e documentado tooensure uma recuperação simples. Essas etapas de preparação incluem:

* Identifique o servidor lógico de saudação em outra região toobecome Olá novo servidor primário. Com replicação geográfica, essa será a pelo menos um e talvez cada um dos servidores secundários hello. Para a restauração geográfica, isso geralmente será um servidor de saudação [região emparelhada](../best-practices-availability-paired-regions.md) para região Olá na qual o banco de dados está localizado.
* Identificar e, opcionalmente, definir, regras de firewall no nível de servidor de saudação necessário em usuários tooaccess Olá novo banco de dados primário.
* Determine como você vai tooredirect usuários toohello novo servidor primário, como alterando cadeias de caracteres de conexão ou alterar as entradas DNS.
* Identificar e, opcionalmente, criar, Olá logons que devem estar presente no banco de dados mestre no servidor primário Olá Olá e certifique-se a que esses logons têm as permissões apropriadas no banco de dados mestre hello, se houver. Para obter mais informações, confira [SQL Database security after disaster recovery](sql-database-geo-replication-security-config.md)
* Identificar as regras de alerta que serão necessário toobe toomap atualizado toohello novo banco de dados primário.
* Configuração de auditoria do documento hello em Olá principal banco de dados atual
* Executar uma [análise de recuperação de desastre](sql-database-disaster-recovery-drills.md). toosimulate uma interrupção para restauração geográfica, você pode excluir ou renomear a falha de conectividade de aplicativo hello fonte banco de dados toocause. toosimulate uma interrupção de replicação geográfica ativa, você pode desabilitar o aplicativo da web hello ou máquina virtual conectada toohello banco de dados ou failover Olá banco de dados toocause aplicativo falhas de conectividade.

## <a name="when-tooinitiate-recovery"></a>Quando tooinitiate recuperação
operação de recuperação Olá afeta o aplicativo hello. Ele requer a alteração de cadeia de conexão SQL hello ou redirecionamento usando o DNS e pode resultar em perda de dados permanente. Portanto, ele deve ser feito apenas quando a interrupção de saudação for provavelmente toolast mais de objetivo de tempo de recuperação do aplicativo. Quando o aplicativo hello é implantado tooproduction devem executar o monitoramento regular da integridade do aplicativo hello e usar hello está garantido tooassert pontos que Olá recuperação de dados a seguir:

1. Falha de conectividade permanente do banco de dados do aplicativo da camada toohello hello.
2. Olá portal do Azure mostra um alerta sobre um incidente na região de saudação com grande impacto.
3. servidor de banco de dados do Azure SQL Hello está marcado como degradado.

Dependendo de responsabilidade de negócios seu aplicativo tolerância toodowntime e possíveis, você pode considerar Olá as opções de recuperação a seguir.

Saudação de uso [obter banco de dados recuperável](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) ponto de restauração replicado geograficamente tooget hello mais recente.

## <a name="wait-for-service-recovery"></a>Aguarde a recuperação de serviço
Olá equipes do Azure funcionam cuidadosamente disponibilidade do serviço toorestore como rapidamente possível, mas dependendo da causa raiz de saudação pode levar horas ou dias.  Se seu aplicativo pode tolerar tempo de inatividade significativo, que você pode simplesmente aguardar Olá toocomplete de recuperação. Nesse caso, nenhuma ação sua é necessária. Você pode ver o status atual do serviço Olá no nosso [painel de integridade do serviço Azure](https://azure.microsoft.com/status/). Após a recuperação de saudação da região de saudação de disponibilidade do aplicativo será restaurada.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Failover replicadas toogeo banco de dados secundário
Se o tempo de inatividade do aplicativo puder resultar em responsabilidade comercial, você deverá usar bancos de dados replicados geograficamente em seu aplicativo. Ele permite disponibilidade de restauração de tooquickly Olá aplicativos em uma região diferente no caso de uma interrupção. Saiba como muito[configurar a replicação geográfica](sql-database-geo-replication-portal.md).

disponibilidade de toorestore de saudação bancos de dados você precisa tooinitiate Olá failover toohello replicado geograficamente secundário usando um dos métodos de saudação com suporte.

Use uma saudação toofail guias a seguir sobre tooa replicado geograficamente banco de dados secundário:

* [Failover tooa secundário de replicação geográfica usando o Portal do Azure](sql-database-geo-replication-portal.md)
* [Failover tooa replicado geograficamente secundário usando o PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Failover tooa secundário de replicação geográfica usando o T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Recuperação usando a restauração geográfica
Se o tempo de inatividade do aplicativo não resulta em responsabilidade de negócios que você pode usar [restauração geográfica](sql-database-recovery-using-backups.md) como um método toorecover seus bancos de dados do aplicativo. Ele cria uma cópia do banco de dados de saudação de seu último backup com redundância geográfica.

## <a name="configure-your-database-after-recovery"></a>Configurar o banco de dados após a recuperação
Se você estiver usando replicação geográfica failover ou restauração geográfica toorecover de uma interrupção, você deve verificar se Olá conectividade toohello novos bancos de dados está configurado corretamente para que a função de aplicativo normal Olá poderá ser retomada. Isso é uma lista de verificação de tarefas tooget preparado para produção seu banco de dados recuperado.

### <a name="update-connection-strings"></a>Atualizar cadeias de conexão
Porque o banco de dados recuperado residem em um servidor diferente, você precisa tooupdate toopoint toothat servidor do seu aplicativo conexão cadeia de caracteres.

Para obter mais informações sobre como alterar as cadeias de caracteres de conexão, consulte o idioma de desenvolvimento apropriadas Olá para sua [biblioteca de conexão](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Configurar regras de firewall
Você precisa toomake-se de que Olá regras de firewall configuradas no servidor e na correspondência de banco de dados de saudação aqueles que foram configurados no servidor primário hello e banco de dados primário. Para saber mais, consulte [Como definir configurações de firewall (Banco de Dados SQL do Azure)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Configurar logons e usuários do banco de dados
Você precisa toomake-se de que todos os logons de saudação usados pelo seu aplicativo existem no servidor de saudação que está hospedando o banco de dados recuperado. Para saber mais, confira [Configuração de segurança para replicação geográfica](sql-database-geo-replication-security-config.md).

> [!NOTE]
> Você deve configurar e testar suas regras de firewall de servidor e logons (e suas permissões) durante uma análise de recuperação de desastre. Esses objetos de nível de servidor e suas configurações podem não estar disponíveis durante a interrupção de saudação.
> 
> 

### <a name="setup-telemetry-alerts"></a>Configurar alertas de telemetria
É necessário toomake se que as configurações de regra de alerta existentes são atualizados toomap toohello banco de dados e hello diferente servidor recuperado.

Para obter mais informações sobre regras de alerta de banco de dados, consulte [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) e [Acompanhar a integridade do serviço](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Habilitar a auditoria
Se a auditoria é necessário tooaccess seu banco de dados, você precisa tooenable auditoria após a recuperação de banco de dados de saudação. Para obter mais informações, consulte [Auditoria de banco de dados](sql-database-auditing.md).

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md)
* toolearn sobre continuidade design e recuperação de cenários de negócios, consulte [cenários de continuidade](sql-database-business-continuity.md)
* toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups de iniciadas pelo serviço de saudação](sql-database-recovery-using-backups.md)

