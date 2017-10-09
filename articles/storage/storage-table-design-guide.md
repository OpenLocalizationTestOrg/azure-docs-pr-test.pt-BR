---
title: Guia de Design de tabela de armazenamento de aaaAzure | Microsoft Docs
description: "Projete tabelas escalonáveis e de alto desempenho no Armazenamento de Tabelas do Azure"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Guia de Design de tabela de armazenamento do Azure: projetando tabelas escalonáveis e de alto desempenho
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign escalonável e tabelas de alto desempenho, você deve considerar vários fatores como custo, escalabilidade e desempenho. Se você criou anteriormente esquemas de bancos de dados relacionais, essas considerações será tooyou familiar, mas existem algumas semelhanças entre o modelo de armazenamento de serviço de tabela do Azure hello e modelos relacionais, também há muitas importantes diferenças. Normalmente, essas diferenças resultam toovery diferentes designs que pode ser contrário à intuição ou errada toosomeone familiarizado com bancos de dados relacionais, mas que fazem sentido bom se você criar um repositório de chave/valor NoSQL como Olá serviço tabela do Azure. Muitas das diferenças seu design refletirá Olá fato de serviço de tabela Olá projetado toosupport aplicativos de escala de nuvem que podem conter bilhões de entidades (linhas na terminologia de banco de dados relacional) de dados ou para conjuntos de dados devem oferecer suporte a muito alta volumes de transações: portanto, você precisa toothink diferente sobre como armazenar os dados e entender como funciona a saudação serviço tabela. Um repositório de dados NoSQL bem projetado pode habilitar a sua solução tooscale muito mais (e um custo menor) que uma solução que usa um banco de dados relacional. Este guia ajuda você com esses tópicos.  

## <a name="about-hello-azure-table-service"></a>Sobre Olá serviço tabela do Azure
Esta seção destaca alguns Olá principais recursos do serviço de tabela de saudação que são especialmente relevante toodesigning para desempenho e escalabilidade. Se você estiver tooAzure novo armazenamento e hello serviço tabela, primeiro leia [tooMicrosoft Introdução armazenamento do Azure](storage-introduction.md) e [Introdução ao armazenamento de tabela do Azure usando o .NET](storage-dotnet-how-to-use-tables.md) antes de ler o restante da saudação da artigo. Embora foco deste guia Olá Olá serviço tabela, ele incluirá alguns discussão de saudação fila do Azure e serviços Blob e como você pode usar-os junto com hello serviço de tabela em uma solução.  

O que é o serviço de tabela Olá? Como você pode esperar do nome hello, Olá serviço tabela usa dados de toostore um formato tabular. Na terminologia de saudação padrão, cada linha da tabela Olá representa uma entidade e repositório de colunas Olá Olá várias propriedades de entidade. Cada entidade tem um par de chaves toouniquely identificá-lo, e uma coluna de carimbo de hora que Olá serviço tabela usa tootrack entidade Olá foi atualizada pela última vez (Isso ocorre automaticamente e não é possível substituir manualmente Olá timestamp com um valor arbitrário). Olá serviço tabela usa esta última modificação timestamp (LMT) toomanage a simultaneidade otimista.  

> [!NOTE]
> operações de API REST do serviço de tabela Olá também retornam um **ETag** valor deriva de timestamp última modificação da saudação (LMT). Neste documento, usamos o hello termos ETag e LMT alternadamente porque elas fazem referência toohello mesmo dados subjacentes.  
> 
> 

Olá exemplo a seguir mostra um toostore de design de tabela simples employee e department entidades. Muitos dos exemplos de saudação mostrados mais adiante neste guia são baseados nesse design simple.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td>Jun</td>
<td>Cao</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Departamento</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Vendas</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Até agora, parece muito semelhante tabela de tooa em um banco de dados relacional com algumas diferenças de saudação sendo Olá colunas obrigatórias e hello capacidade toostore entidade vários tipos no hello mesma tabela. Além disso, cada um dos Olá propriedades definidas pelo usuário, como **FirstName** ou **idade** tem um tipo de dados, como integer ou string, assim como uma coluna em um banco de dados relacional. Embora, ao contrário de um banco de dados relacional, natureza sem esquema Olá Olá significa do serviço de tabela que não precisa ter uma propriedade Olá mesmo tipo de dados em cada entidade. tipos de dados complexos toostore em uma única propriedade, você deve usar um formato serializado como JSON ou XML. Para obter mais informações sobre tipos de dados de serviço, como suporte de tabela hello, intervalos de datas com suporte, as regras de nomenclatura e restrições de tamanho, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Como veremos, a escolha do **PartitionKey** e **RowKey** é fundamental toogood design da tabela. Cada entidade armazenada em uma tabela deve ter uma combinação exclusiva de **PartitionKey** e **RowKey**. Assim como acontece com as chaves em uma tabela de banco de dados relacional, Olá **PartitionKey** e **RowKey** valores são indexada toocreate um índice clusterizado que permite pesquisas rápidas; no entanto, Olá serviço tabela não criar qualquer índices secundários, portanto esses são Olá apenas duas propriedades indexadas (alguns dos padrões Olá descritos posteriormente mostram como você pode contornar essa limitação aparente).  

Como você verá muitos Olá decisões tomadas vai ser em torno de escolher um adequado de design e uma tabela é composta de uma ou mais partições **PartitionKey** e **RowKey** toooptimize sua solução. Uma solução poderia consistir em apenas uma única tabela que contém todas as suas entidades organizadas em partições, mas normalmente uma solução terá várias tabelas. Ajudarão-lo a tabelas toologically organizar suas entidades, ajudam você a gerenciar o acesso toohello dados usando listas de controle de acesso e você pode descartar uma tabela inteira usando uma única operação de armazenamento.  

