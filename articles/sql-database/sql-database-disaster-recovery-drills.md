---
title: "banco de dados de recuperação de desastre do aaaSQL | Microsoft Docs"
description: "Saiba mais diretrizes e práticas recomendadas para usar manter toohelp detalhada de recuperação do banco de dados do Azure SQL tooperform desastres sua missão essenciais aos negócios aplicativos resilientes toofailures e interrupções."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Executar análise de recuperação de desastres
Recomenda-se a validação periódica da preparação do aplicativo para o fluxo de trabalho de recuperação. Verificando o comportamento do aplicativo hello e implicações de interrupção de perda de e/ou saudação de dados que o failover envolve é uma boa prática de engenharia. Isso também é uma exigência da maioria dos padrões do setor, como parte da certificação de continuidade dos negócios.

A execução de uma análise de recuperação de desastres é composta por:

* Simulação da interrupção da camada de dados
* Recuperando
* Validação da integridade do aplicativo após a recuperação

Dependendo de como você [seu aplicativo para continuidade de negócios](sql-database-business-continuity.md), análise de Olá Olá fluxo de trabalho tooexecute pode variar. Abaixo descrevemos práticas recomendadas de saudação realizando uma simulação de recuperação de desastres no contexto de saudação do banco de dados do SQL Azure.

## <a name="geo-restore"></a>Restauração geográfica
tooprevent Olá potencial perda de dados ao realizar uma simulação de recuperação de desastres, é recomendável executar análise hello usando um ambiente de teste ao criar uma cópia do ambiente de produção de hello e usá-lo fluxo de trabalho de failover do aplicativo do tooverify hello.

#### <a name="outage-simulation"></a>Simulação de interrupção
toosimulate Olá interrupção, você pode excluir ou renomear o banco de dados de origem de saudação. Isso causará falha de conectividade do aplicativo.

#### <a name="recovery"></a>Recuperação
* Executar restauração geográfica de saudação do banco de dados de saudação em um servidor diferente, conforme descrito [aqui](sql-database-disaster-recovery.md).
* Alteração Olá aplicativo configuração tooconnect toohello recuperado banco de dados e siga Olá [configurar um banco de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de saudação toocomplete.

#### <a name="validation"></a>Validação
* Olá completa drill verificando recuperação Olá aplicativos integridade post (incluindo cadeias de caracteres de conexão, logons, teste de funcionalidade básica ou outra parte de validações de procedimentos de aprovações de aplicativo padrão).

## <a name="geo-replication"></a>Replicação geográfica
Para um banco de dados que é protegido usando a análise de saudação de replicação geográfica exercício envolve toohello failover planejado banco de dados secundário. Olá failover planejado garante que hello primário e bancos de dados secundários Olá sincronizados quando a troca de funções hello. Ao contrário de Olá failover não planejado, esta operação não resulta na perda de dados, assim drill Olá pode ser executada no ambiente de produção de hello.

#### <a name="outage-simulation"></a>Simulação de interrupção
interrupção de saudação toosimulate, você pode desabilitar o aplicativo hello ou banco de dados de toohello de máquina virtual conectada. Isso resulta em falhas de conectividade Olá para clientes do hello da web.

#### <a name="recovery"></a>Recuperação
* Fazer se a configuração aplicativo hello em Olá DR região pontos toohello antiga secundária que se torna Olá totalmente acessível novo primário.
* Executar [failover planejado](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake Olá secundário um novo primário do banco de dados
* Siga Olá [configurar um banco de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de saudação toocomplete.

#### <a name="validation"></a>Validação
* Olá completa drill verificando recuperação Olá aplicativos integridade post (incluindo cadeias de caracteres de conexão, logons, teste de funcionalidade básica ou outra parte de validações de procedimentos de aprovações de aplicativo padrão).

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre cenários de continuidade de negócios, consulte [cenários de continuidade](sql-database-business-continuity.md)
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md)
* toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups de iniciadas pelo serviço de saudação](sql-database-recovery-using-backups.md)
* toolearn sobre as opções de recuperação mais rápidas, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md)  
