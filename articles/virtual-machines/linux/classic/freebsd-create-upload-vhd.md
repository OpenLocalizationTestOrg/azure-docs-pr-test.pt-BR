---
title: Criar e carregar uma imagem de VM FreeBSD | Microsoft Docs
description: "Saiba como criar e carregar um VHD (disco rígido virtual) que contenha um sistema operacional FreeBSD para criar uma máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="99736-103">Criar e carregar um VHD FreeBSD para o Azure</span><span class="sxs-lookup"><span data-stu-id="99736-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="99736-104">Este artigo mostra como criar e carregar um VHD (disco rígido virtual) que contenha um sistema operacional FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="99736-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="99736-105">Depois de carregá-lo, você pode usá-lo como sua própria imagem para criar uma VM (máquina virtual) no Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="99736-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="99736-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="99736-107">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="99736-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="99736-108">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="99736-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="99736-109">Para obter informações sobre como carregar um VHD usando o modelo do Resource Manager, veja [aqui](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99736-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99736-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99736-110">Prerequisites</span></span>
<span data-ttu-id="99736-111">Este artigo pressupõe que você tenha os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="99736-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="99736-112">**Uma assinatura do Azure**– Se não tiver uma conta, você poderá criar uma em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="99736-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="99736-113">Se você tiver uma assinatura do MSDN, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="99736-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="99736-114">Caso contrário, saiba como [criar uma conta de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99736-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="99736-115">**Ferramentas do Azure PowerShell**– O módulo do Azure PowerShell deve estar instalado e configurado para que a assinatura do Azure possa ser usada.</span><span class="sxs-lookup"><span data-stu-id="99736-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="99736-116">Para baixar o módulo, consulte [Downloads do Azure](https://azure.microsoft.com/downloads/)(a página pode estar em inglês).</span><span class="sxs-lookup"><span data-stu-id="99736-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="99736-117">Um tutorial que descreve como instalar e configurar o módulo está disponível aqui.</span><span class="sxs-lookup"><span data-stu-id="99736-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="99736-118">Use o cmdlet [Downloads do Azure](https://azure.microsoft.com/downloads/) para carregar o VHD.</span><span class="sxs-lookup"><span data-stu-id="99736-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="99736-119">**Sistema operacional FreeBSD instalado em um arquivo .vhd** – É necessário instalar um sistema operacional FreeBSD com suporte em um disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="99736-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="99736-120">Existem várias ferramentas para criar arquivos .vhd.</span><span class="sxs-lookup"><span data-stu-id="99736-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="99736-121">Por exemplo, você pode usar uma solução de virtualização, como o Hyper-V, para criar o arquivo .vhd e instalar o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="99736-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="99736-122">Para obter instruções sobre como instalar e usar o Hyper-V, confira [Instalar o Hyper-V e criar uma máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="99736-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="99736-123">Não há suporte para o formato VHDX mais recente no Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="99736-124">Você pode converter o disco em formato VHD usando o Gerenciador do Hyper-V ou o cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="99736-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="99736-125">Além disso, há um [tutorial no MSDN sobre como usar o FreeBSD com o Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="99736-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="99736-126">Esta tarefa inclui as cinco etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="99736-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="99736-127">Etapa 1: preparar a imagem para upload</span><span class="sxs-lookup"><span data-stu-id="99736-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="99736-128">Na máquina virtual na qual o sistema operacional FreeBSD foi instalado, conclua os procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="99736-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="99736-129">Habilitar DHCP.</span><span class="sxs-lookup"><span data-stu-id="99736-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="99736-130">Habilitar SSH.</span><span class="sxs-lookup"><span data-stu-id="99736-130">Enable SSH.</span></span>

    <span data-ttu-id="99736-131">Confira se o servidor SSH está instalado e configurado para iniciar no tempo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="99736-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="99736-132">Ele é habilitado por padrão após a instalação do disco FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="99736-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="99736-133">Instalar um console serial.</span><span class="sxs-lookup"><span data-stu-id="99736-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="99736-134">Instalar o sudo.</span><span class="sxs-lookup"><span data-stu-id="99736-134">Install sudo.</span></span>

    <span data-ttu-id="99736-135">A conta raiz está desabilitada no Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="99736-136">Isso significa que você precisa utilizar o sudo de um usuário sem privilégios para executar comandos com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="99736-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="99736-137">Pré-requisitos para agente do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="99736-138">Instalar o agente do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-138">Install Azure Agent.</span></span>

    <span data-ttu-id="99736-139">A versão mais recente do agente do Azure sempre pode ser encontrada no [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="99736-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="99736-140">A versão 2.0.10 + oficialmente dá suporte a FreeBSD 10 e 10.1 e a versão 2.1.4 + (incluindo 2.2.x) oficialmente dá suporte a FreeBSD 10.2 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="99736-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="99736-141">Para o 2.0, vamos usar 2.0.16 como exemplo:</span><span class="sxs-lookup"><span data-stu-id="99736-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="99736-142">Para o 2.1, vamos usar 2.1.4 como exemplo:</span><span class="sxs-lookup"><span data-stu-id="99736-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="99736-143">Depois de instalar o agente do Azure, convém verificar se ele está funcionando:</span><span class="sxs-lookup"><span data-stu-id="99736-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="99736-144">Desprovisione o sistema.</span><span class="sxs-lookup"><span data-stu-id="99736-144">Deprovision the system.</span></span>

    <span data-ttu-id="99736-145">Desprovisione o sistema para limpá-lo e torná-lo adequado para o reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="99736-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="99736-146">O comando a seguir também exclui a última conta de usuário provisionada e os dados associados:</span><span class="sxs-lookup"><span data-stu-id="99736-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="99736-147">Agora você pode desligar sua VM.</span><span class="sxs-lookup"><span data-stu-id="99736-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="99736-148">Etapa 2: Criar uma conta de armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="99736-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="99736-149">Você precisa de uma conta de armazenamento no Azure para carregar um arquivo .vhd para que ele possa ser usado para criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="99736-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="99736-150">Você pode usar o portal clássico do Azure para criar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99736-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="99736-151">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="99736-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="99736-152">Na barra de comandos, selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="99736-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="99736-153">Selecione **Serviços de Dados** > **Armazenamento** > **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="99736-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Criação rápida de uma conta de armazenamento](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="99736-155">Preencha os campos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="99736-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="99736-156">No campo **URL** , digite um nome de subdomínio para usar na URL da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99736-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="99736-157">A entrada pode conter de três a 24 letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="99736-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="99736-158">Esse nome se torna o nome do host na URL usada para tratar os recursos de armazenamento do Armazenamento de Blobs do Azure, do Armazenamento de Filas do Azure ou dos recursos do Armazenamento de Tabelas da assinatura.</span><span class="sxs-lookup"><span data-stu-id="99736-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="99736-159">No menu suspenso **Local/Grupo de Afinidades**, escolha o **local ou um grupo de afinidades** para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99736-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="99736-160">Um grupo de afinidades permite colocar seus serviços de nuvem e armazenamento no mesmo data center.</span><span class="sxs-lookup"><span data-stu-id="99736-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="99736-161">No campo **Replicação**, decida se quer usar a replicação com **Redundância Geográfica** para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99736-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="99736-162">A replicação geográfica é ativada por padrão.</span><span class="sxs-lookup"><span data-stu-id="99736-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="99736-163">Essa opção replica os dados para um local secundário, sem nenhum custo para você, para que o armazenamento efetue o failover para o local se ocorrer uma falha grave no local principal.</span><span class="sxs-lookup"><span data-stu-id="99736-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="99736-164">O local secundário é atribuído automaticamente e não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="99736-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="99736-165">Se você precisar de mais controle sobre o local do armazenamento baseado em nuvem devido a requisitos legais ou política organizacional, você pode desligar a replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="99736-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="99736-166">No entanto, saiba que ao ativar a replicação geográfica posteriormente, você deverá pagar uma taxa de transferência de uma única vez para replicar seus dados existentes para o local secundário.</span><span class="sxs-lookup"><span data-stu-id="99736-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="99736-167">Serviços de armazenamento sem replicação geográfica são oferecidos com desconto.</span><span class="sxs-lookup"><span data-stu-id="99736-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="99736-168">Encontre mais detalhes sobre como gerenciar a replicação geográfica de contas de armazenamento aqui: [Replicação do Armazenamento do Azure](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="99736-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Insira os detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="99736-170">Escolha **Criar Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="99736-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="99736-171">A conta aparece agora em **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="99736-171">The account now appears under **storage**.</span></span>

    ![Conta de armazenamento criada com êxito](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="99736-173">Em seguida, crie um contêiner para os seus .vhd carregados.</span><span class="sxs-lookup"><span data-stu-id="99736-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="99736-174">Escolha o nome da conta de armazenamento e selecione **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="99736-174">Select the storage account name, and then select **Containers**.</span></span>

    ![Detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="99736-176">Escolha **Criar um Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="99736-176">Select **Create a Container**.</span></span>

    ![Detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="99736-178">No campo **Nome** , digite um nome para seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="99736-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="99736-179">Em seguida, no menu suspenso **Acesso** , selecione o tipo de política de acesso desejado.</span><span class="sxs-lookup"><span data-stu-id="99736-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nome do contêiner](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="99736-181">Por padrão, o contêiner é privado e só pode ser acessado pelo proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="99736-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="99736-182">Para permitir acesso de leitura público dos blobs no contêiner, mas não das propriedades ou metadados do contêiner, use a opção **Blob Público** .</span><span class="sxs-lookup"><span data-stu-id="99736-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="99736-183">Para permitir o acesso de leitura público completo do contêiner e de blobs, use a opção **Contêiner Público** .</span><span class="sxs-lookup"><span data-stu-id="99736-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="99736-184">Etapa 3: Preparar a conexão com o Azure</span><span class="sxs-lookup"><span data-stu-id="99736-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="99736-185">Para poder carregar um arquivo .vhd, você precisa estabelecer uma conexão segura entre seu computador e sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="99736-186">No entanto, você pode usar o método do Azure AD (Azure Active Directory) ou o método de certificado para realizar esse tipo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99736-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="99736-187">Usar o método do Azure AD para carregar um arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="99736-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="99736-188">Abra o console do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="99736-189">Digite o seguinte comando: </span><span class="sxs-lookup"><span data-stu-id="99736-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="99736-190">Esse comando abre uma janela de entrada para que você possa entrar com sua conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="99736-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Janela do PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="99736-192">O Azure autentica e salva as informações de credenciais.</span><span class="sxs-lookup"><span data-stu-id="99736-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="99736-193">Em seguida, ele fecha a janela.</span><span class="sxs-lookup"><span data-stu-id="99736-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="99736-194">Usar o método de certificado para carregar um arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="99736-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="99736-195">Abra o console do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="99736-196">Digite: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="99736-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="99736-197">Uma janela de navegador será aberta e baixará automaticamente o arquivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="99736-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="99736-198">Esse arquivo contém informações e um certificado para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Procurar página de download](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="99736-200">Salve o arquivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="99736-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="99736-201">Digite: `Import-AzurePublishSettingsFile <PathToFile>`, em que `<PathToFile>` é o caminho completo para o arquivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="99736-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="99736-202">Para obter mais informações, consulte [Introdução aos cmdlets do Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="99736-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="99736-203">Para saber mais sobre como instalar e configurar o PowerShell, confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="99736-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="99736-204">Etapa 4: carregar o arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="99736-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="99736-205">Quando carrega o arquivo .vhd, você pode colocá-lo em qualquer lugar em seu Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="99736-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="99736-206">Veja a seguir alguns termos que você usará ao carregar o arquivo:</span><span class="sxs-lookup"><span data-stu-id="99736-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="99736-207">**BlobStorageURL** é a URL da conta de armazenamento que você criou na Etapa2.</span><span class="sxs-lookup"><span data-stu-id="99736-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="99736-208">**YourImagesFolder** é o contêiner dentro do Armazenamento de Blobs em que você deseja armazenar as imagens.</span><span class="sxs-lookup"><span data-stu-id="99736-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="99736-209">**VHDName** é o rótulo que aparece no portal clássico do Azure para identificar o disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="99736-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="99736-210">**PathToVHDFile** é o caminho completo e o nome do arquivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="99736-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="99736-211">Na janela PowerShell do Azure que você usou na etapa anterior, digite:</span><span class="sxs-lookup"><span data-stu-id="99736-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="99736-212">Etapa 5: Criar uma VM com o arquivo .vhd carregado</span><span class="sxs-lookup"><span data-stu-id="99736-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="99736-213">Depois de carregar o arquivo .vhd, você pode adicioná-lo como uma imagem à lista de imagens personalizadas associadas à sua assinatura e criar uma máquina virtual com essa imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="99736-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="99736-214">Na janela PowerShell do Azure que você usou na etapa anterior, digite:</span><span class="sxs-lookup"><span data-stu-id="99736-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="99736-215">Use o Linux como o tipo de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="99736-215">Use Linux as the OS type.</span></span> <span data-ttu-id="99736-216">A versão atual do Azure PowerShell aceita apenas "Linux" ou "Windows" como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="99736-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="99736-217">Após concluir as etapas anteriores, a nova imagem será listada ao escolher a guia **Imagens** no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Escolher uma imagem](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="99736-219">Crie uma máquina virtual da galeria.</span><span class="sxs-lookup"><span data-stu-id="99736-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="99736-220">Essa nova imagem agora está disponível em **Minhas imagens**.</span><span class="sxs-lookup"><span data-stu-id="99736-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="99736-221">Escolha a nova imagem.</span><span class="sxs-lookup"><span data-stu-id="99736-221">Select the new image.</span></span> <span data-ttu-id="99736-222">Em seguida, percorra as instruções para configurar um nome de host, senha, chave SSH etc.</span><span class="sxs-lookup"><span data-stu-id="99736-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![Imagem personalizada](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="99736-224">Após a conclusão do provisionamento, você verá sua VM do FreeBSD em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="99736-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Imagem do FreeBSD no azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
