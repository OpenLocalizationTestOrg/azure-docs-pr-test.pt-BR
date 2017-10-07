---
title: "Serviços de Domínio do Azure AD: diretrizes de rede | Microsoft Docs"
description: "Considerações de rede para os Serviços de Domínio do Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Considerações de rede para Serviços de Domínio do Azure AD
## <a name="how-tooselect-an-azure-virtual-network"></a>Como tooselect uma rede virtual do Azure
Olá diretrizes a seguir ajudam a selecionar um toouse de rede virtual com os serviços de domínio do AD do Azure.

### <a name="type-of-azure-virtual-network"></a>Tipo de rede virtual do Azure
* Você pode habilitar os Serviços de Domínio do Azure AD em uma rede virtual clássica do Azure.
* Os Serviços de Domínio do Azure AD **não podem ser habilitados em redes virtuais criadas usando o Azure Resource Manager**.
* Você pode conectar uma rede virtual com base no Gerenciador de recursos tooa clássico rede virtual no qual os serviços de domínio do AD do Azure está habilitado. Depois disso, você pode usar os serviços de domínio do AD do Azure na rede virtual com base no Gerenciador de recursos de saudação. Para obter mais informações, consulte Olá [conectividade de rede](active-directory-ds-networking.md#network-connectivity) seção.
* **As redes virtuais regionais**: se você planejar toouse uma rede virtual existente, certifique-se de que se trata de uma rede virtual regional.

  * Redes virtuais que usam o mecanismo herdado de grupos de afinidade de saudação não podem ser usadas com os serviços de domínio do AD do Azure.
  * toouse serviços de domínio do AD do Azure, [migrar as redes virtuais herdados redes virtuais tooregional](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Região do Azure para a rede virtual Olá
* Os serviços de domínio do AD do Azure implantado no domínio gerenciado Olá mesma região do Azure como rede virtual hello, que escolha o serviço de saudação tooenable no.
* Selecione uma rede virtual em uma região do Azure com suporte dos Serviços de Domínio do Azure AD.
* Consulte Olá [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/) tooknow página Olá regiões do Azure, na qual os serviços de domínio do AD do Azure está disponível.

### <a name="requirements-for-hello-virtual-network"></a>Requisitos de rede virtual Olá
* **Proximidade tooyour Azure cargas de trabalho**: selecione Olá rede virtual que hospeda atualmente/hospeda máquinas virtuais que precisam acessar os serviços de domínio tooAzure AD.
* **Os servidores DNS personalizado/traga seu próprio**: Certifique-se de que não há nenhum servidor DNS personalizado configurado para a rede virtual hello.
* **Olá de domínios existentes com o mesmo nome de domínio**: Certifique-se de que você não tem um domínio existente com hello mesmo nome de domínio disponível nessa rede virtual. Por exemplo, suponha que você tem um domínio denominado "contoso.com" já está disponível na rede virtual selecionada de saudação. Posteriormente, você pode tentar tooenable um domínio gerenciado de serviços de domínio do AD do Azure com hello mesmo nome de domínio (ou seja, 'contoso.com') no qual a rede virtual. Encontrar uma falha durante a tentativa de serviços de domínio tooenable AD do Azure. Essa falha é devido a conflitos de tooname Olá nome de domínio no qual a rede virtual. Nessa situação, você deve usar tooset um nome diferente, o domínio gerenciado de serviços de domínio do AD do Azure. Como alternativa, você pode desprovisionar domínio existente hello e prossiga em serviços de domínio tooenable AD do Azure.

> [!WARNING]
> Você não pode mover a rede virtual diferente do serviços de domínio tooa depois que você tiver ativado o serviço de saudação.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Grupos de Segurança de Rede e design de sub-rede
Um [grupo de segurança de rede (NSG)](../virtual-network/virtual-networks-nsg.md) contém uma lista de regras de lista de controle de acesso (ACL) que permitem ou negam o tráfego de rede tooyour instâncias VM em uma rede Virtual. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um NSG está associado uma sub-rede, regras de ACL de saudação se aplicam a instâncias de VM Olá tooall nessa sub-rede. Além disso, o tráfego tooan VM individual pode ser restrito adicional associando um NSG toothat VM diretamente.

![Design de sub-rede recomendado](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Práticas recomendadas para escolher uma sub-rede
* Implantar serviços de domínio do AD do Azure tooa **separar sub-rede dedicada** dentro de sua rede virtual do Azure.
* Não se aplicam a subrede NSGs toohello dedicado para seu domínio gerenciado. Se você deve aplicar os NSGs toohello dedicado sub-rede, certifique-se de **não bloquear Olá portas necessárias tooservice e gerenciar o domínio**.
* Não excessivamente restringem o número de saudação de endereços IP disponíveis na sub-rede Olá dedicado para seu domínio gerenciado. Essa restrição impede que o serviço de saudação disponibilizando dois controladores de domínio para seu domínio gerenciado.
* **Não habilite os serviços de domínio do AD do Azure na sub-rede de gateway Olá** da sua rede virtual.

> [!WARNING]
> Quando você associa um NSG com uma sub-rede na qual de serviços de domínio do AD do Azure está habilitado, você pode interromper tooservice de capacidade da Microsoft e gerenciar domínio hello. Além disso, a sincronização entre o seu locatário do Azure AD e seu domínio gerenciado é interrompida. **Olá SLA não se aplica a toodeployments onde um NSG foi aplicado que bloqueia os serviços de domínio do AD do Azure de atualização e o gerenciamento de seu domínio.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Portas necessárias para os Serviços de Domínio do Azure AD
Hello portas a seguir são necessárias para serviços de domínio do AD do Azure tooservice e mantêm seu domínio gerenciado. Certifique-se de que essas portas não estão bloqueadas para a sub-rede Olá no qual você habilitou o seu domínio gerenciado.

| Número da porta | Finalidade |
| --- | --- |
| 443 |Sincronização com seu locatário do Azure AD |
| 3389 |Gerenciamento do seu domínio |
| 5986 |Gerenciamento do seu domínio |
| 636 |Seguro (LDAPS) LDAP acesso tooyour domínio gerenciado |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>NSG de exemplo para redes virtuais com o Azure AD Domain Services
Olá, a tabela a seguir ilustra um exemplo NSG, você pode configurar para uma rede virtual com um domínio gerenciado do serviços de domínio do AD do Azure. Essa regra permite tráfego de entrada da saudação acima tooensure portas especificadas que seu domínio gerenciado permanece corrigido, atualizado e pode ser monitorado pela Microsoft. Olá padrão 'DenyAll' regra se aplica tooall outro tráfego de entrada de saudação à internet.

Além disso, Olá NSG também ilustra como toolock para acesso LDAP seguro sobre Olá da internet. Ignorar esta regra se você não tiver habilitado seguro LDAP acesso tooyour domínio gerenciado pela Olá da internet. Olá NSG contém um conjunto de regras que permitam o acesso LDAPS entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP. Olá NSG regra tooallow LDAPS o acesso por Olá internet de endereços IP especificados tem uma prioridade mais alta que Olá regra DenyAll NSG.

![Acesso ao exemplo NSG toosecure LDAPS por Olá da internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Mais informações** - [Criar um grupo de segurança de rede](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Conectividade de rede
Um domínio gerenciado dos Serviços de Domínio do Azure AD só pode ser habilitado dentro de uma única rede virtual clássica no Azure. Não há suporte para as redes virtuais criadas usando o Azure Resource Manager.

### <a name="scenarios-for-connecting-azure-networks"></a>Cenários para conexão de redes do Azure
Conecte redes virtuais do Azure toouse Olá domínio gerenciado em qualquer Olá os seguintes cenários de implantação:

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Olá Use gerenciados domínio em mais de uma rede de virtual clássico do Azure
Você pode se conectar a outros toohello Azure redes virtuais clássicas do Azure classic rede virtual no qual você habilitou os serviços de domínio do AD do Azure. Essa conexão VPN permite que você toouse Olá gerenciado domínio com suas cargas de trabalho implantadas em outras redes virtuais.

![Conectividade de rede virtual clássica](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Usar Olá domínio gerenciado em uma rede virtual com base no Gerenciador de recursos
Você pode se conectar a um toohello com base no Gerenciador de recursos de rede virtual do Azure classic rede virtual no qual você habilitou os serviços de domínio do AD do Azure. Esta conexão permite que você toouse Olá gerenciado domínio com suas cargas de trabalho implantadas na rede virtual com base no Gerenciador de recursos de saudação.

![Conectividade de rede virtual do Gerenciador de recursos tooclassic](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Opções de conexão de rede
* **Conexões de rede virtual a rede usando conexões VPN site a site**: conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma rede virtual tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE.

    ![Conectividade de rede virtual usando o Gateway de VPN](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Mais informações - conectar redes virtuais usando o gateway de VPN](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **Emparelhamento de rede de conexões de rede virtual a rede usando o virtual**: emparelhamento de rede Virtual é um mecanismo que se conecta a duas redes virtuais no hello mesma região por meio de rede do hello backbone do Azure. Depois de emparelhadas, duas redes virtuais de saudação aparecem como um para todas as finalidades de conectividade. Elas ainda são gerenciadas como recursos separados, mas as máquinas virtuais nessas redes virtuais podem se comunicar diretamente usando o endereço IP privado.

    ![Conectividade de rede virtual usando emparelhamento](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Mais informações - emparelhamento de rede virtual](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Emparelhamento de redes virtuais do Azure](../virtual-network/virtual-network-peering-overview.md)
* [Configurar uma conexão de rede virtual a rede para o modelo de implantação clássico Olá](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Grupos de Segurança de Rede do Azure](../virtual-network/virtual-networks-nsg.md)
* [Criar um Grupo de Segurança de Rede](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
