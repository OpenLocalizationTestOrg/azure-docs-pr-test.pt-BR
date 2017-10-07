---
title: aaaDeploy VMs do Linux em uma rede existente com o portal do Azure | Microsoft Docs
description: "Implante uma VM do Linux em uma rede Virtual do Azure existente usando o portal de saudação."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Como toodeploy uma máquina virtual do Linux em uma rede Virtual do Azure existente com hello portal do Azure

Este artigo mostra como toodeploy uma máquina virtual (VM) em uma rede virtual existente (VNet). Os ativos do Azure como VNets e grupos de segurança de rede devem ser recursos estáticos e de longa duração que raramente são implantados. Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por constantes reimplantações sem nenhuma infraestrutura de toohello efeitos adversos. Pensar em uma rede virtual como sendo um tradicional comutador de rede de hardware - você não precisará tooconfigure alternar de um novo hardware com cada implantação.  

Com uma rede virtual configurada corretamente, você pode continuar toodeploy novos servidores para essa rede virtual repetidamente com poucas, se houver, alterações necessárias sobre a vida útil de saudação do hello VNet.

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Primeiro, crie um tooorganize do grupo de recursos tudo que você cria neste passo a passo. Para saber mais sobre os grupos de recursos do Azure, confira [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Criar hello VNet

Em seguida, crie VMs em uma saudação toolaunch de rede virtual. Olá VNet contém uma sub-rede e está associada ao grupo de segurança de rede Olá essa sub-rede em uma etapa posterior.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Adicionar uma sub-rede de toohello VNic

Placas de rede virtual (VNics) são importantes para você pode conectá-los toodifferent VMs. Essa abordagem mantém Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário. Crie uma VNic e associá-lo a sub-rede Olá criado na etapa anterior hello.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Criar grupo de segurança de rede Olá

Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello. Para obter mais informações sobre grupos de segurança de rede do Azure, confira [O que é um grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Adicionar uma regra de permissão de SSH de entrada

Olá VM precisa ter acesso de saudação à internet, para uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM é criada.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Associar Olá NSG sub-rede Olá

Com o hello rede virtual e sub-rede Olá criada, associe o grupo de segurança de rede Olá sub-rede hello. Os grupos de segurança de rede podem ser associados a uma sub-rede inteira ou a uma VNic individual. Com o firewall Olá filtrando o tráfego no nível de sub-rede Olá, todos os VNics e Olá VMs na sub-rede Olá são protegidos pelo grupo de segurança de rede hello. Olá outra abordagem é Olá sendo de grupo de segurança de rede associado a apenas uma único VNic e proteger apenas uma máquina virtual.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implantar hello VM em Olá VNet e NSG

Usando Olá portal do Azure, Olá VM do Linux é implantado toohello grupo de recursos do Azure, redes, sub-rede e VNic existentes.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Usando recursos existentes do hello toochoose portal, você instruir Olá toodeploy Azure VM dentro da rede existente hello. Depois que uma VNET e uma sub-rede forem implantadas, elas poderão ser mantidas como recursos estáticos ou permanentes na região do Azure.  

## <a name="next-steps"></a>Próximas etapas

* [Usar um modelo de Gerenciador de recursos do Azure toocreate uma implantação específica](../windows/cli-deploy-templates.md)
* [Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente](create-cli-complete.md)
* [Criar uma VM do Linux no Azure usando modelos](create-ssh-secured-vm-from-template.md)
