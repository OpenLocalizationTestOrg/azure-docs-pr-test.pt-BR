---
title: imagem de aaaCreate e carregar uma VM FreeBSD | Microsoft Docs
description: "Saiba toocreate e carregar um disco rígido virtual (VHD) que contém a saudação FreeBSD sistema operacional toocreate uma máquina virtual do Azure"
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
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="d001d-103">Criar e carregar um VHD FreeBSD tooAzure</span><span class="sxs-lookup"><span data-stu-id="d001d-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="d001d-104">Este artigo mostra como toocreate e carregar um disco rígido virtual (VHD) que contém Olá sistema de operacional FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="d001d-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="d001d-105">Depois que você carregá-lo, você pode usá-lo como toocreate sua própria imagem uma máquina virtual (VM) no Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d001d-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d001d-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d001d-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="d001d-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d001d-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d001d-109">Para obter informações sobre como carregar um VHD usando o modelo do Gerenciador de recursos de hello, consulte [aqui](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d001d-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d001d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d001d-110">Prerequisites</span></span>
<span data-ttu-id="d001d-111">Este artigo pressupõe que você tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d001d-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="d001d-112">**Uma assinatura do Azure**– Se não tiver uma conta, você poderá criar uma em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d001d-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="d001d-113">Se você tiver uma assinatura do MSDN, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="d001d-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="d001d-114">Caso contrário, saiba como muito[criar uma conta de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d001d-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="d001d-115">**Ferramentas do Azure PowerShell**– módulo do PowerShell do Azure Olá deve ser instalado e configurado toouse sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="d001d-116">módulo de saudação toodownload, consulte [downloads do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d001d-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="d001d-117">Um tutorial que descreve como tooinstall e configurar o módulo Olá está disponível aqui.</span><span class="sxs-lookup"><span data-stu-id="d001d-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="d001d-118">Saudação de uso [Downloads do Azure](https://azure.microsoft.com/downloads/) saudação do cmdlet tooupload VHD.</span><span class="sxs-lookup"><span data-stu-id="d001d-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="d001d-119">**Sistema de operacional FreeBSD instalado em um arquivo. vhd**– um sistema de operacional FreeBSD deve ser instalado tooa do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="d001d-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="d001d-120">Várias ferramentas existem toocreate arquivos. vhd.</span><span class="sxs-lookup"><span data-stu-id="d001d-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="d001d-121">Por exemplo, você pode usar uma solução de virtualização, como o arquivo. vhd do Hyper-V toocreate hello e instalar o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="d001d-122">Para obter instruções sobre como tooinstall e use o Hyper-V, consulte [instalar o Hyper-V e criar uma máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d001d-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d001d-123">Não há suporte para o formato VHDX mais recente de saudação no Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="d001d-124">Você pode converter o formato de tooVHD de disco de saudação usando o Gerenciador do Hyper-V ou Olá cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="d001d-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="d001d-125">Além disso, há um [tutorial no MSDN sobre como toouse FreeBSD com Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="d001d-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="d001d-126">Esta tarefa inclui Olá cinco etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d001d-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="d001d-127">Etapa 1: Preparar a imagem de saudação para carregamento</span><span class="sxs-lookup"><span data-stu-id="d001d-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="d001d-128">Na máquina virtual do hello onde você instalou o sistema de operacional FreeBSD hello, conclua Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d001d-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="d001d-129">Habilitar DHCP.</span><span class="sxs-lookup"><span data-stu-id="d001d-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="d001d-130">Habilitar SSH.</span><span class="sxs-lookup"><span data-stu-id="d001d-130">Enable SSH.</span></span>

    <span data-ttu-id="d001d-131">Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="d001d-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="d001d-132">Ele é habilitado por padrão após a instalação do disco FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="d001d-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="d001d-133">Instalar um console serial.</span><span class="sxs-lookup"><span data-stu-id="d001d-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="d001d-134">Instalar o sudo.</span><span class="sxs-lookup"><span data-stu-id="d001d-134">Install sudo.</span></span>

    <span data-ttu-id="d001d-135">conta de raiz Hello está desabilitada no Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="d001d-136">Isso significa que você precise sudo tooutilize de comandos de toorun um usuário sem privilégios com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="d001d-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="d001d-137">Pré-requisitos para agente do Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="d001d-138">Instalar o agente do Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-138">Install Azure Agent.</span></span>

    <span data-ttu-id="d001d-139">Olá versão mais recente do hello agente do Azure pode sempre ser encontrada no [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="d001d-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="d001d-140">Olá versão 2.0.10 + com suporte oficial à 10 FreeBSD & 10.1 e versão Olá 2.1.4 + (incluindo 2.2) com suporte oficial à FreeBSD 10.2 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="d001d-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="d001d-141">Para o 2.0, vamos usar 2.0.16 como exemplo:</span><span class="sxs-lookup"><span data-stu-id="d001d-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="d001d-142">Para o 2.1, vamos usar 2.1.4 como exemplo:</span><span class="sxs-lookup"><span data-stu-id="d001d-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="d001d-143">Depois de instalar o agente do Azure, é tooverify uma boa ideia que ele está em execução:</span><span class="sxs-lookup"><span data-stu-id="d001d-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="d001d-144">Desprovisione o sistema hello.</span><span class="sxs-lookup"><span data-stu-id="d001d-144">Deprovision hello system.</span></span>

    <span data-ttu-id="d001d-145">Desprovisionamento Olá sistema tooclean-lo e disponibilizá-lo adequado para reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="d001d-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="d001d-146">Olá comando a seguir também exclui última conta de usuário provisionado hello e dados associado de saudação:</span><span class="sxs-lookup"><span data-stu-id="d001d-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="d001d-147">Agora você pode desligar sua VM.</span><span class="sxs-lookup"><span data-stu-id="d001d-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="d001d-148">Etapa 2: Criar uma conta de armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="d001d-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="d001d-149">Você precisa de uma conta de armazenamento no Azure tooupload um arquivo. vhd que ela possa ser usada toocreate uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d001d-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="d001d-150">Você pode usar o hello toocreate portal clássico do Azure uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d001d-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="d001d-151">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d001d-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d001d-152">Na barra de comandos hello, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="d001d-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="d001d-153">Selecione **Serviços de Dados** > **Armazenamento** > **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="d001d-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Criação rápida de uma conta de armazenamento](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="d001d-155">Preencha os campos de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d001d-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="d001d-156">Em Olá **URL** , digite um toouse de nome de subdomínio no hello URL da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d001d-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="d001d-157">Olá entrada pode conter de 3 a 24 números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d001d-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="d001d-158">Esse nome se torna o nome de host de saudação em URL Olá tooaddress usado armazenamento de BLOBs do Azure, armazenamento de fila do Azure, ou recursos de armazenamento de tabela do Azure para a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="d001d-159">Em Olá **local/grupo de afinidade** menu suspenso, escolha Olá **local ou grupo de afinidade** Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d001d-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="d001d-160">Um grupo de afinidade permite colocar seus serviços de nuvem e o armazenamento em Olá mesmo data center.</span><span class="sxs-lookup"><span data-stu-id="d001d-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="d001d-161">Em Olá **replicação** campo, decida se toouse **com redundância geográfica** replicação Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d001d-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="d001d-162">A replicação geográfica é ativada por padrão.</span><span class="sxs-lookup"><span data-stu-id="d001d-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="d001d-163">Essa opção replica seu dados tooa local secundário, em nenhum custo tooyou, para que o armazenamento local toothat se uma falha grave o failover ocorre no local primário hello.</span><span class="sxs-lookup"><span data-stu-id="d001d-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="d001d-164">local secundário Olá é atribuído automaticamente e não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="d001d-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="d001d-165">Se você precisar de mais controle sobre o local de saudação do armazenamento baseado em nuvem devido a requisitos de toolegal ou política organizacional, você pode desativar a replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="d001d-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="d001d-166">No entanto, lembre-se de que se ativar replicação geográfica mais tarde, você será cobrado um único tooreplicate de taxa de transferência de dados secundário local de toohello seus dados existente.</span><span class="sxs-lookup"><span data-stu-id="d001d-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="d001d-167">Serviços de armazenamento sem replicação geográfica são oferecidos com desconto.</span><span class="sxs-lookup"><span data-stu-id="d001d-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="d001d-168">Encontre mais detalhes sobre como gerenciar a replicação geográfica de contas de armazenamento aqui: [Replicação do Armazenamento do Azure](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="d001d-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Insira os detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="d001d-170">Escolha **Criar Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d001d-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="d001d-171">Olá conta agora aparece em **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d001d-171">hello account now appears under **storage**.</span></span>

    ![Conta de armazenamento criada com êxito](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="d001d-173">Em seguida, crie um contêiner para os seus .vhd carregados.</span><span class="sxs-lookup"><span data-stu-id="d001d-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="d001d-174">Selecione o nome de conta de armazenamento hello e, em seguida, selecione **contêineres**.</span><span class="sxs-lookup"><span data-stu-id="d001d-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="d001d-176">Escolha **Criar um Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="d001d-176">Select **Create a Container**.</span></span>

    ![Detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="d001d-178">Em Olá **nome** , digite um nome para seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="d001d-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="d001d-179">Em seguida, no hello **acesso** menu suspenso, selecione o tipo de política de acesso desejado.</span><span class="sxs-lookup"><span data-stu-id="d001d-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nome do contêiner](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="d001d-181">Por padrão, o contêiner de saudação é privado e só pode ser acessado pelo proprietário da conta hello.</span><span class="sxs-lookup"><span data-stu-id="d001d-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="d001d-182">tooallow acesso de leitura público toohello blobs no contêiner de hello, mas não as propriedades de contêiner toohello e metadados, usam Olá **Blob público** opção.</span><span class="sxs-lookup"><span data-stu-id="d001d-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="d001d-183">acesso de leitura público completo tooallow para hello contêiner e blobs, use Olá **contêiner público** opção.</span><span class="sxs-lookup"><span data-stu-id="d001d-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="d001d-184">Etapa 3: Preparar Olá conexão tooAzure</span><span class="sxs-lookup"><span data-stu-id="d001d-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="d001d-185">Antes de carregar um arquivo. vhd, é necessário tooestablish uma conexão segura entre o computador e sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="d001d-186">Você pode usar o método do hello Azure Active Directory (AD do Azure) ou Olá certificado método toodo-lo.</span><span class="sxs-lookup"><span data-stu-id="d001d-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="d001d-187">Usar tooupload de método de saudação do AD do Azure um arquivo. vhd</span><span class="sxs-lookup"><span data-stu-id="d001d-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="d001d-188">Console do Azure PowerShell Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="d001d-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="d001d-189">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d001d-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="d001d-190">Esse comando abre uma janela de entrada para que você possa entrar com sua conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="d001d-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Janela do PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="d001d-192">O Azure autentica e salva informações de credencial de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="d001d-193">Fecha a janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="d001d-194">Usar tooupload de método de certificado Olá um arquivo. vhd</span><span class="sxs-lookup"><span data-stu-id="d001d-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="d001d-195">Console do Azure PowerShell Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="d001d-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="d001d-196">Digite: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="d001d-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="d001d-197">Uma janela do navegador é aberta e solicita que você toodownload Olá arquivo. publishsettings.</span><span class="sxs-lookup"><span data-stu-id="d001d-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="d001d-198">Esse arquivo contém informações e um certificado para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Procurar página de download](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="d001d-200">Salve o arquivo. publishsettings de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="d001d-201">Tipo: `Import-AzurePublishSettingsFile <PathToFile>`, onde `<PathToFile>` é o arquivo. publishsettings do hello caminho completo toohello.</span><span class="sxs-lookup"><span data-stu-id="d001d-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="d001d-202">Para obter mais informações, consulte [Introdução aos cmdlets do Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="d001d-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="d001d-203">Para obter mais informações sobre como instalar e configurar o PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d001d-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="d001d-204">Etapa 4: Carregar o arquivo. vhd de saudação</span><span class="sxs-lookup"><span data-stu-id="d001d-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="d001d-205">Quando você carregar o arquivo. vhd de saudação, você pode colocá-lo em qualquer lugar dentro de seu armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="d001d-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="d001d-206">Estes são alguns termos que você usará ao carregar o arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="d001d-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="d001d-207">**BlobStorageURL** é URL Olá Olá conta de armazenamento que você criou na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="d001d-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="d001d-208">**YourImagesFolder** é o contêiner Olá no armazenamento de Blob onde você deseja toostore suas imagens.</span><span class="sxs-lookup"><span data-stu-id="d001d-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="d001d-209">**VHDName** é Olá rótulo que aparece no hello tooidentify de portal clássico do Azure saudação do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="d001d-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="d001d-210">**PathToVHDFile** é o caminho completo de saudação e o nome do arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="d001d-211">Na janela do PowerShell do Azure de Olá usado na etapa anterior hello, digite:</span><span class="sxs-lookup"><span data-stu-id="d001d-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="d001d-212">Etapa 5: Criar uma VM com o arquivo. vhd carregado de saudação</span><span class="sxs-lookup"><span data-stu-id="d001d-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="d001d-213">Depois de carregar o arquivo. vhd de hello, você pode adicioná-lo como uma lista de toohello de imagem de imagens personalizadas que são associados a sua assinatura e criar uma máquina virtual com esta imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="d001d-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="d001d-214">Na janela do PowerShell do Azure de Olá usado na etapa anterior hello, digite:</span><span class="sxs-lookup"><span data-stu-id="d001d-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="d001d-215">Use o Linux como tipo de SO hello.</span><span class="sxs-lookup"><span data-stu-id="d001d-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="d001d-216">versão do Hello atual do PowerShell do Azure aceita apenas "Linux" ou "Windows" como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d001d-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="d001d-217">Depois de concluir as etapas anteriores hello, nova imagem de saudação está listada quando você escolhe Olá **imagens** guia Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Escolher uma imagem](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="d001d-219">Crie uma máquina virtual da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="d001d-220">Essa nova imagem agora está disponível em **Minhas imagens**.</span><span class="sxs-lookup"><span data-stu-id="d001d-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="d001d-221">Selecione a nova imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d001d-221">Select hello new image.</span></span> <span data-ttu-id="d001d-222">Em seguida, percorra Olá solicita tooset um nome de host, senha, chave SSH e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d001d-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Imagem personalizada](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="d001d-224">Depois de concluir o provisionamento de saudação, você verá seu FreeBSD VM em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="d001d-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Imagem do FreeBSD no azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
