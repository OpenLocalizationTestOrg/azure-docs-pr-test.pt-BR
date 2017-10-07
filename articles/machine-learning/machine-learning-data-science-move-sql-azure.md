---
title: "dados de aaaMove tooan banco de dados SQL Azure para o aprendizado de máquina do Azure | Microsoft Docs"
description: Criar tabela de SQL e carregar dados tooSQL tabela
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure
Este tópico descreve as opções de saudação de movimentação de dados de arquivos simples (formatos CSV ou TSV) ou de dados armazenados em um banco de dados local do SQL Server tooan SQL Azure. Essas tarefas para mover dados na nuvem toohello fazem parte da saudação processo de ciência de dados de equipe.

Para um tópico que descreve as opções de saudação para tooan movimentação de dados locais do SQL Server para o aprendizado de máquina, consulte [mover dados tooSQL Server em uma máquina virtual do Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

a seguir Olá **menu** links tootopics que descrevem como dados tooingest em ambientes de destino onde os dados saudação podem ser armazenados e processados durante Olá processo de ciência de dados da equipe (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Olá tabela a seguir resume as opções de saudação para mover dados tooan banco de dados do SQL Azure.

| <b>FONTE</b> | <b>DESTINO: Banco de Dados SQL do Azure</b> |
| --- | --- |
| <b>Arquivo simples (CSV ou TSV formatado)</b> |<a href="#bulk-insert-sql-query">Consulta SQL de inserção em massa |
| <b>SQL Server local</b> |1. <a href="#export-flat-file">Exportar arquivo de tooFlat<br> 2. <a href="#insert-tables-bcp">Assistente de migração de Banco de Dados SQL<br> 3. <a href="#db-migration">Backup e restauração do banco de dados<br> 4. <a href="#adf">Azure Data Factory (ADF) |

## <a name="prereqs"></a>Pré-requisitos
procedimentos de saudação descritos aqui exigem que você tenha:

* Uma **assinatura do Azure**. Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Uma **conta de armazenamento do Azure**. Você pode usar uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial. Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo. Depois que você criou a conta de armazenamento hello, você precisa de conta de saudação tooobtain chave usada tooaccess armazenamento de saudação. Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Acesso tooan **banco de dados do SQL Azure**. Se você deve configurar um banco de dados SQL do Azure, [guia de Introdução ao banco de dados SQL do Microsoft Azure](../sql-database/sql-database-get-started.md) fornece informações sobre como tooprovision uma nova instância de um banco de dados do SQL Azure.
* **Azure PowerShell** instalado e configurado localmente. Para obter instruções, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

**Dados**: processos de migração de saudação são demonstrados usando Olá [NYC táxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/). Olá NYC táxi conjunto de dados contém informações sobre os dados de processamento e feiras e está disponível no armazenamento de BLOBs do Azure: [NYC táxi dados](http://www.andresmh.com/nyctaxitrips/). Um exemplo e uma descrição desses arquivos são fornecidos na [Descrição do Conjunto de Dados de Viagens de Táxi de NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Você pode adaptar Olá procedimentos tooa aqui descrito conjunto de seus próprios dados ou execute as etapas de saudação conforme descrito usando Olá NYC táxi dataset. Olá tooupload NYC táxi de conjunto de dados em seu banco de dados do SQL Server local, execute o procedimento de saudação descrito no [dados de importação em massa no banco de dados do SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Essas instruções são para um SQL Server em uma máquina Virtual do Azure, mas o procedimento Olá para carregar toohello local SQL Server é Olá mesmo.

## <a name="file-to-azure-sql-database"></a>Movimentação de dados de um banco de dados do arquivo simples origem tooan SQL Azure
Dados em arquivos simples (CSV ou TSV formatado) podem ser um banco de dados do SQL Azure tooan movida usando uma consulta de SQL de inserção em massa.

### <a name="bulk-insert-sql-query"></a> Consulta SQL de inserção em massa
etapas de saudação para procedimento hello usando Olá consulta de SQL de inserção em massa são semelhante toothose abordado nas seções de saudação para mover dados de uma fonte de arquivo simples tooSQL Server em uma VM do Azure. Para obter detalhes, consulte [Consulta SQL de inserção em massa](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Movimentação de dados de banco de dados do SQL Azure tooan local do SQL Server
Se os dados de origem Olá estiver armazenados em um local no SQL Server, há várias possibilidades de movimentação Olá dados tooan Azure banco de dados SQL:

1. [Exportar arquivo de tooFlat](#export-flat-file)
2. [Assistente de Migração de Banco de Dados SQL](#insert-tables-bcp)
3. [Backup e restauração de banco de dados](#db-migration)
4. [Azure Data Factory](#adf)

etapas para Olá três primeiros Hello são muito semelhantes seções toothose [mover dados tooSQL Server em uma máquina virtual do Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) que abrangem esses mesmos procedimentos. Links toohello apropriadas seções desse tópico são fornecidas nos Olá instruções a seguir.

### <a name="export-flat-file"></a>Exportar arquivo de tooFlat
etapas de Olá para esse arquivo de plano tooa exportação são semelhante toothose abordado [tooFlat arquivo de exportação](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Assistente de Migração de Banco de Dados SQL
etapas para usar o hello SQL Database Migration Wizard Hello são semelhante toothose abordado [SQL Database Migration Wizard](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Backup e restauração de banco de dados
etapas de Olá para usar o banco de dados de backup e restauração são semelhante toothose abordado [banco de dados back backup e restauração](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Azure Data Factory
procedimento de saudação para mover dados tooan Azure SQL database com fábrica de dados do Azure (AAD) é fornecido no tópico Olá [mover dados de um tooSQL de servidor local no SQL Azure com o Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md). Este tópico mostra como toomove dados de um tooan de banco de dados do SQL Server local SQL Azure banco de dados por meio do armazenamento de BLOBs do Azure usando o AAD.

Considere o uso de ADF quando dados necessidades toobe continuamente migrada em um cenário híbrido que acessa locais e recursos de nuvem e quando dados saudação são transacionados ou precisam toobe modificado ou lógica de negócios adicionou tooit ao que está sendo migrado. ADF permite Olá planejamento e monitoramento de trabalhos usando scripts JSON simples que gerencia Olá movimento de dados em uma base periódica. O ADF também possui outros recursos, como suporte para operações complexas.
