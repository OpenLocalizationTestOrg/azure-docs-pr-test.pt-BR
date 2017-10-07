---
title: as senhas SSH aaaDisable em sua VM Linux Configurando SSHD | Microsoft Docs
description: Proteja sua VM Linux no Azure desabilitando logons de senha para SSH.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="b1942-103">Desabilitar senhas SSH na sua VM Linux configurando o SSHD</span><span class="sxs-lookup"><span data-stu-id="b1942-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="b1942-104">Este artigo se concentra em como toolock segurança de logon de saudação da VM Linux.</span><span class="sxs-lookup"><span data-stu-id="b1942-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="b1942-105">Como Olá porta SSH 22 é aberto toohello world bots iniciar tentar toologin através de adivinhação de senhas.</span><span class="sxs-lookup"><span data-stu-id="b1942-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="b1942-106">O que vamos fazer neste artigo é desabilitar os logons de senha via SSH.</span><span class="sxs-lookup"><span data-stu-id="b1942-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="b1942-107">Removendo completamente a capacidade de saudação toouse senhas protegemos Olá VM Linux neste tipo de bruta de ataque de força.</span><span class="sxs-lookup"><span data-stu-id="b1942-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="b1942-108">Olá adicionado bônus é configuraremos Linux SSHD tooonly permitir logons através de chaves SSH públicas e privadas, sem dúvida Olá tooLinux de toologin de maneira mais segura.</span><span class="sxs-lookup"><span data-stu-id="b1942-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="b1942-109">combinações possíveis de saudação do mesmo exigiria a chave privada do tooguess Olá é grande e, portanto, não recomenda robôs do mesmo incomodar chaves SSH tootry toobrute force.</span><span class="sxs-lookup"><span data-stu-id="b1942-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="b1942-110">Metas</span><span class="sxs-lookup"><span data-stu-id="b1942-110">Goals</span></span>
* <span data-ttu-id="b1942-111">Configure SSHD toodisallow:</span><span class="sxs-lookup"><span data-stu-id="b1942-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="b1942-112">Logons de senha</span><span class="sxs-lookup"><span data-stu-id="b1942-112">Password logins</span></span>
  * <span data-ttu-id="b1942-113">Logon de usuário raiz</span><span class="sxs-lookup"><span data-stu-id="b1942-113">Root user login</span></span>
  * <span data-ttu-id="b1942-114">Autenticação de desafio/resposta</span><span class="sxs-lookup"><span data-stu-id="b1942-114">Challenge-response authentication</span></span>
