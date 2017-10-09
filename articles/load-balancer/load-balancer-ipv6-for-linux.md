---
title: aaaConfiguring DHCPv6 para VMs do Linux | Microsoft Docs
description: Como tooconfigure DHCPv6 para VMs do Linux.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a>Configuração de DHCPv6 para VMs Linux

Algumas imagens de máquina virtual Linux Olá no hello Azure Marketplace não tem DHCPv6 configurado por padrão. toosupport IPv6 e DHCPv6 deve ser configurado em dentro de distribuição do SO Linux Olá que você está usando. Distribuições diferentes do Linux têm maneiras diferentes de configurar o DHCPv6, pois usam pacotes diferentes.

> [!NOTE]
> Recente SUSE Linux e CoreOS imagens em hello Azure Marketplace tem sido pré-configurado com DHCPv6. Nenhuma alteração adicional é necessária ao usar essas imagens.

Este documento descreve como tooenable DHCPv6 para que sua máquina virtual do Linux obtém um endereço IPv6.

> [!WARNING]
> Incorretamente editando arquivos de configuração de rede pode fazer com que você toolose rede acesso tooyour VM. Recomendamos que você teste as alterações de configuração em sistemas de não produção. instruções de saudação neste artigo foram testadas em versões mais recentes de saudação de imagens Linux Olá Olá Azure Marketplace. Consulte a documentação de saudação para a versão específica do Linux para obter instruções mais detalhadas.

## <a name="ubuntu"></a>Ubuntu

1. Editar arquivo hello `/etc/dhcp/dhclient6.conf` e adicione a seguinte linha de saudação:

        timeout 10;

2. Edite configuração de rede de saudação para interface de eth0 Olá com hello a seguinte configuração:

   * Em **12.04 Ubuntu e 14.04**, edite o arquivo hello`/etc/network/interfaces.d/eth0.cfg`
   * Em **16.04 Ubuntu**, edite o arquivo hello`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renove endereço IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Editar arquivo hello `/etc/dhcp/dhclient6.conf` e adicione a seguinte linha de saudação:

        timeout 10;

2. Editar arquivo hello `/etc/network/interfaces` e adicione Olá a seguinte configuração:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renove endereço IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Editar arquivo hello `/etc/sysconfig/network` e adicione Olá parâmetro a seguir:

        NETWORKING_IPV6=yes

2. Editar arquivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá dois parâmetros a seguir:

        IPV6INIT=yes
        DHCPV6C=yes

3. Renove endereço IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 & openSUSE 13

Imagens recentes de SLES e openSUSE no Azure foram pré-configuradas com DHCPv6. Nenhuma alteração adicional é necessária ao usar essas imagens. Se você tiver uma VM com base em uma imagem SUSE mais antiga ou personalizada, use Olá etapas a seguir:

1. Instalar Olá `dhcp-client` do pacote, se necessário:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Editar arquivo hello `/etc/sysconfig/network/ifcfg-eth0` e adicione Olá parâmetro a seguir:

        DHCLIENT6_MODE='managed'

3. Renove endereço Olá IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 e openSUSE Leap

Imagens recentes de SLES e openSUSE no Azure foram pré-configuradas com DHCPv6. Nenhuma alteração adicional é necessária ao usar essas imagens. Se você tiver uma VM com base em uma imagem SUSE mais antiga ou personalizada, use Olá etapas a seguir:

1. Editar arquivo hello `/etc/sysconfig/network/ifcfg-eth0` e substitua esse parâmetro

        #BOOTPROTO='dhcp4'

    com hello seguinte valor:

        BOOTPROTO='dhcp'

2. Adicionar Olá seguindo o parâmetro muito`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Renove endereço Olá IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Imagens recentes de CoreOS no Azure foram pré-configuradas com DHCPv6. Nenhuma alteração adicional é necessária ao usar essas imagens. Se você tiver uma VM com base em uma imagem de CoreOS mais antiga ou personalizada, use Olá etapas a seguir:

1. Editar arquivo hello.`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Renove endereço Olá IPv6:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
