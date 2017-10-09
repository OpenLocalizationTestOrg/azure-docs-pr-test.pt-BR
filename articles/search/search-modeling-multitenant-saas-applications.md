---
title: "aaaModeling multilocação na pesquisa do Azure | Microsoft Docs"
description: "Saiba mais sobre padrões de design comuns para aplicativos SaaS multilocatários ao usar o Azure Search."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Padrões de design para aplicativos SaaS multilocatários e Azure Search
Um aplicativo multilocatário é aquele que fornece Olá mesmo número de tooany de serviços e recursos de locatários que não pode ver ou compartilhar dados de saudação de nenhum outro locatário. Este documento discute estratégias de isolamento de locatário para aplicativos multilocatários criados com o Azure Search.

## <a name="azure-search-concepts"></a>Conceitos do Azure Search
Como uma solução de pesquisa como um serviço, a pesquisa do Azure permite experiências de pesquisa avançada do desenvolvedores tooadd tooapplications sem nenhuma infraestrutura de gerenciamento ou se tornar um especialista em pesquisa. Os dados são carregados toohello serviço e, em seguida, são armazenados na nuvem hello. Usando solicitações simples toohello API de pesquisa do Azure, dados saudação podem ser modificados e pesquisados. Uma visão geral do serviço de saudação pode ser encontrada no [neste artigo](http://aka.ms/whatisazsearch). Antes de discutir sobre padrões de design, é importante toounderstand alguns conceitos na pesquisa do Azure.

### <a name="search-services-indexes-fields-and-documents"></a>Serviços de pesquisa, índices, campos e documentos
Ao usar a pesquisa do Azure, um assina tooa *serviço de pesquisa*. Os dados são carregado tooAzure pesquisa, são armazenados em um *índice* no serviço de pesquisa de saudação. Pode haver um número de índices em um único serviço. conceitos familiares de saudação de toouse de bancos de dados, o serviço de pesquisa Olá pode ser comparado tooa banco de dados enquanto os índices de saudação dentro de um serviço podem ser comparadas tootables dentro de um banco de dados.

Cada índice dentro de um serviço de pesquisa tem seu próprio esquema, que é definido por um número de *campos*personalizáveis. Os dados serão adicionados tooan índice de pesquisa do Azure no formulário de saudação do indivíduo *documentos*. Cada documento deve ser carregado tooa determinado índice e deve se ajustar o esquema do índice. Ao pesquisar dados usando a pesquisa do Azure, as consultas de pesquisa de texto completo de saudação são emitidas em relação a um índice específico.  toocompare toothose esses conceitos de banco de dados, os campos podem ser comparadas toocolumns em uma tabela e os documentos podem ser comparadas toorows.

### <a name="scalability"></a>Escalabilidade
Qualquer serviço de pesquisa do Azure na saudação padrão [preço](https://azure.microsoft.com/pricing/details/search/) pode aumentar em duas dimensões: armazenamento e disponibilidade.

* *Partições* podem ser adicionados como armazenamento de saudação tooincrease de um serviço de pesquisa.
* *Réplicas* podem ser adicionados a taxa de transferência do tooa serviço tooincrease Olá de solicitações que um serviço de pesquisa pode manipular.

Adicionando e removendo partições e réplicas em permitirá que a capacidade de saudação do toogrow de serviço de pesquisa Olá com valor de saudação de dados e o tráfego demandas de aplicativo hello. Em ordem para um tooachieve de serviço de pesquisa uma leitura [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), ele requer duas réplicas. Em ordem para um serviço tooachieve uma leitura-gravação [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), ele requer três réplicas.

### <a name="service-and-index-limits-in-azure-search"></a>Limites de serviço e índice no Azure Search
Existem alguns diferentes [camadas de preços](https://azure.microsoft.com/pricing/details/search/) na pesquisa do Azure, cada uma das camadas de saudação tem diferentes [limites e cotas](search-limits-quotas-capacity.md). Alguns desses limites são a saudação de nível de serviço, alguns estão no nível de índice hello e alguns estão no nível de partição hello.

|  | Basic | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Máximo de réplicas por serviço |3 |12 |12 |12 |12 |
| Máximo de partições por serviço |1 |12 |12 |12 |1 |
| Máximo de unidades de pesquisa (réplicas * partições) por serviço |3 |36 |36 |36 |36 (máx. de 3 partições) |
| Máximo de documentos por serviço |1 milhão |180 milhões |720 milhões |1.4 bilhão |600 milhões |
| Armazenamento máximo por serviço |2 GB |300 GB |1,2 TB |2,4 TB |600 GB |
| Máximo de documentos por partição |1 milhão |15 milhões |60 milhões |120 milhões |200 milhões |
| Armazenamento máximo por partição |2 GB |25 GB |100 GB |200 GB |200 GB |
| Índices máximos por serviço |5 |50 |200 |200 |3000 (máx. de 1000 índices/partição) |

#### <a name="s3-high-density"></a>Alta densidade S3
Na camada de preços de S3 da pesquisa do Azure, há uma opção para o modo de alta densidade (HD) Olá projetado especificamente para cenários multilocatários. Em muitos casos, é necessário toosupport um grande número de locatários menores em benefícios de Olá de tooachieve um único serviço de simplicidade e redução de custos.

S3 HD permite Olá muitos toobe de índices pequenos compactados em gerenciamento de saudação de um serviço de pesquisa único pelo comerciais Olá capacidade tooscale out índices usando partições para Olá capacidade toohost mais índices em um único serviço.

Concretamente, um serviço S3 poderia ter entre 1 e 200 índices que juntos podem hospedar documentos bilhões too1.4. Um HD S3 em Olá outro lado permitiria índices individuais tooonly subir too1 milhões de documentos, mas ele pode tratar dos índices de too1000 por partição (backup too3000 por serviço) com uma contagem de documento total de 200 milhões por partição (backup too600 milhões por serviço).

## <a name="considerations-for-multitenant-applications"></a>Considerações para aplicativos multilocatários
Aplicativos multilocatários devem distribuir de forma eficiente recursos entre locatários Olá preservando algum nível de privacidade entre hello vários locatários. Há algumas considerações ao criar a arquitetura de saudação para esse aplicativo:

* *Isolamento de locatários:* os desenvolvedores de aplicativos precisam tootake medidas apropriadas tooensure que nenhum locatários tem não autorizado ou indesejado toohello de acessar dados de outros locatários. Além da perspectiva de saudação de privacidade de dados, estratégias de isolamento de locatário exigem o gerenciamento eficaz de recursos compartilhados e a proteção de vizinhos com ruídos.
* *Custo de recursos de nuvem:* como com qualquer outro aplicativo, as soluções de software devem permanecer competitivas em termos de custo como um componente de um aplicativo multilocatário.
* *Facilidade de operações:* ao desenvolver uma arquitetura de multilocatária, Olá impacto nas operações do aplicativo hello e complexidade é uma consideração importante. O Azure Search tem um [SLA de 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Espaço global:* aplicativos Multilocatários talvez seja necessário tooeffectively sirvam locatários que são distribuídos entre globo hello.
* *Escalabilidade:* os desenvolvedores de aplicativos precisam tooconsider como eles reconciliam entre manter um nível de complexidade do aplicativo suficientemente baixo e criando Olá aplicativo tooscale com número de locatários e Olá tamanho dos dados de locatários e carga de trabalho.

A pesquisa do Azure oferece alguns limites que podem ser usados tooisolate locatários dados e carga de trabalho.

## <a name="modeling-multitenancy-with-azure-search"></a>Modelagem de multilocação com o Azure Search
No caso de saudação de um cenário de multilocatário, o desenvolvedor do aplicativo hello consome um ou mais serviços de pesquisa e dividir seus locatários entre serviços, índices ou ambos. O Azure Search tem alguns padrões comuns ao modelar um cenário de multilocatário:

1. *Índice por locatário:* cada locatário tem seu próprio índice dentro de um serviço de pesquisa que é compartilhado com outros locatários.
2. *Serviço por locatário:* cada locatário tem seu próprio serviço do Azure Search dedicado, oferecendo o nível mais alto de separação de dados e a carga de trabalho.
3. *Mistura de ambos:* locatários maiores e mais ativos são atribuídos a serviços dedicados enquanto locatários menores são atribuídos a índices individuais dentro de serviços compartilhados.

## <a name="1-index-per-tenant"></a>1. Indexar por locatário
![Um portrayal de modelo de índice por locatário Olá](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

Em um modelo de índice por locatário, vários locatários ocupam um único serviço do Azure Search, em que cada locatário tem seu próprio índice.

Locatários atingem o isolamento de dados porque todas as solicitações de pesquisa e operações de documento são emitidas em um nível de índice no Azure Search. Na camada de aplicativo hello, não há reconhecimento de necessidade de saudação toodirect Olá índices adequados de toohello de tráfego de vários locatários ao também gerenciar recursos no nível de serviço Olá entre todos os locatários.

Um atributo de chave do modelo de índice por locatário Olá é a capacidade de Olá Olá aplicativo developer toooversubscribe Olá capacidade de um serviço de pesquisa entre locatários do aplicativo hello. Se locatários Olá têm uma distribuição irregular de carga de trabalho, a combinação ideal de saudação de locatários pode ser distribuídos em um serviço de pesquisa índices tooaccommodate um número de locatários altamente ativos, uso intensivo de recursos ao servir simultaneamente uma cauda longa de locatários menos ativos. compensação de saudação é a incapacidade de saudação toohandle situações Olá modelo onde cada locatário simultaneamente é altamente ativo.

modelo de índice por locatário Olá fornece a base de saudação para um modelo de variável de custo, em que um serviço de pesquisa do Azure inteiro é comprou inicial e subsequentemente preenchido com locatários. Isso possibilita a capacidade não utilizada toobe designado para as avaliações e as contas gratuitas.

Para aplicativos com um espaço global, modelo de índice por locatário Olá pode não ser hello mais eficiente. Se locatários do aplicativo são distribuídos globo hello, um serviço separado pode ser necessário para cada região que pode duplicar os custos em cada um deles.

Pesquisa do Azure permite a escala de saudação de índices individuais hello e o número total de saudação do toogrow de índices. Se um preço apropriado camada for escolhido, partições e réplicas podem ser adicionadas a serviço de pesquisa inteira toohello quando um índice individual no serviço Olá ficar muito grande em termos de armazenamento ou o tráfego.

Se o número total de saudação de índices aumenta muito grande para um único serviço, o outro serviço tem tooaccommodate toobe provisionado Olá novos locatários. Se os índices têm toobe movido entre serviços de pesquisa à medida que são adicionados novos serviços, dados de saudação do índice de saudação tem toobe copiado manualmente um índice toohello outros como pesquisa do Azure não permite uma toobe índice movido.

## <a name="2-service-per-tenant"></a>2. Serviço por locatário
![Um portrayal de modelo de serviço por locatário Olá](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

Em uma arquitetura de serviço por locatário, cada locatário tem seu próprio serviço de pesquisa.

Nesse modelo, o aplicativo hello atinge o nível máximo de isolamento para seus locatários hello. Cada serviço tem armazenamento dedicado e taxa de transferência para lidar com solicitação de pesquisa, bem como chaves de API separadas.

Para aplicativos em que cada locatário tem um volume grande ou carga de trabalho Olá tem pouca variação de locatário tootenant, o modelo de serviço por locatário Olá é uma opção adequada como recursos não são compartilhados entre as cargas de trabalho de vários locatários.

Um serviço de acordo com o modelo de locatário também oferece o benefício de saudação de um modelo de custo fixo e previsível. Não há nenhum investimento inicial em um serviço de pesquisa inteira até que haja um locatário toofill, porém Olá custo por locatário for maior do que um modelo de índice por locatário.

modelo de serviço por locatário Olá é uma opção eficiente para aplicativos com um espaço global. Com locatários geograficamente distribuídas, é fácil toohave serviço cada locatário na região apropriada hello.

os desafios de Olá na expansão deste padrão surgir quando locatários individuais mais atender o crescimento seu serviço. A pesquisa do Azure atualmente não dá suporte para atualização Olá preço de um serviço de pesquisa, para que todos os dados teria toobe copiado manualmente tooa novo serviço.

## <a name="3-mixing-both-models"></a>3. Combinação dos dois modelos
Outro padrão para modelar a multilocação é misturar estratégias de índice por locatário e de serviço por locatário.

Misturando padrões Olá dois, locatários maior de um aplicativo podem ocupar serviços dedicados enquanto Olá longa parte final do menos locatários ativos, menores pode ocupar índices em um serviço compartilhado. Esse modelo garante que locatários maior Olá consistentemente alto desempenho do serviço de saudação enquanto ajuda tooprotect Olá locatários menores de qualquer vizinhos com ruídos.

No entanto, implementar essa estratégia depende da antecipação para prever quais locatários exigirão um serviço dedicado em vez de um índice em um serviço compartilhado. Complexidade de aplicativo aumenta com hello necessidade toomanage dois desses modelos de multilocação.

## <a name="achieving-even-finer-granularity"></a>Como obter granularidade ainda maior
Olá acima cenários multilocatário de toomodel do padrões de design na pesquisa do Azure suponha um escopo uniforme, onde cada locatário é toda a instância de um aplicativo. No entanto, às vezes, os aplicativos podem manipular vários escopos menores.

Se os modelos de serviço por locatário e índice por locatário não forem suficientemente pequenos escopos, é possível toomodel tooachieve um índice um grau de granularidade até mesmo mais detalhado.

toohave um único índice se comportam de forma diferente para pontos de extremidade de cliente diferentes, um campo pode ser índice tooan adicionado, que designa um determinado valor para cada cliente possíveis. Cada vez que um cliente chama tooquery de pesquisa do Azure ou modificar um índice, código de saudação do aplicativo de cliente hello Especifica valor apropriado de saudação para esse campo usando a pesquisa do Azure [filtro](https://msdn.microsoft.com/library/azure/dn798921.aspx) recurso no momento da consulta.

Esse método pode ser usado tooachieve funcionalidade de contas de usuário separadas, níveis de permissão separados e aplicativos até mesmo completamente separados.

> [!NOTE]
> Usando a abordagem de saudação descrita acima tooconfigure tooserve um único índice vários locatários afeta Olá de relevância de resultados da pesquisa. Pontuações de relevância da pesquisa são calculadas em um escopo de nível de índice, não é um escopo de nível de locatário, para que os dados de todos os locatários são incorporados na estatísticas subjacentes de pontuações de relevância hello, como a frequência do termo.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Pesquisa do Azure é uma opção atraente para muitos aplicativos, [Leia mais sobre recursos avançados do serviço Olá](http://aka.ms/whatisazsearch). Quando avaliar Olá vários padrões para aplicativos multilocatários de design, considere Olá [várias camadas de preços](https://azure.microsoft.com/pricing/details/search/) e hello respectivo [limites de serviço](search-limits-quotas-capacity.md) toobest personalizar toofit de pesquisa do Azure arquiteturas de todos os tamanhos e cargas de trabalho do aplicativo.

Dúvidas sobre cenários de multilocatários e de pesquisa do Azure podem ser direcionadas tooazuresearch_contact@microsoft.com.

