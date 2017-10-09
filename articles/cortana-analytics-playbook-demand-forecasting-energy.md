---
title: "aaaCortana guia estratégico de modelo de solução de inteligência para previsão de demanda de energia | Microsoft Docs"
description: "Um Modelo de Solução com o Microsoft Cortana Intelligence que ajuda a prever a demanda para uma concessionária de energia elétrica."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Manual do Modelo de Solução do Cortana Intelligence para a previsão de demanda de energia
## <a name="executive-summary"></a>Resumo executivo
Na Olá os últimos anos, Internet das coisas (IoT), fontes de energia alternativo e grandes dados têm mescladas oportunidades grande toocreate no utilitário hello e o domínio de energia. Em Olá simultaneamente, utilitário hello e do setor de energia todo Olá viu consumo nivelamento com consumidores mais exigentes toocontrol de maneiras melhor o uso de energia. Portanto, Olá utilitário e grade inteligente empresas estão em grande necessidade tooinnovate e renovar a mesmos. Além disso, muitos grades de consumo de energia e utilitário estão se tornando toomaintain desatualizado e muito cara e gerenciar. Durante a saudação no ano passado, equipe Olá tem trabalhado em um número de contratos no domínio de energia hello. Durante esses contratos, encontramos muitos casos, no qual Olá utilitários ou ISVs (fornecedores independentes de Software) foi procurando na previsão de demanda de energia futuras. Essas previsões desempenham um papel importante em seus negócios atuais e futuros e tornaram foundation Olá para vários casos de uso. Elas incluem, a curto e a longo prazos, a previsão, comércio, balanceamento de carga e otimização da rede da carga de energia, entre outras. Dados grandes e métodos de análise avançada (AA) como o aprendizado de máquina (ML) são habilitadores-chave Olá para produzir previsões precisas e confiáveis.  

Neste guia estratégico, reunimos business hello e diretrizes analíticas necessárias para um desenvolvimento bem-sucedido e solução de previsão de implantação de demanda de energia. Essas diretrizes propostas podem ajudar empresas de serviços, cientistas de dados e engenheiros de dados no estabelecimento de soluções totalmente operacionalizadas, baseadas em nuvem, de previsão de demanda. Para as empresas que estão iniciando seus dados grandes e jornada de análise avançada, essa solução pode representar a propagação inicial Olá em sua estratégia de grade inteligente a longo prazo.

