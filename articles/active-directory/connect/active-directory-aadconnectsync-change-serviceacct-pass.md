---
title: "Sincronização do Azure AD Connect: alterando a conta do serviço de sincronização do Azure AD Connect | Microsoft Docs"
description: "Este documento tópico descreve a chave de criptografia e como abandoná-la depois que a senha tiver sido alterada."
services: active-directory
keywords: "Conta do serviço de sincronização do Azure AD, senha"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="c1872-104">Alteração da senha da conta do serviço de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c1872-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="c1872-105">Se você alterar a senha de conta do serviço de sincronização do Azure AD Connect, o serviço de sincronização não será capaz de iniciar corretamente até você ter abandonado a chave de criptografia e reinicializado a senha da conta do serviço de sincronização do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c1872-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="c1872-106">O Azure AD Connect, como parte dos serviços de sincronização, usa uma chave de criptografia para armazenar as senhas das contas de serviço do AD DS e do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1872-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="c1872-107">Essas contas são criptografadas antes de serem armazenadas no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c1872-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="c1872-108">A chave de criptografia usada é protegida usando o [Data Protection do Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1872-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="c1872-109">O DPAPI protege a chave de criptografia usando a **senha da conta do serviço de sincronização do Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="c1872-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="c1872-110">Se você precisar alterar a senha da conta do serviço, use os procedimentos em [Abandono da chave de criptografia de sincronização do Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key) para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c1872-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="c1872-111">Estes procedimentos também deverão ser usados se você precisar abandonar a chave de criptografia por algum motivo.</span><span class="sxs-lookup"><span data-stu-id="c1872-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="c1872-112">Os problemas que surgem da alteração da senha</span><span class="sxs-lookup"><span data-stu-id="c1872-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="c1872-113">Há duas coisas que precisam ser feitas quando você altera a senha da conta do serviço.</span><span class="sxs-lookup"><span data-stu-id="c1872-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="c1872-114">Primeiro, você precisa alterar a senha no Gerenciador de Controle de Serviços do Windows.</span><span class="sxs-lookup"><span data-stu-id="c1872-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="c1872-115">Até que esse problema seja resolvido, você verá os seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="c1872-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="c1872-116">Se você tentar iniciar o serviço de sincronização no Gerenciador de Controle de Serviços do Windows, receberá o erro "**O Windows não pôde iniciar o serviço de sincronização do Microsoft Azure AD no computador local**".</span><span class="sxs-lookup"><span data-stu-id="c1872-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="c1872-117">**Erro 1069: O serviço não foi iniciado devido a uma falha de logon.**"</span><span class="sxs-lookup"><span data-stu-id="c1872-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="c1872-118">No Visualizador de Eventos do Windows, o log de eventos do sistema contém um erro com **ID de evento 7038** e a mensagem "**O serviço ADSync não pôde fazer logon com a senha configurada atualmente devido ao seguinte erro: nome de usuário ou senha incorretos.**"</span><span class="sxs-lookup"><span data-stu-id="c1872-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="c1872-119">Segundo, sob condições específicas, se a senha for atualizada, o serviço de sincronização não poderá mais recuperar a chave de criptografia pelo DPAPI.</span><span class="sxs-lookup"><span data-stu-id="c1872-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="c1872-120">Sem a chave de criptografia, o serviço de sincronização não poderá descriptografar as senhas necessárias para sincronizar de/para o AD local e o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1872-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="c1872-121">Você verá erros, como:</span><span class="sxs-lookup"><span data-stu-id="c1872-121">You will see errors such as:</span></span>

- <span data-ttu-id="c1872-122">No Gerenciador de Controle de Serviços do Windows, se você tentar iniciar o serviço de sincronização e ele não conseguir recuperar a chave de criptografia, receberá o erro “**O Windows não pôde iniciar a sincronização do Microsoft Azure AD no computador local.</span><span class="sxs-lookup"><span data-stu-id="c1872-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="c1872-123">Para saber mais, examine o log de eventos do sistema.</span><span class="sxs-lookup"><span data-stu-id="c1872-123">For more information, review the System Event log.</span></span> <span data-ttu-id="c1872-124">Se for um serviço de terceiros, não Microsoft, entre em contato com o fornecedor do serviço e mencione o código de erro específico do serviço **-21451857952****”.</span><span class="sxs-lookup"><span data-stu-id="c1872-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="c1872-125">No Visualizador de Eventos do Windows, o log de eventos do aplicativo contém um erro com **ID de evento 6028** e a mensagem de erro *“**A chave de criptografia do servidor não pode ser acessada* *”.*</span><span class="sxs-lookup"><span data-stu-id="c1872-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="c1872-126">Para garantir que você não receba esses erros, siga os procedimentos em [Abandonando a chave de criptografia de sincronização do Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key) ao alterar a senha.</span><span class="sxs-lookup"><span data-stu-id="c1872-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="c1872-127">Abandono da chave de criptografia de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c1872-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="c1872-128">Os procedimentos a seguir aplicam-se somente ao Azure AD Connect compilação 1.1.443.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="c1872-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="c1872-129">Use os procedimentos a seguir para abandonar a chave de criptografia.</span><span class="sxs-lookup"><span data-stu-id="c1872-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="c1872-130">O que fazer se você precisar abandonar a chave de criptografia</span><span class="sxs-lookup"><span data-stu-id="c1872-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="c1872-131">Se você precisar abandonar a chave de criptografia, use os procedimentos a seguir para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c1872-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="c1872-132">Abandone a chave de criptografia existente</span><span class="sxs-lookup"><span data-stu-id="c1872-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="c1872-133">Forneça a senha da conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="c1872-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="c1872-134">Reinicialize a senha da conta de sincronização do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1872-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="c1872-135">Inicie o serviço de sincronização</span><span class="sxs-lookup"><span data-stu-id="c1872-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="c1872-136">Abandone a chave de criptografia existente</span><span class="sxs-lookup"><span data-stu-id="c1872-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="c1872-137">Abandone a chave de criptografia existente para que essa nova chave de criptografia possa ser criada:</span><span class="sxs-lookup"><span data-stu-id="c1872-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="c1872-138">Faça logon no seu servidor do Azure AD Connect como administrador.</span><span class="sxs-lookup"><span data-stu-id="c1872-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="c1872-139">Inicie uma nova sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1872-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="c1872-140">Navegue até a pasta: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="c1872-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="c1872-141">Execute o comando: `./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="c1872-141">Run the command: `./miiskmu.exe /a`</span></span>

![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="c1872-143">Forneça a senha da conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="c1872-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="c1872-144">Como as senhas existentes armazenadas no banco de dados não podem ser descriptografadas, você precisará fornecer ao serviço de sincronização a senha da conta do AD DS.</span><span class="sxs-lookup"><span data-stu-id="c1872-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="c1872-145">O serviço de sincronização criptografa as senhas usando a nova chave de criptografia:</span><span class="sxs-lookup"><span data-stu-id="c1872-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="c1872-146">Inicie o Synchronization Service Manager (INICIAR → Serviço de Sincronização).</span><span class="sxs-lookup"><span data-stu-id="c1872-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="c1872-147">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="c1872-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="c1872-148">Acesse a guia **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="c1872-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="c1872-149">Selecione o **AD Connector** que corresponde ao seu AD local.</span><span class="sxs-lookup"><span data-stu-id="c1872-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="c1872-150">Se você tiver mais de um AD Connector, repita as etapas a seguir para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="c1872-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="c1872-151">Em **Ações**, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="c1872-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="c1872-152">Na caixa de diálogo pop-up, selecione **Conectar-se à floresta do Active Directory**:</span><span class="sxs-lookup"><span data-stu-id="c1872-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="c1872-153">Insira a senha da conta do AD DS na caixa de texto **Senha**.</span><span class="sxs-lookup"><span data-stu-id="c1872-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="c1872-154">Se você não souber a senha, configure-a para um valor conhecido antes de executar essa etapa.</span><span class="sxs-lookup"><span data-stu-id="c1872-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="c1872-155">Clique em **OK** para salvar a nova senha e fechar a caixa de diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="c1872-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="c1872-156">![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="c1872-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="c1872-157">Reinicialize a senha da conta de sincronização do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1872-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="c1872-158">Você não pode fornecer diretamente a senha da conta de serviço do Azure AD para o serviço de sincronização.</span><span class="sxs-lookup"><span data-stu-id="c1872-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="c1872-159">Em vez disso, você precisa usar o cmdlet **Add-ADSyncAADServiceAccount** para reinicializar a conta de serviço do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1872-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="c1872-160">O cmdlet redefine a senha da conta e a torna disponível para o serviço de sincronização:</span><span class="sxs-lookup"><span data-stu-id="c1872-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="c1872-161">Inicie uma nova sessão do PowerShell no servidor do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c1872-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="c1872-162">Execute o cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="c1872-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="c1872-163">Na caixa de diálogo pop-up, forneça as credenciais de administrador global do Azure AD para seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1872-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="c1872-164">![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="c1872-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="c1872-165">Se isso for bem-sucedido, você verá o prompt de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1872-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="c1872-166">Inicie o serviço de sincronização</span><span class="sxs-lookup"><span data-stu-id="c1872-166">Start the Synchronization Service</span></span>
<span data-ttu-id="c1872-167">Agora que o serviço de sincronização tem acesso à chave de criptografia e todas as senhas necessárias, você poderá reiniciar o serviço no Gerenciador de Controle de Serviços do Windows:</span><span class="sxs-lookup"><span data-stu-id="c1872-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="c1872-168">Vá para o Gerenciador de Controle de Serviços do Windows (INICIAR → Serviços).</span><span class="sxs-lookup"><span data-stu-id="c1872-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="c1872-169">Selecione **Sincronização do Microsoft Azure AD** e clique em Reiniciar.</span><span class="sxs-lookup"><span data-stu-id="c1872-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1872-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1872-170">Next steps</span></span>
<span data-ttu-id="c1872-171">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="c1872-171">**Overview topics**</span></span>

* [<span data-ttu-id="c1872-172">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="c1872-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="c1872-173">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c1872-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
