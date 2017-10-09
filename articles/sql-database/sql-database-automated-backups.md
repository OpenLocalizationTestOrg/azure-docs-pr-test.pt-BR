---
title: "backups de automático, com redundância geográfica de banco de dados SQL aaaAzure | Microsoft Docs"
description: "O Banco de dados SQL cria automaticamente um backup de banco de dados local a cada poucos minutos e usa o armazenamento com redundância geográfica de acesso de leitura do Azure para redundância geográfica."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Saiba mais sobre backups automáticos de Banco de Dados SQL

Banco de dados SQL cria backups de banco de dados e usa a redundância geográfica de armazenamento com redundância geográfica de acesso de leitura do Azure (RA-GRS) tooprovide automaticamente. Esses backups são criados automaticamente e sem nenhum custo adicional. Você não precisa toodo nada toomake-los acontecem. Os backups de banco de dados são uma parte essencial de qualquer estratégia de recuperação de desastre e continuidade dos negócios, porque eles protegem seus dados contra exclusão ou corrupção acidentais. Se você quiser tookeep backups no seu próprio contêiner de armazenamento, você pode configurar uma política de retenção de backup de longo prazo. Para obter mais informações, consulte [Retenção de longo prazo](sql-database-long-term-retention.md).

## <a name="what-is-a-sql-database-backup"></a>O que é um backup de Banco de Dados SQL?

