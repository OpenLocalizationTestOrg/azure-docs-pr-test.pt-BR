<!--author=SharS last changed: 02/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="53692-101">Para configurar e registrar o dispositivo</span><span class="sxs-lookup"><span data-stu-id="53692-101">To configure and register the device</span></span>
1. <span data-ttu-id="53692-102">Acesse a interface do Windows PowerShell no console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="53692-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="53692-103">Consulte [Usar o PuTTY para se conectar ao console serial do dispositivo](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="53692-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="53692-104">**Siga o procedimento corretamente ou você não conseguirá acessar o console.**</span><span class="sxs-lookup"><span data-stu-id="53692-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="53692-105">Na sessão que é aberta, pressione Enter uma vez para obter um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="53692-105">In the session that opens up, press Enter one time to get a command prompt.</span></span>
3. <span data-ttu-id="53692-106">Você deverá escolher o idioma que deseja definir para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53692-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="53692-107">Especifique o idioma e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="53692-107">Specify the language, and then press Enter.</span></span>
   
    ![O StorSimple configura e registra o dispositivo 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="53692-109">No menu do console serial apresentado, escolha a opção 1 para efetuar logon com acesso completo.</span><span class="sxs-lookup"><span data-stu-id="53692-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![Dispositivo de registro do StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="53692-111">Conclua as etapas a seguir para definir as configurações de rede necessárias e mínimas para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53692-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="53692-112">Essas etapas de configuração devem ser executadas no controlador ativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53692-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="53692-113">O menu do console serial indica o estado do controlador na mensagem de faixa.</span><span class="sxs-lookup"><span data-stu-id="53692-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="53692-114">Se você não estiver conectado ao controlador ativo, desconecte e conecte-se ao controlador ativo.</span><span class="sxs-lookup"><span data-stu-id="53692-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="53692-115">No prompt de comando, digite sua senha.</span><span class="sxs-lookup"><span data-stu-id="53692-115">At the command prompt, type your password.</span></span> <span data-ttu-id="53692-116">A senha do dispositivo padrão é **Senha1**.</span><span class="sxs-lookup"><span data-stu-id="53692-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="53692-117">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="53692-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="53692-118">Um assistente de instalação aparecerá para ajudá-lo a configurar as definições da rede para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53692-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="53692-119">Forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="53692-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="53692-120">Endereço IP da interface de rede DADOS 0</span><span class="sxs-lookup"><span data-stu-id="53692-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="53692-121">Máscara da sub-rede</span><span class="sxs-lookup"><span data-stu-id="53692-121">Subnet mask</span></span>
      * <span data-ttu-id="53692-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="53692-122">Gateway</span></span>
      * <span data-ttu-id="53692-123">Endereço IP do servidor DNS Primário</span><span class="sxs-lookup"><span data-stu-id="53692-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="53692-124">Endereço IP do servidor NTP Primário</span><span class="sxs-lookup"><span data-stu-id="53692-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="53692-125">Você terá que aguardar alguns minutos para que a máscara de sub-rede e as configurações de DNS sejam aplicadas.</span><span class="sxs-lookup"><span data-stu-id="53692-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="53692-126">Opcionalmente, configure seu servidor proxy da Web.</span><span class="sxs-lookup"><span data-stu-id="53692-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="53692-127">Embora a configuração do proxy da Web seja opcional, saiba que se você usar um proxy da Web, só poderá configurá-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="53692-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="53692-128">Para obter mais informações, visite [Configurar proxy da Web para seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="53692-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="53692-129">Pressione Ctrl + C para sair do assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="53692-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="53692-130">Instale as atualizações da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="53692-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="53692-131">Use o seguinte cmdlet para definir IPs em ambos os controladores:</span><span class="sxs-lookup"><span data-stu-id="53692-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="53692-132">No prompt de comando, execute `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="53692-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="53692-133">Você deve ser notificado de que há atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="53692-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="53692-134">Execute `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="53692-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="53692-135">Você pode executar esse comando em qualquer nó.</span><span class="sxs-lookup"><span data-stu-id="53692-135">You can run this command on any node.</span></span> <span data-ttu-id="53692-136">As atualizações serão aplicadas ao primeiro controlador, o controlador realizará failover e, em seguida, as atualizações serão aplicadas ao outro controlador.</span><span class="sxs-lookup"><span data-stu-id="53692-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="53692-137">Você pode monitorar o progresso da atualização executando `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="53692-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="53692-138">A saída de exemplo a seguir mostra a atualização em andamento.</span><span class="sxs-lookup"><span data-stu-id="53692-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="53692-139">A saída de exemplo a seguir indica que a atualização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="53692-139">The following sample output indicates that the update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="53692-140">Pode levar até 11 horas para que todas as atualizações sejam aplicadas, incluindo as atualizações do Windows.</span><span class="sxs-lookup"><span data-stu-id="53692-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>
8. <span data-ttu-id="53692-141">Execute o cmdlet a seguir para apontar o dispositivo para o portal do Microsoft Azure Governamental (já que ele aponta para o portal clássico do Azure público por padrão).</span><span class="sxs-lookup"><span data-stu-id="53692-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="53692-142">Isso reiniciará os dois controladores.</span><span class="sxs-lookup"><span data-stu-id="53692-142">This will restart both controllers.</span></span> <span data-ttu-id="53692-143">É recomendável que você use duas sessões PuTTY para se conectar simultaneamente a ambos os controladores para poder ver quando cada controlador for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="53692-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="53692-144">Você verá uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="53692-144">You will see a confirmation message.</span></span> <span data-ttu-id="53692-145">Aceite o padrão (**Y**).</span><span class="sxs-lookup"><span data-stu-id="53692-145">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="53692-146">Execute o seguinte cmdlet para retomar a instalação:</span><span class="sxs-lookup"><span data-stu-id="53692-146">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Retomar o assistente de instalação](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="53692-148">Quando você retomar a instalação, o assistente será a versão de Atualização 2.</span><span class="sxs-lookup"><span data-stu-id="53692-148">When you resume setup, the wizard will be the Update 2 version.</span></span>
10. <span data-ttu-id="53692-149">Aceite as configurações de rede.</span><span class="sxs-lookup"><span data-stu-id="53692-149">Accept the network settings.</span></span> <span data-ttu-id="53692-150">Você verá uma mensagem de validação depois que aceitar cada configuração.</span><span class="sxs-lookup"><span data-stu-id="53692-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="53692-151">Por motivos de segurança, a senha de administrador do dispositivo expira após a primeira sessão, e você precisará alterá-la agora.</span><span class="sxs-lookup"><span data-stu-id="53692-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="53692-152">Quando solicitado, forneça uma senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53692-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="53692-153">Uma senha de administrador do dispositivo válida deve ter entre 8 e 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="53692-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="53692-154">A senha deve conter três das seguintes opções: caracteres com letras minúsculas e maiúsculas, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="53692-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Dispositivo de registro do StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="53692-156">A etapa final do assistente de instalação registra seu dispositivo no serviço Gerenciador StorSimple.</span><span class="sxs-lookup"><span data-stu-id="53692-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="53692-157">Para isso, será necessária a chave de registro do serviço obtida na [Etapa 2: Obter a chave de registro](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="53692-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="53692-158">Depois de fornecer a chave de registro, talvez seja necessário aguardar de 2 a 3 minutos antes do dispositivo ser registrado.</span><span class="sxs-lookup"><span data-stu-id="53692-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="53692-159">Você pode pressionar Ctrl + C a qualquer momento para sair do assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="53692-159">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="53692-160">Se você tiver inserido todas as configurações de rede (endereço IP para Dados 0, Máscara de sub-rede e Gateway), as entradas serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="53692-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progresso do registro do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="53692-162">Depois do dispositivo ser registrado, uma chave de Criptografia de Dados do Serviço será exibida.</span><span class="sxs-lookup"><span data-stu-id="53692-162">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="53692-163">Copie essa chave e salve-a em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="53692-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="53692-164">**Essa chave será necessária com a chave de registro do serviço para registrar dispositivos adicionais no serviço Gerenciador StorSimple.**</span><span class="sxs-lookup"><span data-stu-id="53692-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="53692-165">Consulte a [segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre essa chave.</span><span class="sxs-lookup"><span data-stu-id="53692-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Dispositivo de registro do StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="53692-167">Para copiar o texto da janela do console serial, basta selecionar o texto.</span><span class="sxs-lookup"><span data-stu-id="53692-167">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="53692-168">Então, você conseguirá colá-lo na área de transferência ou em qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="53692-168">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="53692-169">NÃO use Ctrl + C para copiar a chave de criptografia de dados do serviço.</span><span class="sxs-lookup"><span data-stu-id="53692-169">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="53692-170">Usar Ctrl + C fará com que você saia do assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="53692-170">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="53692-171">Como resultado, a senha de administrador do dispositivo não será alterada, e o dispositivo voltará para a senha padrão.</span><span class="sxs-lookup"><span data-stu-id="53692-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
14. <span data-ttu-id="53692-172">Saia do console serial.</span><span class="sxs-lookup"><span data-stu-id="53692-172">Exit the serial console.</span></span>
15. <span data-ttu-id="53692-173">Volte para o Portal do Azure Governamental e conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="53692-173">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="53692-174">Clique duas vezes no serviço Gerenciador StorSimple para acessar a página **Início Rápido** .</span><span class="sxs-lookup"><span data-stu-id="53692-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="53692-175">Clique em **Exibir dispositivos conectados**.</span><span class="sxs-lookup"><span data-stu-id="53692-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="53692-176">Na página **Dispositivos** , verifique se o dispositivo conectou com êxito o serviço pesquisando o status.</span><span class="sxs-lookup"><span data-stu-id="53692-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="53692-177">O status do dispositivo deve ser **Online**.</span><span class="sxs-lookup"><span data-stu-id="53692-177">The device status should be **Online**.</span></span>
       
        ![Página dos Dispositivos StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="53692-179">Se o status do dispositivo for **Offline**, aguarde alguns minutos para o dispositivo ficar online.</span><span class="sxs-lookup"><span data-stu-id="53692-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="53692-180">Se o dispositivo continuar offline após alguns minutos, você precisará se certificar de que a rede do firewall foi configurada conforme descrito nos [requisitos de rede para seu dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="53692-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="53692-181">Verifique se a porta 9354 está aberta para comunicações de saída, pois ela é usada pelo barramento de serviço para a comunicação serviço-dispositivo do StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="53692-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span></span>

