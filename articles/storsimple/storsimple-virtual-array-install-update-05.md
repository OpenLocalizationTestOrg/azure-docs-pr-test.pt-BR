---
title: "Instalar a Atualização 0.5 em uma StorSimple Virtual Array | Microsoft Docs"
description: "Descreve como usar a IU da Web do StorSimple Virtual Array para aplicar atualizações usando o portal do Azure e o método de hotfix"
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
ms.openlocfilehash: c47da5b90c16e2d5b5709e2a6affc026238b9468
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="b4a4e-103">Instalar a Atualização 0.5 em sua StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="b4a4e-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="b4a4e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b4a4e-104">Overview</span></span>

<span data-ttu-id="b4a4e-105">Este artigo descreve as etapas necessárias para instalar a Atualização 0.5 na sua StorSimple Virtual Array usando a interface do usuário da Web local e por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-105">This article describes the steps required to install Update 0.5 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="b4a4e-106">É necessário aplicar atualizações de software ou hotfixes para manter seu StorSimple Virtual Array atualizado.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="b4a4e-107">Antes de aplicar uma atualização, é recomendável que você deixe os volumes ou compartilhamentos offline no host primeiro e, em seguida, no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="b4a4e-108">Isso minimiza a possibilidade de dados corrompidos.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="b4a4e-109">Depois que os volumes ou compartilhamentos estiverem offline, você também deverá fazer um backup manual do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="b4a4e-110">A Atualização de 0.5 corresponde à versão do software **10.0.10290.0** em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-110">Update 0.5 corresponds to **10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="b4a4e-111">Para obter informações sobre as novidades nessa versão, consulte as [Notas de versão da Atualização 0.5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="b4a4e-111">For information on what is new in this update, go to [Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="b4a4e-112">Caso esteja executando a Atualização 0.2 ou posterior, recomendamos que você instale as atualizações por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="b4a4e-113">Se estiver executando a Atualização 0.1 ou versões de software GA, você deverá usar o método de hotfix por meio da interface do usuário da Web local para instalar a Atualização 0.5.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.5.</span></span>
>
> - <span data-ttu-id="b4a4e-114">Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="b4a4e-115">Uma vez que o StorSimple Virtual Array é um dispositivo de nó único, qualquer processo de E/S em andamento será interrompido e o dispositivo apresentará tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="b4a4e-116">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b4a4e-116">Use the Azure portal</span></span>

<span data-ttu-id="b4a4e-117">Caso esteja executando a Atualização 0.2 ou posterior, é recomendável que você instale atualizações por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="b4a4e-118">O procedimento do portal requer que o usuário verifique, baixe e instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="b4a4e-119">Esse procedimento leva cerca de 7 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="b4a4e-120">Execute as etapas a seguir para instalar a atualização ou o hotfix.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="b4a4e-121">Após a instalação ser concluída, vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="b4a4e-122">Selecione **Dispositivos** e, em seguida, selecione e clique no dispositivo que você acabou de atualizar.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="b4a4e-123">Vá para **Configurações > Gerenciar > Atualizações de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="b4a4e-124">A versão de software exibida deve ser **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-124">The displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="b4a4e-125">Usar a interface do usuário da Web local</span><span class="sxs-lookup"><span data-stu-id="b4a4e-125">Use the local web UI</span></span>

<span data-ttu-id="b4a4e-126">Há duas etapas ao usar a interface do usuário da Web local:</span><span class="sxs-lookup"><span data-stu-id="b4a4e-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="b4a4e-127">Baixe a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="b4a4e-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="b4a4e-128">Instale a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="b4a4e-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="b4a4e-129">Baixe a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="b4a4e-129">Download the update or the hotfix</span></span>

<span data-ttu-id="b4a4e-130">Execute as etapas a seguir para baixar a atualização do software do Catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="b4a4e-131">Para baixar a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="b4a4e-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="b4a4e-132">Inicie o Internet Explorer e acesse [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b4a4e-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="b4a4e-133">Caso esta seja a primeira vez que você usa o Catálogo do Microsoft Update neste computador, clique em **Instalar** quando a instalação do complemento do Catálogo do Microsoft Update for solicitada.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-133">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="b4a4e-134">Na caixa de pesquisa do catálogo do Microsoft Update, insira o número da KB (base de dados de conhecimento) do hotfix que deseja baixar.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="b4a4e-135">Digite **4021576** para a Atualização 0.5 e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="b4a4e-136">A listagem de hotfix aparece, por exemplo, como **StorSimple Virtual Array Atualização 0.5**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="b4a4e-138">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-138">Click **Download**.</span></span> 

5. <span data-ttu-id="b4a4e-139">Você deverá ver dois arquivos para download, um *.msu* e um *.cab*.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-139">You should see two files to download, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="b4a4e-140">Baixe cada um desses arquivos para uma pasta.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-140">Download each of those files to a folder.</span></span> <span data-ttu-id="b4a4e-141">A pasta também pode ser copiada para um compartilhamento de rede que seja acessível do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="b4a4e-142">Abra a pasta na qual os arquivos estão localizados.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="b4a4e-143">![Arquivos no pacote](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="b4a4e-143">![Files in the package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="b4a4e-144">Você verá:</span><span class="sxs-lookup"><span data-stu-id="b4a4e-144">You see:</span></span>
    -  <span data-ttu-id="b4a4e-145">Um arquivo do Pacote Autônomo do Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="b4a4e-146">Esse arquivo é usado para atualizar o software do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="b4a4e-147">Um arquivo do Pacote do Agente de Monitoramento Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="b4a4e-148">Esse arquivo é usado para atualizar o agente de MDS (Monitoramento e Diagnóstico).</span><span class="sxs-lookup"><span data-stu-id="b4a4e-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="b4a4e-149">Clique duas vezes no arquivo cab.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-149">Double-click the cab file.</span></span> <span data-ttu-id="b4a4e-150">Um .msi é exibido.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-150">A .msi is displayed.</span></span> <span data-ttu-id="b4a4e-151">Selecione o arquivo, clique com botão direito do mouse e, em seguida, utilize a opção **Extrair** para realizar a extração do arquivo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="b4a4e-152">Você usará o arquivo _.msi_ para atualizar o agente.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-152">You will use the _.msi_ file to update the agent.</span></span>

        ![Extraia o arquivo de Atualização do Agente de MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="b4a4e-154">Instale a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="b4a4e-154">Install the update or the hotfix</span></span>

<span data-ttu-id="b4a4e-155">Antes da instalação da atualização ou hotfix, certifique-se de que você tem a atualização ou hotfix baixado localmente em seu host ou acessível por meio de um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-155">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="b4a4e-156">Use esse método para instalar atualizações em um dispositivo que executa as versões de software GA ou a Atualização 0.1.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-156">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="b4a4e-157">Esse procedimento leva menos de 2 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-157">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="b4a4e-158">Execute as etapas a seguir para instalar a atualização ou o hotfix.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-158">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="b4a4e-159">Para instalar a atualização ou hotfix</span><span class="sxs-lookup"><span data-stu-id="b4a4e-159">To install the update or the hotfix</span></span>

1. <span data-ttu-id="b4a4e-160">Na interface do usuário da Web local, vá para **Manutenção** > **Atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-160">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="b4a4e-162">Em **Caminho de arquivo de atualização**, digite o nome de arquivo para a atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-162">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="b4a4e-163">Você também pode navegar até o arquivo de instalação de hotfix ou atualização se colocado em um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-163">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="b4a4e-164">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-164">Click **Apply**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="b4a4e-166">Será exibido um aviso.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-166">A warning is displayed.</span></span> <span data-ttu-id="b4a4e-167">Dado que esse é um dispositivo de nó único, depois que a atualização for aplicada, o dispositivo será reiniciado e haverá tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-167">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="b4a4e-168">Clique no ícone de verificação.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-168">Click the check icon.</span></span>
   
   ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="b4a4e-170">A atualização será iniciada.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-170">The update starts.</span></span> <span data-ttu-id="b4a4e-171">Depois que for atualizado com êxito, o dispositivo será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-171">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="b4a4e-172">A interface do usuário local não estará acessível durante esse tempo.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-172">The local UI is not accessible in this duration.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="b4a4e-174">Depois que a reinicialização for concluída, você será levado à página **Entrar** .</span><span class="sxs-lookup"><span data-stu-id="b4a4e-174">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="b4a4e-175">Para confirmar se o software do dispositivo foi atualizado, na interface do usuário da Web local, vá para **Manutenção** > **Atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-175">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="b4a4e-176">A versão de software exibida deve ser **10.0.0.0.0.10290.0** para a Atualização 0.5.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-176">The displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4a4e-177">Relatamos as versões de software de maneira ligeiramente diferente na interface do usuário da Web local e no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-177">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="b4a4e-178">Por exemplo, a interface do usuário da Web local informa **10.0.0.0.0.10290** e o portal do Azure informa **10.0.10290.0** para a mesma versão.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-178">For example, the local web UI reports **10.0.0.0.0.10290** and the Azure portal reports **10.0.10290.0** for the same version.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="b4a4e-180">A próxima etapa é atualizar o agente de MDS.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-180">The next step is to update the MDS agent.</span></span> <span data-ttu-id="b4a4e-181">Na página **Atualização de Software**, vá até o **Caminho do arquivo de atualização** e navegue até o arquivo `GenevaMonitoringAgentPackageInstaller.msi`.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-181">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="b4a4e-182">Repita as etapas de 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-182">Repeat steps 2-4.</span></span> <span data-ttu-id="b4a4e-183">Depois que a matriz virtual for reiniciada, entre na interface do usuário da Web local.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-183">After the virtual array restarts, sign into the local web UI.</span></span>

<span data-ttu-id="b4a4e-184">A atualização está concluída.</span><span class="sxs-lookup"><span data-stu-id="b4a4e-184">The update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4a4e-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4a4e-185">Next steps</span></span>

<span data-ttu-id="b4a4e-186">Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="b4a4e-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