Banco de dados SQL usa o SQL Server tecnologia toocreate [completo](https://msdn.microsoft.com/library/ms186289.aspx), [diferencial](https://msdn.microsoft.com/library/ms175526.aspx), e [log de transações](https://msdn.microsoft.com/library/ms191429.aspx) backups. backups de log de transações Olá geralmente ocorrem a cada 5 a 10 minutos, com frequência de saudação com base no nível de desempenho de saudação e a quantidade de atividade de banco de dados. Os backups de log de transações com backups diferenciais e completos, permitem que você toorestore um toohello de point-in-time específico do banco de dados tooa mesmo servidor que hospeda o banco de dados de saudação. Quando você restaurar um banco de dados, Olá descobre serviço qual completo, diferencial e backups de log de transação necessário toobe restaurado.


Use esses backups para:

* Restaure um banco de dados tooa point-in-time dentro do período de retenção de saudação. Esta operação criará um novo banco de dados em Olá mesmo servidor como banco de dados original hello.
* Restaure um tempo de toohello excluído do banco de dados que foi excluído ou a qualquer momento dentro do período de retenção de saudação. banco de dados de saudação excluído só pode ser restaurado no hello mesmo servidor onde o banco de dados original Olá foi criado.
* Restaure uma região geográfica do banco de dados tooanother. Isso permite que você toorecover de desastres geográficas quando você não pode acessar o servidor e o banco de dados. Ele cria um novo banco de dados em qualquer servidor existente em qualquer lugar no Olá, mundo. 
* Restaure um banco de dados de um backup específico armazenado no cofre dos Serviços de Recuperação do Azure. Isso permite que você toorestore uma versão antiga do banco de dados de saudação toosatisfy uma solicitação de conformidade ou toorun uma versão antiga do aplicativo hello. Consulte [Retenção de longo prazo](sql-database-long-term-retention.md).
* tooperform uma restauração, consulte [restaurar o banco de dados de backups](sql-database-recovery-using-backups.md).

> [!NOTE]
> No armazenamento do Azure, o termo de saudação *replicação* refere-se a arquivos de toocopying de tooanother de um local. Do SQL *replicação de banco de dados* refere-se tookeeping toomultiple bancos de dados secundários sincronizados com o banco de dados primário. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Quanto armazenamento de backup é incluído sem custo adicional?
Banco de dados SQL fornece o too200% do armazenamento máximo de banco de dados configurado como armazenamento de backup sem custo adicional. Por exemplo, se você tiver uma instância de banco de dados Standard com tamanho provisionado de 250 GB, você terá 500 GB de espaço de armazenamento para backup sem custo adicional. Se seu banco de dados exceder Olá fornecido o armazenamento de backup, você pode escolher o período de retenção de saudação tooreduce entrando em contato com o suporte do Azure. Outra opção é toopay extra para armazenamento de backup que será cobrado na taxa padrão de acesso de leitura geograficamente redundantes (RA-GRS) hello. 

## <a name="how-often-do-backups-happen"></a>Com que frequência os backups ocorrem?
Os backups de banco de dados completos ocorrem semanalmente, os backups de banco de dados diferenciais geralmente ocorrem em horários determinados e os backups de log de transações geralmente ocorrem a cada 5 a 10 minutos. primeiro backup completo de saudação é agendado imediatamente após a criação de um banco de dados. Normalmente é concluída em 30 minutos, mas pode levar mais tempo quando o banco de dados de saudação é de tamanho significativo. Por exemplo, backup de saudação inicial pode levar mais tempo em um banco de dados restaurado ou uma cópia do banco de dados. Após o primeiro backup de completo hello, todos os outros backups sejam agendados automaticamente e gerenciados silenciosamente em segundo plano da saudação. tempo de saudação exato de todos os backups de banco de dados é determinado pela Olá serviço de banco de dados SQL de saldos de saudação geral carga de trabalho do sistema. 

replicação geográfica de armazenamento de backup de saudação ocorre com base no agendamento de replicação de armazenamento do Azure hello.

## <a name="how-long-do-you-keep-my-backups"></a>Por quanto tempo meus backups são armazenados?
Cada backup de banco de dados SQL tem um período de retenção com base no hello [da camada de serviço](sql-database-service-tiers.md) de banco de dados de saudação. período de retenção de saudação para um banco de dados do:


* A camada de serviço Básico é de 7 dias.
* Camada de serviço Standard é de 35 dias.
* Camada de serviço Premium é de 35 dias.

Se você reduzir o banco de dados de saudação padrão ou tooBasic de camadas de serviço Premium, backups de saudação são salvos por sete dias. Todos os backups existentes com mais de sete dias não estarão mais disponíveis. 

Se você atualizar o banco de dados de tooStandard de nível de serviço básico hello ou Premium, o banco de dados SQL mantém backups existentes até que eles sejam 35 dias. Isso armazena os backups novos à medida que eles ocorrem durante 35 dias.

Se você excluir um banco de dados, o banco de dados SQL mantém backups Olá no hello mesma maneira que faria para um banco de dados online. Por exemplo, vamos supor que você exclui um banco de dados Básico que tenha um período de retenção de sete dias. Um backup com quatro dias será salvo por mais três dias.

> [!IMPORTANT]
> Se você excluir hello Azure do SQL server que hospeda bancos de dados SQL, todos os bancos de dados que pertencem a toohello servidor também são excluídos e não podem ser recuperados. Você não pode restaurar um servidor excluído.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Como tooextend Olá backup período de retenção?
Se seu aplicativo requer que os backups de saudação estão disponíveis para o período de tempo você pode estender o período de retenção internas Olá Configurando a política de retenção de backup de longo prazo Olá para bancos de dados individuais (política LTR). Isso permite que você período de retenção de it criados de saudação do tooextend de anos de too10 tooup 35 dias. Para obter mais informações, consulte [Retenção de longo prazo](sql-database-long-term-retention.md).

Depois de adicionar Olá LTR política tooa banco de dados usando o portal do Azure ou API, backups de banco de dados completo semanal hello serão automaticamente copiado tooyour possui o serviço de cofre do Azure Backup. Se seu banco de dados for criptografado com backups de saudação TDE automaticamente são criptografados em repouso.  Olá Cofre de serviços excluirá automaticamente seus backups expiradas com base em seu carimbo de hora e hello política LTR.  Para que você não precisam de agendamento de backup toomanage hello ou preocupações sobre limpeza de saudação do hello arquivos antigos. Olá restauração API dá suporte a backups armazenados no hello cofre como cofre hello está em Olá mesma assinatura que o banco de dados SQL. Você pode usar Olá portal do Azure ou o PowerShell tooaccess esses backups.

> [!TIP]
> Para um tooguide como, consulte [configurar e a restauração da retenção de backup de longo prazo do banco de dados SQL](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>Os backups são criptografados?

Quando a TDE está habilitada para um banco de dados SQL do Azure, os backups também são criptografados. Todos os novos bancos de dados SQL do Azure são configurados com TDE habilitada por padrão. Para obter mais informações sobre a TDE, confira [Transparent Data Encryption com o Banco de Dados SQL do Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Próximas etapas

- Os backups de banco de dados são uma parte essencial de qualquer estratégia de recuperação de desastre e continuidade dos negócios, porque eles protegem seus dados contra exclusão ou corrupção acidentais. toolearn sobre Olá outras soluções de continuidade de negócios do Azure SQL Database, consulte [visão geral de continuidade de negócios](sql-database-business-continuity.md).
- toorestore tooa pontual usando Olá portal do Azure, consulte [restaurar banco de dados tooa ponto no tempo usando o portal do Azure de saudação](sql-database-recovery-using-backups.md).
- toorestore tooa ponto no tempo usando o PowerShell, consulte [restaurar o banco de dados tooa ponto no tempo usando o PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, gerenciem e restaurem de retenção de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure usando hello Azure portal, consulte [gerenciar usando o armazenamento de backup a longo prazo Olá portal do Azure](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, gerenciar e restaurar a partir de retenção de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure usando o PowerShell, consulte [gerenciar a retenção de backup a longo prazo, usando o PowerShell](sql-database-long-term-backup-retention-configure.md).
