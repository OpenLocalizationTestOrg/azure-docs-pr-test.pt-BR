---
title: aaaConnect remotamente o dispositivo StorSimple tooyour | Microsoft Docs
description: Explica como tooconfigure seu dispositivo para o gerenciamento remoto e como tooconnect tooWindows PowerShell para StorSimple via HTTP ou HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="d4e15-103">Conectar-se remotamente dispositivo da série StorSimple 8000 do tooyour</span><span class="sxs-lookup"><span data-stu-id="d4e15-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d4e15-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d4e15-104">Overview</span></span>

<span data-ttu-id="d4e15-105">Você pode se conectar remotamente tooyour dispositivo por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4e15-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="d4e15-106">Ao se conectar dessa maneira, você não vê um menu.</span><span class="sxs-lookup"><span data-stu-id="d4e15-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="d4e15-107">(Você verá um menu somente se você usar o console serial Olá em Olá dispositivo tooconnect.) Com a comunicação remota do Windows PowerShell, você pode se conectar runspace específico tooa.</span><span class="sxs-lookup"><span data-stu-id="d4e15-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="d4e15-108">Você também pode especificar o idioma de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4e15-108">You can also specify hello display language.</span></span>

<span data-ttu-id="d4e15-109">Para obter mais informações sobre como usar o Windows PowerShell remoting toomanage seu dispositivo, vá muito[usar o Windows PowerShell para StorSimple tooadminister seu dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d4e15-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="d4e15-110">Este tutorial explica como tooconfigure seu dispositivo para gerenciamento remoto e, em seguida, como tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4e15-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="d4e15-111">Você pode usar HTTP ou HTTPS tooremotely conectar via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4e15-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="d4e15-112">No entanto, quando você estiver decidindo como tooconnect tooWindows PowerShell para StorSimple, considere Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4e15-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="d4e15-113">Conectando-se diretamente toohello console serial do dispositivo é seguro, mas conectar console serial do toohello em comutadores de rede não é.</span><span class="sxs-lookup"><span data-stu-id="d4e15-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="d4e15-114">Seja cauteloso Olá dos riscos de segurança ao conectar-se o console serial do dispositivo toohello em comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="d4e15-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="d4e15-115">Conectando por meio de uma sessão HTTP pode oferecer mais segurança do que conectar-se por meio do console serial Olá via rede hello.</span><span class="sxs-lookup"><span data-stu-id="d4e15-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="d4e15-116">Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="d4e15-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="d4e15-117">Conectando por meio de uma sessão HTTPS com um certificado autoassinado é hello mais seguro e Olá opção recomendada.</span><span class="sxs-lookup"><span data-stu-id="d4e15-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="d4e15-118">Você pode se conectar remotamente toohello interface do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4e15-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="d4e15-119">No entanto, os dispositivos de StorSimple tooyour acesso remoto por meio da interface do Windows PowerShell Olá não está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d4e15-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="d4e15-120">Você deve habilitar o gerenciamento remoto no dispositivo Olá primeiro e, em seguida, em Olá cliente que é usado tooaccess seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="d4e15-121">etapas de saudação descritas neste artigo foram executadas em um sistema de host executando o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d4e15-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="d4e15-122">Conectar-se por meio de HTTP</span><span class="sxs-lookup"><span data-stu-id="d4e15-122">Connect through HTTP</span></span>

<span data-ttu-id="d4e15-123">Conectar tooWindows PowerShell para StorSimple por meio de uma sessão HTTP oferece mais segurança do que se conectam por meio do console de série de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4e15-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="d4e15-124">Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="d4e15-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="d4e15-125">Você pode usar o hello Azure portal ou hello serial tooconfigure gerenciamento remoto do console.</span><span class="sxs-lookup"><span data-stu-id="d4e15-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="d4e15-126">Selecione Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4e15-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="d4e15-127">Usar o gerenciamento remoto do hello tooenable portal do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="d4e15-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="d4e15-128">Usar o gerenciamento remoto do tooenable Olá console serial sobre HTTP</span><span class="sxs-lookup"><span data-stu-id="d4e15-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="d4e15-129">Depois de habilitar o gerenciamento remoto, use Olá seguindo o procedimento tooprepare saudação do cliente para uma conexão remota.</span><span class="sxs-lookup"><span data-stu-id="d4e15-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="d4e15-130">Prepare saudação do cliente para conexão remota</span><span class="sxs-lookup"><span data-stu-id="d4e15-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="d4e15-131">Usar o gerenciamento remoto do hello tooenable portal do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="d4e15-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="d4e15-132">Execute Olá seguindo as etapas no gerenciamento remoto do hello tooenable portal do Azure via HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4e15-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="d4e15-133">gerenciamento remoto de tooenable por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d4e15-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="d4e15-134">Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="d4e15-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="d4e15-135">Selecione **dispositivos** e selecione e clique em dispositivo Olá desejar tooconfigure para gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="d4e15-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="d4e15-136">Vá muito**configurações do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="d4e15-137">Em Olá **as configurações de segurança** folha, clique em **gerenciamento remoto**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="d4e15-138">Em Olá **gerenciamento remoto** folha, defina **habilitar o gerenciamento remoto** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="d4e15-139">Agora você pode escolher tooconnect usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4e15-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="d4e15-140">(o padrão de saudação é tooconnect via HTTPS.) Certifique-se de que HTTP esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="d4e15-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d4e15-141">A conexão por HTTP só será aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="d4e15-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="d4e15-142">Clique em **Salvar** e, quando precisar confirmar, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="d4e15-143">Usar o gerenciamento remoto do tooenable Olá console serial sobre HTTP</span><span class="sxs-lookup"><span data-stu-id="d4e15-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="d4e15-144">Execute Olá seguindo as etapas no gerenciamento remoto do tooenable Olá dispositivo console serial.</span><span class="sxs-lookup"><span data-stu-id="d4e15-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="d4e15-145">gerenciamento remoto de tooenable através do console serial do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="d4e15-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="d4e15-146">No menu do console serial hello, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="d4e15-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="d4e15-147">Para obter mais informações sobre como usar o console serial Olá no dispositivo hello, ir muito[conectar tooWindows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d4e15-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d4e15-148">No prompt de hello, digite:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="d4e15-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="d4e15-149">Você será notificado sobre vulnerabilidades de segurança de saudação do uso de dispositivo de toohello tooconnect HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4e15-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="d4e15-150">Quando solicitado, confirme digitando **Y**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="d4e15-151">Verifique se o HTTP estiver habilitado digitando: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="d4e15-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="d4e15-152">Verifique se esse Olá **RemoteManagementMode** campo mostra **HttpsAndHttpEnabled**.hello ilustração a seguir mostra essas configurações em PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d4e15-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS serial e HTTP habilitados](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="d4e15-154">Prepare saudação do cliente para conexão remota</span><span class="sxs-lookup"><span data-stu-id="d4e15-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="d4e15-155">Execute Olá seguindo as etapas no gerenciamento remoto do hello cliente tooenable.</span><span class="sxs-lookup"><span data-stu-id="d4e15-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="d4e15-156">cliente de saudação tooprepare para conexão remota</span><span class="sxs-lookup"><span data-stu-id="d4e15-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="d4e15-157">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="d4e15-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d4e15-158">Digite hello endereço IP do comando tooadd Olá da lista de hosts confiáveis do cliente do toohello dispositivo StorSimple Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4e15-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="d4e15-159">Substitua <*device_ip*> com o endereço IP de saudação do seu dispositivo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d4e15-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d4e15-160">Digite o seguinte Olá credenciais do dispositivo Olá toosave em uma variável de comando:</span><span class="sxs-lookup"><span data-stu-id="d4e15-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="d4e15-161">Na caixa de diálogo de saudação aparece:</span><span class="sxs-lookup"><span data-stu-id="d4e15-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="d4e15-162">Nome de usuário do tipo hello neste formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="d4e15-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="d4e15-163">Digite a senha do administrador de dispositivo de saudação foi definida quando o dispositivo Olá foi configurado com o Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4e15-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="d4e15-164">a senha padrão Olá é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="d4e15-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="d4e15-165">Inicie uma sessão do Windows PowerShell no dispositivo Olá digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d4e15-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="d4e15-166">toocreate uma sessão do Windows PowerShell para uso com o dispositivo virtual do StorSimple hello, acrescente Olá `–Port` parâmetro e especifique a porta pública de saudação que você configurou na comunicação remota para o dispositivo Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4e15-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="d4e15-167">Neste ponto, você deve ter um dispositivo de toohello de sessão ativado de remoto do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4e15-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![PowerShell remoto usando HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="d4e15-169">Conectar-se por meio de HTTPS</span><span class="sxs-lookup"><span data-stu-id="d4e15-169">Connect through HTTPS</span></span>

<span data-ttu-id="d4e15-170">Conectar tooWindows PowerShell para StorSimple por meio de uma sessão HTTPS é hello mais seguro e recomendado de método do dispositivo de Microsoft Azure StorSimple tooyour conectar remotamente.</span><span class="sxs-lookup"><span data-stu-id="d4e15-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="d4e15-171">Olá procedimentos a seguir explica como tooset backup Olá seriais consoles e computadores clientes para que você possa usar HTTPS tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4e15-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="d4e15-172">Você pode usar o hello Azure portal ou hello serial tooconfigure gerenciamento remoto do console.</span><span class="sxs-lookup"><span data-stu-id="d4e15-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="d4e15-173">Selecione Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4e15-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="d4e15-174">Usar o gerenciamento remoto do hello tooenable portal do Azure via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d4e15-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="d4e15-175">Usar o gerenciamento remoto do hello console serial tooenable via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d4e15-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="d4e15-176">Depois de habilitar o gerenciamento remoto, use Olá seguindo o host de saudação tooprepare procedimentos para o gerenciamento remoto e conecte o dispositivo toohello do host remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="d4e15-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="d4e15-177">Preparar o host Olá para gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="d4e15-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="d4e15-178">Conecte o dispositivo de toohello do host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="d4e15-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="d4e15-179">Usar o gerenciamento remoto do hello tooenable portal do Azure via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d4e15-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="d4e15-180">Execute Olá seguindo as etapas no gerenciamento remoto do hello tooenable portal do Azure via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d4e15-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="d4e15-181">gerenciamento remoto tooenable via HTTPS de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d4e15-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="d4e15-182">Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="d4e15-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="d4e15-183">Selecione **dispositivos** e selecione e clique em dispositivo Olá desejar tooconfigure para gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="d4e15-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="d4e15-184">Vá muito**configurações do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="d4e15-185">Em Olá **as configurações de segurança** folha, clique em **gerenciamento remoto**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="d4e15-186">Definir **habilitar o gerenciamento remoto** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="d4e15-187">Agora você pode escolher tooconnect usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d4e15-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="d4e15-188">(o padrão de saudação é tooconnect via HTTPS.) Certifique-se de que HTTPS esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="d4e15-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="d4e15-189">Clique em ... e em **Baixar Certificado de gerenciamento remoto**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="d4e15-190">Especifique um local toosave esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-190">Specify a location toosave this file.</span></span> <span data-ttu-id="d4e15-191">Você precisará tooinstall este certificado no computador cliente ou host de saudação que você usará tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="d4e15-192">Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="d4e15-193">Usar o gerenciamento remoto do hello console serial tooenable via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d4e15-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="d4e15-194">Execute Olá seguindo as etapas no gerenciamento remoto do tooenable Olá dispositivo console serial.</span><span class="sxs-lookup"><span data-stu-id="d4e15-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="d4e15-195">gerenciamento remoto de tooenable através do console serial do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="d4e15-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="d4e15-196">No menu do console serial hello, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="d4e15-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="d4e15-197">Para obter mais informações sobre como usar o console serial Olá no dispositivo hello, ir muito[conectar tooWindows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d4e15-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d4e15-198">No prompt de hello, digite:</span><span class="sxs-lookup"><span data-stu-id="d4e15-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="d4e15-199">Isso deve habilitar HTTPS em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="d4e15-200">Verifique se o HTTP está habilitado digitando:</span><span class="sxs-lookup"><span data-stu-id="d4e15-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="d4e15-201">Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsEnabled**.hello ilustração a seguir mostra essas configurações em PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d4e15-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS serial habilitado](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="d4e15-203">Da saída de saudação de `Get-HcsSystem`, copie Olá o número de série do dispositivo hello e salvá-lo para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="d4e15-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d4e15-204">número de série de saudação mapeia toohello nome CN no certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4e15-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="d4e15-205">Obtenha um certificado de gerenciamento remoto, digitando:</span><span class="sxs-lookup"><span data-stu-id="d4e15-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="d4e15-206">Uma certificado semelhante toohello a seguir será exibida.</span><span class="sxs-lookup"><span data-stu-id="d4e15-206">A certificate similar toohello following will appear.</span></span>
   
    ![Obter certificado de gerenciamento remoto](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="d4e15-208">Copiar informações de saudação no certificado de saudação do **---iniciar certificado---** muito**---concluir certificado---** em um editor de texto como bloco de notas e salve-o como um arquivo. cer.</span><span class="sxs-lookup"><span data-stu-id="d4e15-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="d4e15-209">(Você copiará esse host remoto do arquivo tooyour quando você prepara o host hello.)</span><span class="sxs-lookup"><span data-stu-id="d4e15-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d4e15-210">toogenerate um novo certificado, use Olá `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d4e15-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="d4e15-211">Preparar o host Olá para gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="d4e15-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="d4e15-212">computador de host tooprepare Olá para uma conexão remota que usa uma sessão HTTPS, execute Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4e15-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="d4e15-213">[Arquivo de importação. cer de saudação no repositório de raiz de saudação do cliente hello ou host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d4e15-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="d4e15-214">[Adicionar números de série do dispositivo de Olá toohello arquivo hosts em seu host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d4e15-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="d4e15-215">Cada saudação anterior procedimentos, é descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="d4e15-216">certificado de saudação tooimport no host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="d4e15-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="d4e15-217">Clique em arquivo. cer de saudação e selecione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="d4e15-218">Isso inicia o hello Assistente de importação de certificado.</span><span class="sxs-lookup"><span data-stu-id="d4e15-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![Assistente para importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="d4e15-220">Em **Localização do repositório**, selecione **Computador Local** e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="d4e15-221">Selecione **colocar todos os certificados no hello repositório a seguir**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="d4e15-222">Navegue toohello repositório de raiz do seu host remoto e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistente para importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="d4e15-224">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-224">Click **Finish**.</span></span> <span data-ttu-id="d4e15-225">Será exibida uma mensagem que informa que Olá importação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d4e15-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![Assistente para importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="d4e15-227">host remoto do toohello tooadd dispositivo números de série</span><span class="sxs-lookup"><span data-stu-id="d4e15-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="d4e15-228">Inicie o bloco de notas como administrador e, em seguida, abra o arquivo de hosts de saudação localizado em \WINDOWS\system32\drivers\etc..</span><span class="sxs-lookup"><span data-stu-id="d4e15-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="d4e15-229">Adicionar Olá após o arquivo de hosts do três entradas tooyour: **endereço IP DATA 0**, **endereço IP fixo do controlador 0**, e **endereço IP fixo do controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="d4e15-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="d4e15-230">Insira o número de série do dispositivo Olá que você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d4e15-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="d4e15-231">Mapear este endereço IP toohello conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4e15-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="d4e15-232">Para o controlador 0 e 1, acrescente **Controller0** e **Controller1** final Olá Olá do número de série (nome CN).</span><span class="sxs-lookup"><span data-stu-id="d4e15-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Adicionando nome CN toohosts arquivo](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="d4e15-234">Salvar arquivo de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4e15-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="d4e15-235">Conecte o dispositivo de toohello do host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="d4e15-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="d4e15-236">Usar o Windows PowerShell e SSL tooenter uma sessão SSAdmin em seu dispositivo de um host remoto ou cliente.</span><span class="sxs-lookup"><span data-stu-id="d4e15-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="d4e15-237">sessão de SSAdmin Olá mapeia toooption 1 no hello [console serial](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="d4e15-238">Execute Olá seguindo o procedimento no computador de saudação do qual você deseja a conexão do toomake Olá remoto do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4e15-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="d4e15-239">tooenter uma sessão SSAdmin no dispositivo hello usando o Windows PowerShell e SSL</span><span class="sxs-lookup"><span data-stu-id="d4e15-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="d4e15-240">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="d4e15-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d4e15-241">Adicione hosts confiáveis do cliente do toohello endereço IP hello dispositivo digitando:</span><span class="sxs-lookup"><span data-stu-id="d4e15-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="d4e15-242">Onde <*device_ip*> é o endereço IP de saudação do seu dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d4e15-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d4e15-243">toocreate uma nova credencial, digite:</span><span class="sxs-lookup"><span data-stu-id="d4e15-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="d4e15-244">Onde <*IP do dispositivo de destino*> é Olá endereço IP de DATA 0 do seu dispositivo; por exemplo, **10.126.173.90** conforme Olá anterior a imagem do arquivo de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4e15-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="d4e15-245">Além disso, forneça a senha do administrador de saudação para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="d4e15-246">Crie uma sessão, digitando:</span><span class="sxs-lookup"><span data-stu-id="d4e15-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="d4e15-247">Olá - ComputerName no parâmetro no cmdlet hello, fornecer hello <*número de série do dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="d4e15-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="d4e15-248">Este número de série foi mapeado toohello endereço IP de DATA 0 no arquivo de hosts Olá no seu host remoto. Por exemplo, **SHX0991003G44MT** conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4e15-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="d4e15-249">Tipo:</span><span class="sxs-lookup"><span data-stu-id="d4e15-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="d4e15-250">Você precisará toowait alguns minutos e, em seguida, será conectado tooyour dispositivo via HTTPS sobre SSL.</span><span class="sxs-lookup"><span data-stu-id="d4e15-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="d4e15-251">Você verá uma mensagem que indica que você está conectado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4e15-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![PowerShell remoto usando HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="d4e15-253">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4e15-253">Next steps</span></span>

* <span data-ttu-id="d4e15-254">Saiba mais sobre [usando o Windows PowerShell tooadminister seu dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d4e15-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="d4e15-255">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d4e15-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

