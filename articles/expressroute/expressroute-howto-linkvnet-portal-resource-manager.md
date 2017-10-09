---
title: 'Vincular um circuito de rota expressa do tooan de rede virtual: portal do Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Conectar uma rede virtual de tooan circuito de rota expressa
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI do Azure](howto-linkvnet-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-linkvnet-classic.md)
> 

Este artigo ajuda você a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e Olá portal do Azure. Redes virtuais podem ser na Olá mesma assinatura, ou eles podem fazer parte de outra assinatura.

## <a name="before-you-begin"></a>Antes de começar
* Saudação de revisão [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
* Você deve ter um circuito do ExpressRoute ativo.
  
  * Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter circuito Olá habilitado por seu provedor de conectividade.
  * Verifique se o emparelhamento privado do Azure está configurado para seu circuito. Consulte Olá [Configurar roteamento](expressroute-howto-routing-portal-resource-manager.md) artigo para obter instruções de roteamentos.
  * Certifique-se de que o emparelhamento particular do Azure está configurado e Olá emparelhamento via protocolo BGP entre sua rede e a Microsoft está ativo para que você pode habilitar a conectividade de ponta a ponta.
  * Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados. Siga as instruções de saudação muito[criar um gateway de rede virtual para o ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Um gateway de rede virtual para a rota expressa usa Olá GatewayType 'ExpressRoute', não VPN.

* Você pode vincular o circuito de rota expressa padrão do too10 redes virtuais tooa. Todas as redes virtuais devem estar em Olá mesma região geopolíticas ao usar um circuito de rota expressa padrão. 
* Você pode vincular uma rede virtual fora da região geopolíticas Olá Olá circuito de rota expressa ou conectar-se um grande número de redes virtuais tooyour circuito de rota expressa se você habilitou o complemento do premium Olá rota expressa. Verificar Olá [perguntas frequentes sobre](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.
* Você pode [exibir um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) antes de toobetter início entender as etapas de saudação.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura

### <a name="toocreate-a-connection"></a>toocreate uma conexão

> [!NOTE]
> Informações de configuração de BGP não aparecerá se o provedor de camada 3 Olá configurado seu emparelhamentos. Se o circuito está em um estado de provisionamento, você deve ser capaz de toocreate conexões.
>

1. Certifique-se de que o circuito de ExpressRoute e emparelhamento privado do Azure foram configurados com êxito. Siga as instruções de saudação em [criar um circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [Configurar roteamento](expressroute-howto-routing-arm.md). O circuito de rota expressa deve ter aparência Olá a imagem a seguir:

    ![Captura de tela de circuito do ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. Agora você pode começar o provisionamento de uma conexão toolink seu gateway de rede virtual tooyour circuito de rota expressa. Clique em **Conexão** > **adicionar** tooopen Olá **Adicionar conexão** folha e, em seguida, configure os valores de saudação.

    ![Adicionar a captura de tela de conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Depois que a conexão tiver sido configurado com êxito, seu objeto de conexão mostrará informações Olá para conexão hello.

     ![Captura de tela de objeto de conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete uma conexão
Você pode excluir uma conexão selecionando Olá **excluir** ícone na folha de saudação para sua conexão.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar uma rede virtual em um circuito de tooa assinatura diferente
Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas. a Figura Olá abaixo mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização.
- Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços, mas eles podem compartilhar uma única rede rota expressa circuito tooconnect tooyour back local.
- Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello. Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.

    > [!NOTE]
    > Encargos de largura de banda e conectividade para o circuito dedicado de saudação será proprietário do circuito de rota expressa toohello aplicado. Todas as redes virtuais compartilham Olá mesma largura de banda.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Administração – proprietários e usuários do circuito

Olá 'proprietário do circuito' é um usuário autorizado Power Olá recursos de circuito de rota expressa. proprietário do circuito Olá pode criar autorizações que podem ser trocadas por 'usuários do circuito'. Os usuários do circuito são proprietários da rede virtual gateways que não estão no hello mesma assinatura conforme Olá circuito de rota expressa. Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).

proprietário do circuito Olá tem autorizações de toomodify e revoke power Olá a qualquer momento. Revogando uma resulta de autorização em todas as conexões de link que está sendo excluídas da assinatura de saudação cujo acesso foi revogado.

### <a name="circuit-owner-operations"></a>Operações do proprietário do circuito

**toocreate uma autorização de conexão**

proprietário do circuito Olá cria uma autorização. Isso resulta na criação de saudação de uma chave de autorização que pode ser usado por um tooconnect de usuário do circuito seu gateways de rede virtual toohello circuito de rota expressa. Uma autorização é válida apenas para uma conexão.

1. Na folha de rota expressa hello, clique em **autorizações** e, em seguida, digite um **nome** para autorização hello e clique em **salvar**.

    ![Autorizações](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Depois de salvo, configuração de saudação copiar Olá **ID de recurso** e hello **chave de autorização**.

    ![Chave de autorização](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete uma autorização de conexão**

Você pode excluir uma conexão selecionando Olá **excluir** ícone na folha de saudação para sua conexão.

### <a name="circuit-user-operations"></a>Operações do usuário do circuito

usuários do circuito Olá precisa Olá ID de recurso e uma chave de autorização do proprietário do circuito hello. 

**tooredeem uma autorização de conexão**

1.  Clique em Olá **+ novo** botão.

    ![Clique em Novo](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Procurar **"Conexão"** em Olá Marketplace, selecione-o e clique em **criar**.

    ![Pesquisar conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Verifique se Olá **o tipo de Conexão** está definido muito "Rota expressa".


4.  Preencha os detalhes de saudação, clique em **Okey** na folha de Noções básicas de saudação.

    ![Folha de Noções básicas](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  Em Olá **configurações** folha, selecione Olá **gateway de rede Virtual** e verifique Olá **resgatar autorização** caixa de seleção.

6.  Digite hello **chave de autorização** e hello **par circuito URI** e dê um nome de conexão de saudação. Clique em **OK**.

    ![Folha de configurações](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Revise as informações de Olá Olá **resumo** folha e clique em **Okey**.


**toorelease uma autorização de conexão**

Você pode liberar uma autorização Excluindo conexão Olá que vincula a rede virtual de toohello Olá de circuito ExpressRoute.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
