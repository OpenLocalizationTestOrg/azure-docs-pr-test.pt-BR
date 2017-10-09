---
title: aaaHow tooinstall um servidor de destino mestre Linux para o failover de local de tooon do Azure | Microsoft Docs
description: "Antes de proteger novamente uma máquina virtual Linux, você precisa de um servidor de destino mestre do Linux. Saiba como tooinstall um."
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
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="502c4-104">Instalar o servidor de destino mestre do Linux</span><span class="sxs-lookup"><span data-stu-id="502c4-104">Install a Linux master target server</span></span>
<span data-ttu-id="502c4-105">Depois de executar o failover suas máquinas virtuais, você pode falhar Olá back máquinas virtuais toohello no site local.</span><span class="sxs-lookup"><span data-stu-id="502c4-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="502c4-106">toofail novamente, você precisa tooreprotect Olá VM do Azure toohello no site local.</span><span class="sxs-lookup"><span data-stu-id="502c4-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="502c4-107">Para esse processo, é necessário um tráfego de saudação de tooreceive do servidor de destino mestre local.</span><span class="sxs-lookup"><span data-stu-id="502c4-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="502c4-108">Se sua máquina virtual protegida for uma máquina virtual do Windows, será necessário um destino mestre do Windows.</span><span class="sxs-lookup"><span data-stu-id="502c4-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="502c4-109">Para uma máquina virtual Linux, é necessário um destino mestre do Linux.</span><span class="sxs-lookup"><span data-stu-id="502c4-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="502c4-110">As etapas a seguir de saudação de leitura toolearn como toocreate e instale um Linux mestre de destino.</span><span class="sxs-lookup"><span data-stu-id="502c4-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="502c4-111">A partir da versão do servidor de destino mestre Olá 9.10.0, servidor de destino mestre hello mais recente pode ser instalado de apenas em um servidor do Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="502c4-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="502c4-112">Novas instalações não são permitidas em servidores CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="502c4-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="502c4-113">No entanto, você pode continuar tooupgrade seus servidores de destino mestre antiga usando Olá 9.10.0 versão.</span><span class="sxs-lookup"><span data-stu-id="502c4-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="502c4-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="502c4-114">Overview</span></span>
<span data-ttu-id="502c4-115">Este artigo fornece instruções sobre como a tooinstall um Linux de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="502c4-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="502c4-116">Poste comentários ou perguntas no final da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="502c4-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="502c4-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="502c4-117">Prerequisites</span></span>

