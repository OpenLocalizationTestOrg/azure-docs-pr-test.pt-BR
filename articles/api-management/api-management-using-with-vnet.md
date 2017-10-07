---
title: aaaHow toouse gerenciamento de API do Azure com redes virtuais
description: "Saiba como toosetup uma rede virtual de tooa de conexão de acesso e gerenciamento do Azure API web services por meio dele."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>Como toouse gerenciamento de API do Azure com redes virtuais
Redes virtuais do Azure (VNETs) permitem que você tooplace qualquer um dos recursos do Azure em uma rede de internet não routeable que você controle de acesso para. Essas redes podem ser redes locais de tooyour conectado usando diversas tecnologias VPN. toolearn mais sobre redes virtuais do Azure iniciar com informações de saudação aqui: [visão geral da rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).

Gerenciamento de API do Azure pode ser implantado dentro da rede virtual da saudação (VNET), para que ele pode acessar os serviços de back-end em rede hello. Olá portal do desenvolvedor e o gateway de API, pode ser configurado toobe acessível de saudação da Internet ou dentro de rede virtual hello.

> [!NOTE]
> O Gerenciamento de API do Azure oferece suporte às VNets clássicas e do Azure Resource Manager.
>
>

## <a name="enable-vpn"> </a>Habilitar conexão de VNET
> [!NOTE]
> Conectividade de rede virtual está disponível no hello **Premium** e **desenvolvedor** camadas. tooswitch entre camadas hello, abra seu serviço de gerenciamento de API no portal do Azure de saudação e Olá **escala e preços** guia. Em Olá **preço** seção, selecione a camada Premium ou o desenvolvedor de saudação e clique em Salvar.
>

conectividade de rede virtual tooenable, abra seu serviço de gerenciamento de API no portal do Azure de saudação e Olá **rede Virtual** página.

![Menu de rede virtual de Gerenciamento de API][api-management-using-vnet-menu]

Selecione o tipo de acesso de saudação desejado:

* **Externa**: portal de desenvolvedor e o gateway de gerenciamento de API Olá são acessíveis de Olá internet pública por meio de um balanceador externo. gateway Olá pode acessar recursos na rede virtual hello.

![Emparelhamento público][api-management-vnet-public]

* **Interno**: portal de desenvolvedor e o gateway de gerenciamento de API Olá são acessíveis somente de dentro da rede virtual de saudação por meio de um balanceador de carga interno. gateway Olá pode acessar recursos na rede virtual hello.

![Emparelhamento privado][api-management-vnet-private]

Agora você verá uma lista de todas as regiões em que o serviço de Gerenciamento de API é disponibilizado. Selecione uma VNET e uma sub-rede para cada região. Olá lista é preenchida com clássico e redes virtuais do Gerenciador de recursos disponíveis em suas assinaturas do Azure que são configurados na região de saudação que você está configurando.

> [!NOTE]
> **Ponto de extremidade de serviço** Olá acima diagrama inclui/Proxy de Gateway, Portal do publicador, Portal do desenvolvedor, GIT e Olá ponto de extremidade de gerenciamento direto.
> **Ponto de extremidade de gerenciamento** em Olá acima diagrama é o ponto de extremidade de saudação hospedado Olá configuração de serviço toomanage por meio do portal do Azure e o Powershell.
> Além disso, observe que, mesmo que o diagrama de saudação mostra endereços IP para seus vários pontos de extremidade, o serviço de gerenciamento de API **somente** responde em seus nomes de host configurado.

> [!IMPORTANT]
> Ao implantar uma instância de gerenciamento de API do Azure tooa VNET Gerenciador de recursos, o serviço de saudação deve estar em uma sub-rede dedicada que não contém outros recursos, exceto as instâncias de gerenciamento de API do Azure. Se uma tentativa for feita toodeploy uma instância de gerenciamento de API do Azure tooa sub-rede VNET Gerenciador de recursos que contém outros recursos, a implantação de saudação falhará.
>
>

![Selecionar VPN][api-management-setup-vpn-select]

Clique em **salvar** na parte superior de saudação da tela hello.

> [!NOTE]
> Olá endereço VIP da instância de gerenciamento de API Olá mudará sempre VNET está habilitado ou desabilitado.  
> Olá endereço VIP também será alterada quando o gerenciamento de API é movido de **externo** muito**interno** ou vice-versa
>


> [!IMPORTANT]
> Se você remove o gerenciamento de API de uma rede virtual ou alterar Olá um em que é implantado, Olá redes usadas anteriormente podem permanecer bloqueados por backup too4 horas. Durante esse período ele não serão possíveis toodelete Olá VNET ou implantar um novo tooit de recursos.

