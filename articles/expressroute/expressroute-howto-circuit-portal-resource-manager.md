---
title: 'Criar e modificar um circuito ExpressRoute: portal do Azure | Microsoft Docs'
description: Este artigo descreve como toocreate, provisionar, verifique se, atualizar, excluir e cancelar o provisionamento de um circuito de rota expressa.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Criar e modificar um circuito do ExpressRoute
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI do Azure](howto-circuit-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-circuit-classic.md)
>

Este artigo descreve como toocreate um circuito de rota expressa do Azure usando hello Azure modelo de implantação de Gerenciador de recursos do Azure do portal e hello. Olá também etapas a seguir mostra como toocheck Olá status do circuito hello, atualizá-lo, ou excluir e seu provisionamento.


## <a name="before-you-begin"></a>Antes de começar
* Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
* Verifique se você tem acesso toohello [portal do Azure](https://portal.azure.com).
* Certifique-se de que você tenha recursos de rede novas permissões toocreate. Se você não tem permissões corretas hello, entre em contato com o administrador da conta.
* Você pode [exibir um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de começar em ordem toobetter entender as etapas de saudação.

## <a name="create-and-provision-an-expressroute-circuit"></a>Criar e provisionar um circuito do ExpressRoute
### <a name="1-sign-in-toohello-azure-portal"></a>1. Entrar toohello portal do Azure
Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e entre com sua conta do Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Criar um novo circuito do ExpressRoute
> [!IMPORTANT]
> O circuito de rota expressa será cobrado do momento Olá que uma chave de serviço é emitida. Certifique-se de que você executar esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.
> 
> 

1. Você pode criar um circuito de rota expressa selecionando Olá opção toocreate um novo recurso. Clique em **novo** > **rede** > **ExpressRoute**, conforme mostrado no Olá a imagem a seguir:
   
    ![Criar um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Depois de clicar em **ExpressRoute**, você verá Olá **circuito de rota expressa criar** folha. Quando você estiver preenchendo valores hello nesta folha, certifique-se de que você especifique a camada SKU correta hello e medição de dados.
   
   * **camada** determina se um complemento padrão ou premium do ExpressRoute está habilitado. Você pode especificar **padrão** tooget Olá SKU standard ou **Premium** para o complemento do premium Olá.
   * **Dados de medição** determina o tipo de saudação de cobrança. Você pode especificar **Limitado** para um plano de dados limitado e **Ilimitado** para um plano de dados ilimitado. Observe que você pode alterar o tipo de cobrança de saudação do **Metered** muito**Unlimited**, mas você não pode alterar o tipo de saudação do **Unlimited** muito**Metered**.
     
     ![Configurar a camada de SKU hello e medição de dados](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Esteja ciente de que Olá local de emparelhamento indica Olá [local físico](expressroute-locations.md) onde você é emparelhamento com a Microsoft. Isso é **não** vinculado muito propriedade "Local", que se refere a geografia toohello onde se encontra Olá provedor de recursos de rede do Azure. Embora eles não estão relacionados, é toochoose uma boa prática toohello de geograficamente fechar um provedor de recursos de rede local de emparelhamento do circuito hello. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Circuitos de saudação do modo de exibição e propriedades
**Exibir todos os circuitos Olá**

Você pode exibir todos os circuitos Olá criado selecionando **todos os recursos** no menu do lado esquerdo de saudação.

![Exibir circuitos](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Exibir propriedades de saudação**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Exibir propriedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Enviar Olá tooyour chave conectividade provedor para provisionamento
Nesta folha **status do provedor** fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação. **Status de circuito** informa o estado de saudação em Olá lado da Microsoft. Para obter mais informações sobre estados de provisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.

Quando você cria um novo circuito de rota expressa, circuito Olá estará em Olá estado a seguir:

Status do provedor: não provisionado<BR>
Status do circuito: habilitado

![Iniciar o processo de provisionamento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

circuito Olá alterará toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:

Status do provedor: provisionando<BR>
Status do circuito: habilitado

Para você toobe capaz de toouse um circuito de rota expressa, ele deve ser Olá estado a seguir:

Status do provedor: provisionado<BR>
Status do circuito: habilitado

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação
Você pode exibir as propriedades de saudação do circuito Olá que você está interessado em selecionando-a. Verificar Olá **status do provedor** e certifique-se de que ele foi movido muito**provisionado** antes de continuar.

![Status do circuito e do provedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Criar sua configuração de roteamento
Para obter instruções passo a passo, consulte toohello [configuração de roteamento de circuito de rota expressa](expressroute-howto-routing-portal-resource-manager.md) artigo toocreate e modificar os emparelhamentos de circuito.

> [!IMPORTANT]
> Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade. Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Vincular um circuito de rota expressa do tooan de rede virtual
Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual. Saudação de uso [vinculação virtual redes circuitos tooExpressRoute](expressroute-howto-linkvnet-arm.md) quando você trabalha com o modelo de implantação do Gerenciador de recursos de saudação do artigo.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Obter status de saudação de um circuito de rota expressa
Você pode exibir o status de saudação de um circuito, selecionando-o. 

![Status de um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Modificando um circuito do ExpressRoute
Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.

Você pode fazer Olá sem tempo de inatividade a seguir:

* Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.
* Aumento de largura de banda de saudação do circuito ExpressRoute fornecido há capacidade disponível na porta hello. Observe que a largura de banda de saudação de um circuito de downgrade não é suportado. 
* Alterar o plano de dados limitados tooUnlimited dados de medição de saudação. Observe que esse plano de medição Olá alteração de dados ilimitada tooMetered que dados não tem suporte.
* Você pode habilitar e desabilitar *Permitir Operações Clássicas*.

Para obter mais informações sobre limitações e limites, consulte toohello [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

toomodify um circuito de rota expressa, clique em Olá **configuração** conforme mostrado na figura abaixo a saudação.

![Modificar o circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Você pode modificar a largura de banda hello, SKU, modelo de cobrança e permitem operações clássicas dentro de folha de configuração de saudação.

> [!IMPORTANT]
> Você pode ter o circuito de rota expressa Olá toorecreate se não houver capacidade insuficiente na porta existente Olá. Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.
>
> Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções. Downgrade da largura de banda requer que o circuito de rota expressa Olá toodeprovision e, em seguida, Reprovisionar um novo circuito de rota expressa.
> 
> Desabilitar complemento premium operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desprovisionamento e exclusão de um circuito do ExpressRoute
Você pode excluir o circuito de rota expressa selecionando Olá **excluir** ícone. Observe o seguinte hello:

* Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa. Se essa operação falhar, verifique se as redes virtuais são vinculadas toohello circuito.
* Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado** você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado. Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.
* Se o provedor de serviços de saudação tem desprovisionada circuito hello (provedor de serviços de saudação estado de provisionamento está definido muito**não provisionado**), em seguida, você pode excluir o circuito de saudação. Isso interromperá a cobrança para o circuito Olá

## <a name="next-steps"></a>Próximas etapas
Depois de criar o circuito, certifique-se de que Olá a seguir:

* [Criar e modificar o roteamento do circuito do ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Vincular sua rede virtual de tooyour circuito de rota expressa](expressroute-howto-linkvnet-arm.md)

