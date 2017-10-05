---
title: Conectar remotamente ao seu dispositivo StorSimple | Microsoft Docs
description: Explica como configurar seu dispositivo para o gerenciamento remoto e como se conectar ao Windows PowerShell para StorSimple via HTTP ou HTTPS.
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
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="182dd-103">Conectar remotamente ao seu dispositivo StorSimple série 8000</span><span class="sxs-lookup"><span data-stu-id="182dd-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="182dd-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="182dd-104">Overview</span></span>

<span data-ttu-id="182dd-105">É possível conectar-se remotamente ao seu dispositivo por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="182dd-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="182dd-106">Ao se conectar dessa maneira, você não vê um menu.</span><span class="sxs-lookup"><span data-stu-id="182dd-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="182dd-107">(Você verá um menu apenas se usar o console serial no dispositivo para se conectar.) Com a comunicação remota do Windows PowerShell, você se conectar a um espaço de execução específico.</span><span class="sxs-lookup"><span data-stu-id="182dd-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="182dd-108">Também é possível especificar o idioma de exibição.</span><span class="sxs-lookup"><span data-stu-id="182dd-108">You can also specify the display language.</span></span>

<span data-ttu-id="182dd-109">Para obter mais informações sobre como usar o Windows PowerShell remotamente para gerenciar seu dispositivo, acesse [Usar o Windows PowerShell para StorSimple para administrar seu dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="182dd-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="182dd-110">Este tutorial explica como configurar seu dispositivo para o gerenciamento remoto e, em seguida, como se conectar ao Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="182dd-111">É possível usar HTTP ou HTTPS para se conectar remotamente por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="182dd-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="182dd-112">No entanto, quando estiver decidindo a forma de conexão ao Windows PowerShell para StorSimple, considere as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="182dd-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="182dd-113">Conectar-se diretamente ao console serial do dispositivo é seguro, mas se conectar ao console serial em comutadores de rede não é seguro.</span><span class="sxs-lookup"><span data-stu-id="182dd-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="182dd-114">Tenha cuidado com os riscos de segurança ao se conectar ao console serial do dispositivo em comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="182dd-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="182dd-115">A conexão através de uma sessão HTTP pode oferecer mais segurança do que a conexão por meio do console serial através da rede.</span><span class="sxs-lookup"><span data-stu-id="182dd-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="182dd-116">Embora não seja o método mais seguro, é aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="182dd-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="182dd-117">A conexão através de uma sessão HTTPS com um certificado autoassinado é a mais segura, sendo a opção recomendada.</span><span class="sxs-lookup"><span data-stu-id="182dd-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="182dd-118">Você pode se conectar remotamente à interface do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="182dd-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="182dd-119">No entanto, o acesso remoto ao seu dispositivo StorSimple por meio da interface do Windows PowerShell não está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="182dd-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="182dd-120">É necessário habilitar o gerenciamento remoto primeiro no dispositivo e, em seguida, habilitá-lo no cliente usado para acessar seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="182dd-121">As etapas descritas neste artigo foram executadas em um sistema de host executando o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="182dd-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="182dd-122">Conectar-se por meio de HTTP</span><span class="sxs-lookup"><span data-stu-id="182dd-122">Connect through HTTP</span></span>

<span data-ttu-id="182dd-123">Conectar-se ao Windows PowerShell para StorSimple por meio de uma sessão HTTP oferece mais segurança do que se conectar por meio do console serial do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="182dd-124">Embora não seja o método mais seguro, é aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="182dd-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="182dd-125">É possível usar o Portal do Azure ou o console serial para configurar o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="182dd-126">Escolha um dos seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="182dd-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="182dd-127">Usar o Portal do Azure para habilitar o gerenciamento remoto via HTTP</span><span class="sxs-lookup"><span data-stu-id="182dd-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="182dd-128">Usar o console serial para habilitar o gerenciamento remoto via HTTP</span><span class="sxs-lookup"><span data-stu-id="182dd-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="182dd-129">Depois de habilitar o gerenciamento remoto, use o procedimento a seguir para preparar o cliente para uma conexão remota.</span><span class="sxs-lookup"><span data-stu-id="182dd-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="182dd-130">Preparar o cliente para a conexão remota</span><span class="sxs-lookup"><span data-stu-id="182dd-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="182dd-131">Usar o Portal do Azure para habilitar o gerenciamento remoto via HTTP</span><span class="sxs-lookup"><span data-stu-id="182dd-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="182dd-132">Siga as seguintes etapas no Portal do Azure para habilitar o gerenciamento remoto via HTTP.</span><span class="sxs-lookup"><span data-stu-id="182dd-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="182dd-133">Para habilitar o gerenciamento remoto por meio do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="182dd-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="182dd-134">Vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="182dd-135">Selecione **Dispositivos** e, em seguida, selecione e clique no dispositivo que você deseja configurar para o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="182dd-136">Acesse **Configurações do dispositivo > Segurança**.</span><span class="sxs-lookup"><span data-stu-id="182dd-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="182dd-137">Na folha **Configurações de Segurança**, clique em **Gerenciamento Remoto**.</span><span class="sxs-lookup"><span data-stu-id="182dd-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="182dd-138">Na folha **Gerenciamento remoto**, defina **Habilitar Gerenciamento Remoto** como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="182dd-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="182dd-139">Agora, você pode optar por conectar-se usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="182dd-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="182dd-140">(O padrão é conectar-se por HTTPS.) Certifique-se de que HTTP esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="182dd-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="182dd-141">A conexão por HTTP só será aceitável em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="182dd-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="182dd-142">Clique em **Salvar** e, quando precisar confirmar, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="182dd-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="182dd-143">Usar o console serial para habilitar o gerenciamento remoto via HTTP</span><span class="sxs-lookup"><span data-stu-id="182dd-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="182dd-144">Execute as seguintes etapas no console serial do dispositivo para habilitar o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="182dd-145">Para habilitar o gerenciamento remoto por meio do console serial</span><span class="sxs-lookup"><span data-stu-id="182dd-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="182dd-146">No menu do console serial, escolha a opção 1.</span><span class="sxs-lookup"><span data-stu-id="182dd-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="182dd-147">Para obter mais informações sobre como usar o console serial no dispositivo, vá para [Conectar-se ao Windows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="182dd-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="182dd-148">No prompt, digite: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="182dd-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="182dd-149">Você é notificado sobre as vulnerabilidades de segurança do uso de HTTP para se conectar ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="182dd-150">Quando solicitado, confirme digitando **Y**.</span><span class="sxs-lookup"><span data-stu-id="182dd-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="182dd-151">Verifique se o HTTP estiver habilitado digitando: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="182dd-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="182dd-152">Verifique se o campo **RemoteManagementMode** mostra **HttpsAndHttpEnabled**. A ilustração a seguir mostra essas configurações em PuTTY.</span><span class="sxs-lookup"><span data-stu-id="182dd-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS serial e HTTP habilitados](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="182dd-154">Preparar o cliente para a conexão remota</span><span class="sxs-lookup"><span data-stu-id="182dd-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="182dd-155">Execute as seguintes etapas no cliente para habilitar o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="182dd-156">Para preparar o cliente para a conexão remota</span><span class="sxs-lookup"><span data-stu-id="182dd-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="182dd-157">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="182dd-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="182dd-158">Digite o seguinte comando para adicionar o endereço IP do dispositivo StorSimple na lista de hosts confiáveis do cliente:</span><span class="sxs-lookup"><span data-stu-id="182dd-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="182dd-159">Substitua <*device_ip*> pelo endereço IP do dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="182dd-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="182dd-160">Digite o seguinte comando para salvar as credenciais do dispositivo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="182dd-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="182dd-161">Na caixa de diálogo que é exibida:</span><span class="sxs-lookup"><span data-stu-id="182dd-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="182dd-162">Digite o nome de usuário no seguinte formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="182dd-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="182dd-163">Digite a senha de administrador do dispositivo que foi definida quando o dispositivo foi configurado com o assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="182dd-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="182dd-164">A senha padrão é *Senha1*.</span><span class="sxs-lookup"><span data-stu-id="182dd-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="182dd-165">Inicie uma sessão do Windows PowerShell no dispositivo digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="182dd-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="182dd-166">Para criar uma sessão do Windows PowerShell para ser usada com o dispositivo virtual StorSimple, acrescente o parâmetro `–Port` e especifique a porta pública que você configurou na comunicação remota do dispositivo virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="182dd-167">Neste momento, uma sessão do Windows PowerShell remota já deve estar ativa para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![PowerShell remoto usando HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="182dd-169">Conectar-se por meio de HTTPS</span><span class="sxs-lookup"><span data-stu-id="182dd-169">Connect through HTTPS</span></span>

<span data-ttu-id="182dd-170">A conexão ao Windows PowerShell para StorSimple por meio de uma sessão HTTPS é o método mais seguro e recomendado de se conectar remotamente ao seu dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="182dd-171">Os procedimentos a seguir explicam como configurar os computadores de cliente e o console seriais para que você possa usar HTTPS para se conectar ao Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="182dd-172">É possível usar o Portal do Azure ou o console serial para configurar o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="182dd-173">Escolha um dos seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="182dd-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="182dd-174">Usar o Portal do Azure para habilitar o gerenciamento remoto via HTTPS</span><span class="sxs-lookup"><span data-stu-id="182dd-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="182dd-175">Usar o console serial para habilitar o gerenciamento remoto via HTTPS</span><span class="sxs-lookup"><span data-stu-id="182dd-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="182dd-176">Depois de habilitar o gerenciamento remoto, use os procedimentos a seguir para preparar o host para um gerenciamento remoto e conecte ao dispositivo a partir do host remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="182dd-177">Preparar o host para gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="182dd-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="182dd-178">Conectar ao dispositivo a partir do host remoto</span><span class="sxs-lookup"><span data-stu-id="182dd-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="182dd-179">Usar o Portal do Azure para habilitar o gerenciamento remoto via HTTPS</span><span class="sxs-lookup"><span data-stu-id="182dd-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="182dd-180">Siga as seguintes etapas no Portal do Azure para habilitar o gerenciamento remoto via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="182dd-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="182dd-181">Para habilitar o gerenciamento remoto via HTTPS no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="182dd-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="182dd-182">Vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="182dd-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="182dd-183">Selecione **Dispositivos** e, em seguida, selecione e clique no dispositivo que você deseja configurar para o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="182dd-184">Acesse **Configurações do dispositivo > Segurança**.</span><span class="sxs-lookup"><span data-stu-id="182dd-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="182dd-185">Na folha **Configurações de Segurança**, clique em **Gerenciamento Remoto**.</span><span class="sxs-lookup"><span data-stu-id="182dd-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="182dd-186">Defina **Habilitar o Gerenciamento Remoto** como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="182dd-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="182dd-187">Agora, você pode optar por conectar-se usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="182dd-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="182dd-188">(O padrão é conectar-se por HTTPS.) Certifique-se de que HTTPS esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="182dd-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="182dd-189">Clique em ... e em **Baixar Certificado de gerenciamento remoto**.</span><span class="sxs-lookup"><span data-stu-id="182dd-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="182dd-190">Especifique um local para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-190">Specify a location to save this file.</span></span> <span data-ttu-id="182dd-191">É necessário instalar esse certificado no computador cliente ou host que será usado para se conectar ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="182dd-192">Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="182dd-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="182dd-193">Usar o console serial para habilitar o gerenciamento remoto via HTTPS</span><span class="sxs-lookup"><span data-stu-id="182dd-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="182dd-194">Execute as seguintes etapas no console serial do dispositivo para habilitar o gerenciamento remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="182dd-195">Para habilitar o gerenciamento remoto por meio do console serial</span><span class="sxs-lookup"><span data-stu-id="182dd-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="182dd-196">No menu do console serial, escolha a opção 1.</span><span class="sxs-lookup"><span data-stu-id="182dd-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="182dd-197">Para obter mais informações sobre como usar o console serial no dispositivo, vá para [Conectar-se ao Windows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="182dd-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="182dd-198">No prompt, digite:</span><span class="sxs-lookup"><span data-stu-id="182dd-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="182dd-199">Isso deve habilitar HTTPS em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="182dd-200">Verifique se o HTTP está habilitado digitando:</span><span class="sxs-lookup"><span data-stu-id="182dd-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="182dd-201">Certifique-se de que o campo **RemoteManagementMode** mostre **HttpsEnabled**. A ilustração a seguir mostra essas configurações em PuTTY.</span><span class="sxs-lookup"><span data-stu-id="182dd-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS serial habilitado](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="182dd-203">Na saída de `Get-HcsSystem`, copie o número de série do dispositivo e salve-o para usar depois.</span><span class="sxs-lookup"><span data-stu-id="182dd-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="182dd-204">O número de série é mapeado para o nome CN no certificado.</span><span class="sxs-lookup"><span data-stu-id="182dd-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="182dd-205">Obtenha um certificado de gerenciamento remoto, digitando:</span><span class="sxs-lookup"><span data-stu-id="182dd-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="182dd-206">Um certificado similar ao seguinte aparecerá.</span><span class="sxs-lookup"><span data-stu-id="182dd-206">A certificate similar to the following will appear.</span></span>
   
    ![Obter certificado de gerenciamento remoto](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="182dd-208">Copie as informações do certificado de **---INICIAR CERTIFICADO---** até **---TERMINAR CERTIFICADO---** em um editor de texto como o bloco de notas e salve-o como arquivo .cer.</span><span class="sxs-lookup"><span data-stu-id="182dd-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="182dd-209">(Você vai copiar esse arquivo para o host remoto quando preparar o host.)</span><span class="sxs-lookup"><span data-stu-id="182dd-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="182dd-210">Para gerar um novo certificado, use o cmdlet `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="182dd-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="182dd-211">Preparar o host para gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="182dd-211">Prepare the host for remote management</span></span>

<span data-ttu-id="182dd-212">Para preparar o computador host para a conexão remota que use uma sessão HTTPS, execute os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="182dd-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="182dd-213">[Importe o arquivo. cer no repositório de raiz do cliente ou host remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="182dd-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="182dd-214">[Adicione os números de série do dispositivo ao arquivo de hosts em seu host remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="182dd-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="182dd-215">Cada um dos procedimentos acima é descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="182dd-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="182dd-216">Para importar o certificado no host remoto</span><span class="sxs-lookup"><span data-stu-id="182dd-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="182dd-217">Clique com o botão direito do mouse no arquivo .cer e selecione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="182dd-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="182dd-218">Isso inicia o Assistente para importação de certificados.</span><span class="sxs-lookup"><span data-stu-id="182dd-218">This starts the Certificate Import Wizard.</span></span>
   
    ![Assistente para importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="182dd-220">Em **Localização do repositório**, selecione **Computador Local** e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="182dd-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="182dd-221">Selecione **Colocar todos os certificados no seguinte repositório** e, em seguida, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="182dd-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="182dd-222">Navegue até o repositório de raiz do seu host remoto e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="182dd-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistente para importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="182dd-224">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="182dd-224">Click **Finish**.</span></span> <span data-ttu-id="182dd-225">Será exibida uma mensagem que informa que a importação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="182dd-225">A message that tells you that the import was successful appears.</span></span>
   
    ![Assistente para importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="182dd-227">Para adicionar números de série do dispositivo ao host remoto</span><span class="sxs-lookup"><span data-stu-id="182dd-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="182dd-228">Inicie o bloco de notas como administrador e abra o arquivo hosts localizado em \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="182dd-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="182dd-229">Adicione as três entradas a seguir ao arquivo hosts: **endereço IP DATA 0**, **endereço IP fixo do controlador 0** e **endereço IP fixo do controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="182dd-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="182dd-230">Insira o número de série do dispositivo que você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="182dd-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="182dd-231">Mapeie-o para o endereço IP conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="182dd-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="182dd-232">Em controlador 0 e controlador 1, acrescente **Controller0** e **Controller1** no final do número de série (nome CN).</span><span class="sxs-lookup"><span data-stu-id="182dd-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Adicionando um Nome CN ao arquivo hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="182dd-234">Salve o arquivo hosts.</span><span class="sxs-lookup"><span data-stu-id="182dd-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="182dd-235">Conectar ao dispositivo a partir do host remoto</span><span class="sxs-lookup"><span data-stu-id="182dd-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="182dd-236">Use o Windows PowerShell e o SSL para inserir uma sessão SSAdmin no dispositivo pelo cliente ou host remoto.</span><span class="sxs-lookup"><span data-stu-id="182dd-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="182dd-237">A sessão SSAdmin é mapeada para a opção 1 no menu de [console serial](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="182dd-238">Execute o procedimento a seguir no computador do qual você deseja fazer a conexão remota do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="182dd-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="182dd-239">Para inserir uma sessão SSAdmin no dispositivo usando Windows PowerShell e SSL</span><span class="sxs-lookup"><span data-stu-id="182dd-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="182dd-240">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="182dd-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="182dd-241">Adicione o endereço IP do dispositivo aos hosts confiáveis do cliente, digitando:</span><span class="sxs-lookup"><span data-stu-id="182dd-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="182dd-242">Em que <*device_ip*> é o endereço IP do dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="182dd-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="182dd-243">Para criar uma nova credencial, digite:</span><span class="sxs-lookup"><span data-stu-id="182dd-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="182dd-244">Em que <*IP do dispositivo de destino*> é o endereço IP de DATA 0 do seu dispositivo; por exemplo, **10.126.173.90** conforme mostrado na imagem anterior do arquivo hosts.</span><span class="sxs-lookup"><span data-stu-id="182dd-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="182dd-245">Além disso, forneça a senha de administrador do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="182dd-246">Crie uma sessão, digitando:</span><span class="sxs-lookup"><span data-stu-id="182dd-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="182dd-247">Para o parâmetro -ComputerName no cmdlet, forneça o <*número de série do dispositivo de destino*>.</span><span class="sxs-lookup"><span data-stu-id="182dd-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="182dd-248">Esse número de série foi mapeado para o endereço IP de DATA 0 no arquivo de hosts em seu host remoto; por exemplo, **SHX0991003G44MT** , como mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="182dd-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="182dd-249">Tipo:</span><span class="sxs-lookup"><span data-stu-id="182dd-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="182dd-250">Você precisará aguardar alguns minutos e, em seguida, será conectado ao dispositivo via HTTPS por SSL.</span><span class="sxs-lookup"><span data-stu-id="182dd-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="182dd-251">Você verá uma mensagem que indica que está conectado ao seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="182dd-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![PowerShell remoto usando HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="182dd-253">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="182dd-253">Next steps</span></span>

* <span data-ttu-id="182dd-254">Saiba mais sobre como [usar o Windows PowerShell para administrar seu dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="182dd-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="182dd-255">Saiba mais sobre como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="182dd-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

