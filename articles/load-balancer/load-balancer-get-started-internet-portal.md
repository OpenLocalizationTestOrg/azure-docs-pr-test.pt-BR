---
title: Balanceador de carga aaaCreate um voltados para Internet - portal do Azure | Microsoft Docs
description: "Saiba como o balanceador de carga toocreate um com a Internet usando o Gerenciador de recursos Olá portal do Azure"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Criando um balanceador de carga para a Internet usando Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [Saiba usando implantação clássica de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Isso abrange a sequência de Olá das tarefas individuais que têm toocreate toobe feito um balanceador de carga e explique detalhadamente o que está sendo feito a meta de saudação tooaccomplish.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>O que é necessário toocreate um balanceador de carga para a Internet?

Você precisa toocreate e configure Olá objetos toodeploy um balanceador de carga a seguir.

* Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.
* Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.
* Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.
* Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.
* Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.

É possível obter mais informações sobre componentes do balanceador de carga com o gerenciador de recursos do Azure em [Suporte do Azure Resource Manager para o Balanceador de Carga](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Configurar um balanceador de carga no portal do Azure

> [!IMPORTANT]
> Este exemplo pressupõe que você tem uma rede virtual chamada **myVNet**. Consulte também[criar rede virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo isso. Ele também considera que há uma sub-rede dentro de **myVNet** chamado **LB sub-rede ser** e duas VMs chamadas **web1** e **web2** respectivamente dentro Olá mesmo chamada de conjunto de disponibilidade **myAvailSet** na **myVNet**. Consulte também[este link](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate VMs.

1. Em um navegador, navegue toohello portal do Azure: [http://portal.azure.com](http://portal.azure.com) e faça logon com sua conta do Azure.
2. Olá superior esquerda da tela hello selecione **novo** > **rede** > **balanceador de carga.**
3. Em Olá **criar balanceador de carga** folha, digite um nome para o balanceador de carga. Aqui, ele é chamado de **myLoadBalancer**.
4. Em **Tipo**, selecione **Público**.
5. Em **Endereço IP público**, crie um novo IP público chamado **myPublicIP**.
6. Em Grupo de Recursos, selecione **myRG**. Em seguida, selecione uma **Localização** apropriada e clique em **OK**. Balanceador de carga Olá iniciará toodeploy e levará alguns minutos toosuccessfully completos de implantação.

    ![Atualizando o grupo de recursos do balanceador de carga](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Criar um pool de endereços de back-end

1. Depois que o balanceador de carga for implantado com êxito, selecione-o dentro de seus recursos. Em configurações, selecione Pools de Back-end. Digite um nome para o seu pool de back-end. Em seguida, clique em Olá **adicionar** botão em direção à parte superior de saudação da folha de saudação que aparece.
2. Clique em **adicionar uma máquina virtual** em Olá **Adicionar pool de back-end** folha.  Selecione **Escolher um conjunto de disponibilidade** em **Conjunto de disponibilidade** e selecione **myAvailSet**. Em seguida, selecione **escolha máquinas virtuais de saudação** Olá seção máquinas virtuais na folha de saudação em e clique em **web1** e **web2**, Olá duas VMs criadas para balanceamento de carga. Certifique-se de que ambos têm marcas de seleção azul toohello restantes conforme mostrado na imagem de saudação abaixo. Em seguida, clique em **selecione** na folha seguida Okey em Olá **máquinas virtuais escolha** folha e, em seguida, **Okey** em Olá **Adicionar pool de back-end** folha.

    ![Adicionar pool de endereços de back-end toohello- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Verifique se as notificações de lista suspensa de toomake tem uma atualização em relação ao salvar o pool de back-end de Balanceador de carga de saudação na interface de rede adição tooupdating Olá para ambos Olá VMs **web1** e **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Criar uma investigação, regra de balanceamento de carga e regras de NAT

1. Crie um teste de integridade.

    Em Configurações do balanceador de carga, selecione Investigações. Em seguida, clique em **adicionar** localizado na parte superior de saudação da folha de saudação.

    Há um teste em tooconfigure de duas maneiras: HTTP ou TCP. Este exemplo mostra HTTP, mas TCP pode ser configurado de maneira semelhante.
    Atualize as informações necessárias hello. Conforme mencionado, **myLoadBalancer** balanceará a carga do tráfego na Porta 80. caminho de saudação selecionado é HealthProbe.aspx, intervalo é de 15 segundos e limite não íntegro é 2. Quando terminar, clique **Okey** toocreate investigação de saudação.

    Passe o ponteiro sobre Olá 'i' ícone toolearn mais sobre essas configurações individuais e como eles podem ser alterados toocater tooyour requisitos.

    ![Adicionando uma investigação](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Crie uma regra de balanceador de carga.

    Clique em regras de saudação de balanceamento de carga da seção configurações do balanceador de carga. Na nova folha de saudação, clique em **adicionar**. Nomeie a regra. Aqui, seu nome é HTTP. Escolha Olá portas de front-end e back-end. Aqui, o valor 80 é escolhido para ambas. Escolha **back-end LB** como o pool de back-end e Olá criado anteriormente **HealthProbe** como Olá investigação. Outras configurações podem ser definidas de acordo com os requisitos de tooyour. Clique em regra de balanceamento de carga de saudação toosave Okey.

    ![Adicionando uma regra de balanceamento de carga](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Criar regras NAT de entrada

    Clique em regras de NAT de entrada na seção de configurações de saudação do balanceador de carga. Em Olá nova folha, clique em **adicionar**. Em seguida, nomeie a regra NAT de entrada. Aqui, ela é chamada de **inboundNATrule1**. destino de saudação deve ser Olá que IP público criado anteriormente. Selecione personalizado no serviço e protocolo de saudação você gostaria que toouse. Aqui, a opção TCP foi selecionada. Insira a porta de saudação 3441 e Olá 3389 de porta de destino, nesse caso. em seguida, clique em toosave Okey essa regra.

    Depois de criar a regra primeiro hello, repita essa etapa para Olá segunda regra NAT de entrada chamada inboundNATrule2 do 3442 tooTarget porta 3389.

    ![Adicionando uma regra NAT de entrada](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Remover um balanceador de carga

você deseja tooremove de Balanceador de carga de toodelete um balanceador de carga, selecione hello. Em Olá *balanceador de carga* folha, clique em **excluir** localizado na parte superior de saudação da folha de saudação. Em seguida, selecione **Sim** quando solicitado.

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-cli.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
