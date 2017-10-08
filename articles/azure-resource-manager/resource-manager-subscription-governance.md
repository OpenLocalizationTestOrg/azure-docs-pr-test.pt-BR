---
title: "práticas recomendadas de aaaBest para empresas movendo tooAzure | Microsoft Docs"
description: "Descreve uma estrutura que as empresas podem usar tooensure um ambiente seguro e gerenciável."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Andaime empresarial do Azure — governança de assinatura prescritiva
As empresas estão adotando cada vez mais a nuvem pública Olá seu agilidade e flexibilidade. Eles estão utilizando a receita de toogenerate pontos fortes da nuvem hello ou otimizam os recursos para empresas hello. O Microsoft Azure fornece uma variedade de serviços de empresas podem montar como blocos de construção tooaddress uma ampla gama de aplicativos e cargas de trabalho. 

No entanto, saber onde toobegin pode ser difícil. Depois de decidir toouse do Azure, normalmente surgem algumas perguntas:

* "Como atender aos nossos requisitos legais para domínio dos dados em determinados países?"
* "Como garantir que alguém não altere inadvertidamente um sistema crítico?"
* "Como saber o que cada recurso aceita para que eu possa responsabilizá-lo e cobrá-lo de volta precisamente?"

cliente potencial de saudação de uma assinatura vazia com nenhuma trilhos de proteção é intimidadora. Esse espaço em branco pode atrapalhar tooAzure sua movimentação.

Este artigo fornece um ponto de partida para profissionais técnicos tooaddress Olá necessidade para governança e saldo com hello precisa para agilidade. Ele apresenta o conceito de saudação de scaffold uma empresa que orienta as empresas na implementação e gerenciar suas assinaturas do Azure. 

## <a name="need-for-governance"></a>Necessidade de governança
Ao mover tooAzure, você deve tratar tópico Olá de governança antecipado tooensure Olá bem-sucedida uso da nuvem hello dentro de empresa hello. Infelizmente, tempo de saudação e burocracia de criação de um sistema abrangente de governança significa que alguns grupos de negócios diretamente vá toovendors sem envolver TI empresarial. Essa abordagem pode deixar Olá enterprise abrir toovulnerabilities se recursos Olá não são gerenciados corretamente. características de saudação da nuvem pública, Olá agilidade, flexibilidade e preço com base no consumo - são importantes toobusiness grupos que precisam tooquickly atender às demandas de saudação de clientes (internos e externos). Mas, TI empresarial precisa tooensure sistemas e dados são protegidos com eficiência.

Na vida real, scaffolding é a base de saudação de toocreate usadas da estrutura de saudação. scaffold Olá guias estrutura geral hello e fornece pontos de ancoragem para mais permanente toobe sistemas montado. Uma exibição de scaffold enterprise é Olá mesmo: um conjunto de controles flexíveis e recursos do Azure que fornecem estrutura toohello ambiente e âncoras para serviços baseado em nuvem pública hello. Ele fornece construtores de saudação (IT e grupos de negócios) um toocreate foundation e anexar novos serviços.

scaffold Olá é com base nas práticas coletadas de muitos contratos com clientes de vários tamanhos. Esses variam de clientes de empresas de pequenas porte desenvolver soluções em empresas de tooFortune 500 nuvem hello e fornecedores independentes de software que estão migrando e desenvolver soluções em nuvem hello. scaffold enterprise Hello é toosupport flexível toobe "especificamente" cargas de trabalho tradicionais IT e cargas de trabalho agile; como os desenvolvedores que criam aplicativos de software-como um serviço (SaaS) com base nos recursos do Azure.

scaffold de enterprise Olá é pretendido toobe Olá foundation de cada nova assinatura no Azure. Ele permite que os requisitos de governança mínimo de saudação atender aos administradores tooensure cargas de trabalho de uma organização sem impedindo que os grupos de negócios e desenvolvedores atenda rapidamente suas próprias metas.

> [!IMPORTANT]
> Governança é crucial toohello êxito do Azure. Destinos neste artigo Olá implementação técnica de scaffold de uma empresa, mas só aborda processo mais amplo hello e as relações entre componentes de saudação. Controle de política fluem de cima Olá para baixo e é determinado pelo qual Olá negócios exigirem tooachieve. Naturalmente, criação de saudação de um modelo de controle para o Azure inclui representantes da equipe de TI, mas é mais importante, ele deve ter representação forte de gerenciamento de segurança e riscos e líderes de grupo de negócios. No final do hello, um scaffold enterprise é sobre como eliminar toofacilitate de risco de negócios missão e aos objetivos da organização.
> 
> 

