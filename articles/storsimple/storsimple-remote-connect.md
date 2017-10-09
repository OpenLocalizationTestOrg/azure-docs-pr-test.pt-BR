---
title: aaaConnect remotamente o dispositivo StorSimple tooyour | Microsoft Docs
description: Explica como tooconfigure seu dispositivo para o gerenciamento remoto e como tooconnect tooWindows PowerShell para StorSimple via HTTP ou HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="27a63-103">Conectar-se remotamente dispositivo da série StorSimple 8000 do tooyour</span><span class="sxs-lookup"><span data-stu-id="27a63-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="27a63-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="27a63-104">Overview</span></span>
<span data-ttu-id="27a63-105">Você pode usar o dispositivo StorSimple do Windows PowerShell remoting tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="27a63-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="27a63-106">Ao se conectar dessa maneira, você não verá um menu.</span><span class="sxs-lookup"><span data-stu-id="27a63-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="27a63-107">(Você verá um menu somente se você usar o console serial Olá em Olá dispositivo tooconnect.) Com a comunicação remota do Windows PowerShell, você pode se conectar runspace específico tooa.</span><span class="sxs-lookup"><span data-stu-id="27a63-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="27a63-108">Você também pode especificar o idioma de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a63-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="27a63-109">Para obter mais informações sobre como usar o Windows PowerShell remoting toomanage seu dispositivo, vá muito[usar o Windows PowerShell para StorSimple tooadminister seu dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="27a63-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="27a63-110">Este tutorial explica como tooconfigure seu dispositivo para gerenciamento remoto e, em seguida, como tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="27a63-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="27a63-111">Você pode usar HTTP ou HTTPS tooconnect via comunicação remota do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27a63-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="27a63-112">No entanto, quando você estiver decidindo como tooconnect tooWindows PowerShell para StorSimple, considere o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="27a63-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="27a63-113">Conectando-se diretamente toohello console serial do dispositivo é seguro, mas conectar console serial do toohello em comutadores de rede não é.</span><span class="sxs-lookup"><span data-stu-id="27a63-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="27a63-114">Seja cauteloso Olá dos riscos de segurança ao conectar-se o console serial do dispositivo toohello em comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="27a63-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="27a63-115">Conectando por meio de uma sessão HTTP pode oferecer mais segurança do que conectar-se por meio do console serial Olá via rede hello.</span><span class="sxs-lookup"><span data-stu-id="27a63-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="27a63-116">Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="27a63-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="27a63-117">Conectando por meio de uma sessão HTTPS com um certificado autoassinado é hello mais seguro e Olá opção recomendada.</span><span class="sxs-lookup"><span data-stu-id="27a63-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="27a63-118">Você pode se conectar remotamente toohello interface do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27a63-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="27a63-119">No entanto, os dispositivos de StorSimple tooyour acesso remoto por meio da interface do Windows PowerShell Olá não está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="27a63-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="27a63-120">Você precisa tooenable o gerenciamento remoto no dispositivo Olá primeiro e, em seguida, em Olá cliente que é usado tooaccess seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="27a63-121">etapas de saudação descritas neste artigo foram executadas em um sistema de host executando o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="27a63-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="27a63-122">Conectar-se por meio de HTTP</span><span class="sxs-lookup"><span data-stu-id="27a63-122">Connect through HTTP</span></span>
<span data-ttu-id="27a63-123">Conectar tooWindows PowerShell para StorSimple por meio de uma sessão HTTP oferece mais segurança do que se conectam por meio do console de série de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="27a63-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="27a63-124">Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="27a63-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="27a63-125">Você pode usar o hello portal clássico do Azure ou o gerenciamento remoto do tooconfigure Olá console serial.</span><span class="sxs-lookup"><span data-stu-id="27a63-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="27a63-126">Selecione Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a63-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="27a63-127">Usar o gerenciamento remoto do hello tooenable de portal clássico do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="27a63-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="27a63-128">Usar o gerenciamento remoto do tooenable Olá console serial sobre HTTP</span><span class="sxs-lookup"><span data-stu-id="27a63-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="27a63-129">Depois de habilitar o gerenciamento remoto, use Olá seguindo o procedimento tooprepare saudação do cliente para uma conexão remota.</span><span class="sxs-lookup"><span data-stu-id="27a63-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="27a63-130">Prepare saudação do cliente para conexão remota</span><span class="sxs-lookup"><span data-stu-id="27a63-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="27a63-131">Usar o gerenciamento remoto do hello tooenable de portal clássico do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="27a63-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="27a63-132">Execute Olá seguindo as etapas no gerenciamento remoto do hello tooenable de portal clássico do Azure via HTTP.</span><span class="sxs-lookup"><span data-stu-id="27a63-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="27a63-133">gerenciamento remoto de tooenable por meio de saudação portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="27a63-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="27a63-134">Acesse **Dispositivos** > **Configurar** do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="27a63-135">Role para baixo toohello **gerenciamento remoto** seção.</span><span class="sxs-lookup"><span data-stu-id="27a63-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="27a63-136">Definir **habilitar o gerenciamento remoto** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="27a63-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="27a63-137">Agora você pode escolher tooconnect usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="27a63-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="27a63-138">(o padrão de saudação é tooconnect via HTTPS.) Certifique-se de que HTTP esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="27a63-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27a63-139">A conexão por HTTP só será aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="27a63-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="27a63-140">Clique em **salvar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="27a63-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="27a63-141">Usar o gerenciamento remoto do tooenable Olá console serial sobre HTTP</span><span class="sxs-lookup"><span data-stu-id="27a63-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="27a63-142">Execute Olá seguindo as etapas no gerenciamento remoto do tooenable Olá dispositivo console serial.</span><span class="sxs-lookup"><span data-stu-id="27a63-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="27a63-143">gerenciamento remoto de tooenable através do console serial do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="27a63-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="27a63-144">No menu do console serial hello, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="27a63-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="27a63-145">Para obter mais informações sobre como usar o console serial Olá no dispositivo hello, ir muito[conectar tooWindows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="27a63-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="27a63-146">No prompt de hello, digite:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="27a63-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="27a63-147">Você será notificado sobre vulnerabilidades de segurança de saudação do uso de dispositivo de toohello tooconnect HTTP.</span><span class="sxs-lookup"><span data-stu-id="27a63-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="27a63-148">Quando solicitado, confirme digitando **Y**.</span><span class="sxs-lookup"><span data-stu-id="27a63-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="27a63-149">Verifique se o HTTP estiver habilitado digitando: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="27a63-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="27a63-150">Verifique se esse Olá **RemoteManagementMode** campo mostra **HttpsAndHttpEnabled**.hello ilustração a seguir mostra essas configurações em PuTTY.</span><span class="sxs-lookup"><span data-stu-id="27a63-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS serial e HTTP habilitados](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="27a63-152">Prepare saudação do cliente para conexão remota</span><span class="sxs-lookup"><span data-stu-id="27a63-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="27a63-153">Execute Olá seguindo as etapas no gerenciamento remoto do hello cliente tooenable.</span><span class="sxs-lookup"><span data-stu-id="27a63-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="27a63-154">cliente de saudação tooprepare para conexão remota</span><span class="sxs-lookup"><span data-stu-id="27a63-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="27a63-155">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="27a63-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="27a63-156">Digite hello endereço IP do comando tooadd Olá da lista de hosts confiáveis do cliente do toohello dispositivo StorSimple Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a63-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="27a63-157">Substitua <*device_ip*> com o endereço IP de saudação do seu dispositivo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="27a63-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="27a63-158">Digite o seguinte Olá credenciais do dispositivo Olá toosave em uma variável de comando:</span><span class="sxs-lookup"><span data-stu-id="27a63-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="27a63-159">Na caixa de diálogo de saudação aparece:</span><span class="sxs-lookup"><span data-stu-id="27a63-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="27a63-160">Nome de usuário do tipo hello neste formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="27a63-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="27a63-161">Digite a senha do administrador de dispositivo de saudação foi definida quando o dispositivo Olá foi configurado com o Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a63-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="27a63-162">a senha padrão Olá é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="27a63-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="27a63-163">Inicie uma sessão do Windows PowerShell no dispositivo Olá digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="27a63-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="27a63-164">toocreate uma sessão do Windows PowerShell para uso com o dispositivo virtual do StorSimple hello, acrescente Olá `–Port` parâmetro e especifique a porta pública de saudação que você configurou na comunicação remota para o dispositivo Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="27a63-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="27a63-165">Neste ponto, você deve ter um dispositivo de toohello de sessão ativado de remoto do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27a63-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![PowerShell remoto usando HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="27a63-167">Conectar-se por meio de HTTPS</span><span class="sxs-lookup"><span data-stu-id="27a63-167">Connect through HTTPS</span></span>
<span data-ttu-id="27a63-168">Conectar tooWindows PowerShell para StorSimple por meio de uma sessão HTTPS é hello mais seguro e recomendado de método do dispositivo de Microsoft Azure StorSimple tooyour conectar remotamente.</span><span class="sxs-lookup"><span data-stu-id="27a63-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="27a63-169">Olá procedimentos a seguir explica como tooset backup Olá seriais consoles e computadores clientes para que você possa usar HTTPS tooconnect tooWindows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="27a63-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="27a63-170">Você pode usar o hello portal clássico do Azure ou o gerenciamento remoto do tooconfigure Olá console serial.</span><span class="sxs-lookup"><span data-stu-id="27a63-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="27a63-171">Selecione Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a63-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="27a63-172">Usar o gerenciamento remoto do hello tooenable de portal clássico do Azure via HTTPS</span><span class="sxs-lookup"><span data-stu-id="27a63-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="27a63-173">Usar o gerenciamento remoto do hello console serial tooenable via HTTPS</span><span class="sxs-lookup"><span data-stu-id="27a63-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="27a63-174">Depois de habilitar o gerenciamento remoto, use Olá seguindo o host de saudação tooprepare procedimentos para o gerenciamento remoto e conecte o dispositivo toohello do host remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="27a63-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="27a63-175">Preparar o host Olá para gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="27a63-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="27a63-176">Conecte o dispositivo de toohello do host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="27a63-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="27a63-177">Usar o gerenciamento remoto do hello tooenable de portal clássico do Azure via HTTPS</span><span class="sxs-lookup"><span data-stu-id="27a63-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="27a63-178">Execute Olá seguindo as etapas no gerenciamento remoto do hello tooenable de portal clássico do Azure via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="27a63-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="27a63-179">gerenciamento remoto tooenable via HTTPS de saudação portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="27a63-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="27a63-180">Acesse **Dispositivos** > **Configurar** do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="27a63-181">Role para baixo toohello **gerenciamento remoto** seção.</span><span class="sxs-lookup"><span data-stu-id="27a63-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="27a63-182">Definir **habilitar o gerenciamento remoto** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="27a63-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="27a63-183">Agora você pode escolher tooconnect usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="27a63-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="27a63-184">(o padrão de saudação é tooconnect via HTTPS.) Certifique-se de que HTTPS esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="27a63-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="27a63-185">Clique em **Baixar certificado de gerenciamento remoto**.</span><span class="sxs-lookup"><span data-stu-id="27a63-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="27a63-186">Especifique um local toosave esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-186">Specify a location toosave this file.</span></span> <span data-ttu-id="27a63-187">Você precisará tooinstall este certificado no computador cliente ou host de saudação que você usará tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="27a63-188">Clique em **salvar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="27a63-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="27a63-189">Usar o gerenciamento remoto do hello console serial tooenable via HTTPS</span><span class="sxs-lookup"><span data-stu-id="27a63-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="27a63-190">Execute Olá seguindo as etapas no gerenciamento remoto do tooenable Olá dispositivo console serial.</span><span class="sxs-lookup"><span data-stu-id="27a63-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="27a63-191">gerenciamento remoto de tooenable através do console serial do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="27a63-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="27a63-192">No menu do console serial hello, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="27a63-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="27a63-193">Para obter mais informações sobre como usar o console serial Olá no dispositivo hello, ir muito[conectar tooWindows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="27a63-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="27a63-194">No prompt de hello, digite:</span><span class="sxs-lookup"><span data-stu-id="27a63-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="27a63-195">Isso deve habilitar HTTPS em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="27a63-196">Verifique se o HTTP está habilitado digitando:</span><span class="sxs-lookup"><span data-stu-id="27a63-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="27a63-197">Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsEnabled**.hello ilustração a seguir mostra essas configurações em PuTTY.</span><span class="sxs-lookup"><span data-stu-id="27a63-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS serial habilitado](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="27a63-199">Da saída de saudação de `Get-HcsSystem`, copie Olá o número de série do dispositivo hello e salvá-lo para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="27a63-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27a63-200">número de série de saudação mapeia toohello nome CN no certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a63-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="27a63-201">Obtenha um certificado de gerenciamento remoto, digitando:</span><span class="sxs-lookup"><span data-stu-id="27a63-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="27a63-202">Uma certificado semelhante toohello a seguir será exibida.</span><span class="sxs-lookup"><span data-stu-id="27a63-202">A certificate similar toohello following will appear.</span></span>
   
    ![Obter certificado de gerenciamento remoto](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="27a63-204">Copiar informações de saudação no certificado de saudação do **---iniciar certificado---** muito**---concluir certificado---** em um editor de texto como bloco de notas e salve-o como um arquivo. cer.</span><span class="sxs-lookup"><span data-stu-id="27a63-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="27a63-205">(Você copiará esse host remoto do arquivo tooyour quando você prepara o host hello.)</span><span class="sxs-lookup"><span data-stu-id="27a63-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27a63-206">toogenerate um novo certificado, use Olá `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27a63-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="27a63-207">Preparar o host Olá para gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="27a63-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="27a63-208">computador de host tooprepare Olá para uma conexão remota que usa uma sessão HTTPS, execute Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a63-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="27a63-209">[Arquivo de importação. cer de saudação no repositório de raiz de saudação do cliente hello ou host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="27a63-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="27a63-210">[Adicionar números de série do dispositivo de Olá toohello arquivo hosts em seu host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="27a63-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="27a63-211">Cada um desses procedimentos é descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="27a63-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="27a63-212">certificado de saudação tooimport no host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="27a63-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="27a63-213">Clique em arquivo. cer de saudação e selecione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="27a63-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="27a63-214">Isso iniciará a saudação Assistente de importação de certificado.</span><span class="sxs-lookup"><span data-stu-id="27a63-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Assistente para importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="27a63-216">Em **Localização do repositório**, selecione **Computador Local** e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="27a63-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="27a63-217">Selecione **colocar todos os certificados no hello repositório a seguir**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="27a63-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="27a63-218">Navegue toohello repositório de raiz do seu host remoto e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="27a63-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistente para importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="27a63-220">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="27a63-220">Click **Finish**.</span></span> <span data-ttu-id="27a63-221">Será exibida uma mensagem que informa que Olá importação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="27a63-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Assistente para importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="27a63-223">host remoto do toohello tooadd dispositivo números de série</span><span class="sxs-lookup"><span data-stu-id="27a63-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="27a63-224">Inicie o bloco de notas como administrador e, em seguida, abra o arquivo de hosts de saudação localizado em \WINDOWS\system32\drivers\etc..</span><span class="sxs-lookup"><span data-stu-id="27a63-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="27a63-225">Adicionar Olá após o arquivo de hosts do três entradas tooyour: **endereço IP DATA 0**, **endereço IP fixo do controlador 0**, e **endereço IP fixo do controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="27a63-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="27a63-226">Insira o número de série do dispositivo Olá que você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="27a63-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="27a63-227">Mapear este endereço IP toohello conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="27a63-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="27a63-228">Para o controlador 0 e 1, acrescente **Controller0** e **Controller1** final Olá Olá do número de série (nome CN).</span><span class="sxs-lookup"><span data-stu-id="27a63-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Adicionando nome CN toohosts arquivo](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="27a63-230">Salvar arquivo de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a63-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="27a63-231">Conecte o dispositivo de toohello do host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="27a63-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="27a63-232">Usar o Windows PowerShell e SSL tooenter uma sessão SSAdmin em seu dispositivo de um host remoto ou cliente.</span><span class="sxs-lookup"><span data-stu-id="27a63-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="27a63-233">sessão de SSAdmin Olá mapeia toooption 1 no hello [console serial](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="27a63-234">Execute Olá seguindo o procedimento no computador de saudação do qual você deseja a conexão do toomake Olá remoto do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27a63-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="27a63-235">tooenter uma sessão SSAdmin no dispositivo hello usando o Windows PowerShell e SSL</span><span class="sxs-lookup"><span data-stu-id="27a63-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="27a63-236">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="27a63-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="27a63-237">Adicione hosts confiáveis do cliente do toohello endereço IP hello dispositivo digitando:</span><span class="sxs-lookup"><span data-stu-id="27a63-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="27a63-238">Onde <*device_ip*> é o endereço IP de saudação do seu dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="27a63-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="27a63-239">Crie uma nova credencial, digitando:</span><span class="sxs-lookup"><span data-stu-id="27a63-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="27a63-240">Onde <*IP do dispositivo de destino*> é Olá endereço IP de DATA 0 do seu dispositivo; por exemplo, **10.126.173.90** conforme Olá anterior a imagem do arquivo de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a63-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="27a63-241">Além disso, forneça a senha do administrador de saudação para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="27a63-242">Crie uma sessão, digitando:</span><span class="sxs-lookup"><span data-stu-id="27a63-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="27a63-243">Olá - ComputerName no parâmetro no cmdlet hello, fornecer hello <*número de série do dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="27a63-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="27a63-244">Este número de série foi mapeado toohello endereço IP de DATA 0 no arquivo de hosts Olá no seu host remoto. Por exemplo, **SHX0991003G44MT** conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="27a63-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="27a63-245">Tipo:</span><span class="sxs-lookup"><span data-stu-id="27a63-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="27a63-246">Você precisará toowait alguns minutos e, em seguida, será conectado tooyour dispositivo via HTTPS sobre SSL.</span><span class="sxs-lookup"><span data-stu-id="27a63-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="27a63-247">Você verá uma mensagem que indica que você está conectado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="27a63-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![PowerShell remoto usando HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="27a63-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27a63-249">Next steps</span></span>
* <span data-ttu-id="27a63-250">Saiba mais sobre [usando o Windows PowerShell tooadminister seu dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="27a63-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="27a63-251">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="27a63-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

