---
title: aaaAzure estudo de caso do Azure do banco de dados SQL - Umbraco | Microsoft Docs
description: "Saiba mais sobre como o Umbraco usa a provisão de tooquickly do banco de dados SQL e serviços em escala de milhares de locatários na nuvem de saudação"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>O Umbraco usa provisão de tooquickly do banco de dados SQL e serviços em escala de milhares de locatários na nuvem Olá
![Logotipo da Umbraco](./media/sql-database-implementation-umbraco/umbracologo.png)

O Umbraco é um popular sistema código-fonte aberto gerenciamento de conteúdo (CMS) que pode executar qualquer coisa de pequenos sites campanha ou publicação toocomplex aplicativos para empresas da Fortune 500 e sites de mídia global. 

> "Temos uma grande comunidade de desenvolvedores que usam o sistema hello, com mais de 100.000 desenvolvedores em nossos fóruns e sites de mais de 350.000 ao vivo, executando o Umbraco."
> 
> — Morten Christensen, líder técnico da Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

implantações de cliente toosimplify, Umbraco adicionado Umbraco-como um serviço (UaaS): uma oferta de software-como um serviço (SaaS) que elimina a necessidade de saudação para implantações locais, fornece dimensionamento internos e remove o gerenciamento de sobrecarga, permitindo os desenvolvedores toofocus no gerenciamento de inovação em vez de solução do produto. O Umbraco é capaz de tooprovide todos esses benefícios recorrendo Olá flexível modelo (PaaS) de plataforma como serviço oferecido pelo Microsoft Azure.

UaaS permite que os clientes de SaaS toouse Umbraco CMS funcionalidades que anteriormente estavam fora do seu alcance. Esses clientes são provisionados com um ambiente de trabalho CMS que inclui um banco de dados de produção. Os clientes podem se acumular tootwo bancos de dados adicionais para desenvolvimento e teste ambientes, dependendo de seus requisitos. Quando um novo ambiente é solicitado, um processo automatizado atribui esse cliente a um banco de dados automaticamente. novo banco de dados de saudação está pronto em segundos, porque o banco de dados de saudação já tiver sido configurado previamente pelo Umbraco de um pool Elástico do Azure dos bancos de dados disponíveis (consulte a Figura 1).

