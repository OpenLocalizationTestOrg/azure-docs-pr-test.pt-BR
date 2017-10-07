---
title: redirecionamento de aaaUsing no Azure RemoteApp | Microsoft Docs
description: Saiba como tooconfigure e usar redirecionamento no RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="4e15f-103">Usando o redirecionamento no RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="4e15f-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4e15f-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="4e15f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4e15f-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="4e15f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4e15f-106">Redirecionamento do dispositivo permite que os usuários interagem com aplicativos remotos usando o computador local do hello dispositivos anexados tootheir, telefone ou tablet.</span><span class="sxs-lookup"><span data-stu-id="4e15f-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="4e15f-107">Por exemplo, se você tiver fornecido Skype por meio do Azure RemoteApp, o usuário precisa de câmera Olá instalada em seu toowork de PC com o Skype.</span><span class="sxs-lookup"><span data-stu-id="4e15f-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="4e15f-108">Isso também é verdadeiro para impressoras, alto-falantes, monitores e uma variedade de periféricos conectados por USB.</span><span class="sxs-lookup"><span data-stu-id="4e15f-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="4e15f-109">RemoteApp aproveita Olá protocolo de área de trabalho remota (RDP) e RemoteFX tooprovide redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="4e15f-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="4e15f-110">Qual redirecionamento está habilitado por padrão?</span><span class="sxs-lookup"><span data-stu-id="4e15f-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="4e15f-111">Quando você usa o RemoteApp, Olá redirecionamentos a seguir é habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="4e15f-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="4e15f-112">informações de saudação entre parênteses mostram a configuração de RDP de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e15f-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="4e15f-113">Tocar sons no computador local hello (**reproduzir neste computador**).</span><span class="sxs-lookup"><span data-stu-id="4e15f-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="4e15f-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="4e15f-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="4e15f-115">Captura de áudio Olá computadores local e enviar toohello remoto (**gravar deste computador**).</span><span class="sxs-lookup"><span data-stu-id="4e15f-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="4e15f-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="4e15f-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="4e15f-117">Imprimir toolocal impressoras (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="4e15f-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="4e15f-118">Portas COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="4e15f-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="4e15f-119">Dispositivo de cartão inteligente (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="4e15f-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="4e15f-120">Área de transferência (toocopy de capacidade e colar) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="4e15f-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="4e15f-121">Suavização de fonte clear type (permitir suavização de fonte: i:1)</span><span class="sxs-lookup"><span data-stu-id="4e15f-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="4e15f-122">Redirecionar todos os dispositivos Plug and Play com suporte.</span><span class="sxs-lookup"><span data-stu-id="4e15f-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="4e15f-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="4e15f-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="4e15f-124">Quais são os outros redirecionamentos disponíveis?</span><span class="sxs-lookup"><span data-stu-id="4e15f-124">What other redirection is available?</span></span>
<span data-ttu-id="4e15f-125">Duas opções de redirecionamento estão desabilitadas por padrão:</span><span class="sxs-lookup"><span data-stu-id="4e15f-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="4e15f-126">Redirecionamento de unidade (mapeamento da unidade): unidades do computador local se tornar unidades mapeadas na sessão remota hello.</span><span class="sxs-lookup"><span data-stu-id="4e15f-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="4e15f-127">Isso permite que você salvar ou abrir arquivos de suas unidades locais enquanto você trabalha na sessão remota hello.</span><span class="sxs-lookup"><span data-stu-id="4e15f-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="4e15f-128">Redirecionamento de USB: você pode usar o computador local do hello USB dispositivos anexados tooyour na sessão remota hello.</span><span class="sxs-lookup"><span data-stu-id="4e15f-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="4e15f-129">Alterar as configurações de redirecionamento no RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4e15f-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="4e15f-130">Você pode alterar as configurações de redirecionamento de dispositivo Olá para uma coleção usando saudação do PowerShell do Microsoft Azure com o SDK.</span><span class="sxs-lookup"><span data-stu-id="4e15f-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="4e15f-131">Depois de instalar Olá PowerShell novos e o SDK, primeiro configure toomanage sua assinatura como descrita em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e15f-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="4e15f-132">Em seguida, use um toohello semelhante do comando Propriedades RDP tooset Olá personalizadas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e15f-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="4e15f-133">(Observe que  *\`n*  é usado como um delimitador entre propriedades individuais.)</span><span class="sxs-lookup"><span data-stu-id="4e15f-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="4e15f-134">tooget uma lista de quais propriedades RDP personalizadas são configuradas, execute Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e15f-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="4e15f-135">Observe que as propriedades personalizadas somente são mostradas como resultados de saída e não Olá propriedades padrão:</span><span class="sxs-lookup"><span data-stu-id="4e15f-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="4e15f-136">Quando você define as propriedades personalizadas você deve especificar todas as propriedades personalizadas a cada hora; Caso contrário, a configuração de saudação reverte toodisabled.</span><span class="sxs-lookup"><span data-stu-id="4e15f-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="4e15f-137">Exemplos comuns</span><span class="sxs-lookup"><span data-stu-id="4e15f-137">Common examples</span></span>
<span data-ttu-id="4e15f-138">Use Olá redirecionamento de unidade tooenable cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e15f-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="4e15f-139">Use este cmdlet tooenable USB e unidade de redirecionamento:</span><span class="sxs-lookup"><span data-stu-id="4e15f-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="4e15f-140">Use esse compartilhamento de área de transferência do cmdlet toodisable:</span><span class="sxs-lookup"><span data-stu-id="4e15f-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="4e15f-141">Toocompletely se faça logoff de todos os usuários na coleção de saudação (e não apenas desconectá-los) antes de você testar a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e15f-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="4e15f-142">tooensure os usuários são completamente desconectados, vá toohello **sessões** guia na coleção de saudação no hello portal do Azure e logoff de todos os usuários que estão desconectados ou conectados.</span><span class="sxs-lookup"><span data-stu-id="4e15f-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="4e15f-143">Às vezes, pode levar vários segundos para Olá unidades locais tooshow no Gerenciador de sessão hello.</span><span class="sxs-lookup"><span data-stu-id="4e15f-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="4e15f-144">Alterar as configurações de redirecionamento de USB no cliente do Windows</span><span class="sxs-lookup"><span data-stu-id="4e15f-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="4e15f-145">Se você quiser toouse redirecionamento de USB em um computador que se conecta tooRemoteApp, há 2 ações que precisam de toohappen.</span><span class="sxs-lookup"><span data-stu-id="4e15f-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="4e15f-146">1 - o administrador precisa de redirecionamento de USB tooenable no nível de coleção de saudação usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e15f-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="4e15f-147">2 - em cada dispositivo em que você deseja que o redirecionamento de USB toouse, é necessário tooenable uma política de grupo que permite que ele.</span><span class="sxs-lookup"><span data-stu-id="4e15f-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="4e15f-148">Esta etapa terá toobe feito para cada usuário que deseja toouse redirecionamento de USB.</span><span class="sxs-lookup"><span data-stu-id="4e15f-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="4e15f-149">O redirecionamento de USB com o RemoteApp do Azure só tem suporte para computadores com Windows.</span><span class="sxs-lookup"><span data-stu-id="4e15f-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="4e15f-150">Habilitar o redirecionamento de USB para Olá coleção do RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4e15f-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="4e15f-151">Use Olá cmdlet tooenable redirecionamento de USB no nível de coleção Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e15f-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="4e15f-152">Habilitar o redirecionamento de USB para o computador de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="4e15f-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="4e15f-153">configurações de redirecionamento de USB tooconfigure em seu computador:</span><span class="sxs-lookup"><span data-stu-id="4e15f-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="4e15f-154">Olá abrir Editor de diretiva de Grupo Local (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="4e15f-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="4e15f-155">(Execute gpedit.msc no prompt de comando).</span><span class="sxs-lookup"><span data-stu-id="4e15f-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="4e15f-156">Abra **Configuração do Computador\Políticas\Modelos Administrativos\Componentes do Windows\Serviços da Área de Trabalho Remota\Cliente de Conexão da Área de Trabalho Remota\Redirecionamento de Dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="4e15f-157">Clique duas vezes em **Permitir redirecionamento de RDP de outros dispositivos USB RemoteFX com suporte deste computador**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="4e15f-158">Selecione **habilitado**e, em seguida, selecione **administradores e usuários em Olá direitos de acesso de redirecionamento de USB do RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="4e15f-159">Abra um prompt de comando com permissões administrativas e execute o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="4e15f-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="4e15f-160">Reinicie o computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e15f-160">Restart hello computer.</span></span>

<span data-ttu-id="4e15f-161">Você também pode usar o hello toocreate de ferramenta de gerenciamento de política de grupo e aplicar diretiva de redirecionamento de USB Olá para todos os computadores no seu domínio:</span><span class="sxs-lookup"><span data-stu-id="4e15f-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="4e15f-162">Faça logon no controlador de domínio Olá como administrador de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="4e15f-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="4e15f-163">Olá abrir o Console de gerenciamento de diretiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="4e15f-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="4e15f-164">(Clique em **Iniciar > Ferramentas Administrativas > Gerenciamento de Política de Grupo**.)</span><span class="sxs-lookup"><span data-stu-id="4e15f-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="4e15f-165">Navegue toohello domínio ou unidade organizacional para o qual você deseja toocreate política de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e15f-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="4e15f-166">Clique com o botão da direita do mouse em **Política de Domínio Padrão** e, em seguida, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="4e15f-167">Abra **Configuração do Computador\Políticas\Modelos Administrativos\Componentes do Windows\Serviços da Área de Trabalho Remota\Cliente de Conexão da Área de Trabalho Remota\Redirecionamento de Dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="4e15f-168">Clique duas vezes em **Permitir redirecionamento de RDP de outros dispositivos USB RemoteFX com suporte deste computador**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="4e15f-169">Selecione **habilitado**e, em seguida, selecione **administradores e usuários em Olá direitos de acesso de redirecionamento de USB do RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="4e15f-170">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e15f-170">Click **OK**.</span></span>  

