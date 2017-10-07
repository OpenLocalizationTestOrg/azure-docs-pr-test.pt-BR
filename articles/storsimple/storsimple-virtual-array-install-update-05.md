---
title: "aaaInstall atualização 0,5 na matriz Virtual StorSimple | Microsoft Docs"
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="dd007-103">Instalar a Atualização 0.5 em sua StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="dd007-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="dd007-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dd007-104">Overview</span></span>

<span data-ttu-id="dd007-105">Este artigo descreve Olá de etapas necessárias tooinstall atualização 0,5 em sua matriz Virtual StorSimple através da interface do usuário da web local hello e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd007-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="dd007-106">Você precisa de tookeep de hotfixes ou atualizações de software tooapply sua matriz Virtual StorSimple atualizado.</span><span class="sxs-lookup"><span data-stu-id="dd007-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="dd007-107">Antes de aplicar uma atualização, é recomendável colocar Olá volumes ou compartilhamentos offline Olá hospedam primeiro e hello, em seguida, o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dd007-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="dd007-108">Isso minimiza a possibilidade de dados corrompidos.</span><span class="sxs-lookup"><span data-stu-id="dd007-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="dd007-109">Depois Olá volumes ou compartilhamentos estiverem offline, você deve fazer backup do dispositivo Olá manual.</span><span class="sxs-lookup"><span data-stu-id="dd007-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="dd007-110">Atualização de 0,5 corresponde muito**10.0.10290.0** versão do software em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dd007-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="dd007-111">Para obter informações sobre o que há de novo nesta atualização, acesse muito[notas de versão de atualização 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="dd007-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="dd007-112">Se você estiver executando a atualização 0,2 ou posterior, recomendamos que você instalar atualizações de saudação via Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd007-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="dd007-113">Se você estiver executando a atualização 0,1 ou versões de software GA, você deverá usar o método de hotfix do hello via tooinstall da interface do usuário da web local Olá atualização 0,5.</span><span class="sxs-lookup"><span data-stu-id="dd007-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="dd007-114">Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dd007-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="dd007-115">Considerando que Olá matriz Virtual StorSimple é um dispositivo de nó único, qualquer e/s em andamento será interrompido e o dispositivo apresenta o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="dd007-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="dd007-116">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd007-116">Use hello Azure portal</span></span>

<span data-ttu-id="dd007-117">Se executar o Update 0.2 e posterior, recomendamos que você instale atualizações por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd007-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="dd007-118">requer o procedimento portal Olá Olá usuário tooscan, baixar e instalar atualizações de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd007-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="dd007-119">Esse procedimento utiliza toocomplete cerca de 7 minutos.</span><span class="sxs-lookup"><span data-stu-id="dd007-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="dd007-120">Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="dd007-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="dd007-121">Depois Olá a instalação estiver concluída, vá tooyour serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dd007-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="dd007-122">Selecione **dispositivos** e selecione e clique em dispositivo Olá acabou de ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="dd007-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="dd007-123">Vá muito**Configurações > Gerenciar > atualizações de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="dd007-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="dd007-124">Olá exibido software versão deve ser **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="dd007-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="dd007-125">Use a interface da web local Olá</span><span class="sxs-lookup"><span data-stu-id="dd007-125">Use hello local web UI</span></span>

<span data-ttu-id="dd007-126">Há duas etapas ao usar a interface da web local hello:</span><span class="sxs-lookup"><span data-stu-id="dd007-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="dd007-127">Baixar atualização hello ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="dd007-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="dd007-128">Instalação da atualização de saudação ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="dd007-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="dd007-129">Baixar atualização hello ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="dd007-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="dd007-130">Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="dd007-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="dd007-131">hotfix de atualização ou Olá Olá toodownload</span><span class="sxs-lookup"><span data-stu-id="dd007-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="dd007-132">Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="dd007-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="dd007-133">Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="dd007-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="dd007-134">Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de Olá Olá hotfix que você deseja toodownload.</span><span class="sxs-lookup"><span data-stu-id="dd007-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="dd007-135">Digite **4021576** para a Atualização 0.5 e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="dd007-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="dd007-136">Olá hotfix listagem aparece, por exemplo, **StorSimple Virtual Array atualização 0,5**.</span><span class="sxs-lookup"><span data-stu-id="dd007-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="dd007-138">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="dd007-138">Click **Download**.</span></span> 

