---
title: "aaaConfigure SSHD em máquinas de virtuais de Linux do Azure | Microsoft Docs"
description: "Configure SSHD para práticas recomendadas de segurança e toolockdown SSH tooAzure máquinas virtuais do Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="49b02-103">Configurar o SSHD em VMs do Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="49b02-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="49b02-104">Este artigo mostra como toolockdown Olá servidor SSH no Linux, tooprovide segurança de práticas recomendada e também toospeed o processo de logon do hello SSH usando as chaves de SSH, em vez de senhas.</span><span class="sxs-lookup"><span data-stu-id="49b02-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="49b02-105">bloqueio toofurther SSHD vamos toodisable usuário de raiz de saudação de ser capaz de toologin, limitar Olá os usuários que têm permissão toologin por meio de uma lista de grupos aprovados, desabilitando o protocolo SSH versão 1, definir um bit de chave mínimo e configurar automaticamente logoff de usuários inativos.</span><span class="sxs-lookup"><span data-stu-id="49b02-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="49b02-106">Olá requisitos deste artigo são: uma conta do Azure ([obter uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e [arquivos de chave públicos e privados SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49b02-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="49b02-107">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="49b02-107">Quick Commands</span></span>

<span data-ttu-id="49b02-108">Configurar `/etc/ssh/sshd_config` com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="49b02-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="49b02-109">Desabilitar logons de senha</span><span class="sxs-lookup"><span data-stu-id="49b02-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="49b02-110">Desabilitar logon pelo usuário de raiz de saudação</span><span class="sxs-lookup"><span data-stu-id="49b02-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="49b02-111">Lista de grupos permitidos</span><span class="sxs-lookup"><span data-stu-id="49b02-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="49b02-112">Lista de usuários permitidos</span><span class="sxs-lookup"><span data-stu-id="49b02-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="49b02-113">Desabilitar o protocolo SSH versão 1</span><span class="sxs-lookup"><span data-stu-id="49b02-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="49b02-114">Bits de chave mínimos</span><span class="sxs-lookup"><span data-stu-id="49b02-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="49b02-115">Desconectar usuários ociosos</span><span class="sxs-lookup"><span data-stu-id="49b02-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="49b02-116">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="49b02-116">Detailed Walkthrough</span></span>

<span data-ttu-id="49b02-117">SSHD é hello SSH servidor que executa o hello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="49b02-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="49b02-118">O SSH é um cliente executado em um shell no MacBook, uma estação de trabalho do Linux ou um Bash no Windows.</span><span class="sxs-lookup"><span data-stu-id="49b02-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="49b02-119">SSH é também protocolo hello usado toosecure e criptografar a comunicação de saudação entre sua estação de trabalho e hello tornando SSH também uma VPN (rede Virtual privada) de VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="49b02-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="49b02-120">Neste artigo, é muito importante tookeep logon tooyour abrir VM Linux para apresentação inteira hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="49b02-121">Depois de estabelecer uma conexão SSH, ele permanece como uma sessão aberta como janela Olá não está fechada.</span><span class="sxs-lookup"><span data-stu-id="49b02-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="49b02-122">Tendo um terminal conectado, permite alterações toobe feita toohello service SSHD sem bloqueio se for feita uma alteração significativa.</span><span class="sxs-lookup"><span data-stu-id="49b02-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="49b02-123">Se você seja bloqueado da sua VM do Linux com uma configuração SSHD interrompida, o Azure oferece Olá capacidade tooreset uma configuração SSHD interrompida com hello [extensão de acesso do Azure VM](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49b02-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="49b02-124">Por esse motivo, abra dois terminais e SSH toohello VM do Linux de ambos.</span><span class="sxs-lookup"><span data-stu-id="49b02-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="49b02-125">Usamos Olá primeiro toomake terminal Olá alterações tooSSHDs arquivo de configuração e reiniciar o serviço SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="49b02-126">Usamos Olá tootest terminal segundo as alterações depois que o serviço Olá for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="49b02-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="49b02-127">Como desabilitar o SSH senhas e contar estritamente com chaves SSH, se as chaves SSH não estão corretas e fechar Olá conexão toohello VM, hello VM será permanentemente bloqueado e não será capaz de toologin tooit solicitá-la toobe excluído e recriado.</span><span class="sxs-lookup"><span data-stu-id="49b02-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="49b02-128">Desabilitar logons de senha</span><span class="sxs-lookup"><span data-stu-id="49b02-128">Disable password logins</span></span>

<span data-ttu-id="49b02-129">Olá toosecure de maneira mais rápida que a VM do Linux é toodisable logons de senha.</span><span class="sxs-lookup"><span data-stu-id="49b02-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="49b02-130">Quando os logons de senha são habilitados, bots rastreamento Olá web será iniciado imediatamente a tentar toobrute forçar senha de saudação de previsão para sua VM do Linux usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="49b02-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="49b02-131">Desabilitar completamente os logons de senha, permite Olá SSH server tooignore todas as tentativas de logon de senha.</span><span class="sxs-lookup"><span data-stu-id="49b02-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="49b02-132">Desabilitar logon pelo usuário de raiz de saudação</span><span class="sxs-lookup"><span data-stu-id="49b02-132">Disable login by hello root user</span></span>

<span data-ttu-id="49b02-133">Seguindo práticas recomendadas do Linux, hello `root` usuário nunca deve ser conectado via SSH ou usando `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="49b02-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="49b02-134">Todos os comandos que precisam de permissões no nível raiz devem sempre ser executados por meio de saudação `sudo` comando, que registra todas as ações de auditoria futuras.</span><span class="sxs-lookup"><span data-stu-id="49b02-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="49b02-135">Desabilitar Olá `root` usuário faça logon por meio do SSH é uma etapa práticas de segurança recomendada que garante que somente usuários autorizados podem tooSSH.</span><span class="sxs-lookup"><span data-stu-id="49b02-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="49b02-136">Lista de grupos permitidos</span><span class="sxs-lookup"><span data-stu-id="49b02-136">Allowed groups list</span></span>

<span data-ttu-id="49b02-137">O SSH oferece um método de restringir usuários e grupos que têm ou não permissão de logon via SSH.</span><span class="sxs-lookup"><span data-stu-id="49b02-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="49b02-138">Esse recurso usa listas tooapprove ou negar usuários e grupos específicos de fazer logon no.</span><span class="sxs-lookup"><span data-stu-id="49b02-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="49b02-139">Configuração Olá roda grupo toohello `AllowGroups` lista restringe logons aprovados em contas de usuário do SSH toojust que estão no grupo de roda hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="49b02-140">Lista de usuários permitidos</span><span class="sxs-lookup"><span data-stu-id="49b02-140">Allowed users list</span></span>

<span data-ttu-id="49b02-141">Restringindo os usuários toojust de logons SSH é uma maneira mais específica tooaccomplish Olá a mesma tarefa que `AllowGroups` é.</span><span class="sxs-lookup"><span data-stu-id="49b02-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="49b02-142">Desabilitar o protocolo SSH versão 1</span><span class="sxs-lookup"><span data-stu-id="49b02-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="49b02-143">O protocolo SSH versão 1 não é seguro e deve ser desabilitado.</span><span class="sxs-lookup"><span data-stu-id="49b02-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="49b02-144">O protocolo SSH versão 2 é a versão de atual de saudação que oferece um servidor de tooyour de tooSSH de maneira segura.</span><span class="sxs-lookup"><span data-stu-id="49b02-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="49b02-145">Desabilitar SSH versão 1 nega a todos os clientes SSH que estão tentando tooestablish em uma conexão com servidor SSH Olá com SSH versão 1.</span><span class="sxs-lookup"><span data-stu-id="49b02-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="49b02-146">Apenas conexões do SSH versão 2 são permitidas toonegotiate uma conexão com o servidor SSH hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="49b02-147">Bits de chave mínimos</span><span class="sxs-lookup"><span data-stu-id="49b02-147">Minimum key bits</span></span>

<span data-ttu-id="49b02-148">Seguindo práticas recomendadas de segurança, logons SSH de senha são desabilitados e somente as chaves de SSH são permitidas toobe usado tooauthenticate com o servidor SSH hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="49b02-149">Essas chaves SSH podem ser criadas usando chaves de comprimento diferente, medidas em bits.</span><span class="sxs-lookup"><span data-stu-id="49b02-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="49b02-150">Estados de chaves de 2048 bits de comprimento são intensidade da chave aceitável mínimo Olá de práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="49b02-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="49b02-151">Em teoria, chaves com menos de 2048 bits poderiam ser violadas.</span><span class="sxs-lookup"><span data-stu-id="49b02-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="49b02-152">Saudação de configuração `ServerKeyBits` muito`2048` permite todas as conexões usando chaves de 2048 bits ou superior e negar conexões de menos de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="49b02-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="49b02-153">Desconectar usuários ociosos</span><span class="sxs-lookup"><span data-stu-id="49b02-153">Disconnect idle users</span></span>

<span data-ttu-id="49b02-154">SSH tem usuários de toodisconnect de capacidade de saudação que têm conexões abertas que permaneceram ociosas por mais de um período definido de segundos.</span><span class="sxs-lookup"><span data-stu-id="49b02-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="49b02-155">Mantendo sessões abertas tooonly os usuários que estão ativos limita a exposição de saudação do hello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="49b02-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="49b02-156">Reiniciar o SSHD</span><span class="sxs-lookup"><span data-stu-id="49b02-156">Restart SSHD</span></span>

<span data-ttu-id="49b02-157">configurações de saudação tooenable no `/etc/ssh/sshd_config` reiniciar processo SSHD Olá que reinicia o servidor SSH hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="49b02-158">janela do terminal Olá usar toorestart Olá SSH server permanecem abertos sem perder a sessão aberta de SSH hello.</span><span class="sxs-lookup"><span data-stu-id="49b02-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="49b02-159">configurações de servidor SSH novo do tootest Olá use uma segunda janela de terminal ou a guia.  Usar uma saudação separada tootest terminal SSH conexão permite que você toogo voltar e fazer alterações adicionais toohello `/etc/ssh/sshd_config` no terminal primeiro hello, sem que está sendo bloqueado por uma alteração SSHD significativa.</span><span class="sxs-lookup"><span data-stu-id="49b02-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="49b02-160">No Redhat, Centos e Fedora</span><span class="sxs-lookup"><span data-stu-id="49b02-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="49b02-161">No Debian e Ubuntu</span><span class="sxs-lookup"><span data-stu-id="49b02-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="49b02-162">Redefinir o SSHD usando o acesso de redefinição do Azure</span><span class="sxs-lookup"><span data-stu-id="49b02-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="49b02-163">Se bloqueada de uma configuração de SSHD toohello quebra de alteração, você pode usar Olá extensão de acesso da máquina virtual do Azure tooreset Olá SSHD toohello back original do configuration.</span><span class="sxs-lookup"><span data-stu-id="49b02-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="49b02-164">Substitua os nomes de exemplo pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="49b02-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="49b02-165">Instalar o Fail2ban</span><span class="sxs-lookup"><span data-stu-id="49b02-165">Install Fail2ban</span></span>

<span data-ttu-id="49b02-166">É altamente recomendável tooinstall e instalação Olá código-fonte aberto aplicativo Fail2ban, quais blocos repetidas tentativas toologin tooyour VM Linux via SSH usando força bruta.</span><span class="sxs-lookup"><span data-stu-id="49b02-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="49b02-167">Logs de Fail2ban repetidos falha tentativas toologin via SSH e, em seguida, cria regras de firewall de endereço IP do hello tooblock são provenientes de tentativas de saudação.</span><span class="sxs-lookup"><span data-stu-id="49b02-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="49b02-168">Home page do Fail2ban</span><span class="sxs-lookup"><span data-stu-id="49b02-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="49b02-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49b02-169">Next Steps</span></span>

<span data-ttu-id="49b02-170">Agora que você configurou e bloqueado servidor SSH de saudação em sua VM Linux há práticas recomendadas de segurança adicionais, que você pode seguir.</span><span class="sxs-lookup"><span data-stu-id="49b02-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="49b02-171">Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="49b02-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="49b02-172">Criptografar discos em uma VM do Linux usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="49b02-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="49b02-173">Acesso e segurança em modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="49b02-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
