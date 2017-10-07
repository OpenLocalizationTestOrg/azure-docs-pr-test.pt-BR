---
title: "Sincronização do Azure AD Connect: Alterar conta de serviço de sincronização se conectar de saudação do AD do Azure | Microsoft Docs"
description: "Este documento de tópico descreve chave de criptografia hello e como tooabandon após a senha de saudação é alterado."
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
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="e16ae-104">Alteração da senha de conta de serviço de sincronização do hello Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="e16ae-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="e16ae-105">Se você alterar a senha da conta de serviço para o Azure AD Connect sincronização de hello, Olá serviço de sincronização não será capaz de iniciar corretamente até ter abandonado a chave de criptografia de saudação e reiniciadas a senha da conta de serviço para o Azure AD Connect sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e16ae-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="e16ae-106">Como parte da saudação serviços de sincronização do Azure AD Connect, usa uma criptografia toostore chave Olá senhas hello AD DS e contas de serviço do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e16ae-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="e16ae-107">Essas contas são criptografadas antes de serem armazenadas no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e16ae-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="e16ae-108">Olá chave de criptografia usada é protegida usando [proteção de dados do Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="e16ae-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="e16ae-109">DPAPI protege a chave de criptografia de saudação usando Olá **senha da conta de serviço de sincronização do hello AD do Azure Connect**.</span><span class="sxs-lookup"><span data-stu-id="e16ae-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="e16ae-110">Se você precisar de senha da conta de serviço toochange hello, você pode usar procedimentos Olá [chave de criptografia de sincronização se conectar de saudação do AD do Azure Abandoning](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish isso.</span><span class="sxs-lookup"><span data-stu-id="e16ae-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="e16ae-111">Esses procedimentos também devem ser usados se você precisar de chave de criptografia de saudação tooabandon por qualquer motivo.</span><span class="sxs-lookup"><span data-stu-id="e16ae-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="e16ae-112">Problemas que surgem da alteração da senha Olá</span><span class="sxs-lookup"><span data-stu-id="e16ae-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="e16ae-113">Há duas coisas que precisam toobe feita quando você alterar a senha da conta de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="e16ae-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="e16ae-114">Primeiro, é necessário toochange senha de saudação em Olá Gerenciador de controle de serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="e16ae-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="e16ae-115">Até que esse problema seja resolvido, você verá os seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="e16ae-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="e16ae-116">Se você tentar toostart Olá serviço de sincronização no Gerenciador de controle de serviço do Windows, você recebe o erro de hello "**Windows não pôde iniciar o serviço de sincronização do AD do Microsoft Azure Olá no computador Local**".</span><span class="sxs-lookup"><span data-stu-id="e16ae-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="e16ae-117">**Erro 1069: o serviço de saudação não foi iniciado devido a falha de logon tooa.** "</span><span class="sxs-lookup"><span data-stu-id="e16ae-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="e16ae-118">Em Visualizador de eventos do Windows, o log de eventos do sistema Olá contém um erro com **7038 de ID de evento** e a mensagem "**Olá serviço ADSync foi toolog não é possível em como com senha Olá configurado no momento devido toohello seguinte erro: Olá nome de usuário ou senha está incorreta.** "</span><span class="sxs-lookup"><span data-stu-id="e16ae-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="e16ae-119">Em segundo lugar, sob condições específicas, se Olá senha for atualizada, Olá serviço de sincronização não mais recuperar chave de criptografia Olá via DPAPI.</span><span class="sxs-lookup"><span data-stu-id="e16ae-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="e16ae-120">Sem a chave de criptografia Olá Olá de que serviço de sincronização não é possível descriptografar Olá senhas necessárias toosynchronize local AD e o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e16ae-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="e16ae-121">Você verá erros, como:</span><span class="sxs-lookup"><span data-stu-id="e16ae-121">You will see errors such as:</span></span>

