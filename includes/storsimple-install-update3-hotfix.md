<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="ca6df-101">hotfixes toodownload</span><span class="sxs-lookup"><span data-stu-id="ca6df-101">toodownload hotfixes</span></span>
<span data-ttu-id="ca6df-102">Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ca6df-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="ca6df-103">Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ca6df-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="ca6df-104">Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ca6df-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="ca6df-105">![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="ca6df-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="ca6df-106">Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de saudação de saudação hotfix que você deseja toodownload, por exemplo **3186843**e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3186843**, and then click **Search**.</span></span>
   
    <span data-ttu-id="ca6df-107">Olá hotfix listagem aparece, por exemplo, **cumulativa 3.0 de atualização de pacote de Software para StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="ca6df-109">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-109">Click **Add**.</span></span> <span data-ttu-id="ca6df-110">atualização de saudação é adicionada toohello carrinho.</span><span class="sxs-lookup"><span data-stu-id="ca6df-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="ca6df-111">Procure os hotfixes adicionais listadas na tabela de saudação acima (**3186859**) e adicionar cada carrinho toohello.</span><span class="sxs-lookup"><span data-stu-id="ca6df-111">Search for any additional hotfixes listed in hello table above (**3186859**), and add each toohello basket.</span></span>
6. <span data-ttu-id="ca6df-112">Clique em **Exibir carrinho**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="ca6df-113">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-113">Click **Download**.</span></span> <span data-ttu-id="ca6df-114">Especifique ou **procurar** tooa local local onde você deseja Olá downloads tooappear.</span><span class="sxs-lookup"><span data-stu-id="ca6df-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="ca6df-115">Olá as atualizações são baixadas toohello local especificado e colocada em uma subpasta com mesmo nome como atualização de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="ca6df-115">hello updates are downloaded toohello specified location and placed in a sub-folder with hello same name as hello update.</span></span> <span data-ttu-id="ca6df-116">pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca6df-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="ca6df-117">Olá hotfixes deve ser acessíveis de ambos os toodetect controladores mensagens de qualquer erro em potencial do controlador de par de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca6df-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="ca6df-118">tooinstall e verifique se os hotfixes do modo normal</span><span class="sxs-lookup"><span data-stu-id="ca6df-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="ca6df-119">Executar Olá tooinstall as etapas a seguir e verifique se a hotfixes do modo normal.</span><span class="sxs-lookup"><span data-stu-id="ca6df-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="ca6df-120">Se você já instalou usando Olá Portal do Azure, vá em frente muito[instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="ca6df-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="ca6df-121">tooinstall Olá hotfixes, interface do acesso saudação do Windows PowerShell no seu console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ca6df-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="ca6df-122">Siga Olá detalhadas instruções [console serial do PuTTy Use tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ca6df-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="ca6df-123">No prompt de comando hello, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="ca6df-124">Selecione **opção 1** toolog toohello dispositivo com acesso completo.</span><span class="sxs-lookup"><span data-stu-id="ca6df-124">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="ca6df-125">É recomendável que você instale o hotfix Olá no controlador passivo Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="ca6df-125">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="ca6df-126">tooinstall Olá hotfix, no prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="ca6df-126">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="ca6df-127">Use o IP em vez de DNS no caminho de compartilhamento Olá acima de comando.</span><span class="sxs-lookup"><span data-stu-id="ca6df-127">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="ca6df-128">parâmetro de credencial de saudação é usado somente se você estiver acessando um compartilhamento autenticado.</span><span class="sxs-lookup"><span data-stu-id="ca6df-128">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="ca6df-129">É recomendável que você use compartilhamentos de tooaccess de parâmetro de credencial de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca6df-129">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="ca6df-130">Mesmo compartilhamentos que estão abertos muito "everyone" é normalmente não abrir toounauthenticated usuários.</span><span class="sxs-lookup"><span data-stu-id="ca6df-130">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="ca6df-131">Fornece Olá senha quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="ca6df-131">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="ca6df-132">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca6df-132">A sample output is shown below.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="ca6df-133">Tipo **Y** quando tooconfirm solicitada Olá a instalação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="ca6df-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="ca6df-134">Monitorar atualização hello usando Olá `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca6df-134">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="ca6df-135">atualização de saudação primeiro será concluída em controlador passivo hello.</span><span class="sxs-lookup"><span data-stu-id="ca6df-135">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="ca6df-136">Depois que o controlador passivo Olá é atualizado, haverá um failover e atualização hello, em seguida, será aplicada em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="ca6df-136">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="ca6df-137">atualização de saudação é concluída quando ambos os controladores de saudação são atualizados.</span><span class="sxs-lookup"><span data-stu-id="ca6df-137">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="ca6df-138">Olá seguinte saída de exemplo mostra Olá atualização em andamento.</span><span class="sxs-lookup"><span data-stu-id="ca6df-138">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="ca6df-139">Olá `RunInprogress` será `True` quando a atualização de saudação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="ca6df-139">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="ca6df-140">Olá saída de exemplo a seguir indica que a atualização Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="ca6df-140">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="ca6df-141">Olá `RunInProgress` será `False` quando a atualização de saudação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="ca6df-141">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="ca6df-142">Ocasionalmente, Olá cmdlet relatórios `False` quando a atualização de saudação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="ca6df-142">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="ca6df-143">tooensure que Olá hotfix for concluída, aguarde alguns minutos, execute o comando novamente e verificar que Olá `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="ca6df-143">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="ca6df-144">Se for, Olá hotfix foi concluída.</span><span class="sxs-lookup"><span data-stu-id="ca6df-144">If it is, then hello hotfix has completed.</span></span>

1. <span data-ttu-id="ca6df-145">Após a conclusão da atualização de software Olá, verificar se as versões de software de sistema hello.</span><span class="sxs-lookup"><span data-stu-id="ca6df-145">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="ca6df-146">Tipo:</span><span class="sxs-lookup"><span data-stu-id="ca6df-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="ca6df-147">Você deve ver Olá versões a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca6df-147">You should see hello following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     <span data-ttu-id="ca6df-148">Se números de versão de saudação não serão alterados após a aplicação de atualização de hello, indica que esse hotfix Olá falhou tooapply.</span><span class="sxs-lookup"><span data-stu-id="ca6df-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="ca6df-149">Caso isso aconteça, entre em contato com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="ca6df-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ca6df-150">Você deve reiniciar o controlador ativo do hello via Olá `Restart-HcsController` cmdlet antes de aplicar Olá restantes atualizações.</span><span class="sxs-lookup"><span data-stu-id="ca6df-150">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="ca6df-151">Repita as etapas 3 a 5 driver de saudação LSI tooinstall e firmware hotfix **KB3186859**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-151">Repeat steps 3-5 tooinstall hello LSI driver and firmware hotfix **KB3186859**.</span></span> <span data-ttu-id="ca6df-152">Após a instalação do hotfix hello, use Olá `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca6df-152">After hello hotfix is installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="ca6df-153">Olá LSI versão deve ser:</span><span class="sxs-lookup"><span data-stu-id="ca6df-153">hello LSI version should be:</span></span>
   
   * `Lsisas2Version: 2.0.78.00`
3. <span data-ttu-id="ca6df-154">Repita as etapas 3 a 5 tooinstall Olá Storport e atualização Spaceport **KB3121261**.</span><span class="sxs-lookup"><span data-stu-id="ca6df-154">Repeat steps 3-5 tooinstall hello Storport and Spaceport update **KB3121261**.</span></span>
4. <span data-ttu-id="ca6df-155">Se você estiver atualizando de atualização 2 ou versão anterior, você também precisará toodownload:</span><span class="sxs-lookup"><span data-stu-id="ca6df-155">If you are updating from Update 2 or earlier version, you will also need toodownload:</span></span>
   
   * <span data-ttu-id="ca6df-156">Correção de iSCSI usando o KB3146621</span><span class="sxs-lookup"><span data-stu-id="ca6df-156">iSCSI fix using KB3146621</span></span>
   * <span data-ttu-id="ca6df-157">Correção de WMI usando o KB3103616</span><span class="sxs-lookup"><span data-stu-id="ca6df-157">WMI fix using KB3103616</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="ca6df-158">tooinstall e verifique se os hotfixes do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="ca6df-158">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="ca6df-159">Use atualizações de firmware de disco KB3121899 tooinstall.</span><span class="sxs-lookup"><span data-stu-id="ca6df-159">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="ca6df-160">Essas atualizações precisam de interrupção e levar cerca de 30 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ca6df-160">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="ca6df-161">Você pode escolher tooinstall em uma janela de manutenção planejada, console serial do dispositivo de toohello conexão.</span><span class="sxs-lookup"><span data-stu-id="ca6df-161">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="ca6df-162">Observe que se o firmware de disco já está atualizado, você não precisará tooinstall essas atualizações.</span><span class="sxs-lookup"><span data-stu-id="ca6df-162">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="ca6df-163">Executar Olá `Get-HcsUpdateAvailability` de toocheck de console serial do dispositivo Olá se atualizações estiverem disponíveis e se Olá atualiza são interrompida (modo de manutenção) ou interrupções (modo normal) atualizações.</span><span class="sxs-lookup"><span data-stu-id="ca6df-163">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="ca6df-164">atualizações de firmware de disco de saudação tooinstall, siga as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca6df-164">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="ca6df-165">Coloque o dispositivo de saudação no modo de manutenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca6df-165">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="ca6df-166">Observe que você não deve usar o Windows PowerShell remoto ao conectar-se o dispositivo tooa no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="ca6df-166">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="ca6df-167">Em vez disso, execute este cmdlet no controlador de dispositivo hello quando conectados por meio do console serial do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ca6df-167">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="ca6df-168">Tipo:</span><span class="sxs-lookup"><span data-stu-id="ca6df-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="ca6df-169">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca6df-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="ca6df-170">Ambos os controladores Olá reinicie em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="ca6df-170">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="ca6df-171">atualização de firmware de disco de saudação do tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="ca6df-171">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="ca6df-172">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca6df-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="ca6df-173">Usando o monitor Olá instalar progresso `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="ca6df-173">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="ca6df-174">Olá atualização é concluída quando hello `RunInProgress` muda muito`False`.</span><span class="sxs-lookup"><span data-stu-id="ca6df-174">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="ca6df-175">Após a conclusão da instalação hello, reinicia controlador Olá no qual Olá hotfix do modo de manutenção foi instalado.</span><span class="sxs-lookup"><span data-stu-id="ca6df-175">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="ca6df-176">Faça logon como opção 1 com acesso completo e verifique se a versão de firmware de disco hello.</span><span class="sxs-lookup"><span data-stu-id="ca6df-176">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="ca6df-177">Tipo:</span><span class="sxs-lookup"><span data-stu-id="ca6df-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="ca6df-178">Olá esperado versões de firmware de disco são:</span><span class="sxs-lookup"><span data-stu-id="ca6df-178">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="ca6df-179">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca6df-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="ca6df-180">Executar Olá `Get-HcsFirmwareVersion` comando Olá segundo controlador tooverify que Olá a versão do software foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="ca6df-180">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="ca6df-181">Em seguida, você pode sair do modo de manutenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca6df-181">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="ca6df-182">toodo, digite Olá comando para cada controlador de dispositivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca6df-182">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="ca6df-183">controladores de saudação reiniciar quando você sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="ca6df-183">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="ca6df-184">Depois de firmware de disco Olá atualizações são aplicadas com êxito e dispositivo Olá saiu do modo de manutenção, toohello retorno portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca6df-184">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="ca6df-185">Observe que esse portal Olá não pode mostrar que você instalou as atualizações do modo de manutenção Olá por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ca6df-185">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

