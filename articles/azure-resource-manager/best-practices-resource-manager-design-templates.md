---
title: "aaaDesign Azure modelos para soluções complexas | Microsoft Docs"
description: "Mostra as práticas recomendadas para criação de modelos do Azure Resource Manager para cenários complexos"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Padrões de design para modelos do Azure Resource Manager ao implantar soluções complexas
Usando uma abordagem flexível com base em modelos do Azure Resource Manager, você pode implantar topologias complexas de forma rápida e consistente. Você pode adaptar essas implantações facilmente como principais ofertas evoluem ou tooaccommodate variantes para cenários de exceção ou clientes.

Este tópico faz parte de um whitepaper mais amplo. baixar tooread Olá completo papel, [World classe Azure Resource Manager modelos considerações e práticas comprovadas](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Modelos de combinam benefícios Olá Olá subjacente do Azure Resource Manager com capacidade de adaptação hello e facilitar a leitura do objeto notação JSON (JavaScript). Usando modelos, você pode:

* Implantar consistentemente topologias e suas cargas de trabalho.
* Gerencie todos os seus recursos em um aplicativo coletivamente usando grupos de recursos.
* Aplica serviços, grupos e acesso baseado em função (RBAC) controle toogrant acesso apropriado toousers.
* Use tarefas de toostreamline associações marcação, como pacotes cumulativos de cobrança.

Este artigo fornece detalhes sobre cenários de consumo, arquitetura e padrões de implementação identificados durante nossas sessões de design e implementações de modelos do mundo real com os clientes da AzureCAT (Azure Customer Advisory Team). Distantes acadêmica, essas abordagens são práticas comprovadas, informadas por desenvolvimento Olá dos modelos de 12 das tecnologias principais sistemas operacionais baseados em Linux de hello, incluindo: Kafka Apache, Apache Spark, Cloudera, Couchbase, Hortonworks HDP, Enterprise DataStax da plataforma Apache Cassandra, Elasticsearch, Jenkins, MongoDB, PostgreSQL, Redis e Nagios. 

Este artigo compartilha essas toohelp práticas comprovadas projetar modelos de Gerenciador de recursos do Azure de classe mundial.  

Em nosso trabalho com clientes, identificamos várias experiências de consumo de modelos do Resource Manager entre empresas, SIs (integradores de sistemas) e CSVs (fornecedores de serviço de nuvem). Olá seções a seguir fornecem uma visão geral de cenários e padrões comuns para diferentes tipos de clientes.

## <a name="enterprises-and-system-integrators"></a>Empresas e integradores de sistemas
Em grandes organizações, normalmente observamos dois consumidores de modelos do Azure Resource Manager: as equipes de desenvolvimento interno de software e o TI empresarial. Descobrimos que os cenários de saudação do Olá SIs mapeiam toohello cenários para empresas, portanto Olá mesmas considerações se aplicam.

### <a name="internal-software-development-teams"></a>Equipes de desenvolvimento interno de software
Se sua equipe desenvolve software toosupport seu negócio, modelos fornecem uma maneira fácil tooquickly implantar tecnologias para uso em soluções comerciais específicas. Você também pode usar modelos toorapidly criar ambientes de treinamento que habilitam as habilidades necessárias de toogain de membros de equipe.

Você pode usar modelos como-é estender ou integrá-las tooaccommodate suas necessidades. Usando marcação nos modelos, você pode fornecer um resumo de cobrança com várias exibições, como equipe, projeto, indivíduo e educação.

As empresas geralmente deseja equipes de desenvolvimento de software toocreate um modelo de implantação consistente de uma solução. modelo de saudação facilita restrições para que determinados itens dentro desse ambiente permanecem fixos e não podem ser substituídos. Por exemplo, um banco pode exigir um modelo tooinclude RBAC para um programador não é possível revisar uma solução toosend conta de armazenamento pessoal de tooa de dados.

### <a name="corporate-it"></a>TI Empresarial
As organizações de TI empresarial normalmente usam modelos para fornecer capacidade de nuvem e recursos hospedados na nuvem.

#### <a name="cloud-capacity"></a>Capacidade de nuvem
É uma maneira comum para corporativa IT grupos tooprovide capacidade da nuvem para equipes com "tamanhos camisa", que são padrão oferta tamanhos como pequeno, médio e grande. ofertas de camisa dimensionado Olá podem misturar tipos diferentes de recursos e quantidades oferecendo um nível de padronização que torna possível toouse modelos. modelos de saudação oferecem a capacidade de uma maneira consistente que impõe políticas corporativas e usa a marcação tooprovide estorno tooconsuming organizações.

Por exemplo, talvez seja necessário tooprovide desenvolvimento, teste ou ambientes de produção no qual Olá equipes de desenvolvimento de software podem implantar suas soluções. ambiente Olá com uma topologia de rede predefinidas e elementos que Olá equipes de desenvolvimento de software não é possível alterar, como regras que regem o acesso toohello públicos na internet e pacote inspeção. Você também pode ter funções específicas da organização para esses ambientes com direitos de acesso distintos para o ambiente de saudação.

#### <a name="cloud-hosted-capabilities"></a>Recursos hospedados na nuvem
Você pode usar modelos toosupport hospedados em nuvem recursos, incluindo pacotes de software individuais ou ofertas compostas que são oferecidas toointernal linhas de negócios. Um exemplo de uma oferta composta seria análise como serviço - análise, visualização e outras tecnologias - entregue em uma configuração otimizada e conectada, em uma topologia de rede predefinida.

Recursos hospedados em nuvem são afetados por Olá função considerações sobre segurança e estabelecido pela capacidade da nuvem Olá oferta em que sejam criados. Esses recursos são oferecidos como são ou como um serviço gerenciado. Olá último, funções de restrição de acesso são obrigatórias acesso tooenable no ambiente de saudação para fins de gerenciamento.

## <a name="cloud-service-vendors"></a>Fornecedores de serviço de nuvem
Depois de falar toomany CSVs, identificamos várias abordagens que você pode executar serviços toodeploy para seus clientes e os requisitos associados.

### <a name="csv-hosted-offering"></a>Oferta hospedada em CSV
Se você hospeda sua oferta em sua própria assinatura do Azure, há duas abordagens de hospedagem comuns: uma implantação distinta para cada cliente ou então a implantação de unidades de escala, que são a base de uma infraestrutura compartilhada usada para todos os clientes.

* **Implantações distintas para cada cliente.** Implantações distintas para cada cliente exigem topologias fixas de diferentes configurações conhecidas. Essas implantações podem ter diferentes tamanhos de VM (máquina virtual), números variados de nós e quantidades diferentes de armazenamento associado. A marcação de implantações é usada para cobrança de valores acumulados de cada cliente. RBAC pode ser habilitado tooallow clientes acesso tooaspects do ambiente de nuvem.
* **Unidades de escala em ambientes multilocatário compartilhados.** Um modelo pode representar uma unidade de escala para ambientes multilocatário. Nesse caso, Olá mesma infraestrutura é toosupport usado em todos os clientes. implantações de saudação representam um grupo de recursos que fornecem um nível de capacidade para Olá hospedado oferta, como o número de usuários e o número de transações. Essas unidades de escala são aumentadas ou reduzidas conforme a demanda.

### <a name="csv-offering-injected-into-customer-subscription"></a>Oferta de CSV introduzida na assinatura do cliente
Talvez você queira toodeploy o software em assinaturas pertencentes a clientes finais. Você pode usar implantações distintas do toodeploy modelos em uma conta de cliente do Azure.

Essas implantações usam RBAC, portanto, você pode atualizar e gerenciar a implantação de saudação em conta saudação do cliente.

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise e vender suas ofertas por meio de um mercado, como o Azure Marketplace, você pode desenvolver modelos toodeliver diferentes tipos de implantações que são executados em uma conta de cliente do Azure. Essas implantações distintas normalmente podem ser descritas como um tamanho de camiseta (pequeno, médio, grande), tipo de produto/público (community, developer, enterprise) ou tipo de recurso (básico, de alta disponibilidade).  Em alguns casos, esses tipos permitem que você toospecify determinados atributos de implantação de saudação, como tipo VM ou o número de discos.

## <a name="oss-projects"></a>Projetos de software livre
Dentro de projetos de código-fonte aberto, modelos do Gerenciador de recursos permitem uma comunidade toodeploy uma solução rapidamente usando práticas comprovadas. Você pode armazenar modelos em um repositório do GitHub para que comunidade Olá poderá revisá-los ao longo do tempo. Os usuários implantam esses modelos em suas próprias assinaturas do Azure.

Olá seções a seguir identificam coisas Olá precisar tooconsider antes de projetar sua solução.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Identificando o que está fora e o que está dentro de uma VM
Como criar seu modelo, é útil toolook requisitos Olá em termos de novidades externas e internas Olá máquinas de virtuais (VMs):

* Fora significa Olá VMs e outros recursos de sua implantação, como a topologia de rede hello, marcação, os segredos da certificados referências toohello e controle de acesso baseado em função. Todos esses recursos fazem parte do seu modelo.
* Configuração de estado significa dentro hello software instalado e geral desejado. Outros mecanismos, como scripts ou extensões de VM, são usados no todo ou em parte. Esses mecanismos podem ser identificados e executados pelo modelo hello, mas não nele.

Exemplos comuns de atividades "dentro da caixa hello" inclua-  

* Instalar ou remover recursos e funções de servidor
* Instalar e configurar o software no nível de cluster ou nó de saudação
* Implantar sites em um servidor Web
* Implantar esquemas de banco de dados
* Gerenciar o Registro ou outros tipos de configurações
* Gerenciar arquivos e diretórios
* Iniciar, parar e gerenciar processos e serviços
* Gerenciar contas de usuário e grupos locais
* Instalar e gerenciar pacotes (. msi, .exe, yum, etc.)
* Gerenciar variáveis de ambiente
* Executar scripts nativos (Windows PowerShell, bash, etc.)

### <a name="desired-state-configuration-dsc"></a>Configuração de estado desejado (DSC)
Pensar sobre o estado interno de saudação de suas VMs além da implantação, você deseja toomake-se de que essa implantação não "descompasso" da configuração de saudação que você definiu e verificados no controle de origem. Essa abordagem garante que os desenvolvedores ou equipe de operações não faça o ambiente de tooan de alterações ad hoc que não são verificadas, testado ou registrados no controle de origem. Esse controle é importante, porque alterações manuais Olá não estão no controle de origem. Eles também não são parte da implantação padrão da saudação e terá impacto sobre futuras implantações automatizadas de software hello.

Além de seus funcionários internos, a configuração de estado desejado também é importante segundo uma perspectiva de segurança. Hackers regularmente estão tentando toocompromise e exploram os sistemas de software. Quando obtiver êxito, ele é arquivos tooinstall comuns e alterar estado de saudação de um sistema comprometido. Usando a configuração de estado desejado, você pode identificar deltas entre hello desejado e o estado real e restaurar uma configuração conhecida.

Existem extensões de recurso hello mais populares mecanismos para DSC - PowerShell DSC, Chef e Puppet. Cada uma dessas extensões pode implantar o estado inicial de saudação da VM e também ser usada toomake se Olá desejado de estado é mantido.

## <a name="common-template-scopes"></a>Escopos de modelo comuns
Em nossa experiência, vimos três escopos principais de modelos de solução surgirem. Esses três escopos – capacidade, a funcionalidade e solução de ponta a ponta – são descritos na Olá seções a seguir.

### <a name="capacity-scope"></a>Escopo de capacidade
Um escopo de capacidade fornece um conjunto de recursos em uma topologia padrão que é pré-configurado toobe em conformidade com regulamentos e políticas. exemplo mais comum de saudação está implantando um ambiente de desenvolvimento padrão em um cenário de TI da empresa ou SI.

### <a name="capability-scope"></a>Escopo de funcionalidade
Um escopo de funcionalidade concentra-se em como implantar e configurar uma topologia para uma determinada tecnologia. Cenários comuns, incluindo tecnologias como SQL Server, Cassandra, Hadoop.

### <a name="end-to-end-solution-scope"></a>Escopo da solução de ponta a ponta
Um escopo de solução de ponta a ponta é direcionado além de um único recurso e em vez disso, orientado para fornecer uma solução de tooend final composta de vários recursos.  

Um escopo de modelo com escopo de solução se manifesta como um conjunto de um ou mais modelos com escopo de funcionalidade com recursos, lógica e estado desejado específicos da solução. Um exemplo de um modelo no escopo de solução é um modelo de solução final tooend dados pipeline. modelo Olá pode misturar topologia de solução específica e estado com vários modelos de solução no escopo do recurso como Kafka, tempestade e Hadoop.

## <a name="choosing-free-form-vs-known-configurations"></a>Escolhendo entre configurações de forma livre e configurações conhecidas
Você pode pensar inicialmente um modelo deve fornecer aos clientes flexibilidade máxima hello, mas muitas considerações afetam a opção de saudação de configurações de forma livre toouse versus configurações conhecidas. Esta seção identifica Olá principais necessidades do cliente e considerações técnicas que formatada abordagem Olá compartilhada neste documento.

### <a name="free-form-configurations"></a>Configurações de forma livre
Na superfície de hello, configurações de forma livre de som ideais. Eles permitem tooselect um tipo VM e fornecer um número arbitrário de nós e discos para os nós conectados — e fazê-lo como modelo de tooa de parâmetros. No entanto, essa abordagem não é ideal para alguns cenários.

Em [tamanhos das máquinas virtuais](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), Olá diferentes tipos VM e tamanhos disponíveis são identificados, e cada número de saudação do durável discos (2, 4, 8, 16 ou 32) que podem ser anexados. Cada disco conectado fornece 500 IOPS e múltiplos desses discos podem ser agrupados (pooling) para se obter um multiplicador desse número de IOPS. Por exemplo, 16 discos pode ser agrupada tooprovide 8.000 IOPS. O pool é feito com a configuração no sistema de operacional hello, usando espaços de armazenamento do Microsoft Windows ou matriz redundante de discos independentes (RAID) no Linux.

Uma configuração de forma livre permite Olá seleção várias instâncias VM, VM vários tipos e tamanhos para essas instâncias, vários discos para Olá tipo VM, e um ou mais scripts tooconfigure conteúdo VM de saudação.

É comum que uma implantação tenha vários tipos de nós, como nós mestres e de dados; portanto, essa flexibilidade geralmente é fornecida para todos os tipos de nó.

Conforme você começa a clusters toodeploy qualquer significativo, começar toowork com esses cenários complexos. Se você foram Implantando um cluster Hadoop, por exemplo, com 8 nós mestres e nós de 200 dados e em pool 4 discos anexados em cada nó mestre e em pool 16 discos anexados por nó de dados, você teria 208 VMs e 3,232 discos toomanage.

Uma conta de armazenamento será acelerador solicitações acima que seu 20.000 identificado transações/segundo limite, para que você deve examinar o particionamento de conta de armazenamento e usar cálculos número apropriado de saudação de toodetermine de armazenamento contas tooaccommodate esta topologia. Considerando várias Olá combinações com suporte pela abordagem de forma livre hello, cálculos dinâmicos são toodetermine necessário Olá particionamento apropriadas. saudação de linguagem de modelo do Gerenciador de recursos do Azure não oferece atualmente funções matemáticas, portanto, você deve executar esses cálculos no código, gerar um modelo exclusivo, codificada com detalhes apropriados hello.

Em cenários de SI e TI empresarial, alguém deve manter Olá modelos e suporte a topologias Olá implantado para organizações de um ou mais. Essa sobrecarga adicional - diferentes configurações e modelos para cada cliente - está longe de ser desejável.

Você pode usar esses ambientes de toodeploy modelos na assinatura do Azure do cliente, mas as equipes de TI corporativos e CSVs normalmente implantação-los em suas próprias assinaturas, usando um toobill de função de estorno seus clientes. Nesses cenários, o objetivo de saudação é toodeploy capacidade para vários clientes em um pool de assinaturas e implantações de manter densamente populadas no hello assinaturas toominimize assinatura proliferação — ou seja, mais toomanage de assinaturas. Com tamanhos de implantação verdadeiramente dinâmico para alcançar esse tipo de densidade requer um planejamento cuidadoso e desenvolvimento adicional para o trabalho de estrutura em nome da organização hello.

Além disso, você não pode criar assinaturas por meio de uma chamada de API, mas deve fazê-lo manualmente por meio do portal hello. Conforme aumenta o número Olá de assinaturas, qualquer acúmulo assinatura resultante requer intervenção humana, ele não pode ser automatizado. Com grande variabilidade em tamanhos de saudação de implantações, você teria toopre provisionar um número de assinaturas manualmente tooensure assinaturas estão disponíveis.

Considerando todos esses fatores, uma configuração de forma verdadeiramente livre é menos atraente do que parece à primeira vista.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Conhecido configurações — Olá abordagem de dimensionamento de camisa
Em vez disso, que oferecem um modelo que oferece total flexibilidade e inúmeras variações, em nossa experiência um padrão comum é tooprovide Olá capacidade tooselect conhecido configurações — em vigor, os tamanhos de camisa padrão como área restrita, pequena, média e grande. Outros exemplos de tamanhos de camiseta são ofertas de produtos, como community edition ou enterprise edition.  Em outros casos, podem se tratar de configurações de uma tecnologia específicas para uma determinada carga de trabalho - como mapear/reduzir ou no SQL.

Muitas organizações de TI empresarial, fornecedores de software livre e SIs disponibilizam hoje suas ofertas dessa maneira em ambientes virtualizados (empresas) locais ou como ofertas de SaaS (software como serviço) - CSVs e OSVs.

Essa abordagem fornece boas configurações conhecidas, de tamanhos variados que são pré-configurados para os clientes. Sem configurações conhecidas, clientes finais devem determinar dimensionamento do cluster por conta própria, leve em restrições de recursos de plataforma e faça a matemática tooidentify Olá resultante de contas de armazenamento e outros recursos (vencimento toocluster tamanho e o recurso de particionamento restrições). Conhecido configurações Habilitar tamanho Olá selecione camisa certo tooeasily clientes — ou seja, uma determinada implantação. Além disso toomaking uma melhor experiência de cliente Olá, um pequeno número de configurações conhecidas é mais fácil toosupport e pode ajudar a fornecer um nível mais alto de densidade.

Uma abordagem de configuração conhecida voltada para tamanhos de camiseta também pode ter um número variável de nós em um determinado tamanho. Por exemplo, um tamanho de camiseta pequeno pode ter entre 3 e 10 nós.  tamanho de camisa Olá seria projetado tooaccommodate backup too10 nós e fornecer Olá seleções de forma livre de toomake consumidor Olá capacidade toohello tamanho máximo identificado.  

Um tamanho de camisa com base no tipo de carga de trabalho, pode ser mais forma livre por natureza em termos de número de saudação de nós que podem ser implantados, mas terá o tamanho de nó distintos de carga de trabalho e a configuração do software Olá nó hello.

Tamanhos de roupa com base em ofertas de produtos, como comunidade ou Enterprise, pode ter tipos distintos de recursos e o número máximo de nós que podem ser implantados, tipicamente ligados toolicensing considerações ou disponibilidade de recursos entre as diferentes ofertas hello.

Você também pode acomodar clientes com variantes exclusivos usando modelos de saudação com base em JSON. Ao lidar com exceções, você pode incorporar o planejamento adequado hello e considerações para o desenvolvimento, suporte e custos.

Com base em requisitos identificados no início de saudação deste documento e cenários de consumo de modelo de cliente de saudação, identificamos um padrão de Decomposição de modelo.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Modelos de solução no escopo de capacidade e funcionalidade
Decomposição fornece desenvolvimento de tootemplate uma abordagem modular que dá suporte à reutilização de extensibilidade, teste e ferramentas. Esta seção fornece detalhes sobre como uma abordagem de Decomposição pode ser aplicadas tootemplates com um escopo de capacidade ou recursos.

Nessa abordagem, um modelo principal recebe valores de parâmetro de um consumidor de modelo, em seguida, vincula tooseveral tipos de modelos e scripts de downstream, conforme mostrado abaixo. Parâmetros, variáveis estáticas e gerados variáveis são valores de tooprovide usado dentro e fora de modelos de saudação vinculado.

![Parâmetros de modelo](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**Os parâmetros são passados modelo principal tooa e modelos de toolinked**

Olá foco seções a seguir em tipos de saudação de modelos e scripts que um único modelo é decomposto em. seções de saudação apresentam abordagens para transmitir informações de estado entre modelos de saudação. Cada modelo e hello tipos de script na imagem de saudação são descritos junto com exemplos. Para obter um exemplo contextual, consulte "Juntando as peças: um exemplo de implementação", mais adiante neste documento.

### <a name="template-metadata"></a>Metadados de modelo
Metadados de modelo (arquivo de metadata.json Olá) contém pares chave/valor que descrevem um modelo em JSON, que pode ser lido por humanos e sistemas de software.

![Metadados de modelo](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Metadados do modelo é descrito no arquivo de metadata.json de saudação**

Os agentes do software podem recuperar Olá metadata.json arquivo e publicar informações de saudação e um modelo de toohello link em uma página da web ou o diretório. Os elementos incluem *itemDisplayName*, *description*, *summary*, *githubUsername* e *dateUpdated*.

Um exemplo de arquivo é mostrado abaixo em sua totalidade.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Modelo principal
modelo principal Olá recebe parâmetros de um usuário, usa variáveis informações toopopulate objeto complexo e executa modelos Olá vinculado.

![Modelo principal](./media/best-practices-resource-manager-design-templates/main-template.png)

**modelo principal Olá recebe parâmetros de um usuário**

Um parâmetro que é fornecido é um tipo de configuração também conhecido como Olá camisa parâmetro de tamanho devido a seus valores padronizados como pequeno, médio ou grande. Na prática, você pode usar esse parâmetro de várias maneiras. Para obter detalhes, consulte "Modelo de recursos de configuração conhecida", posteriormente neste documento.

Alguns recursos são implantados, independentemente da configuração de saudação especificada pelo parâmetro de um usuário. Esses recursos são provisionados usando um modelo de recurso compartilhado único e são compartilhados com outros modelos, portanto, modelo de recurso compartilhado Olá é executado primeiro.

Alguns recursos são implantados opcionalmente, independentemente da configuração especificada de conhecidos hello.

### <a name="shared-resources-template"></a>Modelo de recursos compartilhados
Esse modelo fornece recursos que são comuns a todas as configurações conhecidas. Ele contém a rede virtual hello, conjuntos de disponibilidade e outros recursos que são necessários, independentemente do modelo de configuração de saudação que é implantado.

![Recursos de modelo](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Modelo de recursos compartilhados**

Nomes de recursos, como nome de rede virtual Olá baseiam-se no modelo principal hello. Você pode especificá-los como uma variável no modelo ou recebê-los como um parâmetro de usuário hello, conforme exigido por sua organização.

### <a name="optional-resources-template"></a>Modelo de recursos opcionais
modelo de recursos opcionais de saudação contém recursos que são implantados por meio de programação com base no valor de saudação de um parâmetro ou variável.

![Recursos opcionais](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**Modelo de recursos opcionais**

Por exemplo, você pode usar um modelo de recursos opcionais tooconfigure um jumpbox que permite acesso indireto tooa implantado ambiente da saudação Internet pública. Você usaria um parâmetro ou variável tooidentify se Olá jumpbox deve ser habilitada e hello *concat* função como o nome de destino toobuild Olá para hello, *jumpbox_enabled.json*. Modelo de vinculação usaria Olá resultante tooinstall variável Olá jumpbox.

Você pode vincular o modelo de recursos opcionais de saudação de vários locais:

* Quando aplicável tooevery implantação, criar um link orientado por parâmetros de modelo de recursos compartilhados hello.
* Quando aplicável tooselect conhecido configurações — por exemplo, instalar somente em grandes implantações — criar um link orientado por parâmetros ou orientado a variável de modelo de configuração de saudação.

Se um determinado recurso é opcional pode não ser controlada pelo consumidor de modelo Olá mas pelo provedor de modelos de saudação. Por exemplo, talvez seja necessário toosatisfy um requisito de produto específico ou complemento do produto (comum para CSVs) ou políticas tooenforce (comuns para SIs e a TI empresarial grupos). Nesses casos, você pode usar uma variável tooidentify se o recurso de saudação deve ser implantado.

### <a name="known-configuration-resources-template"></a>Modelo de recursos de configuração conhecida
No modelo principal de saudação, um parâmetro pode ser exposto tooallow Olá modelo consumidor toospecify toodeploy uma configuração desejada. Muitas vezes, essa configuração usa uma abordagem de tamanho de camiseta com um conjunto de tamanhos de configuração fixa, como área restrita, pequeno, médio e grande.

![Recursos de configuração conhecida](./media/best-practices-resource-manager-design-templates/known-config.png)

**Modelo de recursos de configuração conhecida**

abordagem de tamanho de camisa Olá é comumente usada, mas os parâmetros de saudação podem representar qualquer conjunto de configurações conhecidas. Por exemplo, você pode especificar um conjunto de ambientes para um aplicativo empresarial como Development, Test e Product. Ou você pode usá-lo para um toorepresent de serviço de nuvem diferente dimensionar unidades, versões ou configurações de produto como comunidade, Developer ou Enterprise.

Como com o modelo de recurso compartilhado hello, variáveis são passadas toohello modelo de configurações conhecidas do:

* Um usuário final – ou seja, os parâmetros de saudação enviados modelo principal toohello.
* Uma organização — ou seja, Olá variáveis no modelo principal Olá que representam requisitos internos ou políticas.

### <a name="member-resources-template"></a>Modelo de recursos de membro
Em uma configuração conhecida, um ou mais tipos de nó de membro costumam ser incluídos. Por exemplo, com o Hadoop, você tem nós mestres e nós de dados. Se estiver instalando o MongoDB, você terá nós de dados e um arbitrador. Se está implantando o DataStax, você tem nós de dados e uma máquina virtual com OpsCenter instalado.

![Recursos de membros](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Modelo de recursos de membro**

Cada tipo de nós pode ter diferentes tamanhos de máquinas virtuais, número de discos anexados, scripts tooinstall e configurar nós hello, configurações de porta para Olá VMs, número de instâncias e outros detalhes. Para que cada tipo de nó obtém seu próprio modelo de recursos de membro, que contém a saudação detalhes para implantar e configurar uma infraestrutura, bem como executar scripts toodeploy e configurar o software em Olá VM.

Para VMs, geralmente dois tipos de scripts são utilizados: os amplamente reutilizáveis e os personalizados.

### <a name="widely-reusable-scripts"></a>Scripts amplamente reutilizáveis
Scripts amplamente reutilizáveis podem ser usados em vários tipos de modelos. Um dos exemplos de melhor Olá desses scripts reutilizáveis amplamente configura RAID em Linux toopool discos e obter um maior número de IOPS. Independentemente do software Olá sendo instalado na VM de hello, o script fornece reutilização das práticas comprovadas para cenários comuns.

![Scripts reutilizáveis](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**Modelos de recursos de membro podem chamar scripts amplamente reutilizáveis**

### <a name="custom-scripts"></a>Scripts personalizados
Modelos normalmente chamam um ou mais scripts que instalam e configuram software em máquinas virtuais. Um padrão comum é visto com grandes topologias em que várias instâncias de um ou mais tipos de membro são implantadas. Um script de instalação é iniciado para cada VM que pode ser executada em paralelo, seguido por um script de instalação que é chamado depois que todas as máquinas virtuais (ou todas as máquinas virtuais de um determinado tipo de membro) são implantadas.

![Scripts personalizados](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**Modelos de recursos de membro podem chamar scripts para uma finalidade específica, como a configuração da VM**

## <a name="capability-scoped-solution-template-example---redis"></a>Exemplo de modelo de solução no escopo de funcionalidade - Redis
tooshow como uma implementação pode funcionar, vamos examinar um exemplo prático de como criar um modelo que facilita a implantação de saudação e configuração do Redis em tamanhos de roupa padrão.  

Para implantação de hello, há um conjunto de recursos compartilhados (rede virtual, conta de armazenamento, conjuntos de disponibilidade) e um recurso opcional (jumpbox). Há várias configurações conhecidas representadas como tamanhos de camiseta (pequeno, médio, grande), mas cada uma com um único tipo de nó. Há também dois scripts específicos para a finalidade (instalação, configuração).

### <a name="creating-hello-template-files"></a>Criando arquivos de modelo de saudação
Você cria um modelo principal chamado azuredeploy.json.

Você cria um modelo de recursos compartilhados chamado shared-resources.json

Criar um modelo de recurso opcional tooenable Olá de implantação um jumpbox, denominado jumpbox_enabled.json

O Redis usa apenas um tipo de nó, portanto, você cria um modelo único de recurso de membro chamado node-resources.json.

Com Redis, você deseja tooinstall cada nó individual e, em seguida, configurar o cluster de saudação.  Tem scripts tooaccommodate Olá instalação e configurar, install.sh de cluster de redis e setup.sh de cluster de redis.

### <a name="linking-hello-templates"></a>Modelos de saudação de vinculação
Usando vinculação de modelo, modelo principal Olá vincula modelo de recursos compartilhados toohello, que estabelece a rede virtual hello.

Lógica é adicionada em consumidores de tooenable Olá modelo principal de saudação modelo toospecify se um jumpbox deve ser implantado. Um *habilitado* valor Olá *EnableJumpbox* parâmetro indica que esse cliente Olá quer toodeploy um jumpbox. Quando esse valor é fornecido, o modelo de saudação concatena *_enabled* como um nome de modelo base tooa sufixo para o recurso de jumpbox hello.

modelo principal Olá aplica Olá *grande* valor de parâmetro como um nome de modelo base tooa sufixo para tamanhos de roupa e, em seguida, usa esse valor em um link de modelo out muito*technology_on_os_large.json*.

topologia de saudação seria semelhante a esta ilustração.

![Modelo de Redis](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Estrutura de modelo para um modelo de Redis**

### <a name="configuring-state"></a>Configurando o estado
Para nós de saudação em cluster Olá, há duas etapas tooconfiguring estado de hello, representadas por Scripts de finalidade específica.  Redis instala "install.sh de cluster redis" e "setup.sh de cluster redis" configura o cluster hello.

### <a name="supporting-different-size-deployments"></a>Suporte a implantações de tamanho diferente
Dentro de variáveis de modelo de tamanho de camisa Olá Especifica o número de saudação de nós de cada tipo de tamanho especificado de toodeploy para hello (*grande*). Em seguida, implanta esse número de instâncias VM usando loops de recursos, fornecendo tooresources nomes exclusivos, acrescentando o nome do nó com um número de sequência numérica de *copyIndex()*. Ele faz essas etapas para ambas as VMs de zona e a quente, conforme definido no modelo de nome de camisa Olá

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>Modelos com escopo de solução de ponta a ponta e decomposição
Um modelo de solução com um escopo de solução de ponta a ponta se concentra em fornecer uma solução desse tipo.  Normalmente, essa abordagem é uma composição de vários modelos com escopo de funcionalidade com recursos, lógica e estado adicionais.

Conforme realçado na imagem de saudação abaixo, hello mesmo modelo usado para modelos de recurso com escopo é estendido para modelos com um escopo de solução de ponta a ponta.

Um modelo de recursos compartilhados e os modelos de recursos opcionais servem Olá a mesma função, como a capacidade de saudação no escopo do modelo abordagens, mas têm o escopo para solução de tooend Olá final.

Como o escopo da solução tooend modelos também podem normalmente têm tamanhos de roupa, modelo de recursos de configuração conhecido Olá reflete o que é necessário para uma determinada configuração conhecida de solução de saudação.

Olá tooone de links de modelo de recursos de configuração conhecido ou mais capacidade de escopo modelos de solução solução tooend toohello relevantes, bem como Olá modelos de recursos de membro que são necessários para a solução tooend hello.

Como tamanho de camisa Olá de solução de saudação pode ser diferente de modelo de escopo do recurso de saudação individuais, variáveis em Olá conhecido modelo de configuração de recursos são tooprovide usado Olá os valores apropriados para a solução capacidade downstream no escopo modelos toodeploy Olá camisa tamanho apropriado.

![Ponta a ponta](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**modelo de saudação usado para a capacidade ou modelos de solução de recurso com escopo podem ser estendidos para escopos de modelo de solução final tooend prontamente**

## <a name="preparing-templates-for-hello-marketplace"></a>Preparando modelos para Olá Marketplace
Olá anterior abordagem prontamente acomoda cenários onde empresas, SIs e CSVs tooeither de deseja implantar modelos Olá sozinhos ou habilitar toodeploy seus clientes por conta própria.

Outro cenário desejado está implantando um modelo por meio do marketplace hello.  Essa abordagem de Decomposição funciona para o marketplace de hello, com algumas pequenas alterações.

Conforme mencionado anteriormente, os modelos podem ser tipos de implantação distintas de toooffer usado para venda no mercado de saudação. Tipos distintos de implantação podem ser tamanhos de camiseta (pequeno, médio, grande), tipo de produto/público (community, developer, enterprise) ou tipo de recurso (básico, de alta disponibilidade).

Como mostrado abaixo, Olá existente final tooend solução ou a funcionalidade de modelos de escopo podem ser prontamente utilizado toolist Olá diferentes configurações conhecidas no marketplace de saudação.

Olá parâmetros toohello principal são primeiro modificado tooremove Olá parâmetro de entrada denominado tshirtSize.

Enquanto a tipos de implantação distintas de saudação mapeiam toohello conhecido modelo de configuração de recursos, eles também precisam recursos comuns de saudação e configuração encontrada no hello modelo de recursos compartilhados e potencialmente os modelos de recursos opcionais.

Se você quiser toopublish marketplace de toohello seu modelo, você pode estabelecer cópias diferentes do seu modelo principal que substitui Olá anteriormente disponível parâmetro de entrada da variável de tooa tshirtSize inserido no modelo de saudação.

![Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Adaptar uma solução no escopo do modelo para o marketplace Olá**

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como compartilhar o estado dentro e fora de modelos, consulte [compartilhamento de estado em modelos do Azure Resource Manager](best-practices-resource-manager-state.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