![Ciclo de vida de provisionamento da Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Figura 1. Provisionando o ciclo de vida da UaaS (Umbraco como serviço)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Pools elásticos do Azure e automação simplificam implantações
Com o Banco de Dados SQL do Azure e outros serviços do Azure, os clientes da Umbraco podem autoprovisionar seus ambientes, e a Umbraco pode monitorar e gerenciar facilmente bancos de dados como parte de um fluxo de trabalho intuitivo:

1. Provisão
   
   A Umbraco mantém uma capacidade de 200 bancos de dados pré-provisionados disponíveis de pools elásticos. Quando um novo cliente se inscreve para UaaS, Umbraco fornece Prezado cliente com um novo ambiente de CMS quase em tempo real, atribuindo-lhes um banco de dados do grupo de disponibilidade de saudação.
   
   Quando um pool de disponibilidade atinge seu limite, um novo pool Elástico é criado e novos bancos de dados são pré-provisionado toobe atribuído toocustomers conforme necessário.
   
   A implementação é totalmente automatizada usando bibliotecas de gerenciamento do C# e filas do Barramento de Serviço do Azure.
2. Utilização
   
   Os clientes usam um ambientes toothree (para produção, teste e desenvolvimento), cada com seu próprio banco de dados. Bancos de dados do cliente estão em pools Elásticos, que permite que o Umbraco tooprovide eficiente de dimensionamento sem a necessidade de provisionar tooover.
   
   ![Visão geral do projeto da Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Detalhes do projeto da Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Figura 2. Site do cliente da UaaS (Umbraco como serviço), mostrando a visão geral e os detalhes do projeto
   
   Banco de dados SQL do Azure usa unidades de transação do banco de dados (DTUs) toorepresent Olá relativa energia necessária para transações de banco de dados do mundo real. Para os clientes UaaS, bancos de dados geralmente operam em 10 DTUs, mas cada um tem Olá elasticidade tooscale sob demanda. Isso significa que a UaaS pode garantir que os clientes sempre tenham os recursos necessários, mesmo durante os horários de pico. Por exemplo, durante um evento de esportes domingo recente, um cliente UaaS apresentou picos de banco de dados para cima too100 DTUs durante saudação jogo hello. Azure pools Elásticos tornam possível que o Umbraco toosupport que exigem alta sem degradação do desempenho.
3. Monitoramento
   
   Monitores Umbraco usar os painéis em Olá portal do Azure, junto com os alertas de email personalizada de atividade de banco de dados.
4. Recuperação de desastre
   
   O Azure fornece duas opções de DR (recuperação de desastre): replicação geográfica ativa e restauração geográfica. Olá opção de recuperação de desastres que uma empresa deve selecionar depende de seu [objetivos de continuidade de negócios](sql-database-business-continuity.md).
   
   replicação geográfica ativa fornece o nível de mais rápido de saudação de resposta no evento de saudação do tempo de inatividade. Usando a replicação geográfica ativa, é possível criar até toofour a secundários legíveis em servidores em diferentes regiões e, em seguida, você pode iniciar failover tooany de secundários Olá na saudação de uma falha.
   
   O Umbraco não exige a replicação geográfica, mas ele tirar proveito da restauração de replicação geográfica do Azure toohelp garantir tempo de inatividade mínimo no evento de saudação de uma interrupção. A restauração geográfica conta com backups de banco de dados no armazenamento do Azure com redundância geográfica. Quando houver uma interrupção na região primária hello, que permite toorestore de usuários de uma cópia de backup.
5. Cancelar provisionamento
   
   Quando um ambiente de projeto é excluído, todos os bancos de dados associados (desenvolvimento, preparo ou ativo) são removidos durante a limpeza da fila do Barramento de Serviço do Azure. Esse processo automatizado restaurações Olá pool de disponibilidade de banco de dados Elástico do tooUmbraco não utilizado de bancos de dados, disponibilizando-as para provisionamento futuro mantendo utilização máxima.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Pools Elásticos permitem UaaS tooscale com facilidade
Aproveitando de pools Elásticos do Azure, Umbraco pode otimizar o desempenho para os seus clientes sem ter que tooover ou provisionar insuficiente. Umbraco atualmente tem aproximadamente 3.000 bancos de dados de pools Elásticos 19, com hello capacidade tooeasily dimensionar como tooaccommodate necessária qualquer um dos seus 325.000 clientes existentes ou novos clientes que são toodeploy pronto um CMS na nuvem hello.

Na verdade, tooMorten Christensen, técnico-chefe da Umbraco, de acordo com "UaaS está agora apresentando o crescimento de cerca de 30 novos clientes por dia. Nossos clientes estão satisfeitos com a conveniência de saudação de ser capaz de tooprovision novos projetos em segundos, publicar atualizações tootheir ao vivo sites de um ambiente de desenvolvimento usando 'implantação de um único clique' instantaneamente e faça alterações tão rapidamente se encontrar erros . "

Se um cliente não precisar mais de um segundo e/ou terceiro ambiente, ele simplesmente poderá removê-los. Que libera os recursos que podem ser usados para outros clientes como parte da saudação pool de disponibilidade de banco de dados Elástico Umbraco.

![Arquitetura de implantação da Umbraco](./media/sql-database-implementation-umbraco/figure4.png)

Figura 3. Arquitetura de implantação da UaaS no Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>caminho de saudação do datacenter toocloud
Quando os desenvolvedores de Umbraco Olá inicialmente Olá decisão toomove tooa modelo SaaS, sabiam que precisam toobuild uma maneira econômica e dimensionável serviço hello.

> "Os pools elásticos são ideais para nossa oferta de SaaS, pois podemos aumentar ou diminuir a capacidade conforme a necessidade. O provisionamento é fácil, e com a nossa configuração, podemos manter a utilização no máximo”.
> 
> — Morten Christensen, líder técnico da Umbraco
> 
> 

"Queríamos toospend nosso tempo na solução de problemas de nossos clientes, não gerenciar a infraestrutura. Queremos toomake fácil para nossos clientes tooget Olá máximo, "diz Niels Hartvig, fundador da Umbraco. "Consideramos inicialmente servidores Olá nós de hospedagem, mas o planejamento de capacidade seria um pesadelo". Coincidentemente, a Umbraco não emprega administradores de banco de dados, o que ressalta uma importante proposta de valor para usar a UaaS.

Um objetivo importante para os desenvolvedores de Umbraco Olá foi tooprovide uma maneira para os ambientes de clientes do tooprovision UaaS rapidamente e sem limitações de capacidade. Mas, fornecer que um serviço hospedado dedicado em datacenters Umbraco teria necessária muita capacidade em excesso toohandle estourar de processamento. Isso significaria adicionar infraestrutura considerável de computação que teria sido regulamente subutilizada.

Além disso, a equipe de desenvolvimento Umbraco Olá desejava uma solução que permitiria tooreuse ao máximo seus códigos existentes possível. Como desenvolvedor Umbraco Mikkel Madsen estados, "ficamos felizes com ferramentas de desenvolvimento do Microsoft hello já foi familiarizados, como Microsoft SQL Server, o banco de dados do Microsoft Azure SQL, ASP.net e serviços de informações da Internet (IIS). Antes de investir em um IaaS ou um PaaS nuvem solução, queremos se ele seria dão suporte a nossas ferramentas da Microsoft e plataformas, portanto, não temos toomake base de código de tooour de alterações em grandes quantidades de toomake. "

toomeet todos os seus critérios, Umbraco procurado em um parceiro de nuvem com hello qualificações a seguir:

* Confiabilidade e capacidade suficientes
* Suporte para ferramentas de desenvolvimento da Microsoft, para que o Umbraco engenheiros não seria forçado toocompletely reinventar o ambiente de desenvolvimento
* Presença em todos os mercados geográficos hello, no qual UaaS compete (empresas necessidade tooensure que eles podem acessar seus dados rapidamente e que seus dados estão armazenados em um local que atenda aos seus requisitos normativos regionais)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Por que a Umbraco escolheu o Azure para a UaaS
De acordo com o tooMorten Christensen "depois de se considerar todas as opções de nosso, selecionamos Azure porque ela atenda a todos os nossos critérios, de capacidade de gerenciamento e escalabilidade toofamiliarity e custo-benefício. Podemos configurar ambientes de saudação em VMs do Azure, e cada ambiente tem sua própria instância do banco de dados SQL, com todas as instâncias de saudação em pools elásticos. Separação de bancos de dados entre o desenvolvimento, teste e ambientes em tempo real, podemos oferecer nossos clientes desempenho robusto isolamento correspondentes tooscale — um enorme ganho. "

Luís continua, "antes, tivemos tooprovision servidores de bancos de dados da web manualmente. Agora, não temos toothink sobre ele. Tudo o que é automatizado — do provisionamento toocleanup. "

Luís também está satisfeito com hello dimensionar os recursos fornecidos pelo Azure. "Os pools elásticos são ideais para nossa oferta de SaaS, pois podemos aumentar ou diminuir a capacidade conforme a necessidade. O provisionamento é fácil, e com a nossa configuração, podemos manter a utilização no máximo”. Luís estados, "hello simplicidade de pools Elásticos, juntamente com garantia de saudação de DTUs baseado em camada de serviço, fornece nos Olá power tooprovision novos pools de recursos sob demanda. Recentemente, um de nossos clientes maior pico too100 DTUs em seu ambiente dinâmico. Usando o Azure, nosso pools Elásticos fornecido bancos de dados do cliente Olá com recursos de saudação que eles necessários em tempo real sem a necessidade de requisitos de DTU toopredict. Em outras palavras, nossos clientes obtém Olá tempo descarregamento que esperam e pode atender aos nossos contratos de nível de serviço de desempenho".

Mikkel Madsen resume: "nós já adotada Olá avançado do Azure algoritmo que se conecta a um padrão comum de SaaS cenário (integração novos clientes em tempo real em escala) tooour aplicativo (provisionamento prévio de bancos de dados, os dois desenvolvimento e ao vivo) sobre Olá tecnologia subjacente (usando filas do barramento de serviço do Azure em conjunto com o banco de dados do SQL Azure)."

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Com o Azure, a UaaS está superando as expectativas dos clientes
Desde escolher Azure como seu parceiro de nuvem, Umbraco foi capaz de tooprovide UaaS clientes com desempenho otimizado do gerenciamento de conteúdo, sem o investimento Olá recursos de TI necessários de uma solução de hospedagem interna. Como Luís afirma, "amamos conveniência de desenvolvedor hello e escalabilidade que o Azure fornece nós e nossos clientes são felizes com recursos de saudação e confiabilidade. De modo geral, tem sido uma grande vitória para nós!"

## <a name="more-information"></a>Mais informações
* toolearn mais informações sobre pools Elásticos do Azure, consulte [pools Elásticos](sql-database-elastic-pool.md).
* toolearn mais sobre o barramento de serviço do Azure, consulte [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn mais informações sobre funções Web e funções de trabalho, consulte [funções de trabalho](../fundamentals-introduction-to-azure.md#compute).    
* toolearn mais sobre redes virtuais, consulte [a rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn mais informações sobre backup e recuperação, consulte [continuidade dos negócios](sql-database-business-continuity.md).    
* toolearn mais sobre o monitoramento ppols, consulte [monitoramento pools](sql-database-elastic-pool-manage-portal.md).    
* toolearn mais sobre o Umbraco como um serviço, consulte [Umbraco](https://umbraco.com/cloud).

