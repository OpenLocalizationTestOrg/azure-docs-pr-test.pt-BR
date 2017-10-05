---
title: Como instalar o servidor de destino mestre do Linux para o failover do Azure no local | Microsoft Docs
description: "Antes de proteger novamente uma máquina virtual Linux, você precisa de um servidor de destino mestre do Linux. Saiba como instalar um."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="083c6-104">Instalar o servidor de destino mestre do Linux</span><span class="sxs-lookup"><span data-stu-id="083c6-104">Install a Linux master target server</span></span>
<span data-ttu-id="083c6-105">Após o failover de suas máquinas virtuais, você poderá executar failback das máquinas virtuais para o site local.</span><span class="sxs-lookup"><span data-stu-id="083c6-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="083c6-106">Para realizar failback, você precisa proteger novamente a máquina virtual do Azure para o site local.</span><span class="sxs-lookup"><span data-stu-id="083c6-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="083c6-107">Para este processo, é necessário um servidor de destino mestre para receber o tráfego.</span><span class="sxs-lookup"><span data-stu-id="083c6-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="083c6-108">Se sua máquina virtual protegida for uma máquina virtual do Windows, será necessário um destino mestre do Windows.</span><span class="sxs-lookup"><span data-stu-id="083c6-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="083c6-109">Para uma máquina virtual Linux, é necessário um destino mestre do Linux.</span><span class="sxs-lookup"><span data-stu-id="083c6-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="083c6-110">Leia as etapas a seguir para saber como criar e instalar um destino mestre do Linux.</span><span class="sxs-lookup"><span data-stu-id="083c6-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="083c6-111">A partir da versão 9.10.0 do servidor de destino mestre, o servidor de destino mestre mais recente somente pode ser instalado em um servidor Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="083c6-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="083c6-112">Novas instalações não são permitidas em servidores CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="083c6-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="083c6-113">No entanto, você pode continuar a atualizar os servidores de destino mestre antigos usando a versão 9.10.0.</span><span class="sxs-lookup"><span data-stu-id="083c6-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="083c6-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="083c6-114">Overview</span></span>
<span data-ttu-id="083c6-115">Este artigo fornece instruções sobre como instalar um destino mestre do Linux.</span><span class="sxs-lookup"><span data-stu-id="083c6-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="083c6-116">Publique comentários ou perguntas no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="083c6-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="083c6-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="083c6-117">Prerequisites</span></span>