* <span data-ttu-id="502c4-118">host de saudação toochoose qual destino mestre do hello de toodeploy, determinar se o failback Olá será toobe tooan existente na máquina virtual ou local tooa nova máquina de virtual.</span><span class="sxs-lookup"><span data-stu-id="502c4-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="502c4-119">Para uma máquina virtual existente, host de saudação do destino mestre Olá deve ter acesso toohello repositórios de dados da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="502c4-120">Se a máquina virtual no local, Olá não existir, Olá failback VM é criado no hello mesmo host como um destino mestre hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="502c4-121">Você pode escolher qualquer host ESXi destino mestre do tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="502c4-122">destino mestre Olá deve estar em uma rede que pode se comunicar com o servidor de processo hello e o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="502c4-123">versão de saudação do destino mestre Olá deve ser igual tooor anteriores a versões de saudação do servidor de processo hello e o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="502c4-124">Por exemplo, se a versão Olá saudação do servidor de configuração for 9.4, versão de saudação do destino mestre Olá pode ser 9.4 ou 9.3 mas não 9,5.</span><span class="sxs-lookup"><span data-stu-id="502c4-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="502c4-125">destino mestre Olá só pode ser uma máquina virtual VMware e não um servidor físico.</span><span class="sxs-lookup"><span data-stu-id="502c4-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="502c4-126">Criar destino mestre hello, de acordo com toohello diretrizes de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="502c4-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="502c4-127">Crie destino mestre de saudação conforme Olá cumprimento das diretrizes de dimensionamento:</span><span class="sxs-lookup"><span data-stu-id="502c4-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="502c4-128">**RAM**: 6 GB ou mais</span><span class="sxs-lookup"><span data-stu-id="502c4-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="502c4-129">**Tamanho de disco do sistema operacional**: 100 GB ou mais (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="502c4-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="502c4-130">**Tamanho de disco adicional para a unidade de retenção**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="502c4-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="502c4-131">**Núcleos de CPU**: 4 núcleos ou mais</span><span class="sxs-lookup"><span data-stu-id="502c4-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="502c4-132">a seguir Olá suporte para Ubuntu kernels têm suporte.</span><span class="sxs-lookup"><span data-stu-id="502c4-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="502c4-133">Série de Kernel</span><span class="sxs-lookup"><span data-stu-id="502c4-133">Kernel Series</span></span>  |<span data-ttu-id="502c4-134">Suporte a backup muito</span><span class="sxs-lookup"><span data-stu-id="502c4-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="502c4-135">4.4</span><span class="sxs-lookup"><span data-stu-id="502c4-135">4.4</span></span>      |<span data-ttu-id="502c4-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="502c4-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="502c4-137">4.8</span><span class="sxs-lookup"><span data-stu-id="502c4-137">4.8</span></span>      |<span data-ttu-id="502c4-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="502c4-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="502c4-139">4.10</span><span class="sxs-lookup"><span data-stu-id="502c4-139">4.10</span></span>     |<span data-ttu-id="502c4-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="502c4-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="502c4-141">Implantar o servidor de destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="502c4-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="502c4-142">Instalar o Ubuntu 16.04.2 Minimal</span><span class="sxs-lookup"><span data-stu-id="502c4-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="502c4-143">Levar Olá Olá etapas tooinstall Olá Ubuntu 16.04.2 64-bit operacional sistema a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="502c4-144">**Etapa 1:** vá toohello [link de download](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) e escolha espelho mais próximo de saudação do qual baixar um ISO de 64 bits Ubuntu 16.04.2 mínimo.</span><span class="sxs-lookup"><span data-stu-id="502c4-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="502c4-145">Manter um ISO de 64 bits Ubuntu 16.04.2 mínimo na unidade de DVD do hello e iniciar o sistema hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="502c4-146">**Etapa 2:** selecione **Inglês** como o seu Idioma de preferência e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selecionar um idioma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="502c4-148">**Etapa 3:** selecione **Instalar Servidor Ubuntu** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selecionar Instalar Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="502c4-150">**Etapa 4:** selecione **Inglês** como o idioma de preferência e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selecionar Inglês como seu idioma preferencial](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="502c4-152">**Etapa 5:** selecione Olá opção apropriada da saudação **fuso horário** lista de opções e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Selecione o fuso horário correto de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="502c4-154">**Etapa 6:** selecione **não** (hello a opção padrão) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Configurar o teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="502c4-156">**Etapa 7:** selecione **inglês (EUA)** como Olá país de origem para teclado hello e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Selecione EUA como país Olá de origem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="502c4-158">**Etapa 8:** selecione **inglês (EUA)** como o layout do teclado hello e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Selecione inglês (EUA) como o layout do teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="502c4-160">**Etapa 9:** insira o nome do host Olá para o servidor de saudação **Hostname** caixa e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="502c4-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Digite o nome de host de saudação do servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="502c4-162">**Etapa 10:** toocreate uma conta de usuário, insira o nome de usuário hello e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="502c4-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Criar uma conta do usuário](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="502c4-164">**Etapa 11:** Insira senha Olá Olá nova conta de usuário e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="502c4-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Insira a senha de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="502c4-166">**Etapa 12:** Confirmar senha Olá Olá novo usuário e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="502c4-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Confirmar senhas Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="502c4-168">**Etapa 13:** selecione **não** (hello a opção padrão) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Configurar usuários e senhas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="502c4-170">**Etapa 14:** se Olá fuso horário é exibido está correto, selecione **Sim** (hello a opção padrão) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="502c4-171">tooreconfigure seu fuso horário, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="502c4-171">tooreconfigure your time zone, select **No**.</span></span>

![Configure o relógio Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="502c4-173">**Etapa 15:** Olá opções do método de particionamento, selecione **interativa - usar o disco inteiro**e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selecione Olá opção método de particionamento](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="502c4-175">**Etapa 16:** selecione Olá disco adequado de saudação **Selecionar disco toopartition** opções e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Selecione o disco Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="502c4-177">**Etapa 17:** selecione **Sim** toowrite Olá toodisk de alterações e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Gravar saudação alterações toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="502c4-179">**Etapa 18:** selecione a opção padrão de saudação, selecione **continuar**e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Selecione a opção padrão de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="502c4-181">**Etapa 19:** selecione a opção apropriada Olá para gerenciar atualizações em seu sistema e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selecione como as atualizações toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="502c4-183">Porque o servidor de destino mestre do Azure Site Recovery Olá requer uma versão muito específica de saudação Ubuntu, é necessário tooensure que kernel Olá atualizações estão desabilitadas para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="502c4-184">Se eles estiverem habilitados, todas as atualizações regulares causam Olá toomalfunction de servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="502c4-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="502c4-185">Verifique se você selecionou Olá **não existem atualizações automáticas** opção.</span><span class="sxs-lookup"><span data-stu-id="502c4-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="502c4-186">**Etapa 20:** selecione as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="502c4-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="502c4-187">Se você desejar openSSH para conexão SSH, selecione Olá **OpenSSH servidor** opção e, em seguida, selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="502c4-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Selecionar o software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="502c4-189">**Etapa 21:** selecione **Sim**e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Carregador de inicialização GRUB instalação Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="502c4-191">**Etapa 22:** selecione Olá dispositivo apropriado para a instalação do carregador de inicialização hello (preferencialmente **/desenvolvimento/sda**) e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="502c4-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selecionar um dispositivo para a instalação do carregador de inicialização](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="502c4-193">**Etapa 23:** selecione **continuar**e, em seguida, selecione **Enter** toofinish instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Concluir a instalação de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="502c4-195">Após instalação hello, entre toohello VM com novas credenciais de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="502c4-196">(Consulte muito**etapa 10** para obter mais informações.)</span><span class="sxs-lookup"><span data-stu-id="502c4-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="502c4-197">Etapas Olá Olá Olá tooset de captura de tela raiz a seguir descritas senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="502c4-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="502c4-198">Faça logon como usuário raiz.</span><span class="sxs-lookup"><span data-stu-id="502c4-198">Then sign in as ROOT user.</span></span>

![Senha de usuário do conjunto Olá raiz](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="502c4-200">Preparar o computador de saudação para a configuração como um servidor de destino mestre</span><span class="sxs-lookup"><span data-stu-id="502c4-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="502c4-201">Em seguida, prepare o computador de saudação para a configuração como um servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="502c4-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="502c4-202">tooget Olá ID para cada disco SCSI em uma máquina virtual Linux, habilitar Olá **em disco. EnableUUID = TRUE** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="502c4-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="502c4-203">tooenable esse parâmetro, Olá take seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="502c4-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="502c4-204">Desligue sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="502c4-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="502c4-205">Entrada Olá para a máquina virtual de saudação no painel esquerdo do hello e, em seguida, selecione **editar configurações de**.</span><span class="sxs-lookup"><span data-stu-id="502c4-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="502c4-206">Selecione Olá **opções** guia.</span><span class="sxs-lookup"><span data-stu-id="502c4-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="502c4-207">No painel esquerdo do hello, selecione **avançado** > **geral**e, em seguida, selecione Olá **parâmetros de configuração** botão na parte inferior direita Olá tela hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Guia Opções](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="502c4-209">Olá **parâmetros de configuração** opção não está disponível quando a saudação máquina está em execução.</span><span class="sxs-lookup"><span data-stu-id="502c4-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="502c4-210">toomake este guia ativa, desligar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="502c4-211">Verifique se já existe uma linha com **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="502c4-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="502c4-212">Se o valor de saudação existe e está definido muito**False**, altere o valor de saudação muito**True**.</span><span class="sxs-lookup"><span data-stu-id="502c4-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="502c4-213">(os valores hello não diferenciam maiusculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="502c4-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="502c4-214">Se o valor de saudação existe e está definido muito**True**, selecione **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="502c4-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="502c4-215">Se o valor de saudação não existir, selecione **Adicionar linha**.</span><span class="sxs-lookup"><span data-stu-id="502c4-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="502c4-216">Na coluna de nome hello, adicionar **em disco. EnableUUID**e, em seguida, defina o valor de saudação muito**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="502c4-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Verificação se disk.EnableUUID já existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="502c4-218">Desabilitar atualizações de kernel</span><span class="sxs-lookup"><span data-stu-id="502c4-218">Disable kernel upgrades</span></span>

<span data-ttu-id="502c4-219">Servidor de destino mestre do Azure Site Recovery requer uma versão muito específica de saudação Ubuntu, verifique se as atualizações de kernel Olá estão desabilitadas para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="502c4-220">Se as atualizações de kernel estiverem habilitadas, todas as atualizações regulares causam Olá toomalfunction de servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="502c4-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="502c4-221">Baixar e instalar pacotes adicionais</span><span class="sxs-lookup"><span data-stu-id="502c4-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="502c4-222">Certifique-se de que você tenha toodownload de conectividade de Internet e instala outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="502c4-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="502c4-223">Se você não tiver conectividade com a Internet, será necessário toomanually localizar esses pacotes RPM e instalá-los.</span><span class="sxs-lookup"><span data-stu-id="502c4-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="502c4-224">Obter o instalador Olá para instalação</span><span class="sxs-lookup"><span data-stu-id="502c4-224">Get hello installer for setup</span></span>

<span data-ttu-id="502c4-225">Se o destino mestre tem conectividade com a Internet, você pode usar o hello instalador de saudação do toodownload as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="502c4-226">Caso contrário, você pode copiar o instalador Olá saudação do servidor de processo e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="502c4-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="502c4-227">Baixe os pacotes de instalação de destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="502c4-227">Download hello master target installation packages</span></span>

<span data-ttu-id="502c4-228">[Fazer o download de bits de instalação de destino mestre do hello mais recentes Linux](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="502c4-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="502c4-229">toodownload usando o Linux, tipo:</span><span class="sxs-lookup"><span data-stu-id="502c4-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="502c4-230">Certifique-se de que você baixe e descompacte o instalador de saudação em seu diretório base.</span><span class="sxs-lookup"><span data-stu-id="502c4-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="502c4-231">Se você descompactar muito**usr/Local**, Olá instalação falhará.</span><span class="sxs-lookup"><span data-stu-id="502c4-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="502c4-232">Instalador de saudação do acesso saudação do servidor de processo</span><span class="sxs-lookup"><span data-stu-id="502c4-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="502c4-233">No servidor de processo hello, ir muito**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="502c4-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="502c4-234">Copie o arquivo de instalador necessário de saudação saudação do servidor de processo e salve-o como **latestlinuxmobsvc.tar.gz** em seu diretório base.</span><span class="sxs-lookup"><span data-stu-id="502c4-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="502c4-235">Aplicar alterações de configuração personalizadas</span><span class="sxs-lookup"><span data-stu-id="502c4-235">Apply custom configuration changes</span></span>

<span data-ttu-id="502c4-236">alterações de configuração personalizada tooapply, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="502c4-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="502c4-237">Execute Olá binário de saudação do comando toountar a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de tela da saudação comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="502c4-239">Execute Olá toogive permissão a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="502c4-240">Olá executar script do comando toorun Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="502c4-241">Execute o script de saudação apenas uma vez no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="502c4-242">Desligar o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-242">Shut down hello server.</span></span> <span data-ttu-id="502c4-243">Reinicie o servidor de saudação, em seguida, depois de adicionar um disco, conforme descrito na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="502c4-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="502c4-244">Adicionar uma máquina virtual retenção disco toohello Linux destino mestre</span><span class="sxs-lookup"><span data-stu-id="502c4-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="502c4-245">Use Olá etapas toocreate um disco de retenção a seguir:</span><span class="sxs-lookup"><span data-stu-id="502c4-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="502c4-246">Anexar uma novo disco de 1 TB toohello Linux mestre máquina virtual de destino e, em seguida, inicie a máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="502c4-247">Saudação de uso **multipath -ll** toolearn Olá multipath ID do disco de retenção de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="502c4-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Olá ID de vários caminhos de disco de retenção Olá](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="502c4-249">Formatar a unidade hello e, em seguida, criar um sistema de arquivos na unidade de novo hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Criando um sistema de arquivos na unidade de saudação](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="502c4-251">Depois de criar o sistema de arquivos hello, monte o disco de retenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco de retenção de saudação de montagem](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="502c4-253">Criar hello **fstab** entrada toomount Olá unidade de retenção sempre Olá sistema é iniciado.</span><span class="sxs-lookup"><span data-stu-id="502c4-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="502c4-254">Selecione **inserir** toobegin editando o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="502c4-255">Criar uma nova linha e insira Olá texto a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="502c4-256">Edite ID vários caminhos do disco Olá com base na ID de vários caminhos Olá realçado do comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="502c4-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="502c4-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="502c4-258">Selecione **Esc**e, em seguida, digite **: wq** (gravação e sair) tooclose janela do editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="502c4-259">Instalar o destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="502c4-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="502c4-260">versão de Olá Olá mestre do servidor de destino deve ser igual tooor anteriores a versões de saudação do servidor de processo hello e o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="502c4-261">Se essa condição não for atendida, o proteger novamente terá êxito, mas a replicação falhará.</span><span class="sxs-lookup"><span data-stu-id="502c4-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="502c4-262">Antes de instalar o servidor de destino mestre hello, verifique que Olá **/etc/hosts** arquivo na máquina virtual de saudação contém entradas que mapeiam Olá nome do host local toohello endereços IP associados a todos os adaptadores de rede.</span><span class="sxs-lookup"><span data-stu-id="502c4-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="502c4-263">Copiar senha de saudação do **C:\ProgramData\Microsoft do Azure Site Recovery\private\connection.passphrase** no servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="502c4-264">Em seguida, salve-o como **passphrase.txt** em Olá mesmo diretório local executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="502c4-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="502c4-265">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="502c4-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="502c4-266">Observe o endereço IP do servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="502c4-267">Ele é necessário na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="502c4-268">Executar Olá após o servidor de destino mestre do comando tooinstall hello e registre o servidor de saudação com o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="502c4-269">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="502c4-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="502c4-270">Aguarde até que o script hello termina.</span><span class="sxs-lookup"><span data-stu-id="502c4-270">Wait until hello script finishes.</span></span> <span data-ttu-id="502c4-271">Se o destino mestre Olá registra com êxito, destino mestre hello está listado no hello **infra-estrutura de recuperação de Site** página do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="502c4-272">Instalar o destino mestre hello usando a instalação interativa</span><span class="sxs-lookup"><span data-stu-id="502c4-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="502c4-273">Execute Olá destino mestre do comando tooinstall Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="502c4-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="502c4-274">Para função de agente hello, escolha **destino mestre**.</span><span class="sxs-lookup"><span data-stu-id="502c4-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="502c4-275">Escolha saudação padrão local para a instalação e, em seguida, selecione **Enter** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="502c4-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Escolher um local padrão para a instalação de destino mestre](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="502c4-277">Após instalação hello, registre o servidor de configuração de saudação usando a linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="502c4-278">Anote o endereço IP de saudação saudação do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="502c4-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="502c4-279">Ele é necessário na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="502c4-280">Executar Olá após o servidor de destino mestre do comando tooinstall hello e registre o servidor de saudação com o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="502c4-281">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="502c4-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="502c4-282">Aguarde até que o script hello termina.</span><span class="sxs-lookup"><span data-stu-id="502c4-282">Wait until hello script finishes.</span></span> <span data-ttu-id="502c4-283">Se o destino mestre Olá é com êxito registrado, destino mestre hello está listado no hello **infra-estrutura de recuperação de Site** página do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="502c4-284">Atualizar o destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="502c4-284">Upgrade hello master target</span></span>

<span data-ttu-id="502c4-285">Execute o instalador de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-285">Run hello installer.</span></span> <span data-ttu-id="502c4-286">Detecta automaticamente que o agente hello está instalado no destino mestre hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="502c4-287">tooupgrade, selecione **Y**.  Olá após a instalação for concluída, verifique a versão de saudação do destino mestre hello, instalado usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="502c4-288">Você pode ver que Olá **versão** campo retorna o número de versão de saudação do destino mestre hello.</span><span class="sxs-lookup"><span data-stu-id="502c4-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="502c4-289">Instalar as ferramentas do VMware no servidor de destino mestre Olá</span><span class="sxs-lookup"><span data-stu-id="502c4-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="502c4-290">É necessário tooinstall as ferramentas do VMware no destino mestre Olá para que ele possa descobrir Olá armazenamentos de dados.</span><span class="sxs-lookup"><span data-stu-id="502c4-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="502c4-291">Se as ferramentas de saudação não são instaladas, tela de nova proteção hello não está listada na Olá armazenamentos de dados.</span><span class="sxs-lookup"><span data-stu-id="502c4-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="502c4-292">Após a instalação das ferramentas do VMware Olá, é necessário toorestart.</span><span class="sxs-lookup"><span data-stu-id="502c4-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="502c4-293">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="502c4-293">Next steps</span></span>
<span data-ttu-id="502c4-294">Instalação hello e o registro do destino mestre Olá finsihed, após você pode ver destino mestre Olá em Olá **destino mestre** seção **infra-estrutura de recuperação de Site**, sob Olá Visão geral de servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="502c4-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="502c4-295">Você pode prosseguir com a [nova proteção](site-recovery-how-to-reprotect.md), seguida pelo failback.</span><span class="sxs-lookup"><span data-stu-id="502c4-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="502c4-296">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="502c4-296">Common issues</span></span>

* <span data-ttu-id="502c4-297">Não ative Storage vMotion em quaisquer componentes de gerenciamento como um destino mestre.</span><span class="sxs-lookup"><span data-stu-id="502c4-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="502c4-298">Se o destino mestre Olá move após uma nova proteção bem-sucedida, os discos da máquina virtual hello (VMDKs) não podem ser desanexados.</span><span class="sxs-lookup"><span data-stu-id="502c4-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="502c4-299">Nesse caso, o failback falhará.</span><span class="sxs-lookup"><span data-stu-id="502c4-299">In this case, failback fails.</span></span>

* <span data-ttu-id="502c4-300">destino mestre Olá não deve ter todos os instantâneos na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="502c4-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="502c4-301">Se houver instantâneos, o failback falhará.</span><span class="sxs-lookup"><span data-stu-id="502c4-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="502c4-302">Devido a toosome configurações de NIC personalizadas em alguns clientes, Olá a interface de rede está desabilitada durante a inicialização e não é possível inicializar o agente de destino mestre Olá.</span><span class="sxs-lookup"><span data-stu-id="502c4-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="502c4-303">Certifique-se de que Olá propriedades a seguir estão definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="502c4-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="502c4-304">Verificar essas propriedades no hello Ethernet /etc/sysconfig/network-scripts/ifcfg do arquivo de cartão-eth *.</span><span class="sxs-lookup"><span data-stu-id="502c4-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="502c4-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="502c4-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="502c4-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="502c4-306">ONBOOT=yes</span></span>
