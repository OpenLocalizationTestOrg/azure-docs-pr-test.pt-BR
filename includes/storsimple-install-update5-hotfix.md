<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="6c7ff-101">hotfixes toodownload</span><span class="sxs-lookup"><span data-stu-id="6c7ff-101">toodownload hotfixes</span></span>

<span data-ttu-id="6c7ff-102">Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="6c7ff-103">Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6c7ff-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="6c7ff-104">Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="6c7ff-106">Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de saudação de saudação hotfix que você deseja toodownload, por exemplo **4037264**e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="6c7ff-107">Olá hotfix listagem aparece, por exemplo, **cumulativa 5.0 de atualização de pacote de Software para StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="6c7ff-109">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-109">Click **Download**.</span></span> <span data-ttu-id="6c7ff-110">Especifique ou **procurar** tooa local local onde você deseja Olá downloads tooappear.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="6c7ff-111">Clique em arquivos de saudação toodownload toohello especificado local e a pasta.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="6c7ff-112">pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="6c7ff-113">Procure os hotfixes adicionais listadas na tabela de saudação acima (**4037266**), e correspondente de saudação do download arquivos pastas específicas toohello conforme listado na saudação anterior da tabela.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="6c7ff-114">Olá hotfixes deve ser acessíveis de ambos os toodetect controladores mensagens de qualquer erro em potencial do controlador de par de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="6c7ff-115">Olá hotfixes devem ser copiados em pastas separadas e 3.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="6c7ff-116">Por exemplo, a atualização do agente de Cis/software/MDS de dispositivo Olá pode ser copiada em _FirstOrderUpdate_ Olá a pasta, todas as outras atualizações sem interrupção podem ser copiadas no hello _SecondOrderUpdate_ pasta, e atualizações do modo de manutenção copiadas na _ThirdOrderUpdate_ pasta.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="6c7ff-117">tooinstall e verifique se os hotfixes do modo normal</span><span class="sxs-lookup"><span data-stu-id="6c7ff-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="6c7ff-118">Executar Olá tooinstall as etapas a seguir e verifique se a hotfixes do modo normal.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="6c7ff-119">Se você já instalou usando Olá portal do Azure, vá em frente muito[instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="6c7ff-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="6c7ff-120">tooinstall Olá hotfixes, interface do acesso saudação do Windows PowerShell no seu console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="6c7ff-121">Siga Olá detalhadas instruções [console serial do PuTTy Use tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="6c7ff-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="6c7ff-122">No prompt de comando hello, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="6c7ff-123">Selecione **opção 1** toolog toohello dispositivo com acesso completo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="6c7ff-124">É recomendável que você instale o hotfix Olá no controlador passivo Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="6c7ff-125">tooinstall Olá hotfix, no prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="6c7ff-126">Use o IP em vez de DNS no caminho de compartilhamento Olá acima de comando.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="6c7ff-127">parâmetro de credencial de saudação é usado somente se você estiver acessando um compartilhamento autenticado.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="6c7ff-128">É recomendável que você use compartilhamentos de tooaccess de parâmetro de credencial de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="6c7ff-129">Mesmo compartilhamentos que estão abertos muito "everyone" é normalmente não abrir toounauthenticated usuários.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="6c7ff-130">Fornece Olá senha quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-130">Supply hello password when prompted.</span></span> <span data-ttu-id="6c7ff-131">Uma saída de exemplo para instalar atualizações do hello primeira ordem é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="6c7ff-132">Para a primeira atualização de ordem Olá, é necessário toopoint toohello determinado arquivo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="6c7ff-133">Você deve instalar Olá _HcsSoftwareUpdate.exe_ primeiro.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="6c7ff-134">Após a conclusão dessa instalação, instale _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="6c7ff-135">Tipo **Y** quando tooconfirm solicitada Olá a instalação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="6c7ff-136">Monitorar atualização hello usando Olá `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="6c7ff-137">atualização de saudação primeiro será concluída em controlador passivo hello.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="6c7ff-138">Depois que o controlador passivo Olá é atualizado, haverá um failover e atualização hello, em seguida, será aplicada em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="6c7ff-139">atualização de saudação é concluída quando ambos os controladores de saudação são atualizados.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="6c7ff-140">Olá seguinte saída de exemplo mostra Olá atualização em andamento.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="6c7ff-141">Olá `RunInprogress` é `True` quando a atualização de saudação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="6c7ff-142">Olá saída de exemplo a seguir indica que a atualização Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="6c7ff-143">Olá `RunInProgress` é `False` quando a atualização de saudação é concluída.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="6c7ff-144">Ocasionalmente, Olá cmdlet relatórios `False` quando a atualização de saudação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="6c7ff-145">tooensure que Olá hotfix for concluída, aguarde alguns minutos, execute o comando novamente e verificar que Olá `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="6c7ff-146">Se for, Olá hotfix foi concluída.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="6c7ff-147">Após a conclusão da atualização de software Olá, verificar se as versões de software de sistema hello.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="6c7ff-148">Tipo:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="6c7ff-149">Você deve ver Olá versões a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="6c7ff-150">Se o número de versão Olá não for alterada após a aplicação de atualização de saudação, indica que esse hotfix Olá falhou tooapply.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="6c7ff-151">Caso isso aconteça, entre em contato com o [Suporte da Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="6c7ff-152">Você deve reiniciar o controlador ativo do hello via Olá `Restart-HcsController` Olá cmdlet antes de aplicar a próxima atualização.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="6c7ff-153">Repita as etapas de 3 a 6 tooinstall Olá _CisMDSAgentupdate.exe_ agente baixado tooyour _FirstOrderUpdate_ pasta.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="6c7ff-154">Repita as etapas 3 a 6 tooinstall Olá segundo atualizações da ordem.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="6c7ff-155">Para atualizações de segunda ordem, várias atualizações podem ser instaladas executando apenas Olá `Start-HcsHotfix cmdlet` e toohello pasta onde se encontram segundo atualizações da ordem.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="6c7ff-156">Olá cmdlet executará todas as atualizações de saudação disponíveis na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="6c7ff-157">Se uma atualização já estiver instalada, a lógica de atualização de saudação detectar que e não aplicar essa atualização.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="6c7ff-158">Depois que todos os hotfixes Olá estiverem instalados, use Olá `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="6c7ff-159">Olá versões devem ser:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="6c7ff-160">tooinstall e verifique se os hotfixes do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="6c7ff-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="6c7ff-161">Use atualizações de firmware de disco KB4037263 tooinstall.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="6c7ff-162">Essas atualizações precisam de interrupção e levar cerca de 30 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="6c7ff-163">Você pode escolher tooinstall em uma janela de manutenção planejada, console serial do dispositivo de toohello conexão.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="6c7ff-164">Se o firmware de disco já está atualizado, você não precisará tooinstall essas atualizações.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="6c7ff-165">Executar Olá `Get-HcsUpdateAvailability` de toocheck de console serial do dispositivo Olá se atualizações estiverem disponíveis e se Olá atualiza são interrompida (modo de manutenção) ou interrupções (modo normal) atualizações.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="6c7ff-166">atualizações de firmware de disco de saudação tooinstall, siga as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="6c7ff-167">Coloque o dispositivo de saudação no modo de manutenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="6c7ff-168">Não use a comunicação remota do Windows PowerShell ao conectar-se o dispositivo tooa no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="6c7ff-169">Em vez disso, execute este cmdlet no controlador de dispositivo hello quando conectados por meio do console serial do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="6c7ff-170">controlador de saudação tooplace no modo de manutenção, digite:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="6c7ff-171">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="6c7ff-172">Ambos os controladores Olá reinicie em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="6c7ff-173">atualização de firmware de disco de saudação do tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="6c7ff-174">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="6c7ff-175">Usando o monitor Olá instalar progresso `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="6c7ff-176">Olá atualização é concluída quando hello `RunInProgress` muda muito`False`.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="6c7ff-177">Após a conclusão da instalação hello, reinicia controlador Olá no qual Olá hotfix do modo de manutenção foi instalado.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="6c7ff-178">Faça logon como opção 1 com acesso completo e verifique se a versão de firmware de disco hello.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="6c7ff-179">Tipo:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="6c7ff-180">Olá esperado versões de firmware de disco são:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="6c7ff-181">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="6c7ff-182">Executar Olá `Get-HcsFirmwareVersion` comando Olá segundo controlador tooverify que Olá a versão do software foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="6c7ff-183">Em seguida, você pode sair do modo de manutenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="6c7ff-184">toodo, digite Olá comando para cada controlador de dispositivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c7ff-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="6c7ff-185">controladores de saudação reiniciar quando você sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="6c7ff-186">Depois de firmware de disco Olá atualizações são aplicadas com êxito e dispositivo Olá saiu do modo de manutenção, toohello retorno portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="6c7ff-187">Observe que esse portal Olá não pode mostrar que você instalou as atualizações do modo de manutenção Olá por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="6c7ff-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

