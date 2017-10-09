---
title: "esquema de banco de dados do Azure SQL aaaManage em um aplicativo multilocatário | Microsoft Docs"
description: "Gerenciar o esquema para vários locatários em um aplicativo multilocatário que usa o Banco de Dados SQL do Azure"
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Gerenciar o esquema para vários locatários em Olá aplicativo SaaS Wingtip

Olá [primeiro tutorial Wingtip SaaS](sql-database-saas-tutorial.md) mostra como o aplicativo hello pode provisionar um banco de dados de locatário e registrá-lo no catálogo de saudação. Assim como qualquer aplicativo, Olá aplicativo SaaS Wingtip evoluem ao longo do tempo e às vezes exigirá o banco de dados de toohello alterações. As alterações podem incluir nova ou alterada de esquema, dados de referência novos ou alterados e desempenho de aplicativo ideal tooensure do tarefas de manutenção de rotina do banco de dados. Com um aplicativo SaaS, essas alterações necessitam toobe implantado de maneira coordenada em um fleet potencialmente grande de bancos de dados de locatário. Para essas alterações toobe no futuro locatário bancos de dados, eles precisam toobe incorporada Olá processo de provisionamento.

Este tutorial explora dois cenários - implantação de atualizações de dados de referência para todos os locatários, e reajuste um índice em Olá tabela contendo dados de referência de saudação. Olá [trabalhos Elásticos](sql-database-elastic-jobs-overview.md) recurso é usado tooexecute essas operações em todos os locatários e hello *dourada* banco de dados de locatário que é usado como um modelo para novos bancos de dados.

Neste tutorial, você aprenderá a:

> [!div class="checklist"]

> * Criar uma conta de trabalho
> * Consultar vários locatários
> * Atualizar dados em todos os bancos de dados de locatário
> * Criar um índice em uma tabela em todos os bancos de dados de locatário


toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir forem atendidas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* versão mais recente de saudação do SQL Server Management Studio (SSMS) está instalado. [Baixar e Instalar o SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Este tutorial usa recursos do hello serviço de banco de dados SQL que estão em uma visualização limitada (trabalhos do banco de dados Elástico). Se você quiser toodo neste tutorial, fornecer sua id de assinatura tooSaaSFeedback@microsoft.com com o assunto = Elástico visualização de trabalhos. Depois de receber a confirmação de que sua assinatura tiver sido habilitada, [baixar e instalar cmdlets de pré-lançamento trabalhos mais recentes Olá](https://github.com/jaredmoo/azure-powershell/releases). Esta é uma versão prévia limitada, então contate SaaSFeedback@microsoft.com para conferir perguntas relacionadas ou para obter suporte.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Introdução tooSaaS padrões de gerenciamento de esquema

Hello único locatário por banco de dados SaaS padrão benefícios em muitas maneiras de isolamento de dados Olá resultante, mas em Olá simultaneamente apresenta complexidade adicional Olá manter e gerenciar vários bancos de dados. [Trabalhos Elásticos](sql-database-elastic-jobs-overview.md) facilita a administração e gerenciamento da camada de dados do SQL hello. Trabalhos permitem que você toosecurely e confiável, execute tarefas (scripts T-SQL) independentes da interação do usuário ou de entrada, em relação a um grupo de bancos de dados. Esse método pode ser usado toodeploy esquema e alterações de dados de referência comuns em todos os locatários em um aplicativo. Elásticos trabalhos também podem ser usada toomaintain uma *dourada* cópia do banco de dados de saudação usada toocreate novos locatários, garantindo sempre tem hello mais recentes esquema e dados de referência.

![tela](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Versão prévia limitada dos Trabalhos Elásticos

Há uma nova versão dos Trabalhos Elásticos, que agora é um recurso integrado do Banco de Dados SQL do Azure (que não requer serviços ou componentes adicionais). Essa nova versão dos Trabalhos Elásticos está em versão prévia limitada atualmente. Essa visualização limitada atualmente oferece suporte a contas de trabalho do PowerShell toocreate e toocreate T-SQL e gerenciar trabalhos.

> [!NOTE]
> *Este tutorial usa recursos do hello serviço de banco de dados SQL que estão em uma visualização limitada (trabalhos do banco de dados Elástico). Se você quiser toodo neste tutorial, fornecer sua id de assinatura tooSaaSFeedback@microsoft.com com o assunto = Elástico visualização de trabalhos. Depois de receber a confirmação de que sua assinatura tiver sido habilitada, [baixar e instalar cmdlets de pré-lançamento trabalhos mais recentes Olá](https://github.com/jaredmoo/azure-powershell/releases). Esta é uma versão prévia limitada, então contate SaaSFeedback@microsoft.com para conferir perguntas relacionadas ou para obter suporte.*

## <a name="get-hello-wingtip-application-scripts"></a>Obter scripts de aplicativo hello Wingtip

Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. [As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Criar um banco de dados de conta de trabalho e uma nova conta de trabalho

Este tutorial requer que você usar o PowerShell toocreate Olá trabalho banco de dados e de trabalho da conta. Como o MSDB e o SQL Agent, trabalhos Elástico usa um SQL Azure banco de dados toostore definições de trabalho, o status do trabalho e o histórico. Depois de criar conta de trabalho de saudação, você pode criar e monitorar trabalhos imediatamente.

1. Abrir... \\Módulos de aprendizado\\esquema gerenciamento\\*demonstração SchemaManagement.ps1* em Olá **PowerShell ISE**.
1. Pressione **F5** toorun script de saudação.

Olá *demonstração SchemaManagement.ps1* script chamadas Olá *implantar SchemaManagement.ps1* script toocreate um *S2* banco de dados denominado **jobaccount** no servidor de catálogo hello. Ele, em seguida, cria a conta de trabalho hello, passando o banco de dados do hello jobaccount como uma chamada de criação de conta do parâmetro toohello trabalho.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Criar um trabalho de locatários do toodeploy nova referência dados tooall

Cada banco de dados do locatário inclui um conjunto de tipos de local que definem o tipo de saudação de eventos que são hospedados em um local. Neste exercício, você implanta um tipos de local adicional atualização tooall Olá locatário bancos de dados tooadd dois: *moto corrida* e *nadasse sociedade*. Esses tipos de local correspondem a imagem de plano de fundo toohello que você vê no aplicativo de eventos de locatário hello.

Clique em Olá foro menu suspenso tipo e validar que apenas 10 opções de tipo de local estão disponíveis e, especificamente que 'Moto corrida' e 'Nadasse sociedade' não são incluídos na lista de saudação.

Agora vamos criar uma saudação do trabalho tooupdate *VenueTypes* em todos os bancos de dados de locatário de saudação de tabela e adicionar novos tipos de local de saudação.

toocreate um novo trabalho, usamos um conjunto de trabalhos criados no banco de dados de jobaccount hello quando Olá conta de trabalho foi criada de procedimentos armazenados do sistema.

1. Abra o SSMS e conecte-se o servidor de catálogo toohello: catálogo -\<usuário\>. servidor t
1. Também se conectar o servidor de locatário toohello: tenants1 -\<usuário\>. t
1. Procurar toohello *contosoconcerthall* banco de dados em Olá *tenants1* saudação do servidor e consulta *VenueTypes* tooconfirm de tabela que *moto corrida*  e *nadasse sociedade* **não são** na lista de resultados de saudação.
1. Arquivo hello abrir... \\Módulos de aprendizado\\esquema gerenciamento\\DeployReferenceData.sql
1. Modificar instrução Olá: definir @wtpUser = &lt;usuário&gt; e substitua o valor de usuário Olá usado quando você implantou o aplicativo de Wingtip Olá
1. Certifique-se de que são o banco de dados conectado toohello jobaccount e pressione **F5** para executar o script hello

* **SP\_adicionar\_destino\_grupo** cria o nome do grupo de destino Olá DemoServerGroup, agora precisamos tooadd membros de destino.
* **SP\_adicionar\_destino\_grupo\_membro** adiciona um *server* tipo de membro, o que considerar todos os bancos de dados nesse servidor (note que esta é a saudação tenants1-dedestino&lt; Usuário&gt; que contém os bancos de dados de locatário de saudação do servidor) em tempo de trabalho de execução deve ser incluída no trabalho hello, Olá segundo está adicionando um *banco de dados* tipo de membro de destino, especificamente hello (banco de dados 'final' basetenantdb) que reside no catálogo -&lt;usuário&gt; server e finalmente outro *banco de dados* destino grupo membro tipo tooinclude Olá adhocanalytics banco de dados que é usado em um tutorial posterior.
* **sp\_add\_job** cria um trabalho chamado “Reference Data Deployment”
* **SP\_adicionar\_jobstep** cria Olá etapa de trabalho que contém a tabela de referência Olá no tooupdate texto do T-SQL comando, VenueTypes
* Olá restantes no script hello exibem existência de saudação de objetos hello e execução do trabalho de monitor. Usar o valor de status essas consultas tooreview Olá Olá **ciclo de vida** toodetermine coluna quando o trabalho de saudação foi concluído com êxito em todos os bancos de dados de locatário e Olá dois outros bancos de dados que contém a tabela de referência de saudação.

1. No SSMS, procurar toohello *contosoconcerthall* banco de dados em Olá *tenants1* saudação do servidor e consulta *VenueTypes* tooconfirm de tabela que *moto Corrida* e *nadasse sociedade* **são** agora na lista de resultados de saudação.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Criar um índice de tabela de referência do trabalho toomanage Olá

Semelhante toohello de exercício anterior, este exercício cria um índice de saudação do trabalho toorebuild na chave primária da tabela de referência de hello, uma operação de gerenciamento de banco de dados típico um administrador pode executar após um carregamento de dados grande em uma tabela.

Criar um trabalho usando Olá mesmo trabalhos 'system' procedimentos armazenados.

1. Abra o SSMS e conecte-se toohello catálogo -&lt;usuário&gt;. servidor t
1. Arquivo hello abrir... \\Módulos de aprendizado\\esquema gerenciamento\\OnlineReindex.sql
1. Clique com botão direito, selecione a Conexão e conectar-se toohello catálogo -&lt;usuário&gt;. t server, se ainda não estiver conectado
1. Certifique-se conectado toohello jobaccount no banco de dados e pressione F5 script de saudação de toorun

* sp\_add\_job cria um novo trabalho chamado “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”
* SP\_adicionar\_jobstep cria a etapa de trabalho de saudação que contém o índice de saudação do T-SQL comando texto tooupdate




## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]

> * Criar um tooquery de conta de trabalho por vários locatários
> * Atualizar dados em todos os bancos de dados de locatário
> * Criar um índice em uma tabela em todos os bancos de dados de locatário

[Tutorial de análise ad hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Recursos adicionais

* [Tutoriais adicionais que se baseiam na Olá implantação de aplicativos SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Gerenciando bancos de dados de nuvem com escalonamento horizontal](sql-database-elastic-jobs-overview.md)
* [Criar e gerenciar bancos de dados de nuvem com escalonamento horizontal](sql-database-elastic-jobs-create-and-manage.md)
