<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="a39fc-101">dispositivo de saudação tooconfigure e registrar</span><span class="sxs-lookup"><span data-stu-id="a39fc-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="a39fc-102">Acesse a interface do Windows PowerShell Olá no seu console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a39fc-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="a39fc-103">Consulte [console serial do dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="a39fc-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="a39fc-104">**Ser exatamente o procedimento de saudação toofollow-se ou não será capaz de tooaccess console de saudação.**</span><span class="sxs-lookup"><span data-stu-id="a39fc-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="a39fc-105">Na sessão de saudação que é aberta, pressione Enter de um tempo tooget um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a39fc-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span> 
3. <span data-ttu-id="a39fc-106">Será solicitada toochoose Olá idioma que você deseja tooset para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a39fc-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="a39fc-107">Especifique o idioma de saudação e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="a39fc-107">Specify hello language, and then press Enter.</span></span> 
   
    ![O StorSimple configura e registra o dispositivo 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="a39fc-109">No menu do console serial Olá que é apresentado, escolha toolog opção 1 em com acesso completo.</span><span class="sxs-lookup"><span data-stu-id="a39fc-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span> 
   
    ![Dispositivo de registro do StorSimple 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="a39fc-111">Execute Olá seguindo as etapas tooconfigure Olá mínima necessária as configurações de rede para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a39fc-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a39fc-112">Essas etapas de configuração necessário toobe realizada no controlador active de saudação do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="a39fc-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="a39fc-113">menu do console serial Olá indica o estado do controlador de saudação na mensagem de saudação do banner.</span><span class="sxs-lookup"><span data-stu-id="a39fc-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="a39fc-114">Se você não são conectar o controlador ativo toohello, desconecte e, em seguida, conecte-se o controlador ativo toohello.</span><span class="sxs-lookup"><span data-stu-id="a39fc-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="a39fc-115">No prompt de comando hello, digite sua senha.</span><span class="sxs-lookup"><span data-stu-id="a39fc-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="a39fc-116">senha do dispositivo padrão Olá é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="a39fc-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="a39fc-117">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a39fc-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="a39fc-118">Um Assistente de instalação será exibido toohelp você definir configurações de rede de saudação para dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a39fc-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="a39fc-119">Saudação de fonte de informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a39fc-119">Supply hello following information:</span></span> 
      
      * <span data-ttu-id="a39fc-120">Endereço IP da interface de rede DADOS 0</span><span class="sxs-lookup"><span data-stu-id="a39fc-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="a39fc-121">Máscara da sub-rede</span><span class="sxs-lookup"><span data-stu-id="a39fc-121">Subnet mask</span></span>
      * <span data-ttu-id="a39fc-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="a39fc-122">Gateway</span></span>
      * <span data-ttu-id="a39fc-123">Endereço IP do servidor DNS Primário</span><span class="sxs-lookup"><span data-stu-id="a39fc-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="a39fc-124">Endereço IP do servidor NTP Primário</span><span class="sxs-lookup"><span data-stu-id="a39fc-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a39fc-125">Você pode ter toowait por alguns minutos para máscara de sub-rede hello e toobe de configurações de DNS aplicado.</span><span class="sxs-lookup"><span data-stu-id="a39fc-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="a39fc-126">Opcionalmente, configure seu servidor proxy da Web.</span><span class="sxs-lookup"><span data-stu-id="a39fc-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="a39fc-127">Embora a configuração do proxy da Web seja opcional, saiba que se você usar um proxy da Web, só poderá configurá-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="a39fc-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="a39fc-128">Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="a39fc-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="a39fc-129">Pressione Ctrl + C tooexit Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a39fc-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="a39fc-130">Instale atualizações de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a39fc-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="a39fc-131">Use Olá seguir cmdlet tooset IPs em ambos os controladores de saudação:</span><span class="sxs-lookup"><span data-stu-id="a39fc-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="a39fc-132">No prompt de comando hello, execute `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="a39fc-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="a39fc-133">Você deve ser notificado de que há atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a39fc-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="a39fc-134">Execute `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="a39fc-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="a39fc-135">Você pode executar esse comando em qualquer nó.</span><span class="sxs-lookup"><span data-stu-id="a39fc-135">You can run this command on any node.</span></span> <span data-ttu-id="a39fc-136">Atualizações serão aplicadas no primeiro controlador de hello, controlador Olá realizará o failover e, em seguida, Olá atualizações serão aplicadas em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="a39fc-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="a39fc-137">Você pode monitorar o progresso de Olá Olá atualização executando `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="a39fc-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="a39fc-138">Olá seguinte saída de exemplo mostra Olá atualização em andamento.</span><span class="sxs-lookup"><span data-stu-id="a39fc-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="a39fc-139">Olá saída de exemplo a seguir indica que a atualização Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="a39fc-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="a39fc-140">Pode levar até horas too11 tooapply todas as atualizações, incluindo de Olá Olá atualizações do Windows.</span><span class="sxs-lookup"><span data-stu-id="a39fc-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>

8. <span data-ttu-id="a39fc-141">Depois que todos os hello atualizações são instaladas com êxito, execute hello seguinte cmdlet tooconfirm que Olá software atualizações foram aplicadas corretamente:</span><span class="sxs-lookup"><span data-stu-id="a39fc-141">After all hello updates are successfully installed, run hello following cmdlet tooconfirm that hello software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="a39fc-142">Você deve ver Olá versões a seguir:</span><span class="sxs-lookup"><span data-stu-id="a39fc-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="a39fc-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="a39fc-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="a39fc-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="a39fc-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="a39fc-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="a39fc-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="a39fc-146">Olá execução tooconfirm cmdlet que Olá atualização de firmware a seguir foi aplicada corretamente:</span><span class="sxs-lookup"><span data-stu-id="a39fc-146">Run hello following cmdlet tooconfirm that hello firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="a39fc-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="a39fc-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="a39fc-148">Olá firmware status deve ser **UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="a39fc-148">hello firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="a39fc-149">Execute Olá seguindo o portal do Microsoft Azure Government de cmdlet toopoint Olá dispositivo toohello (porque ele aponta pública portal clássico do Azure toohello por padrão).</span><span class="sxs-lookup"><span data-stu-id="a39fc-149">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="a39fc-150">Isso reiniciará os dois controladores.</span><span class="sxs-lookup"><span data-stu-id="a39fc-150">This will restart both controllers.</span></span> <span data-ttu-id="a39fc-151">É recomendável que você use duas sessões PuTTY toosimultaneously conectar tooboth controladores para que você possa ver quando cada controlador é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="a39fc-151">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="a39fc-152">Você verá uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="a39fc-152">You will see a confirmation message.</span></span> <span data-ttu-id="a39fc-153">Aceite o padrão de saudação (**Y**).</span><span class="sxs-lookup"><span data-stu-id="a39fc-153">Accept hello default (**Y**).</span></span>
11. <span data-ttu-id="a39fc-154">Olá execução após a instalação do cmdlet tooresume:</span><span class="sxs-lookup"><span data-stu-id="a39fc-154">Run hello following cmdlet tooresume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Retomar o assistente de instalação](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="a39fc-156">Quando você continuar a instalação, o assistente Olá será versão Olá Update 1 (que corresponde a tooversion 17469).</span><span class="sxs-lookup"><span data-stu-id="a39fc-156">When you resume setup, hello wizard will be hello Update 1 version (which corresponds tooversion 17469).</span></span> 
12. <span data-ttu-id="a39fc-157">Aceite as configurações de rede hello.</span><span class="sxs-lookup"><span data-stu-id="a39fc-157">Accept hello network settings.</span></span> <span data-ttu-id="a39fc-158">Você verá uma mensagem de validação depois que aceitar cada configuração.</span><span class="sxs-lookup"><span data-stu-id="a39fc-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="a39fc-159">Por motivos de segurança, senha de administrador de dispositivo de saudação expira após Olá primeira sessão, e você precisará toochange it agora.</span><span class="sxs-lookup"><span data-stu-id="a39fc-159">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="a39fc-160">Quando solicitado, forneça uma senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a39fc-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="a39fc-161">Uma senha de administrador do dispositivo válida deve ter entre 8 e 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a39fc-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="a39fc-162">Olá senha deve conter três das seguintes Olá: caracteres minúsculo, maiusculo, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="a39fc-162">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Dispositivo de registro do StorSimple 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="a39fc-164">a etapa final Olá no Assistente de instalação Olá registra seu dispositivo com hello serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="a39fc-164">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="a39fc-165">Para isso, você será necessário Olá a chave de registro de serviço que você obteve na [etapa 2: chave de registro de serviço Get hello](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="a39fc-165">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="a39fc-166">Depois que você fornecer a chave de registro de saudação, talvez seja necessário toowait 2 a 3 minutos antes de saudação dispositivo está registrado.</span><span class="sxs-lookup"><span data-stu-id="a39fc-166">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a39fc-167">Você pode pressionar Ctrl + C a qualquer assistente de instalação do tempo tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="a39fc-167">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="a39fc-168">Se você inseriu todas as configurações de rede de saudação (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="a39fc-168">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progresso do registro do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="a39fc-170">Depois de saudação dispositivo estiver registrado, uma chave de criptografia de dados de serviço será exibida.</span><span class="sxs-lookup"><span data-stu-id="a39fc-170">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="a39fc-171">Copie essa chave e salve-a em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="a39fc-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="a39fc-172">**Essa chave será exigida com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="a39fc-172">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="a39fc-173">Consulte também[segurança de StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre essa chave.</span><span class="sxs-lookup"><span data-stu-id="a39fc-173">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Dispositivo de registro do StorSimple 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="a39fc-175">texto de saudação toocopy da janela de console serial hello, basta selecionar o texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="a39fc-175">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="a39fc-176">Em seguida, você deve ser capaz de toopaste-la na área de transferência de saudação ou qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a39fc-176">You should then be able toopaste it in hello clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="a39fc-177">Não use Ctrl + a chave de criptografia de dados de serviço C toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="a39fc-177">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="a39fc-178">Usar Ctrl + C fará com que você tooexit Olá Assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="a39fc-178">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="a39fc-179">Como resultado, senha de administrador de dispositivo de saudação não será alterada e dispositivo Olá reverterá toohello senha de padrão.</span><span class="sxs-lookup"><span data-stu-id="a39fc-179">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
16. <span data-ttu-id="a39fc-180">Console serial da saudação de saída.</span><span class="sxs-lookup"><span data-stu-id="a39fc-180">Exit hello serial console.</span></span>
17. <span data-ttu-id="a39fc-181">Retornar toohello Portal do Azure governamental e concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a39fc-181">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="a39fc-182">Clique duas vezes em sua saudação do Gerenciador do StorSimple service tooaccess **início rápido** página.</span><span class="sxs-lookup"><span data-stu-id="a39fc-182">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="a39fc-183">Clique em **Exibir dispositivos conectados**.</span><span class="sxs-lookup"><span data-stu-id="a39fc-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="a39fc-184">Em Olá **dispositivos** , verifique se o dispositivo Olá conectou com êxito toohello serviço verificando o status de saudação.</span><span class="sxs-lookup"><span data-stu-id="a39fc-184">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="a39fc-185">status de saudação do dispositivo deve ser **Online**.</span><span class="sxs-lookup"><span data-stu-id="a39fc-185">hello device status should be **Online**.</span></span>
       
        ![Página dos Dispositivos StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="a39fc-187">Se o status do dispositivo Olá **Offline**, aguarde alguns minutos para Olá online toocome de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a39fc-187">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span> 
       
        <span data-ttu-id="a39fc-188">Se o dispositivo de saudação ainda está offline após alguns minutos, você precisará toomake-se de que seu firewall de rede foi configurado conforme descrito em [requisitos de rede para seu dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a39fc-188">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="a39fc-189">Verifique se a porta 9354 é aberta para comunicação de saída como isso é usado pelo barramento de serviço Olá para comunicação de serviço para o dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="a39fc-189">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager service-to-device communication.</span></span>

