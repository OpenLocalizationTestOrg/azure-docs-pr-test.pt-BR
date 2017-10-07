---
title: "aaaIntro Wingtip SaaS - aplicativo de multilocatário do Azure SQL Database | Microsoft Docs"
description: "Saiba por meio de um aplicativo de multilocatário de exemplo que usa o Azure SQL Database, o aplicativo de SaaS Wingtip Olá"
keywords: tutorial do banco de dados SQL
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Introdução toohello aplicativo SaaS Wingtip

Olá *Wingtip SaaS* aplicativo é um aplicativo de multilocatário de exemplo que demonstra as vantagens exclusivas de saudação do banco de dados SQL. aplicativo Hello usa um banco de dados-por locatário, padrão de aplicativo SaaS, tooservice vários locatários. saudação de aplicativo é projetado tooshowcase recursos do banco de dados do SQL Azure que permitem cenários de SaaS, incluindo vários padrões de design e gerenciamento de SaaS. tooquickly subir e em execução, implanta o aplicativo de SaaS Wingtip Olá em menos de cinco minutos!

Scripts de código e gerenciamento de origem do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. scripts de saudação toorun, [baixar a pasta de módulos de aprendizado Olá](#download-and-unblock-the-wingtip-saas-scripts) computador local tooyour.

## <a name="sql-database-wingtip-saas-tutorials"></a>Tutoriais do SaaS Wingtip do Banco de Dados SQL

Depois de implantar o aplicativo hello, explore Olá tutoriais que se baseiam na implantação inicial Olá a seguir. Esses tutoriais exploram padrões comuns de SaaS que aproveitam os recursos internos do banco de dados SQL, SQL Data Warehouse e outros serviços do Azure. Tutoriais incluem scripts do PowerShell, com explicações detalhadas que simplificam bastante a compreensão, e implementar Olá mesmos padrões de gerenciamento de SaaS em seus aplicativos.


| Tutorial | Descrição |
|:--|:--|
|[Implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)| **COMECE AQUI!** Implantar e explore Olá Wingtip SaaS aplicativo tooyour assinatura do Azure. |
|[Provisionar e catalogar locatários](sql-database-saas-tutorial-provision-and-catalog.md)| Saiba como o aplicativo hello se conecta tootenants usando um banco de dados do catálogo, e como o catálogo de saudação mapeia locatários tootheir dados. |
|[Monitorar e gerenciar o desempenho](sql-database-saas-tutorial-performance-monitoring.md)| Saiba como os recursos de monitoramento de toouse de banco de dados SQL e como tooset alertas quando os limites de desempenho são excedidos. |
|[Monitorar com o Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md) | Saiba mais sobre como usar [análise de Log](../log-analytics/log-analytics-overview.md) toomonitor grandes quantidades de recursos em vários pools. |
|[Restaurar um único locatário](sql-database-saas-tutorial-restore-single-tenant.md)| Saiba como toorestore uma tooa de banco de dados de locatário anterior ponto no tempo. Etapas toorestore tooa paralelo banco de dados, deixando Olá existente locatário online, também estão incluídas. |
|[Gerenciar esquemas de locatário](sql-database-saas-tutorial-schema-management.md)| Saiba como esquema tooupdate e atualização de dados de referência, em todos os locatários Wingtip SaaS. |
|[Executar análise local](sql-database-saas-tutorial-adhoc-analytics.md) | Criar um banco de dados de análise ad hoc e executar consultas distribuídas em tempo real em todos os locatários.  |
|[Executar análise de locatário](sql-database-saas-tutorial-tenant-analytics.md) | Extrai dados de locatário em um análise banco de dados ou data warehouse para executar consultas analíticas offline. |



## <a name="application-architecture"></a>Arquitetura do aplicativo

Olá Wingtip SaaS aplicativo usa o modelo de banco de dados por locatário hello e usa a eficiência de toomaximize pools Elásticos SQL. Para provisionar e mapeando locatários tootheir dados, um banco de dados do catálogo é usado. aplicativo de SaaS Wingtip core Hello, usa um pool com três locatários de exemplo, além de Olá catálogo banco de dados. Concluir muitas Olá Wingtip SaaS tutoriais resultam na implantação inicial de toohello complementos, introduzindo bancos de dados analíticos, bancos de dados gerenciamento de esquema, etc.


![Arquitetura de SaaS Wingtip](media/sql-database-wtp-overview/app-architecture.png)


Ao passar por tutoriais hello e trabalhar com o aplicativo hello, é importante toofocus nos padrões de SaaS hello como elas se relacionam toohello da camada de dados. Em outras palavras, se concentrar na camada de dados hello e não em analisar o aplicativo hello em si. Noções básicas sobre a implementação de saudação desses padrões de SaaS é chave tooimplementing esses padrões em seus aplicativos, considerando todas as modificações necessárias para suas necessidades específicas.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Baixe e desbloquear scripts de SaaS Wingtip Olá

Conteúdos executáveis (scripts, dlls) podem ser bloqueados pelo Windows quando arquivos zip são baixados de uma fonte externa e extraídos. Ao extrair os scripts de saudação de um arquivo zip, ***siga as próximas etapas, Olá arquivo do toounblock hello. zip antes da extração***. Isso garante que o script hello pode toorun.

1. Procurar muito[do repositório github Olá Wingtip SaaS](https://github.com/Microsoft/WingtipSaaS).
1. Clique em **Clonar ou baixar**.
1. Clique em **baixar ZIP** e salve o arquivo hello.
1. Saudação de atalho **WingtipSaaS master.zip** de arquivo e selecione **propriedades**.
1. Em Olá **geral** guia, selecione **desbloquear**.
1. Clique em **OK**.
1. Extraia os arquivos de saudação.

Os scripts estão localizados em Olá *... \\WingtipSaaS mestre\\módulos de aprendizado* pasta.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Trabalhando com hello Wingtip Scripts do PowerShell de SaaS

Olá tooget mais fora do exemplo hello precisar toodive em scripts Olá fornecido. Usar pontos de interrupção e percorrer os scripts hello, examinando Olá detalhes de como os padrões de SaaS diferentes Olá são implementados. etapa tooeasily por meio de scripts de saudação fornecida e módulos para Olá entender melhor, é recomendável usar Olá [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Arquivo de configuração de saudação de atualização para sua implantação

Editar saudação **UserConfig.psm1** arquivo com hello recurso grupo e usuário valor definido durante a implantação:

1. Olá abrir *PowerShell ISE* e carga... \\Módulos de aprendizado\\*UserConfig.psm1* 
1. Atualização *ResourceGroupName* e *nome* com valores específicos de saudação para sua implantação (em linhas 10 e 11 somente).
1. Salve alterações de Olá!

Definir esses valores aqui simplesmente mantém você de ter tooupdate esses valores específicos de implantação em cada script.

### <a name="execute-scripts-by-pressing-f5"></a>Executar Scripts pressionando F5

Usam vários scripts *$PSScriptRoot* toonavigate pastas, e *$PSScriptRoot* é avaliada apenas quando os scripts são executados pressionando **F5**.  Realçar e executar uma seleção (**F8**) pode resultar em erros, então pressione **F5** ao executar scripts.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Percorra a implementação de Olá Olá scripts tooexamine

scripts do Hello melhor maneira toounderstand Olá é percorrendo-los toosee o que fazer. Check-out Olá incluído **demonstração -** scripts que apresentam um fluxo de trabalho de alto nível toofollow fácil. Olá **demonstração -** scripts mostram Olá etapas necessárias tooaccomplish cada tarefa, então definir pontos de interrupção e aprofundando em Olá individuais chama toosee detalhes de implementação para Olá diferentes padrões de SaaS.

Dicas para explorar e depurar scripts do PowerShell:

* Abra **demonstração -** scripts no ISE do PowerShell de saudação.
* Execute ou continue com **F5** (o uso de **F8** não é recomendável porque o *$PSScriptRoot* não é avaliado durante a execução de seleções de um script).
* Coloque pontos de interrupção, clicando ou selecionando uma linha e pressionando **F9**.
* Passe por uma função ou chamada de script usando **F10**.
* Intervenha em uma função ou chamada de script usando **F11**.
* Sair da função atual hello ou script chamada usando **Shift + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Explorar o esquema de banco de dados e executar consultas SQL usando o SSMS

Use [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect e procurar Olá servidores de aplicativos e bancos de dados.

implantação de saudação inicialmente tem dois banco de dados SQL servidores tooconnect muito saudação *tenants1 -&lt;usuário&gt;*  server e hello *catálogo -&lt;usuário&gt;* server. tooensure uma conexão bem-sucedida de demonstração, ambos os servidores têm um [regra de firewall](sql-database-firewall-configure.md) permitindo que todos os IPs pelo.


1. Abra *SSMS* e conecte-se toohello *tenants1 -&lt;usuário&gt;. t* server.
1. Clique em **Conectar** > **Mecanismo de Banco de Dados...**:

   ![servidor catalog](media/sql-database-wtp-overview/connect.png)

1. As credenciais de demonstração são: logon = *developer*, senha = *P@ssword1*

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. Repita as etapas 2-3 e conecte-se toohello *catálogo -&lt;usuário&gt;. t* server.

Após se conectar com êxito, você deverá ver ambos os servidores. A lista de bancos de dados pode ser diferente, dependendo de locatários Olá que tiver provisionado:

![pesquisador de objetos](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Próximas etapas

[Implantar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
