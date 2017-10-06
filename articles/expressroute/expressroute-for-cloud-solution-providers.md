---
title: "aaaAzure rota expressa para fornecedores de soluções de nuvem | Microsoft Docs"
description: "Este artigo fornece informações para provedores de serviços de nuvem que tooincorporate desejados do Azure services e rota expressa em suas ofertas."
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>ExpressRoute para Provedores de Soluções na Nuvem (CSP)
A Microsoft fornece serviços de Hyper-escala para revendedores tradicionais e provisionar de toorapidly capaz de toobe distribuidores (CSP) novos serviços e soluções para seus clientes sem Olá necessário tooinvest esses novos serviços de desenvolvimento. tooallow Olá provedor de solução de nuvem (CSP) Olá capacidade toodirectly gerenciar esses novos serviços, a Microsoft oferece programas e APIs que permitem Olá CSP toomanage recursos do Microsoft Azure em nome de seus clientes. Um desses recursos é o ExpressRoute. Rota expressa permite Olá CSP tooconnect cliente recursos tooAzure serviços existentes. O ExpressRoute é um tooservices de link de comunicação privada de alta velocidade no Azure. 

ExpresRoute é composta de um par de circuitos para alta disponibilidade que são anexados tooa assinatura (s) de cliente e não pode ser compartilhado por vários clientes. Cada circuito deve terminar em um roteador diferente toomaintain Olá altamente disponível.

> [!NOTE]
> Existem limites de largura de banda e de conexão no ExpressRoute, o que significa que as implementações grandes/complexas exigirão vários circuitos de ExpressRoute para um único cliente.
> 
> 

O Microsoft Azure fornece um número crescente de serviços que você pode oferecer aos clientes de tooyour.  toobest tirar proveito desses serviços requerem o uso de saudação rota expressa conexões tooprovide alta velocidade baixa latência acesso toohello ambiente Microsoft Azure.

## <a name="microsoft-azure-management"></a>Gerenciamento do Microsoft Azure
A Microsoft fornece CSPs com APIs toomanage assinaturas de cliente do Azure Olá permitindo programática integração com seus próprios sistemas de gerenciamento de serviço. Os recursos de gerenciamento com suporte podem ser encontrados [aqui](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).

## <a name="microsoft-azure-resource-management"></a>Gerenciamento de recursos do Microsoft Azure
Dependendo da saudação contrato com o cliente determinará como assinatura hello será gerenciada. Olá CSP diretamente pode gerenciar a criação de saudação e manutenção de recursos ou cliente Olá pode manter o controle da saudação assinatura do Microsoft Azure e criar hello recursos do Azure que precisam. Se o cliente gerencia a criação de recursos em sua assinatura do Microsoft Azure Olá eles usarão um dos dois modelos: modelo de "Conectar-se por meio" ou "Direto para" modelo. Esses modelos são descritos detalhadamente nas seções a seguir de saudação.  

