---
title: "Criar um pacote de suporte do StorSimple da série 8000 | Microsoft Docs"
description: "Saiba como criar, descriptografar e editar um pacote de suporte para o dispositivo StorSimple da série 8000."
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
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="b46b5-103">Criar e gerenciar um pacote de suporte do StorSimple da série 8000</span><span class="sxs-lookup"><span data-stu-id="b46b5-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="b46b5-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b46b5-104">Overview</span></span>

<span data-ttu-id="b46b5-105">Um pacote de suporte do StorSimple é um mecanismo fácil de usar que coleta todos os logs relevantes para ajudar o Suporte da Microsoft na solução de problemas do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b46b5-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="b46b5-106">Os logs coletados são criptografados e compactados.</span><span class="sxs-lookup"><span data-stu-id="b46b5-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="b46b5-107">Este tutorial inclui instruções passo a passo para criar e gerenciar o pacote de suporte para seu dispositivo StorSimple da série 8000.</span><span class="sxs-lookup"><span data-stu-id="b46b5-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="b46b5-108">Se você estiver trabalhando com uma Matriz Virtual do StorSimple, acesse [Gerar um pacote de log](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="b46b5-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="b46b5-109">Criar um pacote de suporte</span><span class="sxs-lookup"><span data-stu-id="b46b5-109">Create a support package</span></span>

<span data-ttu-id="b46b5-110">Em alguns casos, você precisará criar o pacote de suporte manualmente por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b46b5-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b46b5-111">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b46b5-111">For example:</span></span>

* <span data-ttu-id="b46b5-112">Se você precisar remover informações confidenciais de seus arquivos de log antes de compartilhar com o Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="b46b5-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="b46b5-113">Se você estiver tendo dificuldade para carregar o pacote devido a problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="b46b5-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="b46b5-114">Você pode compartilhar seu pacote de suporte gerado manualmente com o Suporte da Microsoft por email.</span><span class="sxs-lookup"><span data-stu-id="b46b5-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="b46b5-115">Execute as etapas a seguir para criar um pacote de suporte no Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b46b5-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b46b5-116">Para criar um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b46b5-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b46b5-117">Para iniciar uma sessão do Windows PowerShell como administrador no computador remoto usado para se conectar ao dispositivo StorSimple, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b46b5-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="b46b5-118">Na sessão do Windows PowerShell, conecte-se ao console do SSAdmin do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b46b5-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="b46b5-119">No prompt de comando, insira:</span><span class="sxs-lookup"><span data-stu-id="b46b5-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="b46b5-120">Na caixa de diálogo que é aberta, insira sua senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b46b5-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="b46b5-121">A senha padrão é _Senha1_.</span><span class="sxs-lookup"><span data-stu-id="b46b5-121">The default password is _Password1_.</span></span>
     
      ![Caixa de diálogo da credencial do PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="b46b5-123">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="b46b5-123">Select **OK**.</span></span>
   4. <span data-ttu-id="b46b5-124">No prompt de comando, insira:</span><span class="sxs-lookup"><span data-stu-id="b46b5-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="b46b5-125">Na sessão que é aberta, insira o comando apropriado.</span><span class="sxs-lookup"><span data-stu-id="b46b5-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="b46b5-126">Para compartilhamentos de rede protegidos por senha, insira:</span><span class="sxs-lookup"><span data-stu-id="b46b5-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="b46b5-127">Você será solicitado a fornecer uma senha, um caminho para a pasta compartilhada de rede e uma frase secreta de criptografia (porque o pacote de suporte é criptografado).</span><span class="sxs-lookup"><span data-stu-id="b46b5-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="b46b5-128">Um pacote de suporte é criado na pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="b46b5-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="b46b5-129">Para compartilhamentos que não são protegidos por senha, o parâmetro `-Credential` não é necessário.</span><span class="sxs-lookup"><span data-stu-id="b46b5-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="b46b5-130">Insira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b46b5-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="b46b5-131">O pacote de suporte é criado para ambos os controladores na pasta compartilhada de rede especificada.</span><span class="sxs-lookup"><span data-stu-id="b46b5-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="b46b5-132">Ele é um arquivo compactado e criptografado que pode ser enviado ao Suporte da Microsoft para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="b46b5-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="b46b5-133">Para obter mais informações, consulte [Contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b46b5-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="b46b5-134">Os parâmetros do cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="b46b5-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="b46b5-135">Você pode usar os seguintes parâmetros com o cmdlet Export-HcsSupportPackage.</span><span class="sxs-lookup"><span data-stu-id="b46b5-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="b46b5-136">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b46b5-136">Parameter</span></span> | <span data-ttu-id="b46b5-137">Obrigatório/Opcional</span><span class="sxs-lookup"><span data-stu-id="b46b5-137">Required/Optional</span></span> | <span data-ttu-id="b46b5-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="b46b5-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="b46b5-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b46b5-139">Required</span></span> |<span data-ttu-id="b46b5-140">Use para fornecer o local da pasta compartilhada de rede na qual o pacote de suporte é colocado.</span><span class="sxs-lookup"><span data-stu-id="b46b5-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="b46b5-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b46b5-141">Required</span></span> |<span data-ttu-id="b46b5-142">Use para fornecer uma frase secreta para ajudar a criptografar o pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="b46b5-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="b46b5-143">Opcional</span><span class="sxs-lookup"><span data-stu-id="b46b5-143">Optional</span></span> |<span data-ttu-id="b46b5-144">Use para fornecer credenciais de acesso para a pasta compartilhada de rede.</span><span class="sxs-lookup"><span data-stu-id="b46b5-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="b46b5-145">Opcional</span><span class="sxs-lookup"><span data-stu-id="b46b5-145">Optional</span></span> |<span data-ttu-id="b46b5-146">Use para ignorar a etapa de confirmação de frase secreta de criptografia.</span><span class="sxs-lookup"><span data-stu-id="b46b5-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="b46b5-147">Opcional</span><span class="sxs-lookup"><span data-stu-id="b46b5-147">Optional</span></span> |<span data-ttu-id="b46b5-148">Use para especificar um diretório no *Caminho* no qual o pacote de suporte é colocado.</span><span class="sxs-lookup"><span data-stu-id="b46b5-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="b46b5-149">O padrão é [nome do dispositivo]-[data e hora atuais:aaaa-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="b46b5-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="b46b5-150">Opcional</span><span class="sxs-lookup"><span data-stu-id="b46b5-150">Optional</span></span> |<span data-ttu-id="b46b5-151">Especifique como **Cluster** (padrão) para criar um pacote de suporte para ambos os controladores.</span><span class="sxs-lookup"><span data-stu-id="b46b5-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="b46b5-152">Se você quiser criar um pacote somente para o controlador atual, especifique **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="b46b5-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="b46b5-153">Editar um pacote de suporte</span><span class="sxs-lookup"><span data-stu-id="b46b5-153">Edit a support package</span></span>

<span data-ttu-id="b46b5-154">Após gerar um pacote de suporte, talvez seja necessário editar o pacote para remover informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b46b5-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="b46b5-155">Isso pode incluir nomes de volume, endereços IP do dispositivo e nomes de backup dos arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="b46b5-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b46b5-156">Você só pode editar um pacote de suporte que tenha sido gerado por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b46b5-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b46b5-157">Não é possível editar um pacote criado no Portal do Azure com o serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b46b5-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="b46b5-158">Para editar um pacote de suporte antes de carregá-lo no site de Suporte da Microsoft, primeiro descriptografe o pacote de suporte, edite os arquivos e criptografe-os novamente.</span><span class="sxs-lookup"><span data-stu-id="b46b5-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="b46b5-159">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b46b5-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b46b5-160">Para editar um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b46b5-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b46b5-161">Gere um pacote de suporte conforme descrito anteriormente, em [Para criar um pacote de suporte no Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b46b5-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="b46b5-162">[Baixe o script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente em seu cliente.</span><span class="sxs-lookup"><span data-stu-id="b46b5-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="b46b5-163">Importe o módulo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b46b5-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="b46b5-164">Especifique o caminho para a pasta local em que você baixou o script.</span><span class="sxs-lookup"><span data-stu-id="b46b5-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="b46b5-165">Para importar o módulo, insira:</span><span class="sxs-lookup"><span data-stu-id="b46b5-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="b46b5-166">Todos os arquivos são arquivos *.aes* compactados e criptografados.</span><span class="sxs-lookup"><span data-stu-id="b46b5-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="b46b5-167">Para descompactar e descriptografar arquivos, insira:</span><span class="sxs-lookup"><span data-stu-id="b46b5-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="b46b5-168">Observe que as extensões de arquivo reais agora são exibidas para todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="b46b5-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Editar pacote de suporte](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="b46b5-170">Quando você for solicitado a fornecer a senha de criptografia, digite a frase secreta usada quando o pacote de suporte foi criado.</span><span class="sxs-lookup"><span data-stu-id="b46b5-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="b46b5-171">Navegue até a pasta que contém os arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="b46b5-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="b46b5-172">Como os arquivos de log agora estão descompactados e descriptografados, eles terão as extensões de arquivo originais.</span><span class="sxs-lookup"><span data-stu-id="b46b5-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="b46b5-173">Modifique esses arquivos para remover todas as informações específicas do cliente, como nomes de volume e endereços IP de dispositivos, e salve os arquivos.</span><span class="sxs-lookup"><span data-stu-id="b46b5-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="b46b5-174">Feche os arquivos para compactá-los com o gzip e criptografe-os com AES-256.</span><span class="sxs-lookup"><span data-stu-id="b46b5-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="b46b5-175">Isso é para a velocidade e segurança ao transferir o pacote de suporte em uma rede.</span><span class="sxs-lookup"><span data-stu-id="b46b5-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="b46b5-176">Para compactar e criptografar arquivos, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b46b5-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Editar pacote de suporte](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="b46b5-178">Quando solicitado, forneça uma frase secreta de criptografia para o pacote de suporte modificado.</span><span class="sxs-lookup"><span data-stu-id="b46b5-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="b46b5-179">Anote a nova senha para que você possa compartilhá-la com o Suporte da Microsoft quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="b46b5-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="b46b5-180">Exemplo: edição de arquivos em um pacote de suporte em um compartilhamento protegido por senha</span><span class="sxs-lookup"><span data-stu-id="b46b5-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="b46b5-181">O exemplo a seguir mostra como descriptografar, editar e criptografar novamente um pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="b46b5-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="b46b5-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b46b5-182">Next steps</span></span>

* <span data-ttu-id="b46b5-183">Saiba mais sobre as [informações coletadas no pacote de Suporte](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="b46b5-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="b46b5-184">Saiba como [usar pacotes de suporte e logs de dispositivo para solucionar problemas de implantação do dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b46b5-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="b46b5-185">Saiba como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b46b5-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