* <span data-ttu-id="083c6-118">Para escolher o host no qual deseja implantar o destino mestre, determine se o failback vai ser para uma máquina virtual local existente ou para uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="083c6-119">Para uma máquina virtual existente, o host do destino mestre deve ter acesso a armazenamentos de dados da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="083c6-120">Se a máquina virtual no local não existir, a máquina virtual de failback será criada no mesmo host como o destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="083c6-121">Você pode escolher qualquer host ESXi para instalar o destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="083c6-122">O destino mestre deve estar em uma rede que pode se comunicar com o servidor de processo e com o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="083c6-123">A versão de destino mestre deve ser igual ou anterior às versões de servidor de processo e o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="083c6-124">Por exemplo, se a versão do servidor de configuração for a 9.4, a versão de destino mestre poderá ser 9.4 ou 9.3 mas não 9.5.</span><span class="sxs-lookup"><span data-stu-id="083c6-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="083c6-125">O destino mestre só pode ser uma máquina virtual VMware e não um servidor físico.</span><span class="sxs-lookup"><span data-stu-id="083c6-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="083c6-126">Criar o destino mestre de acordo com as diretrizes de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="083c6-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="083c6-127">Crie o destino mestre de acordo com as seguintes diretrizes de dimensionamento:</span><span class="sxs-lookup"><span data-stu-id="083c6-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="083c6-128">**RAM**: 6 GB ou mais</span><span class="sxs-lookup"><span data-stu-id="083c6-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="083c6-129">**Tamanho do disco do sistema operacional**: 100 GB ou mais (para instalar o CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="083c6-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="083c6-130">**Tamanho de disco adicional para a unidade de retenção**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="083c6-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="083c6-131">**Núcleos de CPU**: 4 núcleos ou mais</span><span class="sxs-lookup"><span data-stu-id="083c6-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="083c6-132">Há suporte para os kernels do Ubuntu a seguir.</span><span class="sxs-lookup"><span data-stu-id="083c6-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="083c6-133">Série de Kernel</span><span class="sxs-lookup"><span data-stu-id="083c6-133">Kernel Series</span></span>  |<span data-ttu-id="083c6-134">Suporte até</span><span class="sxs-lookup"><span data-stu-id="083c6-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="083c6-135">4.4</span><span class="sxs-lookup"><span data-stu-id="083c6-135">4.4</span></span>      |<span data-ttu-id="083c6-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="083c6-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="083c6-137">4.8</span><span class="sxs-lookup"><span data-stu-id="083c6-137">4.8</span></span>      |<span data-ttu-id="083c6-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="083c6-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="083c6-139">4.10</span><span class="sxs-lookup"><span data-stu-id="083c6-139">4.10</span></span>     |<span data-ttu-id="083c6-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="083c6-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="083c6-141">Implantar o servidor de destino mestre</span><span class="sxs-lookup"><span data-stu-id="083c6-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="083c6-142">Instalar o Ubuntu 16.04.2 Minimal</span><span class="sxs-lookup"><span data-stu-id="083c6-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="083c6-143">Use as seguinte as etapas para instalar o sistema de operacional de 64 bits do Ubuntu 16.04.2.</span><span class="sxs-lookup"><span data-stu-id="083c6-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="083c6-144">**Etapa 1:** acesse o [link de download](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) e escolha o espelho mais próximo para baixar um ISO do Ubuntu 16.04.2 Minimal de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="083c6-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="083c6-145">Mantenha um ISO do Ubuntu 16.04.2 Minimal de 64 bits na unidade de DVD e inicie o sistema.</span><span class="sxs-lookup"><span data-stu-id="083c6-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="083c6-146">**Etapa 2:** selecione **Inglês** como o seu Idioma de preferência e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selecionar um idioma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="083c6-148">**Etapa 3:** selecione **Instalar Servidor Ubuntu** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selecionar Instalar Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="083c6-150">**Etapa 4:** selecione **Inglês** como o idioma de preferência e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selecionar Inglês como seu idioma preferencial](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="083c6-152">**Etapa 5:** selecione a opção apropriada para o **Fuso Horário** na lista de opções e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![Selecionar o fuso horário correto](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="083c6-154">**Etapa 6:** selecione **Não** (a opção padrão) e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![Configurar o teclado](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="083c6-156">**Etapa 7:** selecione **Inglês (EUA)** como um país de origem para o teclado e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![Selecionar EUA como país de origem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="083c6-158">**Etapa 8:** selecione **inglês (EUA)** como o layout do teclado e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![Selecionar Inglês (Estados Unidos) como o layout do teclado](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="083c6-160">**Etapa 9:** insira o nome do host para o servidor na caixa **Nome do host** e selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="083c6-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![Inserir o nome do host para o servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="083c6-162">**Etapa 10:** para criar uma conta de usuário, digite o nome de usuário e selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="083c6-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![Criar uma conta do usuário](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="083c6-164">**Etapa 11:** digite a senha para a nova conta de usuário e selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="083c6-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![Digitar a senha](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="083c6-166">**Etapa 12:** confirme a senha para o novo usuário e selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="083c6-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![Confirmar as senhas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="083c6-168">**Etapa 13:** selecione **Não** (a opção padrão) e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![Configurar usuários e senhas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="083c6-170">**Etapa 14:** se o fuso horário exibido está correto, selecione **Sim** (a opção padrão) e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="083c6-171">Para reconfigurar seu fuso horário, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="083c6-171">To reconfigure your time zone, select **No**.</span></span>

![Configurar o relógio](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="083c6-173">**Etapa 15:** entre as opções de método de particionamento, selecione **Guiado - usar o disco inteiro**e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selecionar a opção de método de particionamento](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="083c6-175">**Etapa 16:** selecione o disco adequado nas opções para **Selecionar disco para partição** e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![Selecionar o disco](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="083c6-177">**Etapa 17:** selecione **Sim** para gravar as alterações para o disco e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![Gravar as alterações em disco](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="083c6-179">**Etapa 18:** selecione a opção padrão, selecione **Continuar**e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![Selecionar a opção padrão](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="083c6-181">**Etapa 19:** selecione a opção apropriada para o gerenciamento de atualizações em seu sistema e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selecionar a forma de gerenciar atualizações](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="083c6-183">Como o servidor de destino mestre do Azure Site Recovery requer uma versão muito específica do Ubuntu, você precisa fazer com que as atualizações de kernel estejam desabilitadas para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="083c6-184">Se elas estiverem habilitadas, todas as atualizações regulares farão com que o servidor de destino mestre não funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="083c6-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="083c6-185">Selecione a opção **Sem atualizações automáticas**.</span><span class="sxs-lookup"><span data-stu-id="083c6-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="083c6-186">**Etapa 20:** selecione as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="083c6-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="083c6-187">Se você quiser uma conexão do openSSH para SSH, então selecione a opção **OpenSSH server** e depois selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="083c6-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![Selecionar o software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="083c6-189">**Etapa 21:** selecione **Sim**e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Instalar o carregador de inicialização GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="083c6-191">**Etapa 22:** selecione o dispositivo apropriado para a instalação do carregador de inicialização (preferencialmente **/dev/sda**) e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="083c6-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selecionar um dispositivo para a instalação do carregador de inicialização](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="083c6-193">**Etapa 23:** selecione **Continuar**e selecione **Enter** para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="083c6-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![Concluir a instalação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="083c6-195">Após a instalação, entre na VM com as novas credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="083c6-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="083c6-196">(Consulte a **Etapa 10** para saber mais.)</span><span class="sxs-lookup"><span data-stu-id="083c6-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="083c6-197">Execute as etapas descritas na captura de tela a seguir para definir a senha do usuário raiz.</span><span class="sxs-lookup"><span data-stu-id="083c6-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="083c6-198">Faça logon como usuário raiz.</span><span class="sxs-lookup"><span data-stu-id="083c6-198">Then sign in as ROOT user.</span></span>

![Definir a senha do usuário raiz](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="083c6-200">Preparar o computador para ser configurado como um servidor de destino mestre</span><span class="sxs-lookup"><span data-stu-id="083c6-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="083c6-201">Em seguida, prepare o computador para ser configurado como um servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="083c6-202">Para obter a ID de cada disco SCSI em uma máquina virtual Linux, habilite o parâmetro **disk.EnableUUID = TRUE**.</span><span class="sxs-lookup"><span data-stu-id="083c6-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="083c6-203">Para habilitar esse parâmetro, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="083c6-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="083c6-204">Desligue sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="083c6-205">Clique com o botão direito do mouse na entrada da máquina virtual no painel esquerdo e selecione **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="083c6-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="083c6-206">Selecione a guia **Opções**.</span><span class="sxs-lookup"><span data-stu-id="083c6-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="083c6-207">No painel esquerdo, selecione **Avançado** > **Geral**e selecione o botão **Parâmetros de Configuração** no canto inferior direito da tela.</span><span class="sxs-lookup"><span data-stu-id="083c6-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![Guia Opções](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="083c6-209">A opção **Parâmetros de Configuração** não fica disponível enquanto a máquina está em execução.</span><span class="sxs-lookup"><span data-stu-id="083c6-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="083c6-210">Para ativar essa guia, desligue a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="083c6-211">Verifique se já existe uma linha com **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="083c6-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="083c6-212">Se o valor existe e está definido como **False**, altere o valor para **True**.</span><span class="sxs-lookup"><span data-stu-id="083c6-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="083c6-213">(Os valores não diferenciam maiúsculas de minúsculas.)</span><span class="sxs-lookup"><span data-stu-id="083c6-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="083c6-214">Se o valor existir e se está definido como **True**, selecione **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="083c6-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="083c6-215">Se o valor não existir, selecione **Adicionar Linha**.</span><span class="sxs-lookup"><span data-stu-id="083c6-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="083c6-216">Na coluna Nome, adicione **disk.EnableUUID**e defina o valor como **TRUE**.</span><span class="sxs-lookup"><span data-stu-id="083c6-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![Verificação se disk.EnableUUID já existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="083c6-218">Desabilitar atualizações de kernel</span><span class="sxs-lookup"><span data-stu-id="083c6-218">Disable kernel upgrades</span></span>

<span data-ttu-id="083c6-219">O servidor de destino mestre do Azure Site Recovery requer uma versão muito específica do Ubuntu, verifique se as atualizações de kernel estão desabilitadas para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="083c6-220">Se as atualizações de kernel estiverem habilitadas, todas as atualizações regulares farão com que o servidor de destino mestre não funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="083c6-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="083c6-221">Baixar e instalar pacotes adicionais</span><span class="sxs-lookup"><span data-stu-id="083c6-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="083c6-222">Verifique se você tem conectividade com a Internet para baixar e instalar pacotes adicionais.</span><span class="sxs-lookup"><span data-stu-id="083c6-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="083c6-223">Se você não tiver conexão com a Internet, precisará encontrar esses pacotes RPM e instalá-los manualmente.</span><span class="sxs-lookup"><span data-stu-id="083c6-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="083c6-224">Obter o instalador para instalação</span><span class="sxs-lookup"><span data-stu-id="083c6-224">Get the installer for setup</span></span>

<span data-ttu-id="083c6-225">Se o destino mestre tiver conectividade com a Internet, você poderá usar as etapas a seguir para baixar o instalador.</span><span class="sxs-lookup"><span data-stu-id="083c6-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="083c6-226">Caso contrário, você pode copiar o instalador do servidor de processo e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="083c6-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="083c6-227">Baixar os pacotes de instalação do destino mestre</span><span class="sxs-lookup"><span data-stu-id="083c6-227">Download the master target installation packages</span></span>

<span data-ttu-id="083c6-228">[Baixe os bits de instalação de destino mestre Linux mais recentes](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="083c6-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="083c6-229">Para baixá-los usando o Linux, digite:</span><span class="sxs-lookup"><span data-stu-id="083c6-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="083c6-230">Baixe e descompacte o instalador em seu diretório base.</span><span class="sxs-lookup"><span data-stu-id="083c6-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="083c6-231">Se você o descompactar em **/usr/Local**, a instalação falhará.</span><span class="sxs-lookup"><span data-stu-id="083c6-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="083c6-232">Acessar o instalador do servidor de processos</span><span class="sxs-lookup"><span data-stu-id="083c6-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="083c6-233">No servidor de processo, vá para **C:\Arquivos de Programas (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="083c6-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="083c6-234">Copie o arquivo do instalador obrigatório do servidor de processo e salvá-lo como **latestlinuxmobsvc.tar.gz** no seu diretório base.</span><span class="sxs-lookup"><span data-stu-id="083c6-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="083c6-235">Aplicar alterações de configuração personalizadas</span><span class="sxs-lookup"><span data-stu-id="083c6-235">Apply custom configuration changes</span></span>

<span data-ttu-id="083c6-236">Para aplicar alterações de configuração personalizada, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="083c6-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="083c6-237">Execute o comando a seguir para descompactar o binário.</span><span class="sxs-lookup"><span data-stu-id="083c6-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de tela da execução do comando](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="083c6-239">Execute o comando a seguir para conceder permissão.</span><span class="sxs-lookup"><span data-stu-id="083c6-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="083c6-240">Execute o comando a seguir para executar o script.</span><span class="sxs-lookup"><span data-stu-id="083c6-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="083c6-241">Execute o script apenas uma vez no servidor.</span><span class="sxs-lookup"><span data-stu-id="083c6-241">Run the script only once on the server.</span></span> <span data-ttu-id="083c6-242">Desligue o servidor.</span><span class="sxs-lookup"><span data-stu-id="083c6-242">Shut down the server.</span></span> <span data-ttu-id="083c6-243">Em seguida, reinicialize o servidor depois de adicionar um disco, conforme descrito na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="083c6-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="083c6-244">Adicionar um disco de retenção para a máquina virtual de destino mestre do Linux</span><span class="sxs-lookup"><span data-stu-id="083c6-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="083c6-245">Use as etapas a seguir para criar um disco de retenção:</span><span class="sxs-lookup"><span data-stu-id="083c6-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="083c6-246">Anexe um novo disco de 1 TB à máquina virtual de destino mestre Linux e inicialize a máquina.</span><span class="sxs-lookup"><span data-stu-id="083c6-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="083c6-247">Use o comando **multipath -ll** para conhecer a ID de vários caminhos do disco de retenção.</span><span class="sxs-lookup"><span data-stu-id="083c6-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![A ID de vários caminhos do disco de retenção](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="083c6-249">Formate a unidade e crie um sistema de arquivos na nova unidade.</span><span class="sxs-lookup"><span data-stu-id="083c6-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Criação de um sistema de arquivos na unidade](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="083c6-251">Depois de criar o sistema de arquivos, monte o disco de retenção.</span><span class="sxs-lookup"><span data-stu-id="083c6-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Montagem do disco de retenção](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="083c6-253">Crie a entrada **fstab** para montar a unidade de retenção sempre que o sistema iniciar.</span><span class="sxs-lookup"><span data-stu-id="083c6-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="083c6-254">Selecione **Inserir** para começar a editar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="083c6-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="083c6-255">Crie uma nova linha e insira o texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="083c6-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="083c6-256">Edite a ID de vários caminhos de disco com base na ID de vários caminhos realçada no comando anterior.</span><span class="sxs-lookup"><span data-stu-id="083c6-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="083c6-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="083c6-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="083c6-258">Selecione **Esc** e digite **:wq** (gravar e sair) para fechar a janela do editor.</span><span class="sxs-lookup"><span data-stu-id="083c6-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="083c6-259">Instalar o destino mestre</span><span class="sxs-lookup"><span data-stu-id="083c6-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="083c6-260">A versão do servidor de destino mestre deve ser igual ou anterior às versões de servidor de processo e o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="083c6-261">Se essa condição não for atendida, o proteger novamente terá êxito, mas a replicação falhará.</span><span class="sxs-lookup"><span data-stu-id="083c6-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="083c6-262">Antes de instalar o servidor de destino mestre, verifique se o arquivo **/etc/hosts** na máquina virtual contém entradas que mapeiam o nome do host local para os endereços IP associados a todos os adaptadores de rede.</span><span class="sxs-lookup"><span data-stu-id="083c6-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="083c6-263">Copie a frase secreta de **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** no servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="083c6-264">Em seguida, salve-o como **passphrase.txt** no mesmo diretório local executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="083c6-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="083c6-265">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="083c6-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="083c6-266">Anote o endereço IP do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="083c6-267">Você precisará disso na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="083c6-267">You need it in the next step.</span></span>

3. <span data-ttu-id="083c6-268">Execute o comando a seguir para instalar o servidor de destino mestre e registrar o servidor no servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="083c6-269">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="083c6-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="083c6-270">Aguarde até que o script seja concluído.</span><span class="sxs-lookup"><span data-stu-id="083c6-270">Wait until the script finishes.</span></span> <span data-ttu-id="083c6-271">Se o destino mestre for registrado com êxito, ele será listado na página Infraestrutura do **Site Recovery** do portal.</span><span class="sxs-lookup"><span data-stu-id="083c6-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="083c6-272">Instalar o destino mestre usando a instalação interativa</span><span class="sxs-lookup"><span data-stu-id="083c6-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="083c6-273">Execute o comando a seguir para instalar o destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-273">Run the following command to install the master target.</span></span> <span data-ttu-id="083c6-274">Para a função de agente, escolha **Destino Mestre**.</span><span class="sxs-lookup"><span data-stu-id="083c6-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="083c6-275">Escolha o local padrão para instalação e selecione **Enter** para continuar.</span><span class="sxs-lookup"><span data-stu-id="083c6-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![Escolher um local padrão para a instalação de destino mestre](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="083c6-277">Após a conclusão da instalação, registre o servidor de configuração por meio da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="083c6-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="083c6-278">Observe o endereço IP do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="083c6-279">Você precisará disso na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="083c6-279">You need it in the next step.</span></span>

2. <span data-ttu-id="083c6-280">Execute o comando a seguir para instalar o servidor de destino mestre e registrar o servidor no servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="083c6-281">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="083c6-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="083c6-282">Aguarde até que o script seja concluído.</span><span class="sxs-lookup"><span data-stu-id="083c6-282">Wait until the script finishes.</span></span> <span data-ttu-id="083c6-283">Se o destino mestre for registrado com êxito, ele será listado na página Infraestrutura do **Site Recovery** do portal.</span><span class="sxs-lookup"><span data-stu-id="083c6-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="083c6-284">Atualizar o destino mestre</span><span class="sxs-lookup"><span data-stu-id="083c6-284">Upgrade the master target</span></span>

<span data-ttu-id="083c6-285">Execute o instalador.</span><span class="sxs-lookup"><span data-stu-id="083c6-285">Run the installer.</span></span> <span data-ttu-id="083c6-286">Ele detecta automaticamente que o agente está instalado no destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="083c6-287">Para atualizar, selecione **Y**.  Quando a instalação for concluída, verifique a versão de destino mestre instalada usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="083c6-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="083c6-288">Você pode ver que o campo **Versão** fornece o número de versão de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="083c6-289">Instalar ferramentas do VMware no servidor de destino mestre</span><span class="sxs-lookup"><span data-stu-id="083c6-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="083c6-290">Você precisa instalar ferramentas do VMware no destino mestre para que ele possa descobrir os armazenamentos de dados.</span><span class="sxs-lookup"><span data-stu-id="083c6-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="083c6-291">Se as ferramentas não forem instaladas, a tela Proteja Novamente não estará listada nos armazenamentos de dados.</span><span class="sxs-lookup"><span data-stu-id="083c6-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="083c6-292">Após a instalação das ferramentas do VMware, será necessário reiniciar.</span><span class="sxs-lookup"><span data-stu-id="083c6-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="083c6-293">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="083c6-293">Next steps</span></span>
<span data-ttu-id="083c6-294">Depois que a instalação e o registro do destino mestre forem concluídos, você poderá ver o destino mestre na seção **Destino Mestre** na **Infraestrutura do Site Recovery**, na visão geral do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="083c6-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="083c6-295">Você pode prosseguir com a [nova proteção](site-recovery-how-to-reprotect.md), seguida pelo failback.</span><span class="sxs-lookup"><span data-stu-id="083c6-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="083c6-296">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="083c6-296">Common issues</span></span>

* <span data-ttu-id="083c6-297">Não ative Storage vMotion em quaisquer componentes de gerenciamento como um destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="083c6-298">Se o destino mestre se mover após um proteger novamente com êxito, os VMDKs (discos de máquina virtual) não poderão ser desanexados.</span><span class="sxs-lookup"><span data-stu-id="083c6-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="083c6-299">Nesse caso, o failback falhará.</span><span class="sxs-lookup"><span data-stu-id="083c6-299">In this case, failback fails.</span></span>

* <span data-ttu-id="083c6-300">O destino mestre não deve ter todos os instantâneos na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="083c6-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="083c6-301">Se houver instantâneos, o failback falhará.</span><span class="sxs-lookup"><span data-stu-id="083c6-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="083c6-302">Devido a algumas configurações de NIC personalizadas em alguns clientes, a interface de rede é desabilitada durante a inicialização, e não é possível inicializar o destino mestre.</span><span class="sxs-lookup"><span data-stu-id="083c6-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="083c6-303">Verifique se as propriedades a seguir foram definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="083c6-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="083c6-304">Verifique essas propriedades em /etc/sysconfig/network-scripts/ifcfg-eth* do arquivo da placa Ethernet.</span><span class="sxs-lookup"><span data-stu-id="083c6-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="083c6-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="083c6-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="083c6-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="083c6-306">ONBOOT=yes</span></span>