* <span data-ttu-id="b1942-115">Configure SSHD tooallow:</span><span class="sxs-lookup"><span data-stu-id="b1942-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="b1942-116">Somente logons de chave SSH</span><span class="sxs-lookup"><span data-stu-id="b1942-116">only SSH key logins</span></span>
* <span data-ttu-id="b1942-117">Reiniciar o SSHD enquanto ainda estiver conectado</span><span class="sxs-lookup"><span data-stu-id="b1942-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="b1942-118">Configuração do teste Olá novo SSHD</span><span class="sxs-lookup"><span data-stu-id="b1942-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="b1942-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="b1942-119">Introduction</span></span>
[<span data-ttu-id="b1942-120">Definido por SSH</span><span class="sxs-lookup"><span data-stu-id="b1942-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="b1942-121">SSHD é hello SSH servidor que executa o hello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="b1942-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="b1942-122">O SSH é um cliente executado em um shell no seu MacBook ou estação de trabalho Linux.</span><span class="sxs-lookup"><span data-stu-id="b1942-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="b1942-123">SSH é também protocolo hello usado toosecure e criptografar a comunicação de saudação entre sua estação de trabalho e hello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="b1942-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="b1942-124">Para este artigo é muito importante tookeep um logon tooyour VM Linux aberta para Olá todo percorrer.</span><span class="sxs-lookup"><span data-stu-id="b1942-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="b1942-125">Por esse motivo, será aberta dois terminais e SSH toohello VM do Linux de ambos.</span><span class="sxs-lookup"><span data-stu-id="b1942-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="b1942-126">Vamos usar Olá primeiro toomake terminal Olá alterações tooSSHDs arquivo de configuração e reiniciar o serviço SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="b1942-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="b1942-127">Usaremos Olá tootest terminal segundo as alterações depois que o serviço Olá for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="b1942-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="b1942-128">Como desabilitar o SSH senhas e contar estritamente com chaves SSH, se as chaves SSH não estão corretas e fechar Olá conexão toohello VM, hello VM será permanentemente bloqueado e não será capaz de toologin tooit solicitá-la toobe excluído e recriado.</span><span class="sxs-lookup"><span data-stu-id="b1942-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1942-129">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b1942-129">Prerequisites</span></span>
* [<span data-ttu-id="b1942-130">Criar chaves SSH no Linux e Mac para VMs do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="b1942-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="b1942-131">Conta do Azure</span><span class="sxs-lookup"><span data-stu-id="b1942-131">Azure account</span></span>
  * [<span data-ttu-id="b1942-132">assinatura de avaliação gratuita</span><span class="sxs-lookup"><span data-stu-id="b1942-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="b1942-133">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b1942-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="b1942-134">VM Linux em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="b1942-134">Linux VM running on azure</span></span>
* <span data-ttu-id="b1942-135">Par de chaves pública e privada SSH em `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="b1942-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="b1942-136">A chave pública SSH no `~/.ssh/authorized_keys` em Olá VM do Linux</span><span class="sxs-lookup"><span data-stu-id="b1942-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="b1942-137">Direitos do sudo no hello VM</span><span class="sxs-lookup"><span data-stu-id="b1942-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="b1942-138">Porta 22 aberta</span><span class="sxs-lookup"><span data-stu-id="b1942-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b1942-139">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="b1942-139">Quick Commands</span></span>
<span data-ttu-id="b1942-140">*Administradores de Linux experientes que querem apenas a versão TLDR Olá comece aqui.  Para todos os outros que quer Olá explicações detalhadas e passo a passo ignore esta seção.*</span><span class="sxs-lookup"><span data-stu-id="b1942-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="b1942-141">Edite o arquivo de configuração de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b1942-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="b1942-142">Reinicie o serviço SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="b1942-142">Restart hello SSHD service.</span></span> <span data-ttu-id="b1942-143">Em distribuições com base em Debian:</span><span class="sxs-lookup"><span data-stu-id="b1942-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="b1942-144">Em distribuições com base em Red Hat:</span><span class="sxs-lookup"><span data-stu-id="b1942-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="b1942-145">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="b1942-145">Detailed Walk Through</span></span>
<span data-ttu-id="b1942-146">Logon toohello VM do Linux no terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="b1942-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="b1942-147">Logon toohello VM do Linux em 2 de terminal (T2).</span><span class="sxs-lookup"><span data-stu-id="b1942-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="b1942-148">Em T2, vamos arquivo de configuração tooedit Olá SSHD.</span><span class="sxs-lookup"><span data-stu-id="b1942-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="b1942-149">Aqui vamos Editar Olá configurações toodisable senhas e habilitar os logons de chave SSH.</span><span class="sxs-lookup"><span data-stu-id="b1942-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="b1942-150">Há muitas configurações neste arquivo que você deve pesquisar e alterar toomake Linux & SSH como segura, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="b1942-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="b1942-151">Desabilitar logons de senha</span><span class="sxs-lookup"><span data-stu-id="b1942-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="b1942-152">Habilitar a autenticação de chave pública</span><span class="sxs-lookup"><span data-stu-id="b1942-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="b1942-153">Desabilitar logon de raiz</span><span class="sxs-lookup"><span data-stu-id="b1942-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="b1942-154">Desabilitar autenticação de desafio/resposta</span><span class="sxs-lookup"><span data-stu-id="b1942-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="b1942-155">Reiniciar o SSHD</span><span class="sxs-lookup"><span data-stu-id="b1942-155">Restart SSHD</span></span>
<span data-ttu-id="b1942-156">No shell de saudação T1, verifique se que você ainda está conectado.</span><span class="sxs-lookup"><span data-stu-id="b1942-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="b1942-157">Isso é essencial para que você não seja bloqueado na VM se suas chaves SSH não estiverem corretas, uma vez que as senhas agora estão desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="b1942-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="b1942-158">Se qualquer configuração estiverem incorreta em sua VM do Linux que você pode usar T1 toofix sshd_config que ainda serão registrados no e SSH irá manter uma conexão hello atividade durante a saudação service SSHD reinicie.</span><span class="sxs-lookup"><span data-stu-id="b1942-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="b1942-159">No T2, execute:</span><span class="sxs-lookup"><span data-stu-id="b1942-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="b1942-160">Em Olá família Debian</span><span class="sxs-lookup"><span data-stu-id="b1942-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="b1942-161">Em Olá RedHat família</span><span class="sxs-lookup"><span data-stu-id="b1942-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="b1942-162">As senhas agora estão desabilitadas na sua VM, protegendo-a contra tentativas de logon de senha por força bruta.</span><span class="sxs-lookup"><span data-stu-id="b1942-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="b1942-163">Com apenas SSH chaves permitidas será capaz de toologin muito mais rápido e seguro.</span><span class="sxs-lookup"><span data-stu-id="b1942-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

