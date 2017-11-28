---
title: "a sincronização de senha aaaTroubleshoot com a sincronização do Azure AD Connect | Microsoft Docs"
description: "Este artigo fornece informações sobre como tootroubleshoot problemas de sincronização de senha."
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="4bde7-103">Solução de problemas de sincronização de senha com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4bde7-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="4bde7-104">Este tópico fornece etapas para como tootroubleshoot problemas de sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4bde7-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="4bde7-105">Se as senhas não estiverem sincronizando conforme o esperado, isso poderá ocorrer para um subconjunto de usuários ou para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="4bde7-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="4bde7-106">Para o Azure Active Directory (AD do Azure) conecte-se a implantação com a versão 1.1.524.0 ou posterior, agora há um cmdlet de diagnóstico que você pode usar tootroubleshoot problemas de sincronização de senha:</span><span class="sxs-lookup"><span data-stu-id="4bde7-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="4bde7-107">Se você tiver um problema em que nenhum senhas são sincronizadas, consulte toohello [nenhum senhas são sincronizadas: solucionar problemas usando o cmdlet de diagnóstico Olá](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) seção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="4bde7-108">Se você tiver um problema com os objetos individuais, consulte toohello [um objeto não está sincronizando senhas: solucionar problemas usando o cmdlet de diagnóstico Olá](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) seção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="4bde7-109">Para versões mais antigas de implantação do Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="4bde7-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="4bde7-110">Se você tiver um problema em que nenhum senhas são sincronizadas, consulte toohello [nenhum senhas são sincronizadas: manual, as etapas de solução de problemas](#no-passwords-are-synchronized-manual-troubleshooting-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="4bde7-111">Se você tiver um problema com os objetos individuais, consulte toohello [um objeto não está sincronizando senhas: manual, as etapas de solução de problemas](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="4bde7-112">Sem as senhas são sincronizadas: solucionar problemas usando o cmdlet de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="4bde7-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="4bde7-113">Você pode usar o hello `Invoke-ADSyncDiagnostics` toofigure cmdlet out por que não há senhas são sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="4bde7-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="4bde7-114">Olá `Invoke-ADSyncDiagnostics` cmdlet está disponível apenas para o Azure AD Connect versão 1.1.524.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4bde7-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="4bde7-115">Execute o cmdlet de diagnóstico de saudação</span><span class="sxs-lookup"><span data-stu-id="4bde7-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="4bde7-116">problemas de tootroubleshoot onde nenhum senhas são sincronizadas:</span><span class="sxs-lookup"><span data-stu-id="4bde7-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="4bde7-117">Abra uma nova sessão do Windows PowerShell no seu servidor do Azure AD Connect com hello **executar como administrador** opção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="4bde7-118">Execute `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="4bde7-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="4bde7-119">Execute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4bde7-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="4bde7-120">Execute `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="4bde7-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="4bde7-121">Entender os resultados de saudação do cmdlet Olá</span><span class="sxs-lookup"><span data-stu-id="4bde7-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="4bde7-122">Olá diagnóstico executa Olá verificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bde7-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="4bde7-123">Valida que Olá recurso de sincronização de senha está habilitado para seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bde7-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="4bde7-124">Valida que saudação do servidor não está em modo de preparo do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4bde7-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="4bde7-125">Para cada local existente conector do Active Directory (que corresponde a floresta do Active Directory existente de tooan):</span><span class="sxs-lookup"><span data-stu-id="4bde7-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="4bde7-126">Valida que Olá recurso de sincronização de senha está habilitado.</span><span class="sxs-lookup"><span data-stu-id="4bde7-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="4bde7-127">Logs de eventos de aplicativo do Windows procura eventos de pulsação de sincronização de senha em hello.</span><span class="sxs-lookup"><span data-stu-id="4bde7-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="4bde7-128">Para cada domínio do Active Directory em um conector para Active Directory local hello:</span><span class="sxs-lookup"><span data-stu-id="4bde7-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="4bde7-129">Valida que Olá domínio é acessível a partir do servidor de conectar-se de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bde7-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="4bde7-130">Valida que contas de serviços de domínio Active Directory (AD DS) Olá usadas pelo conector para Active Directory local Olá tem correto Olá de nome de usuário, senha e as permissões necessárias para a sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4bde7-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="4bde7-131">Olá diagrama a seguir ilustra os resultados de saudação do cmdlet Olá para uma topologia do Active Directory local único domínio:</span><span class="sxs-lookup"><span data-stu-id="4bde7-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Saída de diagnóstico da sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="4bde7-133">Olá restante desta seção descreve resultados específicos que são retornados pelo cmdlet hello e problemas correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4bde7-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="4bde7-134">O recurso de sincronização de senha não está habilitado</span><span class="sxs-lookup"><span data-stu-id="4bde7-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="4bde7-135">Se você não tiver habilitado a sincronização de senha usando o Assistente do hello Azure AD Connect, Olá erro a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="4bde7-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![A sincronização de senha não está habilitada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="4bde7-137">O servidor do Azure AD Connect está em modo de preparo</span><span class="sxs-lookup"><span data-stu-id="4bde7-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="4bde7-138">Se o servidor do Azure AD Connect hello está em modo de preparo, a sincronização de senha está temporariamente desabilitada e hello seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4bde7-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![O servidor do Azure AD Connect está em modo de preparo](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="4bde7-140">Nenhum evento de pulsação de sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="4bde7-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="4bde7-141">Cada Active Directory Connector local tem seu próprio canal de sincronização de senha.</span><span class="sxs-lookup"><span data-stu-id="4bde7-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="4bde7-142">Quando Olá canal de sincronização de senha é estabelecido e não existem quaisquer toobe de alterações de senha sincronizada, um evento de pulsação (EventId 654) é gerado uma vez a cada 30 minutos em Olá Log de eventos de aplicativo do Windows.</span><span class="sxs-lookup"><span data-stu-id="4bde7-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="4bde7-143">Para cada conector do Active Directory local, Olá cmdlet procura por eventos de pulsação correspondentes no hello últimos três horas.</span><span class="sxs-lookup"><span data-stu-id="4bde7-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="4bde7-144">Se nenhum evento de pulsação é encontrado, hello seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4bde7-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Nenhum evento de pulsação de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="4bde7-146">A conta do AD DS não tem as permissões corretas</span><span class="sxs-lookup"><span data-stu-id="4bde7-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="4bde7-147">Se a conta de saudação AD DS que é usada pelo Olá local hashes de senha do Active Directory connector toosynchronize não tem as permissões apropriadas Olá, hello seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4bde7-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Credenciais incorretas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="4bde7-149">Nome de usuário ou senha incorreta da conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="4bde7-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="4bde7-150">Se o hello AD DS conta usada pelo hello hashes de senha local do Active Directory connector toosynchronize tem um nome de usuário incorreto ou a senha, hello seguinte erro será retornado:</span><span class="sxs-lookup"><span data-stu-id="4bde7-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Credenciais incorretas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="4bde7-152">Um objeto não está sincronizando senhas: solucionar problemas usando o cmdlet de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="4bde7-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="4bde7-153">Você pode usar o hello `Invoke-ADSyncDiagnostics` toodetermine cmdlet por que um objeto não está sincronizando senhas.</span><span class="sxs-lookup"><span data-stu-id="4bde7-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="4bde7-154">Olá `Invoke-ADSyncDiagnostics` cmdlet está disponível apenas para o Azure AD Connect versão 1.1.524.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4bde7-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="4bde7-155">Execute o cmdlet de diagnóstico de saudação</span><span class="sxs-lookup"><span data-stu-id="4bde7-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="4bde7-156">problemas de tootroubleshoot onde nenhum senhas são sincronizadas:</span><span class="sxs-lookup"><span data-stu-id="4bde7-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="4bde7-157">Abra uma nova sessão do Windows PowerShell no seu servidor do Azure AD Connect com hello **executar como administrador** opção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="4bde7-158">Execute `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="4bde7-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="4bde7-159">Execute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4bde7-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="4bde7-160">Execute Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bde7-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="4bde7-161">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4bde7-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="4bde7-162">Entender os resultados de saudação do cmdlet Olá</span><span class="sxs-lookup"><span data-stu-id="4bde7-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="4bde7-163">Olá diagnóstico executa Olá verificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bde7-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="4bde7-164">Examina o estado de saudação do objeto do Active Directory Olá no espaço do conector do Active Directory hello, o metaverso e o Azure espaço do conector AD.</span><span class="sxs-lookup"><span data-stu-id="4bde7-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="4bde7-165">Valida que não existem regras de sincronização com a sincronização de senha habilitada e aplicada de objeto do Active Directory toohello.</span><span class="sxs-lookup"><span data-stu-id="4bde7-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="4bde7-166">Tentativas de tooretrieve e exibir resultados de Olá Olá última tentativa toosynchronize Olá password para objeto hello.</span><span class="sxs-lookup"><span data-stu-id="4bde7-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="4bde7-167">Olá diagrama a seguir ilustra os resultados de Olá Olá cmdlet, ao solucionar problemas de sincronização de senha para um único objeto:</span><span class="sxs-lookup"><span data-stu-id="4bde7-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Saída de diagnóstico da sincronização de senha – objeto único](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="4bde7-169">Olá restante desta seção descreve resultados específicos retornados pelo cmdlet hello e problemas correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4bde7-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="4bde7-170">saudação do Active Directory não está tooAzure exportado AD</span><span class="sxs-lookup"><span data-stu-id="4bde7-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="4bde7-171">Sincronização de senha para essa conta do Active Directory local falhará porque não há nenhum objeto correspondente no locatário do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4bde7-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="4bde7-172">saudação de erro a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="4bde7-172">hello following error is returned:</span></span>

![Objeto do Azure AD está ausente](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="4bde7-174">O usuário tem uma senha temporária</span><span class="sxs-lookup"><span data-stu-id="4bde7-174">User has a temporary password</span></span>
<span data-ttu-id="4bde7-175">Atualmente, o Azure AD Connect não dá suporte à sincronização de senhas temporárias com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bde7-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="4bde7-176">Uma senha é considerada toobe temporário se hello **alterar a senha no próximo logon** opção é definida no usuário do hello local do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4bde7-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="4bde7-177">saudação de erro a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="4bde7-177">hello following error is returned:</span></span>

![A senha temporária não é exportada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="4bde7-179">Resultados da última tentativa de toosynchronize senha não estão disponíveis</span><span class="sxs-lookup"><span data-stu-id="4bde7-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="4bde7-180">Por padrão, o Azure AD Connect armazena resultados Olá de tentativas de sincronização de senha por sete dias.</span><span class="sxs-lookup"><span data-stu-id="4bde7-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="4bde7-181">Se não houver nenhum resultado disponível para o objeto do Active Directory Olá selecionado, Olá aviso a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="4bde7-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Saída de diagnóstico de um único objeto – nenhum histórico de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="4bde7-183">Nenhuma senha é sincronizada: etapas manuais de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="4bde7-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="4bde7-184">Siga essas toodetermine etapas porque não há senhas são sincronizadas:</span><span class="sxs-lookup"><span data-stu-id="4bde7-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="4bde7-185">É servidor conectar Olá [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="4bde7-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="4bde7-186">Um servidor no modo de preparo não sincroniza nenhuma senha.</span><span class="sxs-lookup"><span data-stu-id="4bde7-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="4bde7-187">Executar script Olá Olá [obter status de saudação de configurações de sincronização de senha](#get-the-status-of-password-sync-settings) seção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="4bde7-188">Ele fornece uma visão geral da configuração de sincronização de senha hello.</span><span class="sxs-lookup"><span data-stu-id="4bde7-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Saída de script do PowerShell das configurações de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="4bde7-190">Se o recurso de saudação não está habilitado no AD do Azure ou se Olá status de canal de sincronização não está habilitado, execute o Assistente de instalação de conectar-se de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bde7-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="4bde7-191">Selecione **Personalizar opções de sincronização**e desmarque a sincronização de senha. Essa alteração desabilita temporariamente o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bde7-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="4bde7-192">Em seguida, execute novamente o Assistente de saudação e habilite novamente a sincronização de senha. Execute o script hello novamente tooverify que Olá configuração está correta.</span><span class="sxs-lookup"><span data-stu-id="4bde7-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="4bde7-193">Procure no log de eventos de saudação para erros.</span><span class="sxs-lookup"><span data-stu-id="4bde7-193">Look in hello event log for errors.</span></span> <span data-ttu-id="4bde7-194">Procure Olá eventos, o que poderia indicar um problema a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bde7-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="4bde7-195">Fonte: “Sincronização de diretório” ID: 0, 611, 652, 655 Se um desses eventos aparecer, há um problema de conectividade.</span><span class="sxs-lookup"><span data-stu-id="4bde7-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="4bde7-196">mensagem de saudação do log de eventos contém informações sobre a floresta em que você tem um problema.</span><span class="sxs-lookup"><span data-stu-id="4bde7-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="4bde7-197">Para obter mais informações, consulte [Problema de conectividade](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="4bde7-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="4bde7-198">Se não aparecer nenhuma pulsação ou se nada mais funcionou, execute [Disparar uma sincronização completa de todas as senhas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="4bde7-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="4bde7-199">Execute o script hello apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="4bde7-199">Run hello script only once.</span></span>

6. <span data-ttu-id="4bde7-200">Consulte Olá [solucionar problemas de um objeto que não está sincronizando senhas](#one-object-is-not-synchronizing-passwords) seção.</span><span class="sxs-lookup"><span data-stu-id="4bde7-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="4bde7-201">Problemas de conectividade</span><span class="sxs-lookup"><span data-stu-id="4bde7-201">Connectivity problems</span></span>

<span data-ttu-id="4bde7-202">Você tem conectividade com o Azure AD?</span><span class="sxs-lookup"><span data-stu-id="4bde7-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="4bde7-203">Conta Olá exigi hashes de senha de saudação permissões tooread em todos os domínios?</span><span class="sxs-lookup"><span data-stu-id="4bde7-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="4bde7-204">Se você instalou conectar usando as configurações Express, permissões de saudação já devem estar corretas.</span><span class="sxs-lookup"><span data-stu-id="4bde7-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="4bde7-205">Se você usou a instalação personalizada, defina as permissões de saudação manualmente fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4bde7-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="4bde7-206">conta de saudação toofind usada pelo conector do Active Directory hello, início **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="4bde7-207">Vá muito**conectores**e em seguida, procure a floresta de Active Directory local Olá solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="4bde7-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="4bde7-208">Selecione o conector hello e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="4bde7-209">Vá muito**conectar-se a floresta do diretório tooActive**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Conta usada pelo Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="4bde7-211">Observe Olá nome de usuário e domínio Olá onde Olá conta está localizada.</span><span class="sxs-lookup"><span data-stu-id="4bde7-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="4bde7-212">Iniciar **computadores e usuários do Active Directory**e, em seguida, verifique se que conta Olá você encontrou anteriormente tem permissões de acompanhamento de Olá definidas na raiz de saudação de todos os domínios na floresta:</span><span class="sxs-lookup"><span data-stu-id="4bde7-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="4bde7-213">Replicar alterações de diretório</span><span class="sxs-lookup"><span data-stu-id="4bde7-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="4bde7-214">Replicar todas as alterações de diretório</span><span class="sxs-lookup"><span data-stu-id="4bde7-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="4bde7-215">É Olá controladores de domínio pode ser acessados pelo Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="4bde7-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="4bde7-216">Se o servidor de conectar Olá não pode se conectar a controladores de domínio tooall, configurar **usar somente o controlador de domínio preferencial**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Controlador de domínio usado pelo Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="4bde7-218">Voltar muito**Synchronization Service Manager** e **configurar a partição de diretório**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="4bde7-219">Selecione o domínio no **selecionar partições de diretório**, selecione Olá **usam somente controladores de domínio preferencial** caixa de seleção e, em seguida, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="4bde7-220">Na lista de hello, insira os controladores de domínio Olá conectar deve usar para sincronização de senha. Olá mesma lista é usada para importar e exportar também.</span><span class="sxs-lookup"><span data-stu-id="4bde7-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="4bde7-221">Siga estas etapas para todos os domínios.</span><span class="sxs-lookup"><span data-stu-id="4bde7-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="4bde7-222">Se o script hello mostra que não há nenhuma pulsação, execute o script de saudação [disparar uma sincronização completa de todas as senhas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="4bde7-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="4bde7-223">Um objeto não está sincronizando senhas: etapas manuais de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="4bde7-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="4bde7-224">Facilmente, você pode solucionar problemas de sincronização de senha, revisando o status de saudação de um objeto.</span><span class="sxs-lookup"><span data-stu-id="4bde7-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="4bde7-225">Em **computadores e usuários do Active Directory**, pesquisar por usuário hello e, em seguida, verifique se esse Olá **usuário deve alterar a senha no próximo logon** caixa de seleção é desmarcada.</span><span class="sxs-lookup"><span data-stu-id="4bde7-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Senhas produtivas do Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="4bde7-227">Se Olá caixa é selecionada, peça Olá usuário toosign em e alterar a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bde7-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="4bde7-228">As senhas temporárias não são sincronizadas com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bde7-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="4bde7-229">Se a senha Olá parece correta no Active Directory, execute usuário Olá no mecanismo de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bde7-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="4bde7-230">Por usuário Olá seguinte do local do Active Directory tooAzure AD, você pode ver se há um erro descritivo no objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bde7-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="4bde7-231">a.</span><span class="sxs-lookup"><span data-stu-id="4bde7-231">a.</span></span> <span data-ttu-id="4bde7-232">Iniciar Olá [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="4bde7-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="4bde7-233">b.</span><span class="sxs-lookup"><span data-stu-id="4bde7-233">b.</span></span> <span data-ttu-id="4bde7-234">Clique em **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-234">Click **Connectors**.</span></span>

    <span data-ttu-id="4bde7-235">c.</span><span class="sxs-lookup"><span data-stu-id="4bde7-235">c.</span></span> <span data-ttu-id="4bde7-236">Selecione Olá **conector do Active Directory** onde Olá usuário está localizado.</span><span class="sxs-lookup"><span data-stu-id="4bde7-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="4bde7-237">d.</span><span class="sxs-lookup"><span data-stu-id="4bde7-237">d.</span></span> <span data-ttu-id="4bde7-238">Selecione **Pesquisar Espaço do Conector**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="4bde7-239">e.</span><span class="sxs-lookup"><span data-stu-id="4bde7-239">e.</span></span> <span data-ttu-id="4bde7-240">Em Olá **escopo** selecione **DN ou âncora**e, em seguida, insira DN completo de saudação do usuário Olá solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="4bde7-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Pesquisar por usuário no espaço do conector com DN](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="4bde7-242">f.</span><span class="sxs-lookup"><span data-stu-id="4bde7-242">f.</span></span> <span data-ttu-id="4bde7-243">Localizar usuário Olá você está procurando e, em seguida, clique em **propriedades** toosee Olá a todos os atributos.</span><span class="sxs-lookup"><span data-stu-id="4bde7-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="4bde7-244">Se o usuário Olá não estiver no resultado da pesquisa Olá, verifique se o [regras de filtragem](active-directory-aadconnectsync-configure-filtering.md) e certifique-se de que você execute [aplicar e verifique se as alterações](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) para Olá usuário tooappear em conectar.</span><span class="sxs-lookup"><span data-stu-id="4bde7-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="4bde7-245">g.</span><span class="sxs-lookup"><span data-stu-id="4bde7-245">g.</span></span> <span data-ttu-id="4bde7-246">detalhes de sincronização de senha toosee saudação do objeto Olá Olá semana passada, clique **Log**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Detalhes do log do objeto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="4bde7-248">Se o log de objeto Olá estiver vazio, o Azure AD Connect foi hash de senha não é possível tooread Olá do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4bde7-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="4bde7-249">Continue a solução de problemas com [Erros de conectividade](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="4bde7-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="4bde7-250">Se você vir qualquer outro valor que **êxito**, consulte a tabela toohello [log de sincronização de senha](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="4bde7-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="4bde7-251">h.</span><span class="sxs-lookup"><span data-stu-id="4bde7-251">h.</span></span> <span data-ttu-id="4bde7-252">Selecione Olá **linhagem** guia e verifique se essa regra de pelo menos uma sincronização em Olá **PasswordSync** coluna é **True**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="4bde7-253">Configuração padrão de hello, Olá nome da regra de sincronização de saudação é **em do AD - Useraccountenabled**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informações de linhagem de um usuário](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="4bde7-255">i.</span><span class="sxs-lookup"><span data-stu-id="4bde7-255">i.</span></span> <span data-ttu-id="4bde7-256">Clique em **propriedades de objeto do metaverso** toodisplay uma lista de atributos de usuário.</span><span class="sxs-lookup"><span data-stu-id="4bde7-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Informações de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="4bde7-258">Verifique se não há nenhum atributo **cloudFiltered** presente.</span><span class="sxs-lookup"><span data-stu-id="4bde7-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="4bde7-259">Certifique-se de que os atributos de domínio de saudação (domainFQDN e domainNetBios) têm valores esperados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bde7-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="4bde7-260">j.</span><span class="sxs-lookup"><span data-stu-id="4bde7-260">j.</span></span> <span data-ttu-id="4bde7-261">Clique em Olá **conectores** guia. Certifique-se de que você vê os conectores tooboth do Active Directory local e o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bde7-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Informações de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="4bde7-263">k.</span><span class="sxs-lookup"><span data-stu-id="4bde7-263">k.</span></span> <span data-ttu-id="4bde7-264">Linha de saudação Select que representa o AD do Azure, clique em **propriedades**e, em seguida, clique em Olá **linhagem** objeto de espaço do conector de saudação de guia deve ter uma regra de saída em Olá **PasswordSync** coluna definida muito**True**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="4bde7-265">Configuração padrão de hello, Olá nome da regra de sincronização de saudação é **Out tooAAD - ingresso de usuário**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Caixa de diálogo Propriedades do objeto de espaço do conector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="4bde7-267">Log de sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="4bde7-267">Password sync log</span></span>
<span data-ttu-id="4bde7-268">coluna de status de saudação pode ter Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bde7-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="4bde7-269">Status</span><span class="sxs-lookup"><span data-stu-id="4bde7-269">Status</span></span> | <span data-ttu-id="4bde7-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="4bde7-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4bde7-271">Sucesso</span><span class="sxs-lookup"><span data-stu-id="4bde7-271">Success</span></span> |<span data-ttu-id="4bde7-272">A senha foi sincronizada com êxito.</span><span class="sxs-lookup"><span data-stu-id="4bde7-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="4bde7-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="4bde7-273">FilteredByTarget</span></span> |<span data-ttu-id="4bde7-274">Senha está definida muito**usuário deve alterar a senha no próximo logon**.</span><span class="sxs-lookup"><span data-stu-id="4bde7-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="4bde7-275">A senha não foi sincronizada.</span><span class="sxs-lookup"><span data-stu-id="4bde7-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="4bde7-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="4bde7-276">NoTargetConnection</span></span> |<span data-ttu-id="4bde7-277">Nenhum objeto no metaverso hello, ou no espaço do conector de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bde7-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="4bde7-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="4bde7-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="4bde7-279">Nenhum objeto encontrado no espaço do conector Olá local do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4bde7-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="4bde7-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="4bde7-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="4bde7-281">objeto Olá Olá espaço do conector AD do Azure ainda não foram exportado.</span><span class="sxs-lookup"><span data-stu-id="4bde7-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="4bde7-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="4bde7-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="4bde7-283">A entrada de log foi criada antes da versão 1.0.9125.0 e é mostrada em seu estado herdado.</span><span class="sxs-lookup"><span data-stu-id="4bde7-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="4bde7-284">Erro</span><span class="sxs-lookup"><span data-stu-id="4bde7-284">Error</span></span> |<span data-ttu-id="4bde7-285">O serviço retornou um erro desconhecido.</span><span class="sxs-lookup"><span data-stu-id="4bde7-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="4bde7-286">Desconhecido</span><span class="sxs-lookup"><span data-stu-id="4bde7-286">Unknown</span></span> |<span data-ttu-id="4bde7-287">Ocorreu um erro durante a tentativa de tooprocess um lote de hashes de senha.</span><span class="sxs-lookup"><span data-stu-id="4bde7-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="4bde7-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="4bde7-288">MissingAttribute</span></span> |<span data-ttu-id="4bde7-289">Atributos específicos (por exemplo, o hash de Kerberos) exigidos pelos Azure AD Domain Services não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4bde7-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="4bde7-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="4bde7-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="4bde7-291">Atributos específicos (por exemplo, o hash de Kerberos) exigidos pelos Azure AD Domain Services não estavam disponíveis anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4bde7-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="4bde7-292">É feita uma tentativa de tooresynchronize saudação do hash de senha.</span><span class="sxs-lookup"><span data-stu-id="4bde7-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="4bde7-293">Solução de problemas de toohelp de scripts</span><span class="sxs-lookup"><span data-stu-id="4bde7-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="4bde7-294">Obter status de saudação de configurações de sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="4bde7-294">Get hello status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="4bde7-295">Disparar uma sincronização completa de todas as senhas</span><span class="sxs-lookup"><span data-stu-id="4bde7-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="4bde7-296">Execute este script apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="4bde7-296">Run this script only once.</span></span> <span data-ttu-id="4bde7-297">Se você precisar toorun-mais de uma vez, algo é problema hello.</span><span class="sxs-lookup"><span data-stu-id="4bde7-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="4bde7-298">tootroubleshoot Olá problema, contate o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4bde7-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="4bde7-299">Você pode disparar uma sincronização completa de todas as senhas usando Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bde7-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4bde7-300">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4bde7-300">Next steps</span></span>
* [<span data-ttu-id="4bde7-301">Implementação de sincronização de senha com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4bde7-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="4bde7-302">Sincronização do Azure AD Connect: personalizando as opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="4bde7-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4bde7-303">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4bde7-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