> [!TIP]
> toodownload um diagrama que fornece uma visão geral da arquitetura desse modelo, consulte [arquitetura de modelo de solução de inteligência Cortana para previsão de demanda de energia](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Visão geral
Este documento aborda Olá negócios, dados e aspectos técnicos da usando inteligência de Cortana e em particular do Azure máquina aprendizado AML para implementação de saudação e implantação de soluções de previsão de energia. Olá documento consiste em três partes principais:  

1. Noções básicas sobre negócios  
2. Noções básicas sobre dados  
3. Implementação técnica

Olá **compreensão de negócios** descreve parte Olá business aspecto um necessidades toounderstand e considere toomaking anterior uma decisão de investimento. Ele explica como tooqualify Olá problema de negócios em mão tooensure análises de previsão e aprendizado de máquina são realmente eficaz e aplicável. documento de Hello mais explica conceitos básicos de saudação de aprendizado de máquina e como ele é usado tooaddress previsão energia problemas. Descreve os pré-requisitos de saudação e critérios de qualificação de saudação de um caso de uso. Alguns casos de uso e cenários de caso de uso de exemplo também são fornecidos.

Dados são um elemento principal Olá para qualquer solução de aprendizado de máquina. Olá **dados Noções básicas sobre** parte deste documento aborda alguns aspectos importantes de dados de saudação. Descreve o tipo de saudação de dados que é necessário para previsão de energia, requisitos de qualidade de dados e quais fontes de dados normalmente existem. Explicaremos também como dados brutos de saudação são tooprepare usado recursos de dados que realmente Olá modelagem parte da unidade.

a terceira parte saudação do documento hello abrange Olá **implementação técnica** aspecto de uma solução. Engenharia de recurso e modelagem são Olá núcleo do processo de ciência de dados hello e, portanto, estão sendo discutidos em detalhes. Ele aborda o conceito de saudação de serviços web, que são um importante veículo para implantação de soluções de análise preditiva em nuvem. Nós também descrevemos uma arquitetura típica de uma solução operacionalizada completa.

Além disso, o documento de saudação inclui material de referência que você pode usar toogain melhor entendimento de tecnologia e domínio hello.

É importante toonote que não pretendemos toocover nesse processo do ciência de dados mais profunda no documento hello, seus aspectos técnicos e matemáticos. Esses detalhes podem ser encontrados na documentação do [AM do Azure](http://azure.microsoft.com/services/machine-learning/) e em [blogs](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Público-alvo
Olá público-alvo deste documento são os negócios e a equipe técnica que gostaria de dados de Conhecimento toogain e compreensão de aprendizado de máquina com base em como eles estão sendo usados especificamente no domínio de previsão de energia hello e soluções.

Os cientistas de dados também podem se beneficiar de ler este documento toogain uma melhor compreensão do processo de nível alto de saudação unidades Olá implantação de uma solução de previsão de energia. Neste contexto também pode ser usado tooestablish uma boa linha de base e o ponto de partida para obter mais informações detalhadas e avançados material.

### <a name="industry-trends"></a>Tendências do Setor
Na Olá os últimos anos, IoT, fontes de energia alternativo e grandes dados têm mescladas oportunidades grande toocreate utilitário hello e espaço de energia. Em Olá simultaneamente, utilitário hello e setores de energia todo Olá viu consumo nivelamento com consumidores mais exigentes toocontrol de maneiras melhor o uso de energia.

Muitos utilitário e empresas de energia inteligente tem sido pioneiras Olá [grade inteligente](https://en.wikipedia.org/wiki/Smart_grid) Implantando um número de uso casos que fazem usam de dados de saudação gerados pela grade de saudação. Muitos casos de uso giram em torno de características inerentes de saudação de produção de eletricidade: não podem ser acumulado ou armazenado separadamente, como inventário. Portanto, o que é produzido deve ser usado. Utilitários que deseja toobecome mais eficiente precisam de consumo de energia tooforecast simplesmente porque isso fornecerá a eles maior capacidade muito**equilibrar o fornecimento e a demanda**, evitando assim que o desperdício de energia, **reduzir greenhouse emissão de gás**e controlar os custos.

Quando falamos de custos, há outro aspecto importante, o preço. Novo power tootrade de recursos entre utilitários levou a necessidade de ótima muito**prever as demandas futuras e preços futuros de eletricidade**. Isso pode ajudar as empresas a determinar seus volumes de produção.

Quando usamos a palavra de saudação 'inteligente', nos referimos realmente grade tooa que saiba e, em seguida, fazer previsões. Ela pode prever alterações sazonais no consumo, bem como **prever situações de sobrecarga temporária e ajustar-se automaticamente a elas**. Regulando remotamente consumo (com a Ajuda de saudação desses medidores inteligentes), podem ser manipuladas situações de sobrecarga localizada. **Prevendo primeiro e, em seguida, atuando**, grade Olá se torna mais inteligente ao longo do tempo.

Para rest Olá deste documento, vamos nos concentrar em uma família específica de casos de uso que abrangem a previsão do futuro, curto e longo prazo demanda de energia. Vamos trabalhado nas seguintes áreas para alguns meses e adquirido alguns dados de conhecimento e habilidades que nos permitem tooproduce resultados de classificação de setor. Outros casos de uso serão abordados também documento Olá Olá futuro próximo.

## <a name="business-understanding"></a>Noções básicas sobre negócios
### <a name="business-goals"></a>Metas de Negócios
Olá **energia demonstração** meta é toodemonstrate uma análise preditiva comuns e soluções que podem ser implantadas em um período muito curto de aprendizado de máquina. Especificamente, nosso foco atual é habilitar as soluções de previsão de demanda de energia para que seu valor de negócios possa ser percebido e aproveitado com rapidez. Olá informações neste guia estratégico podem ajudar cliente Olá a realização Olá seguintes metas:

* Solução baseada em toovalue curto período de tempo de aprendizado de máquina
* Capacidade tooexpand um tooother de caso de uso piloto usar casos ou um escopo mais amplo tooa com base em suas necessidades comerciais
* Obter rapidamente o conhecimento sobre o produto Cortana Intelligence Suite

Com esses objetivos em mente, este guia estratégico pretende proporcionar business hello e conhecimento técnico que ajudam a atingir esses objetivos.

### <a name="power-load-and-demand-forecasting"></a>Carga de Energia e Previsão de Demanda
No setor de energia hello, pode haver muitas maneiras em que demanda de previsão pode ajudar a solucionar problemas de negócios críticos. Na verdade, previsão de demanda pode ser considerado foundation Olá para muitos casos de uso principal no setor de saudação. Em geral, consideramos dois tipos de previsões de demanda de energia: a curto prazo e a longo prazo. Cada um pode servir a uma finalidade diferente e utilizar uma abordagem diferente. Olá principal diferença entre Olá dois é Olá horizonte, que significa que o intervalo de saudação de tempo em Olá futuro para o qual podemos seria prever a previsão.

#### <a name="short-term-load-forecasting"></a>Previsão de Carga a Curto Prazo
No contexto de saudação de demanda de energia, curto prazo carregar previsão (STLF) é definido como Olá agregados de carga que é prevista no hello futuro em várias partes de grade hello (ou grade hello como um todo) próximo. Nesse contexto, a curto prazo é prazo toobe definido dentro do intervalo de saudação de horas de too24 de 1 hora. Em alguns casos, um limite de 48 horas também é possível. Portanto, STLF é muito comum em um caso de uso operacional da grade de saudação. Veja alguns exemplos de casos de uso orientados pela STLF:

* Equilíbrio do fornecimento e da demanda
* Suporte à comercialização de energia
* Tomada de mercado (definição do preço da energia)
* Otimização operacional da rede
* [Resposta da demanda](https://en.wikipedia.org/wiki/Demand_response)
* Previsão da demanda de pico
* Gerenciamento do lado da demanda
* Balanceamento de carga e prevenção de sobrecarga
* Previsão de Carga a Longo Prazo
* Detecção de anomalias e de falhas
* Redução/nivelamento do pico 

Modelo STLF baseiam-se principalmente no hello perto anteriores (último dia ou semana) dados de consumo e usar a previsão temperatura como uma previsor importante. Como obter a temperatura precisa para Olá próxima hora e até too24 horas de previsão está se tornando menor um desafio dias agora. Esses modelos são padrões de tooseasonal menos confidenciais ou as tendências de consumo de longo prazo.

Soluções SLTF também são provavelmente toogenerate alto volume de chamadas de previsão (solicitações de serviço) desde que estão sendo invocados por hora e, em alguns casos mesmo com maior frequência. Também é muito comum implantação toosee onde cada Subestação individual ou transformador é representado como um modelo autônomo e, portanto, o volume de saudação de solicitações de previsão é ainda maior.

#### <a name="long-term-load-forecasting"></a>Previsão de Carga a Longo Prazo
o objetivo de saudação de longo prazo carga previsão (LTLF) é tooforecast demanda de energia com um limite de tempo que variam dos meses de toomultiple 1 semana (e, em alguns casos para um número de anos). Esse intervalo de horizonte é aplicável principalmente aos casos de uso de planejamento e de investimento.

Para cenários de longo prazo, é importante toohave dados de alta qualidade que abrange um intervalo de vários anos (mínimo 3 anos). Esses modelos normalmente serão extrair padrões de periodicidade dos dados históricos hello e usam predicators externos, como padrões de tempo e clima.

É importante é tooclarify que Olá Olá mais horizonte de previsão, Olá menos precisos Olá previsão pode ser. Portanto, é importante tooproduce alguns intervalos de confiança com hello real de previsão que permitiria que os usuários toofactor Olá possível diferença em seu processo de planejamento.

Desde que o cenário de consumo de saudação para LTLF principalmente está planejando, podemos esperar muito inferiores volumes de previsão (como comparado tooSTLF). Nós geralmente verá essas previsões incorporadas em ferramentas de visualização, como Excel ou Power BI e ser invocados manualmente pelo usuário hello.

### <a name="short-term-vs-long-term-prediction"></a>Previsão a Curto Prazo versus a Longo Prazo
Olá, a tabela a seguir compara STLF e LTLF em atributos mais importantes de toohello de relação:

| Atributo | Previsão de Carga a Curto Prazo | Previsão de Carga a Longo Prazo |
| --- | --- | --- |
| Horizonte de Previsão |De horas de too48 de 1 hora |De meses 1 too6 ou mais |
| Granularidade de dados |Por hora |Por hora ou por dia |
| Casos de uso típicos |<ul><li>Balanceamento de demanda/fornecimento</li><li>Selecionar a hora de previsão</li><li>Resposta da demanda</li></ul> |<ul><li>Planejamento a longo prazo</li><li>Planejamento de ativos de grade</li><li>Planejamento de recursos</li></ul> |
| Indicadores típicos |<ul><li>Dia ou semana</li><li>Hora do dia</li><li>Temperatura por hora</li></ul> |<ul><li>Mês do ano</li><li>Dia do mês</li><li>Clima e temperatura a longo prazo</li></ul> |
| Intervalo de dados históricos |Dois toothree anos de dados |Cinco too10 anos de dados |
| Precisão típica |MAPE* de 5% ou menos |MAPE* de 25% ou menos |
| Frequência de previsão |Produzida a cada hora ou a cada 24 horas |Produzida uma vez por mês, trimestre ou ano |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) – Erro Percentual Médio

Como pode ser visto desta tabela, é muito importante toodistinguish entre hello curto e longo prazo de saudação previsão cenários como eles representam as diversas necessidades dos negócios e podem ter diferentes de implantação e padrões de consumo.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Caso de Uso do Exemplo 1: Sistemas eSmart – otimização de sobrecarga
Uma função importante de uma [grade inteligente](https://en.wikipedia.org/wiki/Smart_grid) é toodynamically e constantemente otimizar e ajustar para Olá alterando os padrões de consumo. O consumo de energia pode ser afetado por alterações a curto prazo causadas principalmente por flutuações de temperatura (*por exemplo*, mais energia é usada em sistemas de ar condicionado ou de aquecimento). AT Olá mesmo tempo, energia consumo também é influenciado por tendências de longo prazo. Elas podem incluir efeitos de periodicidade, feriados nacionais, crescimento do consumo a longo prazo e até fatores econômicos como o índice do consumidor, o preço do petróleo e o PIB.

No caso de uso, [eSmart](http://www.esmartsystems.com/) quisesse solução toodeploy um baseado em nuvem que permite que a previsão propensity saudação de uma situação de sobrecarga em qualquer determinada Subestação da grade de saudação. Em particular, eSmart desejava substations tooidentify que são provavelmente toooverload dentro Olá próxima hora, para que uma ação imediata podem ser tomadas tooavoid ou resolver a situação.

Uma previsão de execução precisa e rápida exige a implementação de três modelos de previsão:

* Tempo modelo termo que habilita a previsão de consumo de energia em cada Subestação durante Olá Avançar algumas semanas ou meses
* Modelo de curto prazo que permite que a previsão da situação de sobrecarga em uma determinado Subestação durante a saudação próxima hora
* O modelo de temperatura que fornece a previsão de temperatura futura em vários cenários

objetivo de saudação do modelo de longo prazo Olá é substations de saudação toorank por seu toooverload propensity (concedida sua capacidade de transmissão) durante a saudação próxima semana ou mês. Isso permite a criação de saudação de uma lista curta de substations seria servir como uma entrada para previsão a curto prazo hello. Como a temperatura é uma previsor importante para o modelo de longo prazo hello, há uma temperatura de multi-cenário necessidade tooconstantly produzir previsões e feed-los como entrada no modelo de longo prazo toohello. previsão de curto prazo de saudação é invocada em seguida toopredict toooverload provável é que Subestação sobre Olá próxima hora.

modelos de curto e longo prazo de saudação são implantados individualmente por cada Subestação. Portanto, a execução prático Olá desses modelos precisa orquestração ampla. toogain maior precisão de previsão de curto prazo hello, um modelo mais granular dedicado para cada hora do dia de saudação. Todos esses modelos são executados a cada hora e concluir a execução dentro de alguns minutos tooallow suficientes tempo toorespond e tomar medidas preventivas, se necessário. Esta coleção de modelos é mantida atualizada pelo treinamento periódico usando os dados mais recentes hello.

Mais informações sobre este caso de uso podem ser encontradas [aqui](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Usar Critérios de Qualificação de Caso – Pré-requisitos
força de principal de saudação do Cortana inteligência é em sua capacidade poderoso toodeploy e escala machine learning centrado em soluções. Ele é projetado toosupport milhares de previsões que são executadas simultaneamente. Ele pode ser dimensionado automaticamente toomeet um padrão de consumo de alteração. Portanto, o foco da solução é a precisão e o desempenho computacional. Por exemplo, uma empresa de utilitário está interessa na produção de energia precisos previsão de vendas para Olá próxima hora e para cada hora do dia de saudação. Em Olá outro lado, estamos menos interessados em responder a pergunta de saudação por demanda Olá é previsto toobe como (próprio modelo Olá cuidará disso).

Portanto, é importante toorealize que nem todos os casos de uso e problemas de negócios podem ser resolvidos com eficiência usando o aprendizado de máquina.

Inteligência de Cortana e aprendizado de máquina podem ser altamente eficazes para resolver um problema de negócios específico quando Olá critérios a seguir forem atendida:

* Olá problema de negócios em mãos é **previsão** por natureza. Um exemplo de caso de uso de previsão é uma empresa de utilitário que gostaria de carga de energia toopredict em uma determinado Subestação durante a saudação próxima hora. Em Olá outro lado, analisando e drivers de demanda de histórico de classificação deve ser **descritivo** por natureza e, portanto, menos aplicável.
* Há uma clara **caminho da ação** toobe executada uma vez previsão hello está disponível. Por exemplo, prever uma sobrecarga em uma Subestação durante a saudação próxima hora pode disparar uma ação proativa de reduzir a carga que está associada esse Subestação e, portanto, potencialmente, evitando uma sobrecarga.
* caso de uso de saudação representa um **típico tipo de problema** , de modo que quando resolvido Olá maneira toosolving pode preparar outros casos de uso semelhantes.
* Prezado cliente pode definir **metas quantitativas e qualitativas** toodemonstrate uma implementação de solução bem-sucedida. Por exemplo, uma meta quantitativa bom para previsão de demanda de energia seria limiar de exatidão necessária de saudação (*, por exemplo,*, backup too5% erro é permitido) ou durante a previsão de sobrecarga Subestação e precisão hello (taxa de verdadeiros positivos) e Lembre-se (extensão de verdadeiros positivos) deve estar acima de um determinado limite. Essas metas devem ser derivadas de metas de negócios do cliente hello.
* Há uma clara **cenário de integração** ao fluxo de trabalho de negócios da empresa hello. Por exemplo, Olá Subestação carga previsão pode ser integrado em atividades de prevenção de saudação grade controle center tooallow sobrecarga.
* Prezado cliente tem toouse pronto **dados com qualidade suficiente** toosupport Olá caso de uso (consulte mais na próxima seção, Olá, **de qualidade de dados**, neste guia estratégico).
* Olá arquitetura do cliente abraços nuvem centrados em dados ou **aprendizado de máquina com base em nuvem**, incluindo ML do Azure e outros componentes do pacote de inteligência do Cortana.
* Prezado cliente é disposto tooestablish **um fluxo de dados final tooend** que instalações Olá a entrega de dados em nuvem Olá continuamente e estiver dispostas muito**operacionalizar** Olá solução.
* Prezado cliente está pronto muito**dedicar recursos** que será ser ativamente envolvido durante a implementação do piloto inicial Olá para que os dados de conhecimento e a propriedade da solução Olá podem ser transferidos toohello cliente após bem-sucedida conclusão.
* recursos de cliente Olá devem ser um **professional dados qualificados**, preferencialmente um cientista de dados.

Qualificação de um caso de uso com base em Olá critérios acima consideravelmente pode melhorar as taxas de sucesso de saudação de um caso de uso e estabelecer um bom beachhead para implementação de saudação de casos de uso futuro.

### <a name="cloud-based-solutions"></a>Soluções Baseadas em Nuvem
Pacote de inteligência do Cortana no Azure é um ambiente integrado que reside na nuvem hello. implantação de saudação de uma solução de análise avançada em um ambiente de nuvem contém importantes benefícios para empresas e em Olá a mesmo tempo pode significar grande alteração para as empresas que ainda usar local soluções de TI. No setor de energia hello, há uma tendência clara de migração gradual de operações em nuvem hello. Essa tendência vai lado a lado junto com o desenvolvimento de saudação da grade inteligente hello como discutido acima, em **as tendências do setor**. Como este guia estratégico destina-se em uma solução baseada em nuvem no domínio de energia Olá, é importante tooexplain benefícios de saudação e outras considerações de implantação de uma solução baseada em nuvem.

Talvez hello maior vantagem de uma solução baseada em nuvem é Olá custo. Como as soluções utilizam componentes implantados na nuvem, não há custos iniciais ou COGS (Custo dos Bens Vendidos) associados a elas. Isso significa que não há nenhum tooinvest necessidade de hardware, software e manutenção de TI e, portanto, há uma redução significativa de risco para os negócios.

Outra vantagem importante é a estrutura de custo pré-pago de saudação de soluções baseadas em nuvem. Os servidores baseados em nuvem para computação ou armazenamento podem ser implantados e dimensionados conforme o necessário. Isso representa Olá vantagem de eficiência de custo de uma solução baseada em nuvem.

Por fim, não é necessário para investir no desenvolvimento de futuras de infraestrutura ou de manutenção de TI como tudo isso faz parte da oferta de saudação baseado em nuvem. extensão toothat, pacote de inteligência Cortana inclui Olá melhor nos serviços de classe e seu roteiro mantém em evolução. Novos recursos e componentes são constantemente introduzidos e evoluem.

Para uma empresa que está iniciando sua transição para a nuvem hello, altamente recomendamos tootake uma abordagem gradual implementando um roteiro de migração de nuvem. Acreditamos para utilitários e chaves de configuração de energia hello, casos de uso de saudação que são abordados neste guia estratégico representam uma excelente oportunidade para piloto soluções de análise preditiva em nuvem hello.

#### <a name="business-case-justification-considerations"></a>Considerações sobre a Justificativa de Casos de Negócios
Em muitos casos, Prezado cliente pode estar interessado em tornar uma justificativa de negócios para um caso de uso específico em que uma solução baseada em nuvem e aprendizado de máquina são componentes importantes. Ao contrário de uma solução local, no caso de saudação de uma solução baseada em nuvem, Olá componente de custo antecipado é mínimo e a maioria dos elementos de custo Olá está associada com o uso real. Quando se trata de um solução no pacote de inteligência Cortana a previsão de energia toodeploying, vários serviços podem ser integrados com uma única estrutura comum de custo. Por exemplo, bancos de dados (*, por exemplo,*, SQL Azure) podem ser dados brutos de saudação toostore usado e, em seguida, para Olá real prevê ML do Azure é usado toohost Olá previsão serviços. Neste exemplo, Olá custo estrutura pode incluir componentes transacionais e armazenamento.

Em Olá outro lado, um deve ter uma boa compreensão do valor comercial de saudação do operando uma demanda de energia previsão (curto ou longo prazo). Na verdade, é o valor de negócios de saudação toorealize importantes de cada operação de previsão. Por exemplo, com precisão próximas 24 horas de previsão de carga de energia para Olá pode impedir que overproduction ou pode ajudar a evitar sobrecargas em grade hello e isso pode ser determinado em termos de redução de custos em uma base diária.

Uma fórmula básica para calcular o benefício financeiro de saudação de demanda previsão a solução seria: ![básica fórmula para calcular o benefício financeiro de saudação da demanda de solução de previsão](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Desde que o pacote de inteligência Cortana fornece um modelo de preços pré-pago, não é necessário para incorrer em uma fórmula de toothis de componente de custo fixo. Esta fórmula pode ser calculada de forma diária, mensal ou anual.

Os planos de preços atuais do Cortana Intelligence Suite e do AM do Azure podem ser encontrados [aqui](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Processo de Desenvolvimento da Solução
ciclo de desenvolvimento de saudação de uma solução geralmente envolve 4 fases, em que podemos fazer a previsão de demanda de energia usar tecnologias baseadas em nuvem e serviços em Olá Cortana Intelligence Suite.

Isso é ilustrado no diagrama a seguir de saudação:

![Ciclo de Rede Inteligente](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Olá parágrafo a seguir descreve esse processo da 4 etapa:

1. **Coleta de Dados** – qualquer solução baseada em análise avançada baseia-se em dados (veja **Noções básicas sobre dados**). Especificamente, quando se trata de toopredictive análise e previsão, contamos com fluxo contínuo e dinâmico de dados. No caso de saudação de previsão de demanda de energia, esses dados podem ser originados de smart metros ou já agregados em um banco de dados local. Nós também utilizamos fontes de dados externas, como o clima e a temperatura. Esse fluxo contínuo de dados deve ser organizado, agendado e armazenado. [Data Factory do Azure](http://azure.microsoft.com/services/data-factory/) (ADF) é a nossa força de trabalho principal para realizar essa tarefa.
2. **Modelagem** – para previsões precisas e confiáveis de energia, um deve desenvolver (treinar) e manter um modelo excelente que faz uso de dados históricos Olá e extrai Olá significativo e Olá de previsão padrões nos dados. área de saudação do aprendizado de máquina (ML) foi crescendo rapidamente com algoritmos mais avançados que estão sendo desenvolvidos rotineiramente. O Azure ML Studio fornece uma excelente experiência de usuário que ajuda a utilizar hello mais avançada algoritmos ML dentro de um fluxo de trabalho da conclusão. Fluxo de trabalho é ilustrado no diagrama de fluxo de intuitivo e inclui a preparação de dados Olá, extração de um recurso, modelagem e avaliação do modelo. usuário Olá pode efetuar pull de centenas de vários modelos que estão incluídos nesse ambiente. Final de saudação desta fase um cientista de dados terá um modelo de trabalho que é totalmente avaliado e pronto para a implantação.
   
   Olá diagrama a seguir é uma ilustração de um fluxo de trabalho típico:
   
   ![Fluxo de Trabalho de Modelagem](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Implantação** – com um modelo de trabalho simultaneamente, o hello próxima etapa é implantação. Aqui modelo Olá é convertido em um serviço web que expõe uma API RESTful que podem ser invocados simultaneamente em Olá Internet de vários clientes de consumo. ML do Azure fornece uma maneira simples de implantar um modelo diretamente de saudação do Azure ML Studio, com um único clique de um botão. o processo de implantação inteiro Olá acontece subjacente hello. Essa solução pode dimensionar automaticamente toomeet consumo de saudação necessário.
4. **Consumo** – nesta fase, podemos realmente fazer uso de saudação previsões tooproduce de modelo de previsão. consumo de saudação pode ser ativado em um aplicativo de usuário (*, por exemplo,*, painel) ou diretamente de um sistema operacional, como demanda/forneça balanceamento de sistema ou uma solução de otimização da grade. Vários casos de uso podem ser obtidos de um único modelo.

## <a name="data-understanding"></a>Noções básicas sobre dados
Depois de abordar considerações de negócios da saudação (consulte **compreensão de negócios**) de uma demanda de energia a previsão da solução, agora estamos prontos toodiscuss Olá parte de dados. Qualquer solução de análise preditiva se baseia em dados confiáveis. Para a previsão de demanda de energia, podemos contar com dados históricos de consumo com vários níveis de granularidade. Que dados históricos são usados como Olá matérias-primas. Ele passará a uma análise cuidadosa quais Olá cientista de dados identificará previsões (também chamado tooas recursos) que podem ser colocados em um modelo que eventualmente irá gerar previsões Olá necessário.

Restante Olá nesta seção, descreveremos Olá várias etapas e considerações sobre noções básicas sobre dados saudação e como toobring-formulário utilizável tooa.

### <a name="hello-model-development-cycle"></a>Olá ciclo de desenvolvimento de modelo
A produção de bons modelos requer uma preparação e um planejamento cuidadosos. Separando Olá concentrando-se em uma etapa por vez e modelagem de processo em várias etapas pode melhorar drasticamente o resultado de saudação de todo o processo de saudação.

Olá diagrama a seguir ilustra como Olá processo de modelagem pode ser dividida em várias etapas:

![Ciclo de Desenvolvimento do Modelo](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Como pode ser visto Olá ciclo consiste nas seis etapas:

* Formulação do problema
* Ingestão de dados e exploração de dados
* Preparação de dados e engenharia de recursos
* Modelagem
* Avaliação do modelo
* Desenvolvimento

No restante desta seção Olá descreveremos etapas individuais hello e tooconsider de itens em cada etapa.

### <a name="problem-formulation"></a>Formulação do problema
Pode consideramos formulação de problema hello como hello mais importante etapa um precisa tooimplementing anterior tootake qualquer solução de análise de previsão. Aqui nós transformar Olá problema comercial e decompô-lo elementos toospecific que podem ser resolvidos por meio de dados e modelagem técnicas. É um problema de saudação uma boa prática tooformulate como um conjunto de perguntas que gostaria tooanswer. Aqui estão algumas perguntas possíveis que podem ser aplicáveis no escopo de saudação da previsão de demanda de energia:

* O que é a carga Olá esperado em uma Subestação individual no hello próxima hora ou dia?
* O horário do dia Olá minha grade enfrentam picos de demanda?
* Qual é a probabilidade minha grade toosustain Olá esperado picos de carga?
* Quanta energia Olá power estação deve gerar durante cada hora do dia Olá?

Formular a essas perguntas permite toofocus Obtendo dados certos hello e implementando uma solução que está totalmente alinhada com o problema de negócios Olá em questão. Além disso, em seguida, podemos definir algumas métricas-chave que nos permitem tooevaluate desempenho de saudação do modelo de saudação. Por exemplo, a exatidão deve Olá previsão ser e o que é o intervalo de saudação do erro que possa ser aceitável pelos negócios Olá?

### <a name="data-sources"></a>Fontes de dados
grade de smart modernos Olá coleta dados de várias partes e componentes da grade de saudação. Esses dados representam vários aspectos da operação de saudação e a utilização de saudação da grade de energia hello. No escopo de saudação de previsão de demanda de energia hello, podemos limitam o discussão Olá em fontes de dados que refletem o consumo de demanda real hello. Uma fonte do consumo de energia importante é composta pelos medidores inteligentes. Utilitários de mundo Olá são implantar rapidamente metros inteligentes para seus consumidores. Smart metros registram o consumo de energia real hello e retransmissão constantemente esse utilitário de toohello back de dados da empresa. Dados são coletados e enviados de volta em um intervalo fixo, variando de cada hora too1 de 5 minutos. Medidores inteligentes mais avançados podem ser programados remotamente toocontrol e saldo Olá consumo real dentro de uma casa. Os dados dos medidores inteligentes são relativamente confiáveis e incluem um carimbo de data/hora. Dessa maneira, é um ingrediente importante para a previsão da demanda. Dados de medidor podem ser agregados (somados backup) em vários níveis na topologia de grade Olá: transformador subestação, região, *etc*. Podemos, em seguida, escolher toobuild de nível de agregação Olá necessário um modelo de previsão para ele. Por exemplo, se a empresa de utilitário hello como tooforecast futuras carrega em cada um dos seus substations de grade, em seguida, dados dos todos os medidores podem ser agregados para cada Subestação individual e usados como entrada para Olá modelo de previsão. Nós nos referimos toosmart metros como uma fonte de dados interno.

Uma previsão de demanda de energia confiável também se baseará em outras fontes de dados externas. Um importante fator que afeta o consumo de energia é Olá tempo ou temperatura de saudação com mais precisão. Os dados históricos mostram uma forte correlação entre a temperatura externa e o consumo de energia. Durante dias verão ativa, verifique os consumidores usam de seu ar-condicionado e durante a inicialização de inverno Olá em sistemas de aquecimento. Uma fonte confiável de temperaturas históricas no local de grade hello, portanto, é chave. Além disso, também contamos com a previsão exata da temperatura como um indicador do consumo de energia.

Outras fontes de dados externas também podem ajudar na criação de modelos de previsão de demanda de energia. Elas podem incluir alterações de clima a longo prazo, índices econômicos (*por exemplo*, o PIB), entre outros. Neste documento, não incluiremos essas fontes de dados.

### <a name="data-structure"></a>Estrutura de Dados
Depois de identificar Olá necessário fontes de dados, podemos seria como tooensure dados brutos que foram coletados incluem Olá corrija recursos de dados. modelo de previsão toobuild uma demanda confiável, temos tooensure que Olá dados coletados inclui elementos de dados que podem ajudar a prever as demandas futuras hello. Aqui estão alguns requisitos básicos relacionados com a estrutura de dados de saudação (esquema) dos dados brutos de saudação.

dados brutos Olá consistem em linhas e colunas. Cada medição é representada como uma única linha de dados. Cada linha de dados inclui várias colunas (também chamados tooas recursos ou campos).

1. **Carimbo de data / hora** – campo de data e hora de saudação representa tempo real de saudação quando medida Olá foi gravada. Ele deve estar de acordo com um dos formatos de data/hora comuns hello. Ambas as partes de data e de hora devem ser incluídas. Na maioria dos casos, não é necessário para Olá tempo toobe registradas até Olá segundo nível de granularidade. É importante toospecify Olá fuso horário no qual os dados de saudação são gravados.
2. **ID de medidor** -este campo identifica medidor hello ou dispositivo de medição de saudação. É uma variável categórica e pode ser uma combinação de caracteres e de dígitos.
3. **Valor de consumo** – este é o consumo real de saudação em uma determinada data/hora. consumo de saudação pode ser medido em kWh (kilowatt) ou qualquer outro preferencial unidades. É importante toonote que Olá a unidade de medida deve permanecer consistente em todas as medidas dados saudação. Em alguns casos, o consumo pode ser fornecido em mais de três fases de energia. Nesse caso, seria necessário toocollect todas as fases de consumo independente de saudação.
4. **Temperatura** – temperatura Olá normalmente é coletada de uma fonte independente. No entanto, ele deve ser compatível com dados de consumo de saudação. Ele deve incluir um carimbo de hora conforme descrito acima que permitirá que ele toobe sincronizados com os dados de consumo real de saudação. o valor de temperatura Olá pode ser especificado em ° c ou Fahrenheit, mas deve permanecer consistente em todas as medidas.
5. **Local –** campo de local de saudação é geralmente associado com local Olá onde Olá temperatura dados foram coletados. Ele pode ser representado em forma de um número de código postal ou no formato de latitude/longitude (lat/long).

Olá tabelas a seguir mostra exemplos de um formato de dados de consumo e temperatura bom:

| **Data** | **Hora** | **ID de medidor** | **Fase 1** | **Fase 2** | **Fase 3** |
| --- | --- | --- | --- | --- | --- |
| 1/7/2015 |10:00:00 |ABC1234 |7.0 |2,1 |5,3 |
| 1/7/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 1/7/2015 |10:00:02 |ABC1234 |6,0 |2,1 |4,0 |

| **Data** | **Hora** | **Localidade** | **Temperatura** |
| --- | --- | --- | --- |
| 1/7/2015 |10:00:00 |11242 |24,4 |
| 1/7/2015 |10:00:01 |11242 |24,4 |
| 1/7/2015 |10:00:02 |11242 |24,5 |

Como pode ser visto acima, este exemplo inclui três valores diferentes para o consumo associado a três fases de energia. Além disso, observe que os campos de data e hora Olá estão separadas, porém eles também podem ser combinados em uma única coluna. Nesse caso a coluna de local de saudação é representada em um formato de código postal de 5 dígitos e temperatura de saudação em um formato grau Celsius.

### <a name="data-format"></a>Formato de Dados
Pacote de inteligência Cortana pode dar suporte a formatos de dados mais comuns hello como CSV, TSV, JSON, *etc*. É importante que esse formato de dados Olá permanece consistente para Olá todo o ciclo de vida do projeto de saudação.

### <a name="data-ingestion"></a>Ingestão de dados
Desde que a previsão de demanda de energia é previsto constantemente e com frequência, devemos garantir que os dados brutos de saudação estão fluindo por meio de um processo de inclusão de dados confiável e estável. o processo de inclusão de saudação deve garantir que dados brutos hello estão disponíveis para Olá processo de previsão no tempo de saudação necessário. Que implica que frequência de ingestão de dados Olá deve ser maior que Olá frequência de previsão.

Por exemplo: se nossos demanda previsão solução poderia gerar uma nova previsão às 8:00 em uma base diária, em seguida, precisamos tooensure todos os dados de saudação que foram coletados durante a última Olá 24 horas foi totalmente incluída até que ponto e tem tooeven incluem Olá última hora de dados.

Em ordem tooaccomplish isso, Cortana Intelligence Suite oferece toosupport de várias maneiras que um processo de inclusão de dados confiável. Isso será discutido mais em Olá **implantação** seção deste documento.

### <a name="data-quality"></a>Qualidade de Dados
fonte de dados brutos Olá que é necessária para executar a previsão de demanda e do projeto deve atender a alguns critérios de qualidade de dados básico. Embora métodos estatísticos avançados podem ser usada toocompensate para algum problema de qualidade de dados, ainda precisamos tooensure que nós são Cruzando algum limite de qualidade de dados base ingestão de novos dados. Veja algumas considerações em relação à qualidade dos dados brutos:

* **Valor ausente** – refere-se a situação de toohello quando medida específica não foi coletada. requisito básico Olá aqui é que Olá ausente taxa de valor não deve ser maior que 10% para qualquer período de tempo determinado. No caso em que um único valor esteja ausente, ele deverá ser indicado usando um valor predefinido (por exemplo: “9999”) e não “0”, que pode ser uma medição válida.
* **Precisão medida** – valor real de saudação do consumo ou temperatura deve ser registrado com precisão. Medição imprecisas produzirão previsões imprecisas. Normalmente, o erro de medição de saudação deve ser menor que o valor verdadeiro do toohello relativo de 1%.
* **Tempo de medida** – é necessário que Olá real carimbo de hora Olá dados coletados não desviar-se por mais de 10 segundos relativo toohello horário de medida real hello.
* **Sincronização** – quando várias fontes de dados são usadas (*por exemplo*, temperatura e consumo), devemos garantir que não haja problemas de sincronização de horas entre elas. Isso significa que esse tempo de saudação diferença entre o carimbo de hora Olá coletado de fontes de dados independentes dois não deve exceder mais de 10 segundos.
* **Latência** - como discutido acima, em **Ingestão de Dados**, dependemos de um fluxo de dados e de um processo de ingestão confiáveis. toocontrol que devemos garantir que podemos controlar a latência de dados de saudação. Isso é especificado como a diferença de tempo de saudação entre o tempo de saudação medida real Olá foi feita e a hora de saudação em que ele foi carregado no hello armazenamento Cortana Intelligence Suite e está pronto para uso. Para carga de curto prazo previsão latência total de saudação não deve ser maior que 30 minutos. Para carga de longo prazo previsão latência total de saudação não deve ser maior que 1 dia.

### <a name="data-preparation-and-feature-engineering"></a>Preparação de dados e engenharia de recursos
Depois que os dados brutos Olá foram incluídos (consulte **ingestão de dados**) e tem sido com segurança armazenados, é toobe pronto processado. Olá fase de preparação de dados é basicamente colocar dados brutos hello e convertendo (transformar, remodelar) em um formulário para Olá fase de modelagem. Que pode incluir operações simples, como o uso de coluna de dados brutos Olá porque está com seu valor de medida real, valores padronizados, operações mais complexas, como [intervalo de tempo](https://en.wikipedia.org/wiki/Lag_operator)e outros. Olá recém-criado colunas de dados são referidos tooas recursos de dados e o processo de Olá de gerar esses é chamado tooas engenharia de recurso. Por fim hello desse processo seria temos um novo conjunto de dados que é derivado dos dados brutos hello e podem ser usado para modelagem. Além disso, a fase de preparação de dados Olá precisa tootake respeito valores ausentes (consulte **de qualidade de dados**) além de compensá-los. Em alguns casos, também temos toonormalize Olá dados tooensure que todos os valores são representados no hello mesma escala.

Nesta seção, que listamos algumas Olá comuns de recursos de dados que estão incluídos no energia Olá demanda modelos de previsão.

**Controlado por recursos de tempo:** esses recursos são derivados de dados de carimbo de data/hora de saudação. Eles são extraídos e convertidos em recursos categóricos como:

* Hora do dia – isso é hora de saudação do dia de saudação que usa os valores da too23 0
* Dia da semana – isso representa Olá dia da semana hello e usa os valores de 1 (domingo) too7 (sábado)
* Dia do mês – isso representa a data real hello e pode ter valores de 1 too31
* Mês do ano – isso representa o mês de saudação e usa os valores de 1 (janeiro) too12 (dezembro)
* Semana – esse é um recurso de valor binário que usa valores de saudação de 0 para dias da semana ou 1 para final de semana
* Feriado - este é um recurso de valor binário que usa valores de saudação de 0 para um dia regular ou 1 para um feriado
* Termos de Fourier – Olá Fourier termos são pesos derivados de carimbo de hora hello e são usadas toocapture Olá periodicidade (ciclos) nos dados de saudação. Como podemos ter várias estações em nossos dados, talvez sejam necessários vários termos de Fourier. Por exemplo, os valores da demanda podem ter estações/ciclos anuais, semanais e diários, o que resultará em três termos de Fourier.

**Recursos de medição independente:** recursos independentes de saudação incluem todos os elementos de dados de saudação que gostaríamos toouse como previsões em nosso modelo. Aqui é excluir o recurso dependente de saudação que temos toopredict.

* Recurso de retardo – são deslocado de tempo valores de demanda real hello. Por exemplo, recursos de latência de 1 serão manter o valor de demanda de saudação em timestamp atual do toohello relativo Olá hora anterior (supondo que os dados por hora). Da mesma forma, podemos pode adicionar latência 2, 3, de latência *etc*. combinação real de saudação de recursos de latência que são usados são determinados durante a fase de modelagem de saudação pela avaliação de resultados do modelo hello.
* Tendências de longo prazo – esse recurso representa o crescimento linear Olá na demanda entre os anos.

**Recurso dependente:** recurso dependente Olá é a coluna de dados de saudação que gostaríamos toopredict nosso modelo. Com [supervisionado aprendizado de máquina](https://en.wikipedia.org/wiki/Supervised_learning), é preciso primeiro treinar o modelo de saudação usando os recursos dependentes da saudação (que também é chamado tooas rótulos). Isso permite que os padrões de Olá Olá modelo toolearn nos dados Olá associados ao recurso dependente hello. Na previsão de demanda de energia normalmente queremos demanda real do toopredict hello e, portanto, usaríamos-lo como um recurso dependente hello.

**Tratamento de valores ausentes:** durante a fase de preparação de dados hello, temos toodetermine Olá melhor estratégia toohandle valores ausentes. Isso é mais usando Olá várias estatísticas [métodos de imputação dados](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). No caso de saudação de previsão de demanda de energia, é normalmente imputar valores ausentes usando a média móvel anterior disponíveis dos pontos de dados.

**Normalização de dados:** normalização de dados é outro tipo de transformação que é usado toobring todos os dados numéricos, como a demanda de previsão em uma escala semelhante. Normalmente, isso ajuda a melhorar a precisão e a precisão do modelo hello. É normalmente faria isso pela divisão do valor real Olá por intervalo de saudação de dados saudação.
Isso dimensionará o valor original da saudação para baixo em um intervalo menor, normalmente entre -1 e 1.

## <a name="modeling"></a>Modelagem
Olá fase de modelagem é onde ocorre a conversão de saudação de Olá dados em um modelo. Em Olá core desse processo existe avançados algoritmos que examinar dados históricos da saudação (dados de treinamento), extrair padrões e criar um modelo. Esse modelo pode ser mais tarde toopredict usado em novos dados que não foi usado toobuild modelo de saudação.

Assim que tivermos um confiável de trabalho modelo é, em seguida, pode usá-lo tooscore novos dados que é estruturado tooinclude hello necessária recursos (X). Olá pontuação processo fará o uso de modelo persistente de saudação (objeto de fase de treinamento Olá) e prever a variável de destino de saudação que é indicado por Ŷ.

### <a name="demand-forecasting-modeling-techniques"></a>Técnicas de Modelagem da Previsão da Demanda
No caso de saudação de demanda previsão tornamos o uso de dados históricos ordenada por hora. Em geral, fazemos referência toodata que inclui a dimensão de tempo de saudação como [série temporal](https://en.wikipedia.org/wiki/Time_series). meta de saudação no tempo de modelagem de série é hora de toofind relacionada mostra as tendências, sazonalidade, autocorrelação (correlação ao longo do tempo) e formulá-los em um modelo.

Nos últimos anos algoritmos avançados foram desenvolvido tooaccommodate previsão de série de tempo e tooimprove precisão de previsão. Discutiremos brevemente alguns deles aqui.

> [!NOTE]
> Esta seção não é pretendido toobe usada como uma máquina de aprendizado e visão geral de previsão, mas em vez disso, como uma rápida pesquisa de modelagem técnicas que geralmente são usadas para previsão de demanda. Para obter mais informações e material educacional sobre a previsão de série de tempo, é altamente recomendável livros online Olá [previsão: princípios e práticas](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (Média de Movimentação)**](https://www.otexts.org/fpp/6/2)
Média móvel é uma saudação primeiro analíticos técnicas que foi usado para previsão de série de tempo e ainda é uma das técnicas de hello mais usada a partir de hoje. Também é foundation Olá para mais avançadas técnicas de previsão. Com a média móvel é são previsão próximo ponto de dados Olá pela média em pontos de Olá K mais recentes, em que K indica ordem de saudação do hello média móvel.

técnica de média móvel Olá tem Olá efeito de atenuação Olá previsão e, portanto, não pode tratar volatilidade bem grande em dados saudação.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (Suavização Exponencial)**](https://www.otexts.org/fpp/7/5)
Suavização exponencial (ETS) é uma família de vários métodos que usam a média ponderada dos pontos de dados recentes em ordem toopredict Olá próximo dados ponto. ideia Olá é pesos mais altos tooassign valores recente toomore e gradualmente diminuir esse peso para valores de medida mais antigos. Há vários métodos diferentes com esta família, algumas delas incluem tratamento de periodicidade nos dados hello como [método sazonais Terra Winters](https://www.otexts.org/fpp/7/5).

Alguns desses métodos também considerar periodicidade Olá dos dados de saudação.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (Média de Movimentação Integrada de Regressão Automática)**](https://www.otexts.org/fpp/8)
A Média de Movimentação Integrada de Regressão Automática (ARIMA) é outra família de métodos que é normalmente usada na previsão da série temporal. Ela praticamente combina métodos de regressão automática à média de movimentação. Métodos de regressão automática usam modelos de regressão Obtendo valores de série de tempo anterior em ordem toocompute Olá próximo data ponto. Métodos ARIMA também se aplicam a métodos diferenciais que incluem o cálculo Olá diferença entre pontos de dados e aqueles em vez do valor original medido da saudação. Por fim, ARIMA também usa Olá movendo médias técnicas que são discutidas acima. combinação de saudação de todos esses métodos de várias maneiras é que construções Olá família dos métodos ARIMA.

Atualmente, os métodos ETS e ARIMA são amplamente usados na previsão da demanda de energia e em muitos outros problemas de previsão. Em muitos casos eles são combinados toodeliver obter resultados muito precisos.

**Regressão múltipla geral** modelos de regressão podem ser mais importante abordagem de modelagem Olá no domínio de saudação do aprendizado de máquina e estatísticas. No contexto de saudação do MTS usamos valores futuros da regressão toopredict hello (*, por exemplo,*, de demanda). Regressão é faça uma combinação linear de previsões de saudação e aprenda pesos hello (também chamado tooas coeficientes) dessas previsões durante o processo de treinamento hello. meta de saudação é tooproduce uma linha de regressão que preveja nosso valor previsto. Métodos de regressão são adequados, quando a variável de destino Olá é numérico e, portanto, também se encaixa previsão de série de tempo. Há uma grande variedade de métodos de regressão, incluindo modelos de regressão muito simples, como a [Regressão Linear](https://en.wikipedia.org/wiki/Linear_regression), e mais avançados, como as árvores de decisão, as [Florestas Aleatórias](https://en.wikipedia.org/wiki/Random_forest), as [Redes Neurais](https://en.wikipedia.org/wiki/Artificial_neural_network) e as Árvores de Decisão Aumentadas.

Construir um problema de regressão de previsão de demanda de energia fornece uma grande flexibilidade na seleção de nossos recursos de dados que podem ser combinados de dados da série temporal demanda real hello e fatores externos, como a temperatura. Para obter mais informações sobre os recursos de saudação selecionado são discutidos em Olá engenharia de recurso (consulte **preparação de dados e de engenharia de recurso**) seção neste guia estratégico.

Nossa experiência com a implementação e implantação do piloto de previsões de demanda de energia, descobrimos que modelos de regressão avançadas que estão disponíveis no Azure ML hello tendem tooproduce Olá obter os melhores resultados e fazemos utilizá-las.

## <a name="model-evaluation"></a>Avaliação do modelo
Avaliação de modelo tem um papel fundamental em Olá **ciclo de desenvolvimento do modelo**. Nesta etapa, examinamos Validando o modelo hello e seu desempenho com dados reais. Durante a saudação modelagem etapa, usamos uma parte dos dados disponíveis Olá para treinar o modelo de saudação. Durante a fase de avaliação de saudação faremos restante Olá Olá tootest saudação do modelo de dados. Praticamente, isso significa que podemos são alimentar Olá novos dados de modelo que foi reestruturados e contém Olá mesmos recursos como o conjunto de dados de treinamento hello. No entanto, durante o processo de validação Olá, podemos usar variável de destino Olá modelo toopredict Olá em vez de fornecer Olá variável de destino disponíveis. Normalmente, nos referimos toothis processo como modelo de pontuação. Em seguida, usaríamos valores de destino true hello e compará-los com hello previsto aqueles. meta de saudação aqui é toomeasure e minimizar o erro de previsão hello, que significa que a diferença de saudação entre previsões hello e valor true hello. Quantificação de medição de erro de saudação é a chave, desde que deseja ajustar toofine modelo de saudação e validar se o erro hello, na verdade, está diminuindo. Modelo de ajuste fino Olá pode ser feito modificando os parâmetros de modelo que controlam o processo de aprendizado de hello, ou adicionando ou removendo recursos de dados (chamado tooas [varredura de parâmetros](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Praticamente, isso significa que podemos necessário tooiterate entre engenharia de recurso hello, modelagem e modelo várias vezes de fases de avaliação até que estamos tooreduce capaz de nível de toohello necessário de erro de saudação.

É importante tooemphasis erro de previsão Olá nunca serão zero quanto houver nunca é um modelo que perfeitamente pode prever cada resultado. No entanto, há uma magnitude determinada de erro que é aceitável pelos negócios hello. Durante o processo de validação hello, gostaríamos tooensure que nosso erro de previsão do modelo está no hello nível ou melhor do que a tolerância de negócios Olá nível. Portanto, é importante de nível de saudação tooset de erro tolerável de saudação no início de saudação do hello ciclo durante a saudação **problema formulação** fase.

### <a name="typical-evaluation-techniques"></a>Técnicas de Avaliação Típicas
Há várias maneiras nas quais o erro de previsão pode ser medido e quantificado. Nesta seção, vamos nos concentrar discussão Olá na série de tootime relevantes de técnicas de avaliação e em específico para previsão de demanda de energia.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE significa Erro Médio de Porcentagem Absoluta. Com MAPE nós são computando a diferença de saudação entre cada ponto previsto e o valor real de saudação desse ponto de. É, em seguida, quantificar erro Olá por ponto Calculando a proporção de saudação do valor real da saudação diferença toohello relativo. Na última etapa, fazemos a média desses valores. fórmula matemática Hello, usada para MAPE é seguir hello:

![Fórmula de MAPE](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*onde um<sub>t</sub> é o valor real do hello, F<sub>t</sub> é Olá valor previsto e n é Olá horizonte de previsão.*

## <a name="deployment"></a>Implantação
Depois que temos Olá fase de modelagem de configurar e validar o desempenho do modelo Olá estamos toogo pronto na fase de implantação de saudação. Nesse contexto, implantação significa habilitar cliente Olá tooconsume Olá modelo executando previsões reais nela em grande escala. conceito de saudação de implantação é a chave no Azure ML desde que a nossa meta principal é tooconstantly invocar previsões como toojust contrário Obtendo informações de saudação do dados saudação. fase de implantação Olá faz parte de saudação onde podemos habilitar Olá modelo toobe consumido em grande escala.

No contexto de saudação de previsão de demanda de energia, nossa meta é previsões contínuo e periódica de tooinvoke enquanto garante que os dados atualizados estão disponíveis para o modelo de saudação e que Olá previsto cliente consumo toohello voltar os dados são enviados.

### <a name="web-services-deployment"></a>Implantação de Serviços Web
Olá principal implantável bloco de construção no Azure ML é serviço de web de saudação. Isso é tooenable consumo de maneira mais eficaz Olá de um modelo de previsão em nuvem hello. Olá serviço Web encapsula o modelo de saudação e conclui com um [RESTful](http://www.restapitutorial.com/) API (Application Programming Interface). Olá API pode ser usado como parte de qualquer código de cliente, conforme ilustrado no diagrama de saudação abaixo.

![Implantação e Consumo do Serviço Web](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Como pode ser visto, serviço web de saudação é implantado em Olá nuvem do pacote de inteligência de Cortana e pode ser chamado em seu ponto de extremidade de API REST exposto. Tipos diferentes de clientes em vários domínios podem invocar serviço Olá por meio de saudação API da Web simultaneamente. serviço web de saudação também pode ser dimensionados para dar suporte a milhares de chamadas simultâneas.

### <a name="a-typical-solution-architecture"></a>Uma Arquitetura de Solução Típica
Ao implantar uma demanda de energia a previsão da solução, estamos interessados na implantação de uma solução de tooend final que vai além do serviço de web de previsão hello e facilita o fluxo de dados inteiro de saudação. Em tempo de saudação que invocamos uma nova previsão, precisaremos toomake-se de que o modelo Olá é alimentado com os recursos de dados atualizados. Que implica que Olá recentemente coletados dados brutos é constantemente incluídos, processados e transformados em conjunto no qual modelo Olá foi criado de recursos necessários de saudação. AT Olá mesmo tempo, podemos gostariam de ter toomake Olá previsto dados disponíveis para Olá terminar o consumo de clientes. Um exemplo dados ciclo de fluxo (ou pipeline de dados) é ilustrado no diagrama de saudação abaixo:

![Previsão de demanda de energia tooEnd final de fluxo de dados](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Estas são as etapas de saudação que acontecem como parte do ciclo de previsão Olá energia demanda:

1. Milhões de medidores de dados implantados estão constantemente gerando dados de consumo de energia em tempo real.
2. Esses dados estão sendo coletados e carregados em um repositório da nuvem (*por exemplo*, o Blob do Azure).
3. Antes de ser processada, dados brutos de saudação são Subestação tooa agregados ou nível regional conforme definido pelos negócios hello.
4. processamento de recurso da saudação (consulte **preparação de dados e o recurso de processamento**), em seguida, é realizada e o modelo de dados de saudação de produz que é necessários para treinamento ou pontuação – Olá recurso conjunto de dados são armazenados em um banco de dados (*, por exemplo,*, Do SQL Azure).
5. Olá novo treinamento de serviço é chamado hello toore treinar modelo – versão atualizada do modelo de saudação de previsão é persistido para que ele pode ser usado por Olá pontuação serviço da web.
6. Olá pontuação serviço web é chamado em uma agenda que se ajusta a frequência de previsão Olá necessário.
7. Olá previsto dados são armazenados em um banco de dados que pode ser acessado pelo cliente de consumo de término hello.
8. Olá consumo cliente recupera previsões hello, aplica-se novamente na grade de saudação e consome conforme o caso de uso de saudação necessário.

É importante toonote que todo o ciclo é totalmente automatizada e executado em uma agenda. orquestração de inteiro Olá desse ciclo de dados pode ser feita usando ferramentas como [do Azure Data Factory](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>Encerrar tooEnd arquitetura de implantação
Em ordem toopractically implantar uma solução de previsão de demanda de energia inteligência Cortana, precisamos tooensure que os componentes de Olá necessárias são estabelecidas e configurados corretamente.

Olá diagrama a seguir ilustra uma arquitetura de inteligência Cortana com base comum que implementa e orquestra Olá ciclo de fluxo de dados que é descrito acima:

![Encerrar tooEnd arquitetura de implantação](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Para obter mais informações sobre cada um dos componentes de saudação e arquitetura inteira Olá consulte toohello modelo de solução de energia.

