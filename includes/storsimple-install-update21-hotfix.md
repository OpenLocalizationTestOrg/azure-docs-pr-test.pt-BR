<!--author=alkohli last changed: 05/19/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="1aca6-101">Para baixar os hotfixes</span><span class="sxs-lookup"><span data-stu-id="1aca6-101">To download hotfixes</span></span>
<span data-ttu-id="1aca6-102">Execute as etapas a seguir para baixar a atualização do software do Catálogo do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="1aca6-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="1aca6-103">Inicie o Internet Explorer e acesse [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1aca6-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="1aca6-104">Caso esta seja a primeira vez que você usa o Catálogo do Microsoft Update neste computador, clique em **Instalar** quando a instalação do complemento do Catálogo do Microsoft Update for solicitada.</span><span class="sxs-lookup"><span data-stu-id="1aca6-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="1aca6-105">![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="1aca6-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="1aca6-106">Na caixa de pesquisa do Catálogo do Microsoft Update, insira o número do KB (Base de Dados de Conhecimento) do hotfix que você quer baixar, por exemplo, **3179904** e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="1aca6-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="1aca6-107">A listagem de hotfixes aparece, por exemplo, **Atualização de pacote cumulativo de software 2.2 para a série 8000 do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="1aca6-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Pesquisar o catálogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="1aca6-109">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1aca6-109">Click **Add**.</span></span> <span data-ttu-id="1aca6-110">A atualização é adicionada ao carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="1aca6-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="1aca6-111">Pesquise quaisquer hotfixes adicionais relacionados na tabela acima (**3103616**, **3146621**) e adicione cada um deles ao carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="1aca6-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span></span>
6. <span data-ttu-id="1aca6-112">Clique em **Exibir carrinho**.</span><span class="sxs-lookup"><span data-stu-id="1aca6-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="1aca6-113">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="1aca6-113">Click **Download**.</span></span> <span data-ttu-id="1aca6-114">Especifique ou **Navegue** até o local em que deseja que o download apareça.</span><span class="sxs-lookup"><span data-stu-id="1aca6-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="1aca6-115">As atualizações são baixadas para o local especificado e colocadas em uma subpasta com o mesmo nome que a atualização.</span><span class="sxs-lookup"><span data-stu-id="1aca6-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="1aca6-116">A pasta também pode ser copiada para um compartilhamento de rede que seja acessível do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="1aca6-117">Os hotfixes devem estar acessíveis nos dois controladores para detectar mensagens de erro potenciais do controlador em par.</span><span class="sxs-lookup"><span data-stu-id="1aca6-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="1aca6-118">Para instalar e verificar os hotfixes do modo normal</span><span class="sxs-lookup"><span data-stu-id="1aca6-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="1aca6-119">Siga as etapas abaixo para instalar e verificar os hotfixes do modo normal.</span><span class="sxs-lookup"><span data-stu-id="1aca6-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="1aca6-120">Caso você já os tenha instalado usando o Portal do Azure, ignore essa etapa e vá para [Instalar e verificar hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="1aca6-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="1aca6-121">Para instalar os hotfixes, acesse a interface do Windows PowerShell no console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1aca6-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="1aca6-122">Siga as instruções detalhadas em [Usar o PuTTy para se conectar ao console serial do dispositivo](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="1aca6-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="1aca6-123">No prompt de comando, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1aca6-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="1aca6-124">Selecione a **Opção 1** para fazer logon no dispositivo com acesso completo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="1aca6-125">Recomendamos que você instale o hotfix no controlador passivo primeiro.</span><span class="sxs-lookup"><span data-stu-id="1aca6-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="1aca6-126">Para instalar o hotfix, no prompt de comando, digite:</span><span class="sxs-lookup"><span data-stu-id="1aca6-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1aca6-127">Use o IP em vez do DNS no caminho de compartilhamento no comando acima.</span><span class="sxs-lookup"><span data-stu-id="1aca6-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="1aca6-128">O parâmetro credential é usado somente para acessar um compartilhamento autenticado.</span><span class="sxs-lookup"><span data-stu-id="1aca6-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="1aca6-129">É recomendável usar o parâmetro de credencial para acessar compartilhamentos.</span><span class="sxs-lookup"><span data-stu-id="1aca6-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="1aca6-130">Até mesmo os compartilhamentos abertos para "todos" geralmente não são abertos para usuários não autenticados.</span><span class="sxs-lookup"><span data-stu-id="1aca6-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="1aca6-131">Forneça a senha, quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="1aca6-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="1aca6-132">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="1aca6-133">Digite **Y** quando solicitado a confirmar a instalação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="1aca6-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="1aca6-134">Se estiver instalando a Atualização 2.2, instale apenas o arquivo binário precedido por “all-hcsmdssoftwareudpate”.</span><span class="sxs-lookup"><span data-stu-id="1aca6-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="1aca6-135">Não instale a atualização do agente MDS e Cis precedido por all-cismdsagentupdatebundle.</span><span class="sxs-lookup"><span data-stu-id="1aca6-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="1aca6-136">Se você não fizer isso, receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="1aca6-136">Failure to do so will result in an error.</span></span> 

5. <span data-ttu-id="1aca6-137">Monitore a atualização usando o cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="1aca6-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="1aca6-138">Primeiro, a atualização será concluída no controlador passivo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="1aca6-139">Depois que o controlador passivo for atualizado, haverá um failover e a atualização será, então, aplicada no outro controlador.</span><span class="sxs-lookup"><span data-stu-id="1aca6-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="1aca6-140">A atualização é concluída quando ambos os controladores são atualizados.</span><span class="sxs-lookup"><span data-stu-id="1aca6-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="1aca6-141">A saída de exemplo a seguir mostra a atualização em andamento.</span><span class="sxs-lookup"><span data-stu-id="1aca6-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="1aca6-142">O `RunInprogress` será `True` quando a atualização estiver em andamento.</span><span class="sxs-lookup"><span data-stu-id="1aca6-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="1aca6-143">A saída de exemplo a seguir indica que a atualização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="1aca6-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="1aca6-144">O `RunInProgress` será `False` quando a atualização estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="1aca6-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="1aca6-145">Ocasionalmente, o cmdlet relatará `False` quando a atualização ainda estiver em andamento.</span><span class="sxs-lookup"><span data-stu-id="1aca6-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="1aca6-146">Para garantir que o hotfix seja concluído, aguarde alguns minutos, execute esse comando novamente e verifique se `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="1aca6-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="1aca6-147">Em caso positivo, o hotfix foi concluído.</span><span class="sxs-lookup"><span data-stu-id="1aca6-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="1aca6-148">Depois que a atualização do software estiver concluída, verifique as versões de software do sistema.</span><span class="sxs-lookup"><span data-stu-id="1aca6-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="1aca6-149">Digite:</span><span class="sxs-lookup"><span data-stu-id="1aca6-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="1aca6-150">Você deverá ver as seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="1aca6-150">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="1aca6-151">Se os números de versão não mudarem após a aplicação da atualização, isso indica que houve falha na aplicação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="1aca6-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="1aca6-152">Caso isso aconteça, entre em contato com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="1aca6-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="1aca6-153">Você deve reiniciar o controlador ativo por meio do cmdlet `Restart-HcsController` antes de aplicar as atualizações restantes.</span><span class="sxs-lookup"><span data-stu-id="1aca6-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="1aca6-154">Repita as etapas de 3 a 5 para instalar os hotfixes restantes do modo normal.</span><span class="sxs-lookup"><span data-stu-id="1aca6-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="1aca6-155">A atualização do iSCSI KB3146621</span><span class="sxs-lookup"><span data-stu-id="1aca6-155">The iSCSI update KB3146621</span></span>
   * <span data-ttu-id="1aca6-156">A atualização da WMI KB3103616</span><span class="sxs-lookup"><span data-stu-id="1aca6-156">The WMI update KB3103616</span></span>
3. <span data-ttu-id="1aca6-157">Ignore esta etapa se estiver atualizando da Atualização 2.</span><span class="sxs-lookup"><span data-stu-id="1aca6-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="1aca6-158">Se você estiver atualizando de uma versão anterior à Atualização 2, você também precisará baixar:</span><span class="sxs-lookup"><span data-stu-id="1aca6-158">If you are updating from a version prior to Update 2, you will also need to download:</span></span>

    - <span data-ttu-id="1aca6-159">O driver LSI KB3121900</span><span class="sxs-lookup"><span data-stu-id="1aca6-159">The LSI driver KB3121900</span></span>

    - <span data-ttu-id="1aca6-160">A atualização de Spaceport KB3090322</span><span class="sxs-lookup"><span data-stu-id="1aca6-160">The Spaceport update KB3090322</span></span>

    - <span data-ttu-id="1aca6-161">A atualização de Storport KB3080728</span><span class="sxs-lookup"><span data-stu-id="1aca6-161">The Storport update KB3080728</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="1aca6-162">Para instalar e verificar hotfixes do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="1aca6-162">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="1aca6-163">Use o KB3121899 para instalar atualizações de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="1aca6-163">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="1aca6-164">Estas são atualizações com interrupção e levam cerca de 30 minutos para ser concluídas.</span><span class="sxs-lookup"><span data-stu-id="1aca6-164">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="1aca6-165">Você pode optar por instalá-las em uma janela de manutenção planejada conectando-se ao console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="1aca6-166">Observe que, se o firmware de disco já estiver atualizado, você não precisará instalar essas atualizações.</span><span class="sxs-lookup"><span data-stu-id="1aca6-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="1aca6-167">Execute o cmdlet `Get-HcsUpdateAvailability` no console serial do dispositivo para verificar se as atualizações estão disponíveis e se elas são interruptivas (modo de manutenção) ou não interruptivas (modo normal).</span><span class="sxs-lookup"><span data-stu-id="1aca6-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="1aca6-168">Para instalar as atualizações de firmware de disco, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-168">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="1aca6-169">Coloque o dispositivo no Modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1aca6-169">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="1aca6-170">Observe que você não deve usar a comunicação remota do Windows PowerShell ao se conectar a um dispositivo no Modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1aca6-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="1aca6-171">Em vez disso, execute esse cmdlet no controlador do dispositivo quando conectado por meio do console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="1aca6-172">Digite:</span><span class="sxs-lookup"><span data-stu-id="1aca6-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="1aca6-173">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="1aca6-174">Em seguida, ambos os controladores são reiniciados no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1aca6-174">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="1aca6-175">Para instalar a atualização de firmware de disco, digite:</span><span class="sxs-lookup"><span data-stu-id="1aca6-175">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1aca6-176">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="1aca6-177">Monitore o progresso da instalação usando o comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="1aca6-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="1aca6-178">A atualização é concluída quando o `RunInProgress` muda para `False`.</span><span class="sxs-lookup"><span data-stu-id="1aca6-178">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="1aca6-179">Depois que a instalação for concluída, o controlador no qual o hotfix do modo de manutenção foi instalado será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="1aca6-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="1aca6-180">Faça logon como opção 1 com acesso completo e verifique a versão de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="1aca6-180">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="1aca6-181">Digite:</span><span class="sxs-lookup"><span data-stu-id="1aca6-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="1aca6-182">As versões de firmware de disco esperados são:</span><span class="sxs-lookup"><span data-stu-id="1aca6-182">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="1aca6-183">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1aca6-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="1aca6-184">Execute o comando `Get-HcsFirmwareVersion` no segundo controlador para verificar se a versão do software foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="1aca6-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="1aca6-185">Em seguida, você pode sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1aca6-185">You can then exit the maintenance mode.</span></span> <span data-ttu-id="1aca6-186">Para isso, digite o comando a seguir para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="1aca6-186">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="1aca6-187">Os controladores são reiniciados quando você sai do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1aca6-187">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="1aca6-188">Depois que as atualizações do firmware de disco forem aplicadas com êxito e o dispositivo tiver saído do modo de manutenção, retorne ao portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1aca6-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="1aca6-189">Observe que, por 24 horas, o portal poderá não mostrar que as atualizações do modo de manutenção foram instaladas.</span><span class="sxs-lookup"><span data-stu-id="1aca6-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