5. <span data-ttu-id="dd007-139">Você deverá ver dois toodownload de arquivos, um *. msu* e um *. cab* arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd007-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="dd007-140">Baixe cada um desses tooa da pasta de arquivos.</span><span class="sxs-lookup"><span data-stu-id="dd007-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="dd007-141">pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd007-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="dd007-142">Abra a pasta de saudação onde Olá arquivos estão localizados.</span><span class="sxs-lookup"><span data-stu-id="dd007-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="dd007-143">![Arquivos de pacote de saudação](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="dd007-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="dd007-144">Você verá:</span><span class="sxs-lookup"><span data-stu-id="dd007-144">You see:</span></span>
    -  <span data-ttu-id="dd007-145">Um arquivo do Pacote Autônomo do Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="dd007-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="dd007-146">Esse arquivo é um software de dispositivo de saudação tooupdate usado.</span><span class="sxs-lookup"><span data-stu-id="dd007-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="dd007-147">Um arquivo do Pacote do Agente de Monitoramento Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="dd007-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="dd007-148">Esse arquivo é o agente de serviço (MDS) tooupdate usado Olá monitoramento e diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="dd007-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="dd007-149">Clique duas vezes no arquivo cab de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd007-149">Double-click hello cab file.</span></span> <span data-ttu-id="dd007-150">Um .msi é exibido.</span><span class="sxs-lookup"><span data-stu-id="dd007-150">A .msi is displayed.</span></span> <span data-ttu-id="dd007-151">Arquivo hello Select, com o botão direito e, em seguida, **extrair** arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="dd007-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="dd007-152">Você usará Olá _. msi_ agente de saudação do arquivo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="dd007-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Extraia o arquivo de Atualização do Agente de MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="dd007-154">Instalação da atualização de saudação ou hotfix Olá</span><span class="sxs-lookup"><span data-stu-id="dd007-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="dd007-155">Instalação de atualização ou hotfix toohello anterior, verifique se você tem Olá atualização ou hotfix Olá baixado localmente no seu host ou acessível por meio de um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="dd007-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="dd007-156">Usar atualizações de tooinstall este método em um dispositivo que executa o GA ou 0,1 versões de software de atualização.</span><span class="sxs-lookup"><span data-stu-id="dd007-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="dd007-157">Esse procedimento leva menos de 2 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dd007-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="dd007-158">Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="dd007-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="dd007-159">tooinstall Olá atualização ou hotfix de Olá</span><span class="sxs-lookup"><span data-stu-id="dd007-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="dd007-160">Olá interface da web local, vá muito**manutenção** > **atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="dd007-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="dd007-162">Em **caminho do arquivo de atualização**, insira o nome do arquivo hello para atualização de saudação ou Olá hotfix.</span><span class="sxs-lookup"><span data-stu-id="dd007-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="dd007-163">Você também pode procurar o arquivo de instalação de atualização ou hotfix toohello se colocado em um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="dd007-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="dd007-164">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="dd007-164">Click **Apply**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="dd007-166">Será exibido um aviso.</span><span class="sxs-lookup"><span data-stu-id="dd007-166">A warning is displayed.</span></span> <span data-ttu-id="dd007-167">Fornecido isso é um dispositivo de nó único, depois Olá atualização seja aplicada, Olá dispositivo for reiniciado, e não há tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="dd007-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="dd007-168">Clique o ícone de verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd007-168">Click hello check icon.</span></span>
   
   ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="dd007-170">Inicia a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd007-170">hello update starts.</span></span> <span data-ttu-id="dd007-171">Depois que o dispositivo Olá foi atualizado com êxito, ele será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="dd007-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="dd007-172">Olá interface de usuário local não está acessível durante esse período.</span><span class="sxs-lookup"><span data-stu-id="dd007-172">hello local UI is not accessible in this duration.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="dd007-174">Após a conclusão da reinicialização hello, você será direcionado toohello **entrar** página.</span><span class="sxs-lookup"><span data-stu-id="dd007-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="dd007-175">tooverify Olá dispositivo atualizado, na interface do usuário da web local Olá ir muito**manutenção** > **atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="dd007-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="dd007-176">Olá exibido software versão deve ser **10.0.0.0.0.10290.0** para atualização de 0,5.</span><span class="sxs-lookup"><span data-stu-id="dd007-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dd007-177">Estamos versões de software de saudação de relatório de forma ligeiramente diferente na interface da web local hello e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd007-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="dd007-178">Por exemplo, Olá relatórios de interface do usuário da web local **10.0.0.0.0.10290** e Olá relatórios portais do Azure **10.0.10290.0** para Olá mesma versão.</span><span class="sxs-lookup"><span data-stu-id="dd007-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="dd007-180">Olá próxima etapa é o agente do tooupdate Olá MDS.</span><span class="sxs-lookup"><span data-stu-id="dd007-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="dd007-181">Em Olá **atualização de Software** página, ir toohello **caminho do arquivo de atualização** e procurar toohello `GenevaMonitoringAgentPackageInstaller.msi` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd007-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="dd007-182">Repita as etapas de 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="dd007-182">Repeat steps 2-4.</span></span> <span data-ttu-id="dd007-183">Depois de matriz virtual Olá for reiniciado, entre na interface do usuário da web local hello.</span><span class="sxs-lookup"><span data-stu-id="dd007-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="dd007-184">Olá atualização agora está concluída.</span><span class="sxs-lookup"><span data-stu-id="dd007-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd007-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd007-185">Next steps</span></span>

<span data-ttu-id="dd007-186">Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="dd007-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

