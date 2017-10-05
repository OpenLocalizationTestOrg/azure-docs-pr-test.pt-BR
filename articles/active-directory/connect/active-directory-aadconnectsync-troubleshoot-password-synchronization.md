---
title: "Solução de problemas de sincronização de senha com a sincronização do Azure AD Connect | Microsoft Docs"
description: "Este artigo fornece informações de como solucionar problemas de sincronização de senha."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="4a872-103">Solução de problemas de sincronização de senha com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4a872-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="4a872-104">Este tópico fornece etapas para solucionar problemas com a sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="4a872-105">Se as senhas não estiverem sincronizando conforme o esperado, isso poderá ocorrer para um subconjunto de usuários ou para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="4a872-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="4a872-106">Para a implantação do Azure AD (Azure Active Directory) Connect com a versão 1.1.524.0 ou posterior, agora há um cmdlet de diagnóstico que você pode usar para solucionar problemas de sincronização de senha:</span><span class="sxs-lookup"><span data-stu-id="4a872-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="4a872-107">Se ocorrer um problema em que nenhuma senha seja sincronizada, consulte a seção [Nenhuma senha é sincronizada: solucionar problemas usando o cmdlet de diagnóstico](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="4a872-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="4a872-108">Se ocorrer um problema com objetos individuais, consulte a seção [Um objeto não está sincronizando senhas: solucionar problemas usando o cmdlet de diagnóstico](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="4a872-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="4a872-109">Para versões mais antigas de implantação do Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="4a872-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="4a872-110">Se ocorrer um problema em que nenhuma senha seja sincronizada, consulte a seção [Nenhuma senha é sincronizada: etapas manuais de solução de problemas](#no-passwords-are-synchronized-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="4a872-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="4a872-111">Se ocorrer um problema com objetos individuais, consulte a seção [Um objeto não está sincronizando senhas: etapas manuais de solução de problemas](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="4a872-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="4a872-112">Nenhuma senha é sincronizada: solucionar problemas usando o cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4a872-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="4a872-113">Você pode usar o cmdlet `Invoke-ADSyncDiagnostics` para descobrir por que nenhuma senha é sincronizada.</span><span class="sxs-lookup"><span data-stu-id="4a872-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="4a872-114">O cmdlet `Invoke-ADSyncDiagnostics` está disponível apenas para o Azure AD Connect versão 1.1.524.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4a872-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="4a872-115">Executar o cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4a872-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="4a872-116">Para solucionar problemas em que nenhuma senha é sincronizada:</span><span class="sxs-lookup"><span data-stu-id="4a872-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="4a872-117">Abra uma nova sessão do Windows PowerShell no servidor do Azure AD Connect com a opção **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="4a872-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="4a872-118">Execute `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="4a872-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="4a872-119">Execute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4a872-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="4a872-120">Execute `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="4a872-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="4a872-121">Entenda os resultados do cmdlet</span><span class="sxs-lookup"><span data-stu-id="4a872-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="4a872-122">O cmdlet de diagnóstico executa as seguintes verificações:</span><span class="sxs-lookup"><span data-stu-id="4a872-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="4a872-123">Valida se o recurso de sincronização de senha está habilitado para seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a872-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="4a872-124">Valida se o servidor do Azure AD Connect não está em modo de preparo.</span><span class="sxs-lookup"><span data-stu-id="4a872-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="4a872-125">Para cada conector local existente do Active Directory (que corresponde a uma floresta existente do Active Directory):</span><span class="sxs-lookup"><span data-stu-id="4a872-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="4a872-126">Valida se o recurso de sincronização de senha está habilitado.</span><span class="sxs-lookup"><span data-stu-id="4a872-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="4a872-127">Pesquisa eventos de pulsação de sincronização de senha nos logs de eventos de aplicativo do Windows.</span><span class="sxs-lookup"><span data-stu-id="4a872-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="4a872-128">Para cada domínio do Active Directory sob o Active Directory Connector local:</span><span class="sxs-lookup"><span data-stu-id="4a872-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="4a872-129">Valida se o domínio está acessível no servidor do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4a872-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="4a872-130">Valida se as contas do AD DS (Active Directory Domain Services) usadas pelo Active Directory Connector local tem o nome de usuário, a senha e as permissões corretos, necessários para a sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="4a872-131">O diagrama a seguir ilustra os resultados do cmdlet para uma topologia do Active Directory local de domínio único:</span><span class="sxs-lookup"><span data-stu-id="4a872-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Saída de diagnóstico da sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="4a872-133">O restante desta seção descreve resultados específicos que são retornados pelo cmdlet e os problemas correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4a872-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="4a872-134">O recurso de sincronização de senha não está habilitado</span><span class="sxs-lookup"><span data-stu-id="4a872-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="4a872-135">Se você não tiver habilitado a sincronização de senha usando o assistente do Azure AD Connect, o seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![A sincronização de senha não está habilitada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="4a872-137">O servidor do Azure AD Connect está em modo de preparo</span><span class="sxs-lookup"><span data-stu-id="4a872-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="4a872-138">Se o servidor do Azure AD Connect estiver em modo de preparo, a sincronização de senha será temporariamente desabilitada e o seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![O servidor do Azure AD Connect está em modo de preparo](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="4a872-140">Nenhum evento de pulsação de sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="4a872-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="4a872-141">Cada Active Directory Connector local tem seu próprio canal de sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="4a872-142">Quando o canal de sincronização de senha é estabelecido e não existem alterações de senha a serem sincronizadas, um evento de pulsação (EventId 654) é gerado uma vez a cada 30 minutos no log de eventos de aplicativos do Windows.</span><span class="sxs-lookup"><span data-stu-id="4a872-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="4a872-143">Para cada Active Directory Connector local, o cmdlet pesquisa eventos de pulsação correspondentes nas últimas três horas.</span><span class="sxs-lookup"><span data-stu-id="4a872-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="4a872-144">Se nenhum evento de pulsação for encontrado, o seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-144">If no heartbeat event is found, the following error is returned:</span></span>

![Nenhum evento de pulsação de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="4a872-146">A conta do AD DS não tem as permissões corretas</span><span class="sxs-lookup"><span data-stu-id="4a872-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="4a872-147">Se a conta do AD DS usada pelo Active Directory Connector local para sincronizar os hashes de senha não tiver as permissões apropriadas, o seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Credenciais incorretas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="4a872-149">Nome de usuário ou senha incorreta da conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="4a872-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="4a872-150">Se a conta do AD DS usada pelo Active Directory Connector local para sincronizar os hashes de senha tiver um nome de usuário ou uma senha incorreta, o seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Credenciais incorretas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="4a872-152">Um objeto não está sincronizando senhas: solucionar problemas usando o cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4a872-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="4a872-153">Você pode usar o cmdlet `Invoke-ADSyncDiagnostics` para determinar por que um objeto não está sincronizando senhas.</span><span class="sxs-lookup"><span data-stu-id="4a872-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="4a872-154">O cmdlet `Invoke-ADSyncDiagnostics` está disponível apenas para o Azure AD Connect versão 1.1.524.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4a872-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="4a872-155">Executar o cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4a872-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="4a872-156">Para solucionar problemas em que nenhuma senha é sincronizada:</span><span class="sxs-lookup"><span data-stu-id="4a872-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="4a872-157">Abra uma nova sessão do Windows PowerShell no servidor do Azure AD Connect com a opção **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="4a872-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="4a872-158">Execute `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="4a872-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="4a872-159">Execute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4a872-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="4a872-160">Execute o cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a872-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="4a872-161">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4a872-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="4a872-162">Entenda os resultados do cmdlet</span><span class="sxs-lookup"><span data-stu-id="4a872-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="4a872-163">O cmdlet de diagnóstico executa as seguintes verificações:</span><span class="sxs-lookup"><span data-stu-id="4a872-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="4a872-164">Examina o estado do objeto do Active Directory no espaço do Active Directory Connector, no metaverso e no espaço do conector do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a872-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="4a872-165">Valida se há regras de sincronização com a sincronização de senha habilitada e aplicada a objeto do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a872-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="4a872-166">Tenta recuperar e exibir os resultados da última tentativa de sincronizar a senha do objeto.</span><span class="sxs-lookup"><span data-stu-id="4a872-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="4a872-167">O diagrama a seguir ilustra os resultados do cmdlet, ao solucionar problemas de sincronização de senha para um único objeto:</span><span class="sxs-lookup"><span data-stu-id="4a872-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Saída de diagnóstico da sincronização de senha – objeto único](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="4a872-169">O restante desta seção descreve os resultados específicos retornados pelo cmdlet e os problemas correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4a872-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="4a872-170">O objeto do Active Directory não é exportado para o Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a872-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="4a872-171">Falha na sincronização de senha para essa conta do Active Directory local porque não há nenhum objeto correspondente no locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a872-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="4a872-172">O seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-172">The following error is returned:</span></span>

![Objeto do Azure AD está ausente](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="4a872-174">O usuário tem uma senha temporária</span><span class="sxs-lookup"><span data-stu-id="4a872-174">User has a temporary password</span></span>
<span data-ttu-id="4a872-175">Atualmente, o Azure AD Connect não dá suporte à sincronização de senhas temporárias com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a872-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="4a872-176">Uma senha será considerada temporária se o opção **Alterar a senha no próximo logon** estiver definida no usuário do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="4a872-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="4a872-177">O seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4a872-177">The following error is returned:</span></span>

![A senha temporária não é exportada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="4a872-179">Os resultados da última tentativa de sincronizar a senha não estão disponíveis</span><span class="sxs-lookup"><span data-stu-id="4a872-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="4a872-180">Por padrão, o Azure AD Connect armazena os resultados das tentativas de sincronização de senha por sete dias.</span><span class="sxs-lookup"><span data-stu-id="4a872-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="4a872-181">Se não houver nenhum resultado disponível para o objeto selecionado do Active Directory, será retornado o seguinte aviso:</span><span class="sxs-lookup"><span data-stu-id="4a872-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Saída de diagnóstico de um único objeto – nenhum histórico de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="4a872-183">Nenhuma senha é sincronizada: etapas manuais de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="4a872-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="4a872-184">Siga estas etapas para determinar por que nenhuma senha é sincronizada:</span><span class="sxs-lookup"><span data-stu-id="4a872-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="4a872-185">O servidor do Connect está no [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="4a872-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="4a872-186">Um servidor no modo de preparo não sincroniza nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="4a872-187">Execute o script na seção [Obter o status das configurações de sincronização de senha](#get-the-status-of-password-sync-settings).</span><span class="sxs-lookup"><span data-stu-id="4a872-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="4a872-188">Ele fornece uma visão geral da configuração da sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-188">It gives you an overview of the password sync configuration.</span></span>  

    ![Saída de script do PowerShell das configurações de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="4a872-190">Se o recurso não estiver habilitado no Azure AD ou se o status do canal de sincronização não estiver habilitado, execute o assistente de instalação do Connect.</span><span class="sxs-lookup"><span data-stu-id="4a872-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="4a872-191">Selecione **Personalizar opções de sincronização**e desmarque a sincronização de senha. Essa mudança desabilita o recurso temporariamente.</span><span class="sxs-lookup"><span data-stu-id="4a872-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="4a872-192">Em seguida, execute o assistente novamente e reabilite a sincronização de senha. Execute o script novamente para verificar se a configuração está correta.</span><span class="sxs-lookup"><span data-stu-id="4a872-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="4a872-193">Procure se há erros no log de eventos.</span><span class="sxs-lookup"><span data-stu-id="4a872-193">Look in the event log for errors.</span></span> <span data-ttu-id="4a872-194">Procure os seguintes eventos, que poderão indicar um problema:</span><span class="sxs-lookup"><span data-stu-id="4a872-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="4a872-195">Fonte: “Sincronização de diretório” ID: 0, 611, 652, 655 Se um desses eventos aparecer, há um problema de conectividade.</span><span class="sxs-lookup"><span data-stu-id="4a872-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="4a872-196">A mensagem do log de eventos contém informações da floresta em que há um problema.</span><span class="sxs-lookup"><span data-stu-id="4a872-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="4a872-197">Para obter mais informações, consulte [Problema de conectividade](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="4a872-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="4a872-198">Se não aparecer nenhuma pulsação ou se nada mais funcionou, execute [Disparar uma sincronização completa de todas as senhas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="4a872-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="4a872-199">Execute o script apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="4a872-199">Run the script only once.</span></span>

6. <span data-ttu-id="4a872-200">Consulte a seção [Solucionar problemas de um objeto que não está sincronizando senhas](#one-object-is-not-synchronizing-passwords).</span><span class="sxs-lookup"><span data-stu-id="4a872-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="4a872-201">Problemas de conectividade</span><span class="sxs-lookup"><span data-stu-id="4a872-201">Connectivity problems</span></span>

<span data-ttu-id="4a872-202">Você tem conectividade com o Azure AD?</span><span class="sxs-lookup"><span data-stu-id="4a872-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="4a872-203">A conta tem as permissões necessárias para ler os hashes de senha em todos os domínios?</span><span class="sxs-lookup"><span data-stu-id="4a872-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="4a872-204">Se você instalou o Connect usando as configurações Expresso, as permissões já estarão corretas.</span><span class="sxs-lookup"><span data-stu-id="4a872-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="4a872-205">Se você usou a instalação personalizada, defina as permissões manualmente, fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4a872-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="4a872-206">Para localizar a conta usada pelo Active Directory Connector, inicie o **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="4a872-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="4a872-207">Acesse **Conectores** e, em seguida, pesquise a floresta do Active Directory local cujo problema você está solucionando.</span><span class="sxs-lookup"><span data-stu-id="4a872-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="4a872-208">Selecione o conector e, em seguida, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="4a872-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="4a872-209">Vá para **Conectar-se à floresta do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a872-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Conta usada pelo Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="4a872-211">Anote o nome de usuário e o domínio em que a conta está localizada.</span><span class="sxs-lookup"><span data-stu-id="4a872-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="4a872-212">Inicie os **Usuários e Computadores do Active Directory** e, em seguida, verifique se a conta que você encontrou anteriormente tem as seguintes permissões definidas na raiz de todos os domínios na floresta:</span><span class="sxs-lookup"><span data-stu-id="4a872-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="4a872-213">Replicar alterações de diretório</span><span class="sxs-lookup"><span data-stu-id="4a872-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="4a872-214">Replicar todas as alterações de diretório</span><span class="sxs-lookup"><span data-stu-id="4a872-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="4a872-215">Os controladores de domínio estão acessíveis pelo Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="4a872-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="4a872-216">Se o servidor do Connect não puder se conectar a todos os controladores de domínio, configure **Usar somente o controlador de domínio preferencial**.</span><span class="sxs-lookup"><span data-stu-id="4a872-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Controlador de domínio usado pelo Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="4a872-218">Volte para **Synchronization Service Manager** e **Configurar Partição de Diretório**.</span><span class="sxs-lookup"><span data-stu-id="4a872-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="4a872-219">Selecione o domínio em **Selecionar partições de diretório**, selecione a caixa de seleção **Usar somente controladores de domínio preferenciais** e, em seguida, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="4a872-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="4a872-220">Na lista, insira os controladores de domínio que o Connect deve usar para sincronização de senha. A mesma lista também é usada para importação e exportação.</span><span class="sxs-lookup"><span data-stu-id="4a872-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="4a872-221">Siga estas etapas para todos os domínios.</span><span class="sxs-lookup"><span data-stu-id="4a872-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="4a872-222">Se o script mostrar que não há nenhuma pulsação, execute o script [Disparar uma sincronização completa de todas as senhas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="4a872-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="4a872-223">Um objeto não está sincronizando senhas: etapas manuais de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="4a872-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="4a872-224">Você pode solucionar problemas de sincronização de senha problemas facilmente analisando o status de um objeto.</span><span class="sxs-lookup"><span data-stu-id="4a872-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="4a872-225">Em **Usuários e computadores do Active Directory**, pesquise o usuário e, em seguida, verifique se a caixa de seleção **O usuário deve alterar a senha no próximo logon** está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="4a872-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Senhas produtivas do Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="4a872-227">Se a caixa de seleção estiver marcada, solicite que o usuário entre e altere a senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="4a872-228">As senhas temporárias não são sincronizadas com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a872-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="4a872-229">Se a senha estiver correta no Active Directory, siga o usuário no mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="4a872-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="4a872-230">Seguindo o usuário do Active Directory local ao Azure AD, você pode ver se há algum erro descritivo no objeto.</span><span class="sxs-lookup"><span data-stu-id="4a872-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="4a872-231">a.</span><span class="sxs-lookup"><span data-stu-id="4a872-231">a.</span></span> <span data-ttu-id="4a872-232">Inicie o [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="4a872-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="4a872-233">b.</span><span class="sxs-lookup"><span data-stu-id="4a872-233">b.</span></span> <span data-ttu-id="4a872-234">Clique em **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="4a872-234">Click **Connectors**.</span></span>

    <span data-ttu-id="4a872-235">c.</span><span class="sxs-lookup"><span data-stu-id="4a872-235">c.</span></span> <span data-ttu-id="4a872-236">Selecione o **Active Directory Connector** no qual o usuário está localizado.</span><span class="sxs-lookup"><span data-stu-id="4a872-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="4a872-237">d.</span><span class="sxs-lookup"><span data-stu-id="4a872-237">d.</span></span> <span data-ttu-id="4a872-238">Selecione **Pesquisar Espaço do Conector**.</span><span class="sxs-lookup"><span data-stu-id="4a872-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="4a872-239">e.</span><span class="sxs-lookup"><span data-stu-id="4a872-239">e.</span></span> <span data-ttu-id="4a872-240">No **Escopo** selecione **DN ou Âncora** e, em seguida, insira o DN completo do usuário cujo problema você está solucionando.</span><span class="sxs-lookup"><span data-stu-id="4a872-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Pesquisar por usuário no espaço do conector com DN](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="4a872-242">f.</span><span class="sxs-lookup"><span data-stu-id="4a872-242">f.</span></span> <span data-ttu-id="4a872-243">Localize o usuário que você está procurando e, em seguida, clique em **Propriedades** para ver todos os atributos.</span><span class="sxs-lookup"><span data-stu-id="4a872-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="4a872-244">Se o usuário não estiver no resultado da pesquisa, verifique as [regras de filtragem](active-directory-aadconnectsync-configure-filtering.md) e lembre-se de executar [Aplicar e verificar alterações](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) para que o usuário seja exibido no Connect.</span><span class="sxs-lookup"><span data-stu-id="4a872-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="4a872-245">g.</span><span class="sxs-lookup"><span data-stu-id="4a872-245">g.</span></span> <span data-ttu-id="4a872-246">Para ver os detalhes de sincronização de senha do objeto da semana passada, clique em **Log**.</span><span class="sxs-lookup"><span data-stu-id="4a872-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Detalhes do log do objeto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="4a872-248">Se o log do objeto está vazio, o Azure AD Connect não conseguiu ler o hash de senha do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a872-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="4a872-249">Continue a solução de problemas com [Erros de conectividade](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="4a872-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="4a872-250">Se aparecer qualquer outro valor que não seja **êxito**, consulte a tabela no [Log de sincronização de senha](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="4a872-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="4a872-251">h.</span><span class="sxs-lookup"><span data-stu-id="4a872-251">h.</span></span> <span data-ttu-id="4a872-252">Selecione a guia **linhagem** e verifique se pelo menos uma regra de sincronização na coluna **PasswordSync** é **True**.</span><span class="sxs-lookup"><span data-stu-id="4a872-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="4a872-253">Na configuração padrão, o nome da regra de sincronização é **Entrada do AD – AccountEnabled do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4a872-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informações de linhagem de um usuário](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="4a872-255">i.</span><span class="sxs-lookup"><span data-stu-id="4a872-255">i.</span></span> <span data-ttu-id="4a872-256">Clique em **Propriedades de objeto do metaverso** para exibir uma lista de atributos do usuário.</span><span class="sxs-lookup"><span data-stu-id="4a872-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Informações de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="4a872-258">Verifique se não há nenhum atributo **cloudFiltered** presente.</span><span class="sxs-lookup"><span data-stu-id="4a872-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="4a872-259">Verifique se os atributos de domínio (domainFQDN e domainNetBios) têm os valores esperados.</span><span class="sxs-lookup"><span data-stu-id="4a872-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="4a872-260">j.</span><span class="sxs-lookup"><span data-stu-id="4a872-260">j.</span></span> <span data-ttu-id="4a872-261">Clique na guia **Conectores**. Verifique se os conectores do Active Directory local e do Azure AD são exibidos.</span><span class="sxs-lookup"><span data-stu-id="4a872-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Informações de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="4a872-263">k.</span><span class="sxs-lookup"><span data-stu-id="4a872-263">k.</span></span> <span data-ttu-id="4a872-264">Selecione a linha que representa o Azure AD, clique em **Propriedades** e, em seguida, clique na guia **Linhagem**. O objeto de espaço do conector deve ter uma regra de saída na coluna **PasswordSync** definida como **True**.</span><span class="sxs-lookup"><span data-stu-id="4a872-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="4a872-265">Na configuração padrão, o nome da regra de sincronização é **Saída para AAD – Ingresso do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4a872-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Caixa de diálogo Propriedades do objeto de espaço do conector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="4a872-267">Log de sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="4a872-267">Password sync log</span></span>
<span data-ttu-id="4a872-268">A coluna de status pode ter os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="4a872-268">The status column can have the following values:</span></span>

| <span data-ttu-id="4a872-269">Status</span><span class="sxs-lookup"><span data-stu-id="4a872-269">Status</span></span> | <span data-ttu-id="4a872-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="4a872-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a872-271">Sucesso</span><span class="sxs-lookup"><span data-stu-id="4a872-271">Success</span></span> |<span data-ttu-id="4a872-272">A senha foi sincronizada com êxito.</span><span class="sxs-lookup"><span data-stu-id="4a872-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="4a872-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="4a872-273">FilteredByTarget</span></span> |<span data-ttu-id="4a872-274">A senha está definida para **O usuário deve alterar a senha no próximo logon**.</span><span class="sxs-lookup"><span data-stu-id="4a872-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="4a872-275">A senha não foi sincronizada.</span><span class="sxs-lookup"><span data-stu-id="4a872-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="4a872-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="4a872-276">NoTargetConnection</span></span> |<span data-ttu-id="4a872-277">Nenhum objeto no metaverso ou no espaço conector do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a872-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="4a872-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="4a872-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="4a872-279">Nenhum objeto encontrado no espaço conector do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="4a872-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="4a872-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="4a872-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="4a872-281">O objeto no espaço conector do AD do Azure ainda não foi exportado.</span><span class="sxs-lookup"><span data-stu-id="4a872-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="4a872-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="4a872-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="4a872-283">A entrada de log foi criada antes da versão 1.0.9125.0 e é mostrada em seu estado herdado.</span><span class="sxs-lookup"><span data-stu-id="4a872-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="4a872-284">Erro</span><span class="sxs-lookup"><span data-stu-id="4a872-284">Error</span></span> |<span data-ttu-id="4a872-285">O serviço retornou um erro desconhecido.</span><span class="sxs-lookup"><span data-stu-id="4a872-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="4a872-286">Desconhecido</span><span class="sxs-lookup"><span data-stu-id="4a872-286">Unknown</span></span> |<span data-ttu-id="4a872-287">Ocorreu um erro ao tentar processar um lote de hashes de senha.</span><span class="sxs-lookup"><span data-stu-id="4a872-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="4a872-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="4a872-288">MissingAttribute</span></span> |<span data-ttu-id="4a872-289">Atributos específicos (por exemplo, o hash de Kerberos) exigidos pelos Azure AD Domain Services não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4a872-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="4a872-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="4a872-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="4a872-291">Atributos específicos (por exemplo, o hash de Kerberos) exigidos pelos Azure AD Domain Services não estavam disponíveis anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4a872-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="4a872-292">É feita uma tentativa de sincronizar novamente o hash de senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="4a872-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="4a872-293">Scripts para ajudar na solução de problemas</span><span class="sxs-lookup"><span data-stu-id="4a872-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="4a872-294">Obter o status das configurações da sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="4a872-294">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="4a872-295">Disparar uma sincronização completa de todas as senhas</span><span class="sxs-lookup"><span data-stu-id="4a872-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="4a872-296">Execute este script apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="4a872-296">Run this script only once.</span></span> <span data-ttu-id="4a872-297">Se for necessário executá-lo mais de uma vez, haverá algum outro problema.</span><span class="sxs-lookup"><span data-stu-id="4a872-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="4a872-298">Para solucionar o problema, contate o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4a872-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="4a872-299">Você pode disparar uma sincronização completa de todas as senhas usando o script a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a872-299">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="4a872-300">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a872-300">Next steps</span></span>
* [<span data-ttu-id="4a872-301">Implementação de sincronização de senha com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4a872-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="4a872-302">Sincronização do Azure AD Connect: personalizando as opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="4a872-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4a872-303">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4a872-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
