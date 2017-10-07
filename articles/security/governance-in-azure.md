---
title: aaaGovernance no Azure | Microsoft Docs
description: "Saiba mais sobre os serviços que podem ser dimensionada para cima e automaticamente toomeet Olá às necessidades de seu aplicativo ou empresa e serviços de computação em nuvem que incluem uma ampla seleção de instâncias de computação."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Governança no Azure

Sabemos que a segurança é trabalho na nuvem hello e como é importante que você encontrar precisas e em tempo hábil de informações sobre a segurança do Azure. Um dos toouse de motivos melhor Azure Olá para seus aplicativos e serviços é tootake aproveitar sua ampla variedade de recursos e ferramentas de segurança. Essas ferramentas e recursos ajudam a tornar soluções seguras de possíveis toocreate na plataforma Azure segura de saudação.

toohelp que entender melhor matriz Olá de controles de governança implementado no Microsoft Azure de ambos os clientes de saudação e perspectivas as operações da Microsoft, neste artigo, "Governança no Azure", será gravado que fornece uma visão abrangente Olá Recursos de governança disponíveis com o Microsoft Azure.

## <a name="azure-platform"></a>Plataforma do Azure

O Azure é uma plataforma de serviço de nuvem pública que dá suporte a uma ampla seleção de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos. Ele pode executar contêineres do Linux com a integração com o Docker, criar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js e criar back-ends para dispositivos iOS, Android e Windows. Serviços de nuvem pública do Azure oferecem suporte a saudação tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiarem.

Quando você criar ou migra ativos de TI para, um provedor de serviços de nuvem pública que você depender de tooprotect de recursos da organização seus aplicativos e dados com controles de saudação e serviços Olá eles oferecem toomanage Olá segurança de seu baseado em nuvem ativos.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender aos requisitos de segurança. Além disso, você fornece muitas opções de segurança e toocontrol de capacidade de hello Azure-los para que você possa personalizar requisitos exclusivos de segurança toomeet Olá das implantações de sua organização.

Este documento ajudará você a entender como as funcionalidades do Governance do Azure podem ajudá-lo a atender a esses requisitos.

## <a name="abstract"></a>Resumo

Governança de nuvem do Microsoft Azure fornece uma auditoria integrada e a abordagem de consultoria para revisar e informando organizações no uso de saudação plataforma Windows Azure. Governança de nuvem do Microsoft Azure se refere a toohello processos de tomada de decisão, critérios e políticas envolvidas no planejamento hello, arquitetura, aquisição, implantação, operação e gerenciamento de uma nuvem de computação.

toocreate um plano para governança de nuvem do Microsoft Azure, você precisa tootake uma Visão aprofundada de saudação pessoas, processos e tecnologias em vigor no momento e, em seguida, estruturas de compilação que tornam mais fácil para IT tooconsistently dar suporte às necessidades de negócios, proporcionando final usuários com hello flexibilidade toouse Olá recursos avançados do Microsoft Azure.

Este documento descreve como você pode obter um nível elevado de governança de recursos de TI no Microsoft Azure. Este documento pode ajudá-lo a entender os recursos de segurança e controle de saudação internos tooMicrosoft do Azure.

Olá seguem problemas de controle principal Olá abordados neste documento:

- Implementação de políticas, processos e procedimentos de acordo com as metas da organização.

- Segurança e conformidade contínua com os padrões da organização

- Monitoramento e alertas

## <a name="implementation-of-policies-processes-and-procedures"></a>Implementação de políticas, processos e procedimentos 

Gerenciamento estabeleceu a implementação de toooversee funções e responsabilidades de política de segurança de informações de saudação e continuidade operacional no Azure. Gerenciamento do Microsoft Azure é responsável por supervisionar a segurança e as práticas de continuidade em suas respectivas equipes (incluindo terceiros) e facilitar a conformidade com padrões, processos e políticas de segurança.

Aqui estão os fatores de saudação à evolução:

- Provisionamento de conta de usuário

- Controles de assinatura

- Controle de Acesso Baseado em Função

- Gerenciamento de recursos

- Acompanhamento de recursos

- Controle de recursos críticos

- Acesso à API tooBilling informações

- Controles de rede

## <a name="account-provisioning"></a>Provisionamento de conta

Definindo a conta de hierarquia é uma etapa importante toouse e estrutura de serviços do Azure dentro de uma empresa e é a estrutura de governança de núcleo hello. No caso de clientes com contrato do enterprise hello, os clientes podem subdividir o ambiente de saudação em departamentos, contas e, finalmente, as assinaturas.

