---
title: "bancos de dados de nuvem expansíveis aaaManaging | Microsoft Docs"
description: "Ilustra o serviço de trabalho de banco de dados Elástico Olá"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Gerenciando bancos de dados de nuvem com escalonamento horizontal
Olá toomanage expansíveis bancos de dados fragmentados, **trabalhos do banco de dados Elástico** recurso habilita (visualização) tooreliably você executar um script Transact-SQL (T-SQL) em um grupo de bancos de dados, incluindo:

* um conjunto personalizado de bancos de dados (explicado abaixo)
* todos os bancos de dados em um [pool elástico](sql-database-elastic-pool.md)
* um conjunto de fragmentos (criado usando a [biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-database-client-library.md)). 

## <a name="documentation"></a>Documentação
* [Instalar componentes de trabalho de banco de dados Elástico Olá](sql-database-elastic-jobs-service-installation.md). 
* [Introdução aos trabalhos do Banco de Dados Elástico](sql-database-elastic-jobs-getting-started.md).
* [Criar e gerenciar trabalhos usando o PowerShell](sql-database-elastic-jobs-powershell.md).
* [Criar e gerenciar Bancos de Dados SQL do Azure com escala horizontal](sql-database-elastic-jobs-getting-started.md)

**Trabalhos do banco de dados Elásticos** atualmente é um serviço de nuvem para Azure hospedado pelo cliente que permite a execução de saudação do ad hoc e tarefas administrativas agendadas, que são chamadas de **trabalhos**. Com trabalhos, você pode facilmente e gerenciar com confiança grandes grupos de bancos de dados do SQL Azure, executando operações administrativas de tooperform de scripts de Transact-SQL. 

![Serviço do trabalho de banco de dados elástico][1]

## <a name="why-use-jobs"></a>Por que usar os trabalhos?
**Gerenciar**

Realize facilmente alterações de esquema, gerenciamento de credenciais, atualizações de dados de referência, desempenho de coleta de dados ou coleção de telemetria do locatário (cliente).

**Relatórios**

Agregue dados de uma coleção de Bancos de Dados SQL do Azure em uma tabela de destino único.

**Reduzir a sobrecarga**

Normalmente, você deve conectar tooeach banco de dados independentemente de instruções de Transact-SQL toorun ordem ou executar outras tarefas administrativas. Um trabalho trata a tarefa de saudação de registro em log no banco de dados tooeach no grupo de destino hello. Você também define, manter e manter toobe de scripts Transact-SQL executado em um grupo de bancos de dados do SQL Azure.

**Contabilização**

Trabalhos executados status de saudação script e o log de saudação de execução para cada banco de dados. Você também tem a repetição automática quando ocorrem falhas.

**Flexibilidade**

Defina grupos personalizados de Bancos de Dados SQL do Azure e defina agendas para executar um trabalho.

> [!NOTE]
> Olá portal do Azure, somente um conjunto reduzido de funções limitado tooSQL Azure Elástico pools está disponível. Use Olá conjunto completo de APIs do PowerShell tooaccess Olá da funcionalidade atual.
> 
> 

## <a name="applications"></a>Aplicativos
* Realize tarefas administrativas, como a implantação de um novo esquema.
* Atualize informações de dados de referência do produto comuns a todos os bancos de dados. Ou agende atualizações automáticas a cada dia da semana, após o expediente.
* Recrie o desempenho da consulta tooimprove índices. Olá recriação pode ser configurado tooexecute em uma coleção de bancos de dados de forma recorrente, como horário de pico.
* Coletar resultados de consulta de um conjunto de bancos de dados em uma tabela central em uma base contínua. Consultas de desempenho podem ser executadas continuamente e configurado tootrigger tarefas adicionais toobe executado.
* Executar consultas de processamento de dados mais longas em execução em um conjunto grande de bancos de dados, por exemplo hello coleção de telemetria do cliente. Resultados são coletados em uma única tabela de destino para análise posterior.

