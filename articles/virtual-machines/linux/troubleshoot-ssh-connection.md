---
title: "Solucionar problemas de conexão SSH com uma VM do Azure | Microsoft Docs"
description: "Como solucionar problemas como 'conexão SSH com falha' ou 'conexão SSH recusada' para uma VM do Azure executando Linux."
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
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="6b994-104">Solucionar problemas em conexões SSH com uma VM Linux do Azure que falha, apresenta erro ou é recusada</span><span class="sxs-lookup"><span data-stu-id="6b994-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="6b994-105">Há vários motivos pelos quais você pode encontrar erros de SSH (Secure Shell), falhas na conexão SSH ou então o SSH é recusado ao tentar se conectar a uma VM (máquina virtual) Linux.</span><span class="sxs-lookup"><span data-stu-id="6b994-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="6b994-106">Este artigo ajuda você a localizar e corrigir os problemas.</span><span class="sxs-lookup"><span data-stu-id="6b994-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="6b994-107">Você pode usar o portal do Azure, a CLI do Azure ou a Extensão de Acesso da VM para Linux para solucionar problemas de conexão.</span><span class="sxs-lookup"><span data-stu-id="6b994-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="6b994-108">Caso precise de mais ajuda a qualquer momento neste artigo, entre em contato com os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="6b994-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="6b994-109">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b994-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="6b994-110">Vá para o [site de suporte do Azure](http://azure.microsoft.com/support/options/) e selecione **Obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="6b994-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="6b994-111">Para saber mais sobre como usar o suporte do Azure, leia as [Perguntas frequentes sobre o suporte do Microsoft Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="6b994-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="6b994-112">Etapas rápidas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="6b994-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="6b994-113">Após cada etapa de solução de problemas, tente se reconectar à VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="6b994-114">Redefinir a configuração de SSH.</span><span class="sxs-lookup"><span data-stu-id="6b994-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="6b994-115">Redefinir as credenciais para o usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="6b994-116">Verifique se as regras do [Grupo de Segurança de Rede](../../virtual-network/virtual-networks-nsg.md) permitem o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="6b994-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="6b994-117">Certifique-se de que existe uma regra de Grupo de Segurança de Rede para permitir o tráfego SSH (por padrão, a porta TCP 22).</span><span class="sxs-lookup"><span data-stu-id="6b994-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="6b994-118">Você não pode usar o mapeamento/redirecionamento de porta sem usar um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="6b994-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="6b994-119">Verifique a [Integridade do Recurso de VM](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b994-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="6b994-120">Certifique-se de que a VM é relatada como íntegra.</span><span class="sxs-lookup"><span data-stu-id="6b994-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="6b994-121">Se você tiver habilitado o diagnóstico de inicialização, verifique se a VM não está relatando erros de inicialização nos logs.</span><span class="sxs-lookup"><span data-stu-id="6b994-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="6b994-122">Reinicie a VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-122">Restart the VM.</span></span>
6. <span data-ttu-id="6b994-123">Reimplante a VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-123">Redeploy the VM.</span></span>

<span data-ttu-id="6b994-124">Caso você precise de etapas e explicações mais detalhadas para solução de problemas, continue lendo.</span><span class="sxs-lookup"><span data-stu-id="6b994-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="6b994-125">Métodos disponíveis para solucionar problemas de conexão SSH</span><span class="sxs-lookup"><span data-stu-id="6b994-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="6b994-126">Você pode redefinir as credenciais ou configuração de SSH usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="6b994-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="6b994-127">[Portal do Azure](#use-the-azure-portal) – excelente se você precisar redefinir rapidamente as credenciais de usuário ou configurações de SSH ou chave SSH e não tiver as Ferramentas do Azure instaladas.</span><span class="sxs-lookup"><span data-stu-id="6b994-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="6b994-128">[CLI 2.0 do Azure](#use-the-azure-cli-20) – se você já estiver na linha de comando, redefina rapidamente as credenciais ou a configuração de SSH.</span><span class="sxs-lookup"><span data-stu-id="6b994-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="6b994-129">Também é possível usar a [CLI do Azure 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="6b994-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="6b994-130">[Extensão VMAccessForLinux do Azure](#use-the-vmaccess-extension) – criar e reutilizar os arquivos de definição json para redefinir as credenciais de usuário ou configuração do SSH.</span><span class="sxs-lookup"><span data-stu-id="6b994-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="6b994-131">Após cada etapa de solução de problemas, tente se conectar à VM novamente.</span><span class="sxs-lookup"><span data-stu-id="6b994-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="6b994-132">Caso você ainda não consiga conectar, tente a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="6b994-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="6b994-133">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-133">Use the Azure portal</span></span>
<span data-ttu-id="6b994-134">O portal do Azure fornece uma maneira rápida para redefinir as credenciais de usuário ou configuração do SSH sem instalar as ferramentas no computador local.</span><span class="sxs-lookup"><span data-stu-id="6b994-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="6b994-135">No Portal do Azure, selecione sua VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="6b994-136">Role para baixo até a seção **Suporte + Solução de problemas** e selecione **Redefinir senha** como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b994-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Redefinir a configuração de SSH ou credenciais no Portal do Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="6b994-138">Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="6b994-138">Reset the SSH configuration</span></span>
<span data-ttu-id="6b994-139">Como uma primeira etapa, selecione `Reset configuration only` do menu suspenso **Modo** como na captura de tela anterior, depois clique no botão **Redefinir**.</span><span class="sxs-lookup"><span data-stu-id="6b994-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="6b994-140">Quando essa ação for concluída, tente acessar sua VM novamente.</span><span class="sxs-lookup"><span data-stu-id="6b994-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="6b994-141">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="6b994-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="6b994-142">Para redefinir as credenciais de um usuário existente, selecione `Reset SSH public key` ou `Reset password` do menu suspenso **Modo** como na captura de tela anterior.</span><span class="sxs-lookup"><span data-stu-id="6b994-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="6b994-143">Especifique o nome de usuário e uma chave SSH ou a nova senha, depois clique no botão **Redefinir**.</span><span class="sxs-lookup"><span data-stu-id="6b994-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="6b994-144">Você também pode criar um usuário com privilégios sudo na VM nesse menu.</span><span class="sxs-lookup"><span data-stu-id="6b994-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="6b994-145">Insira um novo nome de usuário e senha associada ou chave SSH e, em seguida, clique no botão **Redefinir**.</span><span class="sxs-lookup"><span data-stu-id="6b994-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="6b994-146">Usar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="6b994-147">Se você ainda não fez isso, instale a versão mais recente da [CLI 2.0 do Azure](/cli/azure/install-az-cli2) e faça logon na conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6b994-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6b994-148">Se você criar e carregar uma imagem de disco Linux personalizada, verifique se o [Agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="6b994-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="6b994-149">Para VMs criadas usando imagens da galeria, é possível que essa extensão de acesso já esteja instalada e configurada para você.</span><span class="sxs-lookup"><span data-stu-id="6b994-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="6b994-150">Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="6b994-150">Reset SSH configuration</span></span>
<span data-ttu-id="6b994-151">Inicialmente, você pode tentar redefinir a configuração de SSH para valores padrão e a reinicialização do servidor SSH na VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="6b994-152">Observe que isso não muda o nome, a senha ou as chaves SSH da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="6b994-153">O exemplo a seguir usa [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) para redefinir a configuração de SSH na VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-154">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="6b994-155">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="6b994-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="6b994-156">O exemplo a seguir usa [az vm user update](/cli/azure/vm/user#update) para redefinir as credenciais de `myUsername` para o valor especificado em `myPassword`, na VM chamada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-157">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="6b994-158">Se usar autenticação de chave SSH, você poderá redefinir a chave SSH para um determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="6b994-159">O exemplo a seguir usa **az vm access set-linux-user** para atualizar a chave SSH armazenada em `~/.ssh/id_rsa.pub` para o usuário chamado `myUsername`, na VM chamada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-160">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="6b994-161">Usar a extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="6b994-161">Use the VMAccess extension</span></span>
<span data-ttu-id="6b994-162">A Extensão de Acesso de VM para Linux lê um arquivo json que define as ações a executar. Essas ações incluem redefinir o SSHD, redefinir uma chave SSH ou adicionar um usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="6b994-163">Você ainda usa a CLI do Azure para chamar a extensão VMAccess, mas você pode reutilizar os arquivos json em várias VMs, se desejado.</span><span class="sxs-lookup"><span data-stu-id="6b994-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="6b994-164">Essa abordagem permite que você crie um repositório de arquivos json que podem então ser chamados para determinado cenários.</span><span class="sxs-lookup"><span data-stu-id="6b994-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="6b994-165">Redefinir SSHD</span><span class="sxs-lookup"><span data-stu-id="6b994-165">Reset SSHD</span></span>
<span data-ttu-id="6b994-166">Crie um arquivo chamado `settings.json` com o conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b994-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="6b994-167">Usando a CLI do Azure, você chama em seguida a extensão `VMAccessForLinux` para redefinir sua conexão SSHD ao especificar o arquivo json.</span><span class="sxs-lookup"><span data-stu-id="6b994-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="6b994-168">O exemplo a seguir usa [az vm extension set](/cli/azure/vm/extension#set) para redefinir SSHD na VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-169">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="6b994-170">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="6b994-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="6b994-171">Se o SSHD parecer funcionar corretamente, você poderá redefinir as credenciais para um determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="6b994-172">Para redefinir a senha de um usuário, crie um arquivo chamado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="6b994-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="6b994-173">O exemplo a seguir redefine as credenciais para `myUsername` para o valor especificado em `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="6b994-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="6b994-174">Digite as seguintes linhas no seu arquivo de `settings.json`, usando seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="6b994-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="6b994-175">Ou, para redefinir a chave SSH para um usuário, primeiro crie um arquivo chamado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="6b994-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="6b994-176">O exemplo a seguir redefine as credenciais para `myUsername` para o valor especificado em `myPassword`, na VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-177">Digite as seguintes linhas no seu arquivo de `settings.json`, usando seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="6b994-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="6b994-178">Depois de criar o arquivo json, use a CLI do Azure para chamar a extensão `VMAccessForLinux` para redefinir suas credenciais de usuário SSH, especificando seu arquivo json.</span><span class="sxs-lookup"><span data-stu-id="6b994-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="6b994-179">O exemplo a seguir redefine as credenciais na VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-180">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="6b994-181">Usar a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="6b994-182">Se você ainda não fez isso, [instale a CLI 1.0 do Azure e conecte-se à sua assinatura do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6b994-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="6b994-183">Certifique-se de que você esteja usando o modo Resource Manager da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6b994-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="6b994-184">Se você criar e carregar uma imagem de disco Linux personalizada, verifique se o [Agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="6b994-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="6b994-185">Para VMs criadas usando imagens da galeria, é possível que essa extensão de acesso já esteja instalada e configurada para você.</span><span class="sxs-lookup"><span data-stu-id="6b994-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="6b994-186">Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="6b994-186">Reset SSH configuration</span></span>
<span data-ttu-id="6b994-187">A configuração SSHD em si pode estar definida incorretamente ou o serviço encontrou um erro.</span><span class="sxs-lookup"><span data-stu-id="6b994-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="6b994-188">Você pode redefinir o SSHD para garantir que a configuração de SSH em si é válida.</span><span class="sxs-lookup"><span data-stu-id="6b994-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="6b994-189">Redefinir SSHD deve ser a primeira etapa de solução de problemas para você realizar.</span><span class="sxs-lookup"><span data-stu-id="6b994-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="6b994-190">O exemplo a seguir redefine o SSHD na VM denominada `myVM` no grupo de recursos chamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="6b994-191">Use seus próprios nomes de grupo de recursos e de VM, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="6b994-192">Redefinir credenciais SSH para um usuário</span><span class="sxs-lookup"><span data-stu-id="6b994-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="6b994-193">Se o SSHD parecer funcionar corretamente, você poderá redefinir a senha para um determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="6b994-194">O exemplo a seguir redefine as credenciais para `myUsername` para o valor especificado em `myPassword`, na VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-195">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="6b994-196">Se usar autenticação de chave SSH, você poderá redefinir a chave SSH para um determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="6b994-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="6b994-197">O exemplo a seguir atualiza a chave SSH armazenada em `~/.ssh/id_rsa.pub` para o usuário chamado `myUsername`, na VM denominada `myVM` em `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="6b994-198">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="6b994-199">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="6b994-199">Restart a VM</span></span>
<span data-ttu-id="6b994-200">Se você tiver redefinido as credenciais de usuário e a configuração do SSH ou encontrado um erro ao fazer isso, você poderá tentar reiniciar a VM para solucionar problemas de computação subjacentes.</span><span class="sxs-lookup"><span data-stu-id="6b994-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6b994-201">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-201">Azure portal</span></span>
<span data-ttu-id="6b994-202">Para reiniciar uma VM usando o Portal do Azure, selecione sua VM e clique no botão **Reiniciar** como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b994-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Reiniciar uma VM no Portal do Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="6b994-204">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-204">Azure CLI 1.0</span></span>
<span data-ttu-id="6b994-205">O exemplo a seguir reinicia a VM denominada `myVM` no grupo de recursos denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="6b994-206">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="6b994-207">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-207">Azure CLI 2.0</span></span>
<span data-ttu-id="6b994-208">O exemplo a seguir usa [az vm restart](/cli/azure/vm#restart) para reiniciar a VM chamada `myVM` no grupo de recursos chamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="6b994-209">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="6b994-210">Reimplantar uma VM</span><span class="sxs-lookup"><span data-stu-id="6b994-210">Redeploy a VM</span></span>
<span data-ttu-id="6b994-211">Você pode reimplantar uma VM para outro nó no Azure, o que pode corrigir possíveis problemas de rede subjacentes.</span><span class="sxs-lookup"><span data-stu-id="6b994-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="6b994-212">Para obter informações sobre como reimplantar uma VM, consulte [Reimplantar Máquina Virtual em um novo nó do Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b994-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="6b994-213">Após a conclusão dessa operação, os dados de disco efêmeros serão perdidos e os endereços IP dinâmicos associados à máquina virtual serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="6b994-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="6b994-214">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-214">Azure portal</span></span>
<span data-ttu-id="6b994-215">Para reimplantar uma VM usando o Portal do Azure, selecione sua VM e role para baixo até a seção **Suporte + Solução de Problemas**.</span><span class="sxs-lookup"><span data-stu-id="6b994-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="6b994-216">Clique no botão **Reimplantar** como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b994-216">Click the **Redeploy** button as in the following example:</span></span>

![Reimplantar a VM no Portal do Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="6b994-218">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-218">Azure CLI 1.0</span></span>
<span data-ttu-id="6b994-219">O exemplo a seguir reimplanta a VM denominada `myVM` no grupo de recursos denominado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="6b994-220">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="6b994-221">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6b994-221">Azure CLI 2.0</span></span>
<span data-ttu-id="6b994-222">O exemplo a seguir usa [az vm redeploy](/cli/azure/vm#redeploy) para reimplantar a VM chamada `myVM` no grupo de recursos chamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="6b994-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="6b994-223">Use seus próprios valores, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6b994-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="6b994-224">VMs criadas com o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="6b994-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="6b994-225">Experimente essas etapas para resolver as falhas de conexão SSH mais comuns em VMs criadas usando o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="6b994-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="6b994-226">Após cada etapa, tente se reconectar à VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="6b994-227">Redefina o acesso remoto no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b994-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6b994-228">No Portal do Azure, selecione sua VM e clique no botão **Redefinir Remoto...**.</span><span class="sxs-lookup"><span data-stu-id="6b994-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="6b994-229">Reinicie a VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-229">Restart the VM.</span></span> <span data-ttu-id="6b994-230">No [Portal do Azure](https://portal.azure.com), selecione sua VM e clique no botão **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="6b994-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="6b994-231">Reimplante a VM em um novo nó do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b994-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="6b994-232">Para obter informações sobre como reimplantar uma VM, veja [Reimplantar Máquina Virtual em um novo nó do Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b994-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="6b994-233">Após a conclusão dessa operação, os dados de disco efêmeros serão perdidos e os endereços IP dinâmicos associados à máquina virtual serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="6b994-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="6b994-234">Siga as instruções em [Como redefinir uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:</span><span class="sxs-lookup"><span data-stu-id="6b994-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="6b994-235">Redefinir a senha ou a chave SSH.</span><span class="sxs-lookup"><span data-stu-id="6b994-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="6b994-236">Criar uma nova conta de usuário *sudo*.</span><span class="sxs-lookup"><span data-stu-id="6b994-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="6b994-237">Redefinir a configuração de SSH.</span><span class="sxs-lookup"><span data-stu-id="6b994-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="6b994-238">Verifique se há problemas de plataforma na integridade do recurso da VM.</span><span class="sxs-lookup"><span data-stu-id="6b994-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="6b994-239">Selecione sua VM e role para baixo para **Configurações** > **Verificar Integridade**.</span><span class="sxs-lookup"><span data-stu-id="6b994-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b994-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6b994-240">Additional resources</span></span>
* <span data-ttu-id="6b994-241">Se ainda não puder se conectar com SSH à VM após seguir essas etapas, veja [etapas de solução de problemas mais detalhadas](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para examinar etapas adicionais para resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="6b994-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="6b994-242">Para obter mais informações sobre como solucionar problemas de acesso do aplicativo, consulte [Solucionar problemas de acesso a um aplicativo executado em uma máquina virtual do Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6b994-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="6b994-243">Para obter mais informações sobre como solucionar problemas de máquinas virtuais que foram criadas usando o modelo de implantação clássico, consulte [Como redefinir uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b994-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

