---
title: pacote de suporte de aaaCreate um StorSimple 8000 series | Microsoft Docs
description: "Saiba como toocreate, descriptografar e editar um pacote de suporte para o dispositivo da série StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="a715d-103">Criar e gerenciar um pacote de suporte do StorSimple da série 8000</span><span class="sxs-lookup"><span data-stu-id="a715d-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="a715d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a715d-104">Overview</span></span>

<span data-ttu-id="a715d-105">Um pacote de suporte do StorSimple é um mecanismo fácil de usar que coleta todos os logs relevantes tooassist Microsoft Support na solução de problemas no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a715d-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="a715d-106">Olá logs coletados são criptografados e compactados.</span><span class="sxs-lookup"><span data-stu-id="a715d-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="a715d-107">Este tutorial inclui instruções passo a passo toocreate e gerenciar o pacote de suporte de saudação para seu dispositivo da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="a715d-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="a715d-108">Se você estiver trabalhando com uma matriz Virtual StorSimple, vá muito[gerar um pacote de log](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="a715d-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="a715d-109">Criar um pacote de suporte</span><span class="sxs-lookup"><span data-stu-id="a715d-109">Create a support package</span></span>

<span data-ttu-id="a715d-110">Em alguns casos, você precisará toomanually criar pacote de suporte de saudação por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a715d-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a715d-111">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a715d-111">For example:</span></span>

* <span data-ttu-id="a715d-112">Se você precisar de informações confidenciais de tooremove de seu log de arquivos toosharing anterior com o Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="a715d-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="a715d-113">Se você estiver tendo dificuldades para carregar o pacote hello devido a problemas de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="a715d-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="a715d-114">Você pode compartilhar seu pacote de suporte gerado manualmente com o Suporte da Microsoft por email.</span><span class="sxs-lookup"><span data-stu-id="a715d-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="a715d-115">Execute Olá seguindo as etapas toocreate um pacote de suporte no Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a715d-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a715d-116">toocreate um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="a715d-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="a715d-117">toostart uma sessão do Windows PowerShell como administrador no computador remoto de saudação que tenha usado o dispositivo StorSimple tooyour tooconnect, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a715d-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="a715d-118">Na sessão do Windows PowerShell hello, conecte-se toohello SSAdmin Console do seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a715d-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="a715d-119">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="a715d-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="a715d-120">Na caixa de diálogo de saudação que é aberta, digite sua senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a715d-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="a715d-121">a senha padrão Olá é _Password1_.</span><span class="sxs-lookup"><span data-stu-id="a715d-121">hello default password is _Password1_.</span></span>
     
      ![Caixa de diálogo da credencial do PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="a715d-123">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a715d-123">Select **OK**.</span></span>
   4. <span data-ttu-id="a715d-124">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="a715d-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="a715d-125">Na sessão de saudação que é aberta, insira o comando apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="a715d-126">Para compartilhamentos de rede protegidos por senha, insira:</span><span class="sxs-lookup"><span data-stu-id="a715d-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="a715d-127">Você será solicitado para uma senha, uma caminho toohello pasta compartilhada e uma senha de criptografia (porque o pacote de suporte de saudação é criptografado).</span><span class="sxs-lookup"><span data-stu-id="a715d-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="a715d-128">Um pacote de suporte é criado na pasta especificada hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="a715d-129">Para ações que não são protegidas por senha, você não precisa Olá `-Credential` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a715d-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="a715d-130">Digite hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="a715d-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="a715d-131">pacote de suporte de saudação é criado para ambos os controladores na pasta compartilhada de rede especificado hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="a715d-132">É um arquivo criptografado e compactado que pode ser enviado tooMicrosoft suporte para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="a715d-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="a715d-133">Para obter mais informações, consulte [Contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="a715d-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="a715d-134">Olá parâmetros do cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="a715d-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="a715d-135">Você pode usar o hello parâmetros com hello Export-HcsSupportPackage cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="a715d-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="a715d-136">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a715d-136">Parameter</span></span> | <span data-ttu-id="a715d-137">Obrigatório/Opcional</span><span class="sxs-lookup"><span data-stu-id="a715d-137">Required/Optional</span></span> | <span data-ttu-id="a715d-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="a715d-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="a715d-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a715d-139">Required</span></span> |<span data-ttu-id="a715d-140">Use tooprovide Olá local da pasta compartilhada da rede Olá quais Olá pacote de suporte é colocado.</span><span class="sxs-lookup"><span data-stu-id="a715d-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="a715d-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a715d-141">Required</span></span> |<span data-ttu-id="a715d-142">Use tooprovide toohelp uma frase secreta criptografar o pacote de suporte de saudação.</span><span class="sxs-lookup"><span data-stu-id="a715d-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="a715d-143">Opcional</span><span class="sxs-lookup"><span data-stu-id="a715d-143">Optional</span></span> |<span data-ttu-id="a715d-144">Use credenciais de acesso de toosupply para a pasta compartilhada de rede hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="a715d-145">Opcional</span><span class="sxs-lookup"><span data-stu-id="a715d-145">Optional</span></span> |<span data-ttu-id="a715d-146">Use a etapa de confirmação de senha de criptografia do tooskip hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="a715d-147">Opcional</span><span class="sxs-lookup"><span data-stu-id="a715d-147">Optional</span></span> |<span data-ttu-id="a715d-148">Usar toospecify um diretório em *caminho* que dão suporte a saudação pacote é colocado.</span><span class="sxs-lookup"><span data-stu-id="a715d-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="a715d-149">padrão de saudação é [nome do dispositivo]-[data atual e a data].</span><span class="sxs-lookup"><span data-stu-id="a715d-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="a715d-150">Opcional</span><span class="sxs-lookup"><span data-stu-id="a715d-150">Optional</span></span> |<span data-ttu-id="a715d-151">Especificar como **Cluster** toocreate (padrão) um pacote de suporte para ambos os controladores.</span><span class="sxs-lookup"><span data-stu-id="a715d-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="a715d-152">Se você quiser toocreate um pacote somente para o controlador atual hello, especifique **controlador**.</span><span class="sxs-lookup"><span data-stu-id="a715d-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="a715d-153">Editar um pacote de suporte</span><span class="sxs-lookup"><span data-stu-id="a715d-153">Edit a support package</span></span>

<span data-ttu-id="a715d-154">Após gerar um pacote de suporte, talvez seja necessário tooedit Olá pacote tooremove sigilosos.</span><span class="sxs-lookup"><span data-stu-id="a715d-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="a715d-155">Isso pode incluir nomes de volume, endereços IP do dispositivo e nomes de backup de arquivos de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="a715d-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a715d-156">Você só pode editar um pacote de suporte que tenha sido gerado por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a715d-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a715d-157">Você não pode editar um pacote criado no hello portal do Azure com o serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a715d-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="a715d-158">tooedit um pacote de suporte antes de carregá-lo no site do Microsoft Support hello, primeiro descriptografar o pacote de suporte de hello, editar arquivos hello e, em seguida, criptografe-a novamente.</span><span class="sxs-lookup"><span data-stu-id="a715d-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="a715d-159">Execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="a715d-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a715d-160">tooedit um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="a715d-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="a715d-161">Gerar um pacote de suporte, conforme descrito anteriormente, [toocreate um pacote de suporte no Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="a715d-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="a715d-162">[Baixe o script hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente no seu cliente.</span><span class="sxs-lookup"><span data-stu-id="a715d-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="a715d-163">Importe o módulo do Windows PowerShell de saudação.</span><span class="sxs-lookup"><span data-stu-id="a715d-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="a715d-164">Especifique Olá caminho toohello pasta local em que você baixou o script hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="a715d-165">módulo de saudação tooimport, digite:</span><span class="sxs-lookup"><span data-stu-id="a715d-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="a715d-166">Todos os arquivos de saudação são *. AES* arquivos que são compactados e criptografados.</span><span class="sxs-lookup"><span data-stu-id="a715d-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="a715d-167">toodecompress e descriptografar arquivos, digite:</span><span class="sxs-lookup"><span data-stu-id="a715d-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="a715d-168">Observe que as extensões de arquivo real Olá agora são exibidas para todos os arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a715d-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Editar pacote de suporte](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="a715d-170">Quando você for solicitado para a senha de criptografia hello, insira a frase secreta de saudação que você usou quando o pacote de suporte de saudação foi criado.</span><span class="sxs-lookup"><span data-stu-id="a715d-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="a715d-171">Procure pasta toohello que contém os arquivos de log hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="a715d-172">Porque os arquivos de log de Olá agora são descomprimidos e descriptografados, eles terão as extensões de arquivo original.</span><span class="sxs-lookup"><span data-stu-id="a715d-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="a715d-173">Modificar esses arquivos tooremove todas as informações específicas do cliente, como nomes de volume e endereços IP do dispositivo e salvar arquivos hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="a715d-174">Olá fechar arquivos toocompress-los com gzip e criptografá-los com AES-256.</span><span class="sxs-lookup"><span data-stu-id="a715d-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="a715d-175">Isso é para velocidade e segurança durante a transferência de pacote de suporte de saudação em uma rede.</span><span class="sxs-lookup"><span data-stu-id="a715d-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="a715d-176">toocompress e criptografar os arquivos, digite Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="a715d-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Editar pacote de suporte](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="a715d-178">Quando solicitado, forneça uma senha de criptografia para o pacote de suporte modificado hello.</span><span class="sxs-lookup"><span data-stu-id="a715d-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="a715d-179">Anote Olá nova senha, para que você pode compartilhá-lo com o Microsoft Support quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a715d-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="a715d-180">Exemplo: edição de arquivos em um pacote de suporte em um compartilhamento protegido por senha</span><span class="sxs-lookup"><span data-stu-id="a715d-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="a715d-181">saudação de exemplo a seguir mostra como toodecrypt, editar e criptografar novamente um pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="a715d-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a715d-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a715d-182">Next steps</span></span>

* <span data-ttu-id="a715d-183">Saiba mais sobre Olá [informações coletadas no pacote de suporte de saudação](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="a715d-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="a715d-184">Saiba como muito[use pacotes de suporte e dispositivo logs tootroubleshoot sua implantação de dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a715d-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="a715d-185">Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a715d-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

