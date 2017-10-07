---
title: aaaMicrosoft Data Center do Azure Virtual | Microsoft Docs
description: Saiba como toobuild virtual de seu data center no Azure
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Data center virtual do Microsoft Azure
**Microsoft Azure**: avance mais rapidamente, economize dinheiro, integre aplicativos e dados locais

## <a name="overview"></a>Visão geral
Migrando tooAzure de aplicativos local, mesmo sem quaisquer alterações significativas (um método conhecido como "comparar e deslocar"), permite que as organizações benefícios de saudação de uma infraestrutura segura e eficiente. No entanto, toomake hello mais de agilidade Olá possível com a computação em nuvem, as empresas devem evoluir benefício tootake arquiteturas de recursos do Azure. O Microsoft Azure oferece serviços e infraestrutura em larga escala, recursos e confiabilidade de nível empresarial e várias opções de conectividade híbrida. Os clientes podem escolher Olá de tooaccess esses nuvem serviços via Internet ou com o Azure ExpressRoute, que fornece conectividade de rede privada. plataforma do Microsoft Azure Olá permite aos clientes tooseamlessly estender sua infraestrutura em nuvem hello e compilar arquiteturas de várias camadas. Além disso, os parceiros da Microsoft oferecem recursos avançados, oferecendo serviços de segurança e dispositivos virtuais que são otimizados toorun no Azure.

Este artigo fornece uma visão geral de padrões e designs que podem ser usado toosolve Olá preocupações de segurança, desempenho e escala arquitetura que muitos clientes enfrentam ao pensar sobre como mover em massa toohello nuvem. Uma visão geral de como toofit diferentes organizacionais funções em gerenciamento hello e governança do sistema Olá também é discutido, com os requisitos de toosecurity de ênfase e otimizar os custos.

## <a name="what-is-a-virtual-data-center"></a>O que é um Data Center Virtual?
Em Olá soluções de nuvem a princípio, foram projetados toohost único relativamente isolado, aplicativos, no espectro pública hello. Essa abordagem funcionou bem por alguns anos. No entanto, como os benefícios da nuvem Olá soluções tornou-se aparente e cargas de trabalho em grande escala foram hospedadas na nuvem hello, endereçamento de segurança, confiabilidade, desempenho e custo preocupações de implantações em um ou mais regiões se tornou vitais em toda a saudação ciclo de vida saudação do serviço de nuvem.

Olá nuvem implantação diagrama a seguir ilustra alguns exemplos de falhas de segurança (caixa vermelha) e o espaço para os dispositivos de rede virtual para otimização em cargas de trabalho (caixa amarela).

[![0]][0]

Olá Virtual Data Center (vDC) nasceu com essa necessidade para cargas de trabalho toosupport de dimensionamento e Olá precisa toodeal com problemas de saudação introduzidos ao oferecer suporte a aplicativos de grande escala na nuvem pública hello.

Uma vDC não é apenas Olá cargas de trabalho aplicativos em nuvem hello, mas também rede Olá segurança, gerenciamento e infraestrutura (por exemplo, DNS e serviços de diretório). Geralmente também fornece um tooan voltar de conexão privada rede ou data center local. Como cargas de trabalho mais mover tooAzure, é importante toothink sobre Olá infraestrutura e aos objetos de suporte que essas cargas de trabalho são colocadas em. Pensar cuidadosamente sobre como os recursos são estruturados pode evitar a proliferação de saudação de centenas de "ilhas de carga de trabalho" que devem ser gerenciadas separadamente com o fluxo de dados independente, modelos de segurança e os desafios de conformidade.

Um Data Center Virtual é essencialmente uma coleção de entidades separadas, porém relacionadas, com infraestrutura, recursos e funções de suporte em comum. Exibindo suas cargas de trabalho como uma vDC integrado, você pode obter o custo reduzido devido tooeconomies da escala, segurança otimizada por meio do componente e dados de fluxo de centralização, juntamente com operações mais fácil, gerenciamento e auditorias de conformidade.

> [!NOTE]
> É importante que Olá vDC toounderstand **não** um produto Azure discreto, mas a combinação de saudação de vários recursos muito atender às suas necessidades exatas. vDC é uma maneira de pensar sobre suas cargas de trabalho e uso do Azure toomaximize seus recursos e capacidades na nuvem hello. Olá controlador de domínio virtual é, portanto, uma abordagem modular sobre como toobuild a serviços de TI no Azure, respeitando organizacionais funções e responsabilidades de saudação.

Olá vDC pode ajudar as empresas cargas de trabalho e aplicativos no Azure para Olá os seguintes cenários:

-   Hospedagem de várias cargas de trabalho relacionadas
-   Migrar cargas de trabalho de um tooAzure do ambiente local
-   Implementação de segurança compartilhada ou centralizada e requisitos de acesso entre cargas de trabalho
-   Como combinar TI centralizada e DevOps apropriadamente para uma grande empresa