### <a name="connect-through-model"></a>Modelo Connect-Through
![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

Olá conectar pelo modelo, Olá CSP cria uma conexão direta entre o datacenter e assinatura do Azure do seu cliente. conexão direta Olá é feita usando o ExpressRoute, conectar-se a sua rede com o Azure. Em seguida, o cliente se conecta a rede tooyour. Esse cenário requer o que cliente Olá transmite Olá CSP rede tooaccess serviços do Azure. 

Se o cliente tem outras assinaturas do Azure não gerenciadas pelo Olá você, elas usariam Olá Internet pública ou seus próprios serviços de toothose tooconnect conexão privada provisionados na assinatura do CSP não hello. 

Para gerenciar os serviços do Azure de CSP, presume-se que Olá CSP possui uma identidade de cliente estabelecida anteriormente armazenar que, em seguida, será replicado para o Azure Active Directory para o gerenciamento de sua assinatura do CSP por meio de Administrate-On-Behalf-Of (AOBO). Fatores determinantes para este cenário incluem onde um determinado parceiro ou o provedor de serviços tem uma relação estabelecida com o cliente hello, cliente hello está consumindo serviços provedor atualmente ou parceiro Olá tem um tooprovide desejo uma combinação de provedor hospedado e hospedado do Azure soluções tooprovide flexibilidade e endereço desafios dos clientes que não podem ser atendidos pelo CSP sozinho. Esse modelo é ilustrado na **Figura**abaixo.

![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Conecte-se toomodel
![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-to.png)

Olá toomodel conectar, provedor de serviços de saudação cria uma conexão direta entre o datacenter do seu cliente e CSP hello provisionado assinatura do Azure usando o ExpressRoute saudação do cliente (cliente) rede.

> [!NOTE]
> Para o ExpressRoute cliente Olá seria necessário toocreate e manter o circuito de rota expressa hello.  
> 
> 

Esse cenário de conectividade requer que cliente Olá se conecta diretamente por meio de uma rede de cliente tooaccess gerenciados CSP assinatura do Azure, usando uma conexão de rede direta que é criado, propriedade e gerenciado todo ou em parte pelo cliente hello. Esses clientes supõe-se que provedor Olá atualmente não tem um repositório de identidades de cliente estabelecido e provedor Olá ajudariam cliente Olá na replicação de seu repositório de identidade atual para o Azure Active Directory para o gerenciamento de seus assinatura por meio de AOBO. Fatores determinantes para este cenário incluem onde um determinado parceiro ou o provedor de serviços tem uma relação estabelecida com o cliente hello, cliente hello está consumindo serviços provedor atualmente ou parceiro Olá tem desejo tooprovide services que serão baseadas somente nas Soluções hospedado no Azure sem Olá necessário para um datacenter do provedor existente ou infraestrutura.

![texto alternativo](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Olá escolha entre essas duas opções são com base nas necessidades do cliente e as atuais necessário tooprovide Azure services. detalhes de saudação desses modelos e Olá associado o controle de acesso baseado em função, rede, e padrões de design de identidade são abordados em detalhes no hello links a seguir:

* **RBAC (Controle de Acesso Baseado em Função)** – o RBAC baseia-se no Azure Active Directory.  Para saber mais sobre o RBAC do Azure, entre [aqui](../active-directory/role-based-access-control-configure.md).
* **Rede** – abrange Olá vários tópicos de rede no Microsoft Azure.
* **Azure Active Directory (AAD)** – AAD fornece gerenciamento de identidade Olá Microsoft Azure e 3º aplicativos SaaS de terceiros. Para saber mais sobre o AD do Azure, entre [aqui](https://azure.microsoft.com/documentation/services/active-directory/).  

## <a name="network-speeds"></a>Velocidades de rede
Rota expressa suporta velocidades de rede de 50 Mb/s too10Gb/s. Isso permite que os clientes toopurchase quantidade de saudação de largura de banda de rede necessária para seu ambiente exclusivo.

> [!NOTE]
> Largura de banda de rede pode ser aumentada, conforme necessário, sem interromper as comunicações, mas velocidade da rede tooreduce Olá requer subdividir circuito hello e recriá-la a velocidade de rede mais baixa hello.  
> 
> 

Rota expressa dá suporte à conexão Olá de vários vNets tooa único circuito ExpressRoute para uma melhor utilização de conexões de alta velocidade hello. Um circuito ExpressRoute único pode ser compartilhado entre várias assinaturas do Azure pertencentes a saudação mesmo cliente.

## <a name="configuring-expressroute"></a>Configuração do ExpressRoute
Rota expressa pode ser configurado toosupport três tipos de tráfego ([domínios de roteamento](#ExpressRoute-routing-domains)) em um único circuito ExpressRoute. Esse tráfego é dividido em emparelhamento da Microsoft, emparelhamento público e emparelhamento privado do Azure. Você pode escolher um ou todos os tipos de tráfego toobe enviados por um único circuito ExpressRoute ou usar vários circuitos de rota expressa, dependendo do tamanho de saudação do circuito de rota expressa hello e isolamento exigidos pelo cliente. postura de segurança de saudação do cliente pode não permitir pública tráfego e tráfego privada tootraverse sobre Olá mesmo circuito.

### <a name="connect-through-model"></a>Modelo Connect-Through
Em uma saudação de conectar-se a configuração, você será responsável por todas Olá rede bases tooconnect suas assinaturas toohello de recursos de datacenter de clientes hospedadas no Azure. Cada um dos seus clientes que deseja toouse recursos do Azure será necessário sua própria conexão de rota expressa, que será gerenciado pelo Olá você. Olá você usará Olá mesmo cliente de saudação métodos usaria o circuito de rota expressa tooprocure hello. Olá você seguirá Olá mesmas etapas descritas no artigo Olá [fluxos de trabalho de rota expressa](expressroute-workflows.md) para provisionamento e estados de circuito. Olá, em seguida, você irá configurar Olá Border Gateway Protocol (BGP) rotas toocontrol Olá tráfego que flui entre a rede de local de saudação e rede virtual do Azure.

### <a name="connect-toomodel"></a>Conecte-se toomodel
Em tooconfiguration uma conexão, o seu cliente é o já a tenha um tooAzure de conexão existente ou iniciará um conexão toohello provedor vinculação rota expressa do datacenter do cliente tooAzure diretamente, em vez de seu datacenter. processo de provisionamento toobegin hello, seu cliente será siga as etapas de Olá conforme descrito em Olá conectar pelo modelo, acima. Após o estabelecimento de circuito Olá o cliente precisará tooconfigure Olá local roteadores toobe tooaccess capaz de sua rede e o vNets do Azure.

Você pode ajudar a configurar a conexão de saudação e configurar Olá rotas tooallow recursos de saudação de seu toocommunicate datacenter(s) recursos de cliente de saudação em seu data center ou com recursos de saudação hospedados no Azure.

## <a name="expressroute-routing-domains"></a>Domínios de roteamento do ExpressRoute
o ExpressRoute oferece três domínios de roteamento: público, privado e emparelhamento da Microsoft. Cada um dos domínios de roteamento Olá são configurados com roteadores idênticos na configuração ativa-ativa para alta disponibilidade. Para obter mais detalhes sobre os domínios de roteamento do ExpressRoute, entre [aqui](expressroute-circuit-peerings.md).

Você pode definir as rotas personalizadas filtros tooallow somente Olá route(s) deseja tooallow ou necessário. Para obter mais informações ou toosee como toomake essas alterações consulte artigo: [criar e modificar o roteamento para um circuito de rota expressa usando o PowerShell](expressroute-howto-routing-classic.md) para obter mais detalhes sobre os filtros de roteamentos.

> [!NOTE]
> Para emparelhamento público e Microsoft conectividade deve ser Embora um endereço IP público propriedade Prezado cliente ou de CSP e deve seguir as regras tooall definido. Para obter mais informações, consulte Olá [pré-requisitos do ExpressRoute](expressroute-prerequisites.md) página.  
> 
> 

## <a name="routing"></a>Roteamento
Rota expressa conecta toohello Azure redes por meio de saudação Gateway de rede Virtual do Azure. Os gateways de rede fornecem roteamento para as redes virtuais do Azure.

Criar redes virtuais do Azure também cria uma tabela de roteamento padrão para o tráfego de toodirect Olá vNet de sub-redes Olá Olá vNet. Se a tabela de rota padrão Olá é insuficiente para solução de saudação personalizada rotas podem ser criadas como dispositivos de toocustom de tráfego de saída tooroute ou tooblock roteia toospecific sub-redes ou redes externas.

### <a name="default-routing"></a>Roteamento padrão
tabela de rota padrão Olá inclui Olá rotas a seguir:

* Roteamento em uma sub-rede
* Sub-redes na rede virtual Olá
* toohello da Internet
* Rede virtual para rede virtual usando o gateway de VPN
* Rede virtual para rede local usando um gateway de VPN ou de ExpressRoute

![texto alt](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Roteamento definido pelo usuário (UDR)
Rotas definidas pelo usuário permitem que o controle de saudação do tráfego de saída de hello atribuídos sub-rede tooother sub-redes na rede virtual hello ou em um dos Olá outros gateways predefinidos (rota expressa; internet ou VPN). tabela de roteamento de sistema do saudação padrão pode ser substituída por uma tabela de roteamento definido pelo usuário que substitui a tabela de roteamento saudação padrão com as rotas personalizadas. Com o roteamento de definida pelo usuário, os clientes podem criar tooappliances rotas específicas, como firewalls ou dispositivos de detecção de intrusão ou bloquear acesso toospecific sub-redes da sub-rede Olá rota definida pelo usuário de saudação de hospedagem. Para obter uma visão geral das Rotas Definidas pelo Usuário, entre [aqui](../virtual-network/virtual-networks-udr-overview.md). 

## <a name="security"></a>Segurança
Dependendo de qual modelo está em uso, conectar tooor Connect-por meio do seu cliente define políticas de segurança de saudação em suas redes ou fornece requisitos de política de segurança Olá toohello CSP toodefine tootheir vNets. Olá critérios de segurança a seguir pode ser definido:

1. **Isolamento de cliente** — hello plataforma Windows Azure fornece isolamento de cliente, armazenando informações de ID de cliente e de rede virtual em um banco de dados seguro, o que é usado tooencapsulate tráfego do cliente em um túnel GRE.
2. **Grupo de segurança (NSG) de rede** regras são para definir o tráfego é permitido dentro e fora de sub-redes de saudação em vNets no Azure. Por padrão, a saudação NSG contêm bloquear o tráfego de tooblock de regras de saudação Internet toohello vNet e regras de permissão para o tráfego em uma rede virtual. Para saber mais sobre os Grupos de Segurança de Rede, entre [aqui](https://azure.microsoft.com/blog/network-security-groups/).
3. **Túneis à força** — este é um tooredirect opção internet associado tráfego originado no Azure toobe redirecionada pela Olá toohello de conexão de rota expressa no data center local. Para saber mais sobre a criação de túneis à força, entre [aqui](expressroute-routing.md#advertising-default-routes).  
4. **Criptografia** — mesmo que circuitos do ExpressRoute Olá tooa dedicados específicos do cliente, há possibilidade de Olá Olá provedor de rede foi violada, permitindo que um invasor tooexamine tráfego de pacote. tooaddress que essa possibilidade, um cliente ou CSP pode criptografar o tráfego pela Olá conexão definindo políticas de modo de túnel IPSec para todo o tráfego fluindo entre hello em recursos locais e recursos do Azure (consulte toohello opcional do modo de túnel IPSec para 1 cliente na Figura 5: segurança de rota expressa, acima). opção de segundo Olá seria toouse um dispositivo de firewall em cada ponto de extremidade de saudação do hello circuito de rota expressa. Isso exigirá adicional parte 3 de VMs/dispositivos toobe instalado no tráfego de saudação de tooencrypt ambas extremidades sobre circuito de rota expressa Olá do firewall.

![texto alternativo](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Próximas etapas
Olá serviço de provedor de soluções de nuvem fornece um tooincrease de forma precisam de seus clientes de tooyour valor sem Olá para caras compras de infraestrutura e capacidade, mantendo sua posição como provedor de terceirização primário hello. Integração perfeita com o Microsoft Azure pode ser feita por meio de saudação CSP API, permitindo que você gerenciamento toointegrate do Microsoft Azure em suas estruturas de gerenciamento existente.  

Informações adicionais podem ser encontradas no hello links a seguir:

[Programa Provedor de Soluções na Nuvem da Microsoft](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[Obter pronto tootransact como um provedor de soluções de nuvem](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Recursos do Provedor de Soluções da Nuvem da Microsoft](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

