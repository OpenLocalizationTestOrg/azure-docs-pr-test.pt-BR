---
title: "administração de aaaService para pesquisa do Azure em Olá portal do Azure"
description: "Gerencie a pesquisa do Azure, um serviço de pesquisa de nuvem hospedado no Microsoft Azure, usando Olá portal do Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Administração do serviço de pesquisa do Azure no hello portal do Azure
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [SDK .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

O Azure Search é um serviço de pesquisa baseado em nuvem, totalmente gerenciado usado para criar uma experiência avançada de pesquisa em aplicativos personalizados. Este artigo aborda Olá *administração* tarefas que você pode executar em Olá [portal do Azure](https://portal.azure.com) para um serviço de pesquisa que você já tenha configurado. *Administração de serviço* é simplificados por design, limitada toohello tarefas a seguir:

* Gerenciar e proteger o acesso toohello *chaves de api* usado para o serviço de tooyour de acesso de leitura ou gravação.
* Ajuste a capacidade de serviço, alterando a alocação de saudação de partições e réplicas.
* Monitorar o uso de recursos, limites de toomaximum relativo da camada de serviço.

**Não está no escopo** 

*Gerenciamento de conteúdo* (ou gerenciamento de índice) refere-se toooperations como analisar o volume de tráfego toounderstand consulta na pesquisa, descubra qual pessoas de termos de pesquisa e pesquisa bem-sucedida como resultados estão em guiando toospecific de clientes documentos no índice. Para ajuda nessa área, veja [Análise de Tráfego de Pesquisa para o Azure Search](search-traffic-analytics.md).

*Desempenho de consulta* também está além do escopo deste artigo hello. Para obter mais informações, confira [Monitorar as métricas de uso e consulta](search-monitor-usage.md) e [Desempenho e otimização](search-performance-optimization.md).

*Atualizar* não é uma tarefa administrativa. Porque os recursos são alocados quando Olá serviço é provisionado, movendo tooa outra camada requer um novo serviço. Veja [Criar um serviço do Azure Search](search-create-service-portal.md) para obter detalhes.

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Direitos de administrador
O provisionamento ou encerramento do próprio serviço Olá pode ser feito por um administrador de assinatura do Azure ou coadministrador.

Em um serviço, qualquer pessoa com acesso URL do serviço de toohello e uma chave de api de administração tem acesso de leitura-gravação toohello serviço. Acesso de leitura-gravação fornece Olá capacidade tooadd, excluir ou modificar objetos de servidor, incluindo chaves de api, índices, indexadores, fontes de dados, agendas e atribuições de função, conforme implementado por meio de [funções definidas pelo RBAC](#rbac).

Todas as interações do usuário com a pesquisa do Azure está dentro de um destes modos: leitura / gravação serviço toohello de acesso (direitos de administrador) ou serviço toohello de acesso somente leitura (direitos de consulta). Para obter mais informações, consulte [gerenciar chaves de api Olá](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>Definir funções RBAC para acesso administrativo
O Azure fornece um [modelo global de autorização baseada em função](../active-directory/role-based-access-control-configure.md) para todos os serviços gerenciados por meio do portal de saudação ou APIs do Gerenciador de recursos. Funções de leitor, Colaborador e proprietário determinam o nível de saudação de administração do serviço de função de tooeach atribuído de entidades de segurança, grupos e usuários do Active Directory. 

Pesquisa do Azure, permissões RBAC determinam Olá tarefas administrativas a seguir:

| Função | Tarefa |
| --- | --- |
| Proprietário |Criar ou excluir o serviço de saudação ou qualquer objeto no serviço de hello, incluindo chaves de api, índices, indexadores, fontes de dados do indexador e agendas de indexador.<p>Exibir o status do serviço, incluindo o tamanho de armazenamento e contagens.<p>Adicionar ou excluir a associação de função (somente um Proprietário pode gerenciar a associação de função).<p>Os administradores de assinatura e os proprietários de serviços têm associação automática na função de proprietários de saudação. |
| Colaborador |Mesmo nível de acesso como Proprietário, menos gerenciamento de funções RBAC. Por exemplo, um Colaborador pode exibir e gerar novamente a `api-key`, mas não pode modificar as associações de função. |
| Leitor |Exibir chaves de consulta e de status do serviço. Os membros dessa função não podem alterar a configuração do serviço, nem exibir chaves admin. |

Funções não concedem a extremidade de serviço de toohello de direitos de acesso. As operações do serviço de pesquisa, como gerenciamento de índices, preenchimento de índice e consultas em dados de pesquisa, são controladas por meio de chaves de api, não funções. Para mais informações, consulte "Autorização para gerenciamento versus operações de dados" em [O que é controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md).

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Log e informações do sistema
A pesquisa do Azure não expõe os arquivos de log para um serviço individual por meio do portal de saudação ou interfaces programáticas. A camada básica hello e acima, a Microsoft monitora todos os serviços de pesquisa do Azure para disponibilidade de 99,9% por contratos de nível de serviço (SLA). Se o serviço Olá estiver lento ou taxa de transferência de solicitação fica abaixo de limites de SLA, as equipes de suporte examine Olá log arquivos disponíveis toothem e a emissão de saudação do endereço.

Em termos de informações gerais sobre o serviço, você pode obter informações em Olá maneiras a seguir:

* No portal do hello, no painel de serviço hello, por meio de notificações, propriedades e mensagens de status.
* Usando [PowerShell](search-manage-powershell.md) ou hello [API REST de gerenciamento](https://docs.microsoft.com/rest/api/searchmanagement/) muito[obter propriedades do serviço](https://docs.microsoft.com/rest/api/searchmanagement/services), ou de status sobre o uso do recurso de índice.
* Por meio de [análise de tráfego de pesquisa](search-traffic-analytics.md), conforme observado anteriormente.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>Gerenciar api-keys
Todas as solicitações de serviço de pesquisa de tooa precisa de uma chave de api que foi gerada especificamente para o serviço. Esta chave de api é o mecanismo de único de saudação para autenticar o ponto de extremidade de serviço do acesso tooyour pesquisa. 

Uma chave de api é uma cadeia de caracteres composta de letras e números gerados aleatoriamente. Por meio de [permissões RBAC](#rbac), você pode excluir ou ler chaves hello, mas você não pode substituir uma chave com uma senha definida pelo usuário. 

Dois tipos de chaves são usadas tooaccess o serviço de pesquisa:

* Administração (válida para qualquer operação de leitura / gravação no serviço de saudação)
* Consulta (válida para operações somente leitura, como consultas em um índice)

Uma chave de api de administração é criada quando o serviço de saudação é provisionado. Há duas chaves de administração, designadas como *primário* e *secundário* tookeep-los diretamente, mas na verdade eles são intercambiáveis. Cada serviço tem duas chaves de administração para que você pode passar um sem perder o acesso tooyour serviço. Você pode gerar novamente a chave de administração, mas você não pode adicionar a contagem de chaves de administração total toohello. Pode haver no máximo duas chaves admin por serviço de pesquisa.

Chaves de consulta foram criadas para aplicativos cliente que chamam a Pesquisa diretamente. Você pode criar um backup de chaves de consulta too50. No código do aplicativo, você especifica Olá pesquisa URL e um serviço de toohello consulta api-chave tooallow acesso somente leitura. O código do aplicativo também especifica índice Olá usado pelo seu aplicativo. Juntos, ponto de extremidade hello, uma chave de api para acesso somente leitura e um índice de destino definem Olá escopo e nível de acesso de conexão de saudação do seu aplicativo cliente.

tooget ou regenerar chaves de api, painel de serviço Olá aberto. Clique em **chaves** tooslide abrir a página de gerenciamento de chaves de saudação. Comandos para gerar novamente ou criação de chaves estão na parte superior de saudação da página de saudação. Por padrão, somente as chaves admin são criadas. As chaves de api de consulta devem ser criadas manualmente.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Proteger api-keys
Segurança da chave é garantida, restringindo o acesso por meio do portal de saudação ou interfaces do Gerenciador de recursos (PowerShell ou interface de linha de comando). Conforme observado, os administradores de assinatura podem exibir e gerar novamente todas as chaves de api. Como precaução, revise toounderstand de atribuições de função que tenha acesso toohello as chaves de administração.

1. No painel de serviço hello, clique em folha de usuários Olá acesso ícone tooslide Olá aberto.
   ![][7]
2. Em Usuários, analise as atribuições de função existentes. Conforme o esperado, administradores de assinatura já tem o serviço de acesso completo a toohello por meio da função de proprietário de saudação.
3. toodrill ainda mais, clique em **administradores de assinatura** e, em seguida, expanda toosee lista de atribuição de função de saudação que tenha direitos de administração colegas em seu serviço de pesquisa.

Permissões de acesso a outra maneira tooview é tooclick **funções** na folha de usuários hello. Isso exibe funções disponíveis e o número de saudação da função tooeach atribuído de usuários ou grupos.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>Monitorar o uso de recursos
No painel de hello, monitoramento de recursos é limitado toohello informações mostradas no painel de serviço hello e algumas métricas que você pode obter consultando o serviço de saudação. No painel de serviço hello, na seção de uso hello, você pode determinar rapidamente se os níveis de recursos de partição são adequados para seu aplicativo.

Usando Olá API do serviço de pesquisa, você pode obter uma contagem em documentos e índices. Há limites rígidos associados a essas contagens com base no preço de saudação. Para saber mais, confira [Limites de serviço de pesquisa](search-limits-quotas-capacity.md). 

* [Obter estatísticas de índice](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Contar documentos](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Os comportamentos de cache podem aumentar um limite temporariamente. Por exemplo, ao usar o serviço de saudação compartilhado, você verá um documento de contagem de limite rígido de saudação de 10.000 documentos. overstatement Olá é temporário e será detectado na próxima verificação de imposição de limite hello. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Recuperação de desastre e interrupções de serviço

Embora, pode salvar seus dados, pesquisa do Azure não fornece failover imediato do serviço de saudação se houver uma interrupção no nível de Olá cluster ou data center. Se um cluster falhar no Centro de dados Olá, equipe de operações de saudação detectará e serviço toorestore de trabalho. Haverá tempo de inatividade durante a restauração do serviço. Você pode solicitar toocompensate de créditos de serviço para indisponibilidade de serviço por Olá [contrato de nível de serviço (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Se for necessário serviço contínuo em caso de saudação de falhas catastróficas fora do controle da Microsoft, você poderia [provisionar um serviço adicional](search-create-service-portal.md) em uma região diferente e implementar uma replicação geográfica estratégia tooensure índices são completamente redundante em todos os serviços.

Os clientes que usam [indexadores](search-indexer-overview.md) toopopulate e a atualização de índices podem lidar com a recuperação de desastres por meio de indexadores específicas utilizando Olá mesma fonte de dados. Dois serviços em regiões diferentes, cada um executando um indexador, podem indexar da saudação mesmo tooachieve redundância geográfica da fonte de dados. Se você estiver indexando fontes de dados que também são com redundância geográfica, lembre-se de que a indexadores do Azure Search só podem executar a indexação incremental de réplicas primárias. Em um evento de failover, se se toore ponto Olá indexador toohello nova réplica primária. 

Se você não usar indexadores, você usaria os código toopush objetos e dados toodifferent pesquisa serviços de aplicativo em paralelo. Para obter mais informações, consulte [Desempenho e otimização no Azure Search](search-performance-optimization.md).

## <a name="backup-and-restore"></a>Backup e restauração

Como o Azure Search não é uma solução de armazenamento de dados primário, não fornecemos um mecanismo formal de backup e restauração de autoatendimento. O código do aplicativo usado para criar e popular um índice é Olá opção de restauração de fato se você excluir um índice por engano. 

toorebuild um índice, deseja excluí-lo (supondo que ele exista), recrie o índice de saudação no serviço de saudação e recarregar recuperando dados de seu armazenamento de dados primário. Como alternativa, você pode chegar muito[atendimento]() toosalvage índices se houver uma interrupção regional.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Expandir ou reduzir
Todo serviço de pesquisa começa com um mínimo de uma réplica e uma partição. Se você se inscreveu um [camada que fornece recursos dedicados](search-limits-quotas-capacity.md), clique em Olá **escala** lado a lado no uso de recursos tooadjust do painel de controle de serviço hello.

Quando você adiciona capacidade por meio de um recurso, Olá serviço usa automaticamente. Nenhuma ação adicional é necessária de sua parte, mas há um ligeiro atraso antes que o impacto de saudação do novo recurso de saudação é percebido. Pode levar 15 minutos ou mais tooprovision recursos adicionais.

 ![][10]

### <a name="add-replicas"></a>Adicionar réplicas
O aumento de QPS (consultas por segundo) ou o alcance da alta disponibilidade são feitos adicionando réplicas. Cada réplica tem uma cópia de um índice, para que adicionar uma réplica mais converte tooone mais disponível para tratar as solicitações de consulta do serviço de índice. Um mínimo de 3 réplicas são necessários para alta disponibilidade (consulte [Planejamento de capacidade](search-capacity-planning.md) para obter detalhes).

Um serviço de pesquisa com mais réplicas é capaz de balancear a carga das solicitações de consulta em um número maior de índices. Dado um nível de volume de consultas, taxa de transferência da consulta será toobe mais rápido quando há mais cópias da solicitação de Olá Olá índice tooservice disponíveis. Se você estiver tendo a latência da consulta, você pode esperar um impacto positivo no desempenho quando réplicas adicionais Olá estão online.

Embora a taxa de transferência de consulta aumenta à medida que você adiciona réplicas, ele não exatamente duas vezes ou tripla como adicionar réplicas tooyour serviço. Todos os aplicativos de pesquisa são fatores de tooexternal de assunto que afetará o desempenho de consulta. Consultas complexas e latência de rede são dois fatores que contribuem toovariations em tempos de resposta de consulta.

### <a name="add-partitions"></a>Adicionar partições
A maioria dos aplicativos de serviço possui uma necessidade integrada de mais réplicas em vez de partições. Nos casos em que seja necessária uma contagem maior de documentos, é possível adicionar partições se você se inscreveu no serviço Standard. A camada Básica não fornece partições adicionais.

Na camada padrão do hello, as partições são adicionados em múltiplos de 12 (especificamente, 1, 2, 3, 4, 6 ou 12). Isso é um artefato de fragmentação. Um índice é criado em 12 fragmentos, que podem todos ser armazenados em 1 partição ou divididos igualmente em 2, 3, 4, 6 ou 12 partições (um fragmento por partição).

### <a name="remove-replicas"></a>Remover réplicas
Após períodos de grandes volumes de consulta, você poderá reduzir réplicas quando as cargas de pesquisa tiverem se normalizado (por exemplo, após as vendas de final de ano).

toodo, número mais baixo move Olá réplica controle deslizante tooa voltar. Não são necessárias mais medidas de sua parte. Diminuindo a contagem de réplica Olá abandona máquinas virtuais no data center de saudação. Suas operações de consulta e ingestão de dados passarão a ser executadas em menos VMs do que antes. limite mínimo de saudação é uma réplica.

### <a name="remove-partitions"></a>Remover partições
Em contraste com a remoção de réplicas, que não requer nenhum esforço adicional de sua parte, você pode ter algumas toodo de trabalho se você estiver usando mais armazenamento do que pode ser reduzido. Por exemplo, se sua solução está usando três partições, downsizing tooone ou duas partições gerará um erro se o novo espaço de armazenamento Olá é menor do que o necessário. Como esperado, suas opções são índices toodelete ou documentos dentro de um toofree índice associado espaço ou mantenha a configuração atual de saudação.

Não há um método de detecção que informe quais fragmentos de índices estão armazenados em quais partições. Cada partição fornece aproximadamente 25 GB de armazenamento, portanto, será necessário tooreduce tamanho de tooa de armazenamento que pode ser acomodado pelo número de saudação de partições que existentes. Se você quiser toorevert tooone partição, todos os 12 fragmentos precisará toofit.

toohelp com o planejamento futuro, talvez você queira toocheck armazenamento (usando [obter estatísticas de índice](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee quanto você realmente usada. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Melhores práticas para escala e implantação
Este vídeo de 30 minutos examina as práticas recomendadas para cenários de implantação avançados, incluindo cargas de trabalho distribuídas geograficamente. Você também pode ver [desempenho e otimização na pesquisa do Azure](search-performance-optimization.md) para páginas de Ajuda que Olá rosto mesmo aponta.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Próximas etapas
Depois de compreender Olá conceitos básicos da administração do serviço, considere o uso de [PowerShell](search-manage-powershell.md) tooautomate tarefas.

Também é recomendável revisar Olá [artigo de desempenho e otimização](search-performance-optimization.md).

Outra recomendação é observado na seção anterior Olá vídeo do toowatch hello. Ele fornece cobertura mais profunda das técnicas de saudação mencionadas nesta seção.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