- <span data-ttu-id="e16ae-122">No Gerenciador de controle de serviços do Windows, se você tentar toostart Olá serviço de sincronização e ele não pode recuperar a chave de criptografia de saudação falhar com o erro "* * Windows não pôde iniciar Olá Microsoft Azure AD Sync no computador Local.</span><span class="sxs-lookup"><span data-stu-id="e16ae-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="e16ae-123">Para obter mais informações, examine o log de eventos do sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="e16ae-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="e16ae-124">Se este é um serviço de terceiros, entre em contato com o fornecedor do serviço de saudação e consulte o código de erro específico tooservice * *-21451857952 *. "</span><span class="sxs-lookup"><span data-stu-id="e16ae-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="e16ae-125">No Visualizador de eventos do Windows, o log de eventos do aplicativo hello contém um erro com **6028 de ID de evento** e mensagem de erro *"**não é possível acessar a chave de criptografia do servidor de saudação.* *"*</span><span class="sxs-lookup"><span data-stu-id="e16ae-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="e16ae-126">tooensure que você não recebe esses erros, siga os procedimentos de saudação em [chave de criptografia de sincronização se conectar de saudação do AD do Azure Abandoning](#abandoning-the-azure-ad-connect-sync-encryption-key) ao alterar a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="e16ae-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="e16ae-127">Chave de criptografia do Azure AD Sync conectar Olá abandoná-la</span><span class="sxs-lookup"><span data-stu-id="e16ae-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="e16ae-128">Olá procedimentos a seguir se aplicam somente tooAzure AD Connect compilação 1.1.443.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="e16ae-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="e16ae-129">Use Olá chave de criptografia de saudação de tooabandon procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e16ae-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="e16ae-130">Quais toodo se precisar de chave de criptografia de saudação tooabandon</span><span class="sxs-lookup"><span data-stu-id="e16ae-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="e16ae-131">Se você precisar de chave de criptografia tooabandon hello, use Olá tooaccomplish procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e16ae-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="e16ae-132">Abandone a chave de criptografia existente Olá</span><span class="sxs-lookup"><span data-stu-id="e16ae-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="e16ae-133">Fornecer a senha Olá Olá conta AD DS</span><span class="sxs-lookup"><span data-stu-id="e16ae-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="e16ae-134">Reinicializar senha Olá Olá conta de sincronização do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e16ae-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="e16ae-135">Saudação de iniciar o serviço de sincronização</span><span class="sxs-lookup"><span data-stu-id="e16ae-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="e16ae-136">Abandone a chave de criptografia existente Olá</span><span class="sxs-lookup"><span data-stu-id="e16ae-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="e16ae-137">Abandone a chave de criptografia existente Olá para que essa nova chave de criptografia pode ser criado:</span><span class="sxs-lookup"><span data-stu-id="e16ae-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="e16ae-138">Faça logon no tooyour servidor se conectar do AD do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="e16ae-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="e16ae-139">Inicie uma nova sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e16ae-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="e16ae-140">Navegue até toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="e16ae-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="e16ae-141">Execute o comando hello:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="e16ae-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="e16ae-143">Fornecer a senha Olá Olá conta AD DS</span><span class="sxs-lookup"><span data-stu-id="e16ae-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="e16ae-144">Como as senhas existentes Olá armazenadas dentro do banco de dados de saudação não podem ser descriptografadas, você precisa tooprovide Olá serviço de sincronização com senha Olá conta Olá AD DS.</span><span class="sxs-lookup"><span data-stu-id="e16ae-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="e16ae-145">Olá serviço de sincronização criptografa senhas hello usando a nova chave de criptografia hello:</span><span class="sxs-lookup"><span data-stu-id="e16ae-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="e16ae-146">Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).</span><span class="sxs-lookup"><span data-stu-id="e16ae-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="e16ae-147">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="e16ae-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="e16ae-148">Vá toohello **conectores** guia.</span><span class="sxs-lookup"><span data-stu-id="e16ae-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="e16ae-149">Selecione Olá **conector AD** que corresponde a tooyour AD local.</span><span class="sxs-lookup"><span data-stu-id="e16ae-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="e16ae-150">Se você tiver mais de um conector do AD, repita Olá seguindo as etapas para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="e16ae-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="e16ae-151">Em **Ações**, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e16ae-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="e16ae-152">Na caixa de diálogo pop-up hello, selecione **conectar-se a floresta do diretório tooActive**:</span><span class="sxs-lookup"><span data-stu-id="e16ae-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="e16ae-153">Digite a senha de saudação da conta do AD DS de saudação em hello **senha** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e16ae-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="e16ae-154">Se você não souber a senha, você deve definir tooa conhecido valor antes de executar essa etapa.</span><span class="sxs-lookup"><span data-stu-id="e16ae-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="e16ae-155">Clique em **Okey** toosave Olá nova senha e a caixa de diálogo pop-up Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="e16ae-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="e16ae-156">![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="e16ae-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="e16ae-157">Reinicializar senha Olá Olá conta de sincronização do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e16ae-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="e16ae-158">Diretamente, você não pode fornecer senha Olá Olá AD do Azure serviço conta toohello serviço de sincronização.</span><span class="sxs-lookup"><span data-stu-id="e16ae-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="e16ae-159">Em vez disso, você precisa toouse Olá cmdlet **ADSyncAADServiceAccount adicionar** tooreinitialize Olá conta de serviço do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e16ae-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="e16ae-160">Olá cmdlet redefine a senha da conta hello e facilita o serviço de sincronização de toohello disponível:</span><span class="sxs-lookup"><span data-stu-id="e16ae-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="e16ae-161">Inicie uma nova sessão do PowerShell no servidor do Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="e16ae-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="e16ae-162">Execute o cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="e16ae-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="e16ae-163">Na caixa de diálogo pop-up hello, forneça credenciais de Administrador Global de saudação do AD do Azure para seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e16ae-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="e16ae-164">![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="e16ae-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="e16ae-165">Se for bem-sucedida, você verá o prompt de comando do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e16ae-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="e16ae-166">Saudação de iniciar o serviço de sincronização</span><span class="sxs-lookup"><span data-stu-id="e16ae-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="e16ae-167">Agora que Olá serviço de sincronização tem a chave de criptografia de toohello de acesso e todas as senhas de Olá precisa, você pode reiniciar o serviço de saudação em Olá Gerenciador de controle de serviços do Windows:</span><span class="sxs-lookup"><span data-stu-id="e16ae-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="e16ae-168">Vá tooWindows Gerenciador de controle de serviço (serviços de início →).</span><span class="sxs-lookup"><span data-stu-id="e16ae-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="e16ae-169">Selecione **Sincronização do Microsoft Azure AD** e clique em Reiniciar.</span><span class="sxs-lookup"><span data-stu-id="e16ae-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e16ae-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e16ae-170">Next steps</span></span>
<span data-ttu-id="e16ae-171">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="e16ae-171">**Overview topics**</span></span>

* [<span data-ttu-id="e16ae-172">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="e16ae-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="e16ae-173">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e16ae-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
