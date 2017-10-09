---
title: 'TSQL: Iniciar failover para o Banco de Dados SQL do Azure | Microsoft Docs'
description: "Iniciar um failover planejado ou não planejado para o Banco de Dados SQL do Azure usando o Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Iniciar um failover planejado ou não planejado para o Banco de Dados SQL do Azure com o Transact-SQL

Este artigo mostra como tooinitiate failover tooa banco de dados SQL secundário usando Transact-SQL. tooconfigure replicação geográfica, consulte [configurar a replicação geográfica para o banco de dados do Azure SQL](sql-database-geo-replication-transact-sql.md).

tooinitiate failover, você precisa seguir hello:

* Um logon que seja DBManager em Olá primário
* Ter db_ownership do banco de dados local Olá que você irá replicar geograficamente
* Ser DBManager em toowhich de servidores de parceiro Olá você irá configurar a replicação geográfica
* A versão mais recente do SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> É recomendável que você sempre use Olá versão mais recente do Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Inicie um failover planejado, promovendo um banco de dados secundário toobecome Olá novo primário
Você pode usar o hello **ALTER DATABASE** instrução toopromote um banco de dados secundário toobecome Olá novo primário do banco de dados de modo planejado, rebaixar toobecome primária existente de saudação um secundário. Essa instrução é executada no banco de dados mestre no servidor lógico do banco de dados do Azure SQL Olá no qual Olá replicado geograficamente banco de dados secundário que está sendo promovido reside hello. Essa funcionalidade foi projetada para o failover planejado, como durante detalhada Olá DR e requer o que banco de dados primário Olá estar disponível.

saudação de comando executa Olá fluxo de trabalho a seguir:

1. Temporariamente o modo de toosynchronous replicação comutadores, fazendo com que todos os toobe de transações pendentes liberado toohello secundário e o bloqueio de todas as novas transações;
2. Comutadores Olá funções de dois bancos de dados de saudação na parceria de replicação geográfica hello.  

Esta sequência garante que Olá dois bancos de dados são sincronizados antes de alternar funções hello e, portanto, nenhuma perda de dados. Há um curto período durante o qual ambos os bancos de dados não estão disponíveis (em ordem de saudação de 0 segundos too25) enquanto a troca de funções hello. Se o banco de dados primário Olá tem vários bancos de dados secundários, o comando hello serão automaticamente reconfigure Olá novo primário outros secundários tooconnect toohello.  saudação de toda a operação deve levar menos de um minuto toocomplete em circunstâncias normais. Para saber mais, confira [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [Camadas de Serviço](sql-database-service-tiers.md).

Use Olá seguindo as etapas tooinitiate um failover planejado.

1. No Management Studio, conecte o servidor lógico do banco de dados do Azure SQL toohello replicado geograficamente banco de dados secundário reside.
2. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **mestre**e, em seguida, clique em **nova consulta**.
3. Use os seguintes Olá **ALTER DATABASE** função primária do toohello de banco de dados secundário de saudação do instrução tooswitch.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Clique em **Execute** toorun consulta de saudação.

> [!NOTE]
> Em casos raros, é possível que a operação de saudação não pode ser concluída e pode aparecer presa. Nesse caso, usuário Olá pode executar o comando para forçar o failover hello e aceitar a perda de dados.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Iniciar um failover não planejado do hello banco de dados primário toohello banco de dados secundário
Você pode usar o hello **ALTER DATABASE** instrução toopromote um banco de dados secundário toobecome Olá novo primário do banco de dados de forma não planejada, forçar o rebaixamento de saudação do toobecome primária existente de saudação um secundário em um momento quando Olá banco de dados primário não está mais disponível. Essa instrução é executada no banco de dados mestre no servidor lógico do banco de dados do Azure SQL Olá no qual Olá replicado geograficamente banco de dados secundário que está sendo promovido reside hello.

Essa funcionalidade destina-se a recuperação de desastres quando restaurando a disponibilidade do banco de dados de saudação é crítica e perda de dados é aceitável. Quando o failover forçado é invocado, Olá especificado banco de dados secundário se torna o banco de dados primário Olá imediatamente e começa a aceitar transações de gravação. Como Olá principal banco de dados original é capaz de tooreconnect com esse novo banco de dados primário, um backup incremental é tomado em Olá principal banco de dados original e Olá principal banco de dados antigo é feito em um banco de dados secundário Olá novo banco de dados primário; em seguida, é simplesmente uma réplica de sincronização do novo primário de saudação.

No entanto, porque a restauração pontual não tem suporte em bancos de dados secundários hello, se o usuário Olá deseja toorecover dados confirmados toohello antigo banco de dados primário que não tivesse sido toohello novo principal banco de dados replicado antes de ocorrer failover Olá forçado, Olá usuário precisará tooengage suporte toorecover essa perda de dados.

Se o banco de dados primário Olá tem vários bancos de dados secundários, o comando hello serão automaticamente reconfigure Olá novo primário outros secundários tooconnect toohello.

Use Olá seguindo as etapas tooinitiate um failover não planejado.

1. No Management Studio, conecte o servidor lógico do banco de dados do Azure SQL toohello replicado geograficamente banco de dados secundário reside.
2. Abra a pasta de bancos de dados hello, expanda Olá **bancos de dados do sistema** com o botão direito na pasta **mestre**e, em seguida, clique em **nova consulta**.
3. Use os seguintes Olá **ALTER DATABASE** função primária do toohello de banco de dados secundário de saudação do instrução tooswitch.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Clique em **Execute** toorun consulta de saudação.

> [!NOTE]
> Se o comando de saudação é emitido quando o primário e secundário estão online tornará primário antigo Olá Olá novo secundário imediatamente sem a sincronização de dados. Se for Olá primário transações de confirmação quando o comando Olá é emitido alguma perda de dados podem ocorrer.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Após o failover, certifique-se de requisitos de autenticação de saudação de seu servidor e banco de dados são definidos no novo primário de saudação. Para obter detalhes, consulte [Segurança do Banco de Dados SQL do Azure após a recuperação de desastre](sql-database-geo-replication-security-config.md).
* toolearn recuperação após um desastre usando replicação geográfica ativa, incluindo as etapas de recuperação de pré e pós- e executar uma simulação de recuperação de desastres, consulte [a recuperação de desastres](sql-database-disaster-recovery.md)
* Para ver uma postagem de blog de Sasha Nosov sobre a replicação geográfica ativa, confira [Destaque sobre novos recursos de replicação geográfica](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Para obter informações sobre a criação de nuvem aplicativos toouse replicação geográfica, consulte [criação de aplicativos de nuvem para continuidade de negócios usando a replicação geográfica](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Para obter informações sobre o uso da replicação geográfica ativa com pools elásticos, consulte [Estratégias de recuperação de desastre do pool elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Para obter uma visão geral sobre a continuidade dos negócios, confira [Visão geral de continuidade dos negócios](sql-database-business-continuity.md)

