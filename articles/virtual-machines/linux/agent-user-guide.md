---
title: "Visão geral do Agente de VM do Azure Linux | Microsoft Docs"
description: "Saiba como instalar e configurar o agente Linux (waagent) para gerenciar sua interação de máquina virtual com os Recursos de Infraestrutura do Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="d78c9-103">Noções básicas e uso do Agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="d78c9-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="d78c9-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="d78c9-104">Introduction</span></span>
<span data-ttu-id="d78c9-105">O Agente Linux do Microsoft Azure (waagent) gerencia o provisionamento de Linux e FreeBSD e a interação de VM com o Controlador de malha do Azure.</span><span class="sxs-lookup"><span data-stu-id="d78c9-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="d78c9-106">Ele fornece a seguinte funcionalidade para implantações IaaS do Linux e FreeBSD:</span><span class="sxs-lookup"><span data-stu-id="d78c9-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="d78c9-107">Consulte o arquivo [LEIA-ME](https://github.com/Azure/WALinuxAgent/blob/master/README.md) do agente Linux do Azure para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d78c9-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="d78c9-108">**Provisionamento de imagem**</span><span class="sxs-lookup"><span data-stu-id="d78c9-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="d78c9-109">Criação de uma conta de usuário</span><span class="sxs-lookup"><span data-stu-id="d78c9-109">Creation of a user account</span></span>
  * <span data-ttu-id="d78c9-110">Configurando os tipos de autenticação do SSH</span><span class="sxs-lookup"><span data-stu-id="d78c9-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="d78c9-111">Implantação de chaves públicas do SSH e pares de chaves</span><span class="sxs-lookup"><span data-stu-id="d78c9-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="d78c9-112">Configuração do nome de host</span><span class="sxs-lookup"><span data-stu-id="d78c9-112">Setting the host name</span></span>
  * <span data-ttu-id="d78c9-113">Publicando o nome do host para a plataforma de DNS</span><span class="sxs-lookup"><span data-stu-id="d78c9-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="d78c9-114">Relatório de impressão digital da chave host SSH para a plataforma</span><span class="sxs-lookup"><span data-stu-id="d78c9-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="d78c9-115">Gerenciamento de recursos de disco</span><span class="sxs-lookup"><span data-stu-id="d78c9-115">Resource Disk Management</span></span>
  * <span data-ttu-id="d78c9-116">Formatação e montagem do disco do recurso</span><span class="sxs-lookup"><span data-stu-id="d78c9-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="d78c9-117">Configurando o espaço de permuta</span><span class="sxs-lookup"><span data-stu-id="d78c9-117">Configuring swap space</span></span>
* <span data-ttu-id="d78c9-118">**Rede**</span><span class="sxs-lookup"><span data-stu-id="d78c9-118">**Networking**</span></span>
  
  * <span data-ttu-id="d78c9-119">Gerencia as rotas para melhorar a compatibilidade com os servidores DHCP de plataforma</span><span class="sxs-lookup"><span data-stu-id="d78c9-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="d78c9-120">Garante a estabilidade do nome da interface de rede</span><span class="sxs-lookup"><span data-stu-id="d78c9-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="d78c9-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="d78c9-121">**Kernel**</span></span>
  
  * <span data-ttu-id="d78c9-122">Configura NUMA virtual (desabilitar para kernel < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="d78c9-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="d78c9-123">Consome entropia de Hyper-V para /dev/random</span><span class="sxs-lookup"><span data-stu-id="d78c9-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="d78c9-124">Configura os tempos limite de SCSI para o dispositivo raiz (o qual poderia ser remoto)</span><span class="sxs-lookup"><span data-stu-id="d78c9-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="d78c9-125">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="d78c9-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="d78c9-126">Redirecionamento de console de porta serial</span><span class="sxs-lookup"><span data-stu-id="d78c9-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="d78c9-127">**Implantações SCVMM**</span><span class="sxs-lookup"><span data-stu-id="d78c9-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="d78c9-128">Detecta e inicializa o agente VMM para Linux quando executado em um ambiente de System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d78c9-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="d78c9-129">**Extensão de VM**</span><span class="sxs-lookup"><span data-stu-id="d78c9-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="d78c9-130">Injete o componente criado pela Microsoft e seus Parceiros na VM do Linux (IaaS) para habilitar o software e a automação da configuração</span><span class="sxs-lookup"><span data-stu-id="d78c9-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="d78c9-131">Implementação de referência de extensão de VM em [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="d78c9-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="d78c9-132">Comunicação</span><span class="sxs-lookup"><span data-stu-id="d78c9-132">Communication</span></span>
<span data-ttu-id="d78c9-133">O fluxo de informações da plataforma para o agente ocorre por meio de dois canais:</span><span class="sxs-lookup"><span data-stu-id="d78c9-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="d78c9-134">Um DVD anexado ao tempo de inicialização para as implementações de IaaS.</span><span class="sxs-lookup"><span data-stu-id="d78c9-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="d78c9-135">Este DVD inclui um arquivo de configuração compatível com OVF que inclui todas as informações de configuração que não seja os pares de chaves SSH real.</span><span class="sxs-lookup"><span data-stu-id="d78c9-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="d78c9-136">Um ponto de extremidade TCP expondo uma API REST usada para obter a implantação e a configuração de topologia.</span><span class="sxs-lookup"><span data-stu-id="d78c9-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="d78c9-137">Requisitos</span><span class="sxs-lookup"><span data-stu-id="d78c9-137">Requirements</span></span>
<span data-ttu-id="d78c9-138">Os sistemas a seguir foram testados e funcionam com o agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="d78c9-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="d78c9-139">Essa lista pode ser diferente da lista oficial de sistemas com suporte na plataforma Microsoft Azure, conforme descrito aqui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="d78c9-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="d78c9-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="d78c9-140">CoreOS</span></span>
* <span data-ttu-id="d78c9-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="d78c9-141">CentOS 6.3+</span></span>
* <span data-ttu-id="d78c9-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="d78c9-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="d78c9-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="d78c9-143">Debian 7.0+</span></span>
* <span data-ttu-id="d78c9-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="d78c9-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="d78c9-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="d78c9-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="d78c9-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="d78c9-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="d78c9-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="d78c9-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="d78c9-148">Outros sistemas com suporte:</span><span class="sxs-lookup"><span data-stu-id="d78c9-148">Other Supported Systems:</span></span>

* <span data-ttu-id="d78c9-149">FreeBSD 10+ (Agente Linux do Azure v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="d78c9-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="d78c9-150">O agente do Linux depende de alguns pacotes de sistema para funcionar corretamente:</span><span class="sxs-lookup"><span data-stu-id="d78c9-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="d78c9-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="d78c9-151">Python 2.6+</span></span>
* <span data-ttu-id="d78c9-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="d78c9-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="d78c9-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="d78c9-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="d78c9-154">Utilitários de sistema de arquivos: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="d78c9-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="d78c9-155">Ferramentas de senha: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="d78c9-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="d78c9-156">Ferramentas de processamento de texto: sed, grep</span><span class="sxs-lookup"><span data-stu-id="d78c9-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="d78c9-157">Ferramentas de rede: roteamento ip</span><span class="sxs-lookup"><span data-stu-id="d78c9-157">Network tools: ip-route</span></span>
* <span data-ttu-id="d78c9-158">Suporte a kernel para montar sistemas de arquivos UDF.</span><span class="sxs-lookup"><span data-stu-id="d78c9-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="d78c9-159">Instalação</span><span class="sxs-lookup"><span data-stu-id="d78c9-159">Installation</span></span>
<span data-ttu-id="d78c9-160">Instalação usando um RPM ou um pacote DEB do repositório de pacotes da distribuição é o método preferencial para instalar e atualizar o Azure do Agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="d78c9-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="d78c9-161">Todos os [provedores de distribuição aprovados](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integram o pacote do agente Linux do Azure em suas imagens e repositórios.</span><span class="sxs-lookup"><span data-stu-id="d78c9-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="d78c9-162">Consulte a documentação do [repositório do agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent) para ver opções de instalação avançada, como instalação da origem ou em locais personalizados ou prefixos.</span><span class="sxs-lookup"><span data-stu-id="d78c9-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="d78c9-163">Opções de linha de comando</span><span class="sxs-lookup"><span data-stu-id="d78c9-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="d78c9-164">Sinalizadores</span><span class="sxs-lookup"><span data-stu-id="d78c9-164">Flags</span></span>
* <span data-ttu-id="d78c9-165">verbose: aumentar o nível de detalhes do comando especificado</span><span class="sxs-lookup"><span data-stu-id="d78c9-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="d78c9-166">forçar: Ignorar confirmação interativa para alguns comandos</span><span class="sxs-lookup"><span data-stu-id="d78c9-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="d78c9-167">Comandos</span><span class="sxs-lookup"><span data-stu-id="d78c9-167">Commands</span></span>
* <span data-ttu-id="d78c9-168">Ajuda: lista os comandos com suporte e sinalizadores.</span><span class="sxs-lookup"><span data-stu-id="d78c9-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="d78c9-169">deprovision: tentativa de limpar o sistema e torná-lo adequado para reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="d78c9-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="d78c9-170">Esta operação excluiu o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d78c9-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="d78c9-171">Todas as chaves de host SSH (se Provisioning.RegenerateSshHostKeyPair for 'y' no arquivo de configuração)</span><span class="sxs-lookup"><span data-stu-id="d78c9-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="d78c9-172">Configuração de servidor de nomes em /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="d78c9-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="d78c9-173">Senha raiz do /etc/shadow (se Provisioning.DeleteRootPassword for 'y' no arquivo de configuração)</span><span class="sxs-lookup"><span data-stu-id="d78c9-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="d78c9-174">Concessões de cliente DHCP em cache</span><span class="sxs-lookup"><span data-stu-id="d78c9-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="d78c9-175">Reinicia o nome de host para localdomain.localdomain</span><span class="sxs-lookup"><span data-stu-id="d78c9-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="d78c9-176">O desprovisionamento não garante que a imagem estará livre de todas as informações confidenciais e adequada para redistribuição.</span><span class="sxs-lookup"><span data-stu-id="d78c9-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="d78c9-177">deprovision + user: executa tudo em - deprovision (acima) e também exclui a última conta de usuário provisionado (obtida em /var/lib/waagent) e dados associados.</span><span class="sxs-lookup"><span data-stu-id="d78c9-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="d78c9-178">Este parâmetro é quando a desconfiguração de uma imagem que foi anteriormente provisionamento no Azure para podem ser capturada e usada novamente.</span><span class="sxs-lookup"><span data-stu-id="d78c9-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="d78c9-179">versão: exibe a versão do waagent</span><span class="sxs-lookup"><span data-stu-id="d78c9-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="d78c9-180">serialconsole: configura GRUB para marcar ttyS0 (a primeira porta serial) como o console de inicialização.</span><span class="sxs-lookup"><span data-stu-id="d78c9-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="d78c9-181">Isso garante que os logs de inicialização do kernel são enviados para a porta serial e disponibilizados para depuração.</span><span class="sxs-lookup"><span data-stu-id="d78c9-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="d78c9-182">daemon: executar waagent como um daemon para gerenciar a interação com a plataforma.</span><span class="sxs-lookup"><span data-stu-id="d78c9-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="d78c9-183">Esse argumento é especificado para waagent no script de inicialização de waagent.</span><span class="sxs-lookup"><span data-stu-id="d78c9-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="d78c9-184">Iniciar: executar waagent como um processo em segundo plano</span><span class="sxs-lookup"><span data-stu-id="d78c9-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="d78c9-185">Configuração</span><span class="sxs-lookup"><span data-stu-id="d78c9-185">Configuration</span></span>
<span data-ttu-id="d78c9-186">Um arquivo de configuração (/ etc/waagent.conf) controla as ações de waagent.</span><span class="sxs-lookup"><span data-stu-id="d78c9-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="d78c9-187">Uma amostra do arquivo de configuração é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="d78c9-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="d78c9-188">Várias opções de configuração são descritas em detalhes abaixo.</span><span class="sxs-lookup"><span data-stu-id="d78c9-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="d78c9-189">Há três tipos opções de configuração: Booliano, String ou Integer.</span><span class="sxs-lookup"><span data-stu-id="d78c9-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="d78c9-190">As opções de configuração booliana podem ser especificadas como "y" ou "n".</span><span class="sxs-lookup"><span data-stu-id="d78c9-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="d78c9-191">A palavra-chave especial "Nenhum" pode ser usado para entradas de configuração de tipo algum sequência conforme detalhado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d78c9-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="d78c9-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="d78c9-193">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-193">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-194">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="d78c9-194">Default: y</span></span>

<span data-ttu-id="d78c9-195">Isso permite que o usuário habilite ou desabilite a funcionalidade de provisionamento no agente.</span><span class="sxs-lookup"><span data-stu-id="d78c9-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="d78c9-196">Os valores válidos são "y" ou "n".</span><span class="sxs-lookup"><span data-stu-id="d78c9-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="d78c9-197">Se o provisionamento for desabilitado, as chaves SSH de host e usuário da imagem serão preservadas e qualquer configuração especificada na API de provisionamento do Azure será ignorada.</span><span class="sxs-lookup"><span data-stu-id="d78c9-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="d78c9-198">O parâmetro `Provisioning.Enabled` segue o padrão "n" do Ubuntu Cloud Images, que usa cloud-init para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d78c9-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="d78c9-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="d78c9-200">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-200">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-201">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="d78c9-201">Default: n</span></span>

<span data-ttu-id="d78c9-202">Se definido, a senha raiz no arquivo sombra é apagado durante o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d78c9-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="d78c9-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="d78c9-204">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-204">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-205">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="d78c9-205">Default: y</span></span>

<span data-ttu-id="d78c9-206">Se o conjunto de todos os SSH host pares de chaves (ecdsa, dsa e rsa) será excluído durante o processo de provisionamento de /etc/ssh /.</span><span class="sxs-lookup"><span data-stu-id="d78c9-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="d78c9-207">E um único par de chave novo é gerado.</span><span class="sxs-lookup"><span data-stu-id="d78c9-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="d78c9-208">O tipo de criptografia para o novo par de chaves é configurável pela entrada do Provisioning.SshHostKeyPairType.</span><span class="sxs-lookup"><span data-stu-id="d78c9-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="d78c9-209">Observe que algumas distribuições novamente criará pares de chaves SSH para todos os tipos de criptografia está faltando quando é reiniciado o daemon do SSH (por exemplo, após uma reinicialização).</span><span class="sxs-lookup"><span data-stu-id="d78c9-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="d78c9-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="d78c9-211">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="d78c9-211">Type: String</span></span>  
<span data-ttu-id="d78c9-212">Padrão: rsa</span><span class="sxs-lookup"><span data-stu-id="d78c9-212">Default: rsa</span></span>

<span data-ttu-id="d78c9-213">Isso pode ser definido como um tipo de algoritmo de criptografia com suporte pelo daemon SSH na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d78c9-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="d78c9-214">Os valores geralmente aceitos são "rsa", "dsa" e "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="d78c9-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="d78c9-215">Observe que "putty.exe" no Windows não oferece suporte a "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="d78c9-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="d78c9-216">Portanto, se você pretende usar putty.exe no Windows para conectar-se a uma implantação do Linux, use "rsa" ou "dsa".</span><span class="sxs-lookup"><span data-stu-id="d78c9-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="d78c9-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="d78c9-218">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-218">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-219">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="d78c9-219">Default: y</span></span>

<span data-ttu-id="d78c9-220">Se definido, waagent monitorará máquina virtual Linux para alterações de nome do host (conforme retornado pelo comando "hostname") e atualizar automaticamente a configuração de rede da imagem para refletir a alteração.</span><span class="sxs-lookup"><span data-stu-id="d78c9-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="d78c9-221">Para enviar a alteração do nome para os servidores DNS, a rede será reiniciado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d78c9-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="d78c9-222">Isso resultará em resumo perda de conectividade com a Internet.</span><span class="sxs-lookup"><span data-stu-id="d78c9-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="d78c9-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="d78c9-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="d78c9-224">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-224">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-225">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="d78c9-225">Default: n</span></span>

<span data-ttu-id="d78c9-226">Se definido, o waagent decodificará o CustomData da Base64.</span><span class="sxs-lookup"><span data-stu-id="d78c9-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="d78c9-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="d78c9-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="d78c9-228">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-228">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-229">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="d78c9-229">Default: n</span></span>

<span data-ttu-id="d78c9-230">Se definido, o waagent executará o CustomData após o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d78c9-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="d78c9-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="d78c9-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="d78c9-232">Tipo: Sequência</span><span class="sxs-lookup"><span data-stu-id="d78c9-232">Type:String</span></span>  
<span data-ttu-id="d78c9-233">Padrão: 6</span><span class="sxs-lookup"><span data-stu-id="d78c9-233">Default:6</span></span>

<span data-ttu-id="d78c9-234">Algoritmo usado pelo Crypt ao gerar o hash de senha.</span><span class="sxs-lookup"><span data-stu-id="d78c9-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="d78c9-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="d78c9-235">1 - MD5</span></span>  
 <span data-ttu-id="d78c9-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="d78c9-236">2a - Blowfish</span></span>  
 <span data-ttu-id="d78c9-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="d78c9-237">5 - SHA-256</span></span>  
 <span data-ttu-id="d78c9-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="d78c9-238">6 - SHA-512</span></span>  

<span data-ttu-id="d78c9-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="d78c9-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="d78c9-240">Tipo: Sequência</span><span class="sxs-lookup"><span data-stu-id="d78c9-240">Type:String</span></span>  
<span data-ttu-id="d78c9-241">Padrão: 10</span><span class="sxs-lookup"><span data-stu-id="d78c9-241">Default:10</span></span>

<span data-ttu-id="d78c9-242">Comprimento de sal aleatório usado ao gerar o hash de senha.</span><span class="sxs-lookup"><span data-stu-id="d78c9-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="d78c9-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="d78c9-244">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-244">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-245">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="d78c9-245">Default: y</span></span>

<span data-ttu-id="d78c9-246">Se definido, o disco de recursos fornecido pela plataforma será formatado e montado por waagent se o tipo de sistema de arquivos solicitado pelo usuário em "ResourceDisk.Filesystem" for algo diferente de "ntfs".</span><span class="sxs-lookup"><span data-stu-id="d78c9-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="d78c9-247">Uma única partição do tipo Linux (83) será disponibilizada no disco.</span><span class="sxs-lookup"><span data-stu-id="d78c9-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="d78c9-248">Observe que essa partição não será formatada se ele pode ser montado com êxito.</span><span class="sxs-lookup"><span data-stu-id="d78c9-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="d78c9-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="d78c9-250">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="d78c9-250">Type: String</span></span>  
<span data-ttu-id="d78c9-251">Padrão: ext4</span><span class="sxs-lookup"><span data-stu-id="d78c9-251">Default: ext4</span></span>

<span data-ttu-id="d78c9-252">Especifica o tipo de sistema de arquivos para o disco do recurso.</span><span class="sxs-lookup"><span data-stu-id="d78c9-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="d78c9-253">Valores aceitos variam de acordo com a distribuição do Linux.</span><span class="sxs-lookup"><span data-stu-id="d78c9-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="d78c9-254">Se a sequência for X, em seguida, mkfs.X deve estar presente na imagem do Linux.</span><span class="sxs-lookup"><span data-stu-id="d78c9-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="d78c9-255">Imagens de 11 SLES geralmente devem utilizar 'ext3'.</span><span class="sxs-lookup"><span data-stu-id="d78c9-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="d78c9-256">FreeBSD imagens devem usar 'ufs2' aqui.</span><span class="sxs-lookup"><span data-stu-id="d78c9-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="d78c9-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="d78c9-258">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="d78c9-258">Type: String</span></span>  
<span data-ttu-id="d78c9-259">Padrão: recurso /dev/emcpowera1</span><span class="sxs-lookup"><span data-stu-id="d78c9-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="d78c9-260">Especifica o caminho em que o disco do recurso é montado.</span><span class="sxs-lookup"><span data-stu-id="d78c9-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="d78c9-261">Observe que o disco de recurso é um disco *temporário* e pode ser esvaziado quando a VM é desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="d78c9-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="d78c9-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="d78c9-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="d78c9-263">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="d78c9-263">Type: String</span></span>  
<span data-ttu-id="d78c9-264">Padrão: nenhum</span><span class="sxs-lookup"><span data-stu-id="d78c9-264">Default: None</span></span>

<span data-ttu-id="d78c9-265">Especifica opções de montagem de disco a serem passadas ao comando de montagem -o.</span><span class="sxs-lookup"><span data-stu-id="d78c9-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="d78c9-266">Trata-se de uma lista de valores separados por vírgulas, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="d78c9-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="d78c9-267">'nodev, nosuid'.</span><span class="sxs-lookup"><span data-stu-id="d78c9-267">'nodev,nosuid'.</span></span> <span data-ttu-id="d78c9-268">Consulte montagem(8) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d78c9-268">See mount(8) for details.</span></span>

<span data-ttu-id="d78c9-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="d78c9-270">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-270">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-271">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="d78c9-271">Default: n</span></span>

<span data-ttu-id="d78c9-272">Se definir um arquivo de permuta (/ arquivo de permuta) é criado no disco recursos e adicionado ao espaço de troca de sistema.</span><span class="sxs-lookup"><span data-stu-id="d78c9-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="d78c9-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="d78c9-274">Tipo: inteiro</span><span class="sxs-lookup"><span data-stu-id="d78c9-274">Type: Integer</span></span>  
<span data-ttu-id="d78c9-275">Padrão: 0</span><span class="sxs-lookup"><span data-stu-id="d78c9-275">Default: 0</span></span>

<span data-ttu-id="d78c9-276">Especifica o tamanho máximo do arquivo de permuta em megabytes.</span><span class="sxs-lookup"><span data-stu-id="d78c9-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="d78c9-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="d78c9-278">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-278">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-279">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="d78c9-279">Default: n</span></span>

<span data-ttu-id="d78c9-280">Se definido, a verbosidade do log é aumentado.</span><span class="sxs-lookup"><span data-stu-id="d78c9-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="d78c9-281">Waagent faz /var/log/waagent.log e aproveita a funcionalidade de logrotate do sistema para girar os logs.</span><span class="sxs-lookup"><span data-stu-id="d78c9-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="d78c9-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="d78c9-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="d78c9-283">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="d78c9-283">Type: Boolean</span></span>  
<span data-ttu-id="d78c9-284">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="d78c9-284">Default: n</span></span>

<span data-ttu-id="d78c9-285">Se definido, o agente tentará instalar e, em seguida, carregar um driver de kernel RDMA que corresponde à versão do firmware do hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="d78c9-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="d78c9-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="d78c9-287">Tipo: inteiro</span><span class="sxs-lookup"><span data-stu-id="d78c9-287">Type: Integer</span></span>  
<span data-ttu-id="d78c9-288">Padrão: 300</span><span class="sxs-lookup"><span data-stu-id="d78c9-288">Default: 300</span></span>

<span data-ttu-id="d78c9-289">Isso configura o tempo limite de SCSI em segundos nos drives de disco e os dados de SO.</span><span class="sxs-lookup"><span data-stu-id="d78c9-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="d78c9-290">Se não for definido, o sistema de padrões são usados.</span><span class="sxs-lookup"><span data-stu-id="d78c9-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="d78c9-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="d78c9-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="d78c9-292">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="d78c9-292">Type: String</span></span>  
<span data-ttu-id="d78c9-293">Padrão: nenhum</span><span class="sxs-lookup"><span data-stu-id="d78c9-293">Default: None</span></span>

<span data-ttu-id="d78c9-294">Isso pode ser usado para especificar um caminho alternativo para o openssl binário a ser usado para operações de criptografia.</span><span class="sxs-lookup"><span data-stu-id="d78c9-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="d78c9-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="d78c9-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="d78c9-296">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="d78c9-296">Type: String</span></span>  
<span data-ttu-id="d78c9-297">Padrão: nenhum</span><span class="sxs-lookup"><span data-stu-id="d78c9-297">Default: None</span></span>

<span data-ttu-id="d78c9-298">Se definido, o agente usará este servidor proxy para acessar a internet.</span><span class="sxs-lookup"><span data-stu-id="d78c9-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="d78c9-299">Imagens de nuvem do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d78c9-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="d78c9-300">Observe que as Imagens de Nuvem do Ubuntu utilizam [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) para executar muitas tarefas de configuração que de outra forma seriam gerenciadas pelo Agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="d78c9-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="d78c9-301">Observe as seguintes diferenças:</span><span class="sxs-lookup"><span data-stu-id="d78c9-301">Please note the following differences:</span></span>

* <span data-ttu-id="d78c9-302">**Provisioning.Enabled** segue o padrão "n" nas Imagens de Nuvem do Ubuntu que usam cloud-init para executar tarefas de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d78c9-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="d78c9-303">Os seguintes parâmetros de configuração não têm efeito nas Imagens de Nuvem do Ubuntu que usam cloud-init para gerenciar o disco de recurso e o espaço de troca:</span><span class="sxs-lookup"><span data-stu-id="d78c9-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="d78c9-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="d78c9-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="d78c9-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="d78c9-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="d78c9-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="d78c9-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="d78c9-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="d78c9-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="d78c9-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="d78c9-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="d78c9-309">Consulte os seguintes recursos para configurar o ponto de montagem do disco de recurso e o espaço de troca nas Imagens de Nuvem do Ubuntu durante o provisionamento:</span><span class="sxs-lookup"><span data-stu-id="d78c9-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="d78c9-310">Wiki do Ubuntu: configurar partições de troca</span><span class="sxs-lookup"><span data-stu-id="d78c9-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="d78c9-311">Injetando dados personalizados em uma Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="d78c9-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

