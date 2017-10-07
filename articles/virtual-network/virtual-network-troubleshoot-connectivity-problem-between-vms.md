---
title: "aaaTroubleshooting problemas de conectividade entre máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba como tooTroubleshoot Olá problemas de conectividade entre máquinas virtuais do Azure."
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
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Solucionar problemas de conectividade entre VMs do Azure

Você pode enfrentar problemas de conectividade entre máquinas virtuais do Azure. Este artigo fornece toohelp de etapas de solução de problemas é resolver esse problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Sintoma

Uma VM do Azure não pode se conectar a tooanother VM do Azure.

## <a name="troubleshooting-guidance"></a>Diretriz de solução de problemas 

1. [Verifique se o NIC está configurada incorretamente](#step-1-check-if-nic-is-misconfigured)
2. [Verifique se o tráfego de rede está bloqueado por NSG ou UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Verifique se o tráfego de rede é bloqueado pelo firewall da VM](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Verifique se o aplicativo de máquina virtual ou serviço está escutando na porta de Olá](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Verifique se o problema de saudação é causado por SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Verifique se o tráfego é bloqueado por ACLs para Olá VM clássico](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Verifique se o ponto de extremidade de saudação é criado para Olá VM clássico](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Compartilhamento de rede VM não é possível tooconnect tooa](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Conectividade de rede entre virtuais](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas

Siga o problema de saudação de tootroubleshoot essas etapas. Verifique se o problema de saudação for resolvido após cada etapa. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Etapa 1: Verificar se o NIC está configurada incorretamente

Execute [como tooreset interface de rede de VM do Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Se o problema de saudação ocorre depois de modificar a interface de rede (NIC) do hello, siga estas etapas:

**VMs de NIC redimensionável**

1. Adicionar um NIC.
2. Corrigir problemas de saudação em Olá incorreta NIC ou remover NIC inválida.  Em seguida, readd NIC hello.

Para obter mais informações, consulte [remover adicionar tooor de interfaces de rede de máquinas virtuais](virtual-network-network-interface-vm.md).

**VM com NIC único** 

- [Reimplantar VM do Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Reimplantar VM Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Etapa 2: Verifique se o tráfego de rede está bloqueado por NSG ou UDR

Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Etapa 3: Verifique se o tráfego de rede é bloqueado pelo firewall da VM

Desabilitar Olá firewall e teste o resultado de saudação. Se Olá problema for resolvido, validar as configurações de saudação no firewall hello e habilite novamente.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Etapa 4: Verifique se o aplicativo de máquina virtual ou serviço está escutando na porta de Olá

Você pode usar uma saudação toocheck métodos a seguir se VM aplicativo ou serviço está escutando na porta Olá

- Execute Olá toocheck comandos a seguir se Olá servidor está escutando nessa porta.

**VM Windows**

    netstat –ano

**VM Linux**

    netstat -l

- Executar Olá **Telnet** comando Olá porta de saudação do VM tooitself tootest. Se Olá teste falhar, aplicativo ou serviço não é toolisten configurado na porta hello.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Etapa 5: Verificar se o problema de saudação é causado por SNAT

Em alguns cenários, hello VM é colocada atrás de uma solução de balanceamento de carga que tem uma dependência em recursos fora do Azure. Nesses cenários, se você tiver problemas de conexão intermitente, Olá problema pode ser causado por [esgotamento de porta SNAT](../load-balancer/load-balancer-outbound-connections.md). problema de saudação tooresolve, crie um VIP (ou ILPIP para clássico) para cada VM que está por trás do balanceador de carga Olá e proteger com ACL ou NSG. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Etapa 6: Verifique se o tráfego é bloqueado por ACLs para Olá VM clássico

Uma ACL fornece Olá capacidade tooselectively permitir ou negar o tráfego para um ponto de extremidade de máquina virtual. Para obter mais informações, consulte [gerenciar Olá ACL em um ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Etapa 7: Verifique se o ponto de extremidade de saudação é criado para Olá VM clássico

Todas as máquinas virtuais que você criar no Azure usando o modelo de implantação clássico Olá podem se comunicar automaticamente por um canal de rede privada com outras máquinas virtuais no hello que mesmo serviço ou de rede virtual na nuvem. No entanto, os computadores em outras redes virtuais requerem pontos de extremidade toodirect Olá rede de entrada tráfego tooa máquina virtual. Para obter mais informações, consulte [como tooset pontos de extremidade](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Etapa 8: O compartilhamento de rede VM não é possível tooconnect tooa

Se você for um compartilhamento de rede VM não é possível tooconnect tooa, problema de saudação pode ser causado por NICs indisponíveis em Olá VM. toodelete Olá NICs disponíveis, consulte [como toodelete Olá NICs indisponíveis](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Etapa 9: Conectividade de rede entre virtuais

Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego. Você também pode validar a configuração de rede entre [aqui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
