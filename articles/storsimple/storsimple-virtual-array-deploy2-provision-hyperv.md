---
title: Provisionar um StorSimple Virtual Array no Hyper-V | Microsoft Docs
description: "Esse segundo tutorial sobre a implantação da Matriz Virtual StorSimple envolve o provisionamento de uma matriz virtual no Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bad431c8958f7d381bb9c0410caa3a57c6e75c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="514c1-103">Implantar o StorSimple Virtual Array - Provisionar no Hyper-V</span><span class="sxs-lookup"><span data-stu-id="514c1-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="514c1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="514c1-104">Overview</span></span>
<span data-ttu-id="514c1-105">Este tutorial descreve como provisionar um StorSimple Virtual Array em um sistema de host que executa o Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="514c1-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="514c1-106">Este artigo à implantação de Matrizes Virtuais StorSimple no portal do Azure e na Nuvem do Microsoft Azure Governamental.</span><span class="sxs-lookup"><span data-stu-id="514c1-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="514c1-107">Você precisa de privilégios de administrador para provisionar e configurar uma matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-107">You need administrator privileges to provision and configure a virtual array.</span></span> <span data-ttu-id="514c1-108">O provisionamento e a configuração inicial podem levar cerca de 10 minutos para ser concluídos.</span><span class="sxs-lookup"><span data-stu-id="514c1-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="514c1-109">Pré-requisitos de provisionamento</span><span class="sxs-lookup"><span data-stu-id="514c1-109">Provisioning prerequisites</span></span>
<span data-ttu-id="514c1-110">Aqui você encontrará os pré-requisitos para provisionar uma matriz virtual em um sistema de host que executa o Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="514c1-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="514c1-111">Para implantar o serviço Gerenciador de Dispositivos StorSimple</span><span class="sxs-lookup"><span data-stu-id="514c1-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="514c1-112">Antes de começar, verifique se:</span><span class="sxs-lookup"><span data-stu-id="514c1-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="514c1-113">Você concluiu todas as etapas em [Preparar o portal para o StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="514c1-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="514c1-114">Você baixou a imagem da matriz virtual para o Hyper-V no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="514c1-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="514c1-115">Para obter mais informações, consulte **Etapa 3: baixar a imagem do dispositivo virtual** do [guia Preparar o portal da Matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="514c1-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="514c1-116">O software em execução na matriz virtual StorSimple só pode ser usado com o serviço Gerenciador StorSimple.</span><span class="sxs-lookup"><span data-stu-id="514c1-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="514c1-117">Usar a matriz virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="514c1-117">For the StorSimple Virtual Array</span></span>
<span data-ttu-id="514c1-118">Antes de implantar um dispositivo virtual, verifique se:</span><span class="sxs-lookup"><span data-stu-id="514c1-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="514c1-119">Você tem acesso a um sistema de host que executa o Hyper-V no Windows Server 2008 R2 ou superior que pode ser usado para provisionar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="514c1-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="514c1-120">O sistema de host é capaz de dedicar os recursos abaixo para provisionar seu dispositivo virtual:</span><span class="sxs-lookup"><span data-stu-id="514c1-120">The host system is able to dedicate the following resources to provision your virtual array:</span></span>

  * <span data-ttu-id="514c1-121">Um mínimo de quatro núcleos.</span><span class="sxs-lookup"><span data-stu-id="514c1-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="514c1-122">Pelo menos 8 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="514c1-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="514c1-123">Se você planeja configurar a matriz virtual como servidor de arquivos, 8 GB oferece suporte a menos de 2 milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="514c1-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="514c1-124">Você precisa de 16 GB de RAM para dar suporte a 2-4 milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="514c1-124">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="514c1-125">Uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="514c1-125">One network interface.</span></span>
  * <span data-ttu-id="514c1-126">Um disco virtual de 500 GB para dados.</span><span class="sxs-lookup"><span data-stu-id="514c1-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="514c1-127">Para a rede no datacenter</span><span class="sxs-lookup"><span data-stu-id="514c1-127">For the network in the datacenter</span></span>
<span data-ttu-id="514c1-128">Antes de começar, analise os requisitos de rede para implantar uma Matriz Virtual StorSimple e configure a rede de datacenter de acordo com os eles.</span><span class="sxs-lookup"><span data-stu-id="514c1-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span></span> <span data-ttu-id="514c1-129">Para obter mais informações, consulte [Requisitos de rede do StorSimple Virtual Array](storsimple-ova-system-requirements.md#networking-requirements).</span><span class="sxs-lookup"><span data-stu-id="514c1-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="514c1-130">Provisionamento passo a passo</span><span class="sxs-lookup"><span data-stu-id="514c1-130">Step-by-step provisioning</span></span>
<span data-ttu-id="514c1-131">Para provisionar e se conectar a uma matriz virtual, você precisará executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="514c1-131">To provision and connect to a virtual array, you need to perform the following steps:</span></span>

