---
title: "aaaAzure visão geral de agente de VM do Linux | Microsoft Docs"
description: "Saiba como tooinstall e configurar o agente do Linux (waagent) toomanage interação da sua máquina virtual com o controlador de malha do Azure."
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
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="73eac-103">Entendendo e usando Olá agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="73eac-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="73eac-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="73eac-104">Introduction</span></span>
<span data-ttu-id="73eac-105">Olá Microsoft Azure Linux Agent (waagent) gerencia Linux e FreeBSD provisionamento e interação de VM com hello controlador de malha do Azure.</span><span class="sxs-lookup"><span data-stu-id="73eac-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="73eac-106">Ele fornece Olá funcionalidade para implantações do Linux e FreeBSD IaaS a seguir:</span><span class="sxs-lookup"><span data-stu-id="73eac-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="73eac-107">Consulte hello Azure Linux agent [Leiame](https://github.com/Azure/WALinuxAgent/blob/master/README.md) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="73eac-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="73eac-108">**Provisionamento de imagem**</span><span class="sxs-lookup"><span data-stu-id="73eac-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="73eac-109">Criação de uma conta de usuário</span><span class="sxs-lookup"><span data-stu-id="73eac-109">Creation of a user account</span></span>
  * <span data-ttu-id="73eac-110">Configurando os tipos de autenticação do SSH</span><span class="sxs-lookup"><span data-stu-id="73eac-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="73eac-111">Implantação de chaves públicas do SSH e pares de chaves</span><span class="sxs-lookup"><span data-stu-id="73eac-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="73eac-112">Nome de host da saudação de configuração</span><span class="sxs-lookup"><span data-stu-id="73eac-112">Setting hello host name</span></span>
  * <span data-ttu-id="73eac-113">Publicação Olá nome toohello plataforma de host DNS</span><span class="sxs-lookup"><span data-stu-id="73eac-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="73eac-114">SSH host impressão digital da chave toohello plataforma de relatórios</span><span class="sxs-lookup"><span data-stu-id="73eac-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="73eac-115">Gerenciamento de recursos de disco</span><span class="sxs-lookup"><span data-stu-id="73eac-115">Resource Disk Management</span></span>
  * <span data-ttu-id="73eac-116">Formatação e montar o disco de recurso Olá</span><span class="sxs-lookup"><span data-stu-id="73eac-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="73eac-117">Configurando o espaço de permuta</span><span class="sxs-lookup"><span data-stu-id="73eac-117">Configuring swap space</span></span>
* <span data-ttu-id="73eac-118">**Rede**</span><span class="sxs-lookup"><span data-stu-id="73eac-118">**Networking**</span></span>
  
  * <span data-ttu-id="73eac-119">Gerencia rotas tooimprove compatibilidade com servidores DHCP de plataforma</span><span class="sxs-lookup"><span data-stu-id="73eac-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="73eac-120">Garante a estabilidade de saudação do nome de interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="73eac-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="73eac-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="73eac-121">**Kernel**</span></span>
  
  * <span data-ttu-id="73eac-122">Configura NUMA virtual (desabilitar para kernel < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="73eac-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="73eac-123">Consome entropia de Hyper-V para /dev/random</span><span class="sxs-lookup"><span data-stu-id="73eac-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="73eac-124">Configura o tempo limite de SCSI para dispositivo de raiz da saudação (que poderia ser remoto)</span><span class="sxs-lookup"><span data-stu-id="73eac-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="73eac-125">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="73eac-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="73eac-126">Redirecionamento de console toohello porta serial</span><span class="sxs-lookup"><span data-stu-id="73eac-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="73eac-127">**Implantações SCVMM**</span><span class="sxs-lookup"><span data-stu-id="73eac-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="73eac-128">Detecta e inicializa o agente do VMM Olá para Linux, quando executado em um ambiente do System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="73eac-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="73eac-129">**Extensão de VM**</span><span class="sxs-lookup"><span data-stu-id="73eac-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="73eac-130">Inserir componente criada pela Microsoft e de parceiros para a automação de software e configuração de VM do Linux (IaaS) tooenable</span><span class="sxs-lookup"><span data-stu-id="73eac-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="73eac-131">Implementação de referência de extensão de VM em [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="73eac-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="73eac-132">Comunicação</span><span class="sxs-lookup"><span data-stu-id="73eac-132">Communication</span></span>
<span data-ttu-id="73eac-133">fluxo de informações de saudação do agente de toohello plataforma Olá ocorre por meio de dois canais:</span><span class="sxs-lookup"><span data-stu-id="73eac-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="73eac-134">Um DVD anexado ao tempo de inicialização para as implementações de IaaS.</span><span class="sxs-lookup"><span data-stu-id="73eac-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="73eac-135">DVD inclui um arquivo de configuração compatível com OVF que inclui todas as informações de provisionamento diferente Olá real pares de chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="73eac-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="73eac-136">Um ponto de extremidade TCP expor uma API REST usado tooobtain implantação e configuração de topologia.</span><span class="sxs-lookup"><span data-stu-id="73eac-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="73eac-137">Requisitos</span><span class="sxs-lookup"><span data-stu-id="73eac-137">Requirements</span></span>
<span data-ttu-id="73eac-138">Hello sistemas a seguir foram testados e que são conhecidos toowork com hello agente Linux do Azure:</span><span class="sxs-lookup"><span data-stu-id="73eac-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="73eac-139">Essa lista pode ser diferente da lista oficial de saudação de sistemas em Olá plataforma Microsoft Azure, conforme descrito aqui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="73eac-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="73eac-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="73eac-140">CoreOS</span></span>
* <span data-ttu-id="73eac-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="73eac-141">CentOS 6.3+</span></span>
* <span data-ttu-id="73eac-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="73eac-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="73eac-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="73eac-143">Debian 7.0+</span></span>
* <span data-ttu-id="73eac-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="73eac-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="73eac-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="73eac-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="73eac-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="73eac-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="73eac-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="73eac-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="73eac-148">Outros sistemas com suporte:</span><span class="sxs-lookup"><span data-stu-id="73eac-148">Other Supported Systems:</span></span>

* <span data-ttu-id="73eac-149">FreeBSD 10+ (Agente Linux do Azure v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="73eac-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="73eac-150">agente do Linux Olá depende de alguns pacotes de sistema na ordem toofunction corretamente:</span><span class="sxs-lookup"><span data-stu-id="73eac-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="73eac-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="73eac-151">Python 2.6+</span></span>
* <span data-ttu-id="73eac-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="73eac-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="73eac-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="73eac-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="73eac-154">Utilitários de sistema de arquivos: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="73eac-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="73eac-155">Ferramentas de senha: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="73eac-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="73eac-156">Ferramentas de processamento de texto: sed, grep</span><span class="sxs-lookup"><span data-stu-id="73eac-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="73eac-157">Ferramentas de rede: roteamento ip</span><span class="sxs-lookup"><span data-stu-id="73eac-157">Network tools: ip-route</span></span>
* <span data-ttu-id="73eac-158">Suporte a kernel para montar sistemas de arquivos UDF.</span><span class="sxs-lookup"><span data-stu-id="73eac-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="73eac-159">Instalação</span><span class="sxs-lookup"><span data-stu-id="73eac-159">Installation</span></span>
<span data-ttu-id="73eac-160">Instalação usando um RPM ou um pacote de DEB do repositório de pacotes de distribuição é o método preferido de saudação instalando e atualizando Olá agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="73eac-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="73eac-161">Saudação de todos os [aprovados provedores distribuição](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrar o pacote de saudação do agente Linux do Azure em suas imagens e repositórios.</span><span class="sxs-lookup"><span data-stu-id="73eac-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="73eac-162">Consulte a documentação do toohello em Olá [repositório de agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent) para opções de instalação avançada, como instalação de locais de origem ou toocustom ou prefixos.</span><span class="sxs-lookup"><span data-stu-id="73eac-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="73eac-163">Opções de linha de comando</span><span class="sxs-lookup"><span data-stu-id="73eac-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="73eac-164">Sinalizadores</span><span class="sxs-lookup"><span data-stu-id="73eac-164">Flags</span></span>
* <span data-ttu-id="73eac-165">verbose: aumentar o nível de detalhes do comando especificado</span><span class="sxs-lookup"><span data-stu-id="73eac-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="73eac-166">forçar: Ignorar confirmação interativa para alguns comandos</span><span class="sxs-lookup"><span data-stu-id="73eac-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="73eac-167">Comandos</span><span class="sxs-lookup"><span data-stu-id="73eac-167">Commands</span></span>
* <span data-ttu-id="73eac-168">Ajuda: lista de sinalizadores e comandos de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="73eac-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="73eac-169">desprovisionamento: tentativa de sistema de saudação tooclean e torná-lo adequado para provisionamento novamente.</span><span class="sxs-lookup"><span data-stu-id="73eac-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="73eac-170">Esta operação excluídos seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="73eac-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="73eac-171">Todas as chaves de host do SSH (se Provisioning.RegenerateSshHostKeyPair for 'y' no arquivo de configuração de saudação)</span><span class="sxs-lookup"><span data-stu-id="73eac-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="73eac-172">Configuração de servidor de nomes em /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="73eac-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="73eac-173">Senha de raiz de /etc/shadow (se Provisioning.DeleteRootPassword for 'y' no arquivo de configuração de saudação)</span><span class="sxs-lookup"><span data-stu-id="73eac-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="73eac-174">Concessões de cliente DHCP em cache</span><span class="sxs-lookup"><span data-stu-id="73eac-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="73eac-175">Redefine toolocalhost.localdomain de nome de host</span><span class="sxs-lookup"><span data-stu-id="73eac-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="73eac-176">Desprovisionamento não garante que essa imagem Olá é limpo de todas as informações confidenciais e adequada para redistribuição.</span><span class="sxs-lookup"><span data-stu-id="73eac-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="73eac-177">desprovisionamento + user: executa tudo sob - desprovisionamento (acima) e também exclui a conta de usuário provisionado última hello (obtida /var/lib/waagent) e dados associados.</span><span class="sxs-lookup"><span data-stu-id="73eac-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="73eac-178">Este parâmetro é quando a desconfiguração de uma imagem que foi anteriormente provisionamento no Azure para podem ser capturada e usada novamente.</span><span class="sxs-lookup"><span data-stu-id="73eac-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="73eac-179">versão: exibe a versão de saudação do waagent</span><span class="sxs-lookup"><span data-stu-id="73eac-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="73eac-180">serialconsole: configura GRUB toomark ttyS0 (Olá a primeira porta serial) como o console de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="73eac-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="73eac-181">Isso garante que os logs de inicialização do kernel são enviadas de porta serial toothe e disponibilizados para depuração.</span><span class="sxs-lookup"><span data-stu-id="73eac-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="73eac-182">o daemon: executar waagent como uma interação de toomanage daemon com a plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="73eac-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="73eac-183">Esse argumento é toowaagent especificado no script de inicialização de waagent hello.</span><span class="sxs-lookup"><span data-stu-id="73eac-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="73eac-184">Iniciar: executar waagent como um processo em segundo plano</span><span class="sxs-lookup"><span data-stu-id="73eac-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="73eac-185">Configuração</span><span class="sxs-lookup"><span data-stu-id="73eac-185">Configuration</span></span>
<span data-ttu-id="73eac-186">Um arquivo de configuração (/ etc/waagent.conf) controles Olá ações de waagent.</span><span class="sxs-lookup"><span data-stu-id="73eac-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="73eac-187">Uma amostra do arquivo de configuração é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="73eac-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="73eac-188">Olá que várias opções de configuração são descritas em detalhes abaixo.</span><span class="sxs-lookup"><span data-stu-id="73eac-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="73eac-189">Há três tipos opções de configuração: Booliano, String ou Integer.</span><span class="sxs-lookup"><span data-stu-id="73eac-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="73eac-190">Opções de configuração booliano Olá podem ser especificadas como "y" ou "n".</span><span class="sxs-lookup"><span data-stu-id="73eac-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="73eac-191">Olá palavra-chave especial "None" pode ser usado para entradas de configuração de tipo alguma cadeia de caracteres conforme detalhado abaixo.</span><span class="sxs-lookup"><span data-stu-id="73eac-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="73eac-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="73eac-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="73eac-193">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-193">Type: Boolean</span></span>  
<span data-ttu-id="73eac-194">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="73eac-194">Default: y</span></span>

<span data-ttu-id="73eac-195">Isso permite Olá usuário tooenable ou desabilitar Olá funcionalidade no agente de saudação de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="73eac-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="73eac-196">Os valores válidos são "y" ou "n".</span><span class="sxs-lookup"><span data-stu-id="73eac-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="73eac-197">Se o provisionamento é desabilitado, as chaves de host e o usuário SSH na imagem de saudação são preservadas e todas as configurações especificadas no hello API de provisionamento do Azure será ignorada.</span><span class="sxs-lookup"><span data-stu-id="73eac-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="73eac-198">Olá `Provisioning.Enabled` muito "n" no Ubuntu imagens de nuvem que usam init de nuvem para o provisionamento de padrões de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="73eac-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="73eac-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="73eac-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="73eac-200">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-200">Type: Boolean</span></span>  
<span data-ttu-id="73eac-201">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="73eac-201">Default: n</span></span>

<span data-ttu-id="73eac-202">Se o conjunto de senha de raiz Olá no arquivo hello/etc/sombra é apagado durante Olá o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="73eac-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="73eac-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="73eac-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="73eac-204">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-204">Type: Boolean</span></span>  
<span data-ttu-id="73eac-205">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="73eac-205">Default: y</span></span>

<span data-ttu-id="73eac-206">Se o conjunto, todos os SSH host pares de chave (ecdsa, dsa e rsa) é excluído durante a saudação processo de /etc/hosts ssh/de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="73eac-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="73eac-207">E um único par de chave novo é gerado.</span><span class="sxs-lookup"><span data-stu-id="73eac-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="73eac-208">tipo de criptografia Olá para o par de chaves novo Olá é configurável por Olá Provisioning.SshHostKeyPairType entrada.</span><span class="sxs-lookup"><span data-stu-id="73eac-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="73eac-209">Observe que algumas distribuições recriará pares de chaves de SSH para quaisquer tipos de criptografia ausente quando o daemon do SSH Olá é reiniciado (por exemplo, após uma reinicialização).</span><span class="sxs-lookup"><span data-stu-id="73eac-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="73eac-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="73eac-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="73eac-211">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="73eac-211">Type: String</span></span>  
<span data-ttu-id="73eac-212">Padrão: rsa</span><span class="sxs-lookup"><span data-stu-id="73eac-212">Default: rsa</span></span>

<span data-ttu-id="73eac-213">Isso pode ser definido tooan tipo de algoritmo de criptografia que é compatível com o daemon do SSH Olá na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="73eac-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="73eac-214">valores Hello normalmente existe suportada são "rsa", "dsa" e "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="73eac-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="73eac-215">Observe que "putty.exe" no Windows não oferece suporte a "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="73eac-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="73eac-216">Portanto, se você pretende toouse putty.exe em Windows tooconnect tooa implantação do Linux, use "rsa" ou "dsa".</span><span class="sxs-lookup"><span data-stu-id="73eac-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="73eac-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="73eac-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="73eac-218">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-218">Type: Boolean</span></span>  
<span data-ttu-id="73eac-219">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="73eac-219">Default: y</span></span>

<span data-ttu-id="73eac-220">Se definido, waagent irá monitorar Olá máquina de virtual do Linux para que as alterações de nome de host (como retornado pelo comando de "nome do host" hello) e atualizar automaticamente a configuração de rede Olá na alteração de Olá Olá imagem tooreflect.</span><span class="sxs-lookup"><span data-stu-id="73eac-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="73eac-221">No nome da ordem toopush Olá alterar toohello os servidores DNS, rede será reiniciada na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="73eac-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="73eac-222">Isso resultará em resumo perda de conectividade com a Internet.</span><span class="sxs-lookup"><span data-stu-id="73eac-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="73eac-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="73eac-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="73eac-224">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-224">Type: Boolean</span></span>  
<span data-ttu-id="73eac-225">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="73eac-225">Default: n</span></span>

<span data-ttu-id="73eac-226">Se definido, o waagent decodificará o CustomData da Base64.</span><span class="sxs-lookup"><span data-stu-id="73eac-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="73eac-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="73eac-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="73eac-228">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-228">Type: Boolean</span></span>  
<span data-ttu-id="73eac-229">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="73eac-229">Default: n</span></span>

<span data-ttu-id="73eac-230">Se definido, o waagent executará o CustomData após o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="73eac-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="73eac-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="73eac-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="73eac-232">Tipo: Sequência</span><span class="sxs-lookup"><span data-stu-id="73eac-232">Type:String</span></span>  
<span data-ttu-id="73eac-233">Padrão: 6</span><span class="sxs-lookup"><span data-stu-id="73eac-233">Default:6</span></span>

<span data-ttu-id="73eac-234">Algoritmo usado pelo Crypt ao gerar o hash de senha.</span><span class="sxs-lookup"><span data-stu-id="73eac-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="73eac-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="73eac-235">1 - MD5</span></span>  
 <span data-ttu-id="73eac-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="73eac-236">2a - Blowfish</span></span>  
 <span data-ttu-id="73eac-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="73eac-237">5 - SHA-256</span></span>  
 <span data-ttu-id="73eac-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="73eac-238">6 - SHA-512</span></span>  

<span data-ttu-id="73eac-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="73eac-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="73eac-240">Tipo: Sequência</span><span class="sxs-lookup"><span data-stu-id="73eac-240">Type:String</span></span>  
<span data-ttu-id="73eac-241">Padrão: 10</span><span class="sxs-lookup"><span data-stu-id="73eac-241">Default:10</span></span>

<span data-ttu-id="73eac-242">Comprimento de sal aleatório usado ao gerar o hash de senha.</span><span class="sxs-lookup"><span data-stu-id="73eac-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="73eac-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="73eac-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="73eac-244">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-244">Type: Boolean</span></span>  
<span data-ttu-id="73eac-245">Padrão: y</span><span class="sxs-lookup"><span data-stu-id="73eac-245">Default: y</span></span>

<span data-ttu-id="73eac-246">Se definido, disco de recurso Olá fornecido pela plataforma Olá será formatado e montado pelo waagent se o tipo de sistema de arquivos de saudação solicitado pelo usuário "ResourceDisk.Filesystem" hello é algo diferente de "ntfs".</span><span class="sxs-lookup"><span data-stu-id="73eac-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="73eac-247">Uma única partição do tipo Linux (83) estará disponível em disco hello.</span><span class="sxs-lookup"><span data-stu-id="73eac-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="73eac-248">Observe que essa partição não será formatada se ele pode ser montado com êxito.</span><span class="sxs-lookup"><span data-stu-id="73eac-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="73eac-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="73eac-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="73eac-250">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="73eac-250">Type: String</span></span>  
<span data-ttu-id="73eac-251">Padrão: ext4</span><span class="sxs-lookup"><span data-stu-id="73eac-251">Default: ext4</span></span>

<span data-ttu-id="73eac-252">Isso especifica o tipo de sistema de arquivos de Olá do disco de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="73eac-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="73eac-253">Valores aceitos variam de acordo com a distribuição do Linux.</span><span class="sxs-lookup"><span data-stu-id="73eac-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="73eac-254">Se X, em seguida, mkfs cadeia de caracteres de saudação. X deve estar presente na imagem do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="73eac-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="73eac-255">Imagens de 11 SLES geralmente devem utilizar 'ext3'.</span><span class="sxs-lookup"><span data-stu-id="73eac-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="73eac-256">FreeBSD imagens devem usar 'ufs2' aqui.</span><span class="sxs-lookup"><span data-stu-id="73eac-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="73eac-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="73eac-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="73eac-258">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="73eac-258">Type: String</span></span>  
<span data-ttu-id="73eac-259">Padrão: recurso /dev/emcpowera1</span><span class="sxs-lookup"><span data-stu-id="73eac-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="73eac-260">Isso especifica o caminho de saudação em que o disco de recurso hello está montado.</span><span class="sxs-lookup"><span data-stu-id="73eac-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="73eac-261">Observe que esse disco de recurso Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="73eac-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="73eac-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="73eac-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="73eac-263">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="73eac-263">Type: String</span></span>  
<span data-ttu-id="73eac-264">Padrão: nenhum</span><span class="sxs-lookup"><span data-stu-id="73eac-264">Default: None</span></span>

<span data-ttu-id="73eac-265">Especifica opções de montagem disco toobe passado toohello mount -o comando.</span><span class="sxs-lookup"><span data-stu-id="73eac-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="73eac-266">Trata-se de uma lista de valores separados por vírgulas, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="73eac-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="73eac-267">'nodev, nosuid'.</span><span class="sxs-lookup"><span data-stu-id="73eac-267">'nodev,nosuid'.</span></span> <span data-ttu-id="73eac-268">Consulte montagem(8) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="73eac-268">See mount(8) for details.</span></span>

<span data-ttu-id="73eac-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="73eac-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="73eac-270">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-270">Type: Boolean</span></span>  
<span data-ttu-id="73eac-271">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="73eac-271">Default: n</span></span>

<span data-ttu-id="73eac-272">Se definido, um arquivo de permuta (/ arquivo de permuta) é criado no disco de recurso hello e adicionado toohello espaço de permuta de sistema.</span><span class="sxs-lookup"><span data-stu-id="73eac-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="73eac-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="73eac-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="73eac-274">Tipo: inteiro</span><span class="sxs-lookup"><span data-stu-id="73eac-274">Type: Integer</span></span>  
<span data-ttu-id="73eac-275">Padrão: 0</span><span class="sxs-lookup"><span data-stu-id="73eac-275">Default: 0</span></span>

<span data-ttu-id="73eac-276">tamanho de Olá Olá do arquivo de permuta em megabytes.</span><span class="sxs-lookup"><span data-stu-id="73eac-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="73eac-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="73eac-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="73eac-278">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-278">Type: Boolean</span></span>  
<span data-ttu-id="73eac-279">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="73eac-279">Default: n</span></span>

<span data-ttu-id="73eac-280">Se definido, a verbosidade do log é aumentado.</span><span class="sxs-lookup"><span data-stu-id="73eac-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="73eac-281">Waagent registros too/var/log/waagent.log e aproveita Olá sistema logrotate funcionalidade toorotate logs.</span><span class="sxs-lookup"><span data-stu-id="73eac-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="73eac-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="73eac-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="73eac-283">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="73eac-283">Type: Boolean</span></span>  
<span data-ttu-id="73eac-284">Padrão: n</span><span class="sxs-lookup"><span data-stu-id="73eac-284">Default: n</span></span>

<span data-ttu-id="73eac-285">Se definido, agente Olá irá tentar tooinstall e, em seguida, carregar um driver de kernel RDMA que corresponde à versão de saudação do firmware Olá Olá hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="73eac-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="73eac-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="73eac-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="73eac-287">Tipo: inteiro</span><span class="sxs-lookup"><span data-stu-id="73eac-287">Type: Integer</span></span>  
<span data-ttu-id="73eac-288">Padrão: 300</span><span class="sxs-lookup"><span data-stu-id="73eac-288">Default: 300</span></span>

<span data-ttu-id="73eac-289">Isso configura o tempo limite de SCSI Olá em segundos em unidades de disco e dados Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="73eac-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="73eac-290">Se não for definido, o sistema Olá padrões são usados.</span><span class="sxs-lookup"><span data-stu-id="73eac-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="73eac-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="73eac-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="73eac-292">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="73eac-292">Type: String</span></span>  
<span data-ttu-id="73eac-293">Padrão: nenhum</span><span class="sxs-lookup"><span data-stu-id="73eac-293">Default: None</span></span>

<span data-ttu-id="73eac-294">Isso pode ser usado toospecify um caminho alternativo para Olá openssl binário toouse para operações criptográficas.</span><span class="sxs-lookup"><span data-stu-id="73eac-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="73eac-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="73eac-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="73eac-296">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="73eac-296">Type: String</span></span>  
<span data-ttu-id="73eac-297">Padrão: nenhum</span><span class="sxs-lookup"><span data-stu-id="73eac-297">Default: None</span></span>

<span data-ttu-id="73eac-298">Se definido, Olá agente usará esse proxy server tooaccess Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="73eac-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="73eac-299">Imagens de nuvem do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="73eac-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="73eac-300">Observe que utilizam o Ubuntu nuvem imagens [init nuvem](https://launchpad.net/ubuntu/+source/cloud-init) tooperform Olá de várias tarefas de configuração, caso contrário, deve ser gerenciadas pelo agente Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="73eac-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="73eac-301">Observação Olá diferenças a seguir:</span><span class="sxs-lookup"><span data-stu-id="73eac-301">Please note hello following differences:</span></span>

* <span data-ttu-id="73eac-302">**Provisioning.Enabled** padrões muito "n" no Ubuntu imagens de nuvem que usam tooperform nuvem init tarefas de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="73eac-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="73eac-303">Olá, parâmetros de configuração a seguir não têm nenhum efeito no Ubuntu imagens de nuvem que usam init nuvem toomanage Olá recurso disco e troca de espaço:</span><span class="sxs-lookup"><span data-stu-id="73eac-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="73eac-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="73eac-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="73eac-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="73eac-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="73eac-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="73eac-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="73eac-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="73eac-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="73eac-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="73eac-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="73eac-309">Consulte Olá após o ponto de montagem do disco de recurso do recursos tooconfigure hello e trocar o espaço no Ubuntu nuvem imagens durante o provisionamento:</span><span class="sxs-lookup"><span data-stu-id="73eac-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="73eac-310">Wiki do Ubuntu: configurar partições de troca</span><span class="sxs-lookup"><span data-stu-id="73eac-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="73eac-311">Injetando dados personalizados em uma Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="73eac-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

