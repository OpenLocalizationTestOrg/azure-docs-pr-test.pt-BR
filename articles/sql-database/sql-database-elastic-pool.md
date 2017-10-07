---
title: "aaaWhat tem pools Elásticos? Gerenciar vários Bancos de Dados SQL – Azure | Microsoft Docs"
description: "Gerenciar e dimensionar vários Bancos de Dados SQL – centenas de milhares – usando pools elásticos. Um preço para os recursos que você pode distribuir quando necessário."
keywords: "vários bancos de dados, recursos de banco de dados, desempenho de banco de dados"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Pools elásticos ajudam você a gerenciar e dimensionar vários Bancos de Dados SQL

Pools elásticos do Banco de Dados SQL são uma solução simples e econômica para gerenciar e dimensionar a vários bancos de dados com demandas de uso variadas e imprevisíveis. bancos de dados de saudação em um pool Elástico estão em um único servidor de banco de dados SQL e compartilhar um número definido de recursos ([unidades de transação de banco de dados Elástico](sql-database-what-is-a-dtu.md) (eDTUs)) a um preço de conjunto. Pools Elásticos no banco de dados do SQL Azure habilitam o SaaS desenvolvedores toooptimize Olá preço desempenho para um grupo de bancos de dados em um orçamento prescrito oferecendo elasticidade de desempenho para cada banco de dados.   

> [!NOTE]
> Os pools elásticos têm uma disponibilidade geral (DG) em todas as regiões do Azure, exceto na Índia Ocidental, onde atualmente estão no modo de visualização.  A GA dos pools elásticos nessa região ocorrerá assim que possível.
>

## <a name="what-are-sql-elastic-pools"></a>O que são pools elásticos SQL? 

Desenvolvedores de SaaS compilam aplicativos com base em camadas de dados de grande escala compostas por vários bancos de dados. Um padrão de aplicativo comum é tooprovision um único banco de dados para cada cliente. Mas diferentes clientes frequentemente têm padrões de uso de variáveis e imprevisíveis, e é difícil toopredict requisitos de recursos de saudação de cada usuário de banco de dados individuais. Tradicionalmente, você tinha duas opções: 

- Provisionar excessivamente os recursos com base no uso de pico e pagamento, ou
- Provisionar insuficiente toosave de custo, a despesa de saudação de desempenho e satisfação do cliente durante picos. 

