---
title: "aaaPlan de rede para replicação de tooAzure do VMware com o Site Recovery | Microsoft Docs"
description: "Este artigo aborda o planejamento de rede necessário ao replicar VMs do Azure com o Azure Site Recovery"
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Etapa 3: planejar a rede para a replicação de VM do Azure

Após ter verificado Olá [os pré-requisitos de implantação](azure-to-azure-walkthrough-prerequisites.md), ler Olá de toounderstand este artigo considerações sobre a replicação e a recuperação de máquinas virtuais (VMs) do Azure de uma região do Azure tooanother, acesso à rede usando Olá Serviço de recuperação de Site do Azure. 

- Quando você terminar de artigo hello, você deve ter uma clara compreensão de como tooset a saída de acesso para máquinas virtuais do Azure você deseja tooreplicate e como tooconnect do local do site toothose VMs.
- Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> Atualmente, a replicação de VM do Azure com o Site Recovery está em versão prévia.



## <a name="network-overview"></a>Visão geral da rede

Normalmente suas VMs do Azure estão localizados em uma Azure virtual/sub-rede da rede, e há uma conexão de seu tooAzure de site local usando o rota expressa do Azure, ou uma conexão VPN.

As redes geralmente são protegidas usando firewalls e/ou NSGs (grupos de segurança de rede). Firewalls podem usar baseadas na URL na lista com base em IP, toocontrol conectividade de rede. Os NSGs usam regras baseadas em intervalos de IP. 


Para recuperação de Site toowork de espera, você precisa toomake algumas alterações na conectividade de rede de saída, de máquinas virtuais que você deseja tooreplicate. Recuperação de site não oferece suporte a usar uma autenticação proxy toocontrol de conectividade de rede. Se você tem um proxy de autenticação, a replicação não pode ser habilitada. 


Olá diagrama a seguir mostra um ambiente típico para um aplicativo em execução em VMs do Azure.

