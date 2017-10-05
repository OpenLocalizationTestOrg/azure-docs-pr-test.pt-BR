---
title: "Instalar a Atualização 0.6 em um StorSimple Virtual Array | Microsoft Docs"
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 111976cd684561f5bc63b92f09a20470fe3036d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="0fcda-103">Instalar a Atualização 0.6 em seu StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="0fcda-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="0fcda-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0fcda-104">Overview</span></span>

<span data-ttu-id="0fcda-105">Este artigo descreve as etapas necessárias para instalar a Atualização 0.6 no seu StorSimple Virtual Array usando a interface do usuário da Web local e por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcda-105">This article describes the steps required to install Update 0.6 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="0fcda-106">É necessário aplicar atualizações de software ou hotfixes para manter seu StorSimple Virtual Array atualizado.</span><span class="sxs-lookup"><span data-stu-id="0fcda-106">You apply the software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="0fcda-107">Antes de aplicar uma atualização, é recomendável que você deixe os volumes ou compartilhamentos offline no host primeiro e, em seguida, no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="0fcda-108">Isso minimiza a possibilidade de dados corrompidos.</span><span class="sxs-lookup"><span data-stu-id="0fcda-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="0fcda-109">Depois que os volumes ou compartilhamentos estiverem offline, você também deverá fazer um backup manual do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="0fcda-110">A Atualização 0.6 corresponde à versão do software **10.0.10293.0** em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-110">Update 0.6 corresponds to **10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="0fcda-111">Para saber mais sobre as novidades nessa atualização, veja as [Notas de versão da Atualização 0.6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="0fcda-111">For information on what is new in this update, go to [Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="0fcda-112">Caso esteja executando a Atualização 0.2 ou posterior, recomendamos que você instale as atualizações por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcda-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="0fcda-113">Se estiver executando a Atualização 0.1 ou versões de software GA, você deverá usar o método de hotfix por meio da interface do usuário da Web local para instalar a Atualização 0.6.</span><span class="sxs-lookup"><span data-stu-id="0fcda-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.6.</span></span>
>
> - <span data-ttu-id="0fcda-114">Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="0fcda-115">Uma vez que o StorSimple Virtual Array é um dispositivo de nó único, qualquer processo de E/S em andamento será interrompido e o dispositivo apresentará tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="0fcda-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="0fcda-116">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0fcda-116">Use the Azure portal</span></span>

<span data-ttu-id="0fcda-117">Caso esteja executando a Atualização 0.2 ou posterior, é recomendável que você instale atualizações por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcda-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="0fcda-118">O procedimento do portal requer que o usuário verifique, baixe e instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="0fcda-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="0fcda-119">Esse procedimento leva cerca de 7 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0fcda-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="0fcda-120">Execute as etapas a seguir para instalar a atualização ou o hotfix.</span><span class="sxs-lookup"><span data-stu-id="0fcda-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="0fcda-121">Após a instalação ser concluída, vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0fcda-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="0fcda-122">Selecione **Dispositivos** e, em seguida, selecione e clique no dispositivo que você acabou de atualizar.</span><span class="sxs-lookup"><span data-stu-id="0fcda-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="0fcda-123">Vá para **Configurações > Gerenciar > Atualizações de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="0fcda-124">A versão de software exibida deve ser **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-124">The displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="0fcda-125">Usar a interface do usuário da Web local</span><span class="sxs-lookup"><span data-stu-id="0fcda-125">Use the local web UI</span></span>

<span data-ttu-id="0fcda-126">Há duas etapas ao usar a interface do usuário da Web local:</span><span class="sxs-lookup"><span data-stu-id="0fcda-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="0fcda-127">Baixe a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="0fcda-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="0fcda-128">Instale a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="0fcda-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="0fcda-129">Baixe a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="0fcda-129">Download the update or the hotfix</span></span>

