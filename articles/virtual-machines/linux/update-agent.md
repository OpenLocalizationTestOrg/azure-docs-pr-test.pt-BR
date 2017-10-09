---
title: "Olá aaaUpdate agente Linux do Azure do GitHub | Microsoft Docs"
description: "Saiba como tooupdate agente Linux do Azure para sua VM do Linux no Azure toohello a versão mais recente do GitHub"
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
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="b6544-103">Como tooupdate hello Azure Linux Agent em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b6544-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="b6544-104">tooupdate seu [agente Linux do Azure](https://github.com/Azure/WALinuxAgent) em uma VM do Linux no Azure, você já deve ter:</span><span class="sxs-lookup"><span data-stu-id="b6544-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="b6544-105">uma VM do Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="b6544-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="b6544-106">Uma conexão toothat VM Linux usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="b6544-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="b6544-107">Você sempre deve verificar um pacote no repositório de distribuição de Linux Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="b6544-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="b6544-108">É possível pacote de saudação disponível não pode ser versão mais recente do hello, no entanto, habilitar a atualização automática garantirá Olá agente Linux sempre obterá a atualização mais recente da saudação.</span><span class="sxs-lookup"><span data-stu-id="b6544-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="b6544-109">Se você tiver problemas ao instalar o gerenciadores de pacotes de saudação, busque o suporte do fornecedor de distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6544-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="b6544-110">Atualizando Olá agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="b6544-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="b6544-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b6544-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-112">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="b6544-113">Cache do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="b6544-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-114">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-115">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="b6544-116">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-117">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-118">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-119">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="b6544-120">Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="b6544-121">Reinicie o agente para 14.04</span><span class="sxs-lookup"><span data-stu-id="b6544-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="b6544-122">Reinicie o agente para 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="b6544-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="b6544-123">Debian</span><span class="sxs-lookup"><span data-stu-id="b6544-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="b6544-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="b6544-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-125">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="b6544-126">Cache do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="b6544-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-127">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="b6544-128">Habilitar atualização automática do agente</span><span class="sxs-lookup"><span data-stu-id="b6544-128">Enable agent auto update</span></span>
<span data-ttu-id="b6544-129">Esta versão do Debian não tem uma versão maior ou igual à 2.0.16, portanto, a Atualização automática não está disponível para ele.</span><span class="sxs-lookup"><span data-stu-id="b6544-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="b6544-130">saída de saudação do hello acima comando mostrará se o pacote de saudação está atualizado.</span><span class="sxs-lookup"><span data-stu-id="b6544-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="b6544-131">Debian 8 "Jessie"/Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="b6544-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-132">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="b6544-133">Cache do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="b6544-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-134">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-135">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="b6544-136">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-137">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-138">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-139">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="b6544-140">Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="b6544-141">Redhat/CentOS</span><span class="sxs-lookup"><span data-stu-id="b6544-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="b6544-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="b6544-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-143">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="b6544-144">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="b6544-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-145">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-146">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="b6544-147">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-148">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-149">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-150">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="b6544-151">Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="b6544-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="b6544-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-153">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="b6544-154">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="b6544-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-155">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-156">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="b6544-157">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-158">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-159">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-160">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="b6544-161">Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="b6544-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="b6544-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="b6544-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="b6544-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-164">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="b6544-165">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="b6544-165">Check available updates</span></span>

<span data-ttu-id="b6544-166">Olá acima saída mostrará se o pacote de saudação é o toodate.</span><span class="sxs-lookup"><span data-stu-id="b6544-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-167">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-168">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="b6544-169">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-170">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-171">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-172">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="b6544-173">Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="b6544-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="b6544-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="b6544-175">Verificar a versão atual do pacote</span><span class="sxs-lookup"><span data-stu-id="b6544-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="b6544-176">Verificar as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="b6544-176">Check available updates</span></span>

<span data-ttu-id="b6544-177">Na saída de saudação do hello acima, isso mostrará se o pacote de saudação está atualizada.</span><span class="sxs-lookup"><span data-stu-id="b6544-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="b6544-178">Instalar a versão mais recente do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-179">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="b6544-180">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-181">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-182">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-183">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="b6544-184">Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="b6544-185">Oracle 6 e 7</span><span class="sxs-lookup"><span data-stu-id="b6544-185">Oracle 6 and 7</span></span>

<span data-ttu-id="b6544-186">Para Oracle Linux, certifique-se de que Olá `Addons` repositório está habilitado.</span><span class="sxs-lookup"><span data-stu-id="b6544-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="b6544-187">Escolha o arquivo de saudação tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha hello `enabled=0` muito`enabled=1` em **[ol6_addons]** ou **[ol7_addons]** Nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="b6544-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="b6544-188">Em seguida, tooinstall Olá versão mais recente do hello agente Linux do Azure, tipo:</span><span class="sxs-lookup"><span data-stu-id="b6544-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="b6544-189">Se você não encontrar o repositório de complemento Olá você pode simplesmente adicionar essas linhas no final de saudação do arquivo .repo tooyour Oracle Linux versão de acordo com:</span><span class="sxs-lookup"><span data-stu-id="b6544-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="b6544-190">Para máquinas virtuais do Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="b6544-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="b6544-191">Para máquinas virtuais do Oracle Linux 7:</span><span class="sxs-lookup"><span data-stu-id="b6544-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="b6544-192">Em seguida, digite:</span><span class="sxs-lookup"><span data-stu-id="b6544-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="b6544-193">Normalmente, isso é tudo o que precisa, mas se por alguma razão, que você precisa tooinstall do https://github.com diretamente, use Olá seguindo as etapas.</span><span class="sxs-lookup"><span data-stu-id="b6544-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="b6544-194">Saudação de atualização quando nenhum pacote do agente de distribuição de agentes do Linux</span><span class="sxs-lookup"><span data-stu-id="b6544-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="b6544-195">Instalar wget (há algumas distribuições que não instalação-lo por padrão, como Redhat, CentOS e Oracle Linux versões 6.4 e 6.5) digitando `sudo yum install wget` na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="b6544-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="b6544-196">1. Baixar a versão mais recente da saudação</span><span class="sxs-lookup"><span data-stu-id="b6544-196">1. Download hello latest version</span></span>
<span data-ttu-id="b6544-197">Abra [Olá versão do agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent/releases) em uma página da web e descobrir o número de versão mais recente da saudação.</span><span class="sxs-lookup"><span data-stu-id="b6544-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="b6544-198">(Você pode localizar sua versão atual digitando `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="b6544-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="b6544-199">Para a versão 2.2. x ou posterior, digite:</span><span class="sxs-lookup"><span data-stu-id="b6544-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="b6544-200">Olá linha a seguir usa a versão 2.2.0 como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="b6544-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="b6544-201">2. Instalar Olá agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="b6544-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="b6544-202">Para a versão 2.2. x, use:</span><span class="sxs-lookup"><span data-stu-id="b6544-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="b6544-203">Talvez seja necessário um pacote de saudação tooinstall `setuptools` primeiro – consulte [aqui](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="b6544-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="b6544-204">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="b6544-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="b6544-205">Verificar se a atualização automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="b6544-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="b6544-206">Primeiro, verifique toosee se ela está habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="b6544-207">Localize 'AutoUpdate.Enabled'.</span><span class="sxs-lookup"><span data-stu-id="b6544-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="b6544-208">Se você vir esta saída, ela estará habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6544-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="b6544-209">tooenable executar:</span><span class="sxs-lookup"><span data-stu-id="b6544-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="b6544-210">3. Reinicie o serviço de waagent Olá</span><span class="sxs-lookup"><span data-stu-id="b6544-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="b6544-211">Para a maioria das distribuições do Linux:</span><span class="sxs-lookup"><span data-stu-id="b6544-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="b6544-212">Para o Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="b6544-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="b6544-213">Para o CoreOS, use:</span><span class="sxs-lookup"><span data-stu-id="b6544-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="b6544-214">4. Confirmar hello Azure Linux Agent versão</span><span class="sxs-lookup"><span data-stu-id="b6544-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="b6544-215">Para CoreOS, Olá acima comando pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="b6544-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="b6544-216">Você verá que hello Azure Linux Agent versão tiver sido atualizada toohello nova versão.</span><span class="sxs-lookup"><span data-stu-id="b6544-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="b6544-217">Para obter mais informações sobre Olá agente Linux do Azure, consulte [Azure Linux Agent Leiame](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="b6544-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