Pools Elásticos resolver esse problema, garantindo que bancos de dados obtém recursos de desempenho de saudação que precisam, quando necessário. Eles fornecem um mecanismo de alocação de recursos simples dentro de um orçamento previsível. toolearn mais informações sobre padrões de design para aplicativos SaaS usando pools Elásticos, consulte [padrões de Design para aplicativos de SaaS multilocatário com o Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Pools Elásticos habilitar Olá desenvolvedor toopurchase [unidades de transação de banco de dados Elástico](sql-database-what-is-a-dtu.md) (eDTUs) para um pool compartilhado por vários bancos de dados tooaccommodate imprevisível períodos de uso de bancos de dados individuais. requisito de eDTU Olá para um pool é determinado pela utilização de agregação Olá seus bancos de dados. número de Olá de eDTUs toohello disponível pool é controlado pela alocação de desenvolvedor hello. desenvolvedor Olá simplesmente adiciona pool toohello de bancos de dados, define Olá mínimo e o máximo eDTUs para bancos de dados de saudação e, em seguida, define Olá eDTU do pool de saudação com base no seu orçamento de. Um desenvolvedor pode usar pools tooseamlessly aumentar seus serviços de empresas maduras tooa inicialização lean em escala crescente.

Em pool hello, bancos de dados individuais recebem Olá flexibilidade tooauto escala no conjunto de parâmetros. Sob carga pesada, um banco de dados pode consumir mais demanda de toomeet eDTUs. Bancos de dados sob cargas leves consumem menos e bancos de dados sem carga não consomem nenhum eDTU. O provisionamento de recursos para o pool inteiro Olá em vez de bancos de dados único simplifica as tarefas de gerenciamento. Além disso, você tem uma alocação previsível para o pool de saudação. EDTUs adicionais podem ser adicionados tooan pool existente sem tempo de inatividade do banco de dados, exceto que os bancos de dados Olá talvez seja necessário toobe movido tooprovide Olá adicional recursos para a nova reserva de eDTU Olá de computação. Da mesma forma, se eDTUs extras não forem mais necessários, eles poderão ser removidos de um pool existente a qualquer momento. E você pode adicionar ou subtrair o pool de toohello de bancos de dados. Se um banco de dados é previsível por estar subutilizando recursos, mova-o.

Você pode criar e gerenciar um pool Elástico usando Olá [portal do Azure](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [c#](sql-database-elastic-pool-manage-csharp.md), e Olá API REST. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>Quando um pool elástico do Banco de Dados SQL deve ser considerado?

Pools também são indicados para um grande número de bancos de dados com padrões de utilização específicos. Para um determinado banco de dados, esse padrão é caracterizado por baixa utilização média com picos de utilização relativamente pouco frequentes.

Hello mais bancos de dados você pode adicionar tooa Olá de pool maior que tornam-se a economia. Dependendo de seu padrão de utilização do aplicativo, é possível toosee economia com um mínimo de dois bancos de dados S3.  

a seguir Olá seções ajudam você a compreender como tooassess se seu conjunto específico de bancos de dados pode se beneficiar em um pool. Olá, exemplos usam pools padrão mas hello mesmos princípios também se aplicam tooBasic e pools de Premium.

### <a name="assessing-database-utilization-patterns"></a>Avaliar os padrões de utilização do banco de dados

Olá figura a seguir mostra um exemplo de um banco de dados gasta tempo ocioso, mas também periodicamente picos de atividade. Este é um padrão de utilização adequado para um pool:

   ![um banco de dados individual adequado para um pool](./media/sql-database-elastic-pool/one-database.png)

Para Olá ilustrado o período de cinco minutos, picos DB1 backup too90 DTUs, mas seu uso geral médio é menos do que cinco DTUs. Um S3 nível de desempenho é necessário toorun essa carga de trabalho em um único banco de dados, mas isso deixa a maioria dos recursos de saudação não utilizados durante períodos de pouca atividade.

Um pool de permite que esses toobe DTUs não utilizados compartilhados entre vários bancos de dados e então reduz o custo de necessários e geral de DTUs de saudação.

Aproveitando o exemplo anterior hello, suponha que há bancos de dados adicionais com os padrões de uso semelhantes como DB1. Em Olá próximas duas figuras abaixo, Olá utilização de quatro bancos de dados e 20 bancos de dados são colocadas em camadas para Olá mesmo gráfico natureza de não-sobreposição Olá tooillustrate de sua utilização ao longo do tempo:

   ![quatro bancos de dados com um padrão de utilização adequado para um pool](./media/sql-database-elastic-pool/four-databases.png)

  ![vinte bancos de dados com um padrão de utilização adequado para um pool](./media/sql-database-elastic-pool/twenty-databases.png)

utilização de DTU agregação Olá em todos os bancos de dados de 20 é ilustrada pela linha de saudação preto no hello anterior figura. Isso mostra utilização de DTU agregação Olá nunca excede 100 DTUs e indica que 20 bancos de dados de saudação podem compartilhar 100 eDTUs durante esse período de tempo. Isso resulta em uma redução de 20 x em DTUs e um 13 x preço redução em comparação comparada tooplacing cada de bancos de dados Olá S3 níveis de desempenho para bancos de dados único.

Este exemplo é ideal para Olá motivos a seguir:

* Há grandes diferenças entre o pico de utilização e a utilização média por banco de dados.  
* utilização de saudação de pico para cada banco de dados ocorre em diferentes pontos no tempo.
* eDTUs são compartilhados entre vários bancos de dados.

preço de saudação de um pool é uma função do hello eDTUs de pool. Enquanto Olá eDTU preço unitário um pool é 1,5 x maior Olá DTU preço unitário um único banco de dados, **eDTUs de pool pode ser compartilhado por muitos bancos de dados e eDTUs total menos são necessárias**. Essas diferenças no compartilhamento de eDTU e preços são a base de saudação de potencial de economia do preço Olá pools podem fornecer.  

Olá seguintes regras gerais relacionadas toodatabase banco de dados e a contagem de utilização ajuda tooensure que oferece um pool reduzido custo comparado toousing níveis de desempenho para bancos de dados único.

### <a name="minimum-number-of-databases"></a>Número mínimo de bancos de dados

Se a soma Olá Olá DTUs dos níveis de desempenho para bancos de dados único é mais de 1,5 x eDTUs Olá necessários para o pool de saudação, um pool Elástico é mais econômico. Para ver os tamanhos disponíveis, consulte [Limites de eDTU e armazenamento para pools e bancos de dados elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

***Exemplo***<br>
Pelo menos dois bancos de dados S3 ou pelo menos 15 bancos de dados S0 são necessários para um toobe do pool de 100 eDTU mais econômicos do que usar níveis de desempenho para bancos de dados único.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Número máximo de banco de dados em pico simultaneamente

Compartilhando eDTUs, nem todos os bancos de dados em um pool podem usar simultaneamente eDTUs de limite de toohello disponível ao usar os níveis de desempenho para bancos de dados único. Olá menos bancos de dados simultaneamente de pico, inferior eDTU de pool Olá Olá pode ser definida e Olá que torna-se mais pool de saudação econômico. Em geral, não mais do que 2/3 (ou 67%) de bancos de dados Olá pool Olá simultaneamente devem falar tootheir eDTU limitam.

***Exemplo***<br>
custos de tooreduce para três bancos de dados S3 em um pool de eDTU 200, no máximo dois desses bancos de dados podem aumentar simultaneamente em sua utilização. Caso contrário, se mais de dois desses quatro bancos de dados S3 simultaneamente de pico, pool Olá teria toomore toobe em tamanho de 200 eDTUs. Se o pool de saudação é redimensionado toomore que 200 eDTUs, mais bancos de dados S3 necessário toobe adicionado custos tookeep de pool de toohello menor do que os níveis de desempenho para bancos de dados único.

Observe que este exemplo não considera a utilização de outros bancos de dados no pool de saudação. Se todos os bancos de dados têm algum utilização em qualquer ponto no tempo, em seguida, menor que 2/3 (ou 67%) de bancos de dados Olá podem pico simultaneamente.

### <a name="dtu-utilization-per-database"></a>Utilização de DTU por banco de dados
Uma grande diferença entre o horário de pico hello e utilização média de um banco de dados indica longos períodos de baixa utilização e curtos períodos de alta utilização. Esse padrão de utilização é ideal para compartilhar recursos entre bancos de dados. Um banco de dados deve ser considerado para um pool quando seu pico de utilização for aproximadamente 1,5 vez maior que sua utilização média.

***Exemplo***<br>
Um banco de dados S3 picos de DTUs too100 e usa em média 67 DTUs ou menor é um bom candidato para o compartilhamento de eDTUs em um pool. Como alternativa, um S1 banco de dados que picos de DTUs too20 e usa em Média 13 DTUs ou menor é um bom candidato para um pool.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Como escolher o tamanho do pool correto Olá?

melhor o tamanho de um pool de saudação depende Olá eDTUs de agregação e recursos de armazenamento necessários para todos os bancos de dados no pool de saudação. Isso inclui determinar Olá maior seguinte hello:

* DTUs máxima utilizadas por todos os bancos de dados no pool de saudação.
* Bytes de armazenamento máximo utilizadas por todos os bancos de dados no pool de saudação.

Para ver os tamanhos disponíveis, consulte [Limites de eDTU e armazenamento para pools e bancos de dados elásticos](#what-are-the-resource-limits-for-elastic-pools).

Banco de dados SQL avalia Olá históricos de uso dos bancos de dados em um servidor de banco de dados SQL e recomenda Olá configuração de pool apropriado no portal do Azure de saudação automaticamente. Recomendações de toohello de adição, uma experiência interna calcula uso de eDTU Olá para um grupo personalizado de bancos de dados no servidor de saudação. Isso permite que você toodo um "" hipóteses interativamente adicionando pool toohello de bancos de dados e removê-los a análise de uso do recurso de tooget e dimensionamento aviso antes de confirmar as alterações. Para obter instruções, confira [Monitorar, gerenciar e dimensionar um pool elástico](sql-database-elastic-pool-manage-portal.md).

Em casos onde você não pode usar as ferramentas, passo a passo a seguir Olá pode ajudar a estimar se um pool é mais econômico que bancos de dados único:

1. Estimar Olá eDTUs necessários para o pool de saudação da seguinte maneira:

   MAX (<*Número total de bancos de dados* X *utilização média de DTU por banco de dados*>,<br>
   <*Número de bancos de dados em pico simultaneamente* X *Utilização de DTU em pico por banco de dados*)
2. Estimar o espaço de armazenamento de Olá necessário para o pool de saudação adicionando Olá número de bytes necessários para todos os bancos de dados de saudação no pool de saudação. Em seguida, determine o tamanho do pool de eDTU Olá que fornece essa quantidade de armazenamento. Para ver os limites de armazenamento em pool baseados no tamanho do pool em eDTUs, confira [eDTU and storage limits for elastic pools and elastic databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)(Limites de armazenamento e eDTU para pools elásticos e bancos de dados elásticos).
3. Levar Olá maior das estimativas de eDTU Olá da etapa 1 e 2.
4. Consulte Olá [página de preços do banco de dados do SQL](https://azure.microsoft.com/pricing/details/sql-database/) e localizar pool de eDTU Olá menor tamanho que é maior que a estimativa de saudação da etapa 3.
5. Compare o preço do pool de saudação da etapa 5 toohello preço de usar níveis de desempenho apropriadas de saudação do bancos de dados único.

### <a name="changing-elastic-pool-resources"></a>Alterando os recursos do pool elástico

Você pode aumentar ou diminuir Olá recursos disponíveis tooan pool Elástico com base nas necessidades de recursos.

* Alterar Olá min eDTUs por banco de dados ou o máximo de eDTUs por banco de dados normalmente é concluído em 5 minutos ou menos.
* Alterar eDTUs Olá por pool de depende da quantidade total de saudação do espaço usado por todos os bancos de dados no pool de saudação. As alterações levam, em média, 90 minutos ou menos a cada 100 GB. Por exemplo, se o espaço total Olá usado por todos os bancos de dados no pool de saudação é de 200 GB, Olá esperada de latência para mudar o eDTU do pool de saudação por pool é de 3 horas ou menos.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>Quais são os limites de recurso Olá para pools Elásticos?

Olá tabelas a seguir descreve os limites de recurso de saudação de pools elásticos.  Observe que os limites de recurso de saudação de bancos de dados individuais em pools Elásticos geralmente são Olá igual de bancos de dados único fora pools com base em DTUs e camada de serviço de saudação.  Por exemplo, trabalhadores de simultâneas máx Olá para um banco de dados S2 é 120 trabalhadores.  Portanto, trabalhadores de simultâneas máx Olá para um banco de dados em um pool padrão também é 120 trabalhadores se DTU máx por banco de dados no pool de Olá Olá é 50 DTUs (que é o equivalente tooS2).

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Se todas as DTUs de um pool Elástico forem usadas, cada banco de dados no pool de saudação recebe uma quantidade equivalente de consultas de tooprocess de recursos.  Olá serviço de banco de dados SQL fornece integridade entre bancos de dados, garantindo iguais fatias de tempo de computação de compartilhamento de recursos. Integridade de compartilhamento de recursos de pool Elástico Além disso é tooany quantidade de recursos, caso contrário, a garantia de tooeach banco de dados quando Olá mínimo de DTU por banco de dados estiver definido como valor do tooa diferente de zero.

### <a name="database-properties-for-pooled-databases"></a>Propriedades do banco de dados para bancos de dados em pool

Olá, a tabela a seguir descreve as propriedades de saudação para bancos de dados em pool.

| Propriedade | Descrição |
|:--- |:--- |
| Máximo de eDTUs por banco de dados |número máximo de saudação de eDTUs que qualquer banco de dados no pool de saudação pode usar, se disponível com base no uso por outros bancos de dados no pool de saudação.  O máximo de eDTUs por banco de dados não é uma garantia de recursos para um banco de dados.  Essa é uma configuração global que se aplica a bancos de dados tooall no pool de saudação. Defina eDTUs máximo por banco de dados picos toohandle alta o suficiente na utilização do banco de dados. Um certo grau de excesso é esperado porque o pool Olá geralmente supõe padrões de uso quentes e frios para bancos de dados em que todos os bancos de dados não são simultaneamente peaking. Por exemplo, suponha que a utilização de pico Olá por banco de dados é 20 eDTUs e somente 20% de bancos de dados Olá 100 no pool de saudação são pico em Olá simultaneamente.  Se Olá eDTU máximo por banco de dados é definido too20 eDTUs, é razoável tooovercommit pool de saudação 5 vezes e eDTUs de saudação do conjunto por pool too400. |
| Mínimo de eDTUs por banco de dados |número mínimo de saudação de eDTUs que tem a garantia de qualquer banco de dados no pool de saudação.  Essa é uma configuração global que se aplica a bancos de dados tooall no pool de saudação. Olá min eDTU por banco de dados pode ser definido como too0 e também é o valor padrão de saudação. Essa propriedade é definida tooanywhere entre 0 e hello utilização média de eDTU por banco de dados. produto de saudação do número de saudação de bancos de dados no pool de saudação e Olá min eDTUs por banco de dados não pode exceder eDTUs Olá por pool.  Por exemplo, se um pool tiver 20 bancos de dados e Olá min de eDTU por banco de dados definido too10 eDTUs, em seguida, Olá eDTUs por pool de deve ser pelo menos tão grande quanto o eDTUs de 200. |
| Armazenamento máximo de dados por banco de dados |Olá máximo de armazenamento para um banco de dados em um pool. Pool de bancos de dados compartilham o pool de armazenamento, para que armazenamento de banco de dados é limitado toohello menor de pool de armazenamento restantes e armazenamento máximo por banco de dados. Armazenamento máximo por banco de dados refere-se o tamanho máximo de toohello Olá dos arquivos de dados e não inclui o hello espaço usado pelos arquivos de log. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Usando outros recursos de Banco de Dados SQL com pools elásticos

### <a name="elastic-jobs-and-elastic-pools"></a>Trabalhos e pools elásticos

Com um pool, as tarefas de gerenciamento são simplificadas com a execução de scripts em **[trabalhos elásticos](sql-database-elastic-jobs-overview.md)**. Um trabalho elástico elimina a maioria do tédio associado a um grande número de bancos de dados. toobegin, consulte [guia de Introdução com trabalhos Elásticos](sql-database-elastic-jobs-getting-started.md).

Para saber mais sobre outras ferramentas de banco de dados para trabalhar com vários bancos de dados, veja [Expansão com o Banco de Dados SQL](sql-database-elastic-scale-introduction.md).

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Opções de continuidade dos negócios para bancos de dados em um pool elástico
Pool de bancos de dados geralmente suporte Olá mesmo [recursos de continuidade de negócios](sql-database-business-continuity.md) que estão disponíveis toosingle bancos de dados.

- **Restauração pontual**: ponto no tempo de restauração usa backups de banco de dados automática toorecover um banco de dados em um ponto específico do pool tooa no tempo. Confira [Restauração pontual](sql-database-recovery-using-backups.md#point-in-time-restore)

- **A restauração geográfica**: a restauração geográfica fornece a opção de recuperação padrão hello quando um banco de dados não está disponível devido a um incidente na região Olá onde o banco de dados de saudação está hospedado. Consulte [restaurar um banco de dados do SQL Azure ou failover tooa secundário](sql-database-disaster-recovery.md)

- **Replicação geográfica ativa**: para aplicativos que têm requisitos de recuperação mais agressivos do que a restauração geográfica pode oferecer, configure a [replicação geográfica ativa](sql-database-geo-replication-overview.md).

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Gerenciar pools Elásticos do banco de dados SQL usando Olá portal do Azure

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Criar um novo pool Elástico do banco de dados SQL usando Olá portal do Azure

Há duas maneiras que você pode criar um pool Elástico em Olá portal do Azure. Você pode fazer isso do zero, se você souber que a instalação Olá pool desejado ou começar com uma recomendação do serviço de saudação. Banco de dados SQL tem inteligência interna que recomenda uma configuração de pool Elástico se mais eficiente com base no hello após telemetria de uso de seus bancos de dados. 

Criando um pool Elástico de uma já existente **server** folha no portal de saudação é hello mais fácil maneira toomove bancos de dados existentes em um pool Elástico. Você também pode criar um pool Elástico pesquisando **pool Elástico do SQL** em Olá **Marketplace** ou clicando em **+ adicionar** em Olá **pools Elásticos de SQL**procurar folha. Você é capaz de toospecify um servidor novo ou existente por este fluxo de trabalho de provisionamento do pool.

> [!NOTE]
> Você pode criar vários pools em um servidor, mas você não pode adicionar bancos de dados de diferentes servidores em Olá mesmo pool.
>  

Olá de preço do pool determina Olá recursos elastics toohello disponível no pool de saudação e Olá o número máximo de eDTUs (eDTU máximo) e o banco de dados do armazenamento (GBs) tooeach disponíveis. Para obter detalhes, consulte [Camadas de serviço](#edtu-and-storage-limits-for-elastic-pools).

toochange Olá preço para o pool de saudação, clique em **preço**, clique em Olá preço você deseja e, em seguida, clique em **selecione**.

> [!IMPORTANT]
> Depois que você escolha Olá preço e confirmar suas alterações, clicando em **Okey** na última etapa de hello, não será Olá toochange capaz de preço do pool de saudação. toochange Olá camada de preços para um pool Elástico existente, criar um pool Elástico em Olá desejado de preço e migre Olá bancos de dados toothis novo pool.
>

Se os bancos de dados Olá estiver trabalhando com tem telemetria suficiente histórico de uso, Olá **estimado de eDTU e GB uso** gráfico e hello **real eDTU uso** toohelp de atualização de gráfico de barras que facilitam a configuração decisões. Além disso, o serviço de saudação pode oferecer um toohelp de mensagem de recomendação você direita tamanho Olá pool.

Olá serviço de banco de dados SQL avalia o histórico de uso e recomenda um ou mais pools quando ele é mais econômico que bancos de dados único. Cada recomendação é configurada com um subconjunto de bancos de dados do servidor de saudação que melhor se adaptar pool Olá exclusivo.

![pool recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

recomendação de pool de saudação inclui:

- A camada de preços para o pool de saudação (Basic, Standard, Premium ou Premium RS)
- Os **eDTUs do POOL** apropriados (também chamados de Máx. de eDTUs por pool)
- Olá **eDTU máximo** e **Mín** por banco de dados
- lista de saudação de bancos de dados recomendados para o pool de saudação

> [!IMPORTANT]
> serviço de saudação considera Olá últimos 30 dias de telemetria ao recomendar pools. Para ver um banco de dados do toobe considerado como candidata para um pool Elástico, ele deve existir pelo menos 7 dias. Os bancos de dados que já estão em um pool elástico não são considerados candidatos para as recomendações de pool elástico.
>

serviço de saudação avalia as necessidades de recursos e eficácia dos custos de movimentação Olá único bancos de dados em cada camada de serviço em pools de saudação mesmo nível. Por exemplo, todos os bancos de dados padrão em um servidor são avaliados para sua adaptação em um pool elástico Standard. Isso significa que o serviço Olá não faz recomendações entre camadas como mover um banco de dados padrão em um pool de Premium.

Depois de adicionar o pool de toohello de bancos de dados, as recomendações são geradas dinamicamente com base no histórico de uso de bancos de dados de saudação que você selecionou hello. Essas recomendações são mostradas em Olá eDTU e GB gráfico de uso em uma faixa de recomendação na parte superior de saudação do hello **configurar pool** folha. Essas recomendações são pretendido tooassist você na criação de um pool Elástico otimizado para seus bancos de dados específicos.

![Recomendações dinâmicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>Gerenciamento e monitoração um pool elástico

Em Olá portal do Azure, você pode monitorar a utilização de saudação de um pool Elástico e bancos de dados hello dentro desse pool. Você também pode fazer um conjunto de alterações de pool Elástico tooyour e enviar todas as alterações no hello mesmo tempo. Essas alterações incluem adicionar ou remover bancos de dados, alterar as configurações de pool elástico ou alterar suas configurações de banco de dados.

Olá gráfico a seguir mostra um pool Elástico de exemplo. exibição de saudação inclui:

*  Gráficos de monitoramento de uso do recurso de pool Elástico hello e bancos de dados de saudação contidos no pool de saudação.
*  Olá **configurar** pool botão toomake pool Elástico toohello é alterado.
*  Olá **criar banco de dados** botão que cria um banco de dados e adiciona-o pool Elástico atual de toohello.
*  Trabalhos elásticos que ajudam a gerenciar muitos bancos de dados executando scripts Transact SQL em todos os bancos de dados em uma lista.

![Exibição de pool](./media/sql-database-elastic-pool-manage-portal/basic.png)

Você pode ir tooa determinado pool toosee sua utilização de recursos. Por padrão, o pool de saudação é configurado tooshow armazenamento e eDTU o uso de saudação última hora. gráfico de saudação pode ser configurado tooshow diferentes métricas em várias janelas de tempo. Clique em Olá **utilização de recursos** do gráfico em **monitoramento de pool Elástico** tooshow uma exibição detalhada de saudação especificados métricas em janela de tempo especificada de saudação.

![Monitoramento de pool elástico](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Lâmina Métrica](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>exibição de gráfico de saudação toocustomize

Você pode editar gráfico hello e Olá folha de métricas toodisplay outras métricas como porcentagem da CPU, porcentagem de e/s de dados e porcentagem de e/s de log usado.

![Clique em editar](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

Em Olá **Editar gráfico** formulário, você pode selecionar um intervalo de tempo (última hora, atualmente, ou última semana), ou clique em **personalizado** tooselect qualquer data vão Olá duas últimas semanas. Você pode escolher entre uma barra ou um gráfico de linhas e selecione Olá toomonitor de recursos.

> [!Note]
> Somente o gráfico de métricas com hello mesma unidade de medida pode ser exibida em hello em Olá mesmo tempo. Por exemplo, se você selecionar "percentual de eDTU", em seguida, você pode apenas selecionar outras métricas com porcentagem como a unidade de medida de saudação.
>

[Clique em Editar](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gerenciamento e monitoração de bancos de dados um pool elástico

Bancos de dados individuais também podem ser monitorados para identificar potenciais problemas. Em **Monitoramento de Banco de Dados Elástico**, há um gráfico que exibe as métricas para cinco bancos de dados. Por padrão, Olá gráfico exibe Olá top 5 bancos de dados no pool de saudação pelo uso de eDTU médio em Olá última hora. 

![Monitoramento de pool elástico](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Clique em Olá **uso de eDTU para bancos de dados para a última hora de saudação** em **monitoramento de banco de dados Elástico**. Isso abre **utilização de recursos de banco de dados** e fornece uma exibição detalhada de uso do banco de dados de saudação no pool de saudação. Usando a grade de saudação na parte inferior de saudação da folha Olá, você pode selecionar qualquer banco de dados em Olá pool toodisplay seu uso no gráfico de saudação (backup de bancos de dados too5). Você também pode personalizar a janela de métricas e a hora de saudação exibida no gráfico de saudação clicando **Editar gráfico**.

![Folha Utilização de Recursos do Banco de Dados](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>exibição de saudação toocustomize

Você pode editar Olá gráfico tooselect um intervalo de tempo (última hora ou nas últimas 24 horas), ou clique em **personalizado** tooselect dia diferente no hello após toodisplay de 2 semanas.

![Clique em Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Clique em Personalizar](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

Você também pode clicar em Olá **comparar bancos de dados por** suspensa tooselect um toouse de métrica diferente ao comparar os bancos de dados.

![Editar gráfico Olá](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor de bancos de dados

Na lista de banco de dados de saudação do hello **utilização de recursos de banco de dados** folha, você pode encontrar bancos de dados procurando por meio de páginas de saudação na lista de saudação ou digitando o nome de saudação do banco de dados. Use banco de dados da saudação tooselect Olá caixa de seleção.

![Pesquise toomonitor de bancos de dados](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Adicionar um recurso de pool Elástico tooan alerta

Você pode adicionar regras tooan pool Elástico que enviar email de alerta ou toopeople pontos de extremidade de tooURL de cadeias de caracteres quando o pool Elástico Olá atinge um limite de utilização que você configurou.

**tooadd um recurso de alerta tooany:**

1. Clique em Olá **utilização de recursos** saudação do gráfico tooopen **métrica** folha, clique em **adicionar alerta**e, em seguida, preencha as informações Olá Olá **adicionar um alerta regra** folha (**recurso** configurar automaticamente ao pool de saudação toobe você está trabalhando com).
2. Digite um **nome** e **descrição** que identifica Olá tooyou de alerta e destinatários de saudação.
3. Escolha um **métrica** que você deseja tooalert da lista de saudação.

    gráfico de Olá dinamicamente mostra a utilização de recursos para essa métrica toohelp que você escolher um limite.

4. Escolha uma **Condição** (maior que, menor que, etc.) e um **Limite**.
5. Escolha um **período** de tempo que Olá métrica regra deve ser atendida antes de gatilhos de alerta de saudação.
6. Clique em **OK**.

Para obter mais informações, consulte [Criar alertas do Banco de Dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).

### <a name="move-a-database-into-an-elastic-pool"></a>Mover um banco de dados para um pool elástico

Você pode adicionar ou remover bancos de dados de um pool existente. bancos de dados Olá podem estar em outros pools. No entanto, você só pode adicionar bancos de dados que estão em Olá mesmo servidor lógico.

 ![Clique em Configurar pool](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Clique em Adicionar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Selecione tooadd de bancos de dados](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![Adições de pool pendentes](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Clique em Salvar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Remover um banco de dados de um pool elástico

![lista de bancos de dados](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![lista de bancos de dados](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![visualização de adição ou remoção de banco de dados](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Clique em Salvar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Alterar as configurações de desempenho de um pool elástico

Como monitorar a utilização de recursos de saudação de um pool Elástico, você pode descobrir que alguns ajustes são necessários. Talvez pool Olá precisa de uma alteração nos limites de armazenamento ou desempenho hello. Possivelmente, você deseja toochange configurações de banco de dados de saudação no pool de saudação. Você pode alterar a instalação de saudação do pool de saudação em qualquer tempo tooget Olá melhor equilíbrio entre desempenho e custo. Veja [Quando um pool elástico deve ser usado?](sql-database-elastic-pool.md) para saber mais.

toochange Olá eDTUs armazenamento limites ou por pool e eDTUs por banco de dados:

![Utilização de recursos de pool elástico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Atualização de um pool elástico e o novo custo mensal](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>Gerenciar pools elásticos do Banco de Dados SQL usando o PowerShell

toocreate e gerenciar pools Elásticos do banco de dados SQL com o Azure PowerShell, use Olá cmdlets do PowerShell a seguir. Se você precisa tooinstall ou atualize o PowerShell, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps). toocreate e gerenciar bancos de dados, servidores e regras de firewall, consulte [criar e gerenciar servidores de banco de dados SQL e bancos de dados usando o PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> Para scripts de exemplo do PowerShell, consulte [criar pools Elásticos e mover bancos de dados entre pools e fora de um pool usando o PowerShell](scripts/sql-database-move-database-between-pools-powershell.md) e [toomonitor de usar o PowerShell e a escala elástica um SQL pool no banco de dados do Azure SQL](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | Descrição |
| --- | --- |
|[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Cria um pool de banco de dados elástico em um SQL Server lógico.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Obtém pools elásticos e seus valores de propriedade em um SQL Server lógico.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Modifica as propriedades de um pool de banco de dados elástico em um SQL Server lógico.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Exclui um pool de banco de dados elástico de um SQL Server lógico.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Obtém o status de saudação de operações em um pool Elástico em um servidor SQL lógico.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Cria um novo banco de dados em um pool existente ou como um Banco de Dados Individual. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtém um ou mais bancos de dados.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Define as propriedades para um banco de dados ou move um banco de dados existente para um pool elástico, para fora dele ou entre pools elásticos.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Remove um banco de dados.|

> [!TIP]
> Criação de muitos bancos de dados em um pool Elástico pode levar tempo quando feito usando o portal de saudação ou cmdlets do PowerShell que criar apenas um único banco de dados de cada vez. criação de tooautomate em um pool Elástico, consulte [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Gerenciar pools Elásticos do banco de dados SQL usando Olá CLI do Azure

toocreate e gerenciar pools Elásticos do banco de dados SQL com hello [CLI do Azure](/cli/azure/overview), use os seguintes Olá [banco de dados do SQL Azure CLI](/cli/azure/sql/db) comandos. Saudação de uso [nuvem Shell](/azure/cloud-shell/overview) toorun Olá CLI em seu navegador, ou [instalar](/cli/azure/install-azure-cli) -la no Windows, Linux ou macOS. 

> [!TIP]
> Para scripts de exemplo da CLI do Azure, consulte [toomove CLI Use um banco de dados do SQL Azure em um pool Elástico SQL](scripts/sql-database-move-database-between-pools-cli.md) e [tooscale CLI do Azure Use um pool Elástico do SQL no banco de dados do SQL Azure](scripts/sql-database-scale-pool-cli.md).
>

| Cmdlet | Descrição |
| --- | --- |
|[az sql elastic-pool create](/cli/azure/sql/elastic-pool#create)|Cria um pool elástico.|
|[az sql elastic-pool list](/cli/azure/sql/elastic-pool#list)|Retorna uma lista de pools elásticos em um servidor.|
|[az sql elastic-pool list-dbs](/cli/azure/sql/elastic-pool#list-dbs)|Retorna uma lista de bancos de dados em um pool elástico.|
|[az sql elastic-pool list-editions](/cli/azure/sql/elastic-pool#list-editions)|Também inclui as configurações DTU do pool disponível, limites de armazenamento e configurações por banco de dados. Em detalhes de tooreduce de ordem, limites de armazenamento adicional e por banco de dados configurações ficam ocultos por padrão.|
|[az sql elastic-pool update](/cli/azure/sql/elastic-pool#update)|Atualiza um pool elástico.|
|[az sql elastic-pool delete](/cli/azure/sql/elastic-pool#delete)|Exclui um pool Elástico hello.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Gerenciar pools elásticos de Banco de Dados SQL usando Transact-SQL

toocreate e mover bancos de dados dentro de pools Elásticos existentes ou tooreturn informações sobre um pool Elástico de banco de dados SQL com o Transact-SQL, use Olá comandos T-SQL a seguir. Você pode executar esses comandos usando Olá portal do Azure, [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [código do Visual Studio](https://code.visualstudio.com/docs), ou qualquer outro programa que pode conectar-se o servidor de banco de dados do Azure SQL tooan e passar o Transact-SQL comandos. toocreate e gerenciar bancos de dados, servidores e regras de firewall, consulte [criar e gerenciar servidores de banco de dados SQL e bancos de dados usando o Transact-SQL](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> Não é possível criar, atualizar ou excluir um pool elástico de Banco de Dados SQL do Microsoft Azure usando o Transact-SQL. Você pode adicionar ou remover bancos de dados de um pool Elástico, e você pode usar DMVs tooreturn informações sobre pools Elásticos existentes.
>

| Command | Descrição |
| --- | --- |
|[CREATE DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Cria um novo banco de dados em um pool existente ou como um Banco de Dados Individual. Você deve ser conectado toohello banco de dados mestre toocreate um novo banco de dados.|
| [ALTER DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Move um banco de dados para dentro de um pool elástico, para fora dele ou entre pools elásticos.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Exclui um banco de dados.|
|[sys.elastic_pool_resource_stats (Banco de Dados SQL do Microsoft Azure)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Retorna estatísticas de uso de recursos para todos os pools de banco de dados Elástico Olá em um servidor lógico. Para cada pool de banco de dados elástico, há uma linha para cada janela de relatórios de 15 segundos (quatro linhas por minuto). Isso inclui a utilização da CPU, e/s, Log, o consumo de armazenamento e simultâneas/sessão de solicitação por todos os bancos de dados no pool de saudação.|
|[sys.database_service_objectives (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retorna Olá edition (camada de serviço), o objetivo de serviço (preço) e o nome do pool Elástico, se houver, para um banco de dados do SQL Azure ou um Azure SQL Data Warehouse. Se conectado no banco de dados mestre em um servidor de banco de dados do Azure SQL toohello, retorna informações sobre todos os bancos de dados. Para o Azure SQL Data Warehouse, você deve ser conectado toohello banco de dados mestre.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>Gerenciar pools Elásticos do banco de dados SQL usando a API REST de saudação

toocreate e gerenciar pools Elásticos do banco de dados SQL usando Olá API REST, consulte [API de REST de banco de dados SQL do Azure](/rest/api/sql/).

## <a name="next-steps"></a>Próximas etapas

* Para obter um vídeo, confira [Curso em vídeo da Microsoft Virtual Academy sobre os recursos elásticos do Banco de Dados SQL do Azure](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* toolearn mais informações sobre padrões de design para aplicativos SaaS usando pools Elásticos, consulte [padrões de Design para aplicativos de SaaS multilocatário com o Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Para obter um tutorial de SaaS usando pools Elásticos, consulte [toohello Introdução aplicativo SaaS Wingtip](sql-database-wtp-overview.md).