<span data-ttu-id="0fcda-130">Execute as etapas a seguir para baixar a atualização do software do Catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="0fcda-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="0fcda-131">Para baixar a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="0fcda-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="0fcda-132">Inicie o Internet Explorer e acesse [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0fcda-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="0fcda-133">Se você estiver usando o Catálogo do Microsoft Update pela primeira vez neste computador, clique em **Instalar** quando a instalação do complemento do Catálogo do Microsoft Update for solicitada.</span><span class="sxs-lookup"><span data-stu-id="0fcda-133">If you are using the Microsoft Update Catalog for the first time on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="0fcda-134">Na caixa de pesquisa do catálogo do Microsoft Update, insira o número da KB (base de dados de conhecimento) do hotfix que deseja baixar.</span><span class="sxs-lookup"><span data-stu-id="0fcda-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="0fcda-135">Insira **4023268** para a Atualização 0.6 e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="0fcda-136">A listagem de hotfixes aparece, por exemplo, como **StorSimple Virtual Array Atualização 0.6**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="0fcda-138">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-138">Click **Download**.</span></span>

5. <span data-ttu-id="0fcda-139">Você deve ver cinco arquivos para download.</span><span class="sxs-lookup"><span data-stu-id="0fcda-139">You should see five files to download.</span></span> <span data-ttu-id="0fcda-140">Baixe cada um desses arquivos para uma pasta.</span><span class="sxs-lookup"><span data-stu-id="0fcda-140">Download each of those files to a folder.</span></span> <span data-ttu-id="0fcda-141">A pasta também pode ser copiada para um compartilhamento de rede que seja acessível do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="0fcda-142">Abra a pasta na qual os arquivos estão localizados.</span><span class="sxs-lookup"><span data-stu-id="0fcda-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="0fcda-143">![Arquivos no pacote](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="0fcda-143">![Files in the package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="0fcda-144">Você verá:</span><span class="sxs-lookup"><span data-stu-id="0fcda-144">You see:</span></span>
    -  <span data-ttu-id="0fcda-145">Um arquivo do Pacote Autônomo do Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="0fcda-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="0fcda-146">Esse arquivo é usado para atualizar o software do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="0fcda-147">Um arquivo do Pacote do Agente de Monitoramento Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="0fcda-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="0fcda-148">Esse arquivo é usado para atualizar o agente de MDS (Monitoramento e Diagnóstico).</span><span class="sxs-lookup"><span data-stu-id="0fcda-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="0fcda-149">Clique duas vezes no arquivo cab.</span><span class="sxs-lookup"><span data-stu-id="0fcda-149">Double-click the cab file.</span></span> <span data-ttu-id="0fcda-150">Um _.msi_ é exibido.</span><span class="sxs-lookup"><span data-stu-id="0fcda-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="0fcda-151">Selecione o arquivo, clique com botão direito do mouse e, em seguida, utilize a opção **Extrair** para realizar a extração do arquivo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="0fcda-152">Você usará o arquivo _.msi_ para atualizar o agente.</span><span class="sxs-lookup"><span data-stu-id="0fcda-152">You use the _.msi_ file to update the agent.</span></span>

        ![Extraia o arquivo de Atualização do Agente de MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="0fcda-154">Você não precisará atualizar o agente do MDS, se estiver executando a Atualização do StorSimple 0.5 (0.0.10293.0).</span><span class="sxs-lookup"><span data-stu-id="0fcda-154">You do not need to update the MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="0fcda-155">Três arquivos que contêm atualizações críticas de segurança do Windows, `windows8.1-kb4012213-x64`, `windows8.1-kb3205400-x64` e `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="0fcda-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="0fcda-156">Instale a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="0fcda-156">Install the update or the hotfix</span></span>

<span data-ttu-id="0fcda-157">Antes da instalação da atualização ou hotfix, certifique-se de que você tem a atualização ou hotfix baixado localmente em seu host ou acessível por meio de um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="0fcda-157">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="0fcda-158">Use esse método para instalar atualizações em um dispositivo que executa as versões de software GA ou a Atualização 0.1.</span><span class="sxs-lookup"><span data-stu-id="0fcda-158">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="0fcda-159">Este procedimento leva cerca de 12 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0fcda-159">This procedure takes approximately 12 minutes to complete.</span></span> <span data-ttu-id="0fcda-160">Execute as etapas a seguir para instalar a atualização ou o hotfix.</span><span class="sxs-lookup"><span data-stu-id="0fcda-160">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="0fcda-161">Para instalar a atualização ou hotfix</span><span class="sxs-lookup"><span data-stu-id="0fcda-161">To install the update or the hotfix</span></span>

1. <span data-ttu-id="0fcda-162">Na interface do usuário da Web local, vá para **Manutenção** > **Atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-162">In the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="0fcda-163">Anote a versão do software que você está executando.</span><span class="sxs-lookup"><span data-stu-id="0fcda-163">Make a note of the software version that you are running.</span></span> <span data-ttu-id="0fcda-164">Se você estiver executando **10.0.10290.0**, não será necessário atualizar o agente MDS na etapa 6.</span><span class="sxs-lookup"><span data-stu-id="0fcda-164">If you are running **10.0.10290.0**, you do not need to update the MDS agent in step 6.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="0fcda-166">Em **Caminho de arquivo de atualização**, digite o nome de arquivo para a atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="0fcda-166">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="0fcda-167">Você também pode navegar até o arquivo de instalação de hotfix ou atualização se colocado em um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="0fcda-167">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="0fcda-168">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-168">Click **Apply**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="0fcda-170">Será exibido um aviso.</span><span class="sxs-lookup"><span data-stu-id="0fcda-170">A warning is displayed.</span></span> <span data-ttu-id="0fcda-171">Como a matriz virtual é um dispositivo de nó único, depois que a atualização for aplicada, o dispositivo será reiniciado e haverá tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="0fcda-171">Given the virtual array is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="0fcda-172">Clique no ícone de verificação.</span><span class="sxs-lookup"><span data-stu-id="0fcda-172">Click the check icon.</span></span>
   
   ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="0fcda-174">A atualização será iniciada.</span><span class="sxs-lookup"><span data-stu-id="0fcda-174">The update starts.</span></span> <span data-ttu-id="0fcda-175">Depois que for atualizado com êxito, o dispositivo será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="0fcda-175">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="0fcda-176">A interface do usuário local não estará acessível durante esse tempo.</span><span class="sxs-lookup"><span data-stu-id="0fcda-176">The local UI is not accessible in this duration.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="0fcda-178">Depois que a reinicialização for concluída, você será levado à página **Entrar** .</span><span class="sxs-lookup"><span data-stu-id="0fcda-178">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="0fcda-179">Para confirmar se o software do dispositivo foi atualizado, na interface do usuário da Web local, vá para **Manutenção** > **Atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="0fcda-179">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="0fcda-180">A versão de software exibida deve ser **10.0.0.0.0.10293** para a Atualização 0.6.</span><span class="sxs-lookup"><span data-stu-id="0fcda-180">The displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0fcda-181">Relatamos as versões de software de maneira ligeiramente diferente na interface do usuário da Web local e no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcda-181">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="0fcda-182">Por exemplo, a interface do usuário da Web local informa **10.0.0.0.0.10293** e o Portal do Azure informa **10.0.10293.0** para a mesma versão.</span><span class="sxs-lookup"><span data-stu-id="0fcda-182">For example, the local web UI reports **10.0.0.0.0.10293** and the Azure portal reports **10.0.10293.0** for the same version.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="0fcda-184">Ignore esta etapa se você executou a Atualização 0.5 da Matriz Virtual do StorSimple (**10.0.10290.0**) antes de aplicar essa atualização.</span><span class="sxs-lookup"><span data-stu-id="0fcda-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="0fcda-185">Você fez uma anotação da versão do software na etapa 1 antes de começar a atualizar.</span><span class="sxs-lookup"><span data-stu-id="0fcda-185">You made a note of the software version in step 1 before you began to update.</span></span> <span data-ttu-id="0fcda-186">Se você executou a Atualização 0.5, seu agente do MDS já está atualizado.</span><span class="sxs-lookup"><span data-stu-id="0fcda-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="0fcda-187">Se você estiver executando uma versão do software antes da Atualização 0.5, a próxima etapa será a atualização do agente do MDS.</span><span class="sxs-lookup"><span data-stu-id="0fcda-187">If you are running a software version prior to Update 0.5, the next step for you is to update the MDS agent.</span></span> <span data-ttu-id="0fcda-188">Na página **Atualização de Software**, vá até o **Caminho do arquivo de atualização** e navegue até o arquivo `GenevaMonitoringAgentPackageInstaller.msi`.</span><span class="sxs-lookup"><span data-stu-id="0fcda-188">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="0fcda-189">Repita as etapas de 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="0fcda-189">Repeat steps 2-4.</span></span> <span data-ttu-id="0fcda-190">Depois que a matriz virtual for reiniciada, entre na interface do usuário da Web local.</span><span class="sxs-lookup"><span data-stu-id="0fcda-190">After the virtual array restarts, sign into the local web UI.</span></span>

7. <span data-ttu-id="0fcda-191">Repita a etapa 2 a 4 para instalar as correções de segurança do Windows usando arquivos os `windows8.1-kb4012213-x64`, `windows8.1-kb3205400-x64` e `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="0fcda-191">Repeat step 2-4 to install the Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="0fcda-192">A matriz virtual reinicia após cada instalação e você precisa entrar na interface do usuário da Web local.</span><span class="sxs-lookup"><span data-stu-id="0fcda-192">The virtual array restarts after each install and you need to sign into the local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fcda-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fcda-193">Next steps</span></span>

<span data-ttu-id="0fcda-194">Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="0fcda-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

