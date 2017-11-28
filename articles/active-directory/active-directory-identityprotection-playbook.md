---
title: "Guia estratégico de proteção de identidade do Active Directory aaaAzure | Microsoft Docs"
description: "Saiba como Azure AD Identity Protection permite que você toolimit capacidade Olá tooexploit um invasor uma identidade comprometida ou dispositivo e toosecure uma identidade ou um dispositivo que era anteriormente conhecido ou suspeita toobe comprometido."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="ddace-104">Guia estratégico do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ddace-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="ddace-105">Este guia estratégico vai ajudá-lo a:</span><span class="sxs-lookup"><span data-stu-id="ddace-105">This playbook helps you to:</span></span>

* <span data-ttu-id="ddace-106">Preencher os dados no ambiente de proteção de identidade hello, simulando eventos de risco e vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="ddace-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="ddace-107">Configurar políticas de acesso condicional com base em risco e teste o impacto Olá dessas políticas</span><span class="sxs-lookup"><span data-stu-id="ddace-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="ddace-108">Simulação de Eventos de Risco</span><span class="sxs-lookup"><span data-stu-id="ddace-108">Simulating Risk Events</span></span>
<span data-ttu-id="ddace-109">Esta seção fornece as etapas para simular Olá seguintes tipos de eventos de risco:</span><span class="sxs-lookup"><span data-stu-id="ddace-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="ddace-110">Entradas de endereços IP anônimos (fácil)</span><span class="sxs-lookup"><span data-stu-id="ddace-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="ddace-111">Entradas de locais desconhecidos (moderado)</span><span class="sxs-lookup"><span data-stu-id="ddace-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="ddace-112">Viagem impossível tooatypical locais (difícil)</span><span class="sxs-lookup"><span data-stu-id="ddace-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="ddace-113">Outros eventos de risco não podem ser simulados de maneira segura.</span><span class="sxs-lookup"><span data-stu-id="ddace-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="ddace-114">Entradas de endereços IP anônimos</span><span class="sxs-lookup"><span data-stu-id="ddace-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="ddace-115">Esse tipo de evento de risco identifica os usuários que entraram com êxito de um endereço IP que foi identificado como um endereço IP de proxy anônimo.</span><span class="sxs-lookup"><span data-stu-id="ddace-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="ddace-116">Esses proxies são usados por pessoas que desejam toohide endereço IP do seu dispositivo e podem ser usadas com objetivos mal-intencionados.</span><span class="sxs-lookup"><span data-stu-id="ddace-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="ddace-117">**toosimulate uma entrada de um IP anônimo, executar Olá etapas**:</span><span class="sxs-lookup"><span data-stu-id="ddace-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="ddace-118">Baixar Olá [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="ddace-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="ddace-119">Usando o hello Tor Browser, navegue muito[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ddace-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="ddace-120">Insira as credenciais de saudação da conta de saudação desejado tooappear em hello **entradas de endereços IP anônimos** relatório.</span><span class="sxs-lookup"><span data-stu-id="ddace-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="ddace-121">Olá entrar aparecerão no painel de proteção de identidade Olá em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="ddace-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="ddace-122">Entradas de locais desconhecidos</span><span class="sxs-lookup"><span data-stu-id="ddace-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="ddace-123">risco de locais desconhecidos Hello é um mecanismo de avaliação de entrada em tempo real que considera após entrar locais (IP, Latitude / Longitude e ASN) toodetermine locais de novo / desconhecidos.</span><span class="sxs-lookup"><span data-stu-id="ddace-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="ddace-124">sistema de saudação armazena IPs anterior, Latitude / Longitude e ASNs de um usuário e considera esses locais familiares toobe.</span><span class="sxs-lookup"><span data-stu-id="ddace-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="ddace-125">Um local de entrada é considerado familiarizado se hello local de entrada não corresponde a nenhum dos locais familiares existente de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddace-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="ddace-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="ddace-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="ddace-127">tem um período inicial de aprendizado de 14 dias, durante o qual ele não sinaliza nenhum local novo como desconhecido.</span><span class="sxs-lookup"><span data-stu-id="ddace-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="ddace-128">ignora entradas de dispositivos conhecidos e locais geograficamente fechar tooan local existente de familiar.</span><span class="sxs-lookup"><span data-stu-id="ddace-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="ddace-129">toosimulate de locais desconhecidos, você tem toosign em um local e o dispositivo conta Olá não entrou de antes.</span><span class="sxs-lookup"><span data-stu-id="ddace-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="ddace-130">**toosimulate uma entrada de um local desconhecido, executar Olá etapas**:</span><span class="sxs-lookup"><span data-stu-id="ddace-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="ddace-131">Escolha uma conta com um histórico de entrada de, pelo menos, 14 dias.</span><span class="sxs-lookup"><span data-stu-id="ddace-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="ddace-132">Realize uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="ddace-132">Do either:</span></span>
   
   <span data-ttu-id="ddace-133">a.</span><span class="sxs-lookup"><span data-stu-id="ddace-133">a.</span></span> <span data-ttu-id="ddace-134">Durante o uso de uma VPN, navegue muito[https://myapps.microsoft.com](https://myapps.microsoft.com) e digite as credenciais de saudação da conta de Olá você deseja que o evento de risco toosimulate hello para.</span><span class="sxs-lookup"><span data-stu-id="ddace-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="ddace-135">b.</span><span class="sxs-lookup"><span data-stu-id="ddace-135">b.</span></span> <span data-ttu-id="ddace-136">Peça um colega no toosign local diferente usando credenciais da conta da saudação (não recomendadas).</span><span class="sxs-lookup"><span data-stu-id="ddace-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="ddace-137">Olá entrar aparecerão no painel de proteção de identidade Olá em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="ddace-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="ddace-138">Viagem impossível tooatypical local</span><span class="sxs-lookup"><span data-stu-id="ddace-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="ddace-139">Simulando a condição de viagem impossível Olá é difícil porque o algoritmo de saudação usa tooweed de aprendizado de máquina out falsos positivos, como viagem impossível de dispositivos conhecidos ou entradas de VPNs são usadas por outros usuários no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddace-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="ddace-140">Além disso, o algoritmo de saudação exige um histórico de entrada de 3 dias too14 para usuário Olá antes de começar a gerar eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="ddace-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="ddace-141">**toosimulate um local tooatypical viagem impossível executar Olá etapas**:</span><span class="sxs-lookup"><span data-stu-id="ddace-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="ddace-142">Usando o navegador padrão, navegue muito[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ddace-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="ddace-143">Insira as credenciais de saudação da conta de saudação para que você deseja toogenerate um evento de risco de viagem impossível.</span><span class="sxs-lookup"><span data-stu-id="ddace-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="ddace-144">Altere o agente do usuário.</span><span class="sxs-lookup"><span data-stu-id="ddace-144">Change your user agent.</span></span> <span data-ttu-id="ddace-145">É possível alterar o agente do usuário no Internet Explorer nas Ferramentas de Desenvolvedor ou então no Firefox ou Chrome usando um complemento de alternador de agente do usuário.</span><span class="sxs-lookup"><span data-stu-id="ddace-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="ddace-146">Altere seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ddace-146">Change your IP address.</span></span> <span data-ttu-id="ddace-147">É possível alterar seu endereço IP usando uma VPN, um complemento do Tor ou criando um novo computador no Azure em um diferente.</span><span class="sxs-lookup"><span data-stu-id="ddace-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="ddace-148">Entrada muito[https://myapps.microsoft.com](https://myapps.microsoft.com) usando Olá as mesmas credenciais como antes e após alguns minutos depois de entrar anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="ddace-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="ddace-149">Olá entrar aparecerá no painel de proteção de identidade hello dentro de 2 a 4 horas.</span><span class="sxs-lookup"><span data-stu-id="ddace-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="ddace-150">Devido a saudação complexos de aprendizado de máquina modelos envolvidos, há uma possibilidade que ele será não escolhido.</span><span class="sxs-lookup"><span data-stu-id="ddace-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="ddace-151">Você pode querer tooreplicate essas etapas de várias contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddace-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="ddace-152">Simulação de vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="ddace-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="ddace-153">Vulnerabilidades são pontos fracos no seu ambiente do Azure AD que podem ser explorados por um ator maligno.</span><span class="sxs-lookup"><span data-stu-id="ddace-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="ddace-154">Atualmente, três tipos de vulnerabilidades são exibidas no Azure AD Identity Protection que aproveitam os outros recursos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddace-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="ddace-155">Essas vulnerabilidades serão exibidas no painel de proteção de identidade Olá automaticamente depois que esses recursos são configurados.</span><span class="sxs-lookup"><span data-stu-id="ddace-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="ddace-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ddace-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="ddace-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddace-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="ddace-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ddace-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="ddace-159">Risco de comprometimento do usuário</span><span class="sxs-lookup"><span data-stu-id="ddace-159">User compromise risk</span></span>
<span data-ttu-id="ddace-160">**tootest risco de comprometimento do usuário, executar Olá etapas**:</span><span class="sxs-lookup"><span data-stu-id="ddace-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="ddace-161">Entrada muito[https://portal.azure.com](https://portal.azure.com) com credenciais de administrador global para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="ddace-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="ddace-162">Navegue muito**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="ddace-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="ddace-163">Em Olá principal **Azure AD Identity Protection** folha, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="ddace-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="ddace-164">Em Olá **configurações do Portal** folha, em **as regras de segurança**, clique em **o risco de comprometimento do usuário**.</span><span class="sxs-lookup"><span data-stu-id="ddace-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="ddace-165">Em Olá **entrar risco** folha, ativar **Habilitar regra** off e, em seguida, clique em **salvar** configurações.</span><span class="sxs-lookup"><span data-stu-id="ddace-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="ddace-166">Para uma determinada conta de usuário, simule um evento de risco de locais desconhecidos ou IP anônimo.</span><span class="sxs-lookup"><span data-stu-id="ddace-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="ddace-167">Isso será elevar o nível de risco do usuário Olá para esse usuário muito**médio**.</span><span class="sxs-lookup"><span data-stu-id="ddace-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="ddace-168">Aguarde alguns minutos e verifique se o nível do usuário é **Médio**.</span><span class="sxs-lookup"><span data-stu-id="ddace-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="ddace-169">Vá toohello **configurações do Portal** folha.</span><span class="sxs-lookup"><span data-stu-id="ddace-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="ddace-170">Em Olá **o risco de comprometimento do usuário** folha, em **Habilitar regra**, selecione **em** .</span><span class="sxs-lookup"><span data-stu-id="ddace-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="ddace-171">Selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddace-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="ddace-172">a.</span><span class="sxs-lookup"><span data-stu-id="ddace-172">a.</span></span> <span data-ttu-id="ddace-173">tooblock, selecione **médio** em **bloco entrar**.</span><span class="sxs-lookup"><span data-stu-id="ddace-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="ddace-174">b.</span><span class="sxs-lookup"><span data-stu-id="ddace-174">b.</span></span> <span data-ttu-id="ddace-175">alteração de senha segura tooenforce, selecione **médio** em **exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="ddace-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="ddace-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ddace-176">Click **Save**.</span></span>
12. <span data-ttu-id="ddace-177">Agora você pode testar o acesso condicional baseado em risco ao entrar usando um usuário com um nível de risco elevado.</span><span class="sxs-lookup"><span data-stu-id="ddace-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="ddace-178">Se o risco de usuário Olá é médio, dependendo da configuração de saudação de sua política, sua entrada no é a ser bloqueada ou são forçados toochange sua senha.</span><span class="sxs-lookup"><span data-stu-id="ddace-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="ddace-179">
    ![Guia estratégico](./media/active-directory-identityprotection-playbook/201.png "manual")
    </span><span class="sxs-lookup"><span data-stu-id="ddace-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="ddace-180">Risco de entrada</span><span class="sxs-lookup"><span data-stu-id="ddace-180">Sign-in risk</span></span>
<span data-ttu-id="ddace-181">**tootest um sinal de risco, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ddace-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddace-182">Entrada muito[https://portal.azure.com ](https://portal.azure.com) com credenciais de administrador global para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="ddace-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="ddace-183">Navegue muito**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="ddace-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="ddace-184">Em Olá principal **Azure AD Identity Protection** folha, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="ddace-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="ddace-185">Em Olá **configurações do Portal** folha, em **as regras de segurança**, clique em **entrar risco**.</span><span class="sxs-lookup"><span data-stu-id="ddace-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="ddace-186">Em hello * * entrar risco * * folha, selecione **na** em **Habilitar regra**.</span><span class="sxs-lookup"><span data-stu-id="ddace-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="ddace-187">Selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddace-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="ddace-188">a.</span><span class="sxs-lookup"><span data-stu-id="ddace-188">a.</span></span> <span data-ttu-id="ddace-189">tooblock, selecione **médio** em **bloco entrar**</span><span class="sxs-lookup"><span data-stu-id="ddace-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="ddace-190">b.</span><span class="sxs-lookup"><span data-stu-id="ddace-190">b.</span></span> <span data-ttu-id="ddace-191">alteração de senha segura tooenforce, selecione **médio** em **exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="ddace-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="ddace-192">tooblock, selecione média em bloco entrar.</span><span class="sxs-lookup"><span data-stu-id="ddace-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="ddace-193">autenticação de multifator tooenforce, selecione **médio** em **exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="ddace-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="ddace-194">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="ddace-194">Click on **Save**.</span></span>
10. <span data-ttu-id="ddace-195">Agora você pode testar o acesso condicional com base em risco, simulando locais desconhecidos hello ou IP anônimo corre o risco de eventos porque os dois são **médio** eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="ddace-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="ddace-196">![Guia estratégico](./media/active-directory-identityprotection-playbook/200.png "Guia estratégico")</span><span class="sxs-lookup"><span data-stu-id="ddace-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="ddace-197">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ddace-197">See also</span></span>
* [<span data-ttu-id="ddace-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ddace-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

