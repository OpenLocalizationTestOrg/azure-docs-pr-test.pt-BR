---
title: "Azure AD Connect: Logon Único Contínuo – Início Rápido| Microsoft Docs"
description: Este artigo descreve como tooget iniciada com o Azure Active Directory perfeita Single Sign-On.
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="a45df-104">Logon Único Contínuo do Azure Active Directory: Início Rápido</span><span class="sxs-lookup"><span data-stu-id="a45df-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="a45df-105">Como toodeploy SSO contínuo</span><span class="sxs-lookup"><span data-stu-id="a45df-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="a45df-106">Azure Active Directory perfeita SSO (Azure AD perfeita SSO) assina automaticamente os usuários quando eles estão na sua rede corporativa de tooyour conectado de áreas de trabalho corporativas.</span><span class="sxs-lookup"><span data-stu-id="a45df-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="a45df-107">Ele fornece a seus usuários fácil acesso tooyour baseado em nuvem aplicativos sem a necessidade de todos os componentes locais adicionais.</span><span class="sxs-lookup"><span data-stu-id="a45df-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a45df-108">recurso de SSO contínuo Hello está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="a45df-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="a45df-109">toodeploy SSO contínuo, você precisa toofollow estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a45df-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="a45df-110">Etapa 1: verificar pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a45df-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="a45df-111">Certifique-se de que Olá pré-requisitos a seguir foram atendidos:</span><span class="sxs-lookup"><span data-stu-id="a45df-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="a45df-112">Configurar seu servidor do Azure AD Connect: se você usa a [Autenticação de Passagem](active-directory-aadconnect-pass-through-authentication.md) como seu método de entrada, nenhuma ação adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="a45df-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="a45df-113">Se você usa a [Sincronização de Hash de Senha](active-directory-aadconnectsync-implement-password-synchronization.md) como seu método de entrada e se há um firewall entre o Azure AD Connect e Azure AD, verifique se:</span><span class="sxs-lookup"><span data-stu-id="a45df-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="a45df-114">Você está usando versões 1.1.484.0 ou posteriores do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a45df-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="a45df-115">O Azure AD Connect pode se comunicar com URLs `*.msappproxy.net` e sobre a porta 443.</span><span class="sxs-lookup"><span data-stu-id="a45df-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="a45df-116">Esse pré-requisito é aplicável somente ao habilitar o recurso de hello, não para logons de usuário real.</span><span class="sxs-lookup"><span data-stu-id="a45df-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="a45df-117">Conexão do AD do Azure pode tornar toohello de conexões IP direto [Datacenter do Azure intervalos IP](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="a45df-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="a45df-118">Novamente, esse pré-requisito é aplicável somente quando você habilitar o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="a45df-119">Você precisa ter credenciais de administrador de domínio para cada floresta do AD que você sincronize tooAzure AD (usando o Azure AD Connect) e cujos usuários você deseja tooenable SSO contínuo.</span><span class="sxs-lookup"><span data-stu-id="a45df-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="a45df-120">Etapa 2: Habilitar o recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="a45df-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="a45df-121">O SSO Contínuo pode ser habilitado usando o [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="a45df-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="a45df-122">Se você estiver fazendo uma instalação nova do Azure AD Connect, escolha Olá [caminho de instalação personalizado](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a45df-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="a45df-123">Em hello "usuário" página de entrada, marque a opção de "Habilitar logon único" de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect – Entrada do usuário](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="a45df-125">Se você já tem uma instalação do Azure AD Connect, escolha "Alterar página de entrada do usuário" no Azure AD Connect e clique em "Avançar".</span><span class="sxs-lookup"><span data-stu-id="a45df-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="a45df-126">Em seguida, marque a opção de "Habilitar logon único" de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect – Alterar entrada do usuário](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="a45df-128">Prossiga com o assistente Olá até chegar a página de "Habilitar logon único" toohello.</span><span class="sxs-lookup"><span data-stu-id="a45df-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="a45df-129">Forneça credenciais de administrador de domínio para cada floresta do AD que você sincronize tooAzure AD (usando o Azure AD Connect) e cujos usuários você deseja tooenable SSO contínuo.</span><span class="sxs-lookup"><span data-stu-id="a45df-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="a45df-130">Após a conclusão do Assistente de saudação, SSO contínua está habilitada em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="a45df-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="a45df-131">credenciais de administrador de domínio Olá não são armazenadas no Azure AD Connect ou no AD do Azure, mas são somente o recurso de saudação tooenable usado.</span><span class="sxs-lookup"><span data-stu-id="a45df-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="a45df-132">Siga essas tooverify instruções que você tenha ativado SSO contínuo corretamente:</span><span class="sxs-lookup"><span data-stu-id="a45df-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="a45df-133">Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global de saudação para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="a45df-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="a45df-134">Selecione **Active Directory do Azure** na navegação esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="a45df-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="a45df-135">Selecione **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="a45df-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="a45df-136">Verifique se esse Olá **logon único perfeita** recurso mostra como **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="a45df-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Portal do Azure – folha do Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="a45df-138">Etapa 3: Implantar o recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="a45df-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="a45df-139">tooroll usuários de tooyour recurso hello, terá as configurações de zona de Intranet dos tooadd duas URLs do AD do Azure (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) toousers por meio da política de grupo no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a45df-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="a45df-140">Olá seguindo as instruções só funciona para o Internet Explorer e Google Chrome no Windows (se ele compartilha o conjunto de URLs de sites confiáveis no Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="a45df-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="a45df-141">Ler a próxima seção Olá para instruções tooset Mozilla Firefox e Google Chrome no Mac.</span><span class="sxs-lookup"><span data-stu-id="a45df-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="a45df-142">Por que você precisa de configurações da zona de Intranet toomodify dos usuários?</span><span class="sxs-lookup"><span data-stu-id="a45df-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="a45df-143">Por padrão, o navegador Olá calcula automaticamente zona de saudação à direita (Internet ou Intranet) de uma URL.</span><span class="sxs-lookup"><span data-stu-id="a45df-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="a45df-144">Por exemplo, http://contoso/ é mapeado toohello zona de Intranet, enquanto http://intranet.contoso.com/ é mapeada toohello da zona da Internet (como Olá URL contém um ponto).</span><span class="sxs-lookup"><span data-stu-id="a45df-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="a45df-145">Navegadores não enviam o ponto de extremidade do Kerberos tíquetes tooa nuvem - como Olá duas do Azure AD URLs - a menos que sua URL explicitamente é adicionada a zona de Intranet toohello do navegador.</span><span class="sxs-lookup"><span data-stu-id="a45df-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="a45df-146">Etapas detalhadas</span><span class="sxs-lookup"><span data-stu-id="a45df-146">Detailed steps</span></span>

1. <span data-ttu-id="a45df-147">Abra a ferramenta de gerenciamento de diretiva de grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="a45df-148">Edite saudação diretiva de grupo é aplicada toosome ou todos os seus usuários.</span><span class="sxs-lookup"><span data-stu-id="a45df-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="a45df-149">Neste exemplo, usamos Olá **Default Domain Policy**.</span><span class="sxs-lookup"><span data-stu-id="a45df-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="a45df-150">Navegue muito**página do usuário \ Modelos Administrativos\Componentes do Windows\Internet Explorer controle Panel\Security** e selecione **tooZone lista de atribuição de Site**.</span><span class="sxs-lookup"><span data-stu-id="a45df-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="a45df-151">![Logon Único](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="a45df-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="a45df-152">Habilitar a política de Olá e digite hello valores (URLs AD do Azure onde os tíquetes Kerberos são encaminhados) a seguir e dados (*1* indica a zona da Intranet) na caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="a45df-153">Se você quiser toodisallow alguns usuários usem SSO contínuo - por exemplo, se esses usuários estão entrando em quiosques compartilhados - defina Olá anterior valores muito*4*.</span><span class="sxs-lookup"><span data-stu-id="a45df-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="a45df-154">Essa ação adiciona Olá URLs do AD do Azure toohello zona restrita e falha todo o tempo de saudação de SSO contínuo.</span><span class="sxs-lookup"><span data-stu-id="a45df-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="a45df-155">Clique em **OK** e em **OK** novamente.</span><span class="sxs-lookup"><span data-stu-id="a45df-155">Click **OK** and **OK** again.</span></span>

![Logon único](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="a45df-157">Considerações de navegador</span><span class="sxs-lookup"><span data-stu-id="a45df-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="a45df-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="a45df-158">Mozilla Firefox</span></span>

<span data-ttu-id="a45df-159">O Mozilla Firefox não faz a autenticação Kerberos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a45df-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="a45df-160">Cada usuário tem toomanually adicionar configurações de saudação do AD do Azure URLs tootheir Firefox usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a45df-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="a45df-161">Execute o Firefox e digite `about:config` na barra de endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="a45df-162">Ignore as notificações que aparecerem.</span><span class="sxs-lookup"><span data-stu-id="a45df-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="a45df-163">Pesquise Olá **network.negotiate-auth.trusted-uris** preferência.</span><span class="sxs-lookup"><span data-stu-id="a45df-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="a45df-164">Esta preferência lista os sites confiáveis do Firefox para a autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a45df-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="a45df-165">Clique com o botão direito do mouse e selecione "Modificar".</span><span class="sxs-lookup"><span data-stu-id="a45df-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="a45df-166">Insira "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" no campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="a45df-167">Clique em "Okey" e reabra o navegador hello.</span><span class="sxs-lookup"><span data-stu-id="a45df-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="a45df-168">Safari no Mac OS</span><span class="sxs-lookup"><span data-stu-id="a45df-168">Safari on Mac OS</span></span>

<span data-ttu-id="a45df-169">Verifique essa máquina Olá executando o Mac OS tooAD unida.</span><span class="sxs-lookup"><span data-stu-id="a45df-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="a45df-170">Consulte as instruções sobre como toodo que [aqui](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="a45df-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="a45df-171">Google Chrome no Mac OS</span><span class="sxs-lookup"><span data-stu-id="a45df-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="a45df-172">Para o Google Chrome no Mac OS e outras plataformas não Windows, consulte muito[neste artigo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) para obter informações sobre como toowhitelist Olá URLs do AD do Azure para a autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="a45df-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="a45df-173">Usando a diretiva de grupo de Active Directory de terceiros tooroll extensões Olá URLs do AD do Azure tooFirefox e Google Chrome em usuários do Mac está fora do escopo deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a45df-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="a45df-174">Limitações conhecidas</span><span class="sxs-lookup"><span data-stu-id="a45df-174">Known limitations</span></span>

<span data-ttu-id="a45df-175">O SSO Contínuo não funciona no modo de navegação particular em navegadores Firefox e Edge.</span><span class="sxs-lookup"><span data-stu-id="a45df-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="a45df-176">Também não funciona no Internet Explorer se Olá navegador é executado no modo de proteção aprimorada.</span><span class="sxs-lookup"><span data-stu-id="a45df-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a45df-177">Podemos recentemente revertida suporte para a borda tooinvestigate problemas reportados por clientes.</span><span class="sxs-lookup"><span data-stu-id="a45df-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="a45df-178">Etapa 4: Testar o recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="a45df-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="a45df-179">recurso de saudação tootest para um usuário específico, certifique-se de que _todos os_ Olá condições a seguir foram atendidos:</span><span class="sxs-lookup"><span data-stu-id="a45df-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="a45df-180">usuário Hello está entrando em um dispositivo corporativo.</span><span class="sxs-lookup"><span data-stu-id="a45df-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="a45df-181">dispositivo de saudação foi tooyour anteriormente ingressado no domínio de AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a45df-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="a45df-182">dispositivo Olá tem uma conexão direta de tooyour Domain Controller (DC), na rede corporativa Olá com ou sem fio ou por uma conexão de acesso remoto, como uma conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="a45df-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="a45df-183">Você tem [distribuiu recurso Olá](##step-3-roll-out-the-feature) toothis usuário usando a diretiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="a45df-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="a45df-184">cenário de saudação tootest onde o usuário de Olá insere apenas Olá nome de usuário, mas a senha não é hello:</span><span class="sxs-lookup"><span data-stu-id="a45df-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="a45df-185">Entre no *https://myapps.microsoft.com/* em uma nova sessão privativa do navegador.</span><span class="sxs-lookup"><span data-stu-id="a45df-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="a45df-186">cenário de saudação tootest onde o usuário Olá não tem senha de nome de usuário ou Olá Olá tooenter:</span><span class="sxs-lookup"><span data-stu-id="a45df-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="a45df-187">Entre no *https://myapps.microsoft.com/contoso.onmicrosoft.com* em uma nova sessão privativa do navegador.</span><span class="sxs-lookup"><span data-stu-id="a45df-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="a45df-188">Substitua "*contoso*" pelo nome do seu locatário.</span><span class="sxs-lookup"><span data-stu-id="a45df-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="a45df-189">Ou entre no *https://myapps.microsoft.com/contoso.com* em uma nova sessão privativa do navegador.</span><span class="sxs-lookup"><span data-stu-id="a45df-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="a45df-190">Substitua "*contoso.com*" por um domínio verificado (não um domínio federado) em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="a45df-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="a45df-191">Etapa 5: Sobrepor chaves</span><span class="sxs-lookup"><span data-stu-id="a45df-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="a45df-192">Na etapa 2, o Azure AD Connect cria contas de computador (representando o AD do Azure) em todas as florestas Olá AD no qual você habilitou o SSO contínuo.</span><span class="sxs-lookup"><span data-stu-id="a45df-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="a45df-193">Saiba mais detalhes [aqui](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="a45df-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="a45df-194">Para maior segurança, é recomendável que você frequentemente mudarem chaves de descriptografia de Kerberos Olá dessas contas de computador.</span><span class="sxs-lookup"><span data-stu-id="a45df-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a45df-195">Você não precisará desta etapa toodo _imediatamente_ depois que você habilitou o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="a45df-196">Sobrepor chaves de descriptografia de Kerberos Olá pelo menos a cada 30 dias.</span><span class="sxs-lookup"><span data-stu-id="a45df-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a45df-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a45df-197">Next steps</span></span>

- <span data-ttu-id="a45df-198">[**Aprofundamento técnico**](active-directory-aadconnect-sso-how-it-works.md) – entenda como esse recurso funciona.</span><span class="sxs-lookup"><span data-stu-id="a45df-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="a45df-199">[**Perguntas frequentes sobre** ](active-directory-aadconnect-sso-faq.md) -respostas toofrequently perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="a45df-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="a45df-200">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comum problemas com o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a45df-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="a45df-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="a45df-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
