---
title: "área de trabalho remota de aaaUse tooa VM do Linux no Azure | Microsoft Docs"
description: "Saiba como tooinstall e configurar a área de trabalho remota (xrdp) tooconnect tooa VM do Linux no Azure usando as ferramentas gráficas"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="d4f4f-103">Instalar e configurar a área de trabalho remota tooconnect tooa VM do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="d4f4f-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="d4f4f-104">Máquinas virtuais de Linux (VMs) no Azure geralmente são gerenciadas da linha de comando de saudação usando uma conexão SSH (secure shell).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="d4f4f-105">Quando novos tooLinux, ou para cenários de solução de problemas rápidos, uso de saudação da área de trabalho remota pode ser mais fácil.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="d4f4f-106">Este artigo detalhes como tooinstall e configurar um ambiente de desktop ([xfce](https://www.xfce.org)) e a área de trabalho remota ([xrdp](http://www.xrdp.org)) para sua VM do Linux usando o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d4f4f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4f4f-107">Prerequisites</span></span>
<span data-ttu-id="d4f4f-108">Este artigo exige uma VM do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="d4f4f-109">Se você precisar toocreate uma máquina virtual, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="d4f4f-110">Olá [2.0 do CLI do Azure](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d4f4f-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="d4f4f-111">Olá [portal do Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d4f4f-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="d4f4f-112">Instalar um ambiente de área de trabalho em sua VM do Linux</span><span class="sxs-lookup"><span data-stu-id="d4f4f-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="d4f4f-113">A maioria das VMs do Linux no Azure não tem um ambiente de área de trabalho instalado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="d4f4f-114">As VMs do Linux são gerenciadas normalmente usando conexões SSH, em vez de um ambiente de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="d4f4f-115">Há vários ambientes de área de trabalho no Linux para sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="d4f4f-116">Dependendo de sua escolha de ambiente de desktop, pode consumir um too2 GB de espaço em disco e levar 5 tooinstall de minutos too10 e configure todos os pacotes de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="d4f4f-117">Olá, exemplo a seguir instala lightweight Olá [xfce4](https://www.xfce.org/) ambiente de área de trabalho em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="d4f4f-118">Comandos para outras distribuições variam ligeiramente (use `yum` tooinstall no Red Hat Enterprise Linux e configurar apropriado `selinux` regras ou use `zypper` tooinstall no SUSE, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="d4f4f-119">Primeiro, SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="d4f4f-120">exemplo a seguir Hello conecta toohello VM denominada *myvm.westus.cloudapp.azure.com* com nome de usuário de saudação do *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="d4f4f-121">Se você estiver usando o Windows e precisa de mais informações sobre como usar SSH, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="d4f4f-122">Em seguida, instale o xfce usando `apt` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="d4f4f-123">Instalar e configurar um servidor de área de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="d4f4f-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="d4f4f-124">Agora que você tem um ambiente de desktop instalado, configure um toolisten de serviços de área de trabalho remota para conexões de entrada.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="d4f4f-125">[xrdp](http://xrdp.org) é um servidor RDP (Protocolo de Área de Trabalho Remota) de código-fonte aberto que está disponível na maioria das distribuições Linux e funciona bem com xfce.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="d4f4f-126">Instale o xrdp em sua VM do Ubuntu da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="d4f4f-127">Conte-xrdp toouse o ambiente de desktop quando você iniciar a sessão.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="d4f4f-128">Configure xrdp toouse xfce como seu ambiente de área de trabalho da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="d4f4f-129">Reinicie o serviço de xrdp de Olá Olá alterações tootake efeito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="d4f4f-130">Definir a senha da conta de usuário local</span><span class="sxs-lookup"><span data-stu-id="d4f4f-130">Set a local user account password</span></span>
<span data-ttu-id="d4f4f-131">Se você tiver criado uma senha para sua conta de usuário durante a criação de sua VM, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="d4f4f-132">Se você só usa autenticação de chave SSH e não tem uma senha de conta local definido, especifique uma senha antes de usar xrdp toolog tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="d4f4f-133">O xrdp não pode aceitar chaves SSH para autenticação.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="d4f4f-134">Olá, exemplo a seguir especifica uma senha para a conta de usuário Olá *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="d4f4f-135">Especificando uma senha não atualizar seus logons de senha SSHD configuração toopermit se no momento não.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="d4f4f-136">De uma perspectiva de segurança, você pode desejar tooconnect tooyour VM com um túnel SSH usando a autenticação baseada em chave e, em seguida, conecte-se tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="d4f4f-137">Nesse caso, ignore Olá após a etapa na criação de um segurança grupo regra tooallow remote desktop tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="d4f4f-138">Criar uma regra de Grupo de Segurança de Rede para tráfego de Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="d4f4f-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="d4f4f-139">tooreach de tráfego de área de trabalho remota tooallow sua VM do Linux, uma regra de grupo de segurança de rede precisa toobe criado que permita o TCP em tooreach de porta 3389 sua VM.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="d4f4f-140">Para saber mais sobre grupos de segurança de rede, confira [O que é um Grupo de Segurança de Rede?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d4f4f-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="d4f4f-141">Você também pode [use Olá toocreate portal do Azure uma regra de grupo de segurança de rede](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d4f4f-142">Olá, exemplos a seguir criam uma regra de grupo de segurança de rede com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) chamado *myNetworkSecurityGroupRule* muito*permitir* tráfego em *tcp* porta *3389*.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="d4f4f-143">Conectar-se a sua VM do Linux com um cliente de Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="d4f4f-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="d4f4f-144">Abra seu cliente local de área de trabalho remota e conecte-se toohello endereço IP ou nome DNS de sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="d4f4f-145">Insira Olá nome de usuário e senha para a conta de usuário de saudação na sua VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Conecte-se tooxrdp usando seu cliente de área de trabalho remota](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="d4f4f-147">Depois de autenticar, ambiente de desktop saudação xfce serão carregadas e parecer semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![Ambiente de área de trabalho xfce por meio de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="d4f4f-149">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d4f4f-149">Troubleshoot</span></span>
<span data-ttu-id="d4f4f-150">Se você não conseguir conectar tooyour VM do Linux usando um cliente de área de trabalho remota, use `netstat` em tooverify sua VM do Linux que a VM está escutando conexões RDP da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="d4f4f-151">Olá mostrado no exemplo a seguir Olá VM escutando na porta TCP 3389 conforme o esperado:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="d4f4f-152">Se o serviço de xrdp Olá não estiver escutando, em uma VM Ubuntu reinicie serviço de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="d4f4f-153">Examine logs */var/log*Thug na sua VM Ubuntu indicações de como o serviço de saudação toowhy pode não estar respondendo.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="d4f4f-154">Você também pode monitorar o syslog Olá durante um tooview de tentativa de conexão de área de trabalho remota erros:</span><span class="sxs-lookup"><span data-stu-id="d4f4f-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="d4f4f-155">Outras distribuições do Linux como Red Hat Enterprise Linux e SUSE podem ter serviços toorestart de diferentes maneiras e tooreview de locais de arquivo de log alternativo.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="d4f4f-156">Se você não receber nenhuma resposta no seu cliente de área de trabalho remota e não vir todos os eventos no log do sistema hello, esse comportamento indica que o tráfego de área de trabalho remoto não pode alcançar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="d4f4f-157">Revise seu tooensure regras do grupo da segurança de rede que você tenha uma regra toopermit TCP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="d4f4f-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="d4f4f-158">Para saber mais, veja [Solucionar problemas de conectividade do aplicativo](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d4f4f-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4f4f-159">Next steps</span></span>
<span data-ttu-id="d4f4f-160">Para saber mais sobre como criar e usar chaves SSH com VMs do Linux, veja [Criar chaves SSH para VMs do Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="d4f4f-161">Para obter informações sobre como usar SSH do Windows, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d4f4f-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

