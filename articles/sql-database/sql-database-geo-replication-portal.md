---
title: "Portal do Azure: replicação geográfica do Banco de Dados SQL | Microsoft Docs"
description: "Configurar a replicação geográfica para o banco de dados do SQL Azure hello portal do Azure e iniciar failover"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Configurar a replicação geográfica ativa para o banco de dados do SQL Azure hello portal do Azure e iniciar failover

Este artigo mostra como tooconfigure replicação geográfica ativa para banco de dados SQL em Olá [portal do Azure](http://portal.azure.com) e tooinitiate failover.

failover de tooinitiate com hello portal do Azure, consulte [iniciar um failover planejado ou não planejado para o banco de dados do SQL Azure com hello portal do Azure](sql-database-geo-replication-portal.md).

tooconfigure replicação geográfica usando Olá portal do Azure, você precisará Olá recursos a seguir:

* Um banco de dados do SQL Azure: banco de dados primário Olá que você deseja tooreplicate tooa região geográfica diferente.

> [!Note]
Replicação geográfica deve estar entre bancos de dados em Olá mesma assinatura.

## <a name="add-a-secondary-database"></a>Adicionar um banco de dados secundário
Olá etapas a seguir criam um novo banco de dados secundário em uma parceria de replicação geográfica.  

tooadd um banco de dados secundário, você deve ser o proprietário da assinatura hello ou coproprietário.

banco de dados secundário Olá Olá mesmo nome como o banco de dados primário hello e tem, por padrão, Olá mesmo nível de serviço. banco de dados secundário Olá pode ser um único banco de dados ou um banco de dados em um pool Elástico. Para obter mais informações, consulte [Camadas de serviço](sql-database-service-tiers.md).
Após Olá secundário é criado e propagado, dados começam a replicar de saudação banco de dados primário toohello novo banco de dados secundário.

> [!NOTE]
> Se o banco de dados de parceiro Olá já existe (por exemplo, em decorrência de encerrar um relacionamento de replicação geográfica anterior) Olá falhará.
> 

1. Em Olá [portal do Azure](http://portal.azure.com), procurar toohello banco de dados que você deseja tooset para replicação geográfica.
2. Na página de banco de dados do SQL hello, selecione **georeplicação**e, em seguida, selecione Olá região toocreate Olá banco de dados secundário. Você pode selecionar qualquer região diferente de região Olá hospeda o banco de dados primário hello, mas é recomendável Olá [região emparelhada](../best-practices-availability-paired-regions.md).
   
    ![Configurar a replicação geográfica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Selecione ou configurar o servidor de saudação e preços do banco de dados secundário hello.
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/create-secondary.png)
4. Opcionalmente, você pode adicionar um pool Elástico do banco de dados secundário tooan. toocreate Olá banco de dados secundário em um pool, clique em **pool Elástico** e selecione um pool no servidor de destino de saudação. Um pool já deve existir no servidor de destino de saudação. Esse fluxo de trabalho não cria um pool.
5. Clique em **criar** tooadd Olá secundário.
6. banco de dados secundário Olá é criado e começa a saudação processo de preparação.
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/seeding0.png)
7. Quando Olá propagação processo for concluído, o banco de dados secundário Olá exibe seu status.
   
    ![Propagação concluída](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Iniciar um failover

banco de dados secundário Olá pode ser desligados toobecome Olá primário.  

1. Em Olá [portal do Azure](http://portal.azure.com), procurar banco de dados primário na parceria de replicação geográfica Olá toohello.
2. Na folha de banco de dados SQL hello, selecione **todas as configurações** > **georeplicação**.
3. Em Olá **SECUNDÁRIOS** lista, selecione Olá banco de dados toobecome Olá novo primário e clique em **Failover**.
   
    ![Failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Clique em **Sim** toobegin Olá failover.

comando Olá imediatamente alterna o banco de dados secundário Olá na função primária hello. 

Há um curto período durante o qual ambos os bancos de dados não estão disponíveis (em ordem de saudação de 0 segundos too25) enquanto a troca de funções hello. Se o banco de dados primário Olá tem vários bancos de dados secundários, o comando Olá automaticamente configura Olá novo primário outros secundários tooconnect toohello. saudação de toda a operação deve levar menos de um minuto toocomplete em circunstâncias normais. 

> [!NOTE]
> Esse comando é projetado para rápida recuperação de banco de dados de saudação em caso de uma interrupção. Ele dispara o failover sem sincronização de dados (failover forçado).  Se Olá primário está online e confirmar transações quando o comando Olá é emitido alguma perda de dados pode ocorrer. 
> 
> 

## <a name="remove-secondary-database"></a>Remover banco de dados secundário
Esta operação permanentemente encerra Olá replicação toohello banco de dados secundário e alterações Olá função do banco de dados de leitura-gravação regular Olá tooa secundário. Se Olá conectividade toohello banco de dados secundário for interrompido, o comando Olá terá êxito, mas Olá secundário faz não tornam-se leitura / gravação até depois que a conectividade é restaurada.  

1. Em Olá [portal do Azure](http://portal.azure.com), procurar banco de dados primário na parceria de replicação geográfica Olá toohello.
2. Na página de banco de dados do SQL hello, selecione **georeplicação**.
3. Em Olá **SECUNDÁRIOS** lista, Olá selecione banco de dados tooremove da parceria de replicação geográfica hello.
4. Clique em **Parar Replicação**.
   
    ![Remover secundário](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Uma janela de confirmação é aberta. Clique em **Sim** tooremove o banco de dados de saudação da parceria de replicação geográfica hello. (Defini-lo tooa o banco de dados de leitura / gravação não faz parte de qualquer replicação.)

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a replicação geográfica, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md).
* Para obter uma visão geral e os cenários de continuidade dos negócios, consulte [Visão geral da continuidade dos negócios](sql-database-business-continuity.md).

