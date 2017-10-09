---
title: bancos de dados aaaManage no Azure SQL Data Warehouse | Microsoft Docs
description: "Visão geral do gerenciamento de bancos de dados do SQL Data Warehouse. Inclui ferramentas de gerenciamento, DWUs e escalar o desempenho horizontalmente, solucionar problemas de desempenho de consulta, estabelecer políticas de segurança e restaurar um banco de dados contra dados corrompidos ou de uma interrupção regional."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Gerenciar bancos de dados no SQL Data Warehouse do Azure
O SQL Data Warehouse automatiza muitos aspectos do gerenciamento de seus bancos de dados. Por exemplo, o desempenho tooscale você só precisa tooadjust pague Olá o nível certo de recursos de computação e permitir que o SQL Data Warehouse fazer todo o trabalho de saudação de expansão e dimensionamento back.

Você certamente desejará toomonitor tooidentify sua carga de trabalho, seu desempenho precisa, bem como solucionar problemas de consultas de longa execução. Você também precisará tooperform alguns segurança tarefas toomanage permissões para usuários e logons.

Esta visão geral aborda esses aspectos do gerenciamento do SQL Data Warehouse.

* Ferramentas de gerenciamento
* Computação de escala
* Pausar e retomar
* Práticas recomendadas de desempenho
* Monitoramento de consulta
* Segurança
* Backup e restauração

## <a name="management-tools"></a>Ferramentas de gerenciamento
Você pode usar uma variedade de bancos de dados de toomanage ferramentas no SQL Data Warehouse. Como você gerencia bancos de dados, você desenvolverá preferências de ferramenta para cada tipo de tarefa, você precisa tooperform.

### <a name="azure-portal"></a>Portal do Azure
Olá [portal do Azure] [ Azure portal] é um portal baseado na web, onde você pode criar, atualizar, excluir bancos de dados e monitorar os recursos do banco de dados. Essa ferramenta é ótima é se você estiver apenas começando com o Azure, Gerenciando um pequeno número de bancos de dados do data warehouse, ou precisa tooquickly fazer algo.

tooget iniciado com hello portal do Azure, consulte [criar um Data Warehouse de SQL (portal do Azure)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools no Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) no Visual Studio permite que você tooconnect gerenciar e desenvolver seus bancos de dados. Se você for um desenvolvedor de aplicativos familiarizado com o Visual Studio ou com outros ambientes de desenvolvimento integrados (IDEs), tente usar o SSDT no Visual Studio.

Olá Pesquisador de objetos do SQL Server que permite que você toovisualize o SSDT inclui, conectar e executar scripts em bancos de dados do SQL Data Warehouse. tooquickly conectar tooSQL Data Warehouse, você pode simplesmente clicar Olá **aberto no Visual Studio** botão na barra de comandos Olá ao exibir detalhes do banco de dados de saudação da saudação Portal clássico do Azure.  

tooget iniciado com o SSDT no Visual Studio, consulte [consulta Azure SQL Data Warehouse com o Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Ferramentas da linha de comando
Ferramentas de linha de comando são ideais para automatizar suas cargas de trabalho.  PowerShell e o sqlcmd são tooautomate de duas maneiras ótimas seus processos.  Recomendamos essas ferramentas para gerenciar um grande número de servidores lógicos e implantar as alterações de recursos em um ambiente de produção, como tarefas de saudação necessárias podem ser incluídos no script e automatizadas, em seguida.

### <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico
DMVs são Olá base do SQL Data Warehouse de gerenciamento. Quase todas as informações que aparece no portal de saudação depende DMVs. toosee uma lista de DMVs de depósito de dados do SQL, consulte [exibições do sistema SQL Data Warehouse][SQL Data Warehouse system views].

tooget iniciado, consulte [conectar e consultar com sqlcmd][Connect and query with sqlcmd], e [criar um banco de dados (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Computação de escala
No SQL Data Warehouse você pode, com rapidez, escalar horizontalmente o desempenho ou reverter esse processo, aumentando ou diminuindo os recursos de computação de CPU, memória e largura de banda de E/S. desempenho tooscale, tudo o que você precisa toodo é ajustar Olá número de unidades de depósito de dados (DWUs) que o SQL Data Warehouse aloca tooyour banco de dados. SQL Data Warehouse faz hello e trata todos os Olá subjacente alterações toohardware ou software rapidamente.

toolearn mais sobre como dimensionar DWUs, consulte [dimensionar o desempenho].

## <a name="pause-and-resume"></a>Pausar e retomar
toosave custos, você pode pausar e retomar computação recursos sob demanda. Por exemplo, se você não usar o banco de dados de saudação durante a noite hello e nos finais de semana, você pode pausá-la durante os horários e retomá-lo durante o dia de saudação. Você não será cobrado para DWUs enquanto o banco de dados de saudação está em pausa.

Para saber mais, confira [Pausar computação][Pause compute] e [Retomar a computação][Resume compute].

## <a name="performance-best-practices"></a>Práticas recomendadas de desempenho
Quando a guia de Introdução com uma nova tecnologia, descoberta dicas hello e truques que funcionam melhor direita do início da saudação pode economizar muito tempo.  Você encontrará as práticas recomendadas ao longo de muitos tópicos.

toosee muitos um resumo das considerações de hello mais importantes ao desenvolver sua carga de trabalho, consulte [práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Monitoramento de consulta
Às vezes, uma consulta está em execução muito longa, mas você não tiver certeza de qual é responsável hello. SQL Data Warehouse tem modos de exibição de gerenciamento dinâmico (DMVs) que você pode usar toofigure out qual consulta está demorando muito.

consultas de longa execução toofind, consulte [monitorar sua carga de trabalho usando DMVs][Monitor your workload using DMVs].

## <a name="security"></a>Segurança
toomaintain um sistema seguro, você deve estar em alerta hello e proteger contra qualquer tipo de acesso não autorizado. Um sistema de segurança deve toomake-se de que as regras de firewall estão em vigor autorizado para que somente endereços IP podem se conectar. Ele precisa de autenticação adequada das credenciais do usuário. Depois que um usuário se conectou toohello banco de dados, Olá usuário deve ter somente permissões tooperform um número mínimo de ações. toosecure dados, você pode usar criptografia. Também é importante toohave de auditoria e controle para que você pode refazer eventos se há alguma atividade suspeita.

toolearn sobre gerenciamento de segurança, dirija-toohello [visão geral de segurança][Security overview].

## <a name="backup-and-restore"></a>Backup e restauração
Ter backups confiáveis de seus dados é uma parte essencial de qualquer banco de dados de produção. O SQL Data Warehouse mantém seus dados seguros fazendo backup automaticamente de seus bancos de dados ativos em intervalos regulares. Esses backups permitem toorecover de cenários onde você seus dados corrompidos ou descartado acidentalmente seus dados ou o banco de dados.  Para agendamento de backup de dados do hello, política de retenção e como toorestore um banco de dados, consulte [restauração do instantâneo][Restore from snapshot].

## <a name="next-steps"></a>Próximas etapas
Usar os princípios de design de banco de dados bom tornará mais fácil toomanage seus bancos de dados no SQL Data Warehouse. toolearn mais, dirija-toohello [visão geral do desenvolvimento][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[dimensionar o desempenho]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
