---
title: "Instalar Atualizações em uma Matriz Virtual do Microsoft Azure StorSimple | Microsoft Docs"
description: "Descreve como usar a IU da Web do StorSimple Virtual Array para aplicar atualizações usando o portal e o método de hotfix"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c2d081604c0ca01f47c3ff2aab7477859d280963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="13d47-103">Instalar Atualizações em seu StorSimple Virtual Array — portal do Azure</span><span class="sxs-lookup"><span data-stu-id="13d47-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="13d47-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="13d47-104">Overview</span></span>

<span data-ttu-id="13d47-105">Este artigo descreve as etapas necessárias para instalar atualizações na sua Matriz Virtual StorSimple usando a interface do usuário da Web local e por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d47-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="13d47-106">É necessário aplicar atualizações de software ou hotfixes para manter seu StorSimple Virtual Array atualizado.</span><span class="sxs-lookup"><span data-stu-id="13d47-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="13d47-107">Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13d47-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="13d47-108">Uma vez que o StorSimple Virtual Array é um dispositivo de nó único, qualquer processo de E/S em andamento será interrompido e o dispositivo apresentará tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="13d47-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="13d47-109">Antes de aplicar uma atualização, é recomendável que você deixe os volumes ou compartilhamentos offline no host primeiro e, em seguida, no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13d47-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="13d47-110">Isso minimiza a possibilidade de dados corrompidos.</span><span class="sxs-lookup"><span data-stu-id="13d47-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13d47-111">Se estiver executando a Atualização 0.1 ou versões de software GA, você deverá usar o método de hotfix por meio da interface do usuário da Web local para instalar a atualização 0.3.</span><span class="sxs-lookup"><span data-stu-id="13d47-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="13d47-112">Caso esteja executando a Atualização 0.2, recomendamos que você instale as atualizações por meio do portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d47-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="13d47-113">Usar a interface do usuário da Web local</span><span class="sxs-lookup"><span data-stu-id="13d47-113">Use the local web UI</span></span>

<span data-ttu-id="13d47-114">Há duas etapas ao usar a interface do usuário da Web local:</span><span class="sxs-lookup"><span data-stu-id="13d47-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="13d47-115">Baixe a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="13d47-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="13d47-116">Instale a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="13d47-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="13d47-117">Baixe a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="13d47-117">Download the update or the hotfix</span></span>

