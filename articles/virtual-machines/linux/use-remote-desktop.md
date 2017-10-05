---
title: "Usar a Área de Trabalho Remota para uma VM do Linux no Azure | Microsoft Docs"
description: "Saiba como instalar e configurar a Área de Trabalho Remota (xrdp) para conectar-se a uma VM do Linux no Azure usando ferramentas gráficas"
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
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="707b8-103">Instalar e configurar a Área de Trabalho Remota para conectar-se uma VM do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="707b8-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="707b8-104">As VMs (máquinas virtuais) do Linux no Azure são normalmente gerenciadas a partir da linha de comando usando uma conexão SSH (secure shell).</span><span class="sxs-lookup"><span data-stu-id="707b8-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="707b8-105">Para novos usuários Linux, ou para cenários de solução rápida de problemas, o uso da área de trabalho remota pode ser mais fácil.</span><span class="sxs-lookup"><span data-stu-id="707b8-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="707b8-106">Este artigo fornece detalhes sobre como instalar e configurar um ambiente de área de trabalho ([xfce](https://www.xfce.org)) e área de trabalho remota ([xrdp](http://www.xrdp.org)) para sua VM do Linux usando o modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="707b8-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="707b8-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="707b8-107">Prerequisites</span></span>
<span data-ttu-id="707b8-108">Este artigo exige uma VM do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="707b8-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="707b8-109">Se você precisar criar uma VM, use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="707b8-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="707b8-110">A [CLI 2.0 do Azure](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="707b8-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="707b8-111">O [Portal do Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="707b8-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="707b8-112">Instalar um ambiente de área de trabalho em sua VM do Linux</span><span class="sxs-lookup"><span data-stu-id="707b8-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="707b8-113">A maioria das VMs do Linux no Azure não tem um ambiente de área de trabalho instalado por padrão.</span><span class="sxs-lookup"><span data-stu-id="707b8-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="707b8-114">As VMs do Linux são gerenciadas normalmente usando conexões SSH, em vez de um ambiente de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="707b8-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="707b8-115">Há vários ambientes de área de trabalho no Linux para sua escolha.</span><span class="sxs-lookup"><span data-stu-id="707b8-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="707b8-116">Dependendo de sua escolha de ambiente de área de trabalho, ele pode consumir de um a 2 GB de espaço em disco e demorar de cinco a 10 minutos para instalar e configurar todos os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="707b8-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="707b8-117">O exemplo a seguir instala o ambiente de área de trabalho leve [xfce4](https://www.xfce.org/) em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="707b8-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="707b8-118">Os comandos para outras distribuições variam um pouco (use `yum` para instalar no Red Hat Enterprise Linux e configurar as regras `selinux` apropriadas ou use `zypper` para instalar no SUSE, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="707b8-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="707b8-119">Primeiro, SSH para sua VM.</span><span class="sxs-lookup"><span data-stu-id="707b8-119">First, SSH to your VM.</span></span> <span data-ttu-id="707b8-120">O seguinte exemplo conecta-se à VM chamada *myvm.westus.cloudapp.azure.com* com o nome de usuário *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="707b8-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="707b8-121">Se você estiver usando o Windows e precisar de mais informações sobre como usar o SSH, veja [Como usar chaves do SSH com o Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="707b8-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="707b8-122">Em seguida, instale o xfce usando `apt` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="707b8-123">Instalar e configurar um servidor de área de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="707b8-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="707b8-124">Agora que você tem um ambiente de área de trabalho instalado, configure um serviço de área de trabalho remoto para escutar as conexões de entrada.</span><span class="sxs-lookup"><span data-stu-id="707b8-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="707b8-125">[xrdp](http://xrdp.org) é um servidor RDP (Protocolo de Área de Trabalho Remota) de código-fonte aberto que está disponível na maioria das distribuições Linux e funciona bem com xfce.</span><span class="sxs-lookup"><span data-stu-id="707b8-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="707b8-126">Instale o xrdp em sua VM do Ubuntu da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="707b8-127">Diga ao xrdp o ambiente de área de trabalho a ser usado ao iniciar a sessão.</span><span class="sxs-lookup"><span data-stu-id="707b8-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="707b8-128">Configure xrdp para usar xfce como seu ambiente de área de trabalho da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="707b8-129">Reinicie o serviço xrdp para que as alterações entrem em vigor da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="707b8-130">Definir a senha da conta de usuário local</span><span class="sxs-lookup"><span data-stu-id="707b8-130">Set a local user account password</span></span>
<span data-ttu-id="707b8-131">Se você tiver criado uma senha para sua conta de usuário durante a criação de sua VM, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="707b8-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="707b8-132">Se você usar apenas a autenticação de chave SSH e não tiver uma senha de conta local definida, especifique uma senha antes de usar o xrdp para fazer logon em sua VM.</span><span class="sxs-lookup"><span data-stu-id="707b8-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="707b8-133">O xrdp não pode aceitar chaves SSH para autenticação.</span><span class="sxs-lookup"><span data-stu-id="707b8-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="707b8-134">O seguinte exemplo especifica uma senha para a conta de usuário *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="707b8-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="707b8-135">A especificação de uma senha não atualiza a configuração de SSHD para permitir logons de senha, caso ela não permita no momento.</span><span class="sxs-lookup"><span data-stu-id="707b8-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="707b8-136">De uma perspectiva de segurança, convém conectar-se à sua VM com um túnel SSH usando a autenticação baseada em chave e, depois, conectar-se ao xrdp.</span><span class="sxs-lookup"><span data-stu-id="707b8-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="707b8-137">Nesse caso, ignore a etapa a seguir sobre a criação de uma regra de grupo de segurança de rede para permitir o tráfego de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="707b8-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="707b8-138">Criar uma regra de Grupo de Segurança de Rede para tráfego de Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="707b8-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="707b8-139">Para permitir que o tráfego da Área de Trabalho Remota alcance sua VM do Linux, é necessário criar uma regra de grupo de segurança de rede que permite ao TCP na porta 3389 acessar sua VM.</span><span class="sxs-lookup"><span data-stu-id="707b8-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="707b8-140">Para saber mais sobre grupos de segurança de rede, confira [O que é um Grupo de Segurança de Rede?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="707b8-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="707b8-141">Você também pode [usar o Portal do Azure para criar uma regra de grupo de segurança de rede](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="707b8-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="707b8-142">Os exemplos a seguir criam uma regra de grupo de segurança de rede com [az network nsg rule create](/cli/azure/network/nsg/rule#create) chamada *myNetworkSecurityGroupRule* para *permitir* o tráfego na porta *TCP* *3389*.</span><span class="sxs-lookup"><span data-stu-id="707b8-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="707b8-143">Conectar-se a sua VM do Linux com um cliente de Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="707b8-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="707b8-144">Abra o cliente da área de trabalho remota local e conecte-se ao endereço IP ou nome DNS de sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="707b8-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="707b8-145">Insira o nome de usuário e a senha da conta de usuário em sua VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-145">Enter the username and password for the user account on your VM as follows:</span></span>

![Conectar-se ao xrdp usando seu cliente de Área de Trabalho Remota](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="707b8-147">Após a autenticação, o ambiente de área de trabalho xfce carregará e será semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="707b8-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![Ambiente de área de trabalho xfce por meio de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="707b8-149">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="707b8-149">Troubleshoot</span></span>
<span data-ttu-id="707b8-150">Se você não puder se conectar à sua VM do Linux usando um cliente de Área de Trabalho Remota, use `netstat` em sua VM do Linux para verificar se sua VM está escutando conexões RDP da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="707b8-151">O exemplo a seguir mostra a VM escutando na porta TCP 3389, conforme o esperado:</span><span class="sxs-lookup"><span data-stu-id="707b8-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="707b8-152">Se o serviço xrdp não estiver escutando, em uma VM do Ubuntu, reinicie o serviço da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="707b8-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="707b8-153">Examine os logs */var/log*Thug na VM Ubuntu para obter indicações sobre o motivo de o serviço não estar respondendo.</span><span class="sxs-lookup"><span data-stu-id="707b8-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="707b8-154">Você também pode monitorar o syslog durante uma tentativa de conexão de área de trabalho remota para exibir quaisquer erros:</span><span class="sxs-lookup"><span data-stu-id="707b8-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="707b8-155">Outras distribuições do Linux como Red Hat Enterprise Linux e SUSE podem ter maneiras diferentes de reiniciar serviços e locais alternativos de arquivos de log para examinar.</span><span class="sxs-lookup"><span data-stu-id="707b8-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="707b8-156">Se você não receber nenhuma resposta em seu cliente de área de trabalho remota e não ver quaisquer eventos no log do sistema, esse comportamento indicará que o tráfego da área de trabalho remota não consegue alcançar a VM.</span><span class="sxs-lookup"><span data-stu-id="707b8-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="707b8-157">Examine suas regras de grupo de segurança de rede para garantir que você tenha uma regra para permitir o TCP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="707b8-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="707b8-158">Para saber mais, veja [Solucionar problemas de conectividade do aplicativo](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="707b8-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="707b8-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="707b8-159">Next steps</span></span>
<span data-ttu-id="707b8-160">Para saber mais sobre como criar e usar chaves SSH com VMs do Linux, veja [Criar chaves SSH para VMs do Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="707b8-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="707b8-161">Para saber mais sobre como usar o SSH do Windows, veja [Como usar chaves SSH com o Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="707b8-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

