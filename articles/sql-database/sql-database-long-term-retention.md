---
title: backups de banco de dados do Azure SQL aaaStore para backup too10 anos | Microsoft Docs
description: Saiba como o banco de dados do SQL Azure oferece suporte a backups de armazenamento de backup too10 anos.
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Armazenar os backups de banco de dados de SQL do Azure para backup too10 anos
Muitos aplicativos têm regulamentares, de conformidade ou outros negócios fins que exigem backups de banco de dados tooretain além Olá 7-35 dias fornecidos pelo banco de dados do SQL Azure [backups automáticos](sql-database-automated-backups.md). Usando o recurso de retenção de backup de longo prazo de saudação, você pode armazenar os backups de banco de dados SQL em um cofre de serviços de recuperação do Azure para backup too10 anos. Você pode armazenar até too1, 000 bancos de dados por cofre. Você então pode selecionar qualquer backup no hello cofre toorestore-lo como um novo banco de dados.

> [!IMPORTANT]
> Retenção de backup de longo prazo está atualmente em visualização e está disponível em Olá seguintes regiões: Leste da Austrália, Sudeste da Austrália, Sul do Brasil, centro dos EUA, Ásia Oriental, Leste dos EUA, Leste dos EUA 2, Índia Central, Sul da Índia, Leste do Japão, oeste do Japão, Centro Norte dos EUA, Norte Centro Sul dos EUA, Europa, Sudeste da Ásia, Europa Ocidental e Oeste dos EUA.
>

> [!NOTE]
> Você pode habilitar o backup de bancos de dados too200 por cofre durante um período de 24 horas. É recomendável que você use um cofre separado para cada servidor toominimize Olá o impacto desse limite. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>Como funciona a retenção de backup de longo prazo do banco de dados SQL

Com a retenção de backup de longo prazo é possível associar um servidor de banco de dados SQL com um cofre dos Serviços de Recuperação do Azure. 

* Você deve criar cofre Olá Olá a mesma assinatura do Azure que criou o servidor SQL Olá no e no hello mesmo grupo de recursos e região geográfico. 
* Em seguida, você configura uma política de retenção para qualquer banco de dados. Olá política causas Olá semanal completo do banco de dados backups toobe copiados toohello Cofre de serviços de recuperação e mantidos por um período de retenção especificado hello (backup too10 anos). 
* Em seguida, pode restaurar banco de dados de saudação de qualquer um desses backups tooa novo banco de dados em qualquer servidor na assinatura de saudação. Armazenamento do Azure cria uma cópia de backup existente e cópia de saudação não tem nenhum impacto no desempenho no banco de dados existente do hello.