1. <span data-ttu-id="514c1-132">Verificar se o sistema de host tem recursos suficientes para cumprir os requisitos mínimos da matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span></span>
2. <span data-ttu-id="514c1-133">Provisionar uma matriz virtual no seu hipervisor.</span><span class="sxs-lookup"><span data-stu-id="514c1-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="514c1-134">Iniciar a matriz virtual e obter o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="514c1-134">Start the virtual array and get the IP address.</span></span>

<span data-ttu-id="514c1-135">Cada uma das etapas acima é explicada nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="514c1-135">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="514c1-136">Etapa 1: verificar se o sistema de host cumpre os requisitos mínimos da matriz virtual</span><span class="sxs-lookup"><span data-stu-id="514c1-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="514c1-137">Para criar uma matriz virtual, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="514c1-137">To create a virtual array, you need:</span></span>

* <span data-ttu-id="514c1-138">A função do Hyper-V instalada no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2 SP1.</span><span class="sxs-lookup"><span data-stu-id="514c1-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="514c1-139">Microsoft Hyper-V Manager em um cliente Microsoft Windows conectado ao host.</span><span class="sxs-lookup"><span data-stu-id="514c1-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="514c1-140">Faça com que o hardware subjacente (sistema de host) em que está criando a matriz virtual possa dedicar os recursos a seguir à sua matriz virtual:</span><span class="sxs-lookup"><span data-stu-id="514c1-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span></span>

