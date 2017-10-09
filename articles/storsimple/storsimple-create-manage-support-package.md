---
title: aaaCreate um pacote de suporte do StorSimple | Microsoft Docs
description: Saiba como toocreate, descriptografar e editar um pacote de suporte para seu dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="7f69a-103">Criar e gerenciar um pacote de suporte do StorSimple</span><span class="sxs-lookup"><span data-stu-id="7f69a-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="7f69a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7f69a-104">Overview</span></span>
<span data-ttu-id="7f69a-105">Um pacote de suporte do StorSimple é um mecanismo fácil de usar que coleta todos os logs relevantes tooassist Microsoft Support na solução de problemas no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f69a-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="7f69a-106">Olá logs coletados são criptografados e compactados.</span><span class="sxs-lookup"><span data-stu-id="7f69a-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="7f69a-107">Este tutorial inclui instruções passo a passo toocreate e gerenciar o pacote de suporte de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-107">This tutorial includes step-by-step instructions toocreate and manage hello support package.</span></span>

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="7f69a-108">Criar e carregar um pacote de suporte em Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7f69a-108">Create and upload a support package in hello Azure classic portal</span></span>
<span data-ttu-id="7f69a-109">Você pode criar e carregar um site do Microsoft Support suporte pacote toohello por meio de saudação **manutenção** página serviço de saudação do hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f69a-109">You can create and upload a support package toohello Microsoft Support site through hello **Maintenance** page of hello service in hello Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7f69a-110">carregamento de saudação requer uma chave de acesso de suporte.</span><span class="sxs-lookup"><span data-stu-id="7f69a-110">hello upload requires a support passkey.</span></span> <span data-ttu-id="7f69a-111">Seu engenheiro de suporte deve fornecer esse tooyou em um email.</span><span class="sxs-lookup"><span data-stu-id="7f69a-111">Your support engineer should provide this tooyou in an email.</span></span>
> 
> 

<span data-ttu-id="7f69a-112">Um pacote de suporte criptografado e compactado (arquivo. cab) é criado e carregado toohello site de suporte.</span><span class="sxs-lookup"><span data-stu-id="7f69a-112">An encrypted and compressed support package (.cab file) is created and uploaded toohello Support site.</span></span> <span data-ttu-id="7f69a-113">engenheiro de suporte de saudação pode então recuperar esse pacote hello no site de suporte para solução de problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-113">hello support engineer can then retrieve this package from hello Support site for troubleshooting hello issue.</span></span>