## <a name="enable-vnet-powershell"> </a>Habilitar a conexão de VNET usando cmdlets do PowerShell
Você também pode habilitar a conectividade de rede virtual usando cmdlets do PowerShell Olá

* **Criar um serviço de gerenciamento de API dentro de uma rede virtual**: usar o cmdlet Olá [AzureRmApiManagement novo](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate um serviço de gerenciamento de API do Azure dentro de uma rede virtual.

* **Implantar um serviço de gerenciamento de API existente dentro de uma rede virtual**: usar o cmdlet Olá [AzureRmApiManagementDeployment atualização](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove um serviço de gerenciamento de API do Azure existente dentro de uma rede Virtual.

## <a name="connect-vnet"></a>Conectar tooa web serviço hospedado em uma rede virtual
Depois que o serviço de gerenciamento de API é conectado toohello VNET, acessar os serviços de back-end dentro dele não é diferente de acessar serviços públicos. Basta digitar no endereço IP local de saudação ou Olá nome de host (se um servidor DNS está configurado para Olá rede virtual) do seu serviço web na Olá **URL do serviço Web** campo ao criar uma nova API ou editando uma existente.

![Adicionar a API da VPN][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"> </a>Problemas comuns de configuração de rede
Veja a seguir uma lista de problemas comuns de erro de configuração que podem ocorrer ao implantar o serviço de Gerenciamento de API em uma rede virtual.

* **Instalação de servidor DNS personalizado**: Olá serviço de gerenciamento de API depende de vários serviços do Azure. Quando o gerenciamento de API é hospedado em uma rede virtual com um servidor DNS personalizado, ele precisa tooresolve Olá nomes de host dos serviços do Azure. Siga [estas](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) orientações sobre a configuração de DNS personalizada. Consulte abaixo da tabela de portas de saudação e outros requisitos de rede para referência.

> [!IMPORTANT]
> É recomendável que, se você estiver usando um servidores de DNS personalizados para Olá VNET, você configurar que **antes de** Implantando um serviço de gerenciamento de API para ele. Caso contrário, você precisa muito atualizar serviço de gerenciamento de API Olá cada vez que você alterar os servidores DNS hello (s) executando Olá [aplicar operação de configuração de rede](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Portas necessárias para o gerenciamento de API**: tráfego de entrada e saído no hello sub-rede na qual o gerenciamento de API é implantado pode ser controlado usando [grupo de segurança de rede][Network Security Group]. Se qualquer uma dessas portas estiver indisponível, o Gerenciamento de API poderá não funcionar corretamente e poderá se tornar inacessível. A existência de uma ou mais dessas portas bloqueadas é outro problema de configuração incorreta no uso do Gerenciamento de API em uma VNET.

Quando uma instância do serviço de gerenciamento de API é hospedada em uma rede virtual, portas Olá Olá a tabela a seguir são usadas.

| Porta(s) de Origem/Destino | Direção | Protocolo de transporte | Finalidade | Origem/Destino | Tipo de acesso |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Entrada |TCP |Comunicação de cliente tooAPI gerenciamento |INTERNET / VIRTUAL_NETWORK |Externo |
| * / 3443 |Entrada |TCP |Ponto de extremidade de gerenciamento para o Portal do Azure e o Powershell |INTERNET / VIRTUAL_NETWORK |Interno e externo |
| * / 80, 443 |Saída |TCP |Dependência do Armazenamento do Azure e do Barramento de Serviço do Azure |VIRTUAL_NETWORK/INTERNET |Interno e externo |
| * / 1433 |Saída |TCP |Dependência no SQL Azure |VIRTUAL_NETWORK/INTERNET |Interno e externo |
| * / 11000 - 11999 |Saída |TCP |Dependência do SQL V12 do Azure |VIRTUAL_NETWORK/INTERNET |Interno e externo |
| * / 14000 - 14999 |Saída |TCP |Dependência do SQL V12 do Azure |VIRTUAL_NETWORK/INTERNET |Interno e externo |
| * / 5671 |Saída |AMQP |Dependência de política de Hub tooEvent Log e agente de monitoramento |VIRTUAL_NETWORK/INTERNET |Interno e externo |
| 6381 - 6383 / 6381 - 6383 |Entrada e Saída |UDP |Dependência de Cache Redis |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Interno e externo |-
| * / 445 |Saída |TCP |Dependência do Compartilhamento de Arquivos do Azure para GIT |VIRTUAL_NETWORK/INTERNET |Interno e externo |
| * / * | Entrada |TCP |Balanceador de carga de infraestrutura do Azure | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Interno e externo |

* **Funcionalidade SSL**: certificado SSL tooenable serviço de gerenciamento de API de saudação de compilação e validação de cadeia precisa tooocsp.msocsp.com de conectividade de rede de saída, mscrl.microsoft.com e crl.microsoft.com. Essa dependência não for necessária, se qualquer certificado que você carregar tooAPI gerenciamento conter raiz do hello cadeia completa toohello da autoridade de certificação.

* **Acesos de DNS**: O acesso de saída na porta 53 é necessário para a comunicação com servidores DNS. Se um servidor DNS personalizado existir no Olá outra extremidade de um gateway VPN, servidor DNS Olá deve ser acessível da sub-rede Olá gerenciamento de API de hospedagem.

* **Monitoramento de integridade e métricas**: saída de rede conectividade tooAzure monitoramento pontos de extremidade, resolver em Olá domínios a seguir: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Configuração de rota expressa**: uma configuração de cliente comum é toodefine seu próprios rota padrão (0.0.0.0/0), que força a saída da Internet tráfego tooinstead fluxo local. Este fluxo de tráfego invariavelmente quebras de conectividade com o gerenciamento de API do Azure porque o tráfego de saída hello está bloqueado no local ou NAT por conjunto de irreconhecível tooan de endereços que não funcionam com vários pontos de extremidade do Azure. solução Hello é toodefine uma (ou mais) definidos pelo usuário rotas ([UDRs][UDRs]) na sub-rede Olá que contém Olá gerenciamento de API do Azure. Um UDR define as rotas de sub-rede que serão cumpridas em vez de rota padrão de saudação.
  Se possível, é recomendável Olá toouse seguinte configuração:
 * configuração de rota expressa Olá anuncia 0.0.0.0/0 e todo o tráfego de saída no local de túneis de força por padrão.
 * Olá UDR aplicada toohello sub-rede contendo Olá gerenciamento de API do Azure define 0.0.0.0/0 com um tipo de próximo salto da Internet.
 Olá efeito combinado dessas etapas é que o nível de sub-rede Olá UDR tem precedência sobre Olá ExpressRoute forçada de túneis, garantindo, assim, o acesso de Internet de saída de saudação gerenciamento de API do Azure.

>[!WARNING]  
>Não há suporte para o gerenciamento de API do Azure com configurações de rota expressa que **incorretamente entre-anunciar rotas de saudação emparelhamento caminho toohello privada caminho emparelhamento público**. As configurações de ExpressRoute com emparelhamento público definido receberão anúncios de rota da Microsoft para um grande conjunto de intervalos de endereços IP do Microsoft Azure. Se esses intervalos de endereços incorretamente entre anunciados no caminho de emparelhamento privado hello, Olá final significa que todos os pacotes de saída de rede da sub-rede da instância de gerenciamento de API do Azure Olá estão rede do local do cliente tooa incorretamente túnel de força infraestrutura. Esse fluxo de rede interrompe o Gerenciamento de API do Azure. problema de toothis solução Olá é toostop as rotas entre publicidade Olá emparelhamento caminho toohello privada caminho emparelhamento público.


## <a name="troubleshooting"> </a>Solução de problemas
Ao fazer a rede de tooyour de alterações, consulte muito[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate se Olá serviço de gerenciamento de API não perdeu acesso tooany de saudação recursos críticos que ele depende. status da conectividade Olá devem ser atualizados a cada 15 minutos.

## <a name="limitations"> </a>Limitações
* Uma sub-rede que contém instâncias de Gerenciamento de API não pode conter outros tipos de recursos do Azure.
* subrede Hello e hello gerenciamento de API do serviço deve estar no Olá a mesma assinatura.
* Uma sub-rede que contém instâncias de Gerenciamento de API não pode ser movida entre assinaturas.
* Ao usar uma rede virtual interna, somente um endereço IP interno estará disponível no intervalo de saudação indicado na [RFC 1918](https://tools.ietf.org/html/rfc1918), não é possível fornecer um endereço IP público.
* Para implantações de gerenciamento de API de várias regiões, com redes virtuais internas configuradas, os usuários são responsáveis por gerenciar sua próprias conforme eles possuem Olá DNS de balanceamento de carga.


## <a name="related-content"> </a>Conteúdo relacionado
* [Conectando um toobackend de rede Virtual usando o Gateway de Vpn](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Conectar uma rede virtual de diferentes modelos de implantação](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Como toouse Olá Inspetor API tootrace chama no gerenciamento de API do Azure](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