## <a name="elastic-database-jobs-end-to-end"></a>Trabalhos de Banco de Dados Elástico: ponta a ponta
1. Instalar Olá **trabalhos do banco de dados Elástico** componentes. Para saber mais informações, consulte [Instalando trabalhos de banco de dados elástico](sql-database-elastic-jobs-service-installation.md). Se a instalação Olá falhar, consulte [como toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Use Olá tooaccess de APIs do PowerShell mais funcionalidade, por exemplo, criar coleções de banco de dados personalizadas, adicionando agendas e/ou coleta conjuntos de resultados. Portal de saudação de uso para instalação simples e criação/monitoramento de trabalhos de limitado tooexecution contra um **pool Elástico**. 
3. Criar credenciais criptografadas para execução do trabalho e [adicionar Olá usuário (ou função) tooeach banco de dados no grupo de saudação](sql-database-security-overview.md).
4. Crie um script T-SQL que pode ser executado em cada banco de dados no grupo de saudação idempotentes. 
5. Execute trabalhos de toocreate essas etapas usando o portal do Azure de saudação: [criando e gerenciando trabalhos do banco de dados Elástico](sql-database-elastic-jobs-create-and-manage.md). 
6. Ou use scripts do PowerShell: [Criar e gerenciar trabalhos de banco de dados elástico de Banco de Dados SQL usando o PowerShell (visualização)](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Scripts idempotentes
Olá scripts devem ser [idempotente](https://en.wikipedia.org/wiki/Idempotence). Em termos simples, "idempotente" significa que se o script hello tiver êxito, e ele é executado novamente, hello mesmo resultado ocorre. Um script pode falhar devido a problemas de rede tootransient. Nesse caso, o trabalho Olá repetirá automaticamente um número predefinido de vezes antes de desisting executando o script hello. Um script idempotente tem Olá mesmo resultado, mesmo que tenha sido executado com êxito duas vezes. 

Uma tática simple é tootest existência de saudação de um objeto antes de criá-lo.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

Da mesma forma, um script deve ser capaz de tooexecute com êxito logicamente Testando e responder a quaisquer condições de encontrar.

## <a name="failures-and-logs"></a>Falhas e logs
Se um script falhar após várias tentativas, o trabalho de saudação registra Olá erro e continua. Após o término de um trabalho (ou seja, uma execução em todos os bancos de dados no grupo de saudação), você pode verificar sua lista de tentativas com falha. Olá logs fornecem detalhes scripts com defeito toodebug. 

## <a name="group-types-and-creation"></a>Tipos de grupos e criação
Há dois tipos de grupos: 

1. Conjuntos de fragmento
2. Grupos personalizados

Grupos de conjunto de fragmentos são criados usando Olá [ferramentas de banco de dados Elástico](sql-database-elastic-scale-introduction.md). Quando você cria um grupo de conjunto de fragmentos, bancos de dados são adicionados ou removidos do grupo de saudação automaticamente. Por exemplo, um novo fragmento será automaticamente no grupo hello quando você adiciona o mapa do fragmento toohello. Um trabalho pode ser executado, em seguida, no grupo de saudação.

Grupos personalizados, Olá outro lado, rigidamente são definidos. Você deve adicionar ou remover explicitamente bancos de dados de grupos personalizados. Se um banco de dados no grupo de saudação for descartado, trabalho Olá tentará toorun script hello banco de dados de saudação resultando em uma falha de eventual. Grupos criados usando Olá portal do Azure no momento são grupos personalizados. 

## <a name="components-and-pricing"></a>Componentes e preços
Olá seguintes componentes trabalham juntos toocreate um serviço de nuvem do Azure que permite a execução do ad-hoc de trabalhos administrativos. componentes de saudação são instalados e configurados automaticamente durante a instalação, na sua assinatura. Você pode identificar serviços hello como todos eles têm Olá mesmo gerado automaticamente nome. Olá nome é exclusivo e consiste em prefixo hello "edj" seguido por 21 caracteres geradas aleatoriamente.

* **Serviço de nuvem do Azure**: trabalhos de banco de dados Elástico (visualização) é fornecida como uma nuvem do Azure hospedado cliente serviço tooperform a execução de saudação solicitado tarefas. No portal de hello, serviço de saudação é implantado e hospedado em sua assinatura do Microsoft Azure. serviço de padrão implantado de saudação é executado com um mínimo de saudação de duas funções de trabalho para alta disponibilidade. tamanho padrão de saudação de cada função de trabalho (ElasticDatabaseJobWorker) é executado em uma instância de A0. Para obter os preços, confira [preços dos serviços de Nuvem](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Banco de dados do SQL Azure**: serviço Olá usa um banco de dados do SQL do Azure conhecido como Olá **banco de dados de controle** toostore todos os metadados do trabalho hello. camada de serviço saudação padrão é um S0. Para obter os preços, confira [Preços de Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* **Barramento de serviço do Azure**: é um barramento de serviço do Azure para a coordenação de trabalho hello dentro Olá serviço de nuvem do Azure. Consulte [Preços de Barramento de Serviço](https://azure.microsoft.com/pricing/details/service-bus/).
* **Armazenamento do Azure**: conta de um armazenamento do Azure é usada toostore diagnóstico de saída de log no evento de saudação que um problema requer a depuração adicional (consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](../cloud-services/cloud-services-dotnet-diagnostics.md)). Para obter os preços, confira [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Como os trabalhos de banco de dados elástico funcionam
1. Um **banco de dados de controle** , que armazena todos os dados de estado e metadados, é atribuído a um banco de dados SQL do Azure.
2. banco de dados de controle de saudação é acessado pelo Olá **serviço de trabalho** toolaunch e rastrear tooexecute de trabalhos.
3. Duas diferentes funções se comunicam com o banco de dados de controle de saudação: 
   * Controlador: Determina quais trabalhos exigem Olá de tooperform tarefas solicitadas trabalho e trabalhos de novas tentativas com falha, criando novas tarefas de trabalho.
   * Execução de tarefa do trabalho: Executa tarefas de trabalho hello.

### <a name="job-task-types"></a>Tipos de tarefa de trabalho
Há vários tipos de tarefas de trabalho que realizarão a execução de trabalhos:

* ShardMapRefresh: Consultas Olá toodetermine de mapa do fragmento todos os bancos de dados de saudação usados como fragmentos
* ScriptSplit: Divide o script hello em instruções 'GO' em lotes
* ExpandJob: cria trabalhos filho para cada banco de dados de um trabalho que se destina a um grupo de bancos de dados
* ScriptExecution: executa um script em um banco de dados específico usando credenciais definidas
* Dacpac: Aplica-se um DACPAC tooa banco de dados específico usando credenciais específicas

## <a name="end-to-end-job-execution-work-flow"></a>Fluxo de trabalho de execução de trabalho de ponta a ponta
1. Usando o hello Portal ou Olá API do PowerShell, um trabalho é inserido em Olá **banco de dados de controle**. trabalho de saudação solicita a execução de um script Transact-SQL para um grupo de bancos de dados usando credenciais específicas.
2. controlador Olá identifica o novo trabalho de saudação. Tarefas de trabalho são criadas e executado o script de saudação toosplit e bancos de dados do grupo de saudação toorefresh. Por fim, um novo trabalho é criado e executado o trabalho de saudação tooexpand e cria novo filho trabalhos onde cada trabalho filho é especificado tooexecute Olá script Transact-SQL em relação a um banco de dados individual no grupo de saudação.
3. controlador Olá identifica Olá criado trabalhos filhos. Para cada trabalho, o controlador de saudação cria e aciona um script de saudação do trabalho tarefa tooexecute em relação a um banco de dados. 
4. Depois de concluir todas as tarefas de trabalho, controlador Olá atualiza o estado do hello trabalhos tooa concluída. 
   A qualquer momento durante a execução do trabalho, Olá API PowerShell pode ser usado tooview Olá o estado atual da execução do trabalho. Sempre retornado por Olá APIs do PowerShell são representados no UTC. Se desejado, uma solicitação de cancelamento pode ser iniciada toostop um trabalho. 

## <a name="next-steps"></a>Próximas etapas
[Instalar componentes de saudação](sql-database-elastic-jobs-service-installation.md), em seguida, [criar e adicionar um log no banco de dados tooeach no grupo de saudação de bancos de dados](sql-database-manage-logins.md). toofurther entender o trabalho de criação e gerenciamento, consulte [criar e gerenciar trabalhos do banco de dados Elástico](sql-database-elastic-jobs-create-and-manage.md). Consulte também a [Introdução aos trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


