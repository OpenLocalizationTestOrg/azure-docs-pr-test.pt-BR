---
title: "aaaScenarios e exemplos para governança de assinatura | Microsoft Docs"
description: "Fornece exemplos de como tooimplement governança de assinatura do Azure para cenários comuns."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Exemplos de implementação de scaffold do Azure Enterprise
Este tópico fornece exemplos de como uma empresa pode implementar recomendações de saudação para um [scaffold Azure enterprise](resource-manager-subscription-governance.md). Ele usa uma empresa fictícia chamada Contoso tooillustrate práticas recomendadas para cenários comuns.

## <a name="background"></a>Segundo plano
A Contoso é uma empresa em todo o mundo que fornece soluções de cadeia de fornecimento de clientes tudo, de um modelo de pacote de tooa de modelo "Software como um serviço" implantado no local.  Eles desenvolverem software globo Olá com centros de desenvolvimento significativo na Índia, Olá EUA e Canadá.

parte do ISV Olá da empresa Olá é dividido em várias unidades de negócios que gerenciam os produtos em uma empresa significativa. Cada unidade de negócios tem seus próprios desenvolvedores, gerentes de produto e arquitetos.

unidade de negócios de serviços de tecnologia da empresa (ETS) Olá fornece recursos de TI centralizado e gerencia vários centros de dados onde as unidades de negócios hospedam seus aplicativos. Juntamente com gerenciar datacenters Olá, hello organização ETS fornece e gerencia serviços de rede/telefonia e colaboração centralizada (por exemplo, email e sites). Eles também gerenciam cargas de trabalho voltadas para o cliente para unidades de negócios menores que não contam com equipe operacional.

Olá personas a seguir é usado neste tópico:

* Dave é o administrador do Azure ETS hello.
* Alice é diretor de desenvolvimento da Contoso na unidade de negócios de cadeia de fornecimento de saudação.

A Contoso deve aplicativo toobuild uma linha de negócios e um aplicativo voltado para o cliente. Ela decidiu toorun Olá aplicativos no Azure. Dave lê Olá [governança de assinatura prescritivas](resource-manager-subscription-governance.md) tópico, e está agora pronto tooimplement recomendações hello.

## <a name="scenario-1-line-of-business-application"></a>Cenário 1: aplicativo de linha de negócios
A Contoso está criando uma fonte código management system (BitBucket) toobe, usada por desenvolvedores em Olá, mundo.  aplicativo Hello usa infraestrutura como serviço (IaaS) para hospedagem e consiste em servidores web e um servidor de banco de dados. Os desenvolvedores acessar servidores em seus ambientes de desenvolvimento, mas eles não precisam acessar servidores toohello no Azure. A Contoso ETS aguarda o proprietário do aplicativo hello tooallow e aplicativo do team toomanage hello. aplicativo Hello só está disponível na rede corporativa da Contoso. Dave precisa tooset assinatura Olá para este aplicativo. assinatura de saudação também hospeda outros produtos relacionados ao desenvolvedor de software Olá futuras.  

### <a name="naming-standards--resource-groups"></a>Padrões de nomenclatura e grupos de recursos
Dave cria uma assinatura toosupport ferramentas de desenvolvedor que são comuns a todas as unidades de negócios hello. Ele precisa toocreate de nomes significativos para a assinatura de saudação e grupos de recursos (para o aplicativo hello e redes de saudação). Ele cria Olá grupos de recursos e a assinatura a seguir:

| Item | Nome | Descrição |
| --- | --- | --- |
| Assinatura |Produção de Ferramentas para Desenvolvedor de ETS da Contoso |Dá suporte a ferramentas de desenvolvedor comuns |
| Grupo de recursos |rgBitBucket |Contém Olá aplicativo servidor web e servidor de banco de dados |
| Grupo de recursos |rgCoreNetworks |Contém as redes virtuais hello e conexão de gateway site a site |

### <a name="role-based-access-control"></a>Controle de acesso baseado em função
Depois de criar sua assinatura, Dave quer tooensure que Olá equipes apropriadas e proprietários de aplicativos podem acessar seus recursos. Dave reconhece que cada equipe tem requisitos diferentes. Ele utiliza grupos de saudação que foram sincronizados de tooAzure de Active Directory (AD) local da Contoso do Active Directory e fornece o nível certo de saudação de equipes de toohello de acesso.

