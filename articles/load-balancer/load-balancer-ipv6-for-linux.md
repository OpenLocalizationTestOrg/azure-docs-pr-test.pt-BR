---
title: "Configuração de DHCPv6 para VMs Linux | Microsoft Docs"
description: Como configurar DHCPv6 para VMs Linux.
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="c0a4e-104">Configuração de DHCPv6 para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="c0a4e-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="c0a4e-105">Algumas das imagens de máquina virtual do Linux no Azure Marketplace não tem o DHCPv6 configurado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="c0a4e-106">Para oferecer suporte a IPv6, o DHCPv6 deve ser configurado dentro da distribuição do SO Linux que você está usando.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="c0a4e-107">Distribuições diferentes do Linux têm maneiras diferentes de configurar o DHCPv6, pois usam pacotes diferentes.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="c0a4e-108">Imagens recentes do SUSE Linux e CoreOS no Azure Marketplace foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="c0a4e-109">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="c0a4e-110">Este documento descreve como habilitar o DHCPv6 para que a sua máquina virtual Linux obtenha um endereço IPv6.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="c0a4e-111">A edição inadequada de arquivos de configuração de rede podem causar a perda de acesso à rede para sua VM.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="c0a4e-112">Recomendamos que você teste as alterações de configuração em sistemas de não produção.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="c0a4e-113">As instruções neste artigo foram testadas em versões mais recentes das imagens do Linux no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="c0a4e-114">Consulte a documentação para a versão específica do Linux para obter instruções mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="c0a4e-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c0a4e-115">Ubuntu</span></span>

1. <span data-ttu-id="c0a4e-116">Edite o arquivo `/etc/dhcp/dhclient6.conf` e adicione a linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="c0a4e-117">Edite a configuração de rede para a interface eth0 com a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="c0a4e-118">No **Ubuntu 12.04 e 14.04**, edite o arquivo `/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="c0a4e-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="c0a4e-119">No **Ubuntu 16.04**, edite o arquivo `/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="c0a4e-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="c0a4e-120">Renove endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="c0a4e-121">Debian</span><span class="sxs-lookup"><span data-stu-id="c0a4e-121">Debian</span></span>

1. <span data-ttu-id="c0a4e-122">Edite o arquivo `/etc/dhcp/dhclient6.conf` e adicione a linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="c0a4e-123">Edite o arquivo `/etc/network/interfaces` e adicione a configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="c0a4e-124">Renove endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="c0a4e-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="c0a4e-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="c0a4e-126">Edite o arquivo `/etc/sysconfig/network` e adicione o parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="c0a4e-127">Edite o arquivo `/etc/sysconfig/network-scripts/ifcfg-eth0` e adicione os dois parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="c0a4e-128">Renove endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="c0a4e-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="c0a4e-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="c0a4e-130">Imagens recentes de SLES e openSUSE no Azure foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="c0a4e-131">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="c0a4e-132">Se você tiver uma VM baseada em uma imagem SUSE mais antiga ou personalizada, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="c0a4e-133">Instale o pacote `dhcp-client` , se for necessário:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="c0a4e-134">Edite o arquivo `/etc/sysconfig/network/ifcfg-eth0` e adicione o parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="c0a4e-135">Renove o endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="c0a4e-136">SLES 12 e openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="c0a4e-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="c0a4e-137">Imagens recentes de SLES e openSUSE no Azure foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="c0a4e-138">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="c0a4e-139">Se você tiver uma VM baseada em uma imagem SUSE mais antiga ou personalizada, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="c0a4e-140">Edite o arquivo `/etc/sysconfig/network/ifcfg-eth0` e substitua este parâmetro</span><span class="sxs-lookup"><span data-stu-id="c0a4e-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="c0a4e-141">pelo seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="c0a4e-142">Adicione o seguinte parâmetro a `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="c0a4e-143">Renove o endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="c0a4e-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c0a4e-144">CoreOS</span></span>

<span data-ttu-id="c0a4e-145">Imagens recentes de CoreOS no Azure foram pré-configuradas com DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="c0a4e-146">Nenhuma alteração adicional é necessária ao usar essas imagens.</span><span class="sxs-lookup"><span data-stu-id="c0a4e-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="c0a4e-147">Se você tiver uma VM baseada em uma imagem CoreOS mais antiga ou personalizada, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="c0a4e-148">Edite o arquivo `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="c0a4e-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="c0a4e-149">Renove o endereço IPv6:</span><span class="sxs-lookup"><span data-stu-id="c0a4e-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