Olá toounlock principais vantagens de saudação do vDC, uma topologia centralizado (hub e raios) com uma combinação de recursos do Azure: [VNet do Azure][VNet], [NSGs] [ NSG], [Emparelhamento VNet][VNetPeering], [rotas definidas pelo usuário (UDR)][UDR]e a identidade do Azure com [ Controle de acesso de Base de função (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>Quem precisa de um Data Center Virtual?
Qualquer cliente do Azure que precisa toomove mais do que algumas das cargas de trabalho no Azure podem se beneficiar de pensar sobre como usar os recursos comuns. Dependendo da magnitude do hello, até mesmo aplicativos podem se beneficiar do uso de padrões de saudação e componentes usados toobuild uma vDC.

Se sua organização tiver um segurança de TI, rede, centralizado, e/ou equipe/departamento de conformidade, uma vDC pode ajudar a impor diretiva pontos, diferenciação de imposto e garantir a uniformidade de saudação subjacente componentes comuns dando tanto as equipes do aplicativo liberdade e controle como é apropriada para suas necessidades.

Organizações que desejam tooDevOps podem utilizar os conceitos de vDC Olá tooprovide autorizado alguns recursos do Azure e garantir que eles tenham controle total nesse grupo (assinatura ou o recurso grupo em uma assinatura comum), mas rede hello e limites de segurança manter a conformidade, conforme definido pela política centralizada em um hub de rede virtual e o grupo de recursos.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Considerações sobre a implementação de um Data Center Virtual
Ao projetar uma vDC, há vários tooconsider da Central de problemas:

-   Serviços de identidade e diretório
-   Infraestrutura de segurança
-   Nuvem de toohello de conectividade
-   Conectividade na nuvem Olá

##### <a name="identity-and-directory-service"></a>*Serviço de identidade e de diretório*
Serviços de identidade e diretório são um aspecto fundamental de todos os dados centrais, locais e na nuvem hello. A identidade é tooall relacionados aspectos de tooservices de acesso e autorização em Olá vDC. toohelp Certifique-se de que somente usuários autorizados e processos acessam sua conta do Azure e recursos, o Azure usa vários tipos de credenciais para autenticação. Isso inclui senhas (tooaccess Olá conta do Azure), as chaves de criptografia, assinaturas digitais e certificados. [*MFA* (Autenticação Multifator do Azure)][MFA] é uma camada adicional de segurança para acessar os serviços do Azure. O Azure MFA fornece autenticação forte com uma variedade de opções de verificação fácil — chamada telefônica, mensagem de texto ou notificação de aplicativo móvel — e permitir que os clientes toochoose método de saudação que preferirem.

Qualquer grande empresa precisa toodefine um processo de gerenciamento de identidade que descreve o gerenciamento de saudação de identidades individuais, sua autenticação, autorização, funções e privilégios dentro ou entre Olá vDC. metas Hello desse processo devem ser tooincrease segurança e a produtividade ao diminuir o custo, tempo de inatividade e as tarefas manuais repetitivas.

Empresas/organizações podem exigir uma combinação exigente de serviços para diferentes LOBs (linha de negócios) e os funcionários geralmente têm diferentes funções quando estão envolvido em projetos diferentes. Uma vDC requer boa cooperação entre diferentes equipes, cada um com definições de função específica, tooget sistemas em execução com bom controle. matriz de saudação de direitos, responsabilidades e acesso pode ser extremamente complexa. O gerenciamento de identidade no vDC é implementado por meio do [*AAD* (Azure Active Directory)][AAD] e do RBAC (controle de acesso baseado em função).

Um Serviço de Diretório é uma infraestrutura de informações compartilhadas para localizar, gerenciar, administrar e organizar itens cotidianos e recursos de rede. Esses recursos podem incluir volumes, pastas, arquivos, impressoras, usuários, grupos, dispositivos e outros objetos. Cada recurso Olá rede é considerado um objeto pelo servidor de diretório hello. Informações sobre um recurso são armazenadas como uma coleção de atributos associados a tal recurso ou objeto.

Todos os serviços comerciais online da Microsoft dependem do Azure AD (Azure Active Directory) para conexão e outras necessidades de identidade. O Azure Active Directory é uma solução de nuvem de gerenciamento de acesso e identidade abrangente e altamente disponível que combina os serviços principais de diretório, governança avançada de identidades e gerenciamento do acesso de aplicativos. AAD pode ser integrado com o local do Active Directory tooenable único logon para todos os baseados em nuvem e hospedado localmente aplicativos (local). atributos de usuário de saudação do Active Directory no local podem ser tooAAD sincronizada automaticamente.

Um único administrador global é tooassign não é necessária a todas as permissões em uma vDC. Em vez disso, cada departamento específico (ou grupo de usuários ou serviços em Olá serviço de diretório) pode ter Olá permissões necessárias toomanage seus próprios recursos dentro de uma vDC. Estruturar permissões requer balanceamento. Um número excessivo de permissões pode prejudicar a eficiência de desempenho, enquanto permissões de menos ou não exigentes podem aumentar os riscos de segurança. Controle de acesso do Azure baseado em função (RBAC) ajuda tooaddress esse problema, oferecendo o gerenciamento de acesso refinado para recursos do vDC.

##### <a name="security-infrastructure"></a>*Infraestrutura de Segurança*
Infraestrutura de segurança, no contexto de saudação de um vDC é principalmente toohello relacionados diferenciação de tráfego no segmento de rede virtual específico do vDC hello e como fluxos de toocontrol de entrada e saída durante saudação vDC. O Azure se baseia na arquitetura multilocatário que impede o tráfego não autorizado e não intencional entre implantações, usando isolamento de VNet (rede virtual), ACLs (listas de controle de acesso), balanceadores de carga e filtros IP, juntamente com políticas de fluxo de tráfego. NAT (conversão de endereços de rede) separa o tráfego de rede interno do tráfego externo.

Olá malha do Azure aloca recursos de infraestrutura tootenant cargas de trabalho e gerencia comunicações tooand de máquinas virtuais (VMs). Olá hipervisor do Azure impõe a memória e o processo de separação entre VMs e com segurança locatários de tooguest SO de tráfego de rede de rotas.

##### <a name="connectivity-toohello-cloud"></a>*Nuvem de toohello de conectividade*
Olá vDC precisa de conectividade com redes externas toooffer serviços toocustomers, parceiros e/ou usuários internos. Isso geralmente significa conectividade não apenas toohello da Internet, mas também tooon local redes e data centers.

Os clientes podem criar seu toocontrol de políticas de segurança que e como os serviços específicos vDC hospedado são acessíveis de Olá Internet usando dispositivos de rede Virtual (com inspeção tráfego e filtragem) e políticas personalizadas de roteamento e (filtragem de rede Roteamento definida pelo usuário e grupos de segurança de rede).

Geralmente, as empresas precisam tooconnect vDCs tooon local data centers ou outros recursos. conectividade Olá entre redes do Azure e no local, portanto, é um aspecto essencial ao projetar uma arquitetura efetivada. As empresas têm uma interconexão entre locais e vDC toocreate de duas maneiras diferentes no Azure: trânsito pela Internet da saudação e/ou por conexões diretas privadas.

Um [ **VPN Site a Site do Azure** ] [ VPN] é um serviço de interconexão sobre Olá Internet entre redes locais e vDC hello, estabelecida por meio de seguro criptografados conexões (túneis IPsec/IKE). Conexão de Site a Site do Azure é toocreate rápida, flexível e não requer qualquer compras adicional, como todas as conexões de conexão sobre Olá da internet.

[**Rota expressa** ] [ ExR] é um serviço de conectividade do Azure que permite criar conexões privadas entre vDC e hello redes locais. Conexões de rota expressa não passam em Olá Internet pública e oferecem maior segurança, confiabilidade e velocidades maiores (até too10 Gbps) junto com latência consistente. Rota expressa é muito útil para vDCs, como os clientes podem obter benefícios de saudação de regras de conformidade associadas conexões privadas de rota expressa.

Implantar conexões do ExpressRoute envolve a interação com um provedor de serviços do ExpressRoute. Para clientes que precisam toostart rapidamente, é comum tooinitially use conectividade de tooestablish VPN Site a Site entre os recursos locais e vDC Olá e, em seguida, migrar tooExpressRoute conexão.

##### <a name="connectivity-within-hello-cloud"></a>*Conectividade na nuvem Olá*
[VNets] [ VNet] e [emparelhamento VNet] [ VNetPeering] é serviços de conectividade dentro de uma vDC de rede Olá básico. Uma rede virtual garante um limite natural de isolamento de recursos do vDC e emparelhamento de rede virtual permite a intercomunicação entre diferentes VNets em hello mesma região do Azure. Controle de tráfego dentro de uma rede virtual e entre VNets necessário toomatch um conjunto de segurança regras especificadas por meio de listas de controle de acesso ([grupo de segurança de rede][NSG]), [dispositivos de rede Virtual ] [ NVA]e as tabelas de roteamento personalizadas ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>Visão geral do Data Center Virtual

### <a name="topology"></a>Topologia
Hub e spokes modelo estendido Olá Virtual Data Center em uma única região do Azure

[![1]][1]

hub de saudação é Olá central zona controla e inspeciona o tráfego de entrada e/ou saída entre diferentes regiões: Internet, no local, e Olá spokes. topologia de hub e spoke Olá fornece Olá departamento de TI políticas de segurança de tooenforce uma maneira eficiente em um local central, reduzindo o potencial de saudação de uma configuração incorreta e exposição.

hub de Olá contém componentes de serviço comum Olá consumidos pelo Olá spokes. Aqui estão alguns exemplos típicos de serviços centrais comuns:

-   infraestrutura do Active Directory do Windows Hello (com hello relacionados ao serviço do ADFS) necessário para a autenticação de usuário de terceiros acessando em redes não confiáveis antes de obter acesso toohello cargas de trabalho no hello spoke
-   Um serviço tooresolve nomes DNS para carga de trabalho de saudação em Olá raios, tooaccess recursos locais e na saudação da Internet
-   Uma infraestrutura PKI, tooimplement logon único em cargas de trabalho
-   Controle de fluxo (TCP/UDP) entre spokes hello e Internet
-   Controle de fluxo entre spoke hello e local
-   Se desejar, fluxo de controle entre um spoke e outro

Olá vDC reduz o custo geral usando a infraestrutura de hub compartilhado Olá entre vários spokes.

função Hello de cada spoke pode ser toohost diferentes tipos de cargas de trabalho. Olá spokes também podem fornecer uma abordagem modular para implantações repetidas (por exemplo, desenvolvimento e teste, testes de aceitação do usuário, produção e pré-produção) de saudação às cargas de trabalho. Olá spokes também podem ser usado toosegregate e permitir que diferentes grupos dentro de sua organização (por exemplo, grupos de DevOps). Dentro de um spoke, é possível toodeploy uma carga de trabalho básico ou cargas de trabalho complexas de várias camadas com o tráfego de controle entre camadas de saudação.

##### <a name="subscription-limits-and-multiple-hubs"></a>Limites de assinatura e vários hubs
No Azure, cada componente, qualquer tipo de saudação é implantado em uma assinatura do Azure. isolamento de saudação de componentes do Azure em diferentes assinaturas do Azure pode atender aos requisitos de saudação de LOBs diferentes, como configurar níveis diferenciados de acesso e autorização.

Uma único vDC pode escalar verticalmente toolarge inúmeros raios, embora, assim como acontece com todos os sistemas IT, há limites de plataformas. Olá, implantação hub é acoplado tooa assinatura específica do Azure, que tem restrições e limites (por exemplo, um número máximo de emparelhamentos de rede virtual - consulte [assinatura do Azure e limites de serviço, cotas e restrições] [ Limits] para obter detalhes). Em casos em que os limites podem ser um problema, a arquitetura de saudação pode dimensionar ainda mais estendendo o modelo de saudação de um cluster de tooa raios de hub único de hub e spokes. Vários hubs em uma ou mais regiões do Azure podem ser interconectados usando o ExpressRoute ou a VPN site a site.

[![2]][2]

Hello introdução dos hubs de vários aumenta o esforço de custo e gerenciamento de saudação do sistema hello e só deve ser justificada pelo escalabilidade (exemplos: limites do sistema ou redundância) e replicação regional (exemplos: recuperação de desastres ou de desempenho do usuário final). Em cenários que exigem vários hubs, todos os hubs de saudação esforce-Olá toooffer mesmo conjunto de serviços para facilitar a operacional.

##### <a name="interconnection-between-spokes"></a>Interconexão entre spokes
Dentro de um único spoke, é possível tooimplement complexo cargas de trabalho de várias camadas. Configurações de várias camadas podem ser implementadas usando sub-redes (um para cada camada) na mesma rede virtual e filtragem Olá fluxos usando os NSGs de saudação.

Em Olá outro lado, um arquiteto seja toodeploy uma carga de trabalho de várias camada em múltiplas VNets. Usando o emparelhamento VNet, raios podem conectar tooother raios em Olá mesmo hub ou hubs diferentes. Um exemplo típico desse cenário é o caso de Olá onde servidores de processamento do aplicativo estão em um spoke (VNet), enquanto o banco de dados de saudação é implantado em um spoke diferente (VNet). Nesse caso, ele é fácil toointerconnect spokes saudação com redes emparelhamento e evitando transiting por meio do hub de saudação. Uma análise cuidadosa de arquitetura e a segurança deve ser executada tooensure que ignorar hub Olá não ignorar importantes de segurança ou auditoria de pontos que podem existir somente no hub de saudação.

[![3]][3]

Raios também podem ser spoke tooa interconectados que atua como um hub. Essa abordagem cria uma hierarquia de dois níveis: hub de Olá Olá spoke no nível superior da saudação (nível 0) tornam-se de raios inferiores (nível 1) da hierarquia de saudação. raios de saudação do vDC necessário tooforward Olá tráfego toohello hub central tooreach toohello rede de local ou da internet. Uma arquitetura com dois níveis de hub apresenta roteamento complexo que remove os benefícios de saudação de uma relação de hub-spoke simples.

Embora o Azure permite topologias complexas, um dos princípios básicos de saudação do conceito de vDC Olá é repetição e simplicidade. toominimize esforços de gerenciamento, o design de hub-spoke simples de saudação é Olá recomendado vDC arquitetura de referência.

### <a name="components"></a>Componentes
Um Data Center Virtual é composto por quatro tipos de componente básicos: **Infraestrutura**, **Redes de Perímetro**, **Cargas de Trabalho** e **Monitoramento**.

Cada tipo de componente consiste em vários recursos e funcionalidades do Azure. Seu vDC é composto de instâncias de vários tipos de componentes e muitas variações de saudação mesmo tipo de componente. Por exemplo, você pode ter muitas instâncias de carga de trabalho diferentes e logicamente separadas que representem diferentes aplicativos. Use esses tipos diferentes de componentes e instâncias tooultimately criar Olá vDC.

[![4]][4]

Hello arquitetura de alto nível anterior de uma vDC mostra os tipos de componentes diferentes usados em regiões diferentes de topologia de hub spokes hello. diagrama de Olá mostra os componentes da infraestrutura em várias partes da arquitetura de saudação.

Como uma prática recomendada (para um DC ou vDC local), direitos e privilégios de acesso devem ser baseados em grupo. Lidar com grupos, em vez de usuários individuais, ajuda a manter as políticas de acesso de modo consistente entre equipes e a minimizar erros de configuração. Atribuir e remover tooand de usuários de grupos apropriados ajuda a manter os privilégios de saudação de um usuário específico atualizados.

Cada grupo de função deve ter um prefixo exclusivo em seus nomes, tornando fácil tooidentify grupo ao qual está associado com a qual carga de trabalho. Por exemplo, uma carga de trabalho que hospede um serviço de autenticação pode ter grupos chamados *AuthServiceNetOps, AuthServiceSecOps, AuthServiceDevOps e AuthServiceInfraOps.* Da mesma forma para centralizado funções ou funções não relacionados ao serviço específico tooa, poderia ser precedidos de "Corp" *CorpNetOps* por exemplo.

Muitas organizações usam uma variação de hello grupos tooprovide uma divisão principal das funções a seguir:

-   Olá *grupo central de TI (Corp)* tem componentes de infraestrutura (por exemplo, rede e segurança) do toocontrol de direitos de propriedade Olá e, portanto, precisa de função de saudação toohave de Colaborador de assinatura de saudação (e ter controle de hub de saudação) e direitos de Colaborador em Olá raios de rede. Organizações de grande porte com frequência dividem essas responsabilidades de gerenciamento entre várias equipes, como: um grupo de Operações de Rede (CorpNetOps) (com foco exclusivo na rede) e um grupo de Operações de Segurança (CorpSecOps) (responsável para política de segurança e de firewall). Nesse caso específico, dois grupos diferentes necessário toobe criado para atribuição dessas funções personalizadas.
-   Olá *desenvolvimento & grupo de teste (AppDevOps)* tiver Olá responsabilidade toodeploy cargas de trabalho (aplicativos ou serviços). Este grupo ocupa Olá de Colaborador de máquina Virtual para implantações de IaaS e/ou um ou funções do Colaborador de PaaS mais (consulte [funções internas para o controle de acesso][Roles]). Olá, opcionalmente, dev & equipe de teste pode ser necessário toohave visibilidade em diretivas de segurança (NSGs) e as políticas de roteamento (UDR) dentro do hub de saudação ou um spoke específico. Portanto, em funções de toohello de adição de Colaborador para cargas de trabalho, esse grupo também precisaria função saudação do leitor de rede.
-   Olá *operação e manutenção de grupo (CorpInfraOps ou AppInfraOps)* Olá responsabilidade de gerenciar cargas de trabalho em produção. Esse grupo precisa toobe um colaborador da assinatura em cargas de trabalho em qualquer assinatura de produção. Algumas organizações também podem avaliar se precisar de um grupo de equipe suporte de escalonamento de bloqueios adicionais com a função de saudação do Colaborador de assinatura em produção e na assinatura de hub central hello, em ordem toofix possíveis problemas de configuração em produção de hello ambiente.

Uma vDC é estruturada de forma que os grupos criados para grupos de TI centrais Olá Gerenciando hub Olá tem grupos correspondentes no nível de carga de trabalho de saudação. Além disso seria toomanaging hub recursos somente Olá centrais grupos de TI acesso externo toocontrol capaz e permissões de nível superior na assinatura de saudação. No entanto, os grupos de carga de trabalho seria toocontrol capaz de recursos e as permissões de sua rede virtual independente na Central de TI.

Olá vDC necessidades toobe particionados host toosecurely vários projetos em diferentes linha de negócios (LOBs). Todos os projetos exigem diferentes ambientes isolados (Dev, UAT, produção). Assinaturas separadas do Azure para cada um desses ambientes fornecem isolamento natural.

[![5]][5]

Olá, diagrama anterior mostra Olá relação entre uma organização de projetos, usuários, grupos e ambientes Olá onde hello componentes do Azure são implantados.

Normalmente, em TI, um ambiente (ou camada) é um sistema em que vários aplicativos são implantados e executados. Grandes empresas usam um ambiente de desenvolvimento (em que as alterações são originalmente feitas e testadas) e um ambiente de produção (que os usuários finais usam). Nesses ambientes são separados, geralmente com vários ambientes entre eles de preparo de implantação em fases de tooallow (distribuição), teste e reversão em caso de problemas. Arquiteturas de implantação variarem significativamente, mas geralmente o processo básico Olá começando no desenvolvimento (DES) e terminando em produção (produção) ainda é seguido.

Uma arquitetura comum para esses tipos de ambientes de várias camadas consiste em ambientes de produção DevOps (desenvolvimento e teste), UAT (de preparo) e ambientes de produção. As empresas podem aproveitar único ou vários AD do Azure locatários toodefine ambientes de toothese de acesso e direitos. Olá diagrama anterior mostra um caso onde dois diferentes locatários do AD do Azure são usados: um para DevOps e UAT e Olá exclusivamente para produção.

Olá a presença do AD do Azure diferente locatários impõe a separação de saudação entre ambientes. Olá mesmo grupo de usuários (por exemplo, Central de TI) tooauthenticate usando um tooaccess diferente do URI um locatário diferente do AD precisa modificar funções hello ou permissões de uma saudação DevOps ou ambientes de produção de um projeto. presença de saudação ambientes diferentes de tooaccess de autenticação de usuário diferente reduz possíveis interrupções e outros problemas causados por erros humanos.

#### <a name="component-type-infrastructure"></a>Tipo de componente: infraestrutura
Esse tipo de componente é onde reside a maioria dos Olá infraestrutura de suporte. Também é o ponto em que as equipes centralizadas de TI, Segurança e/ou Conformidade passam a maior parte do tempo.

[![6]][6]

Componentes da infraestrutura fornecem uma interconexão entre diferentes componentes de saudação de uma vDC e estão presentes no hub hello e Olá spokes. Olá responsabilidade de gerenciar e manter componentes de infraestrutura Olá normalmente é atribuída toohello central IT e/ou equipe de segurança.

Uma das tarefas primário Olá Olá, equipe de infraestrutura de TI é a consistência de Olá tooguarantee de esquemas de endereço IP em toda empresa hello. Olá privada IP endereço espaço atribuído toohello vDC precisa toobe consistente e não sobrepostos com endereços IP atribuídos em suas redes locais.

Ao NAT Olá roteadores de borda local ou no Azure ambientes podem evitar conflitos de endereço IP, ele adiciona componentes de infraestrutura de tooyour complicações. Simplicidade de gerenciamento é uma das principais metas de saudação do vDC, portanto não é uma solução recomendada usar NAT toohandle IP preocupações.

Componentes da infraestrutura contenham Olá funcionalidade a seguir:

-   [**Serviços de identidade e diretório**][AAD]. Tipo de recurso de tooevery de acesso no Azure é controlado por uma identidade armazenada em um serviço de diretório. Olá repositórios de serviço de diretório não apenas Olá a lista de usuários, mas também Olá tooresources de direitos de acesso em uma assinatura do Azure específica. Esses serviços podem existir somente em nuvem ou podem ser sincronizados com identidade local armazenada no Active Directory.
-   [**Rede Virtual**][VPN]. Redes virtuais são um dos principais componentes de uma vDC e habilitar toocreate um limite de isolamento de tráfego em Olá plataforma Windows Azure. Uma Rede Virtual é composta por um ou vários segmentos de rede virtual, cada um com um prefixo de rede IP específico (uma sub-rede). Olá rede Virtual define uma área de perímetro interna em que máquinas virtuais e serviços de PaaS podem estabelecer uma comunicação privada. Máquinas virtuais (e os serviços de PaaS) em uma rede virtual não pode se comunicar diretamente tooVMs (e os serviços de PaaS) em uma rede virtual diferente, mesmo se as duas redes virtuais são criadas por Olá mesmo cliente, em Olá a mesma assinatura. Isolamento é uma propriedade vital que garante que as VMs e as comunicações do cliente permaneçam privadas em uma rede virtual.
-   [**UDR**][UDR]. O tráfego em uma rede Virtual é roteado por padrão com base na tabela de roteamento saudação do sistema. Uma rota de definição de usuário é uma tabela de roteamento personalizada que os administradores de rede podem associar tooone ou mais comportamento de saudação toooverwrite sub-redes da tabela de roteamento de sistema hello e definir um caminho de comunicação em uma rede virtual. presença de saudação do UDRs garante que o tráfego de saída de trânsito de spoke Olá por meio de VMs personalizadas específicas e/ou dispositivos de rede Virtual e balanceadores de carga presente no hub hello e nos spokes hello.
-   [**NSG**][NSG]. Um Grupo de Segurança de Rede é uma lista de regras de segurança que atuam como filtragem de tráfego em Fontes IP, Destino IP, Protocolos, portas de Origem IP e portas de Destino IP. Olá NSG pode ser aplicadas tooa sub-rede, um cartão de NIC Virtual associado a uma VM do Azure, ou ambos. Olá NSGs são essencial tooimplement um controle de fluxo correto em hub Olá em Olá spokes. nível de saudação de segurança proporcionada pelo Olá NSG é uma função de quais portas abertas e para cada finalidade. Os clientes devem aplicar filtros adicionais por VM com os firewalls baseados em host, como IPtables ou Olá Firewall do Windows.
-   **DNS**. resolução de nomes de saudação de recursos em Olá VNets de uma vDC é fornecida por meio do DNS. escopo de saudação de resolução de nome do padrão de saudação DNS é limitado toohello VNet. Normalmente, um serviço DNS personalizado deve toobe implantado no hub hello como parte dos serviços comuns, mas consumidores de saudação principal dos serviços DNS residem em spoke hello. Se necessário, os clientes podem criar uma estrutura hierárquica do DNS com a delegação de DNS zonas toohello spokes.
-   [**Assinatura][SubMgmt] e [Gerenciamento de Grupo de Recursos][RGMgmt]**. Uma assinatura define um limite natural toocreate vários grupos de recursos no Azure. Recursos em uma assinatura são montados em conjunto em contêineres lógicos denominados Grupos de Recursos. saudação de grupo de recursos representa um recurso de saudação tooorganize grupo lógico de um vDC.
-   [**RBAC**][RBAC]. Por meio de RBAC, é possível toomap a função organizacional junto com direitos tooaccess específico recursos do Azure, permitindo que você toorestrict usuários tooonly um certo subconjunto de ações. Com RBAC, você pode conceder acesso atribuindo Olá toousers de função apropriada, grupos e aplicativos dentro do escopo de saudação relevantes. escopo de saudação de uma atribuição de função pode ser uma assinatura do Azure, um grupo de recursos ou um único recurso. RBAC permite a herança de permissões. Uma função atribuída a um escopo pai também concede acesso toohello filhos contidos nele. Usando o RBAC, você pode separar deveres e conceder apenas Olá total acesso toousers que precisam tooperform seus trabalhos. Por exemplo, use RBAC toolet um funcionário gerenciar máquinas virtuais em uma assinatura, enquanto outra pode gerenciar bancos de dados SQL em Olá mesma assinatura.
-   [**Emparelhamento VNet**][VNetPeering]. Hello recurso fundamental usado toocreate Olá infraestrutura de uma vDC é emparelhamento de rede virtual, um mecanismo que se conecta a duas redes virtuais (VNets) em hello mesma região através da rede Olá de saudação data center do Azure.

#### <a name="component-type-perimeter-networks"></a>Tipo de componente: redes de perímetro
[Rede de perímetro] [ DMZ] componentes (também conhecido como uma rede DMZ) permitem que você tooprovide a conectividade de rede com seu local ou redes de centro de dados físicos, juntamente com qualquer tooand de conectividade de Internet de saudação. Também é o local em que suas equipes de segurança de rede provavelmente passarão a maior parte do tempo.

Pacotes de entrada devem fluir através de dispositivos de segurança Olá no hub hello, como firewall hello, IDS e IPS, antes de alcançar os servidores de back-end de saudação em Olá spokes. Pacotes direcionado à Internet de cargas de trabalho Olá também devem fluir através de dispositivos de segurança Olá na rede de perímetro Olá para imposição de política, inspeção e auditoria, antes de sair da rede hello.

Componentes de rede de perímetro fornecem Olá recursos a seguir:

-   [Redes Virtuais][VNet], [UDR][UDR], [NSG][NSG]
-   [Solução de Virtualização de Rede][NVA]
-   [Load Balancer][ALB]
-   [Gateway de Aplicativo][AppGW] / [WAF][WAF]
-   [IPs Públicos][PIP]

Geralmente, Olá central IT e as equipes de segurança tem a responsabilidade de definição de requisitos e as operações de redes de perímetro hello.

[![7]][7]

Olá, diagrama anterior mostra a imposição de saudação do dois perímetro com acesso toohello internet e um local de rede, ambos residente no hub de saudação. Em um único hub, Olá toointernet de rede de perímetro pode escalar verticalmente toosupport grandes números de LOBs, usando vários farms de Firewalls de aplicativo Web (WAFs) e/ou firewalls.

[**Redes virtuais** ] [ VNet] hub Olá normalmente é criado em uma rede virtual com várias sub-redes toohost Olá tipo diferente de serviços de filtragem e inspecionar o tráfego tooor de Olá internet através de NVAs, WAFs, e Gateways de aplicativo do Azure.

[**UDR**][UDR] Usando UDR, os clientes podem implantar firewall, IDS/IPS e outras soluções de virtualização, além de rotear o tráfego de rede por meio dessas soluções de segurança para imposição de política, auditoria e inspeção de limite de segurança. UDRs podem ser criadas em ambos os tooguarantee de raios com hello hub e hello que transits de tráfego por meio de hello VMs personalizadas específicas, dispositivos de rede Virtual e balanceadores de carga usadas por Olá vDC. tooguarantee que o tráfego gerado a partir de máquinas virtuais residentes no hello spoke trânsito toohello correto dispositivos virtuais, precisa de um UDR toobe definido em sub-redes Olá de spoke Olá definindo o endereço IP front-end de saudação do balanceador de carga interno hello como saudação de próximo salto. o balanceador de carga interno Olá distribui dispositivos virtuais de toohello tráfego interno da saudação (pool de back-end do balanceador de carga).

[![8]][8]

[**Soluções de virtualização de rede** ] [ NVA] no hub de Olá Olá rede de perímetro com acesso toohello internet normalmente é gerenciado por meio de um farm de firewalls e/ou Firewalls de aplicativo Web (WAFs).

LOBs diferentes geralmente usam muitos aplicativos da web, e esses aplicativos tendem a toosuffer de várias vulnerabilidades e explorações potenciais. Os Firewalls de aplicativos Web são que um tipo especial de produto usado toodetect ataques a aplicativos da web (HTTP/HTTPS) em mais detalhes do que um firewall genérico. Em comparação com a tecnologia de firewall tradição, WAFs tem um conjunto de servidores de web interno tooprotect recursos específicos de ameaças.

Um farm de firewall é o grupo de firewalls para trabalhar em conjunto em Olá mesmo administração comum, com um conjunto de cargas de trabalho Olá tooprotect de regras de segurança hospedada no spokes hello e redes locais tooon do controle de acesso. Um farm de firewall tem menos especializado de softwares comparados com um WAF, mas tem uma ampla aplicação toofilter de escopo e inspecionar qualquer tipo de tráfego de entrada e saída. Farms de servidores de firewall são normalmente implementados no Azure por meio de dispositivos de rede Virtual (NVAs), que estão disponíveis no hello Azure marketplace.

É recomendável conjunto de toouse um de NVAs para tráfego originado no hello Internet e outro para o tráfego originado no local. Usando apenas um conjunto de NVAs para ambos é um risco à segurança, como ele fornece nenhuma perímetro de segurança entre dois conjuntos de saudação do tráfego de rede. Usar NVAs separados reduz a complexidade de saudação de verificação de regras de segurança e deixa claro quais regras correspondem toowhich solicitação de rede de entrada.

A maioria das grandes empresas gerencia vários domínios. DNS do Azure pode ser usado toohost Olá registros DNS para um domínio específico. Como exemplo, Olá endereço de IP Virtual (VIP) de saudação do Azure balanceador externo de carga (ou Olá WAFs) pode ser registrado no registro a saudação de um registro de DNS do Azure.

[**Azure Load Balancer**][ALB] O Azure Load Balancer oferece um serviço de Camada 4 (TCP, UDP) alta disponibilidade, que pode distribuir o tráfego de entrada entre instâncias de serviço definidas em um conjunto com balanceamento de carga. O tráfego enviado toohello balanceador de carga de pontos de extremidade de front-end (pontos de extremidade públicos de IP ou pontos de extremidade IP privados) pode ser redistribuído com ou sem o conjunto de tooa de conversão de endereços do pool de endereços IP de back-end (exemplos sendo; Dispositivos de rede Virtual ou máquinas virtuais).

Balanceador de carga do Azure pode investigação de integridade de saudação do hello várias instâncias de servidor e, em seguida, quando um teste falha toorespond Olá carga balanceador para de enviar a instância não íntegro do tráfego toohello. Uma vDC, temos presença de saudação de um balanceador externo no hub de saudação (por exemplo, saldo Olá tráfego tooNVAs) e nos spokes hello (tooperform tarefas como balanceamento do tráfego entre VMs diferentes de um aplicativo de várias camada).

[**Gateway de Aplicativo**][AppGW] O Gateway de Aplicativo do Microsoft Azure é uma solução de virtualização dedicada que fornece o ADC (controlador de entrega de aplicativos) como um serviço, oferecendo vários recursos de balanceamento de carga de camada 7 para o seu aplicativo. Ele permite que você produtividade de farm da web toooptimize descarregando CPU intensa SSL encerramento toohello gateway de aplicativo. Ele também fornece outros recursos de roteamento de camada 7 incluindo rodízio distribuição de tráfego de entrada, a afinidade de sessão baseada em cookie, roteamento baseado no caminho de URL e Olá capacidade toohost vários sites por trás de um único Gateway de aplicativo. Um firewall do aplicativo web (WAF) também é fornecido como parte do gateway de aplicativo hello WAF SKU. Este SKU fornece proteção tooweb aplicativos comuns de vulnerabilidades de web e explorações. O Gateway de Aplicativo pode ser configurado como um gateway voltado para a Internet, um gateway apenas interno ou uma combinação de ambos. 

[**IPs públicos** ] [ PIP] habilitar recursos de alguns Azure você tooassociate serviço pontos de extremidade tooa endereço IP público que permite tooyour recurso toobe acessado de Olá da internet. Esse ponto de extremidade usa a conversão de endereço de rede (NAT) tooroute tráfego toohello interno endereço e porta no hello rede virtual do Azure. Esse caminho é a principal maneira Olá para toopass tráfego externo na rede virtual hello. endereços IP públicos de saudação podem ser configurado toodetermine tráfego que é passado e como e onde ele é convertido em rede virtual toohello.

#### <a name="component-type-monitoring"></a>Tipo de componente: monitoramento
Monitoramento de componentes fornece Olá a visibilidade e o alerta de todos os outros tipos de componentes. Todas as equipes devem ter acesso toomonitoring para componentes de saudação e serviços que eles têm acesso a. Se você tiver um equipes de suporte técnico ou operações centralizado, precisam toohave integrado acessar toohello dados fornecidos por esses componentes.

Recursos hospedados do Azure oferece diferentes tipos de registro em log e monitoramento de comportamento de saudação tootrack serviços do Azure. Governança e controle de cargas de trabalho no Azure é com base não apenas na coleta de dados de log, mas também as ações de tootrigger de capacidade de saudação com base em eventos específicos de relatado.

Há dois tipos principais de logs no Azure:

-   [**Logs de atividade** ] [ ActLog] (conhecido também como "Log operacional") fornecem informações sobre operações de saudação realizadas nos recursos Olá assinatura do Azure. Esses logs de eventos de plano de controle de saudação para suas assinaturas de relatório. Todos os recursos do Azure geram logs de auditoria.

-   [**Logs de diagnóstico do Azure** ] [ DiagLog] são os logs gerados por um recurso que fornecem dados ricos, frequentes sobre a operação de saudação do recurso. conteúdo de saudação desses logs varia por tipo de recurso.

[![9]][9]

Em uma vDC, é extremamente importante tootrack Olá NSGs logs particularmente essas informações:

-   [**Logs de eventos**][NSGLog]: fornece informações sobre quais regras NSG são aplicadas tooVMs e funções de instância com base no endereço MAC.
-   [**Logs do contador**][NSGLog]: controla quantas vezes cada NSG regra foi executada toodeny ou permitir o tráfego.

Todos os logs podem ser armazenados nas Contas de Armazenamento do Azure para fins de auditoria, análise estática ou backup. Quando a saudação logs são armazenados em uma conta de armazenamento do Azure, os clientes podem usar diferentes tipos de estruturas tooretrieve, preparar, analisar e visualizar esse status de saudação de tooreport de dados e a integridade dos recursos de nuvem.

Grandes empresas devem já tiver adquirido uma estrutura padrão para monitoramento de sistemas no local e pode estender que framework toointegrate logs gerados por implantações de nuvem. Para organizações que desejem tookeep todos Olá log na nuvem hello, [Microsoft Operations Management Suite (OMS)] [ OMS] é uma ótima opção. Como o OMS é implementado como um serviço baseado em nuvem, é possível colocá-lo em funcionamento com investimentos mínimos em serviços de infraestrutura. OMS também pode integrar com componentes do System Center, como System Center Operations Manager tooextend os investimentos de gerenciamento para a nuvem de saudação.

Análise de Log do OMS é um componente do hello OMS framework toohelp coletar, correlacionar, pesquisar e agir sobre dados de desempenho e log gerados por sistemas operacionais, aplicativos de nuvem de infraestrutura componentes. Ele oferece aos clientes informações operacionais em tempo real usando a pesquisa integrada e painéis personalizados tooanalyze todos os registros de saudação em todas as suas cargas de trabalho em uma vDC.

#### <a name="component-type-workloads"></a>Tipo de componente: cargas de trabalho
Componentes de carga de trabalho são o local em que seus aplicativos reais e serviços residem. Também é o ponto em que as equipes de desenvolvimento de aplicativo passam a maior parte do tempo.

possibilidades de carga de trabalho de saudação são realmente infinitas. Olá seguem apenas alguns dos tipos de carga de trabalho possíveis hello:

**Aplicativos de LOB Internos**

Aplicativos de linha de negócios são operação contínua do computador aplicativos toohello críticos de uma empresa. Aplicativos de LOB têm algumas características em comum:

-   **Interativos**. Aplicativos de LOB são interativos por natureza: os dados são inseridos e o resultado/relatórios são retornados.
-   **Conduzidos por dados**. Aplicativos de LOB são intensiva com frequentes toohello bancos de dados ou outro armazenamento de dados.
-   **Integrados**. Aplicativos oferecem integração com outros sistemas dentro ou fora da organização de saudação de LOB.

**Cliente voltados para sites da web (voltado para a Internet ou interno)** a maioria dos aplicativos que interagem com hello Internet são sites da web. O Azure oferece Olá recurso toorun um site da web em uma VM IaaS ou de um [aplicativos Web do Azure] [ WebApps] site (PaaS). Os aplicativos Web do Azure suporte à integração com VNets que permitem a implantação de saudação de saudação aplicativos Web no spoke de saudação de uma vDC. Com hello integração da VNET, você tooexpose um ponto de extremidade de Internet não é necessário para seus aplicativos, mas pode usar Olá recursos internet não roteável endereço privado de sua rede virtual privada em vez disso.

**Grande/análise de dados** quando tooscale volume muito grande de tooa as necessidades de dados, bancos de dados podem ser dimensionado corretamente. Tecnologia de Hadoop oferece um sistema toorun distribuída consultas em paralelo em um grande número de nós. Os clientes têm cargas de trabalho do hello opção toorun dados em VMs de IaaS ou PaaS ([HDInsight][HDI]). HDInsight oferece suporte à implantação em uma rede virtual com base no local, pode ser implantado tooa cluster em um spoke de saudação vDC.

**Eventos e Mensagens**
[Hubs de Eventos do Azure][EventHubs] são um serviço de ingestão de telemetria em hiperescala que coleta, transforma e armazena milhões de eventos. Como uma plataforma de streaming distribuída, ele oferece baixa latência e retenção de tempo configurável, permitindo que você tooingest grandes quantidades de telemetria no Azure e ler esses dados de vários aplicativos. Com Hubs de Evento, um único fluxo pode dar suporte a pipelines tanto em tempo real quanto em lote.

Um serviço de mensagem em nuvem altamente confiável entre aplicativos e serviços pode ser implementado por meio do [Barramento de Serviço do Azure][ServiceBus] que oferece sistema de mensagens agenciado assíncrono entre cliente e servidor, junto com recursos de publicar/assinar e mensagens PEPS (primeiro a entrar, primeiro a sair).

[![10]][10]

### <a name="multiple-vdc"></a>Vários vDCs
Até agora, este artigo se concentrou em uma único vDC, que descreve a arquitetura que contribuem vDC resiliente tooa e componentes básicos de saudação. Recursos do Azure, como conjuntos de disponibilidade de NVAs, balanceador de carga do Azure, conjuntos de escala, juntamente com outros mecanismos de colaboração tooa sistema que permitem a você toobuild sólidos níveis de SLA em seus serviços de produção.

No entanto, uma único vDC está hospedada dentro de uma única região e é vulnerável toomajor interrupção que pode afetar a região inteira. Clientes que desejam tooachieve SLAs alta necessitam serviços de saudação tooprotect por meio de implantações de saudação mesmo projeto em vDCs dois (ou mais), colocados em regiões diferentes.

Questões de tooSLA adição, há vários cenários comuns em que a implantação de vários vDCs faz sentido:

-   Presença regional/global
-   Recuperação de desastre
-   Tráfego do mecanismo toodivert entre o controlador de domínio

#### <a name="regionalglobal-presence"></a>Presença regional/global
Data Centers do Azure estão presentes em várias regiões no mundo todo. Ao selecionar vários data centers do Azure, os clientes precisam tooconsider dois fatores relacionados: distâncias geográficas e latência. Os clientes precisam de distância geográfica do hello tooevaluate entre vDCs hello e distância Olá entre Olá vDC e os usuários finais do hello, toooffer Olá melhor experiência de usuário.

Olá região do Azure que hospedam os vDCs também precisa tooconform com requisitos normativos estabelecidos por qualquer jurisdição legal sob a qual sua organização opera.

#### <a name="disaster-recovery"></a>Recuperação de desastre
implementação de saudação de um plano de recuperação de desastres é fortemente relacionados toohello tipo de carga de trabalho em questão e estado de carga de trabalho de Olá Olá capacidade toosynchronize entre vDCs diferentes. Idealmente, a maioria dos clientes deseja toosynchronize dados de aplicativo entre implantações em execução no mecanismo de tooimplement um failover rápido dois vDCs diferentes. A maioria dos aplicativos são toolatency confidencial e que pode causar o potencial de tempo limite e atraso na sincronização de dados.

Sincronização ou monitoramento de pulsação de aplicativos em diferentes vDCs exige a comunicação entre eles. Dois vDCs em regiões diferentes podem ser conectados por meio de:

-   Privada emparelhamento de rota expressa quando hubs do vDC Olá toohello conectado mesmo circuito de rota expressa
-   vários circuitos de rota expressa conectados via o backbone corporativo e sua malha vDC circuitos do ExpressRoute toohello conectado
-   Conexões de VPN Site a Site entre seus hubs o vDC em cada Região do Azure

Geralmente Olá conexão de rota expressa é mecanismo preferido de saudação devido a maior largura de banda e latência consistente quando transiting por meio de saudação backbone do Microsoft.

Não há nenhum toovalidate receita magic um aplicativo distribuído entre dois (ou mais) vDCs diferentes localizados em regiões diferentes. Os clientes devem executar a latência da rede qualificação testes tooverify hello e largura de banda de conexões de saudação e de destino se a replicação síncrona ou assíncrona de dados é apropriada e o objetivo de tempo de recuperação ideal hello (RTO) pode ser para o cargas de trabalho.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>Tráfego do mecanismo toodivert entre o controlador de domínio
Uma técnica eficaz toodivert Olá tráfego de entrada em um tooanother do controlador de domínio é baseado no DNS. [O Azure Traffic Manager] [ TM] usa Olá sistema de nome de domínio (DNS) mecanismo toodirect saudação do usuário final tráfego toohello mais apropriado ponto de extremidade público em um vDC específico. Por meio de testes, Traffic Manager verifica periodicamente a integridade do serviço Olá de pontos de extremidade públicos em vDCs diferentes e, em caso de falha desses pontos de extremidade, ele automaticamente encaminha vDC secundário toohello.

O Traffic Manager funciona em pontos de extremidade públicos do Azure e pode ser usado, por exemplo, o toocontrol/desviar tráfego tooAzure máquinas virtuais e aplicativos Web no hello apropriado vDC. Gerenciador de tráfego seja resiliente mesmo em face de saudação de uma falha de toda a região do Azure e pode controlar a distribuição de saudação do tráfego do usuário para pontos de extremidade de serviço no vDCs diferentes com base em vários critérios (por exemplo, uma falha de um serviço em uma vDC específico, ou selecionando Olá vDC com menor latência de rede Olá para cliente Olá).

### <a name="conclusion"></a>Conclusão
Olá Virtual Data Center é um abordagem toodata Centro de migração em nuvem de saudação que usa uma combinação de recursos e funcionalidades toocreate uma arquitetura escalonável do Azure que maximiza o uso de recursos de nuvem, reduzindo os custos e simplificar o sistema governança. conceito de vDC Olá baseia-se em uma topologia de hub raios, fornece serviços compartilhados comuns no hub hello e permitindo que aplicativos/cargas de trabalho específicas em Olá spokes. Uma vDC corresponda à estrutura de saudação de funções da empresa, onde departamentos diferentes (Central de TI, DevOps, operação e manutenção) trabalham em conjunto, cada um com uma lista específica de funções e tarefas. Uma vDC atende aos requisitos de saudação para uma migração de "Comparação de precisão e Shift", mas também oferece muitas vantagens toonative implantações de nuvem.

## <a name="references"></a>Referências
Olá recursos a seguir foram abordada neste documento. Clique em Olá links toolearn mais.

| | | |
|-|-|-|
|Recursos de rede|Balanceamento de Carga|Conectividade|
|[Redes Virtuais do Azure][VNet]</br>[Grupos de segurança de rede][NSG]</br>[Logs do NSG][NSGLog]</br>[Roteamento Definido pelo Usuário][UDR]</br>[Soluções de Virtualização de Rede][NVA]</br>[Endereços IP Públicos][PIP]|[Azure Load Balancer (L3) ][ALB]</br>[Gateway de Aplicativo (L7) ][AppGW]</br>[Firewall do Aplicativo Web][WAF]</br>[Gerenciador de Tráfego do Azure][TM] |[Emparelhamento VNet][VNetPeering]</br>[Rede Privada Virtual][VPN]</br>[ExpressRoute][ExR]
|Identidade</br>|Monitoramento</br>|Práticas Recomendadas</br>|
|[Azure Active Directory][AAD]</br>[Autenticação Multifator][MFA]</br>[Controles de Acesso Baseados em Função][RBAC]</br>[Funções Padrão do AAD][Roles] |[Logs de Atividade][ActLog]</br>[Logs de Diagnóstico][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[Práticas Recomendadas de Redes de Perímetro][DMZ]</br>[Gerenciamento de Assinaturas][SubMgmt]</br>[Gerenciamento de Grupo de Recursos][RGMgmt]</br>[Limites de Assinatura do Azure][Limits] |
|Outros serviços do Azure|
|[Aplicativos Web do Azure][WebApps]</br>[HDInsights (Hadoop) ][HDI]</br>[Hubs de Eventos][EventHubs]</br>[Barramento de Serviço][ServiceBus]|



## <a name="next-steps"></a>Próximas etapas
 - Explorar [emparelhamento VNet][VNetPeering], Olá tecnologia de base para vDC hub e spoke designs
 - Implementar [AAD] [ AAD] tooget iniciado com [RBAC] [ RBAC] exploração
 - Desenvolver um modelo de gerenciamento de assinatura e do recurso e RBAC modelar a estrutura toomeet hello, requisitos e as políticas da sua organização. planejamento de atividade de Hello mais importante. Tanto quanto possível, planeje reorganizações, fusões, novas linhas de produto etc.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Exemplos de sobreposição de componente" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Exemplo de alto nível de vDC de hub e spoke"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Cluster de hubs e spokes"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Spoke a spoke"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Diagrama de nível de bloco do vDC Olá"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Usuários, grupos, assinaturas e projetos"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Diagrama de alto nível de infraestrutura"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Diagrama de alto nível de infraestrutura"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "Redes de perímetro e de emparelhamento VNet"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "Diagrama de alto nível para Monitoramento"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "Diagrama de alto nível para Carga de Trabalho"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