![Provisionamento de conta de usuário](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Se você não tiver um enterprise agreement, considere o uso de [marcas Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) na hierarquia de toodefine nível de assinatura. Uma assinatura do Azure é a unidade básica de saudação em que todos os recursos estão contidos. Ela também define vários limites dentro do Azure, como o número de núcleos, recursos, etc. As assinaturas podem conter [Grupos de Recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), que podem conter Recursos. Princípios [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) se aplicam nesses três níveis.

Cada empresa é diferente e hierarquia hello usando marcas do Azure no caso dos clientes corporativos não permite flexibilidade significativas em como o Azure é organizado dentro da empresa de saudação. Antes de implantar os recursos do Microsoft Azure, você deve hierarquia de modelo e entender Olá impacto na cobrança, o acesso a recursos e a complexidade.

## <a name="subscription-controls"></a>Controles de assinatura

Assinatura controla como o uso de recursos é relatado e cobrado. As assinaturas podem ser configuradas para cobrança e pagamento separados. Como mencionado anteriormente, em uma conta do Azure pode haver várias assinaturas. Assinaturas podem ser usadas toodetermine Olá recursos do Azure uso de vários departamentos em uma empresa.

Por exemplo, se uma empresa tiver departamentos de RH, TI e de Marketing e esses departamentos têm diferentes projetos em execução. Com base no uso de saudação de recursos do Azure como máquinas virtuais por cada departamento, eles podem ser cobrados de acordo. Por isso podemos controlar Finanças saudação de cada departamento.

As assinaturas do Azure estabelecem três parâmetros:

- uma ID exclusiva do assinante

- um local de cobrança

- Conjunto de recursos disponíveis

De um indivíduo, que inclui uma ID de conta da Microsoft, um cartão de crédito número e hello pacote completo do Azure services – embora, Microsoft impõe limites de consumo, dependendo do tipo de assinatura de saudação.

Hierarquias de registro do Azure definem como os serviços são estruturados dentro de um Contrato Empresarial. Olá Enterprise Portal permite que os clientes toodivide acessar tooAzure recursos associados com um Enterprise Agreement com base em necessidades específicas da organização de tooan personalizável hierarquias flexíveis. padrão de hierarquia Olá deve corresponder estrutura geográfica e gerenciamento de uma organização para que Olá associado cobrança e acesso a recursos com precisão pode ser considerado para.

padrões de alto nível Olá três são a unidade funcional, o business e departamentos geográficos, usando como uma construção administrativo para agrupamentos de conta. Dentro de cada departamento, contas podem ter assinaturas atribuídas, as quais criam silos de cobrança e vários limites de chave no Azure (por exemplo, o número de VMs, contas de armazenamento, etc.).

![Controles de assinatura](./media/governance-in-azure/security-governance-in-azure-fig2.png)


Para organizações com um Acordo Empresarial, as assinaturas do Azure seguem uma hierarquia de quatro níveis:

- administrador de registro corporativo

- administrador de departamento

- proprietário da conta

- Administrador de serviço

Essa hierarquia rege seguinte hello:

- Relação de cobrança

- Administração de conta

- Função tooartifacts de controle de acesso com base em (RBAC)

- Limites/limites

- Limites

  - Uso e cobrança (cartão de taxa baseada nos números de oferta)

  - limites

  - Rede Virtual

- Anexado too1 AAD (1 AAD ser associado a várias assinaturas)

- Conta de registro corporativo tooan associado

## <a name="role-based-access-controls"></a>Controle de acesso baseado em função

Quando o Azure foi inicialmente lançado, assinatura de tooa de controles de acesso foram básicos: administrador ou Coadministrador. Acesso tooa assinatura Olá clássico modelo implicado acesso tooall Olá recursos no portal de saudação. Esta falta de um controle refinado led toohello a proliferação de assinaturas tooprovide um nível de controle de acesso razoável para um registro do Azure.

![Controle de acesso baseado em função](./media/governance-in-azure/security-governance-in-azure-fig3.png)

Essa proliferação de assinaturas não é mais necessária. Com controle de acesso baseado em função, você pode atribuir usuários a funções toostandard (como "leitor" comuns e tipos de "escritor" de funções). Você também pode definir funções personalizadas.

O [Controle De Acesso Baseado Em Função do Azure (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) permite o gerenciamento de acesso refinado para o Azure. Usando o RBAC, você pode conceder somente a quantidade Olá de acesso que os usuários precisam tooperform seus trabalhos. As empresas orientadas a segurança devem se concentrar em fornecendo aos funcionários permissões exatas de saudação que precisam. Número excessivo de permissões expor um tooattackers de conta. Permissões insuficientes fazem com que os funcionários não consigam trabalhar com eficiência. O RBAC (controle de acesso baseado em função) do Azure ajuda a resolver esse problema ao oferecer o gerenciamento de acesso refinado para o Azure. RBAC ajuda toosegregate tarefas dentro de sua equipe e conceda apenas Olá quantidade de toousers de acesso que eles precisam tooperform seus trabalhos. Em vez de apresentar todos irrestrito permissões em sua assinatura do Azure ou recursos, você pode permitir apenas determinadas ações.

Por exemplo, use RBAC toolet um funcionário gerenciar máquinas virtuais em uma assinatura, enquanto outro pode gerenciar bancos de dados SQL em Olá mesma assinatura.

RBAC do Azure tem três funções básicas que se aplicam a tipos de recurso de tooall:

- **Proprietário** tem acesso completo tooall recursos incluindo Olá toodelegate direito acesso tooothers.

- **Colaborador** pode criar e gerenciar todos os tipos de recursos do Azure, mas não é possível conceder acesso tooothers.

- **leitor** pode exibir os recursos existentes do Azure.

rest Olá das funções de RBAC hello Azure permitir o gerenciamento de recursos do Azure específicos. Por exemplo, hello função Colaborador da máquina Virtual permite Olá toocreate de usuário e gerenciar máquinas virtuais. Ele não oferece a eles acesso a rede virtual toohello ou sub-rede Olá Olá máquina virtual se conecta ao.

[Funções internas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) listas Olá funções disponíveis no Azure. Especifica operações hello e escopo de cada função interna concede toousers.

Conceda acesso atribuindo Olá apropriado RBAC função toousers, grupos e aplicativos em um determinado escopo. escopo de saudação de uma atribuição de função pode ser uma assinatura, um grupo de recursos ou um único recurso. Uma função atribuída a um escopo pai também concede acesso toohello filhos contidos nele.

Por exemplo, um usuário com o grupo de recursos do acesso tooa pode gerenciar todos os recursos de saudação contém, como sites, máquinas virtuais e sub-redes.

RBAC do Azure somente dá suporte a operações de gerenciamento de recursos do Azure de Olá Olá portal do Azure e APIs do Gerenciador de recursos do Azure. Ele não pode autorizar todas as operações no nível de dados para os recursos do Azure. Por exemplo, você pode autorizar alguém toomanage contas de armazenamento, mas não toohello blobs ou tabelas em uma conta de armazenamento não podem. Da mesma forma, um banco de dados SQL pode ser gerenciado, mas não Olá tabelas dentro dele.

Se você quiser saber mais sobre como o RBAC ajuda você a gerenciar o acesso, confira [O que é Controle de Acesso Baseado em Função](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).

Você também pode [criar uma função personalizada](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) no acesso de RBAC (controle) se nenhuma das funções internas Olá atender seu acesso específico precisa. Funções personalizadas podem ser criadas usando [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure Interface de linha de comando (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli)e hello [API REST](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Assim como funções internas, funções personalizadas podem ser atribuídas toousers, grupos e aplicativos na assinatura, no grupo de recursos e escopos do recurso.

Dentro de cada assinatura, você pode conceder a too2000 atribuições de função.

## <a name="resource-management"></a>Gerenciamento de recursos

Somente o modelo de implantação clássico Olá originalmente fornecido pelo Azure. Nesse modelo, cada recurso existia independentemente; havia uma maneira toogroup recursos relacionados juntos. Em vez disso, você precisava toomanually controlar quais recursos constituídos de seu aplicativo ou solução e lembre-se de toomanage-los em uma abordagem de coordenada.

toodeploy uma solução, você precisava tooeither criar cada recurso individualmente por meio do portal clássico do hello ou criar um script que todos os recursos de saudação na ordem correta, Olá implantados. toodelete uma solução, você precisava toodelete cada recurso individualmente. Não era possível aplicar e atualizar facilmente políticas de controle de acesso para recursos relacionados. Por fim, você não pode aplicar marcas tooresources toolabel-los com os termos que ajudarão-lo a monitoram seus recursos e gerenciar cobrança.

No 2014, o Azure introduziu o Gerenciador de recursos, que adicionado o conceito de saudação de um grupo de recursos. Um grupo de recursos é um contêiner de recursos que compartilham um ciclo de vida comum. modelo de implantação do Gerenciador de recursos de saudação oferece várias vantagens:

- Você pode implantar, gerenciar e monitorar todos os serviços de saudação para sua solução como um grupo, em vez de manipular esses serviços individualmente.

- Você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente.

- Você pode aplicar os recursos de tooall de controle de acesso em seu grupo de recursos, e essas políticas são aplicadas automaticamente quando novos recursos são adicionados toohello grupo de recursos.

- Você pode aplicar marcas tooresources toologically organizar todos os recursos de saudação em sua assinatura.

- Você pode usar a infraestrutura de saudação toodefine notação JSON (JavaScript Object) para sua solução. arquivo JSON de saudação é conhecido como um modelo do Gerenciador de recursos.

- Você pode definir dependências de saudação entre os recursos para que eles são implantados na ordem correta, Olá.

![Gerenciamento de recursos](./media/governance-in-azure/security-governance-in-azure-fig4.png)

Gerenciador de recursos permite que você tooput recursos em grupos significativos para afinidade de cobrança ou natural de gerenciamento. Conforme mencionado anteriormente, o Azure tem dois modelos de implantação. Em Olá anteriormente [modelo clássico](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), unidade básica de saudação de gerenciamento foi assinatura hello. Era difícil toobreak recursos dentro de uma assinatura, o que levou toohello criação de um grande número de assinaturas. Com o modelo do Gerenciador de recursos de hello, vimos Introdução Olá de grupos de recursos.

Um grupo de recursos é um contêiner que mantém os recursos relacionados a uma solução do Azure. [grupo de recursos de saudação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) pode incluir todos os recursos de saudação para solução hello, ou apenas os recursos que você deseja toomanage como um grupo. Decidir como deseja que os recursos de tooallocate tooresource grupos com base no que torna hello mais sentido para sua organização.

Para recomendações sobre modelos, consulte [Práticas recomendadas para criar modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

Gerenciador de recursos do Azure analisa dependências tooensure recursos são criados na ordem correta hello. Se um recurso depende de um valor de outro recurso (como uma máquina virtual que precisa de uma conta de armazenamento para discos), você pode definir uma dependência.

>[!Note]
>Para saber mais, confira [Definindo as dependências nos modelos do Gerenciador de Recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies).

Você também pode usar o modelo de saudação de infraestrutura de atualizações de toohello. Por exemplo, você pode adicionar uma solução de tooyour de recursos e adicionar as regras de configuração para os recursos de saudação que já foram implantados. Se o modelo de saudação especifica criando um recurso, mas esse recurso já existe, o Gerenciador de recursos do Azure executa uma atualização em vez de criar um novo ativo. Azure Resource Manager atualizações Olá existente ativo toohello mesmo estado que seria como novo.

Gerenciador de recursos fornece extensões para cenários quando precisar de operações adicionais, como ao instalar o software que não está incluído na instalação de saudação.

## <a name="resource-tracking"></a>Acompanhamento de recursos

Como os usuários em sua organização Adicionar assinatura de recursos de toohello, torna-se recursos tooassociate cada vez mais importante com o departamento apropriado hello, o cliente e o ambiente. Você pode anexar tooresources metadados por meio de marcas. Você usa [marcas](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide informações sobre recursos de saudação ou proprietário de saudação. As marcas permitem que você toonot apenas agregação e recursos do grupo de várias maneiras, mas usam esses dados para fins de saudação de estorno.

Use marcas quando você tiver um conjunto complexo de grupos de recursos e recursos e precisa toovisualize esses ativos de maneira de saudação que torne Olá tooyou de mais sentido. Por exemplo, você pode marcar os recursos que servem para uma função semelhante em sua organização ou pertencem toohello mesmo departamento.

Sem marcas, os usuários em sua organização podem criar vários recursos que podem ser toolater difícil identificam e gerenciar. Por exemplo, você poderá toodelete todos os recursos de saudação para um projeto. Se esses recursos não estão marcados para projeto hello, você deve encontrá-los manualmente. Marcação pode ser uma maneira importante para você tooreduce um custo desnecessário em sua assinatura.

Recursos não é necessário tooreside em Olá tooshare de grupo de recursos mesmo uma marca. Você pode criar seu próprios tooensure taxonomia de marca que todos os usuários em sua organização usam marcas comum em vez de usuários a aplicação acidental de marcas ligeiramente diferentes (por exemplo, "Departamento" em vez de "Departamento").

Políticas de recursos permitem que você toocreate as regras padrão para sua organização. Você pode criar políticas que certifique-se de que recursos estão marcados com valores apropriados hello.

> [!Note]
> Para obter mais informações, consulte [Aplicar políticas de recursos para marcas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

Você também pode exibir recursos marcados por meio de saudação portal do Azure.

Olá [relatório de uso](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) para sua assinatura inclui nomes de marca e valores, que permite que você toobreak os custos por marcas.

> [!Note]
> Para obter mais informações sobre marcas, consulte [usando marcas tooorganize seus recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

Olá seguintes limitações se aplicam a tootags:

- Cada recurso ou grupo de recursos pode ter um máximo de 15 pares chave/valor de marca. Essa limitação se aplica somente tootags diretamente aplicadas toohello recurso grupo ou recurso. Um grupo de recursos pode conter muitos recursos que possuem 15 pares de chave/valor de marca.

- o nome da marca Olá é limitado too512 caracteres.

- valor de marca de saudação é limitado too256 caracteres.

- Grupo de recursos de toohello marcas aplicadas não são herdadas pelos recursos de saudação desse grupo de recursos.

Se você tiver mais de 15 valores que você precisa tooassociate com um recurso, use uma cadeia de caracteres JSON para o valor de marca hello. saudação de cadeia de caracteres JSON pode conter muitos valores que são aplicadas tooa marca única chave.

### <a name="tags-and-billing"></a>Marcas e cobrança

Marcas permitem que você toogroup seus dados de cobrança. Por exemplo, se você estiver executando várias VMs para organizações diferentes, use Olá marcas toogroup uso pelo Centro de custo. Você também pode usar marcas toocategorize custos pelo ambiente de tempo de execução. Olá, como o uso de cobrança para VMs em execução no ambiente de produção.

Você pode recuperar informações sobre marcas por meio de saudação [uso de recursos do Azure e APIs RateCard](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) ou arquivo de valores separados por vírgulas (CSV) de uso de saudação. Baixar o arquivo de uso de saudação do hello [portal de contas do Azure](https://account.windowsazure.com/) ou [portal EA](https://ea.azure.com/).

>[!Note]
> Para obter mais informações sobre toobilling acesso programático, consulte [obter ideias sobre o consumo de recursos do Microsoft Azure](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). Para operações de API REST, confira [Referência da API REST de cobrança do Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Quando você baixar uso Olá CSV para serviços que oferecem suporte a marcas de cobrança, marcas hello serão exibidos na coluna de marcas de saudação.

## <a name="critical-resource-controls"></a>Controle de recursos críticos

Como sua organização adiciona a assinatura do core services toohello, ele se torna tooensure cada vez mais importante que esses serviços são interrupção dos negócios de tooavoid disponíveis. [Bloqueios de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) permitem operações de toorestrict nos recursos de alto valor onde sua modificação ou exclusão teria um impacto significativo sobre os aplicativos ou infraestrutura de nuvem. Você pode aplicar a assinatura de tooa de bloqueios, o grupo de recursos ou o recurso. Normalmente, você pode aplicar bloqueios toofoundational recursos, como redes virtuais, gateways e contas de armazenamento.

Atualmente, os Bloqueios de recursos aceitam dois valores: CanNotDelete e ReadOnly. CanNotDelete significa que os usuários (com os direitos apropriados de saudação) podem ainda ler ou modificar um recurso, mas não é possível excluí-lo. ReadOnly significa que usuários autorizados não podem excluir nem modificar um recurso.

Bloqueios de Gerenciador de recursos se aplicam somente toooperations que acontecem no plano de gerenciamento hello, que consiste em operações enviadas muito<https://management.azure.com>. bloqueios Olá não restringem como recursos de executam suas próprias funções. Alterações de recursos são restritas, mas as operações de recursos não são restritas. Por exemplo, um bloqueio de somente leitura em um banco de dados SQL impede a exclusão ou modificação de banco de dados hello, mas ele não impedem que você criar, atualizar ou excluir dados no banco de dados de saudação.

Aplicando **ReadOnly** pode levar a resultados de toounexpected porque algumas operações que parecerem leitura operações exigem ações adicionais. Por exemplo, colocando uma **ReadOnly** bloqueio em uma conta de armazenamento impede que todos os usuários listando chaves hello. lista de saudação operação de chaves é tratada por meio de uma solicitação POST como Olá retornado chaves estão disponíveis para operações de gravação.

![Controle de Recursos Críticos](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Outro exemplo, colocar um bloqueio de somente leitura em um recurso de serviço de aplicativo impede que o Visual Studio Server Explorer exibindo arquivos de recurso Olá porque essa interação requer acesso de gravação.

Ao contrário de controle de acesso baseado em função, você pode usar bloqueios de gerenciamento tooapply uma restrição em todos os usuários e funções. toolearn sobre como configurar permissões para usuários e funções, consulte [controle de acesso baseado em função do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Quando você aplica um bloqueio em um escopo pai, todos os recursos nesse escopo herdam Olá mesmo bloqueio. Recursos até que você adicionar posteriormente herdam bloqueio de saudação do pai de saudação. bloqueio de Hello mais restritivo em herança Olá terá precedência.

bloqueios de gerenciamento toocreate ou delete, você deve ter acesso tooMicrosoft.Authorization/ _ou Microsoft.Authorization/locks/_ ações. De saudação funções internas, apenas **proprietário** e **administrador de acesso do usuário** recebem essas ações.

## <a name="api-access-toobilling-information"></a>Informações de toobilling de acesso de API

Use dados de uso e recursos de toopull de APIs de cobrança do Azure em suas ferramentas de análise de dados preferencial. Olá uso de recursos do Azure e APIs RateCard podem ajudá-lo a prever com precisão e gerenciar os custos. Olá APIs são implementadas como um provedor de recursos e a parte da família de saudação de APIs expostas pelo hello Azure Resource Manager.

### <a name="azure-resource-usage-api-preview"></a>API de uso de recursos do Azure (visualização)

Saudação de uso do Azure [API de uso do recurso](https://msdn.microsoft.com/library/azure/mt219003) tooget seus dados de consumo do Azure previsto. Olá API inclui:

- **Controle de acesso baseado em função do Azure** -configurar o acesso de políticas em Olá [portal do Azure](https://portal.azure.com/) ou por meio [cmdlets do PowerShell do Azure](https://docs.microsoft.com/powershell/azure/overview) toospecify quais usuários ou aplicativos pode obter acesso dados de uso da assinatura toohello. Os chamadores devem usar tokens padrão do Azure Active Directory para autenticação. Adicione Olá chamador tooeither Olá leitor de cobrança, leitor, proprietário ou colaborador função tooget acesso toohello dados de uso de uma assinatura do Azure específica.

- **Agregações diárias ou por hora** - os chamadores podem especificar se eles desejam seus dados de uso do Azure em buckets por hora ou buckets diários. saudação padrão é diário.

- **Metadados de instância (inclui as marcas de recurso)** – obter os detalhes de nível de instância como Olá uri de recurso totalmente qualificado (/subscriptions/ {id da assinatura} /...), Olá informações do grupo de recursos e as marcas de recurso. Esses metadados ajudam determinística e alocar programaticamente o uso por marcas hello, para casos de uso como a carga entre.

- **Metadados do recurso** -detalhes de recursos, como o nome de medidor hello, medidor categoria, subcategoria do medidor, unidade e região fornecem chamador Olá uma melhor compreensão sobre o que foi consumido. Também estamos trabalhando terminologia de metadados do recurso tooalign em Olá portal do Azure, uso do Azure CSV, EA CSV, de cobrança e outras experiências voltado ao público, toolet correlacionar dados em experiências.

- **Uso para todos os tipos de oferta** – os dados de uso estão disponíveis para todos os tipos de oferta, assim como pré-pago, MSDN, investimento e crédito monetário e EA.

**API RateCard de Recursos do Azure (visualização)**

Use hello Azure recurso RateCard API tooget Olá a lista de recursos do Azure disponíveis e estimado informações de preços para cada um. Olá API inclui:

- **Controle de acesso baseado em função do Azure** - configurar as políticas de acesso em Olá portal do Azure ou por meio de toospecify de cmdlets do PowerShell do Azure que os usuários ou aplicativos podem obter acesso toohello RateCard dados. Os chamadores devem usar tokens padrão do Azure Active Directory para autenticação. Adicione Olá chamador tooeither Olá leitor, proprietário ou colaborador função tooget acesso toohello dados de uso para uma determinada assinatura do Azure.

- **Suporte para pré-pago, MSDN, ofertas de investimento e crédito monetário (EA não tem suporte)** – Esta API fornece informações de taxa no nível da oferta do Azure. o chamador Olá desta API deve passar em taxas e detalhes do recurso Olá oferta informações tooget. Estamos taxas EA tooprovide atualmente não é possível porque o EA oferece personalizou taxas por registro. Aqui estão alguns dos cenários de saudação possibilitado com combinação Olá Olá uso e hello RateCard APIs:

- **Gastos do Azure durante o mês de saudação** -combinação de saudação do uso de Olá RateCard APIs e uso tooget melhor compreensão sobre sua nuvem gastar durante o mês de saudação. Você pode analisar Olá por hora e estimativas de buckets diárias de uso e cobrança.

- **Configurar alertas** – Use Olá uso e hello tooget RateCard APIs estimada consumo de nuvem e encargos e configurar alertas com base em recursos ou monetários com base em.

- **Prever fatura** – obter seu consumo previsto e a nuvem gastam e aplicam toopredict de algoritmos de aprendizado que fatura Olá seria final Olá Olá ciclo de cobrança de máquina.

- **Análise de custo de pré-consumo de** – Use Olá RateCard API toopredict quanto sua fatura seria para seu uso esperado quando você move o tooAzure de cargas de trabalho. Se você tiver cargas de trabalho existentes em outras nuvens ou nuvens privadas, você também pode mapear seu uso com hello Azure taxas tooget gastam uma estimativa melhor do Azure. Isso proporciona estimativa Olá capacidade toopivot na oferta e comparar entre tipos de oferta diferente Olá além pré-pago, como o investimento e crédito monetário. Olá API também lhe Olá capacidade toosee custo as diferenças por região e permite que você toodo um toohelp de análise de custo e se você tomar decisões de implantação.

- **Uma análise hipotética** -você pode determinar se ele é mais econômico toorun cargas de trabalho em outra região, ou em outra configuração de saudação recursos do Azure. Recursos do Azure, os custos podem ser diferentes com base em Olá região do Azure que você está usando.

- Você também pode determinar se outro tipo de oferta do Azure oferece uma melhor taxa em um recurso do Azure.

## <a name="networking-controls"></a>Controles de rede

Tooresources de acesso pode ser interno (dentro da rede da empresa Olá) ou externos (por meio de Olá da internet). É fácil para os usuários de sua tooinadvertently de organização colocar recursos no lugar errado Olá e potencialmente abri-los toomalicious acesso. Assim como no local / dispositivos, as empresas devem adicionar tooensure controles apropriados que usuários do Azure decisões saudação à direita.

![Controles de rede](./media/governance-in-azure/security-governance-in-azure-fig6.png)

Para governança da assinatura, identificamos recursos principais que fornecem controle básico de acesso. recursos principais de saudação consistem em:

### <a name="network-connectivity"></a>Conectividade de rede

[Redes virtuais](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) são objetos de contêiner para sub-redes. Embora não seja estritamente necessário, ele geralmente é usado ao se conectar a recursos corporativos de toointernal de aplicativos. Olá ativa do serviço de rede Virtual do Azure toosecurely você se conectar a recursos do Azure tooeach outros com redes virtuais (VNets).

Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de saudação nuvem do Azure dedicado tooyour assinatura. Você também pode se conectar a rede de local de tooyour VNets.

Os seguintes são os recursos para redes virtuais do Azure:

- **Isolamento**: as VNets são isoladas umas das outras. Você pode criar VNets separadas para o desenvolvimento, teste e produção Olá que use blocos de endereços CIDR mesmo. Por outro lado, você pode criar várias VNets que usam blocos de endereço CIDR diferentes e conectam as redes. Você pode segmentar uma VNet em várias sub-redes. O Azure fornece resolução de nome interno para VMs e instâncias de função de serviços de nuvem conectados tooa VNet. Opcionalmente, você pode configurar uma rede virtual toouse seus próprios servidores DNS, em vez de usar a resolução de nome interno do Azure.

- **Conectividade com a Internet**: instâncias de função de todas as máquinas virtuais (VM) do Azure e serviços de nuvem tiver conectado tooa VNet acessam toohello da Internet, por padrão. Você também pode habilitar recursos de toospecific de acesso de entrada, conforme necessário.

- **Conectividade de recursos do Azure**: recursos do Azure, como serviços de nuvem e máquinas virtuais podem ser conectado toohello mesma rede virtual. recursos de saudação podem se conectar a outros tooeach usando privada endereços IP, mesmo que eles estejam em sub-redes diferentes. O Azure fornece o roteamento padrão entre sub-redes, VNets e redes locais, para que você não tem tooconfigure e gerencie rotas.

- **Conectividade de rede virtual**: VNets pode ser conectado tooeach outras, permitindo que recursos conectado tooany VNet toocommunicate com qualquer recurso em qualquer outra VNet.

- **Conectividade local**: VNets podem ser redes locais tooon conectados por meio de conexões de rede privada entre sua rede e o Azure, ou uma conexão de VPN site a site over Olá da Internet.

- **Filtragem de tráfego**: o tráfego de rede de instâncias de função de VMs e do Serviços de Nuvem pode ser filtrado na entrada e na saída pelo endereço IP e porta de origem, endereço IP e porta de destino e protocolo.

- **Roteamento**: opcionalmente, você pode substituir o roteamento padrão do Azure configurando suas próprias rotas ou usando rotas BGP por meio de um gateway de rede.

## <a name="network-access-controls"></a>Controles de acesso à rede

[Grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) são como um firewall e fornecer regras para como um recurso pode "falar" rede hello. Eles fornecem controle granular sobre como / se uma sub-rede (ou máquina virtual) pode se conectar toohello Internet ou outras sub-redes em Olá mesmo rede virtual.

Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede conectados a redes virtuais do tooAzure (VNet). Os NSGs podem ser associados toosubnets, VMs individuais (clássico) ou interfaces de rede individuais (NIC) anexado tooVMs (Gerenciador de recursos).

Quando um NSG está associado tooa sub-rede, regras de saudação aplicam tooall recursos toohello conectado sub-rede. O tráfego pode ser restringido ainda mais associando também tooa um NSG VM ou NIC.

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Segurança e conformidade contínua com os padrões da organização

Cada empresa tem diferentes necessidades e todo negócio obterá distintos benefícios das soluções de nuvem. Ainda assim, os clientes de todos os tipos têm Olá mesmas preocupações básicas sobre como mover toohello nuvem. Eles querem tooretain controle de seus dados, e que desejam que toobe dados mantido seguros e privada, tudo isso mantendo transparência e conformidade.

O que os clientes desejam de provedores de nuvem é:

- **Proteger nossos dados** enquanto confirmar que a nuvem Olá pode fornecer maior segurança de dados e controle administrativo, líderes de TI ainda se preocupam que migrar nuvem de toohello deixá-los mais vulneráveis toohackers que atual soluções internas.

- **Manter nossos dados** serviços de Nuvem privados aumentam desafios de privacidade única para empresas. Como as empresas parecer toohello nuvem toosave nos custos de infraestrutura e melhorar sua flexibilidade, eles também se preocupar sobre perder o controle de onde seus dados estão armazenados, quem os está acessando e como é usado.

- **Forneça controle** mesmo que se beneficiam da saudação nuvem toodeploy mais soluções inovadoras, as empresas são muito preocupadas perder o controle de seus dados. divulgações de saudação recente dos órgãos do governo acessando dados do cliente, por meio de legal e muito legal, fazer com que alguns CIOs cautela ao armazenar seus dados na nuvem de saudação.

- **Promover a transparência** enquanto o controle, privacidade e segurança são importantes toobusiness responsáveis pelas decisões, eles também querem capacidade Olá tooindependently verificar como os seus dados estão armazenados, acessados e protegidos.

- **Manter a conformidade** como as empresas ampliam o uso de tecnologias de nuvem, Olá complexidade e o escopo dos padrões e normas continuam tooevolve. As empresas precisam tooknow que seus padrões de conformidade serão atendidos e essa conformidade evoluirá como regulamentos alteração ao longo do tempo.

## <a name="security-configuration-monitoring-and-alerting"></a>Configuração de segurança, monitoramento e alertas

Os assinantes do Azure podem gerenciar ambientes de nuvem de vários dispositivos, incluindo estações de trabalho, computadores de desenvolvedores e até mesmo dispositivos de usuário final com privilégios que têm permissões de tarefas específicas. Em alguns casos, as funções administrativas são executadas por meio de consoles baseado na web como Olá portal do Azure. Em outros casos, pode haver tooAzure conexões diretas de sistemas locais através de redes virtuais privadas (VPNs), os serviços de Terminal, protocolos de cliente de aplicativo ou (programaticamente) Olá API de gerenciamento de serviço do Azure (SMAPI). Além disso, os pontos de extremidade do cliente podem ser unidos ao domínio ou isolados e não gerenciados, como tablets ou smartphones.

Embora vários recursos de gerenciamento e acesso fornecem um conjunto avançado de opções, essa variação pode adicionar implantação de nuvem tooa risco significativo. Pode ser difícil toomanage, controlar e auditar as ações administrativas. Essa variação também pode introduzir ameaças de segurança por meio de acesso irregular tooclient os pontos de extremidade que são usados para gerenciar os serviços de nuvem. O uso de estações de trabalho pessoais ou gerais para desenvolvimento e gerenciamento de infraestrutura abre vetores de ameaça imprevisíveis, como navegação na Web (por exemplo, ataques do tipo "watering hole") ou email (por exemplo, engenharia social e phishing).

Monitoramento, log e auditoria fornecem uma base para acompanhamento e Noções básicas sobre atividades administrativas, mas não pode ser sempre viável tooaudit todas as ações em Concluir detalhes devido toohello quantidade de dados gerados. A auditoria de eficácia Olá das políticas de gerenciamento de saudação é uma prática recomendada, no entanto.

Governança de segurança do Azure do AD DS GPOs toocontrol Windows todos os administradores Olá interfaces, como compartilhamento de arquivos. Inclua as estações de trabalho de gerenciamento em processos de auditoria, monitoramento e registro em log. Acompanhe todo o acesso e uso de administradores e desenvolvedores.

### <a name="azure-security-center"></a>Central de Segurança do Azure

Olá [Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) fornece uma visão central do status de segurança de saudação de recursos em assinaturas hello e fornece recomendações que ajudam a evitar o comprometimento de recursos. Ele pode habilitar políticas mais granulares (por exemplo, aplicando políticas toospecific grupos de recursos que permitem Olá enterprise tootailor o risco de toohello postura está tratando).

![Central de Segurança do Azure](./media/governance-in-azure/security-governance-in-azure-fig7.png)

O Centro de Segurança permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança. Depois de habilitar [políticas de segurança](https://docs.microsoft.com/azure/security-center/security-center-policies) para recursos de uma assinatura, Central de segurança analisa a segurança do hello de seus recursos tooidentify as vulnerabilidades potenciais. Informações sobre a configuração de rede estão disponíveis imediatamente.

Central de Segurança do Azure representa uma combinação de análise de melhor prática e gerenciamento de política de segurança para todos os recursos dentro de uma assinatura do Azure. Essa ferramenta toouse poderoso e fácil permite que as equipes de segurança e tooprevent de gerentes de risco, detectar e responder a ameaças toosecurity conforme ele coleta e analisa dados de segurança de seus recursos do Azure, rede hello e soluções de parceiros como automaticamente programas antimalware e firewalls.

Além disso, a Central de segurança do Azure se aplica a análise avançada, incluindo análise comportamental e aprendizado de máquina e aproveitar a inteligência de ameaça global da Microsoft hello produtos e serviços, Olá Microsoft Digital Crimes unidade (DCU), Microsoft Security Response Center (MSRC) e feeds externos. [Governança de segurança](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) podem ser aplicadas em larga escala no nível de assinatura de saudação ou reduzida toospecific, requisitos granular aplicados tooindividual recursos por meio da definição de política.

Por fim, Central de segurança do Azure analisa a integridade dos recursos de segurança com base nessas políticas e usa esse painéis de criteriosos tooprovide e tentativas de alerta de eventos, como detecção de malware ou conexão de IP mal-intencionado.

>[!Note]
> Para obter mais informações sobre como tooapply recomendações, ler [implementar recomendações de segurança na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Central de segurança coleta dados de suas máquinas virtuais tooassess seu estado de segurança, forneça recomendações de segurança e alertá-lo toothreats. Quando você acessa pela primeira vez a Central de Segurança, a coleta de dados é habilitada em todas as máquinas virtuais em sua assinatura. Coleta de dados é recomendada, mas você pode recusar por [desabilitar a coleta de dados](https://docs.microsoft.com/azure/security-center/security-center-faq) no hello política Central de segurança.

Finalmente, a Central de segurança do Azure é uma plataforma aberta que permite que parceiros da Microsoft e software de toocreate de fornecedores independentes de software que se conecta à Central de segurança do Azure tooenhance seus recursos.

Central de segurança do Azure monitora hello Azure recursos a seguir:

- Máquinas virtuais (VMs) (incluindo os Serviços de Nuvem)

- Redes Virtuais do Azure

- Serviço do SQL Azure

- Soluções de parceiros integradas com sua assinatura do Azure, como um firewall de aplicativo Web em VMs e no [Ambiente do Serviço de Aplicativo](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme).

### <a name="operations-management-suite"></a>Operations Management Suite

Olá desenvolvimento de software do OMS e segurança de informações da equipe de serviço e [programa de governança](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) dá suporte a seus requisitos de negócios e adota toolaws e os regulamentos, conforme descrito em [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) e [Microsoft Trust Center conformidade](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). Como o OMS estabelece os requisitos de segurança, identifica os controles de segurança, gerencia e monitora os riscos também são descritos lá. Anualmente, revisamos as políticas, padrões, procedimentos e diretrizes.

Cada membro de equipe de desenvolvimento do OMS recebe treinamento formal sobre a segurança de aplicativo. Internamente, usamos um sistema de controle de versão para o desenvolvimento de software. Cada projeto de software é protegido pelo sistema de controle de versão de saudação.

A Microsoft tem uma equipe de segurança e conformidade que monitora e analisa todos os serviços na Microsoft. Gerentes de segurança de informações Olá equipe e não estão associados com hello engenharia departamentos que desenvolve OMS. os responsáveis pela segurança de saudação têm seu próprios cadeia de gerenciamento e conduzir independentes avaliações de conformidade e segurança tooensure dos serviços e produtos.

Operations Management Suite (também conhecido como o OMS) é uma coleção de serviços de gerenciamento que foram criados na nuvem de saudação do início da saudação. Em vez de implantar e gerenciar recursos locais, os componentes do OMS estão totalmente hospedados no Azure. A configuração é mínima e você pode ter tudo funcionando literalmente em questão de minutos.

![Pacote do Operations Manager](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Só porque os serviços OMS são executados em nuvem Olá não significa que eles não podem gerenciar efetivamente seu ambiente local.

Colocar um agente em qualquer Windows ou computador Linux no seu data center e enviará dados tooLog Analytics onde ele pode ser analisado junto com todos os outros dados coletados da nuvem ou em serviços locais. Use a nuvem de saudação tooleverage Backup do Azure e o Azure Site Recovery para backup e alta disponibilidade para recursos locais.

Runbooks na nuvem Olá normalmente não é possível acessar os recursos locais, mas você pode instalar um agente em um ou mais computadores muito que hospedará os runbooks em seu data center. Quando você inicia um runbook, você simplesmente Especifica se você deseja que ele toorun na nuvem hello, ou em um local de trabalho.

funcionalidade de núcleo de saudação do OMS é fornecida por um conjunto de serviços que são executados no Azure. Cada serviço fornece uma função de gerenciamento específico, e você pode combinar os cenários de gerenciamento diferente de tooachieve de serviços.

![Pacote do Operations Manager](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Gerenciador de operação do Azure estende suas funcionalidades fornecendo soluções de gerenciamento. [Soluções de gerenciamento](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) são conjuntos de lógica pré-empacotados que implementam um cenário de gerenciamento específico utilizando um ou mais serviços do OMS.

![Gerenciamento de operação do Azure](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Soluções diferentes estão disponíveis da Microsoft e de parceiros que você pode adicionar facilmente tooyour assinatura do Azure tooincrease Olá valor seu investimento do OMS.

Como parceiro, você pode criar sua próprias soluções toosupport seus aplicativos e serviços e fornecê-los toousers por meio de saudação do Azure Marketplace ou modelos de início rápido.

## <a name="performance-alerting-and-monitoring"></a>Desempenho do monitoramento e alertas

### <a name="alerting"></a>Alertas

Os alertas são um método para monitorar as métricas do recurso do Azure, eventos ou logs, e ser notificado quando uma condição especificada é atendida.

**Alertas nos diferentes serviços do Azure**

Os alertas estão disponíveis em diferentes serviços, incluindo:

- Application Insights: Permite os alertas de teste da Web e métrica.

>[!Note]
> Consulte [Definir Alertas no Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) e [Monitorar a disponibilidade e a capacidade de resposta de qualquer site](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Análise de log (Operations Management Suite): Habilita Olá roteamento de atividade e Logs de diagnóstico tooLog análise. O Operations Management Suite permite métricas, logs e outros tipos de alerta.

>[!Note]
> Para obter mais informações, consulte Alertas no [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Azure Monitor: Permite alertas com base nos valores das métricas e nos eventos do log de atividades. Você pode usar o hello [API REST do Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx) toomanage alertas.

>[!Note]
> Para obter mais informações, consulte [usando Olá portal do Azure, PowerShell ou alertas de toocreate de interface de linha de comando Olá](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>Monitoramento

Problemas de desempenho em seu aplicativo de nuvem podem afetar seus negócios. Com diversos componentes interconectados e frequentes lançamentos, degradações podem ocorrer a qualquer momento. E se você estiver desenvolvendo um aplicativo, seus usuários normalmente descobrirão problemas que você não encontrou durante os testes. Você deve saber sobre esses problemas imediatamente e ferramentas para diagnosticar e corrigir problemas de saudação. O Microsoft Azure tem uma variedade de ferramentas para identificar esses problemas.

**Como posso monitorar meus aplicativos de nuvem do Azure?**

Há uma variedade de ferramentas para monitorar serviços e aplicativos do Azure. Alguns de seus recursos se sobrepõem. Isso é parcialmente por razões históricas e em parte devido toohello obscurecendo entre o desenvolvimento e a operação de um aplicativo.

Aqui estão as principais ferramentas de saudação:

- O **Azure Monitor** é uma ferramenta básica para monitorar serviços em execução no Azure. Ele fornece dados de nível de infraestrutura sobre taxa de transferência de saudação de um serviço e uma saudação em torno de ambiente. Se você estiver gerenciando seus aplicativos tudo no Azure, decidir se tooscale para cima ou para baixo de recursos, Monitor do Azure permite que você usa toostart.

- O **Application Insights** pode ser usado para desenvolvimento e como uma solução de monitoramento de produção. Ele funciona instalando um pacote em seu aplicativo e, assim, fornecendo uma exibição mais interna do que está acontecendo. Seus dados incluem tempos de resposta de dependências, rastreamentos de exceção, instantâneos de depuração, perfis de execução. Ele fornece ferramentas avançadas de inteligentes para analisar todos os essa telemetria ambos toohelp você depurar um aplicativo e toohelp você entender o que os usuários estão fazendo com que ele. Você pode informar se um aumento no tempo de resposta deve ser feito toosomething em um aplicativo ou algum problema de obtenção de recursos externo. Se você usa o Visual Studio e aplicativo hello está com defeito, você pode ficar certo toohello problema linha (s) de código para que possa corrigi-lo.

- **Análise de log** é para aqueles que precisam de manutenção de desempenho e planejar tootune nos aplicativos em execução na produção. Ele se baseia no Azure. Ele coleta e agrega dados de várias fontes, embora com um atraso de 10 minutos too15. Ele fornece uma solução holística de gerenciamento de TI para a infraestrutura baseada em nuvem de terceiros (como o Amazon Web Services), do Azure e local. Fornece ferramentas mais sofisticadas tooanalyze dados em mais de fontes, permite consultas complexas entre todos os logs e pode alertar proativamente nas condições especificadas. Você pode até mesmo coletar dados personalizados em seu repositório central para que possa consultar e visualizá-los.

- O **SCOM (System Center Operations Manager)** é voltado ao gerenciamento e monitoramento de grandes instalações de nuvem. Você pode já estar familiarizado como ele como uma ferramenta de gerenciamento para nuvens baseadas em Hyper-V e Windows Server local, mas ele também pode se integrar e gerenciar aplicativos do Azure. Entre outras coisas, ele pode instalar o Application Insights em aplicativos ativos existentes. Se um aplicativo falhar, ele lhe informa em segundos.


## <a name="next-steps"></a>Próximas etapas

- [Melhores práticas para criação de modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

- [Exemplos de implementação da governança de assinatura do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples).

- [Governo do Microsoft Azure](https://docs.microsoft.com/azure/azure-government/).
