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
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="f0de6-104">Configuração de DHCPv6 para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="f0de6-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="f0de6-105">Algumas imagens de máquina virtual Linux Olá no hello Azure Marketplace não tem DHCPv6 configurado por padrão.</span><span class="sxs-lookup"><span data-stu-id="f0de6-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="f0de6-106">toosupport IPv6 e DHCPv6 deve ser configurado em dentro de distribuição do SO Linux Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="f0de6-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="f0de6-107">Distribuições diferentes do Linux têm maneiras diferentes de configurar o DHCPv6, pois usam pacotes diferentes.</span><span class="sxs-lookup"><span data-stu-id="f0de6-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="f0de6-108">Recente SUSE Linux e CoreOS imagens em hello Azure Marketplace tem sido pré-configurado com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f0de6-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f0de6-109">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="f0de6-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="f0de6-110">Este documento descreve como tooenable DHCPv6 para que sua máquina virtual do Linux obtém um endereço IPv6.</span><span class="sxs-lookup"><span data-stu-id="f0de6-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="f0de6-111">Incorretamente editando arquivos de configuração de rede pode fazer com que você toolose rede acesso tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="f0de6-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="f0de6-112">Recomendamos que você teste as alterações de configuração em sistemas de não produção.</span><span class="sxs-lookup"><span data-stu-id="f0de6-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="f0de6-113">instruções de saudação neste artigo foram testadas em versões mais recentes de saudação de imagens Linux Olá Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f0de6-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="f0de6-114">Consulte a documentação de saudação para a versão específica do Linux para obter instruções mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="f0de6-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="f0de6-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f0de6-115">Ubuntu</span></span>

1. <span data-ttu-id="f0de6-116">Editar arquivo hello `/etc/dhcp/dhclient6.conf` e adicione a seguinte linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="f0de6-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="f0de6-117">Edite configuração de rede de saudação para interface de eth0 Olá com hello a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="f0de6-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="f0de6-118">Em **12.04 Ubuntu e 14.04**, edite o arquivo hello`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="f0de6-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="f0de6-119">Em **16.04 Ubuntu**, edite o arquivo hello`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="f0de6-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="f0de6-120">Renove endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="f0de6-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="f0de6-121">Debian</span><span class="sxs-lookup"><span data-stu-id="f0de6-121">Debian</span></span>

1. <span data-ttu-id="f0de6-122">Editar arquivo hello `/etc/dhcp/dhclient6.conf` e adicione a seguinte linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="f0de6-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="f0de6-123">Editar arquivo hello `/etc/network/interfaces` e adicione Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="f0de6-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="f0de6-124">Renove endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="f0de6-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="f0de6-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="f0de6-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="f0de6-126">Editar arquivo hello `/etc/sysconfig/network` e adicione Olá parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0de6-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="f0de6-127">Editar arquivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione Olá dois parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0de6-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="f0de6-128">Renove endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="f0de6-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="f0de6-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="f0de6-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="f0de6-130">Imagens recentes de SLES e openSUSE no Azure foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f0de6-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f0de6-131">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="f0de6-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="f0de6-132">Se você tiver uma VM com base em uma imagem SUSE mais antiga ou personalizada, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0de6-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="f0de6-133">Instalar Olá `dhcp-client` do pacote, se necessário:</span><span class="sxs-lookup"><span data-stu-id="f0de6-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="f0de6-134">Editar arquivo hello `/etc/sysconfig/network/ifcfg-eth0` e adicione Olá parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0de6-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="f0de6-135">Renove endereço Olá IPv6:</span><span class="sxs-lookup"><span data-stu-id="f0de6-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="f0de6-136">SLES 12 e openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="f0de6-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="f0de6-137">Imagens recentes de SLES e openSUSE no Azure foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f0de6-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f0de6-138">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="f0de6-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="f0de6-139">Se você tiver uma VM com base em uma imagem SUSE mais antiga ou personalizada, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0de6-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="f0de6-140">Editar arquivo hello `/etc/sysconfig/network/ifcfg-eth0` e substitua esse parâmetro</span><span class="sxs-lookup"><span data-stu-id="f0de6-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="f0de6-141">com hello seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="f0de6-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="f0de6-142">Adicionar Olá seguindo o parâmetro muito`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="f0de6-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="f0de6-143">Renove endereço Olá IPv6:</span><span class="sxs-lookup"><span data-stu-id="f0de6-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="f0de6-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f0de6-144">CoreOS</span></span>

<span data-ttu-id="f0de6-145">Imagens recentes de CoreOS no Azure foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f0de6-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="f0de6-146">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="f0de6-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="f0de6-147">Se você tiver uma VM com base em uma imagem de CoreOS mais antiga ou personalizada, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0de6-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="f0de6-148">Editar arquivo hello.`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="f0de6-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="f0de6-149">Renove endereço Olá IPv6:</span><span class="sxs-lookup"><span data-stu-id="f0de6-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
