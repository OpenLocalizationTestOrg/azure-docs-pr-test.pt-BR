---
title: "aaaMoving dados entre bancos de dados de nuvem expansíveis | Microsoft Docs"
description: "Explica como fragmentos toomanipulate mover dados através de um serviço auto-hospedado usando elástica banco de dados e APIs."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Mover dados entre bancos de dados na nuvem escalados horizontalmente
Se você é um Software como um desenvolvedor de serviço e, de repente, o aplicativo passa por demanda enorme, será necessário tooaccommodate crescimento de saudação. Por isso você adiciona mais bancos de dados (fragmentos). Como você redistribuir Olá dados toohello novos bancos de dados sem afetar a integridade dos dados de Olá? Saudação de uso **ferramenta de mesclagem de divisão** dados toomove restrita toohello novos bancos de dados de bancos de dados.  

ferramenta de mesclagem de divisão de saudação é executado como um serviço web do Azure. Um administrador ou desenvolvedor usa Olá ferramenta toomove shardlets (dados de um fragmento) entre diferentes bancos de dados (fragmentos). ferramenta Olá usa fragmento mapa gerenciamento toomaintain Olá serviço metadados banco de dados e certifique-se de mapeamentos consistentes.

![Visão geral][1]

## <a name="download"></a>Baixar
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Documentação
1. [Tutorial de ferramenta da Divisão de Mesclagem do banco de dados elástico](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Configuração de segurança da divisão e mesclagem](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Considerações de segurança de divisão/mesclagem](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md)
5. [Migrar tooscale-out de bancos de dados existente](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-introduction.md)
7. [Glossário de ferramentas do banco de dados elástico](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Por que usar a ferramenta de mesclagem de divisão de Olá?
**Flexibilidade**

Os aplicativos precisam toostretch flexibilidade além dos limites de saudação de um único banco de dados do banco de dados de SQL do Azure. Use dados de toomove de ferramenta do hello como bancos de dados necessários toonew enquanto mantém a integridade.

**Toogrow de divisão** 

Você precisa tooincrease geral crescimento explosivo de toohandle de capacidade. toodo assim, criar capacidade adicional por dados de saudação de fragmentação e distribuí-lo em bancos de dados incrementalmente mais até que sejam cumpridas as necessidades de capacidade. Este é um exemplo principal do recurso de 'Dividir' hello. 

**Mesclar tooshrink**

Capacidade precisa reduzir devido a natureza sazonais toohello de uma empresa. unidade de escala Olá ferramenta permite que você reduzir toofewer quando reduz a negócios. recurso de 'Mesclagem' Olá Olá escala elástica divisão mesclagem serviço abrange a esse requisito. 

**Gerenciar pontos de acesso movendo shardlets**

Com vários locatários por banco de dados, alocação de saudação de shardlets tooshards pode levar toocapacity afunilamentos em alguns fragmentos. Isso exige a realocação shardlets ou mover shardlets ocupado toonew ou menos utilizadas em fragmentos. 

## <a name="concepts--key-features"></a>Principais recursos e conceitos
**Serviços hospedados no cliente**

mesclagem Olá divisão é entregue como um serviço hospedado pelo cliente. Você deve implantar e hospedar o serviço de saudação em sua assinatura do Microsoft Azure. pacote de saudação que baixar do NuGet contém um toocomplete do modelo de configuração com informações de saudação para sua implantação específica. Consulte Olá [divisão mesclagem tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md) para obter detalhes. Desde que o serviço de saudação é executado na sua assinatura do Azure, você pode controlar e configurar a maioria dos aspectos de segurança do serviço de hello. modelo de padrão de saudação inclui Olá opções tooconfigure SSL, a autenticação de cliente baseada em certificado, a criptografia para credenciais armazenadas, proteção DoS e restrições de IP. Você pode encontrar mais informações sobre Olá aspectos de segurança em Olá documento a seguir [configuração de segurança de divisão mesclagem](sql-database-elastic-scale-split-merge-security-configuration.md).

padrão de saudação implantado o serviço é executado com um operador e uma função web. Cada uma usa o tamanho de VM A1 de saudação nos serviços de nuvem do Azure. Enquanto você não pode modificar essas configurações durante a implantação de pacote hello, eles podem ser alterados depois de uma implantação bem-sucedida em Olá executando o serviço de nuvem (por meio de saudação portal do Azure). Observe a que essa função de trabalho Olá não deve ser configurada para mais de uma única instância por motivos técnicos. 

**Integração de mapa de fragmentos**

serviço de divisão mesclagem Olá interage com o mapa de fragmentos de saudação do aplicativo hello. Ao usar toosplit do serviço de divisão mesclagem hello ou intervalos de mesclagem ou toomove shardlets entre fragmentos, o serviço de saudação mantém automaticamente mapa do fragmento Olá backup toodate. toodo assim, o serviço de Olá conecta-se o banco de dados do toohello fragmento mapa Gerenciador do aplicativo hello e mantém os intervalos e mapeamentos como progresso de solicitações de divisão/mesclagem/mover. Isso garante que mapa do fragmento Olá sempre apresenta uma exibição atualizada quando operações de mesclagem de divisão estão. Dividir, as operações de movimentação de mesclagem e shardlet são implementadas movendo um lote de shardlets de fragmento de destino Olá fonte fragmento toohello. Durante a saudação shardlet movimentação operação Olá shardlets assunto toohello lote atual são marcados como offline no mapa do fragmento hello e não estão disponíveis para conexões de roteamento dependente de dados usando Olá **OpenConnectionForKey** API. 

**Conexões consistentes de shardlet**

Quando a movimentação de dados é iniciado para um novo lote de shardlets, qualquer mapa de fragmento fornecido dependente de dados roteamento conexões toohello fragmento armazenando Olá shardlet são conexões eliminadas e subsequentes do mapa do fragmento Olá APIs toohello essas shardlets são bloqueados enquanto a movimentação de dados Hello está em andamento em inconsistências de tooavoid de ordem. Conexões tooother shardlets em Olá mesmo fragmento também irá obter eliminado, mas terá êxito novamente imediatamente na próxima tentativa. Depois que o lote Olá for movida, Olá shardlets são marcados online novamente para o fragmento de destino hello e dados de origem de saudação são removidos do fragmento de código-fonte hello. serviço de saudação passa por essas etapas para cada lote até que todos os shardlets foram movidos. Isso levará tooseveral operações de eliminação de conexão durante saudação de concluir a operação divisão/mesclagem/mover hello.  

**Gerenciando a disponibilidade de shardlets**

Limitar conexão Olá eliminando toohello o lote atual de shardlets como discutido acima restringe o escopo de saudação do lote de tooone indisponibilidade de shardlets por vez. Isso é preferível uma abordagem onde fragmento completa Olá permaneceria off-line para todos os seus shardlets durante saudação de uma operação de divisão ou mesclagem. tamanho de saudação de um lote, definido como número de saudação de shardlets distintos toomove por vez, é um parâmetro de configuração. Ela pode ser definida para cada operação de divisão e mesclagem dependendo das necessidades de disponibilidade e o desempenho do aplicativo hello. Observe que o intervalo de saudação que está sendo bloqueado no mapa do fragmento Olá pode ser maior do que o tamanho de lote de saudação especificado. Isso ocorre porque o serviço Olá escolhe o tamanho do intervalo de saudação, de modo que o número real de saudação de valores de chave de fragmentação em dados saudação corresponde aproximadamente tamanho de lote de saudação. Isso é importante tooremember em particular para as chaves de fragmentação de modo disperso preenchida. 

**Armazenamento de metadados**

serviço de divisão mesclagem Olá usa um toomaintain de banco de dados, seu status e tookeep logs durante o processamento da solicitação. usuário Olá cria este banco de dados em sua assinatura e fornece a cadeia de caracteres de conexão Olá para ela no arquivo de configuração de saudação para implantação de serviço de saudação. Os administradores de empresa saudação do usuário também podem se conectar toothis andamento tooreview banco de dados e tooinvestigate obter informações detalhadas sobre falhas potenciais.

**Reconhecimento de fragmentação**

serviço de divisão mesclagem Olá faz distinção entre tabelas fragmentadas (1), as tabelas de referência (2) e tabelas (3) normais. semântica de saudação de uma operação de divisão/mesclagem/mover depende do tipo hello da tabela de saudação usada e é definida da seguinte maneira: 

* **Tabelas fragmentadas**: Split, merge e operações de movimentação movem shardlets de fragmento de tootarget de origem. Após a conclusão bem-sucedida da saudação solicitação geral, os shardlets não estão mais presentes na fonte de saudação. Observe que as tabelas de destino de saudação necessário tooexist no fragmento de destino Olá e não devem conter dados no destino Olá tooprocessing anterior de intervalo da operação de saudação. 
* **Tabelas de referência**: para tabelas de referência, Olá split, merge e mover operações copiem dados de saudação de fragmento de destino Olá fonte toohello. No entanto, observe que nenhuma alteração ocorre no fragmento de destino Olá para uma determinada tabela se qualquer linha já está presente nesta tabela no destino hello. tabela de saudação tem toobe vazia para qualquer tooget de operação de cópia do referência tabela processado.
* **Outras tabelas**: outras tabelas podem estar presentes na origem hello ou de destino de saudação de uma operação de divisão e mesclagem. serviço de divisão mesclagem Olá ignora essas tabelas para qualquer movimentação de dados ou operações de cópia. No entanto, observe que elas podem interferir com essas operações no caso de restrições.

informações de saudação em referência versus tabelas fragmentadas são fornecidas pelo Olá **SchemaInfo** APIs no mapa do fragmento hello. saudação de exemplo a seguir ilustra o uso de saudação dessas APIs em smm de objeto um fragmento determinado mapa manager: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Olá tabelas 'region' e 'nação' são definidas como tabelas de referência e serão copiados com operações de divisão/mesclagem/mover. Já “customer” e “order” por sua vez são definidos como tabelas fragmentadas. C_CUSTKEY e O_CUSTKEY servem como chave de fragmentação hello. 

**Integridade referencial**

serviço de divisão mesclagem Olá analisa dependências entre as tabelas e usa relações de chave estrangeira de chave primária toostage Olá operações para mover as tabelas de referência e shardlets. Em geral, as tabelas de referência são copiadas primeiro em ordem de dependência, os shardlets são então copiados na ordem de suas dependências em cada lote. Isso é necessário para que as restrições de FK PK no fragmento de destino Olá são cumpridas Olá novos dados chegam. 

**Consistência de mapa de fragmentos e eventual conclusão**

Na presença de saudação de falhas, o serviço de divisão mesclagem de saudação retoma operações após qualquer interrupção e visa toocomplete qualquer em solicitações de andamento. No entanto, pode haver situações irrecuperáveis, por exemplo, quando o fragmento de destino Olá for perdido ou comprometido reparos. Sob essas circunstâncias, alguns shardlets que deveria toobe movido pode continuar tooreside no fragmento de código-fonte hello. serviço de Olá garante que mapeamentos de shardlet são atualizados somente depois que os dados necessários Olá foi destino toohello foram copiados com êxito. Shardlets só são excluídos na fonte Olá depois que todos os seus dados foram copiados destino toohello e mapeamentos de saudação correspondentes foram atualizados com êxito. operação de exclusão de saudação acontece no plano de fundo Olá enquanto Olá intervalo já está on-line no fragmento de destino hello. serviço de divisão mesclagem Olá sempre garante correção dos mapeamentos de saudação armazenado no mapa do fragmento hello.

## <a name="hello-split-merge-user-interface"></a>interface do usuário de divisão mesclagem Olá
pacote de serviço de divisão mesclagem Olá inclui uma função de trabalho e uma função web. função da web de saudação é solicitações de mesclagem de divisão de toosubmit usado de forma interativa. componentes principais do Olá Olá da interface do usuário são os seguintes:

* Tipo de operação: o tipo de operação de saudação é um botão de opção que controla o tipo de saudação da operação executada pelo serviço Olá para esta solicitação. Você pode escolher entre Olá divisão, mesclar e mover cenários. Você também pode cancelar uma operação enviada anteriormente. Você pode usar divisão, mesclagem e mover solicitações para mapas de fragmento de intervalo. Os mapas de fragmento da lista apenas oferecem suporte para as operações de movimentação.
* Mapa do fragmento: Olá próxima seção de informações de cobertura de parâmetros de solicitação sobre o mapa do fragmento hello e Olá bancos de dados de seu mapa de fragmento. Em particular, você precisa tooprovide Olá nome do servidor de banco de dados SQL do hello e hospedagem Olá shardmap de banco de dados, fragmento de toohello tooconnect credenciais banco de dados do mapa e finalmente Olá nome do mapa do fragmento hello. Atualmente, a operação Olá aceita apenas um único conjunto de credenciais. Essas credenciais precisam de permissões suficientes toohave tooperform altera o mapa do fragmento toohello, bem como dados de usuário de toohello em fragmentos hello.
* Intervalo de origem (dividir e mesclar): uma operação de divisão e mesclagem processa um intervalo usando sua chave de baixa e alta. toospecify uma operação com um unbounded valor alto da chave, seleção hello "chave alta é max" caixa de seleção e deixe o campo de chave alta Olá vazio. Olá principais valores de intervalo que você especificar fazem não correspondência de tooprecisely necessidade um mapeamento e seus limites em seu mapa de fragmento. Se você não especificar nenhum limite de intervalo em todos os serviços Olá deduzirá intervalo mais próximo de saudação para você automaticamente. Você pode usar o hello GetMappings.ps1 PowerShell tooretrieve Olá atual os mapeamentos de scripts em um mapa de fragmento especificado.
* Comportamento de origem dividido (split): para operações de divisão, definir intervalo de origem de Olá Olá toosplit ponto. Para fazer isso, fornecendo a chave de fragmentação Olá onde você deseja Olá dividir toooccur. Botão de opção usar Olá Especifique se deseja que a parte inferior Olá Olá toomove de intervalo (excluindo Olá dividir chave) ou se você quer Olá parte superior toomove (incluindo a chave de divisão de saudação).
* Fonte de Shardlet (mover): mover operações são diferentes de divisão ou mesclagem operações que não precisam de uma fonte de saudação do intervalo toodescribe. Uma fonte para a movimentação simplesmente é identificada pelo valor de chave de fragmentação de saudação que você planeje toomove.
* Fragmento (divisão) de destino: depois que você forneceu informações de saudação na fonte de saudação da sua operação de divisão, será necessário toodefine onde você deseja Olá dados toobe copiados tooby fornecendo hello Azure SQL Db nomes do servidor e banco de dados de destino de saudação.
* O intervalo de destino (mesclagem): operações de mesclagem mover shardlets tooan existente fragmento. Identifique o fragmento existente hello, fornecendo os limites de intervalo de saudação do intervalo de saudação existente que você deseja toomerge com.
* Tamanho do lote: controles de tamanho de lote Olá Olá número de shardlets que entra offline por vez durante a movimentação de dados de saudação. Isso é um valor inteiro, onde você pode usar valores menores quando são confidenciais toolong períodos de tempo de inatividade para shardlets. Valores maiores aumentará o tempo de saudação que um determinado shardlet está offline mas podem melhorar o desempenho.
* Id da operação (Cancelar): Se você tiver uma operação em andamento que não é mais necessário, você pode cancelar a operação de saudação fornecendo sua ID de operação neste campo. Você pode recuperar a ID da operação de saudação da tabela de status de solicitação de saudação (consulte a seção 8.1) ou de saída de hello no navegador da web de saudação onde você enviou a solicitação de saudação.

## <a name="requirements-and-limitations"></a>Requisitos e limitações
a implementação atual saudação do serviço de divisão mesclagem Olá é assunto toohello requisitos e limitações a seguir: 

* fragmentos de saudação necessário tooexist e ser registrados no mapa do fragmento Olá antes de uma operação de mesclagem de divisão nesses fragmentos pode ser executada. 
* Olá service não cria tabelas ou quaisquer outros objetos de banco de dados automaticamente como parte de suas operações. Isso significa que tabelas de referência e Olá esquema para tabelas fragmentadas todos os necessário tooexist na operação de divisão/mesclagem/mover Olá destino fragmento tooany anterior. Tabelas fragmentadas em particular são necessário toobe vazio no intervalo de saudação onde novos shardlets são toobe adicionado por uma operação de divisão/mesclagem/mover. Caso contrário, a operação de saudação falhará verificação de consistência inicial de saudação no fragmento de destino hello. Também Observe que os dados de referência são copiados somente se a tabela de referência hello está vazia e se não há nenhum consistência garante com operações de gravação simultânea de tooother relação nas tabelas de referência de saudação. Recomendamos isso: ao executar operações de divisão/mesclagem, nenhuma outra operação de gravação fazer alterações toohello tabelas de referência.
* serviço Olá depende da identidade de linha estabelecida por um índice exclusivo ou chave que inclui o desempenho de tooimprove chave de fragmentação hello e confiabilidade para shardlets grande. Isso permite que os dados de toomove do serviço de saudação em uma granularidade maior mesmo que apenas Olá fragmentação valor de chave. Isso ajuda a tooreduce Olá máximo de espaço de log e bloqueios são necessários durante a operação de saudação. Considere criar um índice exclusivo ou uma chave primária, incluindo a chave de fragmentação de saudação em uma determinada tabela se você quiser toouse essa tabela com solicitações de divisão/mesclagem/mover. Por motivos de desempenho, chave de fragmentação Olá deve ser a coluna à esquerda Olá na chave de saudação ou o índice de saudação.
* Durante saudação de processamento de solicitação, alguns dados de shardlet podem estar presentes na origem hello e fragmentos de destino hello. Isso é necessário tooprotect contra falhas durante o movimento de shardlet hello. Olá integração da divisão direta com o mapa do fragmento Olá garante que conexões usando Olá dados dependentes roteamento APIs Olá **OpenConnectionForKey** método no mapa do fragmento Olá não vir todos os estados intermediários inconsistente. No entanto, quando conexão de fonte de toohello ou hello destino fragmentos sem usar Olá **OpenConnectionForKey** método, estados intermediários inconsistentes podem estar visíveis quando as solicitações de divisão/mesclagem/mover estão acontecendo. Essas conexões podem mostrar resultados parciais ou duplicados dependendo do tempo de saudação ou conexão de subjacente Olá Olá fragmento. Essa limitação inclui atualmente conexões Olá feitas pelo Multi-Shard de escala elástica-consultas.
* banco de dados de metadados de saudação para o serviço de divisão mesclagem Olá não deve ser compartilhado entre diferentes funções. Por exemplo, uma função do serviço de divisão mesclagem Olá em execução no banco de dados do necessidades toopoint tooa diferentes metadados de função de produção de hello de preparo.

## <a name="billing"></a>Cobrança
serviço de divisão mesclagem Olá é executado como um serviço de nuvem em sua assinatura do Microsoft Azure. Portanto encargos para serviços de nuvem se aplicam a tooyour instância do serviço de saudação. A menos que você execute operações de divisão/mesclagem/movimentação com frequência, recomendamos que você exclua seu serviço de nuvem de divisão/mesclagem. Isso reduz os custos de execução ou de instâncias de serviço de nuvem implantadas. Você pode implantar novamente e iniciar a configuração de prontamente executável sempre que for necessário tooperform dividir ou mesclar as operações. 

## <a name="monitoring"></a>Monitoramento
### <a name="status-tables"></a>Tabelas de status
Serviço de divisão mesclagem Hello fornece Olá **RequestStatus** tabela no banco de dados do repositório de metadados de saudação para o monitoramento de solicitações em andamento e concluídas. tabela de saudação lista uma linha para cada solicitação de mesclagem de divisão que tenha sido enviado toothis instância do serviço de divisão mesclagem hello. Ele oferece Olá informações para cada solicitação a seguir:

* **Carimbo de hora**: Olá hora e data em que a solicitação de saudação foi iniciada.
* **ID da operação**: um GUID que identifica exclusivamente a solicitação de saudação. Essa solicitação também pode ser usado toocancel Olá operação enquanto ele está ainda em andamento.
* **Status**: Olá o estado atual da solicitação de saudação. Para solicitações em andamento, ela também lista Olá fase atual no qual Olá solicitação é.
* **CancelRequest**: um sinalizador que indica se a solicitação de saudação foi cancelada.
* **Andamento**: uma estimativa da porcentagem de conclusão de operação de saudação. Um valor de 50 indica que a operação de saudação é aproximadamente 50% concluída.
* **Detalhes**: um valor XML que fornece um relatório de andamento mais detalhado. relatório de andamento de saudação é atualizado periodicamente como conjuntos de linhas são copiados da origem tootarget. No caso de falhas ou exceções, essa coluna também inclui informações mais detalhadas sobre a falha de saudação.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure
serviço de divisão mesclagem Olá usa o diagnóstico do Azure com base no Azure SDK 2.5 para monitoramento e diagnóstico. Você controla a configuração de diagnóstico de saudação conforme explicado aqui: [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](../cloud-services/cloud-services-dotnet-diagnostics.md). Olá, pacote de download inclui duas configurações de diagnóstico - um para função de web hello e outro para função de trabalho de saudação. Essas configurações de diagnóstico para serviço hello, siga as diretrizes de saudação do [conceitos fundamentais do serviço de nuvem no Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Ele inclui Olá definições toolog contadores de desempenho, logs do IIS, Logs de eventos do Windows e logs de eventos do aplicativo de divisão de mesclagem. 

## <a name="deploy-diagnostics"></a>Implantar Diagnósticos
tooenable monitoramento e diagnóstico usando a configuração de diagnóstico Olá para funções web e de trabalho Olá fornecidas pelo pacote de NuGet hello, executar Olá comandos usando o Azure PowerShell a seguir: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

Você pode encontrar mais informações sobre como tooconfigure e implantar as configurações de diagnóstico aqui: [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Recuperar diagnósticos
Você pode acessar facilmente os diagnósticos de saudação Visual Studio Server Explorer no hello Azure, parte da árvore do Gerenciador de servidores de saudação. Abra uma instância do Visual Studio e, na barra de menus do hello, clique em modo de exibição e o Gerenciador de servidores. Clique em Olá ícone do Azure tooconnect tooyour assinatura do Azure. Em seguida, navegue tooAzure -> armazenamento -> <your storage account> -> tabelas -> WADLogsTable. Para saber mais, veja [Procurando recursos de armazenamento com o Gerenciador de Servidores](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Olá WADLogsTable realçado na figura acima a saudação contém Olá eventos do log de aplicativo do serviço de divisão mesclagem Olá detalhados. Observe que saudação padrão a configuração de saudação baixada pacote é destinado a uma implantação de produção. Portanto o intervalo de saudação no qual logs e contadores são extraídos de instâncias de serviço Olá é grandes (5 minutos). Para teste e desenvolvimento, precisa de intervalo de saudação mais baixo ajustando as configurações de diagnóstico Olá Olá web ou Olá tooyour de função de trabalho. Com o botão direito na função hello em Olá Visual Studio Server Explorer (veja acima) e, em seguida, ajustar Olá período de transferência na caixa de diálogo Olá Olá diagnóstico as definições de configuração: 

![Configuração][3]

## <a name="performance"></a>Desempenho
Em geral, o melhor desempenho é toobe esperado do hello maior, mais camadas de serviço de alto desempenho no banco de dados do SQL Azure. Alocações de e/s, CPU e memória maior para níveis de serviço superiores Olá se beneficiar de cópia em massa hello e excluir operações que Olá usa serviço de divisão de mesclagem. Por esse motivo, aumente a camada de serviço de saudação apenas para os bancos de dados por um período definido, limitado de tempo.

serviço de saudação também executa consultas de validação como parte de suas operações normais. Essas consultas de validação Verificar presença inesperada de dados no intervalo de destino hello e certifique-se de que qualquer operação de divisão/mesclagem/mover começa em um estado consistente. Essas consultas todos trabalha em intervalos de chave de fragmentação definidos por escopo Olá Olá da operação de e tamanho do lote Olá fornecido como parte da definição de solicitação de saudação. Essas consultas têm melhor desempenho quando um índice é apresentado com chave de fragmentação Olá Olá coluna à esquerda. 

Além disso, uma propriedade de exclusividade com chave de fragmentação hello como coluna à esquerda da saudação permitirá Olá serviço toouse uma abordagem otimizada que limita o consumo de recursos em termos de memória e espaço de log. Esta propriedade de exclusividade é necessário toomove tamanhos de dados grandes (normalmente acima de 1GB). 

## <a name="how-tooupgrade"></a>Como tooupgrade
1. Siga as etapas de saudação em [implantar um serviço de divisão mesclagem](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Altere o arquivo de configuração do serviço de nuvem para sua implantação de divisão mesclagem tooreflect Olá novos parâmetros de configuração. Um novo parâmetro obrigatório é informações Olá sobre Olá certificado usado para criptografia. Uma maneira fácil toodo trata toocompare Olá novo modelo arquivo de configuração de download de saudação em relação a sua configuração existente. Certifique-se de que adicionar configurações hello "DataEncryptionPrimaryCertificateThumbprint" e "DataEncryptionPrimary" de Olá web e função de trabalho hello.
3. Antes de implantar Olá tooAzure de atualização, certifique-se de que todas as operações de mesclagem em execução no momento divisão terminar. Você pode fazer isso facilmente consultando tabelas RequestStatus e PendingWorkflows Olá Olá banco de dados de metadados de mesclagem de divisão para solicitações em andamento.
4. Atualize a implantação do serviço de nuvem existente para mesclagem de divisão em sua assinatura do Azure com o novo pacote de saudação e seu arquivo de configuração de serviço atualizado.

Você não precisa tooprovision um novo banco de dados de metadados para tooupgrade de divisão de mesclagem. nova versão de Hello atualizará automaticamente a existente metadados banco de dados toohello nova versão. 

## <a name="best-practices--troubleshooting"></a>Práticas recomendadas e solução de problemas
* Definir um locatário de teste e use as operações de divisão/mesclagem/mover mais importantes com locatário de teste de saudação em vários fragmentos. Certifique-se de que todos os metadados está definido corretamente em seu mapa de fragmento e operações de saudação não violam restrições ou chaves estrangeiras.
* Tamanho dos dados manter Olá teste locatário acima Olá tamanho máximo de dados do seu locatário maior tooensure tamanho dos dados não estiver encontrando problemas relacionados. Isso ajuda você a avaliar um limite superior em Olá tempo toomove um único locatário ao redor. 
* Certifique-se de que seu esquema permita exclusões. serviço de divisão mesclagem Olá requer que Olá capacidade tooremove dados de fragmento de código-fonte hello quando dados saudação tem sido o destino toohello foram copiados com êxito. Por exemplo, **gatilho delete** pode impedir que o serviço de saudação excluindo Olá dados na fonte de saudação e pode causar toofail de operações.
* chave de fragmentação Olá deve ser coluna à esquerda da saudação em sua chave primária ou a definição de índice exclusivo. Que garante o melhor desempenho Olá Olá consultas de validação de divisão ou mesclagem e Olá dados reais a movimentação e a exclusão operações que sempre operam em intervalos de chave de fragmentação.
* Colocar seu serviço de divisão de mesclagem no Centro de dados e de região de saudação onde residem os bancos de dados. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

