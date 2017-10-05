---
title: "Início Rápido do Azure – Criar Portal da VM | Microsoft Docs"
description: "Início Rápido do Azure – Criar Portal da VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d009020e86fdfed6a45b5b63b9664c623bcb1843
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="c4ad2-103">Criar uma máquina virtual Linux com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4ad2-103">Create a Linux virtual machine with the Azure portal</span></span>

<span data-ttu-id="c4ad2-104">Máquinas virtuais do Azure podem ser criadas por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="c4ad2-105">Esse método fornece uma interface do usuário baseada em navegador para a criação e configuração de máquinas virtuais e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="c4ad2-106">Esse Início Rápido percorre a criação de uma máquina virtual e a instalação de um servidor Web na VM.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="c4ad2-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="c4ad2-108">Criar o par de chaves SSH</span><span class="sxs-lookup"><span data-stu-id="c4ad2-108">Create SSH key pair</span></span>

<span data-ttu-id="c4ad2-109">Você precisa de um par de chaves SSH para concluir este início rápido.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-109">You need an SSH key pair to complete this quick start.</span></span> <span data-ttu-id="c4ad2-110">Se você já tiver um par de chave SSH, essa etapa pode ser ignorada.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="c4ad2-111">Em um shell Bash, execute este comando e siga as orientações da tela.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-111">From a Bash shell, run this command and follow the on-screen directions.</span></span> <span data-ttu-id="c4ad2-112">A saída do comando inclui o nome do arquivo da chave pública.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-112">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="c4ad2-113">Copie o conteúdo do arquivo da chave público para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-113">Copy the contents of the public key file to the clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a><span data-ttu-id="c4ad2-114">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="c4ad2-114">Log in to Azure</span></span> 

<span data-ttu-id="c4ad2-115">Faça logon no Portal do Azure em http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-115">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="c4ad2-116">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4ad2-116">Create virtual machine</span></span>

1. <span data-ttu-id="c4ad2-117">Clique no botão **Novo** no canto superior esquerdo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-117">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="c4ad2-118">Selecione **Computação** e, em seguida, selecione **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="c4ad2-119">Insira as informações da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-119">Enter the virtual machine information.</span></span> <span data-ttu-id="c4ad2-120">Para **Tipo de autenticação**, selecione **Chave pública SSH**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="c4ad2-121">Ao colar na sua chave pública SSH, tome cuidado para remover qualquer espaço em branco à direita ou à esquerda.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-121">When pasting in your SSH public key, take care to remove any leading or trailing white space.</span></span> <span data-ttu-id="c4ad2-122">Ao concluir, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-122">When complete, click **OK**.</span></span>

    ![Insira as informações básicas sobre sua VM na folha do portal](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="c4ad2-124">Selecione um tamanho para a VM.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-124">Select a size for the VM.</span></span> <span data-ttu-id="c4ad2-125">Para ver mais tamanhos, selecione **Exibir todos os** ou altere o filtro **Tipo de disco com suporte**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-125">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![A captura de tela que mostra os tamanhos da VM](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="c4ad2-127">Na folha de configurações, mantenha os padrões e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-127">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="c4ad2-128">Na página de resumo, clique em **OK** para iniciar a implantação da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-128">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="c4ad2-129">A VM será fixada ao painel do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-129">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="c4ad2-130">Depois que a implantação for concluída, a folha de resumo da VM abre automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-130">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="c4ad2-131">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4ad2-131">Connect to virtual machine</span></span>

<span data-ttu-id="c4ad2-132">Crie uma conexão SSH com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-132">Create an SSH connection with the virtual machine.</span></span>

1. <span data-ttu-id="c4ad2-133">Clique no botão **Conectar** na folha da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-133">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="c4ad2-134">O botão conectar exibe uma cadeia de conexão SSH que pode ser usada para conectar-se à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-134">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span></span>

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="c4ad2-136">Execute o seguinte comando para criar uma sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-136">Run the following command to create an SSH session.</span></span> <span data-ttu-id="c4ad2-137">Substitua a cadeia de conexão com aquela que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-137">Replace the connection string with the one you copied from the Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="c4ad2-138">Instalar o NGINX</span><span class="sxs-lookup"><span data-stu-id="c4ad2-138">Install NGINX</span></span>

<span data-ttu-id="c4ad2-139">Use o seguinte script bash para atualizar fontes de pacote e instalar o pacote mais recente do NGINX.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="c4ad2-140">Quando terminar, saia da sessão SSH e retorne as propriedades da VM no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-140">When done, exit the SSH session and return the VM properties in the Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="c4ad2-141">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="c4ad2-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="c4ad2-142">Um Grupo de Segurança de Rede (NSG) protege o tráfego de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="c4ad2-143">Quando uma VM é criada no portal do Azure, uma regra de entrada é criada na porta 22 para conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-143">When a VM is created from the Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="c4ad2-144">Como essa VM hospeda um servidor Web, uma regra NSG precisa ser criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-144">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="c4ad2-145">Na máquina virtual, clique no nome do **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-145">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="c4ad2-146">Selecione **o grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-146">Select the **network security group**.</span></span> <span data-ttu-id="c4ad2-147">O NSG pode ser identificado usando a coluna **Tipo**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-147">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="c4ad2-148">No menu à esquerda, em configurações, clique em **Regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-148">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="c4ad2-149">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-149">Click on **Add**.</span></span>
5. <span data-ttu-id="c4ad2-150">Em **Nome**, digite **http**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-150">In **Name**, type **http**.</span></span> <span data-ttu-id="c4ad2-151">Verifique se o **Intervalo de portas** está definido para 80 e a **Ação** está definida para **Permitir**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-151">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="c4ad2-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-152">Click **OK**.</span></span>


## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="c4ad2-153">Exibir a página de boas-vindas do NGINX</span><span class="sxs-lookup"><span data-stu-id="c4ad2-153">View the NGINX welcome page</span></span>

<span data-ttu-id="c4ad2-154">Com o NGINX instalado e a porta 80 aberta para a sua VM, o servidor Web agora pode ser acessada da Internet.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-154">With NGINX installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="c4ad2-155">Abra o navegador Web e insira o endereço IP público da VM.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-155">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="c4ad2-156">O endereço IP público pode ser encontrado na folha da VM no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-156">The public IP address can be found on the VM blade in the Azure portal.</span></span>

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="c4ad2-158">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="c4ad2-158">Clean up resources</span></span>

<span data-ttu-id="c4ad2-159">Quando o grupo de recursos, a máquina virtual e todos os recursos relacionados não forem mais necessários, exclua-os.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-159">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c4ad2-160">Para fazer isso, selecione o grupo de recursos na folha da máquina virtual e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-160">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4ad2-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4ad2-161">Next steps</span></span>

<span data-ttu-id="c4ad2-162">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="c4ad2-163">Para saber mais sobre máquinas virtuais do Azure, continue o tutorial para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c4ad2-163">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4ad2-164">Tutoriais de máquina virtual do Linux Azure</span><span class="sxs-lookup"><span data-stu-id="c4ad2-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
