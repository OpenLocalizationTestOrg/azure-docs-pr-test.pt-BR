---
title: "aaaLoad balanceamento em várias configurações de IP no Azure | Microsoft Docs"
description: "Balanceamento de carga entre as configurações de IP primárias e secundárias."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Balanceamento de carga no várias configurações de IP usando Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

Este artigo descreve como toouse balanceador de carga do Azure com o IP de vários endereços em uma interface de rede secundária (NIC). Para este cenário, temos duas VMs que executam o Windows, cada um com um principal e uma placa de rede secundária. Cada um dos secundários de saudação NICs têm duas configurações de IP. Cada VM hospeda os sites contoso.com e fabrikam.com. Cada site é associado tooone Olá de configurações de IP em uma NIC secundário. Olá Usamos o balanceador de carga do Azure tooexpose dois front-end endereços IP, uma para cada site, toodistribute tráfego toohello respectiva configuração de IP para o site de saudação. Esse cenário usa Olá o mesmo número de porta entre os front-ends, bem como os dois endereços IP do pool de back-end.

![Imagem de cenário do LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Pré-requisitos
Este exemplo presume que você tenha um grupo de recursos denominado *contosofabrikam* com hello a seguinte configuração:
 -  inclui uma rede virtual denominada *myVNet*, duas VMs chamadas *VM1* e *VM2* Olá respectivamente no mesmo conjunto nomeada de disponibilidade *myAvailset*. 
 - cada VM tem um NIC primário e um NIC secundário. Olá primário NICs são nomeados *VM1NIC1* e *VM2NIC1* e secundário Olá NICs são nomeados *VM1NIC2* e *VM2NIC2*. Para saber mais sobre como criar VMs com vários NICs, confira [Criar uma VM com vários NICs usando o PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo de tooload etapas em várias configurações de IP

Siga estas etapas abaixo o cenário de saudação tooachieve descritos neste artigo:

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>Etapa 1: Configurar hello NICs secundárias para cada VM

Para cada VM em sua rede virtual, adicione uma configuração de IP de conjunto para Olá NIC secundário da seguinte maneira:  

1. Em um navegador, navegue toohello portal do Azure: http://portal.azure.com e faça logon com sua conta do Azure.
2. Olá superior esquerda da tela hello, clique Olá ícone do grupo de recursos e clique em Olá Olá de grupo de recursos VMs estão localizadas em (por exemplo, *contosofabrikam*). Olá **grupos de recursos** folha que lista todos os recursos de saudação junto com interfaces de rede Olá para Olá VMs agora é exibida.
3. secundário toohello NIC de cada VM, adicione uma configuração de IP, da seguinte maneira:
    1. Selecione a interface de rede de Olá que deseja tooadd Olá IP configuração.
    2. Olá folha que aparece para Olá NIC que você selecionou, clique em **as configurações de IP**. Em seguida, clique em **adicionar** em direção à parte superior de saudação da folha de saudação que aparece.
    3. Em Olá **as configurações de IP adicionar** folha, adicionar uma segunda toohello de configuração de IP NIC da seguinte maneira: 
        1. Digite um nome para a sua configuração de IP secundária (por exemplo, para VM1 e VM2 nome hello as configurações de IP como *VM1NIC2 ipconfig2* e *VM2NIC2 ipconfig2* respectivamente).
        2. Para **Endereço IP privado**, para **Alocação**, selecione **Estático**.
        3. Clique em **OK**.
        4. Quando Olá segunda configuração IP hello NIC secundário for concluído, ele é exibido no hello **as configurações de IP** folha de configurações para Olá fornecido NIC.

### <a name="step-2-create-a-load-balancer"></a>ETAPA 2: Criar um balanceador de carga

Crie um balanceador de carga da seguinte maneira:

1. Em um navegador, navegue toohello portal do Azure: http://portal.azure.com e faça logon com sua conta do Azure.
2. Olá superior esquerda da tela hello, clique em **novo** > **rede** > **balanceador de carga**. Em seguida, clique em **Criar**.
3. Em Olá **criar balanceador de carga** folha, digite um nome para o balanceador de carga. Aqui, ele é chamado de *mylb*.
4. Em Endereço IP público, crie um novo IP público chamado **PublicIP1**.
5. Grupo de recursos, selecione Olá grupo de recursos existente das suas máquinas virtuais (por exemplo, *contosofabrikam*). Em seguida, selecione uma Localização apropriada e clique em **OK**. Balanceador de carga Olá iniciará toodeploy e levará alguns minutos toosuccessfully completos de implantação.
6. Uma vez implantado, o balanceador de carga Olá é exibido como um recurso em seu grupo de recursos.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>Etapa 3: Configurar o pool IP de front-end Olá

Configure seu pool de IPs de front-end para cada site (Contoso e Fabrikam) da seguinte maneira:

1. No portal de saudação, clique em **mais serviços** > tipo **endereço IP público** Olá caixa de filtro e, em seguida, clique em **endereços IP públicos**. Clique em **adicionar** em direção à parte superior de saudação da folha de saudação que aparece.
2. Configurar dois endereços IP públicos (*PublicIP1* e *PublicIP2*) para os dois sites (contoso e fabrikam) da seguinte maneira:
    1. Digite um nome para seu endereço IP de front-end.
    2. Para **grupo de recursos**, selecione Olá grupo de recursos existente Olá VMs (por exemplo, *contosofabrikam*).
    3. Para **local**, selecione Olá mesmo local como Olá VMs.
    4. Clique em **OK**.
    5. Após a criação de endereços IP públicos de saudação dois, eles são exibidos no hello **IP público** folha de endereços.
3. No portal de saudação, clique em **mais serviços** > tipo **balanceador de carga** Olá caixa de filtro e, em seguida, clique em **balanceador de carga**.  
4. Selecione o balanceador de carga de saudação (*mylb*) que você deseja que o pool de IP de front-end tooadd Olá para.
5. Em **Configurações**, selecione **Pools de Front-end**. Em seguida, clique em **adicionar** em direção à parte superior de saudação da folha de saudação que aparece.
6. Digite um nome para seu endereço IP de front-end (*fabrikamfe* ou **contosofe*).
7. Clique em **endereço IP** e Olá **endereço IP público escolha** folha, endereços IP de saudação select para o front-end (*PublicIP1* ou *PublicIP2*).
8. Repita as etapas de 3 too7 dentro essa seção toocreate Olá segundo front-end endereço IP.
9. Quando a configuração de pool IP de front-end de saudação for concluída, os dois endereços IP de front-end são exibidos no hello **Pool de IP de front-end** folha do balanceador de carga. 
    
### <a name="step-4-configure-hello-backend-pool"></a>Etapa 4: Configurar o pool de back-end Olá   
Configure pools de endereços de back-end Olá no balanceador de carga para cada site (Contoso e Fabrikam) da seguinte maneira:
        
1. No portal de saudação, clique em **mais serviços** > tipo de Balanceador de carga na caixa de filtro hello e, em seguida, clique em **balanceador de carga**.  
2. Selecione o balanceador de carga de saudação (*mylb*) que você deseja tooadd pools de back-end Olá para.
3. Em **Configurações**, selecione **Pools de Back-end**. Digite um nome para o pool de back-ends (por exemplo, *contosopool* ou *fabrikampool*). Em seguida, clique em Olá **adicionar** botão em direção à parte superior de saudação da folha de saudação que aparece. 
4. Para **Associado a**, selecione **Conjunto de disponibilidade**.
5. Para **Conjunto de Disponibilidade**, selecione **myAvailset**.
6. Adicione as Configurações de IP da rede de destino, para as duas VMs, da seguinte maneira (veja a Figura 2):  
    1. Para **Máquina Virtual de destino**, selecione Olá VM que você deseja que o pool de back-end de toohello tooadd (por exemplo, VM1 ou VM2).
    2. Para **configuração de rede IP**, selecione configuração de IP de NICs secundário Olá para a VM (por exemplo, VM1NIC2 ipconfig2 ou VM2NIC2 ipconfig2).
    ![Imagem do cenário de BC](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Figura 2**: configuração de Balanceador de carga Olá com pools de back-end  
7. Clique em **OK**.
8. Quando o configuração do pool de back-end Olá for concluída, ambos os pools de endereços de back-end são exibidos no hello **folha de pool de back-end** do balanceador de carga.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>ETAPA 5: Configurar um teste de integridade para seu balanceador de carga
Configure uma investigação de integridade para o balanceador de carga da seguinte maneira:
    1. No portal de saudação, clique em mais serviços > tipo de Balanceador de carga na caixa de filtro hello e, em seguida, clique em **balanceador de carga**.  
    2. Selecione o balanceador de carga de saudação que deseja que os pools de back-end tooadd Olá para.
    3. Em **Configurações**, selecione **Investigação de integridade**. Em seguida, clique em **adicionar** em direção à parte superior de saudação da folha de saudação que aparece.
    4. Digite um nome para a investigação de integridade da saudação (por exemplo, HTTP) e, em seguida, clique em **Okey**.

### <a name="step-6-configure-load-balancing-rules"></a>ETAPA 6: Configurar regras de balanceamento de carga
Configure as regras de balanceamento de carga (*HTTPc* e *HTTPf*) para cada site da seguinte maneira:
    
1. Em **Configurações**, selecione **Investigação de integridade**. Em seguida, clique em **adicionar** em direção à parte superior de saudação da folha de saudação que aparece.
2. Para **nome**, digite um nome para a regra de balanceamento de carga de saudação (por exemplo, *HTTPc* para a Contoso, ou *HTTPf* para a Fabrikam)
3. Para o endereço IP de Frontend, selecione o endereço IP de front-end Olá Olá (por exemplo *Contosofe* ou *Fabrikamfe*)
4. Para **porta** e **porta de back-end**, mantenha o valor padrão de saudação **80**.
5. Para **IP flutuante (retorno de servidor direto)** clique em **Habilitado**.
6. Clique em **OK**.
7. Repita as etapas de 1 too6 dentro de regra de Balanceador de carga segundo essa seção toocreate hello.
8. Ao balanceamento de carga de saudação regras de configuração for concluída, as regras de ((*HTTPc* e *HTTPf*) são exibidos no hello **regras de balanceamento de carga** folha do balanceador de carga.

### <a name="step-7-configure-dns-records"></a>ETAPA 7: Configurar registros DNS
Por fim, você deve configurar o recurso registros toopoint toohello front-end respectivo endereço IP do DNS saudação do balanceador de carga. Você pode hospedar seus domínios no DNS do Azure. Para saber mais sobre como usar o DNS do Azure com o Load Balancer, confira [Usar o DNS do Azure com outros serviços do Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre como o balanceamento de carga de toocombine serviços no Azure em [usando os serviços de balanceamento de carga no Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Saiba como você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas de Balanceador de carga no [de análise de Log para o balanceador de carga do Azure](../load-balancer/load-balancer-monitor-log.md).