Olá a imagem a seguir descreve os componentes de saudação do scaffold hello. foundation Olá se baseia em um plano sólido para departamentos, contas e assinaturas. pilares Olá consistem em políticas do Gerenciador de recursos e padrões de nomenclatura fortes. restante Olá scaffold hello proveniente principais recursos do Azure e recursos que permitem que um ambiente seguro e gerenciável.

![componentes do andaime](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> O Azure cresceu rapidamente desde sua apresentação em 2008. Esse crescimento necessário toorethink as equipes de engenharia do Microsoft sua abordagem para gerenciar e implantar serviços. modelo do Gerenciador de recursos do Azure Olá foi introduzido no 2014 e substitui o modelo de implantação clássico hello. Gerenciador de recursos permite que as organizações toomore facilmente implantar, organizar e controlar os recursos do Azure. O Resource Manager inclui a paralelização ao criar recursos para implantação mais rápida de soluções complexas e interdependentes. Ele também inclui o controle de acesso granular e recursos de tootag de capacidade de saudação com metadados. A Microsoft recomenda que você criar todos os recursos por meio do modelo do Gerenciador de recursos de saudação. scaffold de enterprise Olá destina-se explicitamente para o modelo do Gerenciador de recursos de saudação.
> 
> 

## <a name="define-your-hierarchy"></a>Definir sua hierarquia
Base de saudação do scaffold Olá é hello Azure Enterprise Enrollment (e Olá Enterprise Portal). o registro enterprise Olá define a forma de saudação e usar serviços do Azure dentro de uma empresa e é a estrutura de governança Olá core. No contrato de corporativo Olá, os clientes conseguem toofurther subdividir o ambiente de saudação em departamentos, contas e, finalmente, as assinaturas. Uma assinatura do Azure é a unidade básica de saudação em que todos os recursos estão contidos. Ela também define vários limites dentro do Azure, como o número de núcleos, recursos, etc.

![hierarquia](./media/resource-manager-subscription-governance/agreement.png)

Cada empresa é diferente e hierarquia Olá na imagem anterior Olá permite flexibilidade significativas em como o Azure é organizado dentro da empresa de saudação. Antes de implementar a orientação de saudação contida neste documento, você deve sua hierarquia de modelo e entender Olá impacto na cobrança, o acesso a recursos e a complexidade.

três padrões comuns Olá para registros do Azure são:

* Olá **funcional** padrão
  
    ![funcional](./media/resource-manager-subscription-governance/functional.png)
* Olá **unidade de negócios** padrão 
  
    ![negócios](./media/resource-manager-subscription-governance/business.png)
* Olá **geográfica** padrão
  
    ![geográfico](./media/resource-manager-subscription-governance/geographic.png)

Aplicar scaffold Olá no hello tooextend nível Olá governança requisitos de assinatura do enterprise Olá para uma assinatura de saudação.

## <a name="naming-standards"></a>Padrões de nomenclatura
padrões de nomenclatura é primeiro pilar de saudação do scaffold hello. Padrões de nomenclatura bem projetados habilitar tooidentify recursos no portal de hello, em uma lista e scripts. Provavelmente, você já tem padrões de nomenclatura para a infraestrutura local. Ao adicionar ambiente de tooyour do Azure, você deve estender os recursos do Azure de tooyour padrões de nomenclatura. Padrão de nomenclatura facilitar o gerenciamento mais eficiente de ambiente Olá em todos os níveis.

> [!TIP]
> Para convenções de nomenclatura:
> * Examine e adotar onde for possível Olá [padrões e práticas recomendadas de orientação](../guidance/guidance-naming-conventions.md). Essas diretrizes ajudam a decidir sobre um padrão de nomenclatura significativo.
> * Use camelCasing para nomes de recursos (como myResourceGroup e vnetNetworkName). Observação: Há certos recursos, como contas de armazenamento, em que a única opção de saudação é toouse letras minúsculas (e não há outros caracteres especiais).
> * Considere o uso do Azure Resource Manager políticas (descritas na próxima seção, Olá) tooenforce padrões de nomenclatura.
> 
> Olá anteriores dicas ajudam a implementar uma convenção de nomenclatura consistente.

## <a name="policies-and-auditing"></a>Políticas e auditoria
Pilar segundo de saudação de scaffold Olá envolve a criação de [políticas do Azure Resource Manager](resource-manager-policy.md) e [auditoria de log de atividades de saudação](resource-group-audit.md). As políticas do Gerenciador de recursos fornecem risco de toomanage capacidade Olá no Azure. Você pode definir políticas que garantem o domínio dos dados, restringindo, impondo ou auditando determinadas ações. 

* A política é um sistema de **permissão** padrão. Você pode controlar ações definindo e atribuindo tooresources políticas que negar ou ações em recursos de auditoria.
* As políticas são descritas pelas definições de política em uma linguagem de definição de política (condições "se-então").
* Crie políticas com arquivos formatados para JSON (Javascript Object Notation). Depois de definir uma política, você atribuí-lo tooa determinado escopo: assinatura, o grupo de recursos ou o recurso.

Políticas têm várias ações que permitem cenários de tooyour uma abordagem refinada. Olá ações são:

* **Negar**: solicitação de recurso de saudação de blocos
* **Auditoria**: permite que a solicitação de saudação mas adiciona um log de atividades de toohello de linha (que pode ser usado tooprovide alertas ou runbooks tootrigger)
* **Acrescentar**: adiciona informações toohello recurso especificado. Por exemplo, se não houver uma marcação "CostCenter" em um recurso, adicione essa marcação com um valor padrão.

### <a name="common-uses-of-resource-manager-policies"></a>Usos comuns das políticas do Resource Manager
Políticas do Gerenciador de recursos do Azure são uma ferramenta avançada de saudação Kit de ferramentas do Azure. Elas permitem que você tooavoid custos inesperados, tooidentify um centro de custos de recursos por meio de marcação e tooensure que requisitos de conformidade. Quando as políticas são combinadas com recursos de auditoria interna hello, você pode modo soluções complexas e flexíveis. As políticas permitem que as empresas tooprovide controles para cargas de trabalho "TI tradicional" e "Agile" cargas de trabalho; como desenvolver aplicativos cliente. padrões mais comuns Hello, que podemos ver para as políticas são:

* **Conformidade/dados de replicação geográfica Soberania** -Azure fornece regiões em Olá, mundo. As empresas costuma ser toocontrol onde os recursos são criados (se tooensure Soberania de dados ou apenas os recursos de tooensure são criados toohello fechar final consumidores de recursos de saudação).
* **Gerenciamento de custo**: uma assinatura do Azure pode conter recursos de muitos tipos e escala. As empresas costuma ser tooensure esse padrão assinaturas Evite usar recursos desnecessariamente grandes, o que podem centenas de dólares por mês ou mais.
* **Padrão de controle por meio de marcas necessárias** -exigir marcas é um dos recursos mais comuns e altamente desejado de saudação. As empresas usando políticas do Gerenciador de recursos do Azure estão tooensure capaz de que um recurso está devidamente marcado. Olá marcas mais comuns são: tipo de departamento, o proprietário do recurso e ambiente (por exemplo - produção, teste, desenvolvimento)

**Exemplos**

Assinatura de "TI Tradicional" para aplicativos de linha de negócios

* Impor as marcações Departamento e Proprietário a todos os recursos
* Restringir a criação de recursos toohello região da América do Norte
* Restringir Olá capacidade toocreate VMs da série G e Clusters de HDInsight

Ambiente "Ágil" para uma unidade de negócios que cria aplicativos de nuvem

* requisitos de Soberania dados toomeet, permitir a criação de saudação de recursos apenas em uma região específica.
* Impor a marcação Ambiente a todos os recursos. Se um recurso é criado sem uma marca, acrescente Olá **ambiente: desconhecido** toohello recursos de marca.
* Fazer auditoria quando os recursos forem criados fora da América do Norte, mas não impedir.
* Fazer auditoria quando recursos de alto custo forem criados.

> [!TIP]
> o uso mais comum de políticas do Gerenciador de recursos entre organizações Hello é toocontrol *onde* recursos podem ser criados e *que* tipos de recursos podem ser criados. Além de controles da tooproviding *onde* e *que*, muitas empresas usar políticas tooensure recursos têm Olá toobill de metadados apropriados para o consumo. Recomendamos a aplicação de políticas no nível de assinatura de saudação para:
> 
> * Domínio geográfico de conformidade/dados
> * Gerenciamento de custo
> * Marcações obrigatórias (determinadas pelas necessidades de negócios, como BillTo, Proprietário do Aplicativo)
> 
> Você pode aplicar políticas adicionais em níveis inferiores do escopo.
> 
> 

### <a name="audit---what-happened"></a>Auditoria — o que aconteceu?
tooview como seu ambiente está funcionando, você precisa de atividade de usuário tooaudit. A maioria dos tipos de recurso no Azure cria logs de diagnóstico que você pode analisar por meio de uma ferramenta de log ou no Azure Operations Management Suite. Você pode coletar logs de atividade entre várias assinaturas de tooprovide um departamento ou exibição de empresa. Registros de auditoria são uma ferramenta de diagnóstica importante e eventos tootrigger um mecanismo crucial Olá ambiente do Azure.

Logs de atividade de implantações do Gerenciador de recursos permitem que você Olá toodetermine **operações** que levou o local e que sejam executados. Os logs de atividades podem ser coletados e agregados usando ferramentas como o Log Analytics.

## <a name="resource-tags"></a>Marcações de recursos
Como os usuários em sua organização Adicionar assinatura de recursos de toohello, torna-se recursos tooassociate cada vez mais importante com o departamento apropriado hello, o cliente e o ambiente. Você pode anexar tooresources metadados por meio de [marcas](resource-group-using-tags.md). Marcas tooprovide informações sobre recursos de saudação ou proprietário hello são usadas. As marcas permitem que você toonot apenas agregação e recursos do grupo de várias maneiras, mas usam esses dados para fins de saudação de estorno. Você pode marcar os recursos com o backup de pares de chave: valor too15. 

As marcas de recurso são flexíveis e devem ser anexado toomost recursos. Os exemplos de marcações de recurso comuns são:

* BillTo
* Departamento (ou Unidade de Negócios)
* Ambiente (Produção, Preparação, Desenvolvimento)
* Camada (Camada da Web, Camada de Aplicativo)
* Proprietário do Aplicativo
* ProjectName

![marcas](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Para obter mais exemplos de marcações, confira [Convenções de nomenclatura recomendadas para recursos do Azure](../guidance/guidance-naming-conventions.md).

> [!TIP]
> Considere criar uma política que exija marcação para:
> 
> * Grupos de recursos
> * Armazenamento
> * Máquinas Virtuais
> * Servidores Web/Ambientes do Serviço de Aplicativo
> 
> Essa estratégia marcação identifica em suas assinaturas quais metadados é necessária para negócios hello, finanças, segurança, gerenciamento de riscos e gerenciamento geral do ambiente de saudação. 

## <a name="resource-group"></a>Grupo de recursos
Gerenciador de recursos permite que você tooput recursos em grupos significativos para afinidade de cobrança ou natural de gerenciamento. Conforme mencionado anteriormente, o Azure tem dois modelos de implantação. Olá modelo clássico anterior, a unidade básica Olá de gerenciamento foi assinatura hello. Era difícil toobreak recursos dentro de uma assinatura, o que levou toohello criação de um grande número de assinaturas. Com o modelo do Gerenciador de recursos de hello, vimos Introdução Olá de grupos de recursos. Os grupos de recursos são contêineres de recursos que têm um ciclo de vida comum ou compartilham um atributo, como "todos os servidores SQL" ou "Aplicativo A".

Grupos de recursos não podem ser contidos em si e recursos podem pertencer somente tooone grupo de recursos. É possível aplicar determinadas ações em todos os recursos em um grupo de recursos. Por exemplo, a exclusão de um grupo de recursos remove todos os recursos no grupo de recursos de saudação. Normalmente, você pode colocar um aplicativo inteiro ou sistema relacionadas em Olá mesmo grupo de recursos. Por exemplo, um aplicativo de três camadas chamado o aplicativo Web da Contoso conteria o servidor de web hello, o servidor de aplicativos e o SQL server no hello mesmo grupo de recursos.

> [!TIP]
> Como organizar os grupos de recursos pode variar muito de cargas de trabalho "TI tradicional" cargas de trabalho "TI Agile":
> 
> * "Tradicional IT" cargas de trabalho geralmente são agrupadas por itens em Olá mesmo ciclo de vida, como um aplicativo. O agrupamento por aplicativo permite o gerenciamento individual de aplicativo.
> * "Agile IT" cargas de trabalho tendem toofocus em aplicativos de nuvem voltado para o cliente externa. grupos de recursos de saudação devem refletir as camadas de saudação de implantação (por exemplo, a camada da Web, camada de aplicativo) e o gerenciamento.
> 
> Noções básicas sobre sua carga de trabalho ajudam a desenvolver uma estratégia de grupo de recursos.

## <a name="role-based-access-control"></a>Controle de acesso baseado em função
Você provavelmente está perguntando "que devem ter acesso tooresources?" e "como controlar esse acesso?" Permitir ou não permitindo acesso toohello portal do Azure e controlando o acesso tooresources no portal de saudação é crucial. 

Quando o Azure foi inicialmente lançado, assinatura de tooa de controles de acesso foram básicos: administrador ou Coadministrador. Acesso tooa assinatura Olá clássico modelo implicado acesso tooall Olá recursos no portal de saudação. Esta falta de um controle refinado led toohello a proliferação de assinaturas tooprovide um nível de controle de acesso razoável para um registro do Azure.

Essa proliferação de assinaturas não é mais necessária. Com controle de acesso baseado em função, você pode atribuir usuários a funções toostandard (como "leitor" comuns e tipos de "escritor" de funções). Você também pode definir funções personalizadas.

> [!TIP]
> controle de acesso baseado em função tooimplement:
> * Conectar-se usando o Active Directory sua identidade corporativa repositório (geralmente Active Directory) tooAzure Olá ferramenta AD Connect.
> * Olá administrador/Coadministrador de uma assinatura usando uma identidade gerenciada do controle. **Não** atribuir administrador/coadministrador tooa novo proprietário da assinatura. Em vez disso, use o RBAC funções tooprovide **proprietário** direitos tooa grupo ou indivíduo.
> * Adicione grupo de tooa de usuários do Azure (por exemplo, proprietários do aplicativo X) no Active Directory. Use Olá sincronizados tooprovide grupo membros Olá direitos apropriados toomanage Olá recurso de grupo que contém o aplicativo hello.
> * Siga Olá princípio de conceder Olá **menos privilégios** toodo necessário Olá esperado de trabalho. Por exemplo:
>   * Grupo de implantação: Um grupo que é capaz de toodeploy apenas os recursos.
>   * Gerenciamento de máquinas virtuais: Um grupo que é capaz de toorestart VMs (para operações)
> 
> Essas dicas ajudam a gerenciar o acesso do usuário em sua assinatura.

## <a name="azure-resource-locks"></a>Bloqueios de recursos do Azure
Como sua organização adiciona a assinatura do core services toohello, ele se torna tooensure cada vez mais importante que esses serviços são interrupção dos negócios de tooavoid disponíveis. [Bloqueios de recursos](resource-group-lock-resources.md) permitem operações de toorestrict nos recursos de alto valor onde sua modificação ou exclusão teria um impacto significativo sobre os aplicativos ou infraestrutura de nuvem. Você pode aplicar a assinatura de tooa de bloqueios, o grupo de recursos ou o recurso. Normalmente, você pode aplicar bloqueios toofoundational recursos, como redes virtuais, gateways e contas de armazenamento. 

Atualmente, os Bloqueios de recursos aceitam dois valores: CanNotDelete e ReadOnly. CanNotDelete significa que os usuários (com os direitos apropriados de saudação) podem ainda ler ou modificar um recurso, mas não é possível excluí-lo. ReadOnly significa que usuários autorizados não podem excluir nem modificar um recurso.

bloqueios de gerenciamento toocreate ou delete, você deve ter acesso muito`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações.
De funções internas do hello, somente o proprietário e o administrador de acesso do usuário são concedidas as ações.

> [!TIP]
> As opções de rede principais devem ser protegidas com bloqueios. A exclusão acidental de um gateway de VPN site a site seria desastroso tooan assinatura do Azure. Azure não permite que você toodelete uma rede virtual que está em uso, mas aplicar mais restrições é útil precaução. 
> 
> * Rede virtual: CanNotDelete
> * Grupo de Segurança de Rede: CanNotDelete
> * Políticas: CanNotDelete
> 
> As políticas também são manutenção toohello essencial de controles apropriados. É recomendável que você aplique uma **CanNotDelete** bloquear toopolices que estão em uso.

## <a name="core-networking-resources"></a>Recursos de rede essenciais
Tooresources de acesso pode ser interno (dentro da rede da empresa Olá) ou externos (por meio de Olá da internet). É fácil para os usuários de sua tooinadvertently de organização colocar recursos no lugar errado Olá e potencialmente abri-los toomalicious acesso. Assim como acontece com dispositivos de locais, as empresas devem adicionar controles apropriados tooensure que os usuários do Azure decisões saudação à direita. Para governança da assinatura, identificamos recursos principais que fornecem controle básico de acesso. recursos principais de saudação consistem em:

* **Redes virtuais** são objetos de contêiner para sub-redes. Embora não seja estritamente necessário, ele geralmente é usado ao se conectar a recursos corporativos de toointernal de aplicativos.
* **Grupos de segurança de rede** são semelhantes firewall de tooa e fornecer regras para como um recurso pode "falar" rede hello. Eles fornecem controle granular sobre como / se uma sub-rede (ou máquina virtual) pode se conectar toohello Internet ou outras sub-redes em Olá mesmo rede virtual.

![rede principal](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Para rede:
> * Crie cargas de trabalho de tooexternal voltados dedicado redes virtuais e cargas de trabalho interface interna. Essa abordagem reduz a chance de saudação de inadvertidamente a colocação de máquinas virtuais que são destinadas para cargas de trabalho internas em um espaço com acesso externo.
> * Configure o acesso de toolimit de grupos de segurança de rede. No mínimo, bloquear acesso toohello internet por meio de redes virtuais internas e a rede corporativa do bloco acesso toohello de redes virtuais externas.
> 
> Essas dicas lhe ajudarão a implementar recursos de rede seguros.

### <a name="automation"></a>Automação
Gerenciar recursos individualmente é demorado e potencialmente sujeito a erros para determinadas operações. O Azure fornece vários recursos de automação, incluindo Automação do Azure, Aplicativos Lógicos e Azure Functions. [Automação do Azure](../automation/automation-intro.md) permite que os administradores toocreate e definir runbooks toohandle as tarefas comuns no gerenciamento de recursos. Crie runbooks usando um editor de código do PowerShell ou um editor gráfico. Você pode produzir fluxos de trabalho complexos de vários estágios. Automação do Azure geralmente é usado toohandle a tarefas comuns como desligar recursos não usados ou criando recursos no gatilho específico de tooa de resposta sem a necessidade de intervenção humana.

> [!TIP]
> Para automação:
> * Criar uma conta de automação do Azure e examine Olá runbooks disponíveis (linha de comando e de gráfica) disponíveis no hello [Galeria de Runbook](../automation/automation-runbook-gallery.md).
> * Importe e personalize runbooks importantes para seu próprio uso.
> 
> Um cenário comum é Olá capacidade tooStart/desligamento virtual máquinas em um agendamento. Não há runbooks de exemplo estão disponíveis na Galeria de saudação que esse cenário e ensiná-lo como tooexpand-lo.
> 
> 

## <a name="azure-security-center"></a>Central de Segurança do Azure
Talvez uma maior adoção de toocloud bloqueadores Olá foi preocupações Olá sobre segurança. Os gerentes de risco de TI e os departamentos de segurança necessário tooensure que recursos no Azure estejam protegidos. 

Olá [Central de segurança do Azure](../security-center/security-center-intro.md) fornece uma visão central do status de segurança de saudação de recursos em assinaturas hello e fornece recomendações que ajudam a evitar o comprometimento de recursos. Ele pode habilitar políticas mais granulares (por exemplo, aplicando políticas toospecific grupos de recursos que permitem Olá enterprise tootailor o risco de toohello postura está tratando). Finalmente, a Central de segurança do Azure é uma plataforma aberta que permite que parceiros da Microsoft e software de toocreate de fornecedores independentes de software que se conecta à Central de segurança do Azure tooenhance seus recursos. 

> [!TIP]
> A Central de Segurança do Azure é habilitada por padrão em cada assinatura. No entanto, você deve habilitar a coleta de dados de máquinas virtuais tooallow Central de segurança do Azure tooinstall seu agente e iniciar a coleta de dados.
> 
> ![coleta de dados](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Agora que você aprendeu sobre controle de assinatura, é hora toosee essas recomendações em prática. Veja [Exemplos de implementação da governança de assinatura do Azure](resource-manager-subscription-examples.md).