### <a name="table-partitions"></a>Partições de tabela
nome da conta Olá, nome da tabela e **PartitionKey** juntos identificar partição Olá no serviço de armazenamento de saudação em que o serviço de tabela Olá armazena entidade hello. Bem como sendo parte do esquema para entidades de endereçamento de hello, as partições definem um escopo de transações (consulte [transações de grupo de entidade](#entity-group-transactions) abaixo) e a base de saudação do formulário de como o serviço de tabela Olá dimensiona. Para obter mais informações sobre partições, consulte [Metas de desempenho e escalabilidade de armazenamento do Azure](storage-scalability-targets.md).  

Olá serviço tabela, um nó individual serviços um ou mais concluir partições e Olá escalas de serviço pelo balanceamento de carga dinamicamente partições em nós. Se um nó está sob carga, o serviço de tabela Olá pode *dividir* intervalo saudação de partições atendido pelo nó em nós diferentes; ao diminuir o tráfego, serviço Olá pode *mesclagem* partição Olá varia de nós silenciosos de volta para um único nó.  

Para obter mais informações sobre Olá detalhes internos de saudação serviço tabela e em particular como o serviço de saudação gerencia partições, consulte papel Olá [armazenamento do Microsoft Azure: um altamente disponível armazenamento de serviço de nuvem com forte consistência](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Transações de Grupo de Entidades
Em Olá serviço tabela, transações de grupo de entidade (EGTs) são mecanismo somente interno de saudação para realizar atualizações atômicas entre várias entidades. EGTs também são chamados de tooas *lote transações* em alguns documentos. EGTs só pode operar em entidades armazenadas em Olá mesma partição (compartilhamento Olá mesma chave de partição em uma determinada tabela), portanto, sempre que precisar atômico comportamento transacional entre várias entidades, você precisa tooensure essas entidades são em Olá mesma partição. Isso geralmente é um motivo para manter vários tipos de entidade no hello mesma tabela (e de partição) e não usar várias tabelas para tipos de entidade diferente. Uma única EGT pode operar no máximo 100 entidades.  Se você enviar várias EGTs simultâneos para processá-lo é importante tooensure esses EGTs não funcionam em entidades que são comuns em EGTs, caso contrário, o processamento pode ser atrasado.

EGTs também apresentam uma compensação potencial para você tooevaluate em seu design: usar mais partições aumentará escalabilidade de saudação do aplicativo porque o Azure tem mais oportunidades para balanceamento de carga solicitações entre nós, mas isso pode limitar Olá capacidade de seu transações atômicas de tooperform do aplicativo e manter a consistência forte para seus dados. Além disso, existem destinos de escalabilidade específico no nível de saudação de uma partição que pode limitar a taxa de transferência de saudação de transações que você pode esperar para um único nó: para obter mais informações sobre os destinos de escalabilidade Olá para contas de armazenamento do Azure e a tabela de saudação serviço, consulte [escalabilidade do armazenamento do Azure e metas de desempenho](storage-scalability-targets.md). As seções posteriores deste guia discutem vários design estratégias ajudarão-lo a gerenciar as compensações como este e discutem a melhor toochoose sua chave de partição com base em requisitos específicos de saudação do seu aplicativo cliente.  

### <a name="capacity-considerations"></a>Considerações sobre a capacidade
Olá tabela a seguir inclui alguns Olá valores de chave toobe atento ao projetar uma solução de serviço de tabela:  

| Capacidade total de uma conta de armazenamento do Azure | 500 TB |
| --- | --- |
| Número de tabelas em uma conta de armazenamento do Azure |Limitado apenas pela capacidade Olá Olá da conta de armazenamento |
| Número de partições em uma tabela |Limitado apenas pela capacidade Olá Olá da conta de armazenamento |
| Número de entidades em uma partição |Limitado apenas pela capacidade Olá Olá da conta de armazenamento |
| Tamanho de uma entidade individual |Até too1 MB com um máximo de 255 propriedades (incluindo Olá **PartitionKey**, **RowKey**, e **Timestamp**) |
| Tamanho da saudação **PartitionKey** |Uma cadeia de caracteres para cima too1 KB de tamanho |
| Tamanho da saudação **RowKey** |Uma cadeia de caracteres para cima too1 KB de tamanho |
| Tamanho de uma Transação de Grupo de Entidades |Uma transação pode incluir no máximo 100 entidades e carga Olá deve ser menor que 4 MB. Uma EGT só pode atualizar uma entidade uma vez. |

Para obter mais informações, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Considerações de custo
Armazenamento de tabela é relativamente baixo custo, mas você deve incluir estimativas de custo para a quantidade de uso e hello ambas as capacidade de transações como parte da avaliação de qualquer solução que usa o serviço de tabela de saudação. No entanto, em muitos cenários de armazenamento de dados desnormalizados ou duplicados em Olá de tooimprove ordem desempenho ou a escalabilidade de sua solução é tootake uma abordagem válida. Para obter mais informações sobre preços, consulte [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Diretrizes de design da tabela
Essas listas resumem algumas diretrizes importantes hello, que você deve ter em mente quando você está criando tabelas, e este guia resolvê-los em mais detalhes posteriormente. Essas diretrizes são muito diferentes das diretrizes de saudação que siga para design de banco de dados relacional.  

Projetando sua toobe de solução do serviço de tabela *ler* eficiente:

* ***Design para consulta em aplicativos com alta taxa de leitura.*** Quando você estiver criando suas tabelas, pense consultas hello (especialmente Olá latência confidenciais) que será executado antes de você pensar em como você atualizará suas entidades. Isso normalmente resulta em uma solução eficiente e de alto desempenho.  
* ***Especifique PartitionKey e RowKey em suas consultas.*** *Ponto de consultas* como essas são consultas de serviço de tabela mais eficientes hello.  
* ***Considere armazenar cópias duplicadas de entidades.*** Armazenamento de tabela é barato portanto, considere armazenar Olá a mesma entidade várias vezes (com chaves diferentes) tooenable consultas mais eficientes.  
* ***Considere a desnormalização de seus dados.*** O armazenamento de tabela é barato, então considere desnormalizar seus dados. Por exemplo, armazene entidades de resumidas para que consultas de agregação de dados precisam apenas tooaccess uma única entidade.  
* ***Use valores de chave composta.*** Olá apenas as chaves que são **PartitionKey** e **RowKey**. Por exemplo, use os valores de chave composta tooenable com chave de acesso alternativo caminhos tooentities.  
* ***Use a projeção de consulta.*** Você pode reduzir a quantidade de saudação de dados que são transferidos pela rede Olá por meio de consultas que seleciona apenas os campos de saudação que necessários.  

Projetando sua toobe de solução do serviço de tabela *gravar* eficiente:  

* ***Não crie partições ativas.*** Escolha suas solicitações de chaves que permitem que você toospread por várias partições em qualquer momento.  
* ***Evite picos no tráfego.*** Suavizar o tráfego de saudação em um período de tempo razoável e evitar picos no tráfego.
* ***Não crie, necessariamente, uma tabela separada para cada tipo de entidade.*** Quando você precisar de transações atômicas em todos os tipos de entidade, você pode armazenar esses vários tipos de entidade em Olá mesma partição Olá mesma tabela.
* ***Considere a taxa de transferência máxima Olá que deve atingir.*** Você deve estar ciente das metas de escalabilidade de saudação para Olá serviço tabela e certifique-se de que seu design não causará você tooexceed-los.  

À medida que você ler este guia, verá exemplos que colocam todos esses princípios em prática.  

## <a name="design-for-querying"></a>Design para consulta
Soluções de serviço de tabela podem ser lidos com uso intensivo, com uso intensivo de gravação ou uma mistura de saudação dois. Esta seção discute Olá coisas toobear em mente quando você está projetando seu toosupport do serviço de tabela com eficiência as operações de leitura. Normalmente, um design que dá suporte a operações de leitura com eficiência também é eficiente para operações de gravação. No entanto, há considerações adicionais toobear em mente quando projetar toosupport operações de gravação, discutidas na próxima seção, Olá, [Design para modificação de dados](#design-for-data-modification).

Um bom ponto de partida para projetar seu tooenable de solução do serviço de tabela você tooread dados com eficiência são tooask "quais consultas serão necessário tooexecute tooretrieve Olá dados do meu aplicativo precisa de saudação serviço tabela?"  

> [!NOTE]
> Com hello serviço tabela, é importante tooget Olá design correto adiantado porque é difícil e caro toochange-lo mais tarde. Por exemplo, em um banco de dados relacional que é geralmente tooaddress possíveis problemas de desempenho simplesmente adicionando índices tooan banco de dados existente: isso não é uma opção com hello serviço tabela.  
> 
> 

Esta seção aborda questões importantes Olá, resolvidos quando você cria as tabelas de consulta. Olá tópicos abordados nesta seção incluem:

* [Como sua escolha de PartitionKey e RowKey afeta o desempenho da consulta](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Escolhendo uma PartitionKey apropriada](#choosing-an-appropriate-partitionkey)
* [Otimização de consultas para Olá serviço tabela](#optimizing-queries-for-the-table-service)
* [Classificando dados em Olá serviço tabela](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Como sua escolha de PartitionKey e RowKey afeta o desempenho da consulta
Olá exemplos a seguir presumem serviço de tabela hello está armazenando as entidades de funcionário com hello estrutura a seguir (a maioria dos exemplos de saudação omite Olá **Timestamp** propriedade para maior clareza):  

| *Nome da coluna* | *Tipo de dados* |
| --- | --- |
| **PartitionKey** (nome de departamento) |Cadeia de caracteres |
| **RowKey** (Id do funcionário) |Cadeia de caracteres |
| **Nome** |Cadeia de caracteres |
| **Sobrenome** |Cadeia de caracteres |
| **Idade** |Número inteiro |
| **EmailAddress** |Cadeia de caracteres |

Olá seção anterior [visão geral do serviço de tabela do Azure](#overview) descreve Olá principais recursos de saudação serviço tabela do Azure que têm uma influência direta sobre a criação de consulta. Esses resultam em Olá diretrizes gerais para a criação de consultas do serviço de tabela a seguir. Observe que a sintaxe do filtro Olá usada nos exemplos de saudação abaixo é saudação do serviço tabela API REST, para obter mais informações, consulte [consultar entidades](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* Um ***consulta*** é Olá toouse de pesquisa mais eficiente e é recomendado toobe usado para pesquisas de alto volume ou pesquisas que requerem a menor latência. Essa consulta pode usar Olá índices toolocate uma entidade individual maneira muito eficiente especificando ambos Olá **PartitionKey** e **RowKey** valores. Por exemplo: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')  
* Segundo melhor é um ***consulta de intervalo*** que usa Olá **PartitionKey** e filtros em um intervalo de **RowKey** valores tooreturn mais de uma entidade. Olá **PartitionKey** valor identifica uma partição específica e hello **RowKey** valores identificam um subconjunto de entidades Olá nessa partição. Por exemplo: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'  
* É melhor terceiro um ***partição verificação*** que usa Olá **PartitionKey** e filtros em outra propriedade de não-chave e que podem retornar mais de uma entidade. Olá **PartitionKey** valor identifica uma partição específica e valores de propriedade de saudação select para um subconjunto de entidades Olá nessa partição. Por exemplo: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'  
* Um ***Table Scan*** não inclui Olá **PartitionKey** e é muito eficiente porque ele procura todas as partições de saudação que compõem sua tabela para as entidades correspondentes. Ele executará uma verificação de tabela, independentemente de estarem ou não o filtro usa Olá **RowKey**. Por exemplo: $filter=LastName eq 'Dias'  
* As consultas que retornam várias entidades as retornam classificadas na ordem **PartitionKey** e **RowKey**. entidades de saudação reclassificação tooavoid no cliente hello, escolha um **RowKey** que define a ordem de classificação hello mais comuns.  

Observe que o uso uma "**ou**" toospecify um filtro baseado em **RowKey** valores resulta em uma verificação de partição e não é tratado como uma consulta de intervalo. Portanto, você deve evitar consultas que usam filtros, como: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')  

Para obter exemplos de código do lado do cliente que usam consultas eficientes do tooexecute Olá biblioteca de cliente de armazenamento, consulte:  

* [Executando uma consulta de ponto usando Olá biblioteca de cliente de armazenamento](#executing-a-point-query-using-the-storage-client-library)
* [Recuperando várias entidades usando LINQ](#retrieving-multiple-entities-using-linq)
* [Projeção do lado do servidor](#server-side-projection)  

Para obter exemplos de código do lado do cliente que pode lidar com a entidade de vários tipos armazenados no hello mesma tabela, consulte:  

* [Trabalhando com tipos de entidade heterogênea](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Escolhendo uma PartitionKey apropriada
A escolha do **PartitionKey** deve equilibrar Olá necessidade tooenables Olá uso EGTs (tooensure consistência) em relação a saudação requisito toodistribute suas entidades por várias partições (tooensure uma solução escalonável).  

De um lado, você pode armazenar todas as suas entidades em uma única partição, mas isso pode limitar a escalabilidade de saudação de sua solução e poderia impedir que o serviço de tabela de saudação de sendo capaz de saldo de tooload solicitações. Em Olá outro lado, você pode armazenar uma entidade por partição, que seriam altamente escalonável e que permite Olá tabela tooload balancear solicitações, mas que o impediria de uso de transações de grupo de entidade.  

O ideal **PartitionKey** é aquele que permite consultas eficientes toouse e que tem suficiente tooensure de partições sua solução é escalável. Normalmente, você descobrirá que as entidades terão uma propriedade adequada que distribui suas entidades em partições suficientes.

> [!NOTE]
> Por exemplo, em um sistema que armazena informações sobre usuários ou funcionários, UserID pode ser uma boa PartitionKey. Você pode ter várias entidades que usam uma determinado UserID como chave de partição hello. Cada entidade que armazena dados sobre um usuário é agrupada em uma única partição, e pode ser acessada por meio de transações do grupo de entidades, continuando altamente escalonável.
> 
> 

Há considerações adicionais de sua escolha do **PartitionKey** que se relacionam toohow irá inserir, atualizar e excluir entidades: consulte a seção Olá [Design para modificação de dados](#design-for-data-modification) abaixo.  

### <a name="optimizing-queries-for-hello-table-service"></a>Otimização de consultas para Olá serviço tabela
Olá serviço tabela indexa automaticamente suas entidades usando Olá **PartitionKey** e **RowKey** valores em um único índice clusterizado, Olá, portanto, o motivo que as consultas de faixas são Olá toouse mais eficiente . No entanto, não há nenhum índice que não seja o no índice clusterizado Olá Olá **PartitionKey** e **RowKey**.

Muitos projetos devem atender a pesquisa de tooenable requisitos de entidades com base em vários critérios. Por exemplo, localizar entidades de funcionário com base em email, ID de funcionário ou sobrenome. Olá seguintes padrões de seção Olá [padrões de Design de tabela](#table-design-patterns) resolver esses tipos de requisito e descrevem as maneiras de contornar fatos Olá que o serviço de tabela de saudação não fornece índices secundários:  

* [Padrão de índice secundário de dentro da partição](#intra-partition-secondary-index-pattern) -armazenar várias cópias de cada entidade usando diferentes **RowKey** valores (em Olá mesma partição) tooenable rápida e eficiente pesquisas e classificação alternativo ordena usando diferentes **RowKey** valores.  
* [Padrão de índice secundário de partição entre](#inter-partition-secondary-index-pattern) - armazenar várias cópias de cada entidade usando diferentes valores de RowKey em partições separadas ou em tabelas separadas tooenable rápida e eficientes pesquisas e classificação alternativo ordens usando diferentes **RowKey** valores.  
* [Índice de entidades padrão](#index-entities-pattern) -manter índice entidades tooenable pesquisas eficientes que retornam listas de entidades.  

### <a name="sorting-data-in-hello-table-service"></a>Classificando dados em Olá serviço tabela
Olá serviço tabela retorna entidades classificadas em ordem crescente com base em **PartitionKey** e, em seguida, por **RowKey**. Essas chaves são valores de cadeia de caracteres e tooensure valores numéricos classificados corretamente, você deve convertê-los tooa fixo de comprimento e preencha-os com zeros. Por exemplo, se hello valor de id de funcionário você usar como Olá **RowKey** é um valor inteiro, você deve converter o id de funcionário **123** muito**00000123**.  

Muitos aplicativos têm requisitos toouse dados classificados em ordens diferentes: por exemplo, classificando os funcionários por nome, unindo Data. Olá seguintes padrões de seção Olá [padrões de Design de tabela](#table-design-patterns) como ordens de classificação de tooalternate para suas entidades de endereços:  

* [Padrão de índice secundário de dentro da partição](#intra-partition-secondary-index-pattern) -armazenar várias cópias de cada entidade usando diferentes valores de RowKey (em Olá mesma partição) tooenable rápida e eficiente pesquisas e classificação alternativo ordena usando diferentes valores de RowKey.  
* [Padrão de índice secundário de partição entre](#inter-partition-secondary-index-pattern) - armazenar várias cópias de cada entidade usando diferentes valores de RowKey em partições separadas em tabelas separadas tooenable rápida e eficientes pesquisas e classificação alternativo ordens usando diferente RowKey valores.
* [O padrão da parte final do log](#log-tail-pattern) -Olá recuperar  *n*  entidades adicionada mais recentemente tooa partição usando uma **RowKey** valor classifica em inversa de data e a ordem de tempo.  

## <a name="design-for-data-modification"></a>Design para modificação de dados
Esta seção se concentra em considerações de design de saudação para otimizar as inserções, atualizações e exclusões. Em alguns casos, você precisará de compensação de saudação tooevaluate entre os designs otimizar para consultar designs otimizam modificação de dados exatamente como você faria em projetos de bancos de dados relacionais (embora técnicas Olá para o gerenciamento Olá design vantagens e desvantagens são diferentes em um banco de dados relacional). Olá seção [padrões de Design de tabela](#table-design-patterns) descreve alguns padrões de design detalhadas para Olá serviço tabela e destaca algumas essas vantagens e desvantagens. Na prática, você descobrirá que muitos designs otimizados para entidades de consulta também funcionam bem para modificar entidades.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Otimizando o desempenho de saudação de inserir, atualizar e excluir operações
tooupdate ou excluir uma entidade, você deve ser capaz de tooidentify usando Olá **PartitionKey** e **RowKey** valores. Nesse sentido, a escolha do **PartitionKey** e **RowKey** para modificar entidades deve seguir semelhante critérios tooyour opção toosupport ponto consultas porque deseja tooidentify entidades maior eficiência possível. Você não quiser toouse um ineficiente partição ou tabela verificação toolocate uma entidade em saudação do pedido toodiscover **PartitionKey** e **RowKey** valores precisar tooupdate ou excluí-lo.  

Olá seguintes padrões de seção Olá [padrões de Design de tabela](#table-design-patterns) endereço otimização de desempenho hello ou sua inserção, atualização e operações de exclusão:  

* [Exclusão de alto volume](#high-volume-delete-pattern) -habilitar exclusão de saudação de um volume alto de entidades, armazenando todas as entidades de saudação para exclusão simultânea em suas próprias tabelas separadas; você excluir entidades de saudação excluindo tabela hello.  
* [Padrão de série de dados](#data-series-pattern) -série de dados completa de armazenamento em um número de saudação toominimize única entidade de solicitações feitas.  
* [Padrão de entidades ampla](#wide-entities-pattern) -usar várias entidades lógicas toostore de entidades físicas com mais de 252 propriedades.  
* [Padrão de entidades grande](#large-entities-pattern) -valores de propriedade grande toostore do armazenamento de blob de uso.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Garantindo a consistência nas suas entidades armazenadas
Olá outro fator chave que influencia sua escolha de chaves para otimizar as modificações de dados é como tooensure consistência usando transações atômicas. Você só pode usar um toooperate EGT em entidades armazenadas em Olá mesma partição.  

Olá seguintes padrões de seção Olá [padrões de Design de tabela](#table-design-patterns) gerenciar a consistência de endereço:  

* [Padrão de índice secundário de dentro da partição](#intra-partition-secondary-index-pattern) -armazenar várias cópias de cada entidade usando diferentes **RowKey** valores (em Olá mesma partição) tooenable rápida e eficiente pesquisas e classificação alternativo ordena usando diferentes **RowKey** valores.  
* [Padrão de índice secundário de partição entre](#inter-partition-secondary-index-pattern) - armazenar várias cópias de cada entidade usando diferentes valores de RowKey em partições separadas ou em tabelas separadas tooenable rápida e eficientes pesquisas e classificação alternativo ordens usando diferentes **RowKey** valores.  
* [Padrão de transações eventualmente consistentes](#eventually-consistent-transactions-pattern) - Habilite comportamento eventualmente consistente entre limites de partição ou limites do sistema de armazenamento usando filas do Azure.
* [Índice de entidades padrão](#index-entities-pattern) -manter índice entidades tooenable pesquisas eficientes que retornam listas de entidades.  
* [Padrão de desnormalização](#denormalization-pattern) -combinar dados relacionados em conjunto em uma única entidade tooenable tooretrieve todos Olá necessário com uma consulta de ponto de dados.  
* [Padrão de série de dados](#data-series-pattern) -série de dados completa de armazenamento em um número de saudação toominimize única entidade de solicitações feitas.  

Para obter informações sobre transações de grupo de entidade, consulte a seção de saudação [transações de grupo de entidade](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Garantir seu design para modificações eficientes facilita consultas eficientes
Em muitos casos, um projeto para resultados de consultando eficientes em modificações eficientes, mas você sempre deve avaliar se esse for o caso de Olá para seu cenário específico. Alguns dos padrões de saudação na seção Olá [padrões de Design de tabela](#table-design-patterns) explicitamente avaliar variações de consulta e modificação de entidades, e você sempre deve levar em número de saudação da conta de cada tipo de operação.  

Olá seguintes padrões de seção Olá [padrões de Design de tabela](#table-design-patterns) prós e contras projetar consultas eficientes e criação de modificação de dados eficiente de endereços:  

* [Padrão de chave composta](#compound-key-pattern) -Use compostas **RowKey** valores tooenable toolookup um cliente relacionadas a dados com uma consulta única.  
* [O padrão da parte final do log](#log-tail-pattern) -Olá recuperar  *n*  entidades adicionada mais recentemente tooa partição usando uma **RowKey** valor classifica em inversa de data e a ordem de tempo.  

## <a name="encrypting-table-data"></a>Criptografando dados de tabela
Olá biblioteca de cliente de armazenamento do Azure .NET oferece suporte à criptografia de propriedades de entidade de cadeia de caracteres para inserir e substituir operações. cadeias de caracteres de saudação criptografada são armazenadas no serviço de saudação como propriedades binárias, e eles são convertidos toostrings voltar depois da descriptografia.    

Para tabelas, além de toohello política de criptografia, usuários devem especificar Olá propriedades toobe criptografado. Isso pode ser feito especificando o atributo [EncryptProperty] \(para entidades POCO que derivam de TableEntity) ou um resolvedor de criptografia nas opções de solicitação. Um resolvedor de criptografia é um delegado que usa uma chave de partição, a chave de linha e o nome da propriedade e retorna um valor booliano que indica se essa propriedade deve ser criptografada. Durante a criptografia, biblioteca de saudação do cliente usará esse toodecide informações se uma propriedade deve ser criptografada durante a gravação toohello durante a transmissão. também fornece delegado Olá possibilidade de saudação da lógica em torno de como as propriedades são criptografadas. (Por exemplo, se X, então criptografar a propriedade A; caso contrário, criptografar as propriedades A e B.) Observe que ele é necessário não tooprovide essas informações durante a leitura ou consultar entidades.

Saiba que atualmente não há suporte para a mesclagem. Como um subconjunto das propriedades pode ter sido criptografado anteriormente usando uma chave diferente, simplesmente mesclando novas propriedades de saudação e atualizar metadados Olá resultará em perda de dados. Mesclar o requer fazer serviço extra chama entidade pré-existente do tooread Olá do serviço hello, ou usando uma nova chave por propriedade, que não são adequados por motivos de desempenho.     

Para obter informações sobre como criptografar dados de tabela, confira [Criptografia do lado do cliente e Cofre da Chave do Azure para Armazenamento do Microsoft Azure](storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Relações de modelagem
Criar modelos de domínio é uma etapa importante no design de saudação dos sistemas complexos. Normalmente, você usa Olá modelagem processo tooidentify entidades e relações de saudação entre-los como uma maneira toounderstand Olá domínio corporativo e informam o design de saudação do seu sistema. Esta seção discute como você pode traduzir alguns dos tipos de relação comuns Olá encontrados no domínio modelos toodesigns para Olá serviço tabela. processo de saudação de mapeamento de um lógica tooa do modelo de dados NoSQL com base em dados-modelo físico é muito diferente da usada durante a criação de um banco de dados relacional. Design de bancos de dados relacionais geralmente supõe que um processo de normalização de dados otimizado para minimizar a redundância – e um recurso de consultando declarativo que abstrai Olá como implementação de como funciona o banco de dados de saudação.  

### <a name="one-to-many-relationships"></a>Relações um-para-muitos
Relações um-para-muitos entre objetos de domínio de negócios ocorrerem com muita frequência: por exemplo, um departamento tem muitos funcionários. Há várias relações de um-para-muitos tooimplement maneiras Olá serviço tabela cada com prós e contras que podem ser relevantes toohello cenário em particular.  

Considere o exemplo hello de uma grande empresa multinacional com dezenas de milhares de departamentos e entidades de funcionário, onde cada departamento tem muitos funcionários e cada funcionário como associada a um departamento específico. Uma abordagem é departamento separado toostore e entidades de funcionário como estes:  

![][1]

Este exemplo mostra uma relação um-para-muitos implícita entre tipos de saudação com base em Olá **PartitionKey** valor. Cada departamento pode ter muitos funcionários.  

Este exemplo também mostra uma entidade de departamento e suas entidades relacionadas funcionário em Olá mesma partição. Você pode escolher toouse diferentes partições, tabelas ou até mesmo as contas de armazenamento para tipos de entidade diferente de saudação.  

Uma abordagem alternativa é toodenormalize suas entidades de dados e o repositório de funcionário somente com dados desnormalizados departamento, conforme mostrado no exemplo a seguir de saudação. Neste cenário específico, essa abordagem desnormalizada pode não ser Olá melhor se você tem detalhes Olá requisito toobe toochange capaz de um gerente de departamento porque toodo isso é necessário tooupdate todos os funcionários do departamento de saudação.  

![][2]

Para obter mais informações, consulte Olá [padrão desnormalização](#denormalization-pattern) posteriormente neste guia.  

Olá tabela a seguir resume os profissionais de saudação e os contras de cada uma das abordagens Olá descritas acima para armazenar entidades de departamento que têm uma relação um-para-muitos e funcionário. Você também deve considerar a frequência você espera que tooperform várias operações: pode ser aceitável toohave um design que inclui uma operação cara se essa operação acontece apenas raramente.  

<table>
<tr>
<th>Abordagem</th>
<th>Prós</th>
<th>Contras</th>
</tr>
<tr>
<td>Separar tipos de entidade, mesma partição, mesma tabela</td>
<td>
<ul>
<li>Você pode atualizar uma entidade de departamento com uma única operação.</li>
<li>Você pode usar uma consistência de toomaintain EGT se você tiver um requisito toomodify uma entidade department sempre que você atualizar/insert/excluir uma entidade funcionário. Por exemplo, se você mantiver uma contagem de funcionários do departamento para cada departamento.</li>
</ul>
</td>
<td>
<ul>
<li>Talvez seja necessário tooretrieve um funcionário e uma entidade de departamento em algumas atividades do cliente.</li>
<li>As operações de armazenamento acontecem em Olá mesmo partição. Em grandes volumes de transações, isso pode resultar em um ponto de acesso.</li>
<li>Você não pode mover um funcionário tooa departamento usando um EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Tipos de entidade separada, diferentes partições ou tabelas ou contas de armazenamento</td>
<td>
<ul>
<li>Você pode atualizar uma entidade de departamento ou funcionário com uma única operação.</li>
<li>Em grandes volumes de transações, isso pode ajudar a carga de espalhamento hello mais partições.</li>
</ul>
</td>
<td>
<ul>
<li>Talvez seja necessário tooretrieve um funcionário e uma entidade de departamento em algumas atividades do cliente.</li>
<li>Não é possível usar EGTs toomaintain consistência quando você atualização/inserção/exclusão um funcionário e atualização de um departamento. Por exemplo, a atualização de uma contagem de funcionários em uma entidade de departamento.</li>
<li>Você não pode mover um funcionário tooa departamento usando um EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Desnormalizar em um único tipo de entidade</td>
<td>
<ul>
<li>Você pode recuperar todas as informações de saudação que necessário com uma única solicitação.</li>
</ul>
</td>
<td>
<ul>
<li>Pode ser caro toomaintain consistência se você precisar de informações do departamento de tooupdate (Isso exigirá que você tooupdate todos os funcionários de saudação de um departamento).</li>
</ul>
</td>
</tr>
</table>

Como escolher entre essas opções e que os profissionais de saudação e contras são mais significativas, depende de seus cenários de aplicativo específico. Por exemplo, quantas vezes você modificar entidades departamento; todas as suas consultas de funcionário precisa de informações departamentais adicionais de saudação; como fechar tem limites de escalabilidade toohello em suas partições ou sua conta de armazenamento?  

### <a name="one-to-one-relationships"></a>Relações um-para-um
Modelos de domínio podem incluir relações um-para-um entre entidades. Se você precisar tooimplement uma relação um para um em Olá serviço tabela, você também deve escolher como toolink Olá duas entidades relacionadas, quando você precisar tooretrieve-os. Esse link pode ser implícita, com base em uma convenção de nos valores de chave hello ou explícita, armazenando um link no formulário de saudação do **PartitionKey** e **RowKey** valores em cada entidade tooits relacionados de entidades. Para obter uma discussão de se você deve armazenar Olá entidades relacionadas no hello mesma partição, consulte a seção Olá [um-para-muitos relações](#one-to-many-relationships).  

Observe que também há considerações de implementação que podem levar relações um para um tooimplement no serviço de tabela hello:  

* Controlando grandes entidades (para obter mais informações, consulte [Padrão de grandes entidades](#large-entities-pattern)).  
* A implementação de controles de acesso (para saber mais, consulte [Controlando o acesso com assinaturas de acesso compartilhado](#controlling-access-with-shared-access-signatures)).  

### <a name="join-in-hello-client"></a>Ingressar no cliente Olá
Embora existam relações de toomodel maneiras na Olá serviço tabela, você deve não se esqueça de que dois motivos principais Olá para usar o serviço de tabela de saudação são escalabilidade e desempenho. Se você encontrar que são modelagem muitas relações que comprometer o desempenho de saudação e a escalabilidade de sua solução, você deve se perguntar que se é necessário toobuild todos Olá relações de dados ao seu design de tabela. Você pode ser capaz de toosimplify design de saudação e melhorar a escalabilidade de saudação e desempenho de sua solução, se você permitir que o aplicativo cliente executar qualquer junções necessárias.  

Por exemplo, se você tiver tabelas pequenas que contêm dados que não se altera muita frequência, em seguida, você pode recuperar esses dados uma vez e armazene em cache no cliente de saudação. Isso pode evitar as idas e voltas repetidas tooretrieve Olá os mesmos dados. Exemplos de hello, examinamos neste guia, hello conjunto de departamentos em uma pequena empresa está provavelmente toobe pequeno e raramente tornando um bom candidato para dados que o aplicativo cliente pode baixar uma vez e o cache como pesquisar dados de alteração.  

### <a name="inheritance-relationships"></a>Relações de herança
Se seu aplicativo cliente usa um conjunto de classes que fazem parte de um entidades de negócios de toorepresent de relação de herança, você pode facilmente persistir as entidades no hello serviço tabela. Por exemplo, você pode ter Olá após o conjunto de classes definidas em seu aplicativo cliente onde **pessoa** é uma classe abstrata.

![][3]

Você pode manter instâncias das duas classes concretas Olá no hello serviço tabela usando uma única tabela pessoa usando entidades em que se parecem com isso:  

![][4]

Para obter mais informações sobre como trabalhar com vários tipos de entidade Olá mesma tabela no código do cliente, consulte a seção de saudação [trabalhando com tipos de entidade heterogêneos](#working-with-heterogeneous-entity-types) posteriormente neste guia. Isso fornece exemplos de como toorecognize Olá tipo de entidade no código do cliente.  

## <a name="table-design-patterns"></a>Padrões de design de tabela
Nas seções anteriores, você viu alguns discussões detalhadas sobre como toooptimize sua tabela de design para recuperar dados entidade usando consultas e para inserir, atualizar e excluir dados de entidade. Esta seção descreve alguns padrões adequados para uso com soluções de serviço Tabela. Além disso, você verá como praticamente abordar alguns dos problemas de saudação e compensações geradas anteriormente neste guia. Olá diagrama a seguir resume as relações de saudação entre diferentes padrões de saudação:  

![][5]

mapa de padrão de saudação acima destaca algumas relações entre os padrões (azuis) e os padrões (laranja) são documentados neste guia. Certamente há muitos outros padrões que vale a pena considerar. Por exemplo, um dos principais cenários de saudação de serviço tabela é Olá toouse [padrão de exibição materializada](https://msdn.microsoft.com/library/azure/dn589782.aspx) de saudação [comando consulta responsabilidade CQRS (segregação)](https://msdn.microsoft.com/library/azure/jj554200.aspx) padrão.  

### <a name="intra-partition-secondary-index-pattern"></a>Padrão de índice secundário intrapartição
Armazenar várias cópias de cada entidade usando diferentes **RowKey** valores (em Olá mesma partição) tooenable rápida e eficiente pesquisas e classificação alternativo ordena usando diferentes **RowKey** valores. Atualizações entre as cópias podem ser mantidas consistentes usando EGTs.  

#### <a name="context-and-problem"></a>Contexto e problema
Olá serviço tabela indexa automaticamente entidades usando Olá **PartitionKey** e **RowKey** valores. Isso permite que um tooretrieve de aplicativo do cliente uma entidade com eficiência usando esses valores. Por exemplo, usando a estrutura da tabela Olá mostrada abaixo, um aplicativo cliente pode usar uma consulta de ponto tooretrieve uma entidade funcionário individual usando o nome do departamento hello e id de funcionário hello (Olá **PartitionKey** e  **RowKey** valores). Um cliente também pode recuperar entidades classificadas por ID de funcionário dentro de cada departamento.

![][6]

Se você deseja toobe capaz de toofind uma entidade funcionário com base no valor de saudação de outra propriedade, como endereço de email, você deve usar um toofind de verificação de partição uma correspondência menos eficiente. Isso ocorre porque o serviço de tabela de saudação não fornece índices secundários. Além disso, não há nenhuma opção toorequest uma lista de funcionários classificados em uma ordem diferente daquela **RowKey** ordem.  

#### <a name="solution"></a>Solução
toowork em torno de falta de saudação de índices secundários, você pode armazenar várias cópias de cada entidade com cada cópia usando outro **RowKey** valor. Se você armazenar uma entidade com estruturas de saudação mostradas abaixo, você pode recuperar com eficiência entidades de funcionário com base na id de funcionário ou de endereço de email. Olá valores de prefixo de saudação **RowKey**, "empid_" e "email_" permitem que você tooquery para um único funcionário ou um intervalo de funcionários por meio de um intervalo de endereços de email ou ids de funcionário.  

![][7]

Olá dois critérios de filtro (um pesquisar por id de funcionário e um pesquisar por endereço de email) a seguir especifica consultas:  

* $filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')  
* $filter=(PartitionKey eq 'Sales') e (RowKey eq 'email_jonesj@contoso.com')  

Se você consultar um intervalo de entidades de funcionário, você pode especificar um intervalo classificados em ordem de id de funcionário, ou um intervalo classificados em ordem de endereço de email por meio de consulta para entidades com o prefixo apropriado de saudação em hello **RowKey**.  

* usam de todos os funcionários de Olá Olá departamento de vendas com uma id de funcionário Olá intervalo 000100 too000199 toofind: $filter = (PartitionKey eq 'Vendas') e (RowKey ge 'empid_000100') e (RowKey le 'empid_000199')  
* toofind todos Olá funcionários do departamento de vendas de saudação com um endereço de email a partir Olá letra 'a' uso: $filter = (PartitionKey eq 'Vendas') e (RowKey ge 'email_a') e (RowKey lt 'email_b')  
  
  Observe que a sintaxe do filtro Olá usada nos exemplos de saudação acima é saudação do serviço tabela API REST, para obter mais informações, consulte [consultar entidades](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Armazenamento de tabela é relativamente barata toouse Olá custo sobrecarga de armazenamento de dados duplicados não deve ser a principal preocupação. No entanto, você deve sempre avalie o custo de saudação do seu design com base nas necessidades de armazenamento previstas e somente adicionar consultas de saudação toosupport entidades duplicadas que executará seu aplicativo cliente.  
* Como entidades de índice secundário Olá são armazenadas em Olá mesma partição como entidades original hello, certifique-se de que você não exceda os destinos de escalabilidade Olá para uma partição específica.  
* Você pode manter suas entidades duplicadas consistentes entre si usando EGTs tooupdate Olá duas cópias da entidade Olá atomicamente. Isso implica que você deve armazenar todas as cópias de uma entidade em Olá mesma partição. Para obter mais informações, consulte a seção de saudação [usando transações de grupo de entidade](#entity-group-transactions).  
* Olá valor usado para Olá **RowKey** devem ser exclusivos para cada entidade. Considere o uso de valores de chave composta.  
* Preenchimento de valores numéricos em Olá **RowKey** (por exemplo, id de funcionário Olá 000223), permite corrigir a classificação e filtragem de limites com base em superiores e inferiores.  
* Não é necessariamente necessário tooduplicate todas as propriedades de saudação da entidade. Por exemplo, se hello consultas entidades de saudação de pesquisa usando Olá email endereços em Olá **RowKey** nunca precisam ter a idade do funcionário hello, essas entidades podem ter Olá estrutura a seguir:

![][8]

* Ele é normalmente melhor toostore os dados duplicados e certifique-se de que você pode recuperar todos os dados de saudação necessário com uma única consulta, que toouse uma consulta toolocate uma entidade e outra saudação de toolookup necessários dados.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando seu aplicativo cliente precisa tooretrieve entidades usando uma variedade de diferentes chaves, quando o cliente precisa tooretrieve entidades diferentes ordens de classificação e onde você pode identificar cada entidade usando uma variedade de valores exclusivos. No entanto, você deve ter certeza de não exceder os limites de escalabilidade de partição Olá durante a execução de pesquisas de entidade usando Olá diferente **RowKey** valores.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de índice secundário entre partições](#inter-partition-secondary-index-pattern)
* [Padrão de chave composta](#compound-key-pattern)
* [Transações do Grupo de Entidades](#entity-group-transactions)
* [Trabalhando com tipos de entidade heterogênea](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Padrão de índice secundário entre partições
Armazenar várias cópias de cada entidade usando diferentes **RowKey** valores em partições separadas ou em tabelas separadas tooenable rápida e eficiente pesquisas e ordens de classificação alternativa usando diferentes **RowKey**valores.  

#### <a name="context-and-problem"></a>Contexto e problema
Olá serviço tabela indexa automaticamente entidades usando Olá **PartitionKey** e **RowKey** valores. Isso permite que um tooretrieve de aplicativo do cliente uma entidade com eficiência usando esses valores. Por exemplo, usando a estrutura da tabela Olá mostrada abaixo, um aplicativo cliente pode usar uma consulta de ponto tooretrieve uma entidade funcionário individual usando o nome do departamento hello e id de funcionário hello (Olá **PartitionKey** e  **RowKey** valores). Um cliente também pode recuperar entidades classificadas por ID de funcionário dentro de cada departamento.  

![][9]

Se você deseja toobe capaz de toofind uma entidade funcionário com base no valor de saudação de outra propriedade, como endereço de email, você deve usar um toofind de verificação de partição uma correspondência menos eficiente. Isso ocorre porque o serviço de tabela de saudação não fornece índices secundários. Além disso, não há nenhuma opção toorequest uma lista de funcionários classificados em uma ordem diferente daquela **RowKey** ordem.  

Você está prevendo um volume muito alto de transações em relação a essas entidades e deseja toominimize risco de saudação do hello limitação seu cliente de serviço de tabela.  

#### <a name="solution"></a>Solução
toowork em torno de falta de saudação de índices secundários, você pode armazenar várias cópias de cada entidade com cada cópia usando diferentes **PartitionKey** e **RowKey** valores. Se você armazenar uma entidade com estruturas de saudação mostradas abaixo, você pode recuperar com eficiência entidades de funcionário com base na id de funcionário ou de endereço de email. Olá valores de prefixo de saudação **PartitionKey**, "empid_" e "email_" permitem que você tooidentify que o índice que você deseja toouse para uma consulta.  

![][10]

Olá dois critérios de filtro (um pesquisar por id de funcionário e um pesquisar por endereço de email) a seguir especifica consultas:  

* $filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')
* $filter=(PartitionKey eq 'email_Sales') e (RowKey eq 'jonesj@contoso.com')  

Se você consultar um intervalo de entidades de funcionário, você pode especificar um intervalo classificados em ordem de id de funcionário, ou um intervalo classificados em ordem de endereço de email por meio de consulta para entidades com o prefixo apropriado de saudação em hello **RowKey**.  

* toofind todos Olá funcionários Olá departamento de vendas com uma id de funcionário no intervalo de saudação **000100** muito**000199** classificados no uso de ordem de id de funcionário: $filter = (PartitionKey eq ' empid_Sales') e (RowKey ge ' 000100') e (RowKey le '000199')  
* toofind todos os funcionários Olá Olá departamento de vendas com um endereço de email que começa com 'a' classificado no uso de ordem de endereço de email: $filter = (PartitionKey eq ' email_Sales') e (RowKey ge 'a') e (RowKey lt 'b')  

Observe que a sintaxe do filtro Olá usada nos exemplos de saudação acima é saudação do serviço tabela API REST, para obter mais informações, consulte [consultar entidades](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Você pode manter suas entidades duplicadas eventualmente consistentes entre si usando Olá [padrão de transações finalmente consistente](#eventually-consistent-transactions-pattern) entidades do toomaintain Olá índice primário e secundário.  
* Armazenamento de tabela é relativamente barata toouse Olá custo sobrecarga de armazenamento de dados duplicados não deve ser a principal preocupação. No entanto, você deve sempre avalie o custo de saudação do seu design com base nas necessidades de armazenamento previstas e somente adicionar consultas de saudação toosupport entidades duplicadas que executará seu aplicativo cliente.  
* Olá valor usado para Olá **RowKey** devem ser exclusivos para cada entidade. Considere o uso de valores de chave composta.  
* Preenchimento de valores numéricos em Olá **RowKey** (por exemplo, id de funcionário Olá 000223), permite corrigir a classificação e filtragem de limites com base em superiores e inferiores.  
* Não é necessariamente necessário tooduplicate todas as propriedades de saudação da entidade. Por exemplo, se hello consultas entidades de saudação de pesquisa usando Olá email endereços em Olá **RowKey** nunca precisam ter a idade do funcionário hello, essas entidades podem ter Olá estrutura a seguir:
  
  ![][11]
* É normalmente melhor dados duplicados toostore e certifique-se de que você pode recuperar todos os dados de saudação que necessário com uma única consulta de toouse toolocate de uma consulta usando uma entidade Olá índice secundário e outro toolookup Olá dados necessários no índice primário hello.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando seu aplicativo cliente precisa tooretrieve entidades usando uma variedade de diferentes chaves, quando o cliente precisa tooretrieve entidades diferentes ordens de classificação e onde você pode identificar cada entidade usando uma variedade de valores exclusivos. Use esse padrão quando você quiser tooavoid exceder os limites de escalabilidade de partição hello quando você estiver executando pesquisas de entidade usando Olá diferente **RowKey** valores.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de transações eventualmente consistentes](#eventually-consistent-transactions-pattern)  
* [Padrão de índice secundário intrapartição](#intra-partition-secondary-index-pattern)  
* [Padrão de chave composta](#compound-key-pattern)  
* [Transações do Grupo de Entidades](#entity-group-transactions)  
* [Trabalhando com tipos de entidade heterogênea](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Padrão de transações eventualmente consistentes
Habilite comportamento eventualmente consistente entre limites de partição ou limites do sistema de armazenamento usando filas do Azure.  

#### <a name="context-and-problem"></a>Contexto e problema
EGTs habilitar transações atômicas entre várias entidades que compartilham Olá mesma chave de partição. Por motivos de escalabilidade e desempenho, você pode decidir toostore entidades que têm requisitos de consistência em partições separadas ou em um sistema de armazenamento separado: nesse cenário, você não pode usar EGTs toomaintain consistência. Por exemplo, você pode ter uma consistência eventual do requisito toomaintain entre:  

* Entidades armazenadas em duas partições diferentes na mesma tabela, em tabelas diferentes, em diferentes contas de armazenamento de saudação.  
* Uma entidade armazenado no hello serviço tabela e um blob armazenado no serviço Blob da saudação.  
* Uma entidade armazenada no serviço de tabela hello e um arquivo em um sistema de arquivos.  
* Uma entidade armazenar em Olá serviço tabela ainda indexadas usando o serviço de pesquisa do Azure hello.  

#### <a name="solution"></a>Solução
Ao usar as filas do Azure, você pode implementar uma solução que fornece consistência eventual em duas ou mais partições ou sistemas de armazenamento.
tooillustrate essa abordagem, suponha que você tiver um requisito toobe tooarchive capaz antigo funcionário entidades. Entidades antigas de funcionário raramente são consultadas e devem ser excluídas de todas as atividades que lidam com funcionários atuais. tooimplement esse requisito é armazenar funcionários ativos em Olá **atual** tabela e funcionários antigos Olá **arquivamento** tabela. Arquivamento de um funcionário requer toodelete entidade de saudação do hello **atual** de tabela e adicionar Olá entidade toohello **arquivamento** tabela, mas você não pode usar um tooperform EGT essas duas operações. o risco de saudação tooavoid que uma falha faz com que uma entidade tooappear nas tabelas de ambos ou nenhum, operação do arquivo hello deve ser finalmente consistente. Hello diagrama sequência a seguir descreve as etapas de saudação nesta operação. Mais detalhes são fornecidos para caminhos de exceção no texto a seguir hello.  

![][12]

Um cliente inicia a operação de arquivo morto de saudação colocando uma mensagem em uma fila do Azure, em que o funcionário do exemplo tooarchive #456. Uma função de trabalho pesquisa a fila de saudação novas mensagens; Quando encontrar um, ele lê a mensagem de saudação e deixa uma cópia oculta na fila de saudação. função de trabalho Olá próxima busca uma cópia da entidade de saudação do hello **atual** da tabela, insere uma cópia da saudação **arquivamento** tabela e, em seguida, exclui Olá original da saudação **atual**tabela. Por fim, se não houver erros de etapas anteriores Olá, função de trabalho Olá exclui mensagem oculta Olá da fila de saudação.  

Neste exemplo, a etapa 4 insere funcionário Olá Olá **arquivamento** tabela. Ela pode adicionar tooa blob funcionário Olá Olá serviço Blob ou um arquivo em um sistema de arquivos.  

#### <a name="recovering-from-failures"></a>Recuperando de falhas
É importante que Olá operações nas etapas **4** e **5** devem ser *idempotente* no caso de função de trabalho Olá precisa de operação de arquivamento toorestart hello. Se você estiver usando o serviço de tabela hello, etapa **4** você deve usar uma operação "inserir ou substituir"; para a etapa **5** você deve usar um "Excluir se existe" operação na biblioteca de cliente Olá você está usando. Se você estiver usando outro sistema de armazenamento, deve usar uma operação idempotente apropriada.  

Se a função de trabalho Olá nunca conclui a etapa **6**, em seguida, depois que uma mensagem de saudação do tempo limite é exibida novamente na fila de saudação pronto para Olá trabalho função tootry tooreprocess-lo. função de trabalho Olá pode verificar quantas vezes uma mensagem na fila de saudação foi lido e, se necessário, o sinalizador é uma mensagem de "suspeita" para investigação, enviando-tooa separar fila. Para obter mais informações sobre a leitura de fila de mensagens e verificando Olá dequeue contagem, consulte [receber mensagens](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Alguns erros de serviços de tabela e fila Olá são erros transitórios, e o aplicativo cliente deve incluir toohandle de lógica de repetição adequada-los.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Esta solução não fornece isolamento da transação. Por exemplo, um cliente pode ler Olá **atual** e **arquivamento** tabelas quando a função de trabalho Olá foi entre as etapas **4** e **5**e consulte um modo de exibição inconsistente dos dados de saudação. Observe que os dados de saudação será consistentes eventualmente.  
* Você deve certificar-se de que as etapas 4 e 5 são idempotentes na consistência eventual tooensure da ordem.  
* Você pode dimensionar a solução hello usando várias filas e instâncias de função de trabalho.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando quiser que a consistência eventual tooguarantee entre entidades que existem nas tabelas ou partições diferentes. Você pode estender esse consistência eventual de tooensure padrão para operações de serviço de tabela hello e serviço de Blob hello e outras fontes de dados não é do armazenamento do Azure, como sistema de arquivos de banco de dados ou hello.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Transações do Grupo de Entidades](#entity-group-transactions)  
* [Mesclar ou substituir](#merge-or-replace)  

> [!NOTE]
> Se o isolamento de transação é uma solução tooyour importante, considere reprojetar sua tooenable tabelas você toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Padrão de entidades de índice
Manter o índice entidades tooenable pesquisas eficientes que retornam listas de entidades.  

#### <a name="context-and-problem"></a>Contexto e problema
Olá serviço tabela indexa automaticamente entidades usando Olá **PartitionKey** e **RowKey** valores. Isso permite que um aplicativo de cliente tooretrieve uma entidade com eficiência usando uma consulta de ponto. Por exemplo, usando a estrutura da tabela Olá mostrada abaixo, um aplicativo cliente pode recuperar de maneira eficiente uma entidade funcionário individual usando o nome do departamento hello e id de funcionário hello (Olá **PartitionKey** e **RowKey** ).  

![][13]

Se você deseja toobe tooretrieve capaz de obter uma lista de entidades de funcionário com base no valor de saudação de outra propriedade não exclusivo, como seu sobrenome, você deve usar uma partição menos eficiente verificar correspondências toofind em vez de usar um índice toolook-los até diretamente. Isso ocorre porque o serviço de tabela de saudação não fornece índices secundários.  

#### <a name="solution"></a>Solução
pesquisa de tooenable por sobrenome com estrutura de entidade Olá mostrada acima, você deve manter a lista de ids de funcionário. Se você quiser entidades de funcionário de saudação tooretrieve com um determinado sobrenome, como Jones, deve primeiro localizar lista Olá de ids de funcionário para os funcionários com Jones como sobrenome e, em seguida, recuperar as entidades do funcionário. Há três opções principais para armazenar as listas de saudação de ids de funcionário:  

* Use o armazenamento de blobs.  
* Crie entidades de índice no hello mesma partição como entidades de funcionário hello.  
* Crie entidades de índice em uma partição ou tabela separada.  

<u>Opção n°. 1: usar o armazenamento de blob</u>  

Opção de primeira Olá, você criou um blob para cada sobrenome exclusivo e em cada repositório de blob uma lista de saudação **PartitionKey** (departamento) e **RowKey** valores (id de funcionário) para os funcionários que têm ou último nome. Quando você adicionar ou excluir um funcionário, você deve garantir que Olá conteúdo blob relevantes Olá é finalmente consistente com entidades de funcionário hello.  

<u>Opção #2:</u> criar entidades de índice na mesma partição de Olá  

Para a segunda opção de Olá, use as entidades de índice que armazenam Olá seguintes dados:  

![][14]

Olá **EmployeeIDs** propriedade contém uma lista de ids de funcionário para os funcionários com o nome do último Olá armazenado em Olá **RowKey**.  

Olá, etapas a seguir descrevem o processo de saudação que você deve seguir quando você estiver adicionando um novo funcionário, se você estiver usando a opção de segundo hello. Neste exemplo, estamos adicionando um funcionário com Id 000152 e um sobrenome Jones Olá departamento de vendas:  

1. Recuperar Olá índice entidade com uma **PartitionKey** valor "Vendas" e hello **RowKey** valor "Jones". Salve Olá ETag do toouse entidade na etapa 2.  
2. Criar uma transação de grupo de entidade (ou seja, uma operação em lote) que insere a nova entidade de funcionário hello (**PartitionKey** valor "Vendas" e **RowKey** valor "000152"), e as atualizações Olá entidade de índice ( **PartitionKey** valor "Vendas" e **RowKey** valor "Jones"), adicionando Olá nova employee id toohello lista no campo de EmployeeIDs de saudação. Para saber mais sobre transações de grupo de entidades, confira a seção [Transações de grupo de entidades](#entity-group-transactions).  
3. Se a transação de grupo de entidades Olá falhar devido a um erro de simultaneidade otimista (apenas alguém tiver modificado entidade de índice Olá), será necessário toostart sobre na etapa 1 novamente.  

Se você estiver usando a opção de segundo hello, você pode usar um toodeleting de abordagem semelhante um funcionário. Alterar sobrenome do funcionário é um pouco mais complexo, pois você precisará tooexecute uma transação de grupo de entidades que atualiza três entidades: Olá entidade employee, entidade de índice Olá antigo nome do último hello e entidade índice Olá Olá novo sobrenome. Você deve recuperar cada entidade antes de fazer alterações na ordem de valores de ETag Olá tooretrieve que você pode usar tooperform Olá atualizações usando simultaneidade otimista.  

Olá, etapas a seguir descrevem o processo de saudação que você deve seguir ao toolook todos os funcionários de saudação com um determinado sobrenome em um departamento é necessário se você estiver usando a opção de segundo hello. Neste exemplo, estamos procurando todos os funcionários de saudação com Sobrenome Jones Olá departamento de vendas:  

1. Recuperar Olá índice entidade com uma **PartitionKey** valor "Vendas" e hello **RowKey** valor "Jones".  
2. Analise a lista de saudação do funcionário Ids no campo de EmployeeIDs hello.  
3. Se você precisar de informações adicionais sobre cada um desses funcionários (como seus endereços de email), recuperar cada uma das entidades de funcionário hello usando **PartitionKey** valor "Vendas" e **RowKey** valores de lista de saudação de funcionários que você obteve na etapa 2.  

<u>Opção 3:</u> criar entidades de índice em uma partição ou tabela separada  

Para a terceira opção de hello, usam as entidades de índice que armazenam Olá seguintes dados:  

![][15]

Olá **EmployeeIDs** propriedade contém uma lista de ids de funcionário para os funcionários com o nome do último Olá armazenado em Olá **RowKey**.  

Com a opção de terceiro hello, você não pode usar EGTs toomaintain consistência porque são entidades de índice de saudação em uma partição separada de entidades de funcionário hello. Certifique-se de que as entidades de índice Olá são finalmente consistentes com entidades de funcionário hello.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Essa solução requer pelo menos duas consultas tooretrieve correspondência entidades: um tooquery Olá índice tooobtain Olá lista entidades de **RowKey** valores e, em seguida, consulta tooretrieve cada entidade na lista de saudação.  
* Considerando que uma entidade individual tem um tamanho máximo de 1 MB, a opção #2 e a opção #3 na solução de saudação supõem que lista saudação de ids de funcionário para qualquer determinado sobrenome nunca é maior que 1 MB. Se lista de saudação de ids de funcionário for provável toobe maior que 1 MB de tamanho, use a opção #1 e armazenar dados de índice de saudação no armazenamento de blob.  
* Se você usar a opção #2 (usando EGTs toohandle adicionando e excluindo os funcionários e alterando o sobrenome do funcionário) você deve avaliar se o volume de saudação de transações alcançarão os limites de escalabilidade de saudação em uma determinada partição. Se esse for o caso de Olá, você deve considerar uma solução finalmente consistente (opção &#1; ou #3) que usa filas toohandle Olá update solicita e permite que você toostore suas entidades de índice em uma partição separada de entidades de funcionário hello.  
* Opção &#2; nesta solução pressupõe que você deseja toolook backup por sobrenome dentro de um departamento: por exemplo, você deseja tooretrieve uma lista de funcionários com um sobrenome Jones Olá departamento de vendas. Se você quiser toolook capaz de toobe todos os funcionários de saudação com um sobrenome Jones em toda a organização hello, use a opção &#1; ou #3.
* Você pode implementar uma solução baseada em fila que fornece consistência eventual (consulte Olá [padrão de transações finalmente consistente](#eventually-consistent-transactions-pattern) para obter mais detalhes).  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando você toolookup um conjunto de entidades que compartilham um valor de propriedade comuns, como todos os funcionários com hello sobrenome Jones.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de chave composta](#compound-key-pattern)  
* [Padrão de transações eventualmente consistentes](#eventually-consistent-transactions-pattern)  
* [Transações do Grupo de Entidades](#entity-group-transactions)  
* [Trabalhando com tipos de entidade heterogênea](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Padrão de desnormalização
Combinar dados relacionados em uma única entidade tooenable tooretrieve todos Olá necessário com uma consulta de ponto de dados.  

#### <a name="context-and-problem"></a>Contexto e problema
Em um banco de dados relacional, você normalmente normaliza tooremove duplicação resultando em consultas que recuperam dados de várias tabelas. Se você normalize os dados nas tabelas do Azure, você deve fazer várias viagens de ida e de saudação cliente toohello server tooretrieve seus dados relacionados. Por exemplo, com estrutura de tabela Olá mostrada abaixo, você precisam de dois arredondar viagens tooretrieve Olá detalhes um departamento: uma toofetch entidade de departamento de saudação que inclui a id do Gerenciador de saudação e detalhes da outra solicitação toofetch Olá manager em um funcionário entidade.  

![][16]

#### <a name="solution"></a>Solução
Em vez de armazenar dados saudação em duas entidades separadas, desnormalizar dados saudação e manter uma cópia de detalhes do Gerenciador de saudação na entidade do departamento de saudação. Por exemplo:  

![][17]

Com entidades de departamento armazenadas com essas propriedades, você agora pode recuperar todos os detalhes de saudação que necessários sobre um departamento usando uma consulta de ponto.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Existe alguma sobrecarga de custo associada ao armazenar alguns dados duas vezes. benefício de desempenho (resultante do serviço de armazenamento do menos solicitações toohello) normalmente Hello supera aumento marginal Olá os custos de armazenamento (e esse custo é deslocado parcialmente por uma redução no número de saudação de transações precisar detalhes de saudação toofetch de um departamento).  
* Você deve manter a consistência de saudação de duas entidades do hello que armazenam informações sobre gerenciadores de. Você pode lidar com problemas de consistência de saudação usando EGTs tooupdate várias entidades em uma única transação atômica: nesse caso, Olá departamento entidades e Olá funcionário para o gerente do departamento de saudação são armazenados em Olá mesma partição.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando é frequentemente necessário toolook as informações relacionadas. Esse padrão reduz o número de saudação de consultas, que o cliente deve fazer dados de saudação tooretrieve requer.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de chave composta](#compound-key-pattern)  
* [Transações do Grupo de Entidades](#entity-group-transactions)  
* [Trabalhando com tipos de entidade heterogênea](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Padrão de chave composta
Use compostas **RowKey** valores tooenable toolookup um cliente relacionadas a dados com uma consulta única.  

#### <a name="context-and-problem"></a>Contexto e problema
Em um banco de dados relacional, é muito natural toouse junções em consultas tooreturn relacionadas a partes do cliente de toohello de dados em uma única consulta. Por exemplo, você pode usar o hello employee id toolook uma lista de entidades relacionadas que contêm o desempenho e examinar os dados para aquele funcionário.  

Suponha que você está armazenando as entidades de funcionário no serviço de tabela hello usando Olá estrutura a seguir:  

![][18]

Você também precisa de dados históricos de toostore relacionadas tooreviews e desempenho para cada funcionário do ano Olá trabalhou para sua organização e tooaccess capaz de toobe essas informações por ano. Uma opção é toocreate outra tabela que armazena as entidades com hello estrutura a seguir:  

![][19]

Observe que, com essa abordagem, você pode decidir tooduplicate algumas informações (como nome e sobrenome) Olá nova entidade tooenable tooretrieve você seus dados com uma única solicitação. No entanto, você não pode manter a consistência forte porque você não pode usar duas entidades um EGT tooupdate Olá atomicamente.  

#### <a name="solution"></a>Solução
Armazene um novo tipo de entidade em sua tabela original com entidades Olá estrutura a seguir:  

![][20]

Observe como Olá **RowKey** é agora uma chave composta composta por id de funcionário hello e ano de saudação de dados de análise de saudação que permite que você tooretrieve Olá desempenho do funcionário e analise dados com uma única solicitação para uma única entidade.  

saudação de exemplo a seguir descreve como você pode recuperar todos os dados de análise de saudação para um funcionário específico (por exemplo, um funcionário 000123 Olá departamento de vendas):  

$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Você deve usar um caractere separador adequado que torna mais fácil tooparse Olá **RowKey** valor: por exemplo, **000123_2012**.  
* Você também estiver armazenando essa entidade em Olá mesma partição como outras entidades que contêm dados relacionados a saudação mesmo funcionário, o que significa que você pode usar EGTs toomaintain forte consistência.
* Você deve considerar a frequência com a qual você consultará Olá dados toodetermine se esse padrão é apropriado.  Por exemplo, se você vai acessar Olá examinar dados raramente e Olá principais dados de funcionário geralmente que devem mantê-los como entidades separadas.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando você precisar toostore uma ou mais entidades relacionadas que você consulta com frequência.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Transações do Grupo de Entidades](#entity-group-transactions)  
* [Trabalhando com tipos de entidade heterogênea](#working-with-heterogeneous-entity-types)  
* [Padrão de transações eventualmente consistentes](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Padrão de rastro do log
Recuperar Olá  *n*  entidades adicionada mais recentemente tooa partição usando uma **RowKey** valor classifica em inversa de data e a ordem de tempo.  

#### <a name="context-and-problem"></a>Contexto e problema
Um requisito comum é ser capaz de tooretrieve entidades Olá criado mais recentemente, por exemplo hello dez mais recentes declarações de despesas enviadas por um funcionário. Suporte de consulta de tabela um **$top** Olá de tooreturn de operação de consulta primeiro  *n*  entidades de um conjunto: não há nenhum equivalente operação tooreturn Olá últimos n entidades de consulta em um conjunto.  

#### <a name="solution"></a>Solução
Repositório Olá entidades usando um **RowKey** que naturalmente classifica em ordem inversa de data/hora ordem usando a entrada mais recente Olá sempre é Olá primeiro uma tabela de saudação.  

Por exemplo, tooretrieve capaz de toobe Olá dez mais recentes declarações de despesas enviadas por um funcionário, você pode usar um valor de escala inversa derivado Olá data/hora atual. Olá c# exemplo de código mostra uma maneira toocreate um valor de "invertido tiques" adequado para um **RowKey** que classifica do toohello mais recente do hello mais antiga:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Você pode voltar toohello valor de data hora usando Olá código a seguir:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

consulta de tabela de saudação tem esta aparência:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Você deve preencher o valor de escala inversa Olá com zeros à esquerda valor de cadeia de caracteres de saudação tooensure classifica conforme o esperado.  
* Você deve estar ciente dos destinos de escalabilidade Olá no nível de saudação de uma partição. Cuidado não criar partições com ponto de acesso.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando você precisar tooaccess entidades na ordem inversa de data/hora ou quando você precisar tooaccess hello mais recentemente adicionado entidades.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Antipadrão prefixar/acrescentar](#prepend-append-anti-pattern)  
* [Recuperando entidades](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Padrão de exclusão de alto volume
Habilitar a exclusão de saudação de um alto volume de entidades, armazenando todas as entidades de saudação para exclusão simultânea em suas próprias tabelas separadas; Excluir tabela Olá para excluir entidades de saudação.  

#### <a name="context-and-problem"></a>Contexto e problema
Muitos aplicativos excluir dados antigos que não precisa mais de aplicativo de cliente disponíveis tooa toobe ou aplicativo hello tenha arquivado tooanother mídia de armazenamento. Você geralmente identificar esses dados por uma data: por exemplo, você tem registros de toodelete a necessidade de todas as solicitações de logon mais de 60 dias.  

Um design possíveis é date de hello toouse e a hora da solicitação de logon de saudação em Olá **RowKey**:  

![][21]

Essa abordagem evita sobrecargas de partição porque o aplicativo hello pode inserir e excluir entidades de logon para cada usuário em uma partição separada. No entanto, essa abordagem pode ser dispendiosa e demorada se você tiver um grande número de entidades porque primeiro é necessário tooperform uma verificação de tabela em ordem tooidentify toodelete de entidades de saudação todas as e, em seguida, você deve excluir cada entidade antiga. Observe que você pode reduzir o número de saudação de viagens de ida e toohello servidor necessário toodelete Olá entidades antigo por envio em lote de várias solicitações de exclusão em EGTs.  

#### <a name="solution"></a>Solução
Use uma tabela separada para cada dia de tentativas de logon. Você pode usar o design de entidade Olá acima tooavoid pontos de acesso quando você estiver inserindo entidades e excluir entidades antigas agora é simplesmente uma questão de excluir uma tabela de todos os dias (uma única operação de armazenamento), em vez de Localizando e excluindo centenas e milhares de entidades de logon individuais diariamente.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Seu design dá suporte a outras maneiras em que o aplicativo usará dados hello como pesquisar entidades específicas, vinculando com outros dados ou informações agregadas de geração?  
* O design evita pontos de acesso quando você está inserindo novas entidades?  
* Esperado um atraso, se você quiser tooreuse Olá mesmo nome da tabela após a exclusão. É melhor tooalways usar nomes de tabela exclusivo.  
* Espere alguns limitação quando você usa uma nova tabela primeiro enquanto hello serviço tabela aprende os padrões de acesso hello e distribui Olá partições em nós. Você deve considerar a frequência com a qual você precisa toocreate novas tabelas.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando você tem um volume alto de entidades que você deve excluir a saudação simultaneamente.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Transações do Grupo de Entidades](#entity-group-transactions)
* [Modificando entidades](#modifying-entities)  

### <a name="data-series-pattern"></a>Padrão de série de dados
Série de dados completo do repositório de entidade única toominimize Olá inúmeras solicitações feitas.  

#### <a name="context-and-problem"></a>Contexto e problema
Um cenário comum é para um aplicativo toostore uma série de dados que normalmente precisa tooretrieve todos de uma vez. Por exemplo, seu aplicativo pode registrar quantas mensagens Instantâneas cada funcionário envia a cada hora e, em seguida, use este tooplot informações quantas mensagens cada usuário enviado pela Olá 24 horas anteriores. Um projeto pode ser entidades de 24 toostore para cada funcionário:  

![][22]

Com esse design, você pode facilmente localizar e atualizar Olá entidade tooupdate para cada funcionário sempre que o aplicativo hello precisa tooupdate valor de contagem de mensagem de saudação. No entanto, tooretrieve Olá informações tooplot um gráfico da atividade Olá Olá anterior 24 horas, você deve recuperar 24 entidades.  

#### <a name="solution"></a>Solução
Use Olá design com uma contagem de mensagem propriedade separada toostore Olá a seguir para cada hora:  

![][23]

Com esse design, você pode usar uma contagem de mensagem mesclagem operação tooupdate Olá para um funcionário para uma hora específica. Agora, você pode recuperar todas as informações de Olá, é necessário que o gráfico de saudação tooplot usando uma solicitação para uma única entidade.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Se a série de dados completa não couber em uma única entidade (uma entidade pode ter propriedades too252), use um repositório de dados alternativos, como um blob.  
* Se você tiver vários clientes simultaneamente uma entidade de atualização, você precisará Olá toouse **ETag** tooimplement a simultaneidade otimista. Se você tiver muitos clientes, poderá enfrentar alta contenção.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando você precisar tooupdate e recuperar uma série de dados associada a uma entidade individual.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de grandes entidades](#large-entities-pattern)  
* [Mesclar ou substituir](#merge-or-replace)  
* [Padrão de transações finalmente consistente](#eventually-consistent-transactions-pattern) (se você estiver armazenando série de dados de saudação em um blob)  

### <a name="wide-entities-pattern"></a>Padrão de entidades longas
Use várias entidades lógicas toostore de entidades físicas com mais de 252 propriedades.  

#### <a name="context-and-problem"></a>Contexto e problema
Uma entidade individual pode ter não mais do que 252 propriedades (excluindo as propriedades de sistema obrigatória Olá) e não é possível armazenar mais de 1 MB de dados no total. Em um banco de dados relacional, você normalmente obteria round os limites de tamanho de saudação de uma linha, adicionando uma nova tabela e impor uma relação de 1 para 1 entre eles.  

#### <a name="solution"></a>Solução
Usando o serviço de tabela hello, você pode armazenar um objeto único de grande porte com mais de 252 propriedades toorepresent de várias entidades. Por exemplo, se você quiser toostore uma contagem do número de saudação de mensagens Instantâneas enviadas por cada funcionário para Olá últimos 365 dias, você pode usar Olá design que usa duas entidades com diferentes esquemas a seguir:  

![][24]

Se você precisar toomake uma alteração que requer a atualização de ambos os tookeep entidades-los sincronizados com o outro, você pode usar um EGT. Caso contrário, você pode usar uma contagem de mensagem mesclagem única operação tooupdate Olá para um dia específico. tooretrieve todos Olá dados para um funcionário individual, você deve recuperar as duas entidades, que pode ser feito com duas solicitações eficientes que usam um **PartitionKey** e um **RowKey** valor.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Recuperar uma entidade lógica completa envolve pelo menos duas transações de armazenamento: entidade física de um tooretrieve.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando o serviço de tabela de entidades de toostore necessidade cujo tamanho ou o número de propriedades excedem os limites de saudação para uma entidade individual no hello.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Transações do Grupo de Entidades](#entity-group-transactions)
* [Mesclar ou substituir](#merge-or-replace)

### <a name="large-entities-pattern"></a>Padrão de entidades grandes
Use valores de propriedade grande de toostore de armazenamento de blob.  

#### <a name="context-and-problem"></a>Contexto e problema
Uma entidade individual não pode armazenar mais de 1 MB de dados no total. Se uma ou várias de suas propriedades armazenam valores que fazer com que o tamanho total de saudação de sua entidade tooexceed esse valor, você não pode armazenar entidade inteira Olá no hello serviço tabela.  

#### <a name="solution"></a>Solução
Se a entidade exceder 1 MB em tamanho, porque uma ou mais propriedades contêm uma grande quantidade de dados, você pode armazenar dados no serviço Blob da saudação e, em seguida, armazenar o endereço de saudação do blob de saudação em uma propriedade na entidade hello. Por exemplo, você pode armazenar fotos de saudação de um funcionário no armazenamento de blob e armazenar uma foto do link toohello em Olá **foto** propriedade da entidade funcionário:  

![][25]

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* a consistência eventual toomaintain entre entidade Olá Olá serviço tabela e dados Olá Olá serviço Blob, use Olá [padrão de transações finalmente consistente](#eventually-consistent-transactions-pattern) toomaintain suas entidades.
* Recuperar uma entidade completa envolve pelo menos duas transações de armazenamento: dados de blob de uma entidade de saudação tooretrieve e uma tooretrieve saudação.  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Use esse padrão quando você precisar entidades toostore cujo tamanho excede os limites de saudação para uma entidade individual no serviço de tabela de saudação.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de transações eventualmente consistentes](#eventually-consistent-transactions-pattern)  
* [Padrão de entidades longas](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Antipadrão prefixar/acrescentar
Aumentar a escalabilidade quando você tiver um volume alto de inserções distribuindo as inserções de saudação em várias partições.  

#### <a name="context-and-problem"></a>Contexto e problema
Acrescentando ou anexar entidades de tooyour armazenado entidades normalmente resulta em aplicativo hello adicionando novos toohello de entidades primeiro ou último partição de uma sequência de partições. Nesse caso, todas Olá inserções em um determinado momento estão ocorrendo em Olá insere mesma partição, criando um ponto de acesso que impede que o serviço de tabela de saudação do balanceamento de carga em vários nós e possivelmente está causando a escalabilidade do aplicativo toohit Olá destinos para a partição. Por exemplo, se você tiver um aplicativo que recursos e logs acesso à rede pelos funcionários, em seguida, uma estrutura de entidade, como mostrado a seguir pode resultar em Olá partição da hora atual se tornar um ponto de acesso se o volume de saudação de transações atingir meta de escalabilidade hello para uma partição individual:  

![][26]

#### <a name="solution"></a>Solução
Olá seguinte estrutura de entidade alternativo evita um ponto de acesso em qualquer partição específica como eventos de logs de aplicativo hello:  

![][27]

Observe neste exemplo como ambos Olá **PartitionKey** e **RowKey** são chaves compostas. Olá **PartitionKey** usa departamento hello e registro em log do funcionário id toodistribute Olá por várias partições.  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como tooimplement esse padrão:  

* Faz Olá chave estrutura alternativa que evita a criação de partições ativas em inserções com eficiência oferecem suporte a consultas Olá seu aplicativo cliente faz?  
* O volume esperado de transações significa que são provavelmente tooreach alvos de escalabilidade de saudação para uma partição específica e ser monitoradas pelo serviço de armazenamento de saudação?  

#### <a name="when-toouse-this-pattern"></a>Quando toouse esse padrão
Evite o antipreceda padrão de / anexar hello quando o volume de transações é provavelmente tooresult na limitação pelo serviço de armazenamento hello quando você acessar uma partição ativa.  

#### <a name="related-patterns-and-guidance"></a>Diretrizes e padrões relacionados
Olá padrões e diretrizes a seguir também podem ser relevantes ao implementar esse padrão:  

* [Padrão de chave composta](#compound-key-pattern)  
* [Padrão de final do log](#log-tail-pattern)  
* [Modificando entidades](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Antipadrão de dados de log
Normalmente, você deve usar o hello serviço Blob em vez da saudação dados de log de toostore de serviço de tabela.  

#### <a name="context-and-problem"></a>Contexto e problema
Caso de uso de um comum para dados de log são tooretrieve uma seleção de entradas de log para um intervalo de data/hora específico: por exemplo, você deseja toofind Olá a todas as mensagens de erro e críticas que seu aplicativo conectado de 15:04 15:06 em uma data específica. Não deseja toouse Olá data e hora da partição Olá log mensagem toodetermine Olá Salvar log entidades: que resulta em uma partição ativa porque compartilham a qualquer momento, todas as entidades de log Olá Olá mesmo **PartitionKey** valor (consulte a seção Olá [coloque/anexar um padrão](#prepend-append-anti-pattern)). Por exemplo, Olá esquema de entidade para uma mensagem de log a seguir resulta em uma partição ativa porque o aplicativo hello grava todas as mensagens de log toohello partição para Olá atual data e hora:  

![][28]

Neste exemplo, Olá **RowKey** inclui date de hello e a hora da saudação tooensure de mensagem de log que as mensagens de log são armazenadas classificados em ordem de data/hora e uma id de mensagem no caso de várias mensagens de log compartilham Olá iguais à data e hora.  

Outra abordagem é toouse uma **PartitionKey** que garante que o aplicativo hello grava mensagens em um intervalo de partições. Por exemplo, se a fonte de Olá Olá da mensagem de log fornece uma maneira toodistribute mensagens através de numerosas partições, você pode usar o hello esquema de entidade a seguir:  

![][29]

No entanto, o problema de saudação com esse esquema é que tooretrieve todos Olá mensagens de log para um período de tempo específico que você deve pesquisar cada partição na tabela de saudação.

#### <a name="solution"></a>Solução
Olá anterior seção Olá realçado problema de tentar toouse Olá entradas de log de toostore de serviço de tabela e sugerido dois insatisfatório, projeta. Uma solução levou tooa hot partição com o risco de saudação do baixo desempenho de gravação de mensagens de log; Olá outra solução resultou em desempenho ruim de consulta devido a saudação requisito tooscan cada partição em mensagens de log de tooretrieve Olá tabela para um período de tempo específico. Armazenamento de blob oferece uma solução melhor para esse tipo de cenário e isso é como o Azure Storage Analytics armazena Olá log dados coletados por ela.  

Esta seção descreve como análise de armazenamento armazena dados de log no armazenamento de blob como ilustração desses dados toostoring abordagem normalmente consultado por intervalo.  

O Storage Analytics armazena mensagens de log em um formato delimitado em vários blobs. formato delimitada Olá torna mais fácil para um cliente de dados do aplicativo tooparse saudação na mensagem de saudação do log.  

Análise de armazenamento usa uma convenção de nomenclatura para os blobs que permite que você toolocate Olá blob (ou blobs) que contêm mensagens de saudação do log que você está pesquisando. Por exemplo, um blob denominado "queue/2014/07/31/1800/000001.log" contém mensagens de log relacionados do serviço de fila de toohello por hora Olá iniciando às 18:00 em 31 de julho de 2014. Olá "000001" indica que este é o primeiro arquivo de log Olá para esse período. Análise de armazenamento também registra Olá carimbos de saudação primeiro e último log mensagens armazenadas no arquivo hello como parte dos metadados do blob hello. Olá API para permite armazenamento de blob localizar blobs em um contêiner com base em um prefixo de nome: toolocate dados de log de todos os blobs de saudação que contêm a fila por hora Olá iniciando às 18:00, você pode usar o hello prefixo "fila/2014/07/31/1800."  

Análise de armazenamento armazena em buffer as mensagens de log internamente e atualiza periodicamente o blob apropriado hello ou cria um novo com o lote mais recente de saudação de entradas de log. Isso reduz o número de saudação de gravações, ela deve executar o serviço de blob toohello.  

Se você estiver implementando uma solução semelhante em seu próprio aplicativo, você deve considerar como toomanage Olá compensação entre confiabilidade (gravando cada armazenamento de tooblob de entrada de log quando isso acontece) e o custo e a escalabilidade (buffer atualizações em seu aplicativo e gravá-los tooblob armazenamento em lotes).  

#### <a name="issues-and-considerations"></a>Problemas e considerações
Considere Olá pontos a seguir ao decidir como toostore dados de log:  

* Se você criar um design de tabela que evita potenciais partições ativas, verá que não pode acessar os dados do log com eficiência.  
* dados de log tooprocess, um cliente geralmente precisa tooload muitos registros.  
* Embora os dados de log sejam geralmente estruturados, o armazenamento de blobs pode ser uma solução melhor.  

### <a name="implementation-considerations"></a>Considerações sobre a implementação
Esta seção discute alguns Olá toobear de considerações em mente ao implementar padrões Olá descritos nas seções anteriores hello. Grande parte dessa seção usa exemplos escritos em c# que usam Olá biblioteca de cliente de armazenamento (versão 4.3.0 no momento de saudação de gravação).  

### <a name="retrieving-entities"></a>Recuperando entidades
Como discutido na seção Olá [Design de consulta](#design-for-querying), consulta mais eficiente Olá é um ponto. No entanto, em alguns cenários talvez seja necessário tooretrieve várias entidades. Esta seção descreve algumas entidades de tooretrieving abordagens comuns usando Olá biblioteca de cliente de armazenamento.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Executando uma consulta de ponto usando Olá biblioteca de cliente de armazenamento
tooexecute de maneira mais fácil de saudação uma consulta de ponto é Olá toouse **recuperar** operação de tabela, conforme mostrado no hello trecho de código c# a seguir recupera uma entidade com uma **PartitionKey** de valor "vendas" e um  **RowKey** de valor "212":  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Observe como esse exemplo espera que a entidade Olá recupera toobe do tipo **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>Recuperando várias entidades usando LINQ
Você pode recuperar várias entidades usando LINQ com a Biblioteca de cliente de armazenamento e especificando uma consulta com uma cláusula **where** . tooavoid uma verificação de tabela, você sempre deve incluir Olá **PartitionKey** valor Olá onde cláusula e se possível Olá **RowKey** valor tooavoid verificações de tabela e de partição. Olá serviço tabela oferece suporte a um conjunto limitado de toouse de (maior que, maior que ou igual, menor que, menor que ou igual, igual e não igual) de operadores de comparação em Olá onde cláusula. Olá seguinte trecho de código c# localiza todos os funcionários Olá cujo sobrenome começa com "B" (supondo que Olá **RowKey** repositórios Olá sobrenome) no departamento de vendas de saudação (supondo que Olá **PartitionKey** armazena o nome do departamento de saudação):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Observe como a consulta de saudação especifica ambos um **RowKey** e um **PartitionKey** tooensure um melhor desempenho.  

Olá, exemplo de código a seguir mostra uma funcionalidade equivalente usando a API fluente hello (para obter mais informações sobre as APIs fluente em geral, consulte [práticas recomendadas para criar uma API fluente](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> exemplo Hello aninha vários **CombineFilters** tooinclude métodos Olá três condições de filtro.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Recuperando grande número de entidades de uma consulta
Uma consulta ideal retorna uma entidade individual com base em um valor de **PartitionKey** e um valor de **RowKey**. No entanto, em alguns cenários você pode ter um requisito tooreturn muitas entidades de saudação mesma partição ou até mesmo de várias partições.  

Você sempre totalmente deve testar o desempenho de saudação do seu aplicativo nesses cenários.  

Uma consulta no serviço de tabela Olá pode retornar um máximo de 1.000 entidades simultaneamente e pode ser executada por um máximo de cinco segundos. Se hello, conjunto de resultados contiver mais de 1.000 entidades, se a consulta Olá não foi concluída dentro de cinco segundos ou se a consulta de Olá ultrapassar o limite da partição Olá, Olá serviço tabela retorna um tooenable de token de continuação Olá Olá de toorequest do aplicativo cliente próximo conjunto de entidades. Para saber mais sobre como funcionam os tokens de continuação, confira [Tempo limite e paginação de consulta](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Se você estiver usando Olá biblioteca de cliente de armazenamento, ele pode manipular automaticamente tokens de acompanhamento para você como ela retorna entidades de saudação serviço tabela. Olá c# exemplo de código seguinte usando Olá biblioteca de cliente de armazenamento automaticamente manipula os tokens de continuação se o serviço de tabela Olá retorna em uma resposta:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

Olá código c# a seguir controla os tokens de continuação explicitamente:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Usando tokens de continuação explicitamente, você pode controlar quando o aplicativo recupera o próximo segmento de dados de saudação. Por exemplo, se seu aplicativo cliente permite que os usuários toopage em entidades de saudação armazenados em uma tabela, um usuário pode decidir não toopage em todas as entidades de saudação recuperados pela consulta de saudação para que seu aplicativo só usaria uma saudação tooretrieve token de continuação lado segmento quando o usuário Olá foi concluída a paginação em todas as entidades de saudação no segmento atual hello. Essa abordagem tem vários benefícios:  

* Ele permite a quantidade de saudação de toolimit de dados tooretrieve de saudação serviço tabela e que você mova pela rede hello.  
* Ele permite que você tooperform e/s assíncrona em .NET.  
* Ele permite armazenamento de toopersistent token de continuação tooserialize Olá para que você pode continuar em caso de saudação de uma falha do aplicativo.  

> [!NOTE]
> Um token de continuação normalmente retorna um segmento que contém 1.000 entidades, embora possa ser menos. Esse também é o caso de Olá, se você limitar o número de saudação de entradas de uma consulta retorna usando **levar** tooreturn Olá primeiro n entidades que correspondem aos critérios de pesquisa: serviço de tabela Olá pode retornar um segmento que contém menos de entidades n ao longo com um tooenable de token de continuação você tooretrieve Olá entidades restantes.  
> 
> 

Olá c# código a seguir mostra como o número de saudação de toomodify de entidades retornadas dentro de um segmento de:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Projeção do lado do servidor
Uma única entidade pode ter propriedades too255 e ser too1 MB de tamanho. Consulta de tabela hello e recuperar entidades, você talvez não precise de todas as propriedades de saudação e pode evitar a transferência de dados desnecessariamente (toohelp reduzir a latência e custo). Você pode usar propriedades de saudação apenas tootransfer de projeção do lado do servidor que é necessário. Olá é um exemplo recupera apenas Olá **Email** propriedade (juntamente com **PartitionKey**, **RowKey**, **Timestamp**e  **ETag**) de entidades de saudação selecionadas pela consulta hello.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Observe como Olá **RowKey** valor estará disponível mesmo que ele não foi incluído na lista de saudação de tooretrieve de propriedades.  

### <a name="modifying-entities"></a>Modificando entidades
Olá biblioteca de cliente de armazenamento permite que você toomodify suas entidades armazenadas no serviço de tabela hello, inserção, exclusão e atualização de entidades. Você pode usar EGTs toobatch várias operações de inserção, atualização e exclusão tooreduce juntos número de saudação de viagens de ida e necessários e melhorar o desempenho de saudação de sua solução.  

Observe que exceções geradas quando Olá biblioteca de cliente de armazenamento é executada uma EGT normalmente incluem índice de saudação da entidade de saudação que causou a saudação lote toofail. Isso é útil quando você está depurando código que usa EGTs.  

Você também deve considerar como seu design afeta a forma de tratamento, por parte do cliente, das operações de simultaneidade e atualização.  

#### <a name="managing-concurrency"></a>Gerenciando simultaneidade
Por padrão, o serviço de tabela Olá implementa simultaneidade otimista no nível de saudação de entidades individuais para **inserir**, **mesclar**, e **excluir** operações, Embora seja possível para uma saudação do cliente tooforce essas verificações de toobypass do serviço de tabela. Para obter mais informações sobre como o serviço de tabela Olá gerencia simultaneidade, consulte [gerenciamento de simultaneidade no armazenamento do Microsoft Azure](storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Mesclar ou substituir
Olá **substituir** método hello **TableOperation** classe sempre substitui a entidade completa Olá Olá serviço tabela. Se você não incluir uma propriedade na solicitação de saudação quando essa propriedade não existe na entidade Olá armazenado, a solicitação de Olá remove a propriedade da saudação armazenados entidade. A menos que você deseje tooremove uma propriedade explicitamente de uma entidade armazenada, você deve incluir todas as propriedades na solicitação de saudação.  

Você pode usar o hello **mesclar** método hello **TableOperation** classe tooreduce Olá total que você envie toohello serviço de tabela quando você desejar tooupdate uma entidade de dados. Olá **mesclar** método substitui as propriedades na entidade Olá armazenado com valores de propriedade da entidade Olá incluído na solicitação hello, mas deixa intacta de propriedades na Olá armazenados entidade que não estão incluídos na solicitação de saudação. Isso é útil se você tiver grandes entidades e só precisa tooupdate um pequeno número de propriedades em uma solicitação.  

> [!NOTE]
> Olá **substituir** e **mesclar** métodos falharem se Olá entidade não existe. Como alternativa, você pode usar o hello **InsertOrReplace** e **InsertOrMerge** métodos que criar uma nova entidade se ele não existir.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Trabalhando com tipos de entidade heterogênea
Olá serviço tabela é uma *sem esquema* armazenamento de tabela que significa que uma única tabela pode armazenar entidades de vários tipos fornecendo grande flexibilidade no design. Olá, exemplo a seguir ilustra uma tabela que armazena o funcionário e entidades de departamento:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Observe que cada entidade deve ter ainda os valores de **PartitionKey**, **RowKey** e **Timestamp**, mas pode ter qualquer conjunto de propriedades. Além disso, não há nada Olá tooindicate tipo de uma entidade, a menos que você escolha toostore essas informações em algum lugar. Há duas opções para identificar o tipo de entidade hello:  

* Preceda toohello de tipo de entidade Olá **RowKey** (ou possivelmente Olá **PartitionKey**). Por exemplo, **EMPLOYEE_000123** ou **DEPARTMENT_SALES** como valores de **RowKey**.  
* Use um tipo de entidade do propriedade separada toorecord Olá conforme mostrado na tabela de saudação abaixo.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td>Funcionário</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td>Funcionário</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>department</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nome</th>
<th>Sobrenome</th>
<th>Idade</th>
<th>Email</th>
</tr>
<tr>
<td>Funcionário</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

primeira opção Hello, acrescentando toohello de tipo de entidade Olá **RowKey**, é útil se houver uma possibilidade de que duas entidades de tipos diferentes podem ter Olá mesmo valor de chave. Ele também agrupa entidades de mesmo tipo juntas na partição de saudação do hello.  

Olá, técnicas discutidas nesta seção são especialmente relevante toohello discussão [relacionamentos de herança](#inheritance-relationships) anteriormente neste guia, na seção de saudação [modelagem relações](#modelling-relationships).  

> [!NOTE]
> Você deve considerar incluir um número de versão no hello entidade valor tooenable cliente aplicativos tooevolve POCO objetos de tipo e funcionam com versões diferentes.  
> 
> 

Olá restante desta seção descreve alguns dos recursos de saudação do hello biblioteca de cliente de armazenamento que facilitam a trabalhar com vários tipos de entidade Olá mesmo tabela.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Recuperando tipos de entidade heterogênea
Se você estiver usando Olá biblioteca de cliente de armazenamento, você tem três opções para trabalhar com vários tipos de entidade.  

Se você souber o tipo de saudação da entidade Olá armazenado com um determinado **RowKey** e **PartitionKey** valores, em seguida, você pode especificar o tipo de entidade hello quando você recupera entidade Olá conforme mostrado nos exemplos de saudação dois anterior que recuperar entidades do tipo **EmployeeEntity**: [executando uma consulta de ponto usando Olá biblioteca de cliente de armazenamento](#executing-a-point-query-using-the-storage-client-library) e [recuperar várias entidades usando o LINQ](#retrieving-multiple-entities-using-linq).  

Olá segunda opção é Olá toouse **DynamicTableEntity** tipo (um recipiente de propriedades) em vez de um tipo de entidade POCO concreto (essa opção pode também melhorar o desempenho porque não há nenhuma necessidade tooserialize e desserializar entidade Olá muito. Tipos de rede). Olá código c# a seguir potencialmente recupera várias entidades de diferentes tipos de tabela Olá, mas retorna todas as entidades como **DynamicTableEntity** instâncias. Ele então usa Olá **EntityType** propriedade toodetermine Olá tipo de cada entidade:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Observe que tooretrieve outras propriedades, você deve usar o hello **TryGetValue** método hello **propriedades** propriedade Olá **DynamicTableEntity** classe.  

Uma terceira opção é toocombine usando Olá **DynamicTableEntity** tipo e uma **EntityResolver** instância. Isso permite tooresolve toomultiple POCO tipos em Olá mesma consulta. Neste exemplo, Olá **EntityResolver** representante está usando Olá **EntityType** toodistinguish de propriedade entre tipos de saudação dois da entidade que Olá consulta retornará. Olá **resolver** usa o método hello **resolvedor** delegar tooresolve **DynamicTableEntity** instâncias muito**TableEntity** instâncias.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Modificando tipos de entidade heterogênea
Tipo de saudação do tooknow de toodelete uma entidade não é necessário-e você sempre saiba tipo hello de uma entidade ao inseri-lo. No entanto, você pode usar **DynamicTableEntity** tooupdate uma entidade de tipo sem saber o tipo e sem usar uma classe de entidade POCO. Olá exemplo de código a seguir recupera uma entidade única e verifica Olá **EmployeeCount** propriedade existe antes da atualização.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Controlando o acesso com assinaturas de acesso compartilhado
Você pode usar a assinatura de acesso compartilhado (SAS) tokens tooenable cliente aplicativos toomodify (e consultar) entidades de tabela diretamente sem Olá necessidade tooauthenticate diretamente com o serviço de tabela de saudação. Normalmente, há três principais vantagens toousing SAS em seu aplicativo:  

* Você não precisa toodistribute seu armazenamento de conta tooan chave de plataforma inseguro (como um dispositivo móvel) em ordem tooallow tooaccess esse dispositivo e modificar entidades Olá serviço tabela.  
* Você pode descarregar a parte do trabalho de Olá web e executam funções de trabalho no gerenciamento de seus dispositivos de tooclient de entidades, como computadores de usuários finais e dispositivos móveis.  
* Você pode atribuir um restrita e tempo conjunto limitado de cliente de tooa de permissões (como permitir o acesso somente leitura toospecific recursos).  

Para obter mais informações sobre como usar tokens SAS com hello serviço tabela, consulte [usando assinaturas (SAS de acesso compartilhado)](storage-dotnet-shared-access-signature-part-1.md).  

No entanto, você ainda deve gerar tokens SAS Olá que conceda um cliente entidades de toohello do aplicativo no serviço de tabela Olá: você deve fazer isso em um ambiente que tem acesso seguro tooyour chaves de conta de armazenamento. Normalmente, você pode usar uma web ou trabalho função toogenerate Olá SAS tokens e enviá-las toohello aplicativos de cliente que precisam acessar tooyour entidades. Porque ainda há uma sobrecarga envolvida na geração e entrega tooclients de tokens SAS, você deve considerar a melhor maneira de tooreduce essa sobrecarga, especialmente em cenários de alto volume.  

É possível toogenerate um token SAS que concede acesso tooa subconjunto de entidades de saudação em uma tabela. Por padrão, você cria um token SAS para uma tabela inteira, mas também é possível toospecify tooeither de acesso de token grant que Olá SAS uma variedade de **PartitionKey** valores ou um intervalo de **PartitionKey** e  **RowKey** valores. Você pode escolher toogenerate tokens SAS para usuários individuais do sistema, de modo que o token SAS de cada usuário só permite a eles acesso tootheir próprias entidades Olá serviço de tabela.  

### <a name="asynchronous-and-parallel-operations"></a>Operações paralelas e assíncronas
Desde que você esteja distribuindo suas solicitações por várias partições, pode melhorar a capacidade de resposta do cliente e a taxa de transferência usando consultas assíncronas ou paralelas.
Por exemplo, você pode ter duas ou mais instâncias de função de trabalho acessando suas tabelas em paralelo. Você pode ter funções de trabalho individuais responsáveis por determinados conjuntos de partições, ou simplesmente ter várias instâncias de função de trabalho, cada tooaccess capaz de todos os Olá partições em uma tabela.  

Dentro de uma instância do cliente, você pode melhorar o desempenho executando operações de armazenamento de forma assíncrona. Olá biblioteca de cliente de armazenamento torna modificações e consultas assíncronas toowrite fácil. Por exemplo, você pode iniciar com o método síncrono de saudação que recupera todas as entidades de saudação em uma partição, conforme mostrado no hello código c# a seguir:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Você pode modificar este código facilmente para que essa consulta Olá executa de modo assíncrono da seguinte maneira:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

Neste exemplo assíncrona, você pode ver o seguinte Olá muda de versão síncrona hello:  

* a assinatura do método Hello agora inclui Olá **async** modificador e retorna um **tarefa** instância.  
* Em vez de chamar hello **ExecuteSegmented** resultados do método tooretrieve, Olá método agora chamadas Olá **ExecuteSegmentedAsync** Olá método e usa **await** modificador tooretrieve resultados de forma assíncrona.  

aplicativo de cliente Hello pode chamar esse método várias vezes (com valores diferentes para Olá **departamento** parâmetro), e cada consulta será executada em um thread separado.  

Observe que não há nenhuma versão assíncrona do hello **Execute** método hello **TableQuery** classe porque Olá **IEnumerable** interface não dá suporte assíncrono enumeração.  

Você também pode inserir, atualizar e excluir entidades de forma assíncrona. Olá c# de exemplo a seguir mostra um método simples e síncrona tooinsert ou substituir uma entidade funcionário:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Facilmente, você pode modificar este código para que a atualização de saudação executa de modo assíncrono da seguinte maneira:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Neste exemplo assíncrona, você pode ver o seguinte Olá muda de versão síncrona hello:  

* a assinatura do método Hello agora inclui Olá **async** modificador e retorna um **tarefa** instância.  
* Em vez de chamar hello **Execute** entidade do método tooupdate hello, Olá método agora chamadas Olá **ExecuteAsync** Olá método e usa **await** tooretrieve de modificador resultados de forma assíncrona.  

aplicativo de cliente Hello pode chamar vários métodos assíncronos como esse, e cada invocação do método será executado em um thread separado.  

### <a name="credits"></a>Credits
Gostaríamos Olá toothank membros da equipe do Azure para suas contribuições de saudação a seguir: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah e Serdar Ozler, bem como Tom Hollander da Microsoft DX. 

Também gostaríamos toothank saudação MVP da Microsoft a seguir para seus valiosos comentários durante ciclos de revisão: Igor Papirov e Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

