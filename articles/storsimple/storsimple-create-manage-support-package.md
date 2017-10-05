---
title: Criar um pacote de suporte do StorSimple | Microsoft Docs
description: Saiba como criar, descriptografar e editar um pacote de suporte para o dispositivo StorSimple.
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
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="027e1-103">Criar e gerenciar um pacote de suporte do StorSimple</span><span class="sxs-lookup"><span data-stu-id="027e1-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="027e1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="027e1-104">Overview</span></span>
<span data-ttu-id="027e1-105">Um pacote de suporte do StorSimple é um mecanismo fácil de usar que coleta todos os logs relevantes para ajudar o Suporte da Microsoft na solução de problemas do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="027e1-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="027e1-106">Os logs coletados são criptografados e compactados.</span><span class="sxs-lookup"><span data-stu-id="027e1-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="027e1-107">Este tutorial inclui instruções passo a passo para criar e gerenciar o pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="027e1-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="027e1-108">Criar e carregar um pacote de suporte no Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="027e1-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="027e1-109">Você pode criar e carregar um pacote de suporte para o site do Suporte da Microsoft por meio da página **Manutenção** do serviço no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="027e1-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="027e1-110">O upload requer uma chave de acesso de suporte.</span><span class="sxs-lookup"><span data-stu-id="027e1-110">The upload requires a support passkey.</span></span> <span data-ttu-id="027e1-111">Seu engenheiro de suporte deve fornecê-la para você em um email.</span><span class="sxs-lookup"><span data-stu-id="027e1-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="027e1-112">Um pacote de suporte criptografado e compactado (arquivo .cab) é criado e carregado para o site de suporte.</span><span class="sxs-lookup"><span data-stu-id="027e1-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="027e1-113">O engenheiro de suporte pode recuperar esse pacote do site de suporte para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="027e1-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="027e1-114">Execute as seguintes etapas no portal clássico para criar um pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="027e1-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="027e1-115">Para criar um pacote de suporte no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="027e1-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="027e1-116">Selecione **Dispositivos** > **Manutenção**.</span><span class="sxs-lookup"><span data-stu-id="027e1-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="027e1-117">Na seção **Pacote de suporte**, selecione **Criar e carregar pacote de suporte**.</span><span class="sxs-lookup"><span data-stu-id="027e1-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="027e1-118">Na caixa de diálogo **Criar e carregar pacote de suporte** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="027e1-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Criar um pacote de suporte](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="027e1-120">Na caixa de texto **Chave de acesso de suporte** , digite a chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="027e1-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="027e1-121">Seu engenheiro de suporte da Microsoft deve enviar essa chave de acesso para você por email.</span><span class="sxs-lookup"><span data-stu-id="027e1-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="027e1-122">Selecione a caixa de seleção para fornecer consentimento para carregar automaticamente o pacote de suporte para o site de Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="027e1-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="027e1-123">Clique no ícone de verificação </span><span class="sxs-lookup"><span data-stu-id="027e1-123">Click the check icon</span></span> ![Ícone de verificação](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="027e1-125">.</span><span class="sxs-lookup"><span data-stu-id="027e1-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="027e1-126">Criar um pacote de suporte manualmente</span><span class="sxs-lookup"><span data-stu-id="027e1-126">Manually create a support package</span></span>
<span data-ttu-id="027e1-127">Em alguns casos, você precisará criar o pacote de suporte manualmente por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="027e1-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="027e1-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="027e1-128">For example:</span></span>

* <span data-ttu-id="027e1-129">Se você precisar remover informações confidenciais de seus arquivos de log antes de compartilhar com o Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="027e1-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="027e1-130">Se você estiver tendo dificuldade para carregar o pacote devido a problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="027e1-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="027e1-131">Você pode compartilhar seu pacote de suporte gerado manualmente com o Suporte da Microsoft por email.</span><span class="sxs-lookup"><span data-stu-id="027e1-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="027e1-132">Execute as etapas a seguir para criar um pacote de suporte no Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="027e1-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="027e1-133">Para criar um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="027e1-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="027e1-134">Para iniciar uma sessão do Windows PowerShell como administrador no computador remoto usado para se conectar ao dispositivo StorSimple, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="027e1-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="027e1-135">Na sessão do Windows PowerShell, conecte-se ao console do SSAdmin do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="027e1-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="027e1-136">No prompt de comando, insira:</span><span class="sxs-lookup"><span data-stu-id="027e1-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="027e1-137">Na caixa de diálogo que é aberta, insira sua senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="027e1-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="027e1-138">A senha padrão é:</span><span class="sxs-lookup"><span data-stu-id="027e1-138">The default password is:</span></span>
     
      `Password1`
     
      ![Caixa de diálogo da credencial do PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="027e1-140">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="027e1-140">Select **OK**.</span></span>
   * <span data-ttu-id="027e1-141">No prompt de comando, insira:</span><span class="sxs-lookup"><span data-stu-id="027e1-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="027e1-142">Na sessão que é aberta, insira o comando apropriado.</span><span class="sxs-lookup"><span data-stu-id="027e1-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="027e1-143">Para compartilhamentos de rede protegidos por senha, insira:</span><span class="sxs-lookup"><span data-stu-id="027e1-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="027e1-144">Você será solicitado a fornecer uma senha, um caminho para a pasta compartilhada de rede e uma frase secreta de criptografia (porque o pacote de suporte é criptografado).</span><span class="sxs-lookup"><span data-stu-id="027e1-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="027e1-145">Um pacote de suporte é criado na pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="027e1-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="027e1-146">Para compartilhamentos que não são protegidos por senha, o parâmetro `-Credential` não é necessário.</span><span class="sxs-lookup"><span data-stu-id="027e1-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="027e1-147">Insira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="027e1-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="027e1-148">O pacote de suporte é criado para ambos os controladores na pasta compartilhada de rede especificada.</span><span class="sxs-lookup"><span data-stu-id="027e1-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="027e1-149">Ele é um arquivo compactado e criptografado que pode ser enviado ao Suporte da Microsoft para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="027e1-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="027e1-150">Para obter mais informações, consulte [Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="027e1-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="027e1-151">Os parâmetros do cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="027e1-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="027e1-152">Você pode usar os seguintes parâmetros com o cmdlet Export-HcsSupportPackage.</span><span class="sxs-lookup"><span data-stu-id="027e1-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="027e1-153">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="027e1-153">Parameter</span></span> | <span data-ttu-id="027e1-154">Obrigatório/Opcional</span><span class="sxs-lookup"><span data-stu-id="027e1-154">Required/Optional</span></span> | <span data-ttu-id="027e1-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="027e1-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="027e1-156">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="027e1-156">Required</span></span> |<span data-ttu-id="027e1-157">Use para fornecer o local da pasta compartilhada de rede na qual o pacote de suporte é colocado.</span><span class="sxs-lookup"><span data-stu-id="027e1-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="027e1-158">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="027e1-158">Required</span></span> |<span data-ttu-id="027e1-159">Use para fornecer uma frase secreta para ajudar a criptografar o pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="027e1-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="027e1-160">Opcional</span><span class="sxs-lookup"><span data-stu-id="027e1-160">Optional</span></span> |<span data-ttu-id="027e1-161">Use para fornecer credenciais de acesso para a pasta compartilhada de rede.</span><span class="sxs-lookup"><span data-stu-id="027e1-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="027e1-162">Opcional</span><span class="sxs-lookup"><span data-stu-id="027e1-162">Optional</span></span> |<span data-ttu-id="027e1-163">Use para ignorar a etapa de confirmação de frase secreta de criptografia.</span><span class="sxs-lookup"><span data-stu-id="027e1-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="027e1-164">Opcional</span><span class="sxs-lookup"><span data-stu-id="027e1-164">Optional</span></span> |<span data-ttu-id="027e1-165">Use para especificar um diretório no *Caminho* no qual o pacote de suporte é colocado.</span><span class="sxs-lookup"><span data-stu-id="027e1-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="027e1-166">O padrão é [nome do dispositivo]-[data e hora atuais:aaaa-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="027e1-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="027e1-167">Opcional</span><span class="sxs-lookup"><span data-stu-id="027e1-167">Optional</span></span> |<span data-ttu-id="027e1-168">Especifique como **Cluster** (padrão) para criar um pacote de suporte para ambos os controladores.</span><span class="sxs-lookup"><span data-stu-id="027e1-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="027e1-169">Se você quiser criar um pacote somente para o controlador atual, especifique **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="027e1-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="027e1-170">Editar um pacote de suporte</span><span class="sxs-lookup"><span data-stu-id="027e1-170">Edit a support package</span></span>
<span data-ttu-id="027e1-171">Após gerar um pacote de suporte, talvez seja necessário editar o pacote para remover informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="027e1-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="027e1-172">Isso pode incluir nomes de volume, endereços IP do dispositivo e nomes de backup dos arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="027e1-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="027e1-173">Você só pode editar um pacote de suporte que tenha sido gerado por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="027e1-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="027e1-174">Você não pode editar um pacote criado no Portal Clássico do Azure com o serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="027e1-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="027e1-175">Para editar um pacote de suporte antes de carregá-lo no site de Suporte da Microsoft, primeiro descriptografe o pacote de suporte, edite os arquivos e criptografe-os novamente.</span><span class="sxs-lookup"><span data-stu-id="027e1-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="027e1-176">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="027e1-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="027e1-177">Para editar um pacote de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="027e1-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="027e1-178">Gere um pacote de suporte conforme descrito anteriormente, em [Para criar um pacote de suporte no Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="027e1-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="027e1-179">[Baixe o script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente em seu cliente.</span><span class="sxs-lookup"><span data-stu-id="027e1-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="027e1-180">Importe o módulo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="027e1-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="027e1-181">Especifique o caminho para a pasta local em que você baixou o script.</span><span class="sxs-lookup"><span data-stu-id="027e1-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="027e1-182">Para importar o módulo, insira:</span><span class="sxs-lookup"><span data-stu-id="027e1-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="027e1-183">Todos os arquivos são arquivos *.aes* compactados e criptografados.</span><span class="sxs-lookup"><span data-stu-id="027e1-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="027e1-184">Para descompactar e descriptografar arquivos, insira:</span><span class="sxs-lookup"><span data-stu-id="027e1-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="027e1-185">Observe que as extensões de arquivo reais agora são exibidas para todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="027e1-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Editar pacote de suporte](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="027e1-187">Quando você for solicitado a fornecer a senha de criptografia, digite a frase secreta usada quando o pacote de suporte foi criado.</span><span class="sxs-lookup"><span data-stu-id="027e1-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="027e1-188">Navegue até a pasta que contém os arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="027e1-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="027e1-189">Como os arquivos de log agora estão descompactados e descriptografados, eles terão as extensões de arquivo originais.</span><span class="sxs-lookup"><span data-stu-id="027e1-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="027e1-190">Modifique esses arquivos para remover todas as informações específicas do cliente, como nomes de volume e endereços IP de dispositivos, e salve os arquivos.</span><span class="sxs-lookup"><span data-stu-id="027e1-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="027e1-191">Feche os arquivos para compactá-los com o gzip e criptografe-os com AES-256.</span><span class="sxs-lookup"><span data-stu-id="027e1-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="027e1-192">Isso é para a velocidade e segurança ao transferir o pacote de suporte em uma rede.</span><span class="sxs-lookup"><span data-stu-id="027e1-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="027e1-193">Para compactar e criptografar arquivos, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="027e1-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Editar pacote de suporte](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="027e1-195">Quando solicitado, forneça uma frase secreta de criptografia para o pacote de suporte modificado.</span><span class="sxs-lookup"><span data-stu-id="027e1-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="027e1-196">Anote a nova senha para que você possa compartilhá-la com o Suporte da Microsoft quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="027e1-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="027e1-197">Exemplo: edição de arquivos em um pacote de suporte em um compartilhamento protegido por senha</span><span class="sxs-lookup"><span data-stu-id="027e1-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="027e1-198">O exemplo a seguir mostra como descriptografar, editar e criptografar novamente um pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="027e1-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="027e1-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="027e1-199">Next steps</span></span>
* <span data-ttu-id="027e1-200">Saiba como [usar pacotes de suporte e logs de dispositivo para solucionar problemas de implantação do dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="027e1-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="027e1-201">Saiba como [usar o serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="027e1-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

