---
title: "aaaAzure início rápido - criar VM Portal | Microsoft Docs"
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
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="fcca6-103">Criar uma máquina virtual Linux com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fcca6-103">Create a Linux virtual machine with hello Azure portal</span></span>

<span data-ttu-id="fcca6-104">Máquinas virtuais do Azure podem ser criadas por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcca6-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="fcca6-105">Esse método fornece uma interface do usuário baseada em navegador para a criação e configuração de máquinas virtuais e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fcca6-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="fcca6-106">Este guia de início rápido percorre criando uma máquina virtual e instalar um servidor Web no hello VM.</span><span class="sxs-lookup"><span data-stu-id="fcca6-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="fcca6-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="fcca6-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="fcca6-108">Criar o par de chaves SSH</span><span class="sxs-lookup"><span data-stu-id="fcca6-108">Create SSH key pair</span></span>

<span data-ttu-id="fcca6-109">É necessário um toocomplete do par de chaves de SSH esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="fcca6-109">You need an SSH key pair toocomplete this quick start.</span></span> <span data-ttu-id="fcca6-110">Se você já tiver um par de chave SSH, essa etapa pode ser ignorada.</span><span class="sxs-lookup"><span data-stu-id="fcca6-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="fcca6-111">De um shell Bash, execute este comando e siga Olá na tela de instruções.</span><span class="sxs-lookup"><span data-stu-id="fcca6-111">From a Bash shell, run this command and follow hello on-screen directions.</span></span> <span data-ttu-id="fcca6-112">saída do comando Olá inclui nome de arquivo de saudação do arquivo de chave pública hello.</span><span class="sxs-lookup"><span data-stu-id="fcca6-112">hello command output includes hello file name of hello public key file.</span></span> <span data-ttu-id="fcca6-113">Copie o conteúdo de saudação da área de transferência de toohello do arquivo de chave pública de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcca6-113">Copy hello contents of hello public key file toohello clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a><span data-ttu-id="fcca6-114">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="fcca6-114">Log in tooAzure</span></span> 

<span data-ttu-id="fcca6-115">Faça logon em toohello portal do Azure em http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="fcca6-115">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="fcca6-116">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fcca6-116">Create virtual machine</span></span>

