---
title: "aaaProvision novos locatários em um aplicativo multilocatário que usa o banco de dados do SQL Azure | Microsoft Docs"
description: "Saiba como tooprovision e catálogo novo locatários no hello aplicativo SaaS Wingtip"
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Provisionar novos locatários e registrá-los no catálogo de saudação

Neste tutorial, você aprenderá sobre provisionar hello e padrões de SaaS do catálogo e como eles são implementados no hello aplicativo SaaS Wingtip. Criar e inicializar novos bancos de dados de locatário e registrá-los no catálogo de locatário do aplicativo hello. Catálogo de saudação é um banco de dados que mantém o mapeamento de saudação entre vários locatários do aplicativo de SaaS hello e seus dados. Catálogo de saudação desempenha um papel importante direcionando aplicativo solicitações toohello banco de dados correto.  

Neste tutorial, você aprenderá como:

> [!div class="checklist"]

> * Provisionar um novo locatário individual, o que inclui como isso é implementado
> * Provisionar um lote de locatários adicionais


toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-catalog-pattern"></a>Introdução toohello padrão do catálogo de SaaS

Em um aplicativo de SaaS do backup de banco de dados multilocatário, é importante tooknow armazenamento de informações para cada locatário. No padrão de catálogo de SaaS hello, um banco de dados do catálogo é usado toohold Olá mapeamento entre cada locatário e onde seus dados estão armazenados. Olá Wingtip SaaS aplicativo usa um único locatário por arquitetura de banco de dados, mas o padrão básico de saudação do armazenamento de mapeamento de locatário no banco de dados em um catálogo aplica se um banco de dados multilocatário ou único locatário é usado.

Cada locatário é atribuído a uma chave que identifica-los no catálogo de saudação e que é mapeado toohello local do banco de dados apropriado hello. No aplicativo de SaaS Wingtip hello, chave Olá é formado de um hash do nome do locatário hello. Isso permite que a parte de nome de locatário Olá de toobe de URL do aplicativo hello usado como chave de saudação tooconstruct. Outros esquemas de chave de locatário podem ser usados.  

Catálogo de Olá permite que o nome de saudação ou local do hello toobe de banco de dados alterado com impacto mínimo sobre o aplicativo hello.  Em um modelo de banco de dados multilocatário, isso também acomoda a 'movimentação' de um locatário entre bancos de dados.  Catálogo de saudação também pode ser usado tooindicate se um locatário ou banco de dados fica offline para manutenção ou outras ações. Isso é explorado Olá [restauração do tutorial de locatário único](sql-database-saas-tutorial-restore-single-tenant.md).

Além disso, o catálogo hello, que é na verdade um banco de dados de gerenciamento para um aplicativo SaaS, pode armazenar metadados adicionais de locatário ou o banco de dados, como Olá camada ou edição de um banco de dados, versão do esquema, o plano de serviço ou os SLAs oferecidos tootenants e outras informações que permite o gerenciamento de aplicativos, suporte ao cliente ou processos de devops.  

Além da saudação aplicativo SaaS, catálogo Olá pode habilitar as ferramentas de banco de dados.  No exemplo de SaaS Wingtip hello, catálogo Olá é consulta de entre locatários de tooenable usadas, explorada Olá [tutorial análise ad hoc](sql-database-saas-tutorial-adhoc-analytics.md). Gerenciamento de trabalhos de bancos de dados é explorado em Olá [gerenciamento esquema](sql-database-saas-tutorial-schema-management.md) e [locatário análise](sql-database-saas-tutorial-tenant-analytics.md) tutoriais. 

No aplicativo de SaaS Wingtip hello, catálogo Olá é implementado usando recursos de gerenciamento de fragmento de saudação do hello [biblioteca de cliente de banco de dados Elástico (EDCL)](sql-database-elastic-database-client-library.md). Olá EDCL permite que um aplicativo toocreate, gerenciar e usar um mapa do fragmento baseado no banco de dados. Um mapa do fragmento contém uma lista de fragmentos (bancos de dados) e o mapeamento de saudação entre chaves (locatários) e bancos de dados.  Funções EDCL podem ser usadas em aplicativos ou scripts do PowerShell durante provisionamento entradas de saudação toocreate no mapa de fragmento de saudação do locatário e de aplicativos tooefficiently conecte toohello banco de dados correto. EDCL armazena em cache conexão informações toominimize Olá tráfego toohello catálogo banco de dados e acelerar o aplicativo hello.  

