---
title: 'Como tooconfigure roteamento (emparelhamento) para um circuito de rota expressa: Gerenciador de recursos: Azure | Microsoft Docs'
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Criar e modificar o emparelhamento de um circuito de ExpressRoute

Este artigo ajuda você a criar e gerenciar a configuração de roteamento para um circuito de rota expressa no modelo de implantação do Gerenciador de recursos do hello usando Olá portal do Azure. Você também pode verificar status hello, update ou delete e desprovisionar emparelhamentos de um circuito de rota expressa. Se você quiser toouse toowork um método diferente com o circuito, selecione um artigo de saudação lista a seguir:


## <a name="configuration-prerequisites"></a>Pré-requisitos de configuração

* Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) página hello [requisitos de roteamento](expressroute-routing.md) página e hello [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração de página.
* Você deve ter um circuito do ExpressRoute ativo. Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar. Olá circuito de rota expressa deve ser em um estado habilitado e configurado para você toobe toorun capaz de saudação cmdlets nas seções próximas hello.
* Se você planeja toouse um hash MD5/chave compartilhado, ser toouse-se de que isso em ambos os lados da saudação túnel e limite Olá o número de máximo de tooa de caracteres de 25.

Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2. Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você. 

> [!IMPORTANT]
> Estamos atualmente não anuncie emparelhamentos configurados pelos provedores de serviço por meio do portal de gerenciamento de serviços de saudação. Estamos trabalhando para habilitar esse recurso em breve. Verifique com seu provedor de serviços antes de configurar os emparelhamentos via protocolo BGP.
> 
> 

Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute. Você pode configurar emparelhamentos em qualquer ordem escolhida. No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.

## <a name="azure-private-peering"></a>Emparelhamento privado do Azure

Esta seção ajuda você a criar, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-private-peering"></a>toocreate emparelhamento particular do Azure

1. Configure o circuito de rota expressa hello. Certifique-se de que o circuito de saudação está totalmente provisionado pelo provedor de conectividade de saudação antes de continuar.

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configure o emparelhamento particular do Azure para o circuito de saudação. Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:

  * Um /30 sub-rede para o link primário hello. subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.
  * Um /30 sub-rede para o link secundário hello. subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes. Você pode usar um número de AS privado para esse emparelhamento. Não use 65515.
  * **Opcional -** um hash MD5 se você escolher toouse um.
3. Selecione a linha hello de emparelhamento particular do Azure, conforme mostrado no exemplo a seguir de saudação:

  ![privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Configure o emparelhamento privado. Olá a imagem a seguir mostra um exemplo de configuração:

  ![configurar o emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Salve configuração Olá depois que você especificou todos os parâmetros. Após a configuração de saudação foi aceita com êxito, você verá algo semelhante toohello exemplo a seguir:

  ![salvar emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview privado emparelhamento detalhes do Azure

Você pode exibir as propriedades de saudação do emparelhamento particular do Azure, selecionando o emparelhamento de saudação.

![exibir emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuração emparelhamento particular do Azure

Você pode selecionar a linha hello para emparelhamento e modificar propriedades de emparelhamento hello.

![atualizar emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete emparelhamento particular do Azure

Você pode remover a configuração do emparelhamento selecionando o ícone de excluir hello, conforme mostrado no Olá a imagem a seguir:

![excluir emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Emparelhamento público do Azure

Esta seção ajuda você a criar, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-public-peering"></a>toocreate emparelhamento público do Azure

1. Configure o circuito do ExpressRoute. Certifique-se de que o circuito de saudação está totalmente provisionado pelo provedor de conectividade de saudação antes de continuar ainda mais.

  ![listar emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configure o emparelhamento público do Azure para o circuito de saudação. Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:

  * Um /30 sub-rede para o link primário hello. Precisa ser um prefixo IPv4 público válido.
  * Um /30 sub-rede para o link secundário hello. Precisa ser um prefixo IPv4 público válido.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
  * **Opcional -** um hash MD5 se você escolher toouse um.
3. Selecione Olá linha emparelhamento pública do Azure, conforme mostrado na Olá a imagem a seguir:

  ![selecionar linha de emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Configure o emparelhamento público. Olá a imagem a seguir mostra um exemplo de configuração:

  ![Configurar o emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Salve configuração Olá depois que você especificou todos os parâmetros. Após a configuração de saudação foi aceita com êxito, você verá algo semelhante toohello exemplo a seguir:

  ![Salvar a configuração do emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview público emparelhamento detalhes do Azure

Você pode exibir as propriedades de saudação do emparelhamento público do Azure, selecionando o emparelhamento de saudação.

![exibir propriedades do emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuração de emparelhamento pública do Azure

Você pode selecionar a linha hello para emparelhamento e modificar propriedades de emparelhamento hello.

![selecionar linha de emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete emparelhamento público do Azure

Você pode remover a configuração do emparelhamento selecionando o ícone de excluir hello, conforme mostrado no exemplo a seguir de saudação:

![excluir emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Emparelhamento da Microsoft

Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.

> [!IMPORTANT]
> Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft hello, mesmo se os filtros de roteamento não estão definidos. Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito. Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate emparelhamento da Microsoft

1. Configure o circuito do ExpressRoute. Certifique-se de que o circuito de saudação está totalmente provisionado pelo provedor de conectividade de saudação antes de continuar ainda mais.

  ![listar emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configure o emparelhamento do circuito de saudação do Microsoft. Certifique-se de que você tenha Olá seguintes informações antes de continuar.

  * Um /30 sub-rede para o link primário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
  * Um /30 sub-rede para o link secundário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
  * Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação. Somente prefixos de endereços IP públicos são aceitos. Se você planejar toosend um conjunto de prefixos, você pode enviar uma lista separada por vírgulas. Esses prefixos devem ser registrado tooyou em um RIR / IRR.
  * **Opcional -** cliente ASN: se você estiver prefixos de anúncios que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, eles são registrados.
  * Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.
  * **Opcional -** um hash MD5 se você escolher toouse um.
3. Você pode selecionar Olá emparelhamento desejar tooconfigure, conforme mostrado no Olá a seguir exemplo. Selecione a linha de emparelhamento de Microsoft hello.

  ![selecionar linha de emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Configure o emparelhamento da Microsoft. Olá a imagem a seguir mostra um exemplo de configuração:

  ![configurar emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Salve configuração Olá depois que você especificou todos os parâmetros.

  Se o seu circuito obtém tooa 'Validação necessária' estado (conforme mostrado na imagem Olá), você deve abrir um tooshow de tíquete de suporte prova de propriedade da equipe de suporte de tooour Olá prefixos.

  ![Salvar a configuração de emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  Você pode abrir um tíquete de suporte diretamente do portal hello, conforme mostrado no exemplo a seguir de saudação:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Após a configuração de saudação foi aceita com êxito, você verá algo semelhante toohello imagem a seguir:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>tooview detalhes de emparelhamento da Microsoft

Você pode exibir as propriedades de saudação do emparelhamento público do Azure, selecionando o emparelhamento de saudação.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate configuração de emparelhamento da Microsoft

Você pode selecionar a linha hello para emparelhamento e modificar propriedades de emparelhamento hello.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete emparelhamento da Microsoft

Você pode remover a configuração do emparelhamento selecionando o ícone de excluir hello, conforme mostrado no Olá a imagem a seguir:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Próximas etapas

Próxima etapa, [vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-portal-resource-manager.md)
* Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).
* Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).
* Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).