* <span data-ttu-id="514c1-141">Um mínimo de quatro núcleos.</span><span class="sxs-lookup"><span data-stu-id="514c1-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="514c1-142">Pelo menos 8 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="514c1-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="514c1-143">Se você planeja configurar a matriz virtual como servidor de arquivos, 8 GB oferece suporte a menos de 2 milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="514c1-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="514c1-144">Você precisa de 16 GB de RAM para dar suporte a 2-4 milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="514c1-144">You need 16 GB RAM to support 2 - 4 million files.</span></span>
* <span data-ttu-id="514c1-145">Uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="514c1-145">One network interface.</span></span>
* <span data-ttu-id="514c1-146">Um disco virtual de 500 GB para dados do sistema.</span><span class="sxs-lookup"><span data-stu-id="514c1-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="514c1-147">Etapa 2: provisionar uma matriz virtual no hipervisor</span><span class="sxs-lookup"><span data-stu-id="514c1-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="514c1-148">Execute as etapas a seguir para provisionar um dispositivo no seu hipervisor.</span><span class="sxs-lookup"><span data-stu-id="514c1-148">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-array"></a><span data-ttu-id="514c1-149">Para provisionar uma matriz virtual</span><span class="sxs-lookup"><span data-stu-id="514c1-149">To provision a virtual array</span></span>
1. <span data-ttu-id="514c1-150">No seu host do Windows Server, copie a imagem da matriz virtual em uma unidade local.</span><span class="sxs-lookup"><span data-stu-id="514c1-150">On your Windows Server host, copy the virtual array image to a local drive.</span></span> <span data-ttu-id="514c1-151">Você baixou essa imagem (VHD ou VHDX) por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="514c1-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span></span> <span data-ttu-id="514c1-152">Anote o local em que você copiou a imagem, pois ela será usada posteriormente no procedimento.</span><span class="sxs-lookup"><span data-stu-id="514c1-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>
2. <span data-ttu-id="514c1-153">Abra o **Gerenciador do Servidor**.</span><span class="sxs-lookup"><span data-stu-id="514c1-153">Open **Server Manager**.</span></span> <span data-ttu-id="514c1-154">No canto superior direito, clique em **Ferramentas** e selecione **Gerenciador do Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="514c1-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="514c1-155">Se você estiver executando o Windows Server 2008 R2, abra o Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="514c1-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="514c1-156">No Gerenciador do Servidor, clique em **Funções > Hyper-V > Gerenciador do Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="514c1-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="514c1-157">No **Gerenciador do Hyper-V**, no painel de escopo, clique com o botão direito do mouse no nó do sistema para abrir o menu de contexto e clique em **Novo** > **Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="514c1-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="514c1-158">Na página **Antes de começar** do Assistente de Nova Máquina Virtual, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="514c1-159">Na página **Especificar nome e localização**, forneça um **Nome** para sua matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="514c1-160">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="514c1-161">Na página **Especificar geração**, escolha o tipo de imagem do dispositivo e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span></span> <span data-ttu-id="514c1-162">Esta página não aparecerá se você estiver usando o Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="514c1-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="514c1-163">Escolha **Geração 2** se você baixou uma imagem .vhdx para o Windows Server 2012 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="514c1-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="514c1-164">Escolha **Geração 1** se você baixou uma imagem .vhdx para o Windows Server 2008 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="514c1-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="514c1-165">Na página **Atribuir memória**, especifique uma **Memória de inicialização** de pelo menos **8192 MB**, não habilite a memória dinâmica e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="514c1-166">Na página **Configurar rede**, especifique o comutador virtual que está conectado à Internet e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="514c1-167">Na página **Conectar disco rígido virtual**, escolha **Usar um disco rígido virtual existente**, especifique a localização da imagem da matriz virtual (.vhdx ou .vhd) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="514c1-168">Examine o **Resumo** e clique em **Concluir** para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="514c1-169">Para cumprir os requisitos mínimos, você precisará de quatro núcleos.</span><span class="sxs-lookup"><span data-stu-id="514c1-169">To meet the minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="514c1-170">Para adicionar quatro processadores virtuais, selecione o sistema de host na janela **Gerenciador Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="514c1-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span></span> <span data-ttu-id="514c1-171">No painel à direita da lista de **máquinas virtuais**, localize a máquina virtual que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="514c1-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="514c1-172">Selecione e clique com o botão direito do mouse no nome do computador e selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="514c1-172">Select and right-click the machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="514c1-173">Na página **Configurações**, no painel à esquerda, clique em **Processador**.</span><span class="sxs-lookup"><span data-stu-id="514c1-173">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="514c1-174">No painel à direita, defina o **número de processadores virtuais** como quatro (ou mais).</span><span class="sxs-lookup"><span data-stu-id="514c1-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="514c1-175">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="514c1-176">Para cumprir os requisitos mínimos, você também precisa adicionar um disco de dados virtual de 500 GB.</span><span class="sxs-lookup"><span data-stu-id="514c1-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="514c1-177">Na página de **Configurações** :</span><span class="sxs-lookup"><span data-stu-id="514c1-177">In the **Settings** page:</span></span>

    1. <span data-ttu-id="514c1-178">No painel à esquerda, selecione **Controlador SCSI**.</span><span class="sxs-lookup"><span data-stu-id="514c1-178">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="514c1-179">No painel à direita, selecione **Disco Rígido** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-179">In the right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="514c1-180">Na página **Disco rígido**, selecione a opção **Disco rígido virtual** e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="514c1-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="514c1-181">O **Assistente novo disco rígido Virtual** é iniciado.</span><span class="sxs-lookup"><span data-stu-id="514c1-181">The **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="514c1-182">Na página **Antes de começar** do Assistente de Novo Disco Rígido Virtual, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="514c1-183">Na página **Escolher Formato de Disco**, aceite a opção padrão de formato **VHDX**.</span><span class="sxs-lookup"><span data-stu-id="514c1-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="514c1-184">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-184">Click **Next**.</span></span> <span data-ttu-id="514c1-185">Esta tela não é apresentada se o Windows Server 2008 R2 está em execução.</span><span class="sxs-lookup"><span data-stu-id="514c1-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="514c1-186">Na página **Escolher Tipo de Disco**, defina o tipo de disco rígido virtual como **Expansão dinâmica** (recomendado).</span><span class="sxs-lookup"><span data-stu-id="514c1-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="514c1-187">Um disco de **Tamanho fixo** funcionaria, mas talvez você precise aguardar bastante.</span><span class="sxs-lookup"><span data-stu-id="514c1-187">**Fixed size** disk would work but you may need to wait a long time.</span></span> <span data-ttu-id="514c1-188">É recomendável que você não use a opção **Diferenciar** .</span><span class="sxs-lookup"><span data-stu-id="514c1-188">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="514c1-189">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-189">Click **Next**.</span></span> <span data-ttu-id="514c1-190">No Windows Server 2012 R2 e no Windows Server 2012, **Expandir dinamicamente** é a opção padrão; já no Windows Server 2008 R2, o padrão é **Tamanho fixo**.</span><span class="sxs-lookup"><span data-stu-id="514c1-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="514c1-191">Na página **Especificar Nome e Localização**, forneça um **nome** e também uma **localização** (é possível navegar até um) para o disco de dados.</span><span class="sxs-lookup"><span data-stu-id="514c1-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="514c1-192">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="514c1-193">Na página **Configurar Disco**, selecione a opção **Criar um novo disco de rígido virtual em branco** e especifique o tamanho como **500 GB** (ou mais).</span><span class="sxs-lookup"><span data-stu-id="514c1-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="514c1-194">Embora 500 GB seja o requisito mínimo, você sempre poderá provisionar um disco maior.</span><span class="sxs-lookup"><span data-stu-id="514c1-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="514c1-195">Observe que, depois de provisionado, você não poderá expandir ou reduzir o disco.</span><span class="sxs-lookup"><span data-stu-id="514c1-195">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="514c1-196">Para obter mais informações sobre o tamanho do disco a ser provisionado, examine a seção sobre dimensionamento no [documento sobre melhores práticas](storsimple-ova-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="514c1-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="514c1-197">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="514c1-198">Na página **Resumo**, examine os detalhes do disco de dados virtual e, se estiver satisfeito, clique em **Concluir** para criar o disco.</span><span class="sxs-lookup"><span data-stu-id="514c1-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="514c1-199">O assistente é fechado e um disco rígido virtual é adicionado à sua máquina.</span><span class="sxs-lookup"><span data-stu-id="514c1-199">The wizard closes and a virtual hard disk is added to your machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="514c1-200">Retorne para a página **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="514c1-200">Return to the **Settings** page.</span></span> <span data-ttu-id="514c1-201">Clique em **OK** para fechar a página **Configurações** e retornar à janela do Gerenciador do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="514c1-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-array-and-get-the-ip"></a><span data-ttu-id="514c1-202">Etapa 3: iniciar a matriz virtual e obter o IP</span><span class="sxs-lookup"><span data-stu-id="514c1-202">Step 3: Start the virtual array and get the IP</span></span>