> [!IMPORTANT]
> dados de mapeamento de saudação estão acessíveis no banco de dados de catálogo hello, mas *não editá-lo*! Edite os dados de mapeamento somente com o uso de APIs da Biblioteca de Cliente do Banco de Dados Elástico. Dados de mapeamento de saudação riscos saudação à corrupção do catálogo e não há suporte para a manipulação direta.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Padrão de provisionamento de SaaS toohello de Introdução

Ao integrar um novo locatário em um aplicativo SaaS que usa um modelo de banco de dados de locatário único, é necessário provisionar um novo banco de dados de locatário.  Ele deve ser criado no local apropriado do hello e camada de serviço, inicializado com dados de referência e o esquema apropriado e, em seguida registrados no catálogo de Olá sob a chave de locatário apropriado de saudação.  

Abordagens diferentes podem ser usado toodatabase provisionamento, que pode incluir a execução de scripts SQL, implantando um bacpac ou copiando um banco de dados de modelo 'dourada'.  

Olá provisionamento abordagem usada deve ser compreendida em sua estratégia de gerenciamento geral do esquema, que deve garantir que os novos bancos de dados são provisionados com esquema mais recente hello.  Isso é explorado Olá [tutorial de gerenciamento de esquema](sql-database-saas-tutorial-schema-management.md).  

Olá Wingtip SaaS aplicativo provisionar novos locatários copiando um banco de dados dourado denominado basetenantdb, implantado no servidor de catálogo hello.  Provisionamento pode ser integrado a aplicativo hello como parte de um processo de inscrição, e/ou suporte offline usando scripts. Este tutorial explorará o provisionamento usando o PowerShell. scripts de provisionamento de saudação copiar Olá basetenantdb toocreate um novo banco de dados de locatário em um pool Elástico, em seguida, inicialização-lo com informações específicas do locatário e registrá-lo no mapa de fragmento de catálogo hello.  No aplicativo de exemplo hello, bancos de dados são fornecidos nomes com base no nome do locatário hello, mas isso não é uma parte crítica do padrão de hello – uso de saudação do catálogo de saudação permite que qualquer banco de dados do nome toobe atribuído toohello. + 


