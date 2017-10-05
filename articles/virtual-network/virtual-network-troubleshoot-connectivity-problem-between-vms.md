---
title: Solucionar problemas de conectividade entre VMs do Azure | Microsoft Docs
description: Saiba como solucionar os problemas de conectividade entre VMs do Azure.
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Solucionar problemas de conectividade entre VMs do Azure

Você pode enfrentar problemas de conectividade entre máquinas virtuais do Azure. Este artigo apresenta etapas para a solução de problemas para ajudá-lo a resolver esse problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Sintoma

Uma VM do Azure não pode se conectar a outra VM do Azure.

## <a name="troubleshooting-guidance"></a>Diretriz de solução de problemas 

1. [Verifique se o NIC está configurada incorretamente](#step-1-check-if-nic-is-misconfigured)
2. [Verifique se o tráfego de rede está bloqueado por NSG ou UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Verifique se o tráfego de rede é bloqueado pelo firewall da VM](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Verifique se o aplicativo ou serviço de VM está escutando na porta](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Verifique se o problema é causado por SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Verifique se o tráfego está bloqueado por ACLs para a VM clássica](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Verifique se o ponto de extremidade é criado para a VM clássica](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Não é possível conectar a um compartilhamento de rede VM](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Conectividade de rede entre virtuais](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas

Execute estas etapas para solucionar o problema. Verifique se o problema for resolvido após cada etapa. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Etapa 1: Verificar se o NIC está configurada incorretamente

Execute [como redefinir a interface de rede de VM do Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Se o problema ocorrer após você modificar o NIC (adaptador de rede), execute estas etapas:

**VMs de NIC redimensionável**

1. Adicionar um NIC.
2. Corrija os problemas no NIC incorreta ou remover NIC inválida.  Em seguida, readd NIC.

Para saber mais, confira [Adicionar ou remover adaptadores de rede de máquinas virtuais](virtual-network-network-interface-vm.md).

**VM com NIC único** 

- [Reimplantar VM do Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Reimplantar VM Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Etapa 2: Verifique se o tráfego de rede está bloqueado por NSG ou UDR

Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) para identificar se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Etapa 3: Verifique se o tráfego de rede é bloqueado pelo firewall da VM

Desabilite o firewall e teste o resultado. Se o problema for resolvido, valide as configurações no firewall e habilitar novamente.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a>Etapa 4: verificar se o aplicativo ou serviço de VM está escutando na porta

Você pode usar um dos métodos a seguir para verificar se a VM de aplicativo ou serviço está escutando na porta

- Execute os seguintes comandos para verificar se o servidor está escutando nessa porta.

**VM Windows**

    netstat –ano

**VM Linux**

    netstat -l

- Execute o **Telnet** comando na VM para si mesmo para testar a porta. Se o teste falhar, aplicativo ou serviço não está configurado para escutar na porta.

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a>Etapa 5: verificar se o problema é causado por SNAT

Em alguns cenários, a VM é colocada atrás de uma solução de balanceamento de carga que tem uma dependência em recursos fora do Azure. Nesses cenários, se você tiver problemas intermitentes de conexão, o problema pode ser causado por [esgotamento da porta SNAT](../load-balancer/load-balancer-outbound-connections.md). Para resolver o problema, crie um VIP (ou ILPIP para clássico) para cada VM que está por trás do balanceador de carga e proteger com ACL ou NSG. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a>Etapa 6: verificar se o tráfego está bloqueado por ACLs para a VM clássica

Uma ACL fornece a capacidade para permitir ou negar seletivamente o tráfego para um ponto de extremidade de máquina virtual. Para saber mais, confira [Gerenciar a ACL em um ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a>Etapa 7: verificar se o ponto de extremidade é criado para a VM clássica

Todas as máquinas virtuais que você criar no Azure usando o modelo de implantação clássico automaticamente podem se comunicar através de um canal de rede privada com outras máquinas virtuais no mesmo serviço de nuvem ou rede virtual. No entanto, os computadores em outras redes virtuais exigem pontos de extremidade para direcionar o tráfego de rede de entrada para uma máquina virtual. Para saber mais, confira [Como configurar pontos de extremidade](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a>Etapa 8: Não é possível conectar a um compartilhamento de rede VM

Se não for possível conectar a um compartilhamento de rede VM, o problema pode ser causado por NICs não está disponíveis na VM. Para excluir as NICs não disponíveis, consulte [Como excluir as NICs não disponíveis](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Etapa 9: Conectividade de rede entre virtuais

Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) para identificar se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego. Você também pode validar a configuração de rede entre [aqui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.