<span data-ttu-id="7f69a-114">Execute Olá etapas toocreate portal clássico Olá um pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="7f69a-114">Perform hello following steps in hello classic portal toocreate a support package.</span></span>

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="7f69a-115">toocreate um pacote de suporte em Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7f69a-115">toocreate a support package in hello Azure classic portal</span></span>
1. <span data-ttu-id="7f69a-116">Selecione **Dispositivos** > **Manutenção**.</span><span class="sxs-lookup"><span data-stu-id="7f69a-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="7f69a-117">Em Olá **pacote de suporte** seção, selecione **criar e carregar pacote de suporte**.</span><span class="sxs-lookup"><span data-stu-id="7f69a-117">In hello **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="7f69a-118">Em Olá **criar e carregar pacote de suporte** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f69a-118">In hello **Create and upload support package** dialog box, do hello following:</span></span>
   
    ![Criar um pacote de suporte](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="7f69a-120">Em Olá **chave de acesso de suporte** texto, digite a chave de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-120">In hello **Support Passkey** text box, enter hello passkey.</span></span> <span data-ttu-id="7f69a-121">Seu engenheiro de suporte da Microsoft deve enviar tooyou esta chave de acesso no email.</span><span class="sxs-lookup"><span data-stu-id="7f69a-121">Your Microsoft support engineer should send this passkey tooyou in email.</span></span>
   * <span data-ttu-id="7f69a-122">Selecione Olá caixa de seleção tooprovide consentimento tooautomatically carregamento Olá suporte pacote toohello Microsoft Support site.</span><span class="sxs-lookup"><span data-stu-id="7f69a-122">Select hello check box tooprovide consent tooautomatically upload hello support package toohello Microsoft Support site.</span></span>
   * <span data-ttu-id="7f69a-123">Clique o ícone de verificação Olá</span><span class="sxs-lookup"><span data-stu-id="7f69a-123">Click hello check icon</span></span> ![Ícone de verificação](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="7f69a-125">.</span><span class="sxs-lookup"><span data-stu-id="7f69a-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="7f69a-126">Criar um pacote de suporte manualmente</span><span class="sxs-lookup"><span data-stu-id="7f69a-126">Manually create a support package</span></span>
<span data-ttu-id="7f69a-127">Em alguns casos, você precisará toomanually criar pacote de suporte de saudação por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f69a-127">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7f69a-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7f69a-128">For example:</span></span>

* <span data-ttu-id="7f69a-129">Se você precisar de informações confidenciais de tooremove de seu log de arquivos toosharing anterior com o Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="7f69a-129">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="7f69a-130">Se você estiver tendo dificuldades para carregar o pacote hello devido a problemas de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="7f69a-130">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="7f69a-131">Você pode compartilhar seu pacote de suporte gerado manualmente com o Suporte da Microsoft por email.</span><span class="sxs-lookup"><span data-stu-id="7f69a-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="7f69a-132">Execute Olá seguindo as etapas toocreate um pacote de suporte no Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f69a-132">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7f69a-133">toocreate um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="7f69a-133">toocreate a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7f69a-134">toostart uma sessão do Windows PowerShell como administrador no computador remoto de saudação que tenha usado o dispositivo StorSimple tooyour tooconnect, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f69a-134">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="7f69a-135">Na sessão do Windows PowerShell hello, conecte-se toohello SSAdmin Console do seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7f69a-135">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="7f69a-136">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="7f69a-136">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="7f69a-137">Na caixa de diálogo de saudação que é aberta, digite sua senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7f69a-137">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="7f69a-138">saudação padrão senha é:</span><span class="sxs-lookup"><span data-stu-id="7f69a-138">hello default password is:</span></span>
     
      `Password1`
     
      ![Caixa de diálogo da credencial do PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="7f69a-140">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f69a-140">Select **OK**.</span></span>
   * <span data-ttu-id="7f69a-141">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="7f69a-141">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="7f69a-142">Na sessão de saudação que é aberta, insira o comando apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-142">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="7f69a-143">Para compartilhamentos de rede protegidos por senha, insira:</span><span class="sxs-lookup"><span data-stu-id="7f69a-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="7f69a-144">Você será solicitado para uma senha, uma caminho toohello pasta compartilhada e uma senha de criptografia (porque o pacote de suporte de saudação é criptografado).</span><span class="sxs-lookup"><span data-stu-id="7f69a-144">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="7f69a-145">Um pacote de suporte é criado na pasta especificada hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-145">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="7f69a-146">Para ações que não são protegidas por senha, você não precisa Olá `-Credential` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7f69a-146">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="7f69a-147">Digite hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="7f69a-147">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="7f69a-148">pacote de suporte de saudação é criado para ambos os controladores na pasta compartilhada de rede especificado hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-148">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="7f69a-149">É um arquivo criptografado e compactado que pode ser enviado tooMicrosoft suporte para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="7f69a-149">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="7f69a-150">Para obter mais informações, consulte [Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="7f69a-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="7f69a-151">Olá parâmetros do cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="7f69a-151">hello Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="7f69a-152">Você pode usar o hello parâmetros com hello Export-HcsSupportPackage cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f69a-152">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="7f69a-153">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="7f69a-153">Parameter</span></span> | <span data-ttu-id="7f69a-154">Obrigatório/Opcional</span><span class="sxs-lookup"><span data-stu-id="7f69a-154">Required/Optional</span></span> | <span data-ttu-id="7f69a-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="7f69a-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="7f69a-156">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7f69a-156">Required</span></span> |<span data-ttu-id="7f69a-157">Use tooprovide Olá local da pasta compartilhada da rede Olá quais Olá pacote de suporte é colocado.</span><span class="sxs-lookup"><span data-stu-id="7f69a-157">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="7f69a-158">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7f69a-158">Required</span></span> |<span data-ttu-id="7f69a-159">Use tooprovide toohelp uma frase secreta criptografar o pacote de suporte de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-159">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="7f69a-160">Opcional</span><span class="sxs-lookup"><span data-stu-id="7f69a-160">Optional</span></span> |<span data-ttu-id="7f69a-161">Use credenciais de acesso de toosupply para a pasta compartilhada de rede hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-161">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="7f69a-162">Opcional</span><span class="sxs-lookup"><span data-stu-id="7f69a-162">Optional</span></span> |<span data-ttu-id="7f69a-163">Use a etapa de confirmação de senha de criptografia do tooskip hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-163">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="7f69a-164">Opcional</span><span class="sxs-lookup"><span data-stu-id="7f69a-164">Optional</span></span> |<span data-ttu-id="7f69a-165">Usar toospecify um diretório em *caminho* que dão suporte a saudação pacote é colocado.</span><span class="sxs-lookup"><span data-stu-id="7f69a-165">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="7f69a-166">padrão de saudação é [nome do dispositivo]-[data atual e a data].</span><span class="sxs-lookup"><span data-stu-id="7f69a-166">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="7f69a-167">Opcional</span><span class="sxs-lookup"><span data-stu-id="7f69a-167">Optional</span></span> |<span data-ttu-id="7f69a-168">Especificar como **Cluster** toocreate (padrão) um pacote de suporte para ambos os controladores.</span><span class="sxs-lookup"><span data-stu-id="7f69a-168">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="7f69a-169">Se você quiser toocreate um pacote somente para o controlador atual hello, especifique **controlador**.</span><span class="sxs-lookup"><span data-stu-id="7f69a-169">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="7f69a-170">Editar um pacote de suporte</span><span class="sxs-lookup"><span data-stu-id="7f69a-170">Edit a support package</span></span>
<span data-ttu-id="7f69a-171">Após gerar um pacote de suporte, talvez seja necessário tooedit Olá pacote tooremove sigilosos.</span><span class="sxs-lookup"><span data-stu-id="7f69a-171">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="7f69a-172">Isso pode incluir nomes de volume, endereços IP do dispositivo e nomes de backup de arquivos de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-172">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f69a-173">Você só pode editar um pacote de suporte que tenha sido gerado por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f69a-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7f69a-174">Você não pode editar um pacote criado no hello portal clássico do Azure com o serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7f69a-174">You can't edit a package created in hello Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="7f69a-175">tooedit um pacote de suporte antes de carregá-lo no site do Microsoft Support hello, primeiro descriptografar o pacote de suporte de hello, editar arquivos hello e, em seguida, criptografe-a novamente.</span><span class="sxs-lookup"><span data-stu-id="7f69a-175">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="7f69a-176">Execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f69a-176">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7f69a-177">tooedit um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="7f69a-177">tooedit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7f69a-178">Gerar um pacote de suporte, conforme descrito anteriormente, [toocreate um pacote de suporte no Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="7f69a-178">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="7f69a-179">[Baixe o script hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente no seu cliente.</span><span class="sxs-lookup"><span data-stu-id="7f69a-179">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="7f69a-180">Importe o módulo do Windows PowerShell de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-180">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="7f69a-181">Especifique Olá caminho toohello pasta local em que você baixou o script hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-181">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="7f69a-182">módulo de saudação tooimport, digite:</span><span class="sxs-lookup"><span data-stu-id="7f69a-182">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="7f69a-183">Todos os arquivos de saudação são *. AES* arquivos que são compactados e criptografados.</span><span class="sxs-lookup"><span data-stu-id="7f69a-183">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="7f69a-184">toodecompress e descriptografar arquivos, digite:</span><span class="sxs-lookup"><span data-stu-id="7f69a-184">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="7f69a-185">Observe que as extensões de arquivo real Olá agora são exibidas para todos os arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f69a-185">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Editar pacote de suporte](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="7f69a-187">Quando você for solicitado para a senha de criptografia hello, insira a frase secreta de saudação que você usou quando o pacote de suporte de saudação foi criado.</span><span class="sxs-lookup"><span data-stu-id="7f69a-187">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="7f69a-188">Procure pasta toohello que contém os arquivos de log hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-188">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="7f69a-189">Porque os arquivos de log de Olá agora são descomprimidos e descriptografados, eles terão as extensões de arquivo original.</span><span class="sxs-lookup"><span data-stu-id="7f69a-189">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="7f69a-190">Modificar esses arquivos tooremove todas as informações específicas do cliente, como nomes de volume e endereços IP do dispositivo e salvar arquivos hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-190">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="7f69a-191">Olá fechar arquivos toocompress-los com gzip e criptografá-los com AES-256.</span><span class="sxs-lookup"><span data-stu-id="7f69a-191">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="7f69a-192">Isso é para velocidade e segurança durante a transferência de pacote de suporte de saudação em uma rede.</span><span class="sxs-lookup"><span data-stu-id="7f69a-192">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="7f69a-193">toocompress e criptografar os arquivos, digite Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="7f69a-193">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Editar pacote de suporte](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="7f69a-195">Quando solicitado, forneça uma senha de criptografia para o pacote de suporte modificado hello.</span><span class="sxs-lookup"><span data-stu-id="7f69a-195">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="7f69a-196">Anote Olá nova senha, para que você pode compartilhá-lo com o Microsoft Support quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="7f69a-196">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="7f69a-197">Exemplo: edição de arquivos em um pacote de suporte em um compartilhamento protegido por senha</span><span class="sxs-lookup"><span data-stu-id="7f69a-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="7f69a-198">saudação de exemplo a seguir mostra como toodecrypt, editar e criptografar novamente um pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="7f69a-198">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="7f69a-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f69a-199">Next steps</span></span>
* <span data-ttu-id="7f69a-200">Saiba como muito[use pacotes de suporte e dispositivo logs tootroubleshoot sua implantação de dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7f69a-200">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="7f69a-201">Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7f69a-201">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