## <a name="get-hello-wingtip-application-scripts"></a>Obter scripts de aplicativo hello Wingtip

Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. [As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Passo a passo detalhado para provisionar e catalogar

como toounderstand Olá Wingtip aplicativo implementa o novo locatário de provisionamento, adicione um ponto de interrupção e percorrer o fluxo de trabalho Olá durante o provisionamento de um locatário:

1. Abrir... \\Módulos de aprendizado\\ProvisionAndCatalog\\_ProvisionAndCatalog.ps1 demonstração_ e saudação do conjunto de parâmetros a seguir:
   * **$TenantName** = nome de saudação do local novo hello (por exemplo, *Bushwillow azuis*).
   * **$VenueType** = um dos tipos de local predefinido Olá: *azuis*, classicalmusic, dança, jazz, judo, motorracing, com várias finalidades, opera, rockmusic, futebol.
   * **$DemoScenario** = **1**, defina muito**1** muito*provisionar um único locatário*.

1. Adicionar um ponto de interrupção colocando o cursor em qualquer lugar na linha hello 48, linha que diz: *novo locatário '*e pressione **F9**.

   ![ponto de interrupção](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. Pressione de script hello toorun **F5**.

1. Após a execução do script hello for interrompida no ponto de interrupção hello, pressione **F11** toostep em código hello.

   ![ponto de interrupção](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Rastreamento de execução do script hello com hello **depurar** opções de menu - **F10** e **F11** toostep pela ou em Olá chamadas de funções. Para saber mais sobre como depurar scripts do PowerShell, confira [Dicas sobre como trabalhar e depurar scripts do PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


a seguir Olá não é as etapas a seguir tooexplicitly, mas uma explicação de fluxo de trabalho Olá que percorrer durante a depuração de script hello:

1. **Saudação de importação SubscriptionManagement.psm1** módulo que contém funções para entrar tooAzure e selecionando Olá assinatura do Azure que você está trabalhando.
1. **Saudação de importação CatalogAndDatabaseManagement.psm1** módulo que fornece um catálogo e o nível de locatário abstração sobre Olá [gerenciamento de fragmento](sql-database-elastic-scale-shard-map-management.md) funções. Este é um módulo importante que encapsula a maior parte do padrão de catálogo hello e vale a pena explorar.
1. **Obter detalhes de configuração**. Intervir Get-configuração (F11) e ver como a configuração de aplicativo hello é especificada. Nomes de recursos e outros valores específicos de aplicativo definidos aqui, mas não altere qualquer um desses valores até que você esteja familiarizado com os scripts de saudação.
1. **Obter o objeto de catálogo Olá**. Etapa para Get-catálogo que compõe e retorna um objeto de catálogo que é usado no script de nível mais alto de saudação.  Essa função usa funções de Gerenciamento de Fragmentos importadas do **AzureShardManagement.psm1**. o objeto de catálogo Olá é composto de seguir hello:
   * $catalogServerFullyQualifiedName é construído usando stem padrão hello mais seu nome de usuário: _catálogo -\<usuário\>. t_.
   * $catalogDatabaseName é recuperado do config Olá: *tenantcatalog*.
   * objeto $shardMapManager foi inicializado de banco de dados de catálogo hello.
   * objeto $shardMap é inicializado de saudação *tenantcatalog* mapa do fragmento no banco de dados de catálogo hello.
   Um objeto de catálogo é composto e retornado e usado no script de nível mais alto de saudação.
1. **Calcular a nova chave de locatário Olá**. Uma função de hash é chave de locatário usado toocreate Olá do nome do locatário hello.
1. **Verifique se já existe uma chave de locatário Olá**. Catálogo de saudação é verificado tooensure Olá chave está disponível.
1. **banco de dados de locatário Hello está provisionado com New-TenantDatabase.** Use **F11** toostep no e ver como é o banco de dados de saudação provisionados usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).

nome do banco de dados de saudação é construído com hello locatário nome toomake claro qual fragmento pertence toowhich locatário. (Outras estratégias de nomeação do banco de dados facilmente usadas.) + Um modelo do Gerenciador de recursos é usado toocreate um banco de dados de locatário copiando um banco de dados ouro (baseTenantDB) no servidor de catálogo hello. Uma abordagem alternativa pode ser toocreate um banco de dados vazio e inicializá-lo com a importação de um bacpac ou tooexecute um script de inicialização de um local conhecido.  

modelo do Gerenciador de recursos de saudação está na pasta do hello ...\Learning Modules\Common\: *tenantdatabasecopytemplate.json*

Após a criação do banco de dados de locatário hello, em seguida, é ainda mais **inicializada com o nome de local (Locatário) de saudação e o tipo de local de saudação**. Outra inicialização também poderia ser feita aqui.

Olá **banco de dados de locatário é registrado no catálogo de saudação** com *TenantDatabaseToCatalog adicionar* usando a chave de locatário hello. Use **F11** toostep detalhes hello:

* banco de dados de catálogo Olá é adicionado mapa do fragmento toohello (lista de saudação de bancos de dados conhecidos).
* Olá mapeamento desse fragmento de toohello links Olá valor da chave é criada.
* Dados adicionais meta (nome do local do evento Olá) sobre o locatário Olá são adicionados toohello tabela de locatários no catálogo de saudação.  tabela de locatários Olá não faz parte do esquema de ShardManagement hello e não é instalada por Olá EDCL.  Esta tabela ilustra como banco de dados de catálogo Olá pode ser estendido dados do toosupport adicionais específicos do aplicativo.   


Após a conclusão do provisionamento, execução retorna toohello original *demonstração ProvisionAndCatalog* script, o que abre Olá **eventos** página para o novo locatário Olá no navegador de saudação:

   ![events](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Provisionar um lote de locatários

Este exercício provisiona um lote com 17 locatários. É recomendável que você provisionar este lote de locatários antes de iniciar outros tutoriais Wingtip SaaS, portanto, há mais do que apenas alguns toowork de bancos de dados com.

1. Abrir... \\Módulos de aprendizado\\ProvisionAndCatalog\\*demonstração ProvisionAndCatalog.ps1* em Olá *PowerShell ISE* e alterar Olá *$ DemoScenario* too3 de parâmetro:
   * **$DemoScenario** = **3**, alterar muito**3** muito*provisionar um lote de locatários*.
1. Pressione **F5** e execute o script hello.

script Hello implanta um lote de locatários adicionais. Ele usa um [modelo do Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md) que controla o lote hello e, em seguida, delega o provisionamento de cada modelo vinculado de tooa do banco de dados. Usando modelos dessa maneira permite que o Azure Resource Manager toobroker Olá processo para o seu script de provisionamento. Modelos de provisionar bancos de dados em paralelo, onde ele pode e manipula as repetições se necessário, otimizando Olá processo geral. Olá script é idempotente assim se ele falha, ou para por qualquer motivo, execute-o novamente.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Verifique se o lote de saudação de locatários foi implantado com êxito

* Olá abrir *tenants1* servidor navegando tooyour lista de servidores no hello [portal do Azure](https://portal.azure.com), clique em **bancos de dados SQL**e verifique se o lote de saudação de 17 bancos de dados adicionais são agora na lista de saudação:

   ![lista de banco de dados](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Outros padrões de provisionamento

Outros padrões de provisionamento não mencionados nesse tutorial incluem:

**Pré-provisionamento de bancos de dados.** Olá previamente provisionamento padrão explora o fato de saudação que bancos de dados em um pool Elástico não adicionam custo extra. A cobrança é para o pool Elástico hello, Olá não bancos de dados e bancos de dados ociosos não consomem nenhum recurso. Ao pré-provisionar bancos de dados em um pool e alocá-los quando necessário, o tempo de integração do locatário poderá ser reduzido consideravelmente. Olá número de bancos de dados previamente provisionado foi ajustado conforme necessário tookeep um buffer adequado para Olá antecipado de provisionamento taxa.

**Provisionamento automático.** No padrão de provisionamento automático Olá, um serviço de provisionamento dedicado é usado tooprovision servidores, pools e bancos de dados automaticamente conforme necessário – incluindo bancos de dados previamente provisionamento em pools Elásticos se desejado. E se os bancos de dados são contratados eliminação e excluídos, intervalos de pools Elásticos podem ser preenchidos pelo Olá provisionamento de serviço conforme desejado. Esse serviço poderá ser simples ou complexo – por exemplo, manipulação do provisionamento em várias áreas geográficas e poderá configurar a replicação geográfica automaticamente, caso essa estratégia esteja sendo usada para a recuperação de desastre. Com padrão de provisionamento automático Olá, um script ou aplicativo cliente pode enviar um provisionamento toobe de fila de tooa solicitação processada pelo Olá provisionar um serviço e, em seguida, seria sondar a conclusão do hello serviço toodetermine. Se for usado o provisionamento prévio, solicitações seriam manipuladas rapidamente com o serviço de saudação Gerenciando o provisionamento de um banco de dados de substituição em execução no plano de fundo de saudação.



## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]

> * Provisionar um novo único locatário
> * Provisionar um lote de locatários adicionais
> * Entrar em detalhes de saudação do provisionamento de locatários e registrando-os no catálogo de saudação

Tente Olá [tutorial de monitoramento de desempenho](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais que se baseiam na Olá aplicativo SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Biblioteca de cliente do banco de dados elástico](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Como tooDebug Scripts no ISE do Windows PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