1. <span data-ttu-id="fcca6-117">Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcca6-117">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="fcca6-118">Selecione **Computação** e, em seguida, selecione **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="fcca6-119">Insira informações da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fcca6-119">Enter hello virtual machine information.</span></span> <span data-ttu-id="fcca6-120">Para **Tipo de autenticação**, selecione **Chave pública SSH**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="fcca6-121">Ao colar na sua chave pública SSH, tome cuidado tooremove qualquer espaço em branco à esquerda ou à direita.</span><span class="sxs-lookup"><span data-stu-id="fcca6-121">When pasting in your SSH public key, take care tooremove any leading or trailing white space.</span></span> <span data-ttu-id="fcca6-122">Ao concluir, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-122">When complete, click **OK**.</span></span>

    ![Insira as informações básicas sobre sua VM na folha portal Olá](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="fcca6-124">Selecione um tamanho para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="fcca6-124">Select a size for hello VM.</span></span> <span data-ttu-id="fcca6-125">toosee mais tamanhos, selecione **exibir todos os** ou alterar Olá **suporte para o tipo de disco** filtro.</span><span class="sxs-lookup"><span data-stu-id="fcca6-125">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![A captura de tela que mostra os tamanhos da VM](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="fcca6-127">Na folha de configurações hello, lembre-Olá padrões e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-127">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="fcca6-128">Na página de resumo de saudação, clique em **Okey** toostart implantação da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fcca6-128">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="fcca6-129">Olá VM será fixado toohello painel do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcca6-129">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="fcca6-130">Após a conclusão da implantação hello, folha de resumo de VM Olá é aberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fcca6-130">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="fcca6-131">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="fcca6-131">Connect toovirtual machine</span></span>

<span data-ttu-id="fcca6-132">Crie uma conexão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcca6-132">Create an SSH connection with hello virtual machine.</span></span>

1. <span data-ttu-id="fcca6-133">Clique em Olá **conectar** botão na folha de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcca6-133">Click hello **Connect** button on hello virtual machine blade.</span></span> <span data-ttu-id="fcca6-134">Olá conectar botão exibe uma cadeia de caracteres de conexão SSH que pode ser usado tooconnect toohello virtual máquina.</span><span class="sxs-lookup"><span data-stu-id="fcca6-134">hello connect button displays an SSH connection string that can be used tooconnect toohello virtual machine.</span></span>

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="fcca6-136">Comando a seguir de execução Olá toocreate uma sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="fcca6-136">Run hello following command toocreate an SSH session.</span></span> <span data-ttu-id="fcca6-137">Substitua cadeia de caracteres de conexão Olá Olá que você copiado da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcca6-137">Replace hello connection string with hello one you copied from hello Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="fcca6-138">Instalar o NGINX</span><span class="sxs-lookup"><span data-stu-id="fcca6-138">Install NGINX</span></span>

<span data-ttu-id="fcca6-139">Use a seguir de saudação bash origens do pacote do script tooupdate e instala pacote NGINX mais recente de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcca6-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="fcca6-140">Quando terminar, saia Olá SSH sessão e retornar propriedades da VM Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcca6-140">When done, exit hello SSH session and return hello VM properties in hello Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="fcca6-141">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="fcca6-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="fcca6-142">Um Grupo de Segurança de Rede (NSG) protege o tráfego de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="fcca6-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="fcca6-143">Quando uma máquina virtual é criada a partir Olá portal do Azure, uma regra de entrada é criada na porta 22 para conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="fcca6-143">When a VM is created from hello Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="fcca6-144">Como essa VM hospeda um servidor Web, uma regra NSG necessita toobe criado para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="fcca6-144">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="fcca6-145">Na máquina virtual de Olá, clique em nome de saudação do hello **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-145">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="fcca6-146">Selecione Olá **grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-146">Select hello **network security group**.</span></span> <span data-ttu-id="fcca6-147">Olá NSG pode ser identificado usando Olá **tipo** coluna.</span><span class="sxs-lookup"><span data-stu-id="fcca6-147">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="fcca6-148">No menu esquerdo hello, em configurações, clique em **regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-148">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="fcca6-149">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-149">Click on **Add**.</span></span>
5. <span data-ttu-id="fcca6-150">Em **Nome**, digite **http**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-150">In **Name**, type **http**.</span></span> <span data-ttu-id="fcca6-151">Certifique-se de **intervalo de portas** é definir too80 e **ação** está definido muito**permitir**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-151">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="fcca6-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-152">Click **OK**.</span></span>


## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="fcca6-153">Página de boas-vindas do modo de exibição Olá NGINX</span><span class="sxs-lookup"><span data-stu-id="fcca6-153">View hello NGINX welcome page</span></span>

<span data-ttu-id="fcca6-154">Com NGINX instalado e a porta 80 abra tooyour VM, Olá servidorweb agora pode ser acessado de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="fcca6-154">With NGINX installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="fcca6-155">Abra um navegador da web e digite o endereço IP público de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="fcca6-155">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="fcca6-156">endereço IP público de saudação pode ser encontrado na folha VM Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcca6-156">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="fcca6-158">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="fcca6-158">Clean up resources</span></span>

<span data-ttu-id="fcca6-159">Quando não é mais necessário, exclua o grupo de recursos de saudação, máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fcca6-159">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="fcca6-160">toodo, portanto, selecione o grupo de recursos de saudação da folha de máquina virtual hello e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-160">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcca6-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fcca6-161">Next steps</span></span>

<span data-ttu-id="fcca6-162">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="fcca6-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="fcca6-163">toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="fcca6-163">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fcca6-164">Tutoriais de máquina virtual do Linux Azure</span><span class="sxs-lookup"><span data-stu-id="fcca6-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
