---
title: "problemas de conexão de SSH aaaTroubleshoot tooan VM do Azure | Microsoft Docs"
description: "Como tootroubleshoot problemas, como 'conexão SSH com falha' ou 'conexão SSH recusada' para uma VM do Azure executando o Linux."
keywords: "conexão ssh recusada, erro de ssh, ssh do azure, falha de conexão SSH"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="1c78c-104">Solucionar problemas de conexões de SSH tooan VM do Linux do Azure que falhar, erros, ou foi recusada</span><span class="sxs-lookup"><span data-stu-id="1c78c-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="1c78c-105">Há vários motivos que você encontrar erros de Secure Shell (SSH), falhas de conexão SSH, ou SSH é recusada quando você tentar tooconnect tooa Linux VM (máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="1c78c-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="1c78c-106">Este artigo ajuda você a localizar e problemas de saudação correto.</span><span class="sxs-lookup"><span data-stu-id="1c78c-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="1c78c-107">Você pode usar o hello portal do Azure, CLI do Azure ou extensão de acesso de VM para Linux tootroubleshoot e resolver problemas de conexão.</span><span class="sxs-lookup"><span data-stu-id="1c78c-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1c78c-108">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1c78c-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1c78c-109">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c78c-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="1c78c-110">Vá toohello [site de suporte do Azure](http://azure.microsoft.com/support/options/) e selecione **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="1c78c-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="1c78c-111">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="1c78c-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="1c78c-112">Etapas rápidas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="1c78c-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="1c78c-113">Depois de cada etapa de solução de problemas, tente reconectar-se toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1c78c-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="1c78c-114">Redefina a configuração de SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c78c-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="1c78c-115">Redefina credenciais de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="1c78c-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="1c78c-116">Verifique se Olá [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) regras permitem o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="1c78c-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="1c78c-117">Certifique-se de que o grupo de segurança de rede existe uma regra de tráfego SSH toopermit (por padrão, a porta TCP 22).</span><span class="sxs-lookup"><span data-stu-id="1c78c-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="1c78c-118">Você não pode usar o mapeamento/redirecionamento de porta sem usar um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="1c78c-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="1c78c-119">Verificar Olá [integridade de recursos da VM](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c78c-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="1c78c-120">Certifique-se de que Olá VM relatórios como íntegro.</span><span class="sxs-lookup"><span data-stu-id="1c78c-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="1c78c-121">Se você tiver habilitado o diagnóstico de inicialização, verifique se Olá VM não está relatando erros de inicialização nos logs de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c78c-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="1c78c-122">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1c78c-122">Restart hello VM.</span></span>
6. <span data-ttu-id="1c78c-123">Reimplante Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1c78c-123">Redeploy hello VM.</span></span>

<span data-ttu-id="1c78c-124">Caso você precise de etapas e explicações mais detalhadas para solução de problemas, continue lendo.</span><span class="sxs-lookup"><span data-stu-id="1c78c-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="1c78c-125">Problemas de conexão métodos disponíveis tootroubleshoot SSH</span><span class="sxs-lookup"><span data-stu-id="1c78c-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="1c78c-126">Você pode redefinir as credenciais ou configuração de SSH usando um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c78c-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="1c78c-127">[Portal do Azure](#use-the-azure-portal) - ótimo se você precisar tooquickly redefinir a configuração de SSH hello ou chave SSH e você não tiver instaladas as ferramentas do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1c78c-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="1c78c-128">[2.0 do CLI do Azure](#use-the-azure-cli-20) - se você já estiver na linha de comando hello, rapidamente configuração de SSH Olá redefinição ou credenciais.</span><span class="sxs-lookup"><span data-stu-id="1c78c-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="1c78c-129">Você também pode usar o hello [1.0 da CLI do Azure](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="1c78c-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="1c78c-130">[Extensão VMAccessForLinux do Azure](#use-the-vmaccess-extension) - crie e reutilizar json definição arquivos tooreset Olá SSH configuração ou credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="1c78c-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="1c78c-131">Depois de cada etapa de solução de problemas, tente conectar-se tooyour VM novamente.</span><span class="sxs-lookup"><span data-stu-id="1c78c-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="1c78c-132">Se você ainda não é possível se conectar, tente Olá próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="1c78c-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="1c78c-133">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-133">Use hello Azure portal</span></span>
<span data-ttu-id="1c78c-134">Olá portal do Azure fornece uma saudação tooreset de maneira rápida as credenciais de usuário ou a configuração de SSH sem instalar as ferramentas no computador local.</span><span class="sxs-lookup"><span data-stu-id="1c78c-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="1c78c-135">Selecione a VM em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c78c-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="1c78c-136">Role para baixo toohello **suporte + solução de problemas** seção e selecione **Redefinir senha** como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c78c-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Redefinir a configuração de SSH ou credenciais no hello portal do Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="1c78c-138">Redefinir a configuração de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="1c78c-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="1c78c-139">Como uma primeira etapa, selecione `Reset configuration only` de saudação **modo** menu suspenso como na saudação anterior a captura de tela, e clique em Olá **redefinir** botão.</span><span class="sxs-lookup"><span data-stu-id="1c78c-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="1c78c-140">Após concluir esta ação, tente tooaccess sua VM novamente.</span><span class="sxs-lookup"><span data-stu-id="1c78c-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1c78c-141">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="1c78c-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1c78c-142">credenciais de saudação tooreset de um usuário existente, selecione `Reset SSH public key` ou `Reset password` de saudação **modo** menu suspenso como Olá anterior a captura de tela.</span><span class="sxs-lookup"><span data-stu-id="1c78c-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="1c78c-143">Especificar nome de usuário hello e uma chave SSH ou nova senha e clique em Olá **redefinir** botão.</span><span class="sxs-lookup"><span data-stu-id="1c78c-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="1c78c-144">Você também pode criar um usuário com privilégios de sudo no hello VM nesse menu.</span><span class="sxs-lookup"><span data-stu-id="1c78c-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="1c78c-145">Insira um novo nome de usuário e a senha associada ou a chave SSH e, em seguida, clique em Olá **redefinir** botão.</span><span class="sxs-lookup"><span data-stu-id="1c78c-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="1c78c-146">Use Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="1c78c-147">Se você ainda não fez isso, instale hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1c78c-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1c78c-148">Se você criou e carregar uma imagem de disco Linux personalizada, verifique se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="1c78c-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="1c78c-149">Para VMs criadas usando imagens da galeria, é possível que essa extensão de acesso já esteja instalada e configurada para você.</span><span class="sxs-lookup"><span data-stu-id="1c78c-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="1c78c-150">Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="1c78c-150">Reset SSH configuration</span></span>
<span data-ttu-id="1c78c-151">Você pode inicialmente tente redefinindo Olá SSH configuração toodefault valores e o servidor SSH de hello está sendo reiniciado no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1c78c-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="1c78c-152">Observe que isso não altera o nome de conta de usuário hello, a senha ou as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="1c78c-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="1c78c-153">Olá exemplo a seguir usa [az vm usuário Redefinir-ssh](/cli/azure/vm/user#reset-ssh) tooreset configuração de SSH Olá em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-154">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1c78c-155">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="1c78c-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1c78c-156">Olá exemplo a seguir usa [atualização de usuário de vm az](/cli/azure/vm/user#update) tooreset Olá credenciais para `myUsername` toohello valor especificado em `myPassword`, em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-157">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="1c78c-158">Se usando a autenticação de chave SSH, você pode redefinir a chave SSH Olá para um determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="1c78c-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="1c78c-159">Hello exemplo a seguir usa **az vm acesso de usuário do linux de conjunto** tooupdate Olá SSH chave armazenada em `~/.ssh/id_rsa.pub` de usuário Olá chamado `myUsername`, em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-160">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="1c78c-161">Usar a extensão VMAccess Olá</span><span class="sxs-lookup"><span data-stu-id="1c78c-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="1c78c-162">Olá extensão de acesso de VM para Linux lê um arquivo json que define ações toocarry-out. Essas ações incluem redefinir o SSHD, redefinir uma chave SSH ou adicionar um usuário.</span><span class="sxs-lookup"><span data-stu-id="1c78c-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="1c78c-163">Você ainda usar Olá toocall da CLI do Azure Olá extensão VMAccess, mas você pode reutilizar arquivos json de saudação entre várias VMs, se desejado.</span><span class="sxs-lookup"><span data-stu-id="1c78c-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="1c78c-164">Essa abordagem permite que você toocreate um repositório de arquivos de json que pode ser chamado para determinado cenários.</span><span class="sxs-lookup"><span data-stu-id="1c78c-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="1c78c-165">Redefinir SSHD</span><span class="sxs-lookup"><span data-stu-id="1c78c-165">Reset SSHD</span></span>
<span data-ttu-id="1c78c-166">Crie um arquivo chamado `settings.json` com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c78c-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="1c78c-167">Usando Olá CLI do Azure, você, em seguida, chamar hello `VMAccessForLinux` extensão tooreset sua conexão SSHD especificando o arquivo json.</span><span class="sxs-lookup"><span data-stu-id="1c78c-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="1c78c-168">Olá exemplo a seguir usa [conjunto de extensão de vm az](/cli/azure/vm/extension#set) tooreset SSHD em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-169">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1c78c-170">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="1c78c-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1c78c-171">Se SSHD aparecer toofunction corretamente, você pode redefinir credenciais de saudação para um usuário doador.</span><span class="sxs-lookup"><span data-stu-id="1c78c-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="1c78c-172">senha de saudação tooreset para um usuário, crie um arquivo chamado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="1c78c-173">Olá, exemplo a seguir redefine credenciais Olá para `myUsername` toohello valor especificado em `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="1c78c-174">Digite hello seguintes linhas no seu `settings.json` de arquivo, usando seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="1c78c-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="1c78c-175">Ou tooreset Olá chave SSH de um usuário, primeiro crie um arquivo chamado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="1c78c-176">Olá, exemplo a seguir redefine credenciais Olá para `myUsername` toohello valor especificado em `myPassword`, em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-177">Digite hello seguintes linhas no seu `settings.json` de arquivo, usando seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="1c78c-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="1c78c-178">Após criar o arquivo json, use saudação do hello CLI do Azure toocall `VMAccessForLinux` tooreset extensão credenciais de usuário SSH, especificando o arquivo json.</span><span class="sxs-lookup"><span data-stu-id="1c78c-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="1c78c-179">Olá, exemplo a seguir redefine credenciais em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-180">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="1c78c-181">Use Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="1c78c-182">Se você ainda não o fez, [instalar Olá 1.0 da CLI do Azure e conecte-se tooyour assinatura do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1c78c-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="1c78c-183">Certifique-se de que você esteja usando o modo Resource Manager da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="1c78c-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1c78c-184">Se você criou e carregar uma imagem de disco Linux personalizada, verifique se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="1c78c-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="1c78c-185">Para VMs criadas usando imagens da galeria, é possível que essa extensão de acesso já esteja instalada e configurada para você.</span><span class="sxs-lookup"><span data-stu-id="1c78c-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="1c78c-186">Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="1c78c-186">Reset SSH configuration</span></span>
<span data-ttu-id="1c78c-187">configuração de SSHD Olá propriamente dita pode estar configurado incorretamente ou Olá serviço encontrou um erro.</span><span class="sxs-lookup"><span data-stu-id="1c78c-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="1c78c-188">Você pode redefinir SSHD toomake-se de que a configuração de SSH Olá propriamente dita é válida.</span><span class="sxs-lookup"><span data-stu-id="1c78c-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="1c78c-189">Redefinir SSHD deve ser Olá primeira etapa para solução de problemas que você tomar.</span><span class="sxs-lookup"><span data-stu-id="1c78c-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="1c78c-190">Olá, exemplo a seguir redefine SSHD em uma VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-191">Use seus próprios nomes de grupo de recursos e de VM, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1c78c-192">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="1c78c-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1c78c-193">Se SSHD aparecer toofunction corretamente, você pode redefinir a senha de saudação para um usuário doador.</span><span class="sxs-lookup"><span data-stu-id="1c78c-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="1c78c-194">Olá, exemplo a seguir redefine credenciais Olá para `myUsername` toohello valor especificado em `myPassword`, em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-195">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="1c78c-196">Se usando a autenticação de chave SSH, você pode redefinir a chave SSH Olá para um determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="1c78c-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="1c78c-197">Olá atualizações de exemplo a seguir Olá chave SSH armazenada em `~/.ssh/id_rsa.pub` de usuário Olá chamado `myUsername`, em Olá VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-198">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="1c78c-199">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="1c78c-199">Restart a VM</span></span>
<span data-ttu-id="1c78c-200">Se você redefinir as credenciais de usuário e a configuração de SSH hello ou encontrou um erro ao fazer isso, você pode tentar reiniciar Olá VM tooaddress subjacente problemas de computação.</span><span class="sxs-lookup"><span data-stu-id="1c78c-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="1c78c-201">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-201">Azure portal</span></span>
<span data-ttu-id="1c78c-202">toorestart uma VM usando hello Azure selecione portal, a saudação VM e clique em **reiniciar** botão como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c78c-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Reiniciar uma VM em Olá portal do Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="1c78c-204">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-204">Azure CLI 1.0</span></span>
<span data-ttu-id="1c78c-205">Olá reinicializações de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-206">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="1c78c-207">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1c78c-207">Azure CLI 2.0</span></span>
<span data-ttu-id="1c78c-208">Olá exemplo a seguir usa [reinicialização de vm az](/cli/azure/vm#restart) toorestart Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-209">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="1c78c-210">Reimplantar uma VM</span><span class="sxs-lookup"><span data-stu-id="1c78c-210">Redeploy a VM</span></span>
<span data-ttu-id="1c78c-211">Você pode reutilizar um nó de tooanother VM no Azure, que pode corrigir problemas de rede subjacentes.</span><span class="sxs-lookup"><span data-stu-id="1c78c-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="1c78c-212">Para obter informações sobre como reimplantar uma VM, consulte [reimplantar a máquina virtual toonew nó do Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c78c-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="1c78c-213">Após concluir esta operação, disco efêmera, os dados serão perdidos e endereços IP dinâmicos que estão associados com a máquina virtual de saudação serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="1c78c-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="1c78c-214">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-214">Azure portal</span></span>
<span data-ttu-id="1c78c-215">tooredeploy uma VM usando hello Azure selecione portal, a VM e role para baixo toohello **suporte + solução de problemas** seção.</span><span class="sxs-lookup"><span data-stu-id="1c78c-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="1c78c-216">Clique em Olá **reimplantar** botão como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c78c-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Reimplantar uma VM em Olá portal do Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="1c78c-218">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="1c78c-218">Azure CLI 1.0</span></span>
<span data-ttu-id="1c78c-219">Olá reimplanta de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-220">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="1c78c-221">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1c78c-221">Azure CLI 2.0</span></span>
<span data-ttu-id="1c78c-222">Olá uso do exemplo a seguir [reimplantação da vm de az](/cli/azure/vm#redeploy) tooredeploy Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1c78c-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1c78c-223">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c78c-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="1c78c-224">Máquinas virtuais criadas usando o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="1c78c-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="1c78c-225">Repita essas etapas tooresolve hello mais comuns SSH conexão falhas para VMs que foram criados usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="1c78c-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="1c78c-226">Depois de cada etapa, tente reconectar-se toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1c78c-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="1c78c-227">Redefinir o acesso remoto de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c78c-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1c78c-228">Na Olá portal do Azure, selecione a VM e clique em Olá **redefinir remoto...**  botão.</span><span class="sxs-lookup"><span data-stu-id="1c78c-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="1c78c-229">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1c78c-229">Restart hello VM.</span></span> <span data-ttu-id="1c78c-230">Em Olá [portal do Azure](https://portal.azure.com), selecione a VM e clique Olá **reiniciar** botão.</span><span class="sxs-lookup"><span data-stu-id="1c78c-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="1c78c-231">Reimplante Olá VM tooa novo nó do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c78c-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="1c78c-232">Para obter informações sobre como tooredeploy uma VM, consulte [reimplantar a máquina virtual toonew nó do Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c78c-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="1c78c-233">Após concluir esta operação, disco efêmera, os dados serão perdidos e endereços IP dinâmicos que estão associados com a máquina virtual de saudação serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="1c78c-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="1c78c-234">Siga as instruções de saudação em [como tooreset uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:</span><span class="sxs-lookup"><span data-stu-id="1c78c-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="1c78c-235">Olá redefinição da senha ou chave SSH.</span><span class="sxs-lookup"><span data-stu-id="1c78c-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="1c78c-236">Criar uma nova conta de usuário *sudo*.</span><span class="sxs-lookup"><span data-stu-id="1c78c-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="1c78c-237">Redefina a configuração de SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c78c-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="1c78c-238">Verifique a integridade dos recursos da VM Olá para quaisquer problemas de plataforma.</span><span class="sxs-lookup"><span data-stu-id="1c78c-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="1c78c-239">Selecione sua VM e role para baixo para **Configurações** > **Verificar Integridade**.</span><span class="sxs-lookup"><span data-stu-id="1c78c-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c78c-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1c78c-240">Additional resources</span></span>
* <span data-ttu-id="1c78c-241">Se você ainda não é possível tooSSH tooyour VM depois de seguir Olá após etapas, consulte [obter as etapas de solução de problemas mais](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview adicional etapas tooresolve seu problema.</span><span class="sxs-lookup"><span data-stu-id="1c78c-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="1c78c-242">Para obter mais informações sobre como solucionar problemas de acesso do aplicativo, consulte [aplicativos de tooan acesso de solução de problemas em execução em uma máquina virtual do Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1c78c-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="1c78c-243">Para obter mais informações sobre como solucionar problemas de máquinas virtuais que foram criadas usando o modelo de implantação clássico hello, consulte [como tooreset uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c78c-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