> [!TIP]
> Para um tooguide como, consulte [configurar e a restauração da retenção de backup de longo prazo do Azure SQL Database](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Habilitar retenção de backup de longo prazo

tooconfigure retenção de backup a longo prazo para um banco de dados:

1. Crie um cofre de serviços de recuperação do Azure no hello mesmo grupo de recursos, assinatura e região que seu servidor de banco de dados SQL. 
2. Registre o Cofre de toohello do servidor de saudação.
3. Crie uma política de proteção dos Serviços de Recuperação do Azure.
4. Aplica Olá proteção política toohello bancos de dados que exigem a retenção de backup de longo prazo.

tooconfigure, gerenciar e restaurar um banco de dados de retenção de backup de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure, siga um destes procedimentos hello:

* Usando Olá portal do Azure: clique em **retenção de backup de longo prazo**, selecione um banco de dados e, em seguida, clique em **configurar**. 

   ![Selecionar um banco de dados para retenção de backup a longo prazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* Usando o PowerShell: Ir muito[configurar e a restauração da retenção de backup de longo prazo do Azure SQL Database](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Restaurar um banco de dados que é armazenado com o recurso de retenção de backup de longo prazo de Olá

toorecover de um backup de retenção de backup de longo prazo:

1. Cofre de saudação lista onde Olá backup é armazenado.
2. Contêiner de saudação de lista é servidor lógico tooyour mapeada.
3. Fonte de dados lista Olá no cofre de saudação que é mapeada tooyour banco de dados.
4. Lista Olá pontos de recuperação que estão disponível toorestore.
5. Restaure o banco de dados de saudação do servidor de destino de toohello de ponto de recuperação de Olá dentro de sua assinatura.

tooconfigure, gerenciar e restaurar um banco de dados de retenção de backup de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure, siga um destes procedimentos hello:

* Usando Olá portal do Azure: ir muito[gerenciar usando o armazenamento de backup a longo prazo Olá portal do Azure](sql-database-long-term-backup-retention-configure.md). 

* Usando o PowerShell: Ir muito[gerenciar a retenção de backup a longo prazo, usando o PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Obter preços para a retenção de backup de longo prazo

Retenção de backup de longo prazo de um banco de dados SQL é cobrada de acordo com o toohello [serviços de backup do Azure, taxas de preço](https://azure.microsoft.com/pricing/details/backup/).

Após o servidor de banco de dados SQL Olá cofre toohello registrado, você é cobrado para Olá total de armazenamento que é usado por backups semanais hello, armazenados no cofre hello.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Exibir backups disponíveis que são armazenados na retenção de backup de longo prazo

tooconfigure, gerenciar e restaurar um banco de dados de retenção de backup de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure usando Olá portal do Azure, siga um destes procedimentos hello:

* Usando Olá portal do Azure: ir muito[gerenciar usando o armazenamento de backup a longo prazo Olá portal do Azure](sql-database-long-term-backup-retention-configure.md). 

* Usando o PowerShell: Ir muito[gerenciar a retenção de backup a longo prazo, usando o PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Desabilitar a retenção de longo prazo

o serviço de recuperação Olá automaticamente trata da limpeza de saudação dos backups com base em Olá fornecido a política de retenção. 

backups de saudação envio toostop para um cofre de toohello do banco de dados específico, remover a política de retenção de saudação do banco de dados.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> backups de saudação que já estão no cofre Olá não são afetados. Eles são excluídos automaticamente pelo serviço de recuperação de saudação quando seu período de retenção expira.

## <a name="long-term-backup-retention-faq"></a>FAQ sobre retenção de backup de longo prazo

**Posso excluir manualmente os backups específicos no cofre Olá?**

Não atualmente. cofre Olá limpa backups automaticamente quando o período de retenção de saudação expirou.

**Posso registrar meu toomore de backups do servidor toostore de um cofre?**

Não, você pode armazenar no momento um compartimento de tooonly de backups por vez.

**Posso ter um cofre e o servidor em assinaturas diferentes?**

Não, atualmente cofre hello e servidor devem estar no hello mesmo assinatura e grupo de recursos.

**Posso usar um cofre que criei em uma região diferente da região do servidor?**

Não, o cofre hello e servidor devem estar no hello mesmo toominimize de região copiar tempo e evitar a cobrança de tráfego.

**Quantos bancos de dados posso armazenar em um cofre?**

Atualmente, há suporte para backup too1, 000 bancos de dados por cofre. 

**Quantos cofres posso criar por assinatura?**

Você pode criar até too25 cofres por assinatura.

**Quantos bancos de dados posso configurar por dia e por cofre?**

Só é possível configurar até 200 bancos de dados por dia e por cofre.

**A retenção de backup de longo prazo funciona com pools elásticos?**

Sim. Qualquer banco de dados no pool de saudação pode ser configurado com a política de retenção de saudação.

**Tempo de saudação em que o backup de saudação é criado pode escolher?**

Não, o banco de dados SQL controla Olá agendamento de backup toominimize Olá impacto no desempenho de seus bancos de dados.

**Tenho a transparent data encryption habilitada para meu banco de dados. Posso usá-lo com o cofre Olá?** 

Sim, há suporte para a criptografia de dados transparente. Pode restaurar banco de dados de saudação do cofre Olá mesmo se o banco de dados original Olá não existe mais.

**O que acontece com backups Olá no cofre Olá se minha assinatura está suspensa?** 

Se sua assinatura for suspensa, podemos manter backups e bancos de dados existentes do hello. Novos backups não são copiados toohello cofre. Após você reativar a assinatura hello, o serviço de saudação retoma copiando backups toohello cofre. Seu cofre torna-se acessível toohello operações de restauração usando backups de saudação que foram copiados existe antes de saudação assinatura foi suspensa. 

**Posso obter acesso toohello arquivos de backup do banco de dados SQL para download ou restaurá-los toohello SQL server?**

Não no momento.

**É possível toohave vários agendamentos (diária, semanal, mensal, anual) dentro de uma política de retenção SQL.**

Não, atualmente vários agendamentos estão disponíveis apenas para backups de máquinas virtuais.

**E se configurarmos a retenção de backup de longo prazo em um banco de dados que é um banco de dados secundário de replicação geográfica ativa?**

Como não fazemos backups em réplicas, atualmente não há nenhuma opção para retenção de backup de longo prazo em bancos de dados secundários. No entanto, é importante para os usuários tooset a retenção de backup de longo prazo em um banco de dados secundário de replicação geográfica ativa por esses motivos:
* Quando ocorre um failover e o banco de dados de saudação se torna um banco de dados primário, podemos usar um backup completo, que é carregado toovault.
* Não há nenhum extra ao cliente toohello de custo para configurar a retenção de backup de longo prazo em um banco de dados secundário.

## <a name="next-steps"></a>Próximas etapas
Como os backups de banco de dados protegem os dados de danos ou exclusão acidental, eles são uma parte essencial de qualquer estratégia de recuperação de desastre e continuidade dos negócios. toolearn sobre Olá outras soluções de continuidade de negócios do banco de dados SQL, consulte [visão geral de continuidade de negócios](sql-database-business-continuity.md).
