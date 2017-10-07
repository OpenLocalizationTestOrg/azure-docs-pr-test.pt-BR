---
title: "uma única tabela de backup de banco de dados SQL do aaaRestore | Microsoft Docs"
description: "Saiba como toorestore uma única tabela de backup de banco de dados SQL."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Como toorestore uma única tabela de um backup de banco de dados SQL
Você pode encontrar uma situação na qual você modificados acidentalmente alguns dados em um banco de dados SQL e agora quer toorecover Olá única afetados tabela. Este artigo descreve como toorestore uma única tabela em um banco de dados de uma saudação banco de dados SQL [backups automáticos](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Etapas de preparação: renomear a tabela hello e restaure uma cópia do banco de dados de saudação
1. Identifique Olá tabela no banco de dados SQL do Azure que você deseja tooreplace com cópia Olá restaurado. Use a tabela do Microsoft SQL Management Studio toorename hello. Por exemplo, renomeie a tabela hello como &lt;nome de tabela&gt;old.
   
   > [!NOTE]
   > tooavoid sendo bloqueado, certifique-se de que não há nenhuma atividade em execução em tabela Olá que você está renomeando. Se tiver problemas, lembre-se de executar esse procedimento durante uma janela de manutenção.
   >

2. Restaurar um backup de seu banco de dados tooa pontual que você deseja toorecover toousing Olá [restauraçãoPoint-In_Time](sql-database-recovery-using-backups.md#point-in-time-restore) etapas.
   
   > [!NOTE]
   > nome de saudação do banco de dados restaurado de saudação será no formato de carimbo de hora + DBName Olá; Por exemplo, **Adventureworks2012_2016-01-01T22-12Z**. Essa etapa não substitui o nome de banco de dados existente Olá no servidor de saudação. Esta é uma medida de segurança, e destina-se tooallow Olá de tooverify você restaurou o banco de dados antes de descartar o banco de dados atual e renomear Olá restaurado de banco de dados para uso em produção.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Copiando a tabela Olá da saudação restaurou o banco de dados usando a ferramenta de migração do banco de dados SQL Olá

1. Baixe e instale Olá [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).
2. Abra Olá SQL Database Migration Wizard no hello **Selecionar processo** , selecione **banco de dados em analisar/migrar**e, em seguida, clique em **próximo**.

   ![SQL Database Migration Wizard – Selecionar processo](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. Em Olá **conectar tooServer** caixa de diálogo caixa, aplicar Olá configurações a seguir:

   * Nome do servidor: **seu SQL Server**
   * Autenticação: **autenticação do SQL Server**
   * Logon: **seu logon**
   * Senha: **sua senha**
   * Banco de dados: **banco de dados mestre (listar todos os bancos de dados)**
   
   > [!NOTE]
   > Por padrão o assistente Olá salva suas informações de logon. Se não desejar que essas informações sejam salvas, selecione **Esquecer Informações de Logon**.
   >
   
     ![SQL Database Migration Wizard – Selecionar origem – etapa 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. Em Olá **Selecionar origem** caixa de diálogo, o nome do banco de dados selecione Olá restaurado da saudação **etapas de preparação** seção como sua fonte e, em seguida, clique em **próximo**.
   
    ![SQL Database Migration Wizard – Selecionar origem – etapa 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. Em Olá **escolher objetos** caixa de diálogo, selecione Olá **selecionar objetos de banco de dados específico** opção e selecione Olá table(or tables) que você deseja que o servidor de destino do toomigrate toohello.
   ![SQL Database Migration Wizard – Escolher objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. Em Olá **resumo do Assistente de Script** , clique em **Sim** quando você for avisado sobre esteja pronto toogenerate um script SQL. Você também tem Olá opção toosave Olá Script TSQL para uso posterior.
   ![SQL Database Migration Wizard – Resumo do Assistente para criação de script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. Em Olá **resumo de resultados** , clique em **próximo**.
   ![SQL Database Migration Wizard – Resumo dos resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. Em Olá **Conexão de servidor de destino de instalação** , clique em **conectar tooServer**e, em seguida, insira os detalhes de saudação da seguinte maneira:
   
   * **Nome do Servidor**: instância do servidor de destino
   * **Autenticação**: **autenticação do SQL Server**. Insira suas credenciais de logon.
   * **Banco de dados**: **banco de dados mestre (listar todos os bancos de dados)**. Essa opção lista todos os bancos de dados de saudação no servidor de destino de saudação.
     
     ![SQL Database Migration Wizard – Configurar conexão do servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Clique em **conectar**, selecione banco de dados de destino de saudação que você deseja toomove Olá tabela e, em seguida, clique em **próximo**. Isso deve terminar de executar o script hello gerado anteriormente, e você deverá ver Olá recentemente movido banco de dados de destino do tabela toohello copiado.

## <a name="verification-step"></a>Etapa de verificação

- Saudação de consulta e teste copiado recentemente tabela toomake-se de que dados saudação estão intactos. Após confirmação, você pode remover o formato de tabela Olá renomeado **etapas de preparação** seção. (por exemplo, &lt;nome da tabela&gt;_old).

## <a name="next-steps"></a>Próximas etapas
[Backups automáticos do Banco de Dados SQL](sql-database-automated-backups.md)