<span data-ttu-id="13d47-118">Execute as etapas a seguir para baixar a atualização do software do Catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="13d47-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="13d47-119">Para baixar a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="13d47-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="13d47-120">Inicie o Internet Explorer e acesse [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="13d47-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="13d47-121">Caso esta seja a primeira vez que você usa o Catálogo do Microsoft Update neste computador, clique em **Instalar** quando a instalação do complemento do Catálogo do Microsoft Update for solicitada.</span><span class="sxs-lookup"><span data-stu-id="13d47-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="13d47-122">Na caixa de pesquisa do catálogo do Microsoft Update, insira o número da KB (base de dados de conhecimento) do hotfix que deseja baixar.</span><span class="sxs-lookup"><span data-stu-id="13d47-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="13d47-123">Digite **3182061** para a Atualização 0.3 e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="13d47-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="13d47-124">A listagem de hotfix aparece, por exemplo, como **StorSimple Virtual Array Atualização 0.3**.</span><span class="sxs-lookup"><span data-stu-id="13d47-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="13d47-126">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="13d47-126">Click **Add**.</span></span> <span data-ttu-id="13d47-127">A atualização é adicionada ao carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="13d47-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="13d47-128">Clique em **Exibir carrinho**.</span><span class="sxs-lookup"><span data-stu-id="13d47-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="13d47-129">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="13d47-129">Click **Download**.</span></span> <span data-ttu-id="13d47-130">Especifique ou **Procure** a localização em que deseja que o download apareça.</span><span class="sxs-lookup"><span data-stu-id="13d47-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="13d47-131">As atualizações são baixadas para o local especificado e colocadas em uma subpasta com o mesmo nome que a atualização.</span><span class="sxs-lookup"><span data-stu-id="13d47-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="13d47-132">A pasta também pode ser copiada para um compartilhamento de rede que seja acessível do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13d47-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="13d47-133">Abra a pasta copiada, você verá um arquivo `WindowsTH-KB3011067-x64`do Pacote Autônomo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="13d47-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="13d47-134">Esse arquivo é usado para instalar a atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="13d47-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="13d47-135">Instale a atualização ou o hotfix</span><span class="sxs-lookup"><span data-stu-id="13d47-135">Install the update or the hotfix</span></span>

<span data-ttu-id="13d47-136">Antes da instalação da atualização ou hotfix, certifique-se de que você tem a atualização ou hotfix baixado localmente em seu host ou acessível por meio de um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="13d47-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="13d47-137">Use esse método para instalar atualizações em um dispositivo que executa as versões de software GA ou a Atualização 0.1.</span><span class="sxs-lookup"><span data-stu-id="13d47-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="13d47-138">Esse procedimento leva menos de 2 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="13d47-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="13d47-139">Execute as etapas a seguir para instalar a atualização ou o hotfix.</span><span class="sxs-lookup"><span data-stu-id="13d47-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="13d47-140">Para instalar a atualização ou hotfix</span><span class="sxs-lookup"><span data-stu-id="13d47-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="13d47-141">Na interface do usuário da Web local, vá para **Manutenção** > **Atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="13d47-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="13d47-143">Em **Caminho de arquivo de atualização**, digite o nome de arquivo para a atualização ou hotfix.</span><span class="sxs-lookup"><span data-stu-id="13d47-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="13d47-144">Você também pode navegar até o arquivo de instalação de hotfix ou atualização se colocado em um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="13d47-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="13d47-145">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="13d47-145">Click **Apply**.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="13d47-147">Será exibido um aviso.</span><span class="sxs-lookup"><span data-stu-id="13d47-147">A warning is displayed.</span></span> <span data-ttu-id="13d47-148">Dado que esse é um dispositivo de nó único, depois que a atualização for aplicada, o dispositivo será reiniciado e haverá tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="13d47-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="13d47-149">Clique no ícone de verificação.</span><span class="sxs-lookup"><span data-stu-id="13d47-149">Click the check icon.</span></span>
   
   ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="13d47-151">A atualização será iniciada.</span><span class="sxs-lookup"><span data-stu-id="13d47-151">The update starts.</span></span> <span data-ttu-id="13d47-152">Depois que for atualizado com êxito, o dispositivo será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="13d47-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="13d47-153">A interface do usuário local não estará acessível durante esse tempo.</span><span class="sxs-lookup"><span data-stu-id="13d47-153">The local UI is not accessible in this duration.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="13d47-155">Depois que a reinicialização for concluída, você será levado à página **Entrar** .</span><span class="sxs-lookup"><span data-stu-id="13d47-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="13d47-156">Para confirmar se o software do dispositivo foi atualizado, na interface do usuário da Web local, vá para **Manutenção** > **Atualização de Software**.</span><span class="sxs-lookup"><span data-stu-id="13d47-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="13d47-157">A versão de software exibida deve ser **10.0.0.0.0.10288.0** para a Atualização 0.3.</span><span class="sxs-lookup"><span data-stu-id="13d47-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="13d47-158">Relatamos as versões de software de maneira ligeiramente diferente na interface do usuário da Web local e no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d47-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="13d47-159">Por exemplo, a interface do usuário da Web local informa **10.0.0.0.0.10288** e o portal do Azure informa **10.0.10288.0** para a mesma versão.</span><span class="sxs-lookup"><span data-stu-id="13d47-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure portal reports **10.0.10288.0** for the same version.</span></span>
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="13d47-161">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="13d47-161">Use the Azure portal</span></span>

<span data-ttu-id="13d47-162">Caso esteja executando a Atualização 0.2, é recomendável que você instale atualizações por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d47-162">If running Update 0.2, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="13d47-163">O procedimento do portal requer que o usuário verifique, baixe e instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="13d47-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="13d47-164">Esse procedimento leva cerca de 7 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="13d47-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="13d47-165">Execute as etapas a seguir para instalar a atualização ou o hotfix.</span><span class="sxs-lookup"><span data-stu-id="13d47-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="13d47-166">Após a instalação ser concluída (conforme indicado pelo status do trabalho em 100%), vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="13d47-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="13d47-167">Selecione **Dispositivos** e selecione e clique no dispositivo que deseja atualizar a partir da lista de dispositivos conectados ao serviço.</span><span class="sxs-lookup"><span data-stu-id="13d47-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="13d47-168">Na folha **Configurações**, vá para a seção **Gerenciar** e selecione **Atualizações de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="13d47-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="13d47-169">A versão de software exibida deve ser **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="13d47-169">The displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="13d47-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13d47-170">Next steps</span></span>

<span data-ttu-id="13d47-171">Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="13d47-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