Dave atribui Olá funções para assinatura Olá a seguir:

| Função | Atribuído muito| Descrição |
| --- | --- | --- |
| [Proprietário](../active-directory/role-based-access-built-in-roles.md#owner) |ID Gerenciada do AD da Contoso |Essa ID é controlada com acesso JIT (Just in Time) por meio da ferramenta de Gerenciamento de Identidades da Contoso e garante que o acesso de proprietário de assinatura seja totalmente auditado. |
| [Gerenciador de Segurança](../active-directory/role-based-access-built-in-roles.md#security-manager) |Departamento de gerenciamento de riscos e de segurança |Esta função permite que usuários toolook em Olá Central de segurança do Azure e o status de saudação de recursos de saudação. |
| [Colaborador de rede](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Equipe de rede |Essa função permite tooSite de Site do hello da equipe para rede da Contoso toomanage VPN e Olá redes virtuais. |
| *Função personalizada* |Proprietário do aplicativo |Dave cria uma função que concede Olá capacidade toomodify recursos no grupo de recursos de saudação. Para obter mais informações, veja [Funções personalizadas no RBAC do Azure](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>Políticas
Dave tem Olá seguindo os requisitos para o gerenciamento de recursos na assinatura hello:

* Como as ferramentas de desenvolvimento de saudação oferecem suporte a desenvolvedores em Olá, mundo, ele não deseja que os usuários de tooblock de criação de recursos em qualquer região. No entanto, ele precisa tooknow onde os recursos são criados.
* Ele está preocupado com os custos. Portanto, ele quer tooprevent proprietários do aplicativo de criação de máquinas de virtuais desnecessariamente caras.  
* Como esse aplicativo serve desenvolvedores em várias unidades de negócios, ele quer tootag cada recurso com o proprietário da empresa Olá unidade e aplicativo. Usando essas marcas, ETS pode cobrar equipes de saudação apropriado.

Ele cria a seguinte Olá [políticas do Gerenciador de recursos](resource-manager-policy.md):

| Campo | Efeito | Descrição |
| --- | --- | --- |
| location |auditar |Criação de saudação de recursos de saudação em qualquer região de auditoria |
| type |deny |Negar a criação de máquinas virtuais da série G |
| marcas |deny |Exigir a marca do proprietário do aplicativo |
| marcas |deny |Exigir a marca do centro de custo |
| marcas |acrescentar |Acrescente o nome da marca **BusinessUnit** e o valor da marca **ETS** tooall recursos |

### <a name="resource-tags"></a>Marcações de recursos
Dave compreende que ele precisa obter informações específicas sobre o Centro de custo de saudação do hello fatura tooidentify toohave para implementação de BitBucket hello. Além disso, Dave deseja tooknow que todos Olá recursos ETS possui.

Ele adiciona a seguir Olá [marcas](resource-group-using-tags.md) toohello grupos de recursos e recursos.

| Nome da marca | Valor da marca |
| --- | --- |
| ApplicationOwner |nome de saudação da pessoa de saudação que gerencia este aplicativo. |
| CostCenter |Centro de custo de saudação do grupo de saudação que é pago para Olá consumo do Azure. |
| BusinessUnit |**ETS** (unidade de negócios Olá associada à assinatura Olá) |

### <a name="core-network"></a>Rede principal
Olá Contoso ETS propostas de informações que a equipe de gerenciamento de segurança e riscos revisões de Dave planejar toomove Olá aplicativo tooAzure. Quiserem tooensure aplicativo hello não é exposto toohello internet.  Dave também tem aplicativos de desenvolvedor que serão movido tooAzure em Olá futuras. Esses aplicativos exigem interfaces públicas.  toomeet esses requisitos, ele oferece redes virtuais internas e externas e um acesso de toorestrict de grupo de segurança de rede.

Ele cria Olá recursos a seguir:

| Tipo de recurso | Nome | Descrição |
| --- | --- | --- |
| Rede Virtual |vnInternal |Usado com hello BitBucket aplicativo e está conectado por meio da rede corporativa da rota expressa tooContoso.  Uma sub-rede (sbBitBucket) fornece um aplicativo hello com um espaço de endereço IP específico. |
| Rede Virtual |vnExternal |Disponível para futuros aplicativos que necessitem de pontos de extremidade públicos. |
| Grupo de Segurança de Rede |nsgBitBucket |Garante que Olá superfície de ataque dessa carga de trabalho é minimizado, permitindo conexões apenas na porta 443 para a sub-rede Olá onde o aplicativo hello reside (sbBitBucket). |

### <a name="resource-locks"></a>Bloqueios de recurso
Dave reconhece que a conectividade da rede corporativa toohello interno rede virtual Contoso Olá deve ser protegida de qualquer script wayward ou exclusão acidental.

Ele cria a seguinte Olá [bloqueio de recurso](resource-group-lock-resources.md):

| Tipo de bloqueio | Recurso | Descrição |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Impede que os usuários de rede virtual de saudação excluindo ou sub-redes, mas não impede a adição de saudação de novas sub-redes. |

### <a name="azure-automation"></a>Automação do Azure
Dave não tem nada tooautomate para este aplicativo. Embora ele tenha criado uma conta de automação do Azure, inicialmente ele não a usará.

### <a name="azure-security-center"></a>Central de Segurança do Azure
Gerenciamento de serviços de TI da Contoso precisa tooquickly identificar e tratar ameaças. Eles também desejam toounderstand os problemas que podem existir.  

toofulfill esses requisitos, Dave habilita Olá [Central de segurança do Azure](../security-center/security-center-intro.md)e fornece a função de Gerenciador de segurança do acesso toohello.

## <a name="scenario-2-customer-facing-app"></a>Cenário 2: aplicativo voltado ao cliente
liderança de negócios Olá na unidade de negócios de cadeia de fornecimento de saudação identificou vários contrato tooincrease de oportunidades com clientes da Contoso usando um cartão de fidelidade. Equipe de Alice deve criar esse aplicativo e decide Azure aumenta sua capacidade toomeet Olá necessidade de negócios. Alice funciona com Dave do ETS tooconfigure duas assinaturas para desenvolver e operacional este aplicativo.

### <a name="azure-subscriptions"></a>Assinaturas do Azure
Dave conecta toohello Azure Enterprise Portal e vê o que departamento de cadeia de fornecimento que Olá já existe.  No entanto, como esse projeto é Olá primeiro projeto de desenvolvimento para a equipe de cadeia de fornecimento de saudação no Azure, Dave reconhece Olá necessidade para uma nova conta para a equipe de desenvolvimento de Alice.  Ele cria a conta de "R & D" Olá para sua equipe e atribui acesso tooAlice. Alice conecta via Olá portal do Azure e cria duas assinaturas: servidores de desenvolvimento uma toohold saudação e servidores de produção uma toohold saudação.  Ela segue os padrões de nomenclatura Olá estabelecida anteriormente ao criar hello assinaturas a seguir:

| Uso de assinaturas | Nome |
| --- | --- |
| Desenvolvimento |SupplyChain ResearchDevelopment LoyaltyCard Desenvolvimento |
| Produção |SupplyChain Operações LoyaltyCard Produção |

### <a name="policies"></a>Políticas
Dave e Alice discutem o aplicativo hello e identificam o que esse aplicativo serve apenas os clientes na região norte-americano hello.  Alice e sua equipe planejar o ambiente de serviço de aplicativo e o aplicativo do Azure SQL toocreate hello toouse do Azure. Máquinas virtuais de toocreate talvez seja necessário durante o desenvolvimento.  Alice quer tooensure que seus desenvolvedores têm recursos de saudação precisam tooexplore e examine os problemas sem trazendo ETS.

Para Olá **assinatura desenvolvimento**, eles criam Olá política a seguir:

| Campo | Efeito | Descrição |
| --- | --- | --- |
| location |auditar |Criação de saudação de recursos de saudação em qualquer região de auditoria. |

Eles não limitar o tipo de saudação do sku, que um usuário pode criar em desenvolvimento, e não requerem marcas de recursos ou grupos de recursos.

Para Olá **assinatura de produção**, eles criam Olá políticas a seguir:

| Campo | Efeito | Descrição |
| --- | --- | --- |
| location |deny |Nega a criação de saudação de todos os recursos fora do data centers de saudação dos EUA. |
| marcas |deny |Exigir a marca do proprietário do aplicativo |
| marcas |deny |Requer a marca de departamento. |
| marcas |acrescentar |Anexe o grupo de recursos de tooeach marca que indica o ambiente de produção. |

Eles não limitam o tipo de saudação do sku, que um usuário pode criar em produção.

### <a name="resource-tags"></a>Marcações de recursos
Dave compreende que ele precisa toohave informações específicas tooidentify Olá corretos de negócios grupos para cobrança e de propriedade. Ele define as marcas de recurso para recursos e grupos de recursos.

| Nome da marca | Valor da marca |
| --- | --- |
| ApplicationOwner |nome de saudação da pessoa de saudação que gerencia este aplicativo. |
| department |Centro de custo de saudação do grupo de saudação que é pago para Olá consumo do Azure. |
| EnvironmentType |**Produção** (embora Olá assinatura inclui **produção** em nome hello, incluir essa marca permite identificação fácil ao examinar os recursos no portal de saudação ou na fatura hello.) |

### <a name="core-networks"></a>Redes principais
Olá Contoso ETS propostas de informações que a equipe de gerenciamento de segurança e riscos revisões de Dave planejar toomove Olá aplicativo tooAzure. Eles querem tooensure que Olá aplicativo do cartão de fidelidade corretamente é isolado e protegido em uma rede DMZ.  toofulfill esse requisito, Dave e Alice criar uma rede virtual externa e uma saudação de tooisolate de grupo de segurança de rede aplicativo do cartão de fidelidade da rede corporativa do hello Contoso.  

Para Olá **assinatura desenvolvimento**, eles criam:

| Tipo de recurso | Nome | Descrição |
| --- | --- | --- |
| Rede Virtual |vnInternal |Serve o ambiente de desenvolvimento do cartão de fidelidade Contoso hello e está conectado por meio da rede corporativa da rota expressa tooContoso. |

Para Olá **assinatura de produção**, eles criam:

| Tipo de recurso | Nome | Descrição |
| --- | --- | --- |
| Rede Virtual |vnExternal |Hospeda o aplicativo do cartão de fidelidade hello e não está conectado diretamente tooContoso's ExpressRoute. Código que é enviado por meio de seu sistema de código-fonte toohello diretamente os serviços de PaaS. |
| Grupo de Segurança de Rede |nsgBitBucket |Garante que Olá superfície de ataque dessa carga de trabalho é minimizado, permitindo que apenas a comunicação de entrada em TCP 443.  A Contoso também está investigando usando um Firewall do aplicativo Web para obter proteção adicional. |

### <a name="resource-locks"></a>Bloqueios de recurso
Dave e Alice confere e decidir tooadd bloqueios de recursos em alguns dos recursos chave Olá Olá ambiente tooprevent a exclusão acidental durante um envio de código errôneo.

Eles criam Olá bloqueio a seguir:

| Tipo de bloqueio | Recurso | Descrição |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |pessoas tooprevent de excluir a rede virtual hello ou sub-redes. bloqueio de saudação não evitar a adição de saudação do novas sub-redes. |

### <a name="azure-automation"></a>Automação do Azure
Alice e sua equipe de desenvolvimento têm ambiente de saudação toomanage runbooks extenso para este aplicativo. Olá runbooks permitem Olá adição ou exclusão de nós para o aplicativo hello e outras tarefas de DevOps.

toouse Esses runbooks, elas permitem [automação](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Central de Segurança do Azure
Gerenciamento de serviços de TI da Contoso precisa tooquickly identificar e tratar ameaças. Eles também desejam toounderstand os problemas que podem existir.  

toofulfill esses requisitos, Dave permite que a Central de segurança do Azure. Ele assegura que o hello Central de segurança do Azure está monitorando recursos hello e fornece acesso a equipes de segurança e DevOps toohello.

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como criar modelos do Gerenciador de recursos, consulte [práticas recomendadas para a criação de modelos do Azure Resource Manager](resource-manager-template-best-practices.md).