![ambiente do cliente](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Ambiente de VM do Azure**

Você também pode ter uma conexão tooAzure configurar de seu site local, usando o rota expressa do Azure ou uma conexão VPN. 

![ambiente do cliente](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**TooAzure de conexão local**



## <a name="outbound-connectivity-for-urls"></a>Conectividade de saída para URLs

Se você estiver usando a conectividade de saída toocontrol um firewall baseado em URL do proxy, verifique se você permitir que as URLs usadas pela recuperação de Site

**URL** | **Detalhes**  
--- | ---
*.blob.core.windows.net | Permite que dados toobe gravado do hello VM, a conta de armazenamento de cache toohello na região de origem de saudação.
login.microsoftonline.com | Fornece tooSite de autenticação e autorização de URLs do serviço de recuperação.
*.hypervrecoverymanager.windowsazure.com | Permite a comunicação com hello serviço de recuperação de Site do hello VM.
*.servicebus.windows.net | Necessário para que os dados de monitoramento e diagnóstico de recuperação de Site Olá podem ser gravados de saudação VM.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Conectividade de saída para intervalos de endereços IP

- Você pode criar automaticamente regras de Olá necessárias no hello NSG baixando e executando [esse script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- É recomendável que você crie regras do NSG Olá necessários em um teste de NSG e verifique se não há nenhum problema, antes de criar regras de saudação em um NSG de produção.
- número de saudação necessário toocreate de regras do NSG, certifique-se de que sua assinatura está na lista de permissões. Contate o suporte tooincrease Olá NSG regra limite na sua assinatura.
Se você estiver usando qualquer proxy firewall baseado em IP ou conectividade de saída regras toocontrol NSG, hello seguintes intervalos de IP precisam toobe na lista de permissões, dependendo de locais de origem e destino de saudação de máquinas virtuais de saudação:

    - Todos os intervalos de endereços IP que correspondam toohello local de origem. Saudação de download [intervalos](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Lista branca é necessária, para que os dados podem ser gravados toohello conta de armazenamento de cache de saudação VM.
    - Todos os intervalos IP que correspondam tooOffice 365 [identidade e autenticação de pontos de extremidade do IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Se novos IPs são adicionados tooOffice 365 intervalos IP, será necessário toocreate novas regras do NSG.
-     Endereços IP de ponto de extremidade do Site Recovery ([disponíveis em um arquivo XML](https://aka.ms/site-recovery-public-ips)), que depende de seu local de destino: 

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

## <a name="example-nsg-configuration"></a>Exemplo de Configuração do NSG

Esta seção mostra como as regras de tooconfigure NSG, para que as replicações funciona para uma máquina virtual. Se você estiver usando a conectividade de saída regras toocontrol NSG, use regras de "Permitir HTTPS saída" para todos os intervalos IP hello necessário.

Neste exemplo, Olá local de origem da VM é "Leste dos Estados Unidos". local de destino de replicação de saudação é centro dos EUA.


### <a name="example"></a>Exemplo

#### <a name="east-us"></a>Leste dos EUA

1. Criar regras que correspondem muito[intervalos de IP do Leste dos EUA](https://www.microsoft.com/download/confirmation.aspx?id=41653). Isso é necessário para que os dados podem ser gravados toohello conta de armazenamento de cache de saudação VM.
2. Criar regras para todos os intervalos IP que correspondam tooOffice 365 [identidade e autenticação de pontos de extremidade do IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Crie regras que correspondem a toohello local de destino:

   **Localidade** | **Serviço de Recuperação do Site IPs** |  **Monitoramento de Recuperação de site IP**
    --- | --- | ---
   Centro dos EUA | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>Centro dos EUA

Essas regras são necessárias para que a replicação pode ser habilitada na região de origem do toohello de região de destino hello, após o failover.

1. Criar regras que correspondem muito[intervalos de IP de Central dos EUA](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Criar regras para todos os intervalos IP que correspondam tooOffice 365 [identidade e autenticação de pontos de extremidade do IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Crie regras que correspondem a toohello local de origem:

   **Localidade** | **Serviço de Recuperação do Site IPs** |  **Monitoramento de Recuperação de site IP**
    --- | --- | ---
   Leste dos EUA | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Conexão local existente

Se você tiver uma conexão de rota expressa ou VPN entre o site local e o local de origem Olá no Azure, siga estas diretrizes:

**Configuração** | **Detalhes**
--- | ---
**Túnel forçado** | Normalmente, uma rota padrão (0.0.0.0/0) força saída tooflow de tráfego de internet por meio de saudação no local. Não recomendamos isso. O tráfego de replicação e as comunicações do Site Recovery devem permanecer no Azure.<br/><br/> Como uma solução, adicione rotas definidas pelo usuário (UDRs) para [desses intervalos IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges), de modo que o tráfego de saudação não for local.
**Conectividade** | Se tooconnect máquinas de tooon local precisam de aplicativos ou clientes locais conectam o aplicativo de toohello sobre locais pela VPN/rota expressa, verifique se você tem pelo menos um [conexão site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), entre o destino de saudação região do Azure e Olá no site local.<br/><br/> Se os volumes de tráfego são altos entre Olá no site local e o destino de saudação região do Azure, crie outro [conexão de rota expressa](../expressroute/expressroute-introduction.md), entre locais e de região de destino hello.<br/><br/> Se você quiser tooretain IPs para máquinas virtuais após o failover, manter a conexão de site para site/ExpressRoute da região de destino Olá em um estado desconectado. Isso garante que não há nenhum conflitos de intervalo entre intervalos de endereços IP de origem e destino de saudação.
**ExpressRoute** | Crie um circuito de rota expressa em Olá regiões de origem e destino.<br/><br/> Crie uma conexão entre a rede de origem de hello e o circuito de rota expressa hello e entre a rede de destino de saudação e circuito hello.<br/><br/> É recomendável que você use intervalos IP diferentes em regiões de origem e destino. Olá circuito não será capaz de tooconnect toomore de um Azure redes com hello mesmo intervalos IP, a saudação simultaneamente.<br/><br/> Você pode criar redes virtuais com hello mesmo IP intervalos em ambas as regiões e crie circuitos de rota expressa em ambas as regiões. Para failover, circuito Olá desconectar da rede virtual de origem hello e conecte-se o circuito Olá na rede virtual de destino de saudação.<br/><br/> Se a região primária hello está completamente inoperante, Olá desconectar a operação pode falhar. Nesse caso, rede virtual de destino Olá não terá conectividade de rota expressa.
**ExpressRoute Premium** | Você pode criar circuitos Olá mesma região geopolíticas.<br/><br/> toocreate circuitos em diferentes regiões geopolíticas, você precisa Premium de rota expressa do Azure.<br/><br/> Com o Premium, o custo de saudação é incremental. Se você já o está usando, não há nenhum custo adicional.<br/><br/> Saiba mais sobre [locais](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) e [preço](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 4: criar um cofre](azure-to-azure-walkthrough-vault.md)

