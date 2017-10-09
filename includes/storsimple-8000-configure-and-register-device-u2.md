<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="89711-101">dispositivo de saudação tooconfigure e registrar</span><span class="sxs-lookup"><span data-stu-id="89711-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="89711-102">Acesse a interface do Windows PowerShell Olá no seu console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="89711-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="89711-103">Consulte [console serial do dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="89711-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="89711-104">**Ser exatamente o procedimento de saudação toofollow-se ou não será capaz de tooaccess console de saudação.**</span><span class="sxs-lookup"><span data-stu-id="89711-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="89711-105">Na sessão de saudação que é aberta, pressione **Enter** tooget de tempo de um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="89711-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="89711-106">Será solicitada toochoose Olá idioma que você deseja tooset para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89711-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="89711-107">Especificar o idioma de saudação e, em seguida, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="89711-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="89711-108">No menu do console serial Olá que é apresentado, escolha a opção 1 muito**entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="89711-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="89711-109">Conclua as etapas 5-12 tooconfigure Olá mínima necessária as configurações de rede para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89711-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="89711-110">**Essas etapas de configuração necessário toobe realizada no controlador active de saudação do dispositivo Olá.**</span><span class="sxs-lookup"><span data-stu-id="89711-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="89711-111">menu do console serial Olá indica o estado do controlador de saudação na mensagem de saudação do banner.</span><span class="sxs-lookup"><span data-stu-id="89711-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="89711-112">Se você não estiver conectado toohello de controlador ativo, desconecte e, em seguida, conecte-se o controlador ativo toohello.</span><span class="sxs-lookup"><span data-stu-id="89711-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="89711-113">No prompt de comando hello, digite sua senha.</span><span class="sxs-lookup"><span data-stu-id="89711-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="89711-114">senha do dispositivo padrão Olá é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="89711-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="89711-115">Saudação de tipo comando a seguir: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="89711-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="89711-116">Um Assistente de instalação será exibido toohelp você definir configurações de rede de saudação para dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="89711-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="89711-117">Forneça Olá Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="89711-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="89711-118">Endereço IP hello dados 0 interface de rede</span><span class="sxs-lookup"><span data-stu-id="89711-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="89711-119">Máscara da sub-rede</span><span class="sxs-lookup"><span data-stu-id="89711-119">Subnet mask</span></span>
   * <span data-ttu-id="89711-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="89711-120">Gateway</span></span>
   * <span data-ttu-id="89711-121">Endereço IP do servidor DNS Primário</span><span class="sxs-lookup"><span data-stu-id="89711-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="89711-122">Veja abaixo um exemplo de saída.</span><span class="sxs-lookup"><span data-stu-id="89711-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="89711-123">Olá precede a saída de exemplo, você pode ver que sistema hello está validando as configurações de rede depois de cada etapa no processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="89711-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="89711-124">Você pode ter toowait por alguns minutos para máscara de sub-rede hello e toobe de configurações de DNS Olá aplicado.</span><span class="sxs-lookup"><span data-stu-id="89711-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="89711-125">Se você receber uma mensagem de erro de "Verificação Olá rede conectividade tooData 0", verifique a conexão de rede física Olá na interface de rede 0 de dados de saudação do seu controlador ativo.</span><span class="sxs-lookup"><span data-stu-id="89711-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="89711-126">(Opcional) configure seu servidor proxy da Web.</span><span class="sxs-lookup"><span data-stu-id="89711-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="89711-127">Embora a configuração do proxy da Web seja opcional, **saiba que se você usar um proxy da Web, poderá apenas configurá-lo aqui**.</span><span class="sxs-lookup"><span data-stu-id="89711-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="89711-128">Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="89711-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="89711-129">Configure um servidor NTP primário para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89711-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="89711-130">Os servidores NTP são necessários, pois seu dispositivo deve sincronizar a hora para que ele possa se autenticar com seus provedores de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="89711-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="89711-131">Certifique-se de que sua rede permite toopass de tráfego NTP do toohello seu data center da Internet.</span><span class="sxs-lookup"><span data-stu-id="89711-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="89711-132">Se isso não for possível, especifique um servidor NTP interno.</span><span class="sxs-lookup"><span data-stu-id="89711-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="89711-133">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="89711-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="89711-134">Por motivos de segurança, senha de administrador de dispositivo de saudação expira após Olá primeira sessão, e você precisará toochange it agora.</span><span class="sxs-lookup"><span data-stu-id="89711-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="89711-135">Quando solicitado, forneça uma senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89711-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="89711-136">Uma senha de administrador do dispositivo válida deve ter entre 8 e 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="89711-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="89711-137">Olá senha deve conter três das seguintes Olá: caracteres minúsculo, maiusculo, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="89711-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="89711-138">a etapa final Olá no Assistente de instalação Olá registra seu dispositivo com hello serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="89711-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="89711-139">Para isso, você precisará Olá chave de registro que você obteve na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="89711-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="89711-140">Depois que você fornecer a chave de registro de saudação, talvez seja necessário toowait 2 a 3 minutos antes de saudação dispositivo está registrado.</span><span class="sxs-lookup"><span data-stu-id="89711-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="89711-141">Você pode pressionar Ctrl + C a qualquer assistente de instalação do tempo tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="89711-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="89711-142">Se você inseriu todas as configurações de rede de saudação (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="89711-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="89711-143">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="89711-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="89711-144">Depois de saudação dispositivo estiver registrado, uma chave de criptografia de dados de serviço será exibida.</span><span class="sxs-lookup"><span data-stu-id="89711-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="89711-145">Copie essa chave e salve-a em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="89711-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="89711-146">**Essa chave será exigida com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço do Gerenciador de dispositivos do StorSimple.**</span><span class="sxs-lookup"><span data-stu-id="89711-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="89711-147">Consulte também[segurança de StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre essa chave.</span><span class="sxs-lookup"><span data-stu-id="89711-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Dispositivo de registro do StorSimple 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="89711-149">texto de saudação toocopy da janela de console serial hello, basta selecionar o texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="89711-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="89711-150">Em seguida, você deve ser capaz de toopaste-la na área de transferência de saudação ou qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="89711-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="89711-151">Não use Ctrl + a chave de criptografia de dados de serviço C toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="89711-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="89711-152">Usar Ctrl + C fará com que você tooexit Olá Assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="89711-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="89711-153">Como resultado, senha de administrador de dispositivo de saudação não será alterada e dispositivo Olá reverterá toohello senha de padrão.</span><span class="sxs-lookup"><span data-stu-id="89711-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="89711-154">Console serial da saudação de saída.</span><span class="sxs-lookup"><span data-stu-id="89711-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="89711-155">Retorno toohello portal do Azure e Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="89711-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="89711-156">Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="89711-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="89711-157">Clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="89711-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="89711-158">No hello tabela lista de dispositivos, verifique se que esse dispositivo Olá conectou com êxito toohello serviço verificando o status de saudação.</span><span class="sxs-lookup"><span data-stu-id="89711-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="89711-159">status de saudação do dispositivo deve ser **pronto tooset backup**.</span><span class="sxs-lookup"><span data-stu-id="89711-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Página dos Dispositivos StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="89711-161">Você pode precisar toowait para alguns minutos para Olá dispositivo status toochange muito**pronto tooset backup**.</span><span class="sxs-lookup"><span data-stu-id="89711-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="89711-162">Se o dispositivo de saudação não aparece nessa lista, você precisará toomake-se de que seu firewall de rede foi configurado conforme descrito em [requisitos de rede para seu dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="89711-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="89711-163">Verifique se a porta 9354 é aberta para comunicação de saída como isso é usado pelo barramento de serviço Olá para comunicação de dispositivo de serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="89711-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

