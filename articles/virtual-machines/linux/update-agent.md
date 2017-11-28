---
title: Atualizar o Agente Linux do Azure por meio do GitHub | Microsoft Docs
description: "Saiba como atualizar o Agente Linux do Azure de sua VM Linux no Azure para a versão mais recente do GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="2355e-103">Como atualizar o Agente Linux do Azure em uma VM</span><span class="sxs-lookup"><span data-stu-id="2355e-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="2355e-104">Para atualizar seu [agente Linux do Azure](https://github.com/Azure/WALinuxAgent) em uma VM do Linux no Azure, você já deve ter:</span><span class="sxs-lookup"><span data-stu-id="2355e-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="2355e-105">uma VM do Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="2355e-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="2355e-106">uma conexão com essa VM do Linux usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="2355e-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="2355e-107">Primeiro, você sempre deve verificar um pacote no repositório de distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="2355e-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="2355e-108">É possível que o pacote disponível não seja a versão mais recente, no entanto, habilitar a atualização automática garantirá que o Agente do Linux sempre obterá a atualização mais recente.</span><span class="sxs-lookup"><span data-stu-id="2355e-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="2355e-109">Se você tiver problemas de instalação a partir dos gerenciadores de pacotes, procure o suporte do fornecedor de distribuição.</span><span class="sxs-lookup"><span data-stu-id="2355e-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="2355e-110">Atualizar o Agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="2355e-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="2355e-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2355e-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-112">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="2355e-113">Cache do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="2355e-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-114">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-115">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="2355e-116">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-117">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-118">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-119">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="2355e-120">Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="2355e-121">Reinicie o agente para 14.04</span><span class="sxs-lookup"><span data-stu-id="2355e-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="2355e-122">Reinicie o agente para 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="2355e-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="2355e-123">Debian</span><span class="sxs-lookup"><span data-stu-id="2355e-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="2355e-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="2355e-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-125">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="2355e-126">Cache do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="2355e-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-127">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="2355e-128">Habilitar atualização automática do agente</span><span class="sxs-lookup"><span data-stu-id="2355e-128">Enable agent auto update</span></span>
<span data-ttu-id="2355e-129">Esta versão do Debian não tem uma versão maior ou igual à 2.0.16, portanto, a Atualização automática não está disponível para ele.</span><span class="sxs-lookup"><span data-stu-id="2355e-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="2355e-130">A saída do comando acima mostrará se o pacote está atualizado.</span><span class="sxs-lookup"><span data-stu-id="2355e-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="2355e-131">Debian 8 "Jessie"/Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="2355e-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-132">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="2355e-133">Cache do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="2355e-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-134">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-135">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="2355e-136">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-137">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-138">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-139">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="2355e-140">Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="2355e-141">Redhat/CentOS</span><span class="sxs-lookup"><span data-stu-id="2355e-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="2355e-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="2355e-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-143">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="2355e-144">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="2355e-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-145">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-146">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="2355e-147">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-148">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-149">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-150">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="2355e-151">Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="2355e-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="2355e-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-153">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="2355e-154">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="2355e-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-155">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-156">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="2355e-157">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-158">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-159">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-160">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="2355e-161">Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="2355e-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="2355e-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="2355e-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="2355e-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-164">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="2355e-165">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="2355e-165">Check available updates</span></span>

<span data-ttu-id="2355e-166">A saída acima mostrará se o pacote está atualizado.</span><span class="sxs-lookup"><span data-stu-id="2355e-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-167">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-168">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="2355e-169">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-170">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-171">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-172">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="2355e-173">Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="2355e-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="2355e-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="2355e-175">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="2355e-176">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="2355e-176">Check available updates</span></span>

<span data-ttu-id="2355e-177">A saída acima mostrará se o pacote está atualizado.</span><span class="sxs-lookup"><span data-stu-id="2355e-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="2355e-178">Instalar a versão mais recente do pacote</span><span class="sxs-lookup"><span data-stu-id="2355e-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-179">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="2355e-180">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-181">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-182">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-183">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="2355e-184">Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="2355e-185">Oracle 6 e 7</span><span class="sxs-lookup"><span data-stu-id="2355e-185">Oracle 6 and 7</span></span>

<span data-ttu-id="2355e-186">Para Oracle Linux, verifique se o repositório `Addons` está habilitado.</span><span class="sxs-lookup"><span data-stu-id="2355e-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="2355e-187">Escolha editar o arquivo `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha `enabled=0` para `enabled=1` em **[ol6_addons]** ou **[ol7_addons]** nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="2355e-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="2355e-188">Em seguida, para instalar a versão mais recente do agente Linux do Azure e digite:</span><span class="sxs-lookup"><span data-stu-id="2355e-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="2355e-189">Caso você não encontre o repositório de complementos, basta adicionar essas linhas no final do arquivo .repo de acordo com sua versão do Oracle Linux:</span><span class="sxs-lookup"><span data-stu-id="2355e-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="2355e-190">Para máquinas virtuais do Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="2355e-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="2355e-191">Para máquinas virtuais do Oracle Linux 7:</span><span class="sxs-lookup"><span data-stu-id="2355e-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="2355e-192">Em seguida, digite:</span><span class="sxs-lookup"><span data-stu-id="2355e-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="2355e-193">Normalmente, isso é tudo de que você precisa. Porém, se por algum motivo for necessário instalá-lo no https://github.com diretamente, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2355e-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="2355e-194">Atualizar o Agente do Linux quando não existir qualquer pacote de agente para distribuição</span><span class="sxs-lookup"><span data-stu-id="2355e-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="2355e-195">Instale o wget (existem algumas distribuições que não o instalam por padrão, como Redhat, CentOS e Oracle Linux versões 6.4 e 6.5) digitando `sudo yum install wget` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="2355e-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="2355e-196">1. Baixar a última versão</span><span class="sxs-lookup"><span data-stu-id="2355e-196">1. Download the latest version</span></span>
<span data-ttu-id="2355e-197">Abra [a versão do Agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent/releases) em uma página da Web e encontre o número de versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="2355e-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="2355e-198">(Você pode localizar sua versão atual digitando `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="2355e-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="2355e-199">Para a versão 2.2. x ou posterior, digite:</span><span class="sxs-lookup"><span data-stu-id="2355e-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="2355e-200">A linha a seguir usa a versão 2.2.0 como exemplo:</span><span class="sxs-lookup"><span data-stu-id="2355e-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="2355e-201">2. Instale o Agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="2355e-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="2355e-202">Para a versão 2.2. x, use:</span><span class="sxs-lookup"><span data-stu-id="2355e-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="2355e-203">Talvez seja necessário instalar o pacote `setuptools` primeiro, veja [aqui](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="2355e-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="2355e-204">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="2355e-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="2355e-205">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="2355e-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="2355e-206">Primeiro, verifique se está habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="2355e-207">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="2355e-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="2355e-208">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="2355e-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="2355e-209">Para habilitar a execução:</span><span class="sxs-lookup"><span data-stu-id="2355e-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="2355e-210">3. Reinicie o serviço do waagent</span><span class="sxs-lookup"><span data-stu-id="2355e-210">3. Restart the waagent service</span></span>
<span data-ttu-id="2355e-211">Para a maioria das distribuições do Linux:</span><span class="sxs-lookup"><span data-stu-id="2355e-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="2355e-212">Para o Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="2355e-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="2355e-213">Para o CoreOS, use:</span><span class="sxs-lookup"><span data-stu-id="2355e-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="2355e-214">4. Confirme a versão do Agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="2355e-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="2355e-215">Para o CoreOS, o comando acima pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="2355e-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="2355e-216">Você verá que a versão do Agente Linux do Azure foi atualizada para a nova versão.</span><span class="sxs-lookup"><span data-stu-id="2355e-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="2355e-217">Para obter mais informações sobre o Agente Linux do Azure, consulte [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent)(LEIAME do Agente Linux do Azure).</span><span class="sxs-lookup"><span data-stu-id="2355e-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>