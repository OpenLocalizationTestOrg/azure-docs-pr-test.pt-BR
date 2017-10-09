---
title: "aaaAzure diretrizes de rede de recuperação de Site para replicação de máquinas virtuais do Azure tooAzure | Microsoft Docs"
description: "Diretrizes de rede para replicar máquinas virtuais do Azure"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Diretrizes de rede para replicar máquinas virtuais do Azure

>[!NOTE]
> Atualmente, a replicação do Site Recovery para máquinas virtuais do Azure está em versão prévia.

Este artigo detalha Olá diretrizes de rede para o Azure Site Recovery, quando você está replicando e a recuperação de máquinas virtuais do Azure da região de tooanother de uma região. Para obter mais informações sobre os requisitos de recuperação de Site do Azure, consulte Olá [pré-requisitos](site-recovery-prereq.md) artigo.

## <a name="site-recovery-architecture"></a>Arquitetura do Site Recovery

Recuperação de site fornece uma maneira simples e fácil tooreplicate aplicativos em execução em máquinas virtuais do Azure tooanother região do Azure para que eles podem ser recuperados se houver uma interrupção na região primária hello. Saiba mais sobre [este cenário e arquitetura de recuperação de Site](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>Sua infraestrutura de rede

Olá diagrama a seguir ilustra típico ambiente Azure Olá para um aplicativo em execução em máquinas virtuais do Azure:

![ambiente do cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Se você estiver usando uma conexão VPN de um tooAzure de rede local ou de rota expressa do Azure, ambiente Olá terá esta aparência:

![ambiente do cliente](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

Normalmente, os clientes protegem suas redes usando firewalls e/ou grupos de segurança de rede (NSGs). firewalls Olá podem usar a lista branca baseado em URL ou IP para controlar a conectividade de rede. Os NSGs as regras de permissão para usar a conectividade de rede de toocontrol de intervalos IP.

>[!IMPORTANT]
> Se você estiver usando uma conectividade de rede toocontrol proxy autenticado, não há suporte e não é possível habilitar a replicação de recuperação de Site. 

Olá seções a seguir discutem Olá rede conectividade de saída alterações necessárias de máquinas virtuais do Azure para recuperação de Site toowork de replicação.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Conectividade de saída para URLs de recuperação de Site do Azure

Se você estiver usando a conectividade de saída toocontrol qualquer firewall baseado em URL do proxy, ser toowhitelist-se de que eles exigidos URLs de serviço do Azure Site Recovery:


**URL** | **Finalidade**  
--- | ---
*.blob.core.windows.net | Necessário para que os dados podem ser gravados toohello conta de armazenamento de cache na região de origem de saudação do hello VM.
login.microsoftonline.com | Necessário para autenticação e autorização de URLs de serviço de recuperação de Site toohello.
*.hypervrecoverymanager.windowsazure.com | Necessário para que a comunicação de serviço de recuperação de Site Olá pode ocorrer de saudação VM.
*.servicebus.windows.net | Necessário para que os dados de monitoramento e diagnóstico de recuperação de Site Olá podem ser gravados de saudação VM.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Conectividade de saída para os intervalos de IP de recuperação de Site do Azure

>[!NOTE]
> tooautomatically criar regras do NSG Olá necessários no grupo de segurança de rede hello, você pode [baixar e usar esse script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * É recomendável que você cria as regras NSG Olá necessários em um grupo de segurança de rede de teste e verifique se não há nenhum problema antes de criar regras de saudação em um grupo de segurança de rede de produção.
> * número de saudação necessário toocreate de regras do NSG, certifique-se de que sua assinatura está na lista de permissões. Contate o suporte tooincrease Olá NSG regra limite na sua assinatura.

Se você estiver usando qualquer proxy firewall baseado em IP ou conectividade de saída regras toocontrol NSG, hello seguintes intervalos de IP precisam toobe na lista de permissões, dependendo de locais de origem e destino de saudação de máquinas virtuais de saudação:

- Todos os intervalos IP que correspondam toohello local de origem. (Você pode baixar Olá [intervalos IP](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Lista branca é necessária para que os dados podem ser gravados toohello conta de armazenamento de cache de saudação VM.

- Todos os intervalos IP que correspondam tooOffice 365 [identidade e autenticação de pontos de extremidade do IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Se novos IPs são adicionados tooOffice 365 intervalos IP no hello futura, será necessário toocreate novas regras do NSG.
    
- Ponto de extremidade de serviço de recuperação de Site IPs ([disponíveis em um arquivo XML](https://aka.ms/site-recovery-public-ips)), que depende de seu local de destino: 

   **Local de destino** | **Serviço de Recuperação do Site IPs** |  **Monitoramento de Recuperação de site IP**
   --- | --- | ---
   Ásia Oriental | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Sudeste Asiático | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   Índia Central | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Sul da Índia | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   Centro-Norte dos EUA | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Norte da Europa | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Europa Ocidental | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   Leste dos EUA | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   Oeste dos EUA | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   Centro-Sul dos Estados Unidos | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   Centro dos EUA | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   Leste dos EUA 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Leste do Japão | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Oeste do Japão | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Sul do Brasil | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Leste da Austrália | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Sudeste da Austrália | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Canadá Central | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Leste do Canadá | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   Centro-Oeste dos EUA | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   Oeste dos EUA 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Oeste do Reino Unido | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Sul do Reino Unido | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>Exemplo de Configuração do NSG
Esta seção explica as regras NSG do hello etapas tooconfigure para que o trabalho de replicação de recuperação de Site em uma máquina virtual. Se você estiver usando a conectividade de saída regras toocontrol NSG, use regras de "Permitir HTTPS saída" para todos os intervalos IP hello necessário.

>[!Note]
> tooautomatically criar regras do NSG Olá necessários no grupo de segurança de rede hello, você pode [baixar e usar esse script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Por exemplo, se o local de origem da VM é "US East" e o local de destino de replicação é "Centro dos EUA", siga as etapas de saudação nas próximas duas seções de saudação.

>[!IMPORTANT]
> * É recomendável que você cria as regras NSG Olá necessários em um grupo de segurança de rede de teste e verifique se não há nenhum problema antes de criar regras de saudação em um grupo de segurança de rede de produção.
> * número de saudação necessário toocreate de regras do NSG, certifique-se de que sua assinatura está na lista de permissões. Contate o suporte tooincrease Olá NSG regra limite na sua assinatura. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>Regras NSG no grupo de segurança de rede Olá Leste dos EUA

* Criar regras que correspondem muito[intervalos de IP do Leste dos EUA](https://www.microsoft.com/download/confirmation.aspx?id=41653). Isso é necessário para que os dados podem ser gravados toohello conta de armazenamento de cache de saudação VM.

* Criar regras para todos os intervalos IP que correspondam tooOffice 365 [identidade e autenticação de pontos de extremidade do IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Crie regras que correspondem a toohello local de destino:

   **Localidade** | **Serviço de Recuperação do Site IPs** |  **Monitoramento de Recuperação de site IP**
    --- | --- | ---
   Centro dos EUA | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Regras NSG no grupo de segurança de rede Olá centro dos EUA

Essas regras são necessárias para que a replicação pode ser habilitada no hello destino região toohello fonte região após o failover:

* As regras que correspondem muito[intervalos de IP de Central dos EUA](https://www.microsoft.com/download/confirmation.aspx?id=41653). Eles são necessários para que os dados podem ser gravados toohello conta de armazenamento de cache de saudação VM.

* Regras para todos os intervalos IP que correspondam tooOffice 365 [identidade e autenticação de pontos de extremidade do IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Local de origem de regras que correspondem a toohello:

   **Localidade** | **Serviço de Recuperação do Site IPs** |  **Monitoramento de Recuperação de site IP**
    --- | --- | ---
   Leste dos EUA | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Diretrizes para configuração da ExpressRoute/VPN do Azure-para-local existente

Se você tiver uma conexão de rota expressa ou VPN entre locais e hello origem local no Azure, siga as diretrizes de saudação nesta seção.

### <a name="forced-tunneling-configuration"></a>Configuração de túnel forçado

Uma configuração de cliente comum é toodefine uma rota padrão (0.0.0.0/0) que força a saída tooflow de tráfego de Internet por meio de saudação no local. Não recomendamos isso. tráfego de replicação Hello e comunicação de serviço de recuperação de Site não devem deixar Olá limites do Azure. Olá solução é tooadd rotas definidas pelo usuário (UDRs) para [desses intervalos IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges) para que o tráfego de replicação de saudação não for local.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Conectividade entre o local de destino e o local de saudação

Siga estas diretrizes para conexões entre o local de destino hello e Olá local:
- Se seu aplicativo precisa de máquinas do tooconnect toohello locais ou se houver clientes que se conectam a aplicativo de toohello do local, por VPN/rota expressa, certifique-se de que você tenha pelo menos um [conexão site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) entre o datacenter do Azure região e hello no local de destino.

- Se você esperar muito tráfego tooflow entre sua região do Azure de destino e o datacenter local de saudação, você deve criar outro [conexão de rota expressa](../expressroute/expressroute-introduction.md) entre o datacenter do hello Azure região e hello no local de destino.

- Se você quiser tooretain IPs para máquinas virtuais de saudação depois que o failover, manter a conexão de site para site/ExpressRoute da região de destino Olá em um estado desconectado. Isso é toomake-se de que não há nenhum conflito de intervalo entre os intervalos de IP da região de origem hello e intervalos IP da região de destino.

### <a name="best-practices-for-expressroute-configuration"></a>Práticas recomendadas para configuração de ExpressRoute
Siga estas práticas recomendadas para configuração de ExpressRoute:

- É necessário toocreate um circuito de rota expressa em ambas as regiões de origem e destino hello. Em seguida, você precisa de uma conexão entre toocreate:
  - rede virtual de origem Hello e o circuito de rota expressa hello.
  - rede virtual de destino Hello e o circuito de rota expressa hello.

- Como parte do padrão de rota expressa, você pode criar circuitos em Olá mesma região geopolíticas. circuitos do ExpressRoute toocreate em diferentes regiões geopolíticas, o Azure ExpressRoute Premium é necessário, que envolve um custo incremental. (Se você já estiver usando o ExpressRoute Premium, não há nenhum custo extra.) Para obter mais detalhes, consulte Olá [documento de locais de rota expressa](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) e [ExpressRoute preços](https://azure.microsoft.com/pricing/details/expressroute/).

- É recomendável que você use intervalos IP diferentes em regiões de origem e destino. Olá circuito de rota expressa não será capaz de intervalos de IP mesmo tooconnect com duas redes virtuais do Azure de saudação em Olá simultaneamente.

- Você pode criar redes virtuais com hello mesmo IP varia em ambas as regiões e, em seguida, criar circuitos de rota expressa em ambas as regiões. No caso de saudação de um evento de failover, circuito Olá desconectar da rede virtual de origem hello e conecte-se o circuito de saudação na rede virtual de destino de saudação.

 >[!IMPORTANT]
 > Se a região primária hello está completamente inoperante, Olá desconectar a operação pode falhar. Que impedirão rede virtual de destino Olá conectividade de rota expressa.

## <a name="next-steps"></a>Próximas etapas
Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).