<span data-ttu-id="514c1-203">Execute as etapas a seguir para iniciar a matriz virtual e conectar-se a ela.</span><span class="sxs-lookup"><span data-stu-id="514c1-203">Perform the following steps to start your virtual array and connect to it.</span></span>

#### <a name="to-start-the-virtual-array"></a><span data-ttu-id="514c1-204">Para iniciar a matriz virtual</span><span class="sxs-lookup"><span data-stu-id="514c1-204">To start the virtual array</span></span>
1. <span data-ttu-id="514c1-205">Configure a matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-205">Start the virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="514c1-206">Depois que o dispositivo estiver em execução, selecione-o, clique com o botão direito do mouse e selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="514c1-206">After the device is running, select the device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="514c1-207">Você terá que esperar de 5 a 10 minutos para que o dispositivo esteja pronto.</span><span class="sxs-lookup"><span data-stu-id="514c1-207">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="514c1-208">Será exibida uma mensagem de status no console para indicar o andamento.</span><span class="sxs-lookup"><span data-stu-id="514c1-208">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="514c1-209">Depois que o dispositivo estiver pronto, vá para **Ação**.</span><span class="sxs-lookup"><span data-stu-id="514c1-209">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="514c1-210">Pressione `Ctrl + Alt + Delete` para entrar na matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span></span> <span data-ttu-id="514c1-211">O usuário padrão é *StorSimpleAdmin* e a senha padrão é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="514c1-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="514c1-212">Por motivos de segurança, a senha do administrador do dispositivo expira no primeiro logon.</span><span class="sxs-lookup"><span data-stu-id="514c1-212">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="514c1-213">Você será solicitado a alterar a senha.</span><span class="sxs-lookup"><span data-stu-id="514c1-213">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="514c1-214">Insira uma senha que contenha pelo menos oito caracteres.</span><span class="sxs-lookup"><span data-stu-id="514c1-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="514c1-215">A senha deve cumprir pelo menos três dos quatro requisitos a seguir: caracteres maiúsculos, minúsculos, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="514c1-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="514c1-216">Insira a senha novamente para confirmá-la.</span><span class="sxs-lookup"><span data-stu-id="514c1-216">Reenter the password to confirm it.</span></span> <span data-ttu-id="514c1-217">Você é notificado de que a senha foi alterada.</span><span class="sxs-lookup"><span data-stu-id="514c1-217">You are notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="514c1-218">Depois que a senha for alterada com êxito, a matriz virtual poderá ser reiniciada.</span><span class="sxs-lookup"><span data-stu-id="514c1-218">After the password is successfully changed, the virtual array may restart.</span></span> <span data-ttu-id="514c1-219">Aguarde até o dispositivo iniciar.</span><span class="sxs-lookup"><span data-stu-id="514c1-219">Wait for the device to start.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="514c1-220">O console do Windows PowerShell do dispositivo é exibido junto com uma barra de progresso.</span><span class="sxs-lookup"><span data-stu-id="514c1-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="514c1-221">As etapas 6 a 8 se aplicam somente na inicialização de um ambiente não DHCP.</span><span class="sxs-lookup"><span data-stu-id="514c1-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="514c1-222">Se você estiver em um ambiente DHCP, ignore essas etapas e vá para a etapa 9.</span><span class="sxs-lookup"><span data-stu-id="514c1-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="514c1-223">Caso tenha inicializado seu dispositivo em um ambiente não DHCP, você verá a tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="514c1-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="514c1-224">Em seguida, configure a rede.</span><span class="sxs-lookup"><span data-stu-id="514c1-224">Next, configure the network.</span></span>
7. <span data-ttu-id="514c1-225">Use o comando `Get-HcsIpAddress` para listar as interfaces de rede habilitadas em sua matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="514c1-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="514c1-226">Se o dispositivo tiver uma única interface de rede habilitada, o nome padrão atribuído a ela é `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="514c1-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="514c1-227">Use o cmdlet `Set-HcsIpAddress` para configurar a rede.</span><span class="sxs-lookup"><span data-stu-id="514c1-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="514c1-228">Veja os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="514c1-228">See the following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="514c1-229">Depois que a configuração inicial for concluída e o dispositivo for inicializado, você verá o texto da faixa do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="514c1-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="514c1-230">Anote o endereço IP e a URL exibida no texto do banner para gerenciar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="514c1-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="514c1-231">Use esse endereço IP para se conectar à interface do usuário da Web da sua matriz virtual e concluir a configuração local e o registro.</span><span class="sxs-lookup"><span data-stu-id="514c1-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="514c1-232">(Opcional) Execute esta etapa somente se você estiver implantando seu dispositivo na Nuvem do governo.</span><span class="sxs-lookup"><span data-stu-id="514c1-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="514c1-233">Agora, você habilitará o modo FIPS (Federal Information Processing Standard) dos Estados Unidos em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="514c1-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="514c1-234">O padrão FIPS 140 define algoritmos criptográficos aprovados para uso por sistemas de computador do governo federal dos EUA para a proteção de dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="514c1-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="514c1-235">Para habilitar o modo FIPS, execute o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="514c1-235">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="514c1-236">Reinicialize o dispositivo após ter habilitado o modo FIPS para que as validações criptográficas tenham efeito.</span><span class="sxs-lookup"><span data-stu-id="514c1-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="514c1-237">Você pode habilitar ou desabilitar o modo FIPS em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="514c1-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="514c1-238">Alternar o dispositivo entre o modo FIPS e não FIPS não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="514c1-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="514c1-239">Se o dispositivo não cumprir os requisitos mínimos de configuração, você verá o erro a seguir no texto da faixa (mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="514c1-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span></span> <span data-ttu-id="514c1-240">Modifique a configuração do dispositivo para que o computador tenha recursos adequados para cumprir os requisitos mínimos.</span><span class="sxs-lookup"><span data-stu-id="514c1-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="514c1-241">Em seguida, você pode reiniciar e conectar-se ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="514c1-241">You can then restart and connect to the device.</span></span> <span data-ttu-id="514c1-242">Consulte os requisitos mínimos de configuração na [Etapa 1: verificar se o sistema de host atende aos requisitos mínimos da matriz virtual](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="514c1-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="514c1-243">Caso observe algum outro erro durante a configuração inicial usando a interface do usuário da Web local, veja os seguintes fluxos de trabalho:</span><span class="sxs-lookup"><span data-stu-id="514c1-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="514c1-244">Execute testes de diagnóstico para [solucionar problemas na configuração da interface do usuário da Web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="514c1-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="514c1-245">[Gere um pacote de log e exiba os arquivos de log](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="514c1-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="514c1-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="514c1-246">Next steps</span></span>
* [<span data-ttu-id="514c1-247">Configurar sua StorSimple Virtual Array como um servidor de arquivos</span><span class="sxs-lookup"><span data-stu-id="514c1-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="514c1-248">Configurar sua StorSimple Virtual Array como um servidor iSCSI</span><span class="sxs-lookup"><span data-stu-id="514c1-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
