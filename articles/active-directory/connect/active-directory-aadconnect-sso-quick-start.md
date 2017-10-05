---
title: "Azure AD Connect: Logon Único Contínuo – Início Rápido| Microsoft Docs"
description: "Este artigo descreve como começar a usar o Logon Único Contínuo do Azure Active Directory."
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
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="2b9df-104">Logon Único Contínuo do Azure Active Directory: Início Rápido</span><span class="sxs-lookup"><span data-stu-id="2b9df-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="2b9df-105">Como implantar o SSO Contínuo</span><span class="sxs-lookup"><span data-stu-id="2b9df-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="2b9df-106">O SSO Contínuo do Azure AD (Logon Único Contínuo do Azure Active Directory) conecta usuários automaticamente quando estiverem nos respectivos desktops corporativos conectados à rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="2b9df-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="2b9df-107">Ele fornece aos usuários acesso fácil a seus aplicativos baseados em nuvem sem a necessidade de nenhum componente local adicional.</span><span class="sxs-lookup"><span data-stu-id="2b9df-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b9df-108">Atualmente, o recurso SSO Contínuo está em visualização.</span><span class="sxs-lookup"><span data-stu-id="2b9df-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="2b9df-109">Para implantar o SSO Contínuo, você precisa seguir estas etapas:</span><span class="sxs-lookup"><span data-stu-id="2b9df-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="2b9df-110">Etapa 1: verificar pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2b9df-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="2b9df-111">Verifique se os seguintes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="2b9df-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="2b9df-112">Configurar seu servidor do Azure AD Connect: se você usa a [Autenticação de Passagem](active-directory-aadconnect-pass-through-authentication.md) como seu método de entrada, nenhuma ação adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="2b9df-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="2b9df-113">Se você usa a [Sincronização de Hash de Senha](active-directory-aadconnectsync-implement-password-synchronization.md) como seu método de entrada e se há um firewall entre o Azure AD Connect e Azure AD, verifique se:</span><span class="sxs-lookup"><span data-stu-id="2b9df-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="2b9df-114">Você está usando versões 1.1.484.0 ou posteriores do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2b9df-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="2b9df-115">O Azure AD Connect pode se comunicar com URLs `*.msappproxy.net` e sobre a porta 443.</span><span class="sxs-lookup"><span data-stu-id="2b9df-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="2b9df-116">Esse pré-requisito é aplicável somente quando você habilita o recurso e não para entradas reais de usuário.</span><span class="sxs-lookup"><span data-stu-id="2b9df-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="2b9df-117">O Azure AD Connect pode realizar conexões IP diretas com os [intervalos de IP do data center do Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2b9df-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="2b9df-118">Novamente, esse pré-requisito é aplicável somente quando você habilita o recurso.</span><span class="sxs-lookup"><span data-stu-id="2b9df-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="2b9df-119">Você precisa de credenciais de Administrador de Domínio para cada floresta do AD que você sincronizar com o Azure AD (usando o Azure AD Connect) e para aqueles usuários que você deseja habilitar o SSO Contínuo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="2b9df-120">Etapa 2: habilitar o recurso</span><span class="sxs-lookup"><span data-stu-id="2b9df-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="2b9df-121">O SSO Contínuo pode ser habilitado usando o [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="2b9df-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="2b9df-122">Se você está realizando uma instalação nova do Azure AD Connect, escolha o [caminho de instalação personalizada](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2b9df-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="2b9df-123">Na página "Entrada do usuário", marque a opção "Habilitar logon único".</span><span class="sxs-lookup"><span data-stu-id="2b9df-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect – Entrada do usuário](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="2b9df-125">Se você já tem uma instalação do Azure AD Connect, escolha "Alterar página de entrada do usuário" no Azure AD Connect e clique em "Avançar".</span><span class="sxs-lookup"><span data-stu-id="2b9df-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="2b9df-126">Em seguida, marque a opção "Habilitar logon único".</span><span class="sxs-lookup"><span data-stu-id="2b9df-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect – Alterar entrada do usuário](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="2b9df-128">Prossiga com o assistente até chegar à página “Habilitar logon único”.</span><span class="sxs-lookup"><span data-stu-id="2b9df-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="2b9df-129">Forneça credenciais de Administrador de Domínio para cada floresta do AD que você sincronizar com o Azure AD (usando o Azure AD Connect) e para aqueles usuários que você deseja habilitar o SSO Contínuo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="2b9df-130">Após a conclusão do assistente, o SSO Contínuo está habilitado no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="2b9df-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="2b9df-131">As credenciais de Administrador de Domínio não são armazenadas no Azure AD Connect ou no Azure AD, mas são usadas somente para habilitar o recurso.</span><span class="sxs-lookup"><span data-stu-id="2b9df-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="2b9df-132">Siga estas instruções para verificar se você habilitou o SSO Contínuo corretamente:</span><span class="sxs-lookup"><span data-stu-id="2b9df-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="2b9df-133">Entre no [centro de administração do Azure Active Directory](https://aad.portal.azure.com) com as credenciais do Administrador Global do seu locatário.</span><span class="sxs-lookup"><span data-stu-id="2b9df-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="2b9df-134">Selecione **Azure Active Directory** na navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b9df-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="2b9df-135">Selecione **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="2b9df-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="2b9df-136">Verifique se o recurso **Logon Único Contínuo** está **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="2b9df-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Portal do Azure – folha do Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="2b9df-138">Etapa 3: distribuir o recurso</span><span class="sxs-lookup"><span data-stu-id="2b9df-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="2b9df-139">Para distribuir o recurso aos seus usuários, você precisará adicionar duas URLs do Azure AD (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) às configurações de zona de Intranet dos usuários por meio da Política de Grupo no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b9df-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="2b9df-140">As instruções a seguir só funcionam para o Internet Explorer e Google Chrome no Windows (se ele compartilha o conjunto de URLs de sites confiáveis com o Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="2b9df-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="2b9df-141">Leia a próxima seção para obter instruções para configurar o Mozilla Firefox e Google Chrome no Mac.</span><span class="sxs-lookup"><span data-stu-id="2b9df-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="2b9df-142">Por que você precisa modificar as configurações de Zona da Intranet dos usuários?</span><span class="sxs-lookup"><span data-stu-id="2b9df-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="2b9df-143">Por padrão, o navegador calcula automaticamente a zona correta (Internet ou Intranet) com base em uma URL.</span><span class="sxs-lookup"><span data-stu-id="2b9df-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="2b9df-144">Por exemplo, http://contoso/ é mapeada para a Zona da Intranet, enquanto que http://intranet.contoso.com/ é mapeada para a Zona da Internet (porque a URL contém um ponto).</span><span class="sxs-lookup"><span data-stu-id="2b9df-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="2b9df-145">Os navegadores não enviam tíquetes Kerberos a um ponto de extremidade de nuvem – como as duas URLs do Azure AD – a menos que a URL seja explicitamente adicionada à Zona da Intranet do navegador.</span><span class="sxs-lookup"><span data-stu-id="2b9df-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="2b9df-146">Etapas detalhadas</span><span class="sxs-lookup"><span data-stu-id="2b9df-146">Detailed steps</span></span>

1. <span data-ttu-id="2b9df-147">Abra a ferramenta de Gerenciamento de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="2b9df-148">Edite a Política de Grupo que é aplicada a alguns ou todos os seus usuários.</span><span class="sxs-lookup"><span data-stu-id="2b9df-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="2b9df-149">Neste exemplo, usamos a **Política de Domínio Padrão**.</span><span class="sxs-lookup"><span data-stu-id="2b9df-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="2b9df-150">Navegue até **Configuração do Usuário\Modelos Administrativos\Componentes do Windows\Internet Explorer\Painel de Controle da Internet\Página de Segurança** e selecione **Lista de Atribuição de Site para Zona**.</span><span class="sxs-lookup"><span data-stu-id="2b9df-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="2b9df-151">![Logon Único](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="2b9df-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="2b9df-152">Habilite a política e insira os seguintes valores (URLs do Azure AD em que os tíquetes Kerberos são encaminhados) e dados (*1* indica a Zona da Intranet) na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="2b9df-153">Se você quiser cancelar a permissão de uso do SSO Contínuo de alguns usuários – por exemplo, se esses usuários estiverem entrando em quiosques compartilhados – defina os valores anteriores como *4*.</span><span class="sxs-lookup"><span data-stu-id="2b9df-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="2b9df-154">Essa ação adiciona as URLs do Azure AD à Zona Restrita e ocasiona a falha do SSO Contínuo todas as vezes.</span><span class="sxs-lookup"><span data-stu-id="2b9df-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="2b9df-155">Clique em **OK** e em **OK** novamente.</span><span class="sxs-lookup"><span data-stu-id="2b9df-155">Click **OK** and **OK** again.</span></span>

![Logon único](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="2b9df-157">Considerações de navegador</span><span class="sxs-lookup"><span data-stu-id="2b9df-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="2b9df-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="2b9df-158">Mozilla Firefox</span></span>

<span data-ttu-id="2b9df-159">O Mozilla Firefox não faz a autenticação Kerberos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2b9df-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="2b9df-160">Cada usuário tem que adicionar manualmente as URLs do Azure AD às suas configurações do Firefox através das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2b9df-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="2b9df-161">Execute o Firefox e digite `about:config` na barra de endereços.</span><span class="sxs-lookup"><span data-stu-id="2b9df-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="2b9df-162">Ignore as notificações que aparecerem.</span><span class="sxs-lookup"><span data-stu-id="2b9df-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="2b9df-163">Pesquise a preferência **network.negotiate-auth.trusted-uris**.</span><span class="sxs-lookup"><span data-stu-id="2b9df-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="2b9df-164">Esta preferência lista os sites confiáveis do Firefox para a autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="2b9df-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="2b9df-165">Clique com o botão direito do mouse e selecione "Modificar".</span><span class="sxs-lookup"><span data-stu-id="2b9df-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="2b9df-166">Insira "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" no campo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="2b9df-167">Clique em "OK" e reabra o navegador.</span><span class="sxs-lookup"><span data-stu-id="2b9df-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="2b9df-168">Safari no Mac OS</span><span class="sxs-lookup"><span data-stu-id="2b9df-168">Safari on Mac OS</span></span>

<span data-ttu-id="2b9df-169">Certifique-se de que o computador executando o Mac OS é associado ao AD.</span><span class="sxs-lookup"><span data-stu-id="2b9df-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="2b9df-170">Para obter instruções sobre como fazer isso [aqui](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="2b9df-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="2b9df-171">Google Chrome no Mac OS</span><span class="sxs-lookup"><span data-stu-id="2b9df-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="2b9df-172">Para o Google Chrome no Mac OS e outras plataformas que não sejam Windows, consulte [este artigo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) para obter informações sobre como adicionar as URLs do Azure AD à lista de permissões para uma autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="2b9df-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="2b9df-173">O uso de extensões de Política de Grupo do Active Directory de terceiros para distribuir as URLs do Azure AD para o Firefox e o Google Chrome em usuários do Mac está fora do escopo deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="2b9df-174">Limitações conhecidas</span><span class="sxs-lookup"><span data-stu-id="2b9df-174">Known limitations</span></span>

<span data-ttu-id="2b9df-175">O SSO Contínuo não funciona no modo de navegação particular em navegadores Firefox e Edge.</span><span class="sxs-lookup"><span data-stu-id="2b9df-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="2b9df-176">Também não funciona no Internet Explorer se o navegador estiver em execução no modo de proteção aprimorada.</span><span class="sxs-lookup"><span data-stu-id="2b9df-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b9df-177">Recentemente, nós revertemos o suporte ao Edge para investigarmos problemas reportados por clientes.</span><span class="sxs-lookup"><span data-stu-id="2b9df-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="2b9df-178">Etapa 4: testar o recurso</span><span class="sxs-lookup"><span data-stu-id="2b9df-178">Step 4: Test the feature</span></span>

<span data-ttu-id="2b9df-179">Para testar o recurso para um usuário específico, verifique se _todas_ as seguintes condições estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="2b9df-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="2b9df-180">O usuário está entrando em um dispositivo corporativo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="2b9df-181">O dispositivo ingressou anteriormente em seu domínio do AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2b9df-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="2b9df-182">O dispositivo tem uma conexão direta com seu DC (Controlador de Domínio), seja na rede corporativa com ou sem fio ou por meio de uma conexão de acesso remoto, como uma conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="2b9df-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="2b9df-183">Você [distribuiu o recurso](##step-3-roll-out-the-feature) a esse usuário usando a Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="2b9df-184">Para testar o cenário em que o usuário insere somente o nome de usuário, mas não a senha:</span><span class="sxs-lookup"><span data-stu-id="2b9df-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="2b9df-185">Entre no *https://myapps.microsoft.com/* em uma nova sessão privativa do navegador.</span><span class="sxs-lookup"><span data-stu-id="2b9df-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="2b9df-186">Para testar o cenário em que o usuário não tenha que inserir o nome de usuário ou a senha:</span><span class="sxs-lookup"><span data-stu-id="2b9df-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="2b9df-187">Entre no *https://myapps.microsoft.com/contoso.onmicrosoft.com* em uma nova sessão privativa do navegador.</span><span class="sxs-lookup"><span data-stu-id="2b9df-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="2b9df-188">Substitua "*contoso*" pelo nome do seu locatário.</span><span class="sxs-lookup"><span data-stu-id="2b9df-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="2b9df-189">Ou entre no *https://myapps.microsoft.com/contoso.com* em uma nova sessão privativa do navegador.</span><span class="sxs-lookup"><span data-stu-id="2b9df-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="2b9df-190">Substitua "*contoso.com*" por um domínio verificado (não um domínio federado) em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="2b9df-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="2b9df-191">Etapa 5: Sobrepor chaves</span><span class="sxs-lookup"><span data-stu-id="2b9df-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="2b9df-192">Na etapa 2, o Azure AD Connect cria contas de computador (representando o AD do Azure) em todas as florestas do AD no qual você habilitou o SSO contínuo.</span><span class="sxs-lookup"><span data-stu-id="2b9df-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="2b9df-193">Saiba mais detalhes [aqui](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="2b9df-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="2b9df-194">Para maior segurança, é recomendável que você sobreponha frequentemente chaves de descriptografia Kerberos dessas contas de computador.</span><span class="sxs-lookup"><span data-stu-id="2b9df-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b9df-195">Você não precisa executar essa etapa _imediatamente_ depois de habilitar o recurso.</span><span class="sxs-lookup"><span data-stu-id="2b9df-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="2b9df-196">Sobrepor as chaves de descriptografia Kerberos pelo menos a cada 30 dias.</span><span class="sxs-lookup"><span data-stu-id="2b9df-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b9df-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b9df-197">Next steps</span></span>

- <span data-ttu-id="2b9df-198">[**Aprofundamento técnico**](active-directory-aadconnect-sso-how-it-works.md) – entenda como esse recurso funciona.</span><span class="sxs-lookup"><span data-stu-id="2b9df-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="2b9df-199">[**Perguntas frequentes**](active-directory-aadconnect-sso-faq.md) – respostas para perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="2b9df-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="2b9df-200">[**Solução de problemas**](active-directory-aadconnect-troubleshoot-sso.md) – Saiba como resolver problemas comuns do recurso.</span><span class="sxs-lookup"><span data-stu-id="2b9df-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="2b9df-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="2b9df-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
