---
title: "Atualizações de aaaInstall na matriz Virtual StorSimple | Microsoft Docs"
description: "Descreve como tooapply toouse Olá matriz Virtual StorSimple web UI atualizações usando Olá método hotfix e o portal do Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="4f0aa-103">Instalar a Atualização 0.4 em seu StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="4f0aa-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="4f0aa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4f0aa-104">Overview</span></span>

<span data-ttu-id="4f0aa-105">Este artigo descreve Olá de etapas necessárias tooinstall atualização 0,4 em sua matriz Virtual StorSimple através da interface do usuário da web local hello e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-105">This article describes hello steps required tooinstall Update 0.4 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="4f0aa-106">Você precisa de tookeep de hotfixes ou atualizações de software tooapply sua matriz Virtual StorSimple atualizado.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="4f0aa-107">Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="4f0aa-108">Considerando que Olá matriz Virtual StorSimple é um dispositivo de nó único, qualquer e/s em andamento será interrompido e o dispositivo apresenta o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="4f0aa-109">Antes de aplicar uma atualização, é recomendável colocar Olá volumes ou compartilhamentos offline Olá hospedam primeiro e hello, em seguida, o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="4f0aa-110">Isso minimiza a possibilidade de dados corrompidos.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f0aa-111">Se você estiver executando a atualização 0,1 ou versões de software GA, você deverá usar o método de hotfix do hello via Olá web local da interface do usuário tooinstall atualização 0.3.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="4f0aa-112">Se você estiver executando a atualização 0,2 ou posterior, recomendamos que você instalar atualizações de saudação via Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="4f0aa-113">Use a interface da web local Olá</span><span class="sxs-lookup"><span data-stu-id="4f0aa-113">Use hello local web UI</span></span>

<span data-ttu-id="4f0aa-114">Há duas etapas ao usar a interface da web local hello:</span><span class="sxs-lookup"><span data-stu-id="4f0aa-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="4f0aa-115">Baixar atualização hello ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="4f0aa-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="4f0aa-116">Instalação da atualização de saudação ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="4f0aa-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="4f0aa-117">Baixar atualização hello ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="4f0aa-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="4f0aa-118">Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="4f0aa-119">hotfix de atualização ou Olá Olá toodownload</span><span class="sxs-lookup"><span data-stu-id="4f0aa-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="4f0aa-120">Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4f0aa-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="4f0aa-121">Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="4f0aa-122">Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de Olá Olá hotfix que você deseja toodownload.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="4f0aa-123">Digite **3216577** para a Atualização 0.4 e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="4f0aa-124">Olá hotfix listagem aparece, por exemplo, **StorSimple Virtual Array atualização 0,4**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="4f0aa-126">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-126">Click **Add**.</span></span> <span data-ttu-id="4f0aa-127">atualização de saudação é adicionada toohello carrinho.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="4f0aa-128">Clique em **Exibir carrinho**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="4f0aa-129">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-129">Click **Download**.</span></span> <span data-ttu-id="4f0aa-130">Especifique ou **procurar** tooa local local onde você deseja Olá downloads tooappear.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="4f0aa-131">Olá as atualizações são baixadas toohello local especificado e colocada em uma subpasta com mesmo nome como atualização de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="4f0aa-132">pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="4f0aa-133">Abra Olá copiou a pasta, você deve ver um arquivo de pacote do Microsoft Update autônomo `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="4f0aa-134">Esse arquivo é usado tooinstall Olá atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="4f0aa-135">Instalação da atualização de saudação ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="4f0aa-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="4f0aa-136">Instalação de atualização ou hotfix toohello anterior, verifique se você tem Olá atualização ou hotfix Olá baixado localmente no seu host ou acessível por meio de um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="4f0aa-137">Usar atualizações de tooinstall este método em um dispositivo que executa o GA ou 0,1 versões de software de atualização.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="4f0aa-138">Esse procedimento leva menos de 2 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="4f0aa-139">Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="4f0aa-140">tooinstall Olá atualização ou hotfix de Olá</span><span class="sxs-lookup"><span data-stu-id="4f0aa-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="4f0aa-141">Olá interface da web local, vá muito**manutenção** > **atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="4f0aa-143">Em **caminho do arquivo de atualização**, insira o nome do arquivo hello para atualização de saudação ou Olá hotfix.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="4f0aa-144">Você também pode procurar o arquivo de instalação de atualização ou hotfix toohello se colocado em um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="4f0aa-145">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-145">Click **Apply**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="4f0aa-147">Será exibido um aviso.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-147">A warning is displayed.</span></span> <span data-ttu-id="4f0aa-148">Fornecido isso é um dispositivo de nó único, depois Olá atualização seja aplicada, Olá dispositivo for reiniciado, e não há tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="4f0aa-149">Clique o ícone de verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-149">Click hello check icon.</span></span>
   
   ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="4f0aa-151">Inicia a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-151">hello update starts.</span></span> <span data-ttu-id="4f0aa-152">Depois que o dispositivo Olá foi atualizado com êxito, ele será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="4f0aa-153">Olá interface de usuário local não está acessível durante esse período.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-153">hello local UI is not accessible in this duration.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="4f0aa-155">Após a conclusão da reinicialização hello, você será direcionado toohello **entrar** página.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="4f0aa-156">tooverify Olá dispositivo atualizado, na interface do usuário da web local Olá ir muito**manutenção** > **atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="4f0aa-157">Olá exibido software versão deve ser **10.0.0.0.0.10289.0** para atualização 0,4.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-157">hello displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4f0aa-158">Estamos versões de software de saudação de relatório de forma ligeiramente diferente na interface da web local hello e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="4f0aa-159">Por exemplo, Olá relatórios de interface do usuário da web local **10.0.0.0.0.10289** e Olá relatórios portais do Azure **10.0.10289.0** para Olá mesma versão.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-159">For example, hello local web UI reports **10.0.0.0.0.10289** and hello Azure portal reports **10.0.10289.0** for hello same version.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="4f0aa-161">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4f0aa-161">Use hello Azure portal</span></span>

<span data-ttu-id="4f0aa-162">Se executar o Update 0.2 e posterior, recomendamos que você instale atualizações por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-162">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="4f0aa-163">requer o procedimento portal Olá Olá usuário tooscan, baixar e instalar atualizações de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="4f0aa-164">Esse procedimento utiliza toocomplete cerca de 7 minutos.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="4f0aa-165">Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="4f0aa-166">Após a saudação instalação é tooyour vá completo (como indicado pelo status do trabalho em 100%), o serviço de Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="4f0aa-167">Selecione **dispositivos** e selecione e clique em dispositivo Olá desejado tooupdate de lista de saudação de dispositivos conectados toothis serviço.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="4f0aa-168">Em Olá **configurações** folha, ir muito**gerenciar** seção e selecione **atualizações de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="4f0aa-169">Olá exibido software versão deve ser **10.0.10289.0**.</span><span class="sxs-lookup"><span data-stu-id="4f0aa-169">hello displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f0aa-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4f0aa-170">Next steps</span></span>

<span data-ttu-id="4f0aa-171">Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="4f0aa-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

