<!--author=SharS last changed: 03/17/2016-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="7cfe0-101">Para baixar os hotfixes</span><span class="sxs-lookup"><span data-stu-id="7cfe0-101">To download hotfixes</span></span>
<span data-ttu-id="7cfe0-102">Execute as etapas a seguir para baixar a atualização do software.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-102">Perform the following steps to download the software update.</span></span>

1. <span data-ttu-id="7cfe0-103">Inicie o Internet Explorer e acesse [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7cfe0-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="7cfe0-104">Caso esta seja a primeira vez que você usa o Catálogo do Microsoft Update neste computador, clique em **Instalar** quando a instalação do complemento do Catálogo do Microsoft Update for solicitada.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="7cfe0-105">![Instalar o catálogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="7cfe0-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="7cfe0-106">Na caixa de pesquisa do Catálogo do Microsoft Update, insira o número do KB (Base de Dados de Conhecimento) do hotfix que você quer baixar, por exemplo, **3063418** e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="7cfe0-107">Você verá o pacote **StorSimple Update 1.2 Appliance Update** .</span><span class="sxs-lookup"><span data-stu-id="7cfe0-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="7cfe0-108">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-108">Click **Add**.</span></span> <span data-ttu-id="7cfe0-109">A atualização será adicionada ao carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-109">The update will be added to the basket.</span></span>
5. <span data-ttu-id="7cfe0-110">Pesquise quaisquer hotfixes adicionais listados na tabela acima (**3043005** e **3063416**) e adicione cada um deles ao carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span></span>
6. <span data-ttu-id="7cfe0-111">Clique em **Exibir carrinho**.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-111">Click **View Basket**.</span></span>
   
    ![Exibir carrinho](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="7cfe0-113">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-113">Click **Download**.</span></span> <span data-ttu-id="7cfe0-114">Especifique ou **Procure** a localização em que deseja que o download apareça.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="7cfe0-115">As atualizações são baixadas para o local especificado e colocadas em uma subpasta com o mesmo nome que a atualização.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="7cfe0-116">A pasta também pode ser copiada para um compartilhamento de rede que seja acessível do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="7cfe0-117">Os hotfixes devem estar acessíveis nos dois controladores para detectar mensagens de erro potenciais do controlador em par.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="7cfe0-118">Para instalar e verificar os hotfixes do modo normal</span><span class="sxs-lookup"><span data-stu-id="7cfe0-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="7cfe0-119">Realize as etapas a seguir para instalar e verificar os hotfixes do modo normal.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-119">Perform the following steps to install and verify the regular-mode hotfixes.</span></span> <span data-ttu-id="7cfe0-120">Caso você já os tenha instalado usando o Portal do Azure, ignore essa etapa e vá para [Instalar e verificar hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="7cfe0-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="7cfe0-121">Para instalar a atualização do software, acesse a interface do Windows PowerShell no console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="7cfe0-122">Siga as instruções detalhadas em [Usar o PuTTy para se conectar ao console serial do dispositivo](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="7cfe0-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="7cfe0-123">No prompt de comando, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="7cfe0-124">Selecione a **Opção 1** para fazer logon no dispositivo com acesso completo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="7cfe0-125">Para instalar o pacote de atualização, no prompt de comando, digite:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-125">To install the update package, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="7cfe0-126">Use o IP em vez do DNS no caminho de compartilhamento no comando acima.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="7cfe0-127">O parâmetro credential é usado somente para acessar um compartilhamento autenticado.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="7cfe0-128">É recomendável usar o parâmetro de credencial para acessar compartilhamentos.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="7cfe0-129">Até mesmo os compartilhamentos abertos para "todos" geralmente não são abertos para usuários não autenticados.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="7cfe0-130">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="7cfe0-131">Digite **Y** quando solicitado a confirmar a instalação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="7cfe0-132">Monitore a atualização usando o cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="7cfe0-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="7cfe0-133">A saída de exemplo a seguir mostra a atualização em andamento.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="7cfe0-134">O `RunInprogress` será `True` quando a atualização estiver em andamento.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="7cfe0-135">A saída de exemplo a seguir indica que a atualização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="7cfe0-136">O `RunInProgress` será `False` quando a atualização estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-136">The `RunInProgress` will be `False` when the update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7cfe0-137">Ocasionalmente, o cmdlet relatará `False` quando a atualização ainda estiver em andamento.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="7cfe0-138">Para garantir que o hotfix seja concluído, aguarde alguns minutos, execute esse comando novamente e verifique se `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="7cfe0-139">Em caso positivo, o hotfix foi concluído.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-139">If it is, then the hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="7cfe0-140">Depois que a atualização do software estiver concluída, verifique as versões de software do sistema.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-140">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="7cfe0-141">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-141">Type the following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="7cfe0-142">Você deverá ver as seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="7cfe0-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="7cfe0-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="7cfe0-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="7cfe0-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="7cfe0-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="7cfe0-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="7cfe0-146">Se os números de versão não mudarem após a aplicação da atualização, isso indica que houve falha na aplicação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="7cfe0-147">Caso isso aconteça, entre em contato com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="7cfe0-148">Repita as etapas 3 a 5 para instalar o hotfix do modo normal restante (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="7cfe0-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="7cfe0-149">Para instalar e verificar hotfixes do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="7cfe0-149">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="7cfe0-150">Use a KB3063416 para instalar atualizações de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-150">Use KB3063416 to install disk firmware updates.</span></span> <span data-ttu-id="7cfe0-151">Estas são atualizações interrompidas e levam cerca de 30 a 45 minutos para ser concluídas.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-151">These are disruptive updates and take around 30-45 minutes to complete.</span></span> <span data-ttu-id="7cfe0-152">Você pode optar por instalá-las em uma janela de manutenção planejada conectando-se ao console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="7cfe0-153">Para instalar as atualizações de firmware de disco, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-153">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="7cfe0-154">Coloque o dispositivo no modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-154">Place the device in Maintenance mode.</span></span> <span data-ttu-id="7cfe0-155">Observe que você não deve usar a comunicação remota do Windows PowerShell ao se conectar a um dispositivo no Modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="7cfe0-156">Você precisará executar esse cmdlet no controlador de dispositivo quando conectado por meio do console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="7cfe0-157">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="7cfe0-158">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="7cfe0-159">Em seguida, ambos os controladores são reiniciados no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-159">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="7cfe0-160">Para instalar a atualização de firmware de disco, digite:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-160">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="7cfe0-161">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="7cfe0-162">Monitore o progresso da instalação usando o comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="7cfe0-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="7cfe0-163">A atualização é concluída quando o `RunInProgress` muda para `False`.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-163">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="7cfe0-164">Depois que a instalação for concluída, o controlador no qual o hotfix do modo de manutenção foi instalado será reinicializado.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="7cfe0-165">Faça logon como opção 1 com acesso completo e verifique a versão de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-165">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="7cfe0-166">Digite:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="7cfe0-167">As versões de firmware de disco esperados são:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-167">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="7cfe0-168">Execute o comando `Get-HcsFirmwareVersion` no segundo controlador para verificar se a versão do software foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="7cfe0-169">Em seguida, você pode sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-169">You can then exit the maintenance mode.</span></span> <span data-ttu-id="7cfe0-170">Digite o comando a seguir para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7cfe0-170">Type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="7cfe0-171">Os controladores são reiniciados quando você sai do modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-171">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="7cfe0-172">Depois que as atualizações do firmware de disco forem aplicadas com êxito e o dispositivo tiver saído do modo de manutenção, retorne ao portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="7cfe0-173">Observe que, por 24 horas, o portal poderá não mostrar que as atualizações do modo de manutenção foram instaladas.</span><span class="sxs-lookup"><span data-stu-id="7cfe0-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

