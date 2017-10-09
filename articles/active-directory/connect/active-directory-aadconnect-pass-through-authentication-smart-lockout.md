---
title: "Azure AD Connect: autenticação de passagem – bloqueio inteligente | Microsoft Docs"
description: "Este artigo descreve como autenticação de passagem do Azure Active Directory (AD do Azure) protege suas contas no local contra ataques de senha de força bruta em nuvem hello."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="dcd1a-104">Autenticação de passagem do Azure Active Directory: bloqueio inteligente</span><span class="sxs-lookup"><span data-stu-id="dcd1a-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="dcd1a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dcd1a-105">Overview</span></span>

<span data-ttu-id="dcd1a-106">O Azure AD protege contra ataques de senha de força bruta e impede que usuários reais sejam impedidos de acessar seus aplicativos de SaaS e do Office 365.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="dcd1a-107">Essa capacidade, chamada **Bloqueio Inteligente**, tem suporte quando você usa a Autenticação de Passagem como seu método de entrada.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="dcd1a-108">Bloqueio inteligente está habilitado por padrão para todos os locatários e está protegendo suas contas de usuário em todo o tempo de saudação; Não há nenhuma necessidade tooturn-la no.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="dcd1a-109">O Bloqueio Inteligente funciona controlando tentativas de logon com falha e, depois de um determinado **Limite de bloqueio**, iniciando uma **Duração de bloqueio**.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="dcd1a-110">As tentativas de entrar de invasor Olá durante a duração do bloqueio de saudação são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="dcd1a-111">Se continuar ataque hello, Olá subsequentes com falha tentativas de entrada após o término do hello duração do bloqueio resultará em mais longas de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="dcd1a-112">padrão de saudação limite de bloqueio é 10 tentativas com falha e o padrão de saudação que duração do bloqueio é 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="dcd1a-113">Bloqueio inteligente também faz distinção entre entradas de usuários originais e contra invasores e bloqueios somente out invasores Olá na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="dcd1a-114">Essa funcionalidade impede que invasores bloqueiem usuários reais de forma mal-intencionada.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="dcd1a-115">Usamos após entrar comportamento, dispositivos dos usuários & navegadores e outros toodistinguish sinais entre usuários original.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="dcd1a-116">Estamos aperfeiçoando constantemente nossos algoritmos.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="dcd1a-117">Como a autenticação de passagem encaminha solicitações de validação de senha para o local do Active Directory (AD), é necessário tooprevent invasores bloqueio de contas de usuários do AD.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="dcd1a-118">Como você tem suas próprias políticas de bloqueio de conta do AD (especificamente, [ **limite de bloqueio de conta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) e [ **políticas de redefinição de contador de bloqueio de conta após** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), é necessário que o limite de bloqueio de tooconfigure do AD do Azure e duração do bloqueio adequadamente valores toofilter ataques na nuvem de saudação antes que elas atinjam suas instalações AD.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="dcd1a-119">Olá bloqueio inteligente recurso está livre e _em_ por padrão para todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="dcd1a-120">No entanto, modificar o limite de bloqueio e a valores de duração do bloqueio usando a API do Graph do AD do Azure precisa de sua licença do locatário toohave pelo menos um AD do Azure Premium P2.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="dcd1a-121">Você não precisa de uma licença Azure AD Premium P2 _por usuário_ recurso de bloqueio inteligente Olá tooget com a autenticação de passagem.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="dcd1a-122">tooensure que os usuários no AD contas locais são protegidas, é necessário tooensure que:</span><span class="sxs-lookup"><span data-stu-id="dcd1a-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="dcd1a-123">O Limite de bloqueio do Azure AD seja _menor_ que o Limite de bloqueio da Conta do AD.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="dcd1a-124">É recomendável que você defina os valores hello, de forma que o limite de bloqueio de conta do AD é pelo menos dois ou três vezes o limite de bloqueio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="dcd1a-125">A Duração de bloqueio do Azure AD (representada em segundos) seja _maior_ que o valor de Redefinir contador de bloqueios de conta após do AD (representado em minutos).</span><span class="sxs-lookup"><span data-stu-id="dcd1a-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="dcd1a-126">Verifique as políticas de bloqueio de conta do AD</span><span class="sxs-lookup"><span data-stu-id="dcd1a-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="dcd1a-127">Use suas políticas de bloqueio de conta do AD de Olá tooverify instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcd1a-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="dcd1a-128">Abra a ferramenta de gerenciamento de diretiva de grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="dcd1a-129">Edite saudação diretiva de grupo é aplicada tooall usuários, por exemplo, Olá diretiva de domínio padrão.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="dcd1a-130">Navegue tooComputer configuração configurações diretivas Conta\diretiva de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="dcd1a-131">Verifique os valores de Limite de bloqueio de conta e Redefinir contador de bloqueios de conta após.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Políticas de bloqueio de conta do AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="dcd1a-133">Use Olá Graph API toomanage valores de bloqueio inteligente do locatário</span><span class="sxs-lookup"><span data-stu-id="dcd1a-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="dcd1a-134">Modificar os valores de Limite de bloqueio e de Duração de bloqueio do Azure AD usando a API do Graph é um recurso do Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="dcd1a-135">Ele também precisa toobe um Administrador Global no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="dcd1a-136">Você pode usar [Gerenciador de gráficos](https://developer.microsoft.com/graph/graph-explorer) tooread, definir e atualizar valores de bloqueio inteligente do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="dcd1a-137">Mas você também pode fazer essas operações de forma programática.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="dcd1a-138">Ler valores de Bloqueio Inteligente</span><span class="sxs-lookup"><span data-stu-id="dcd1a-138">Read Smart Lockout values</span></span>

<span data-ttu-id="dcd1a-139">Siga estas etapas tooread valores de bloqueio inteligente do locatário:</span><span class="sxs-lookup"><span data-stu-id="dcd1a-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="dcd1a-140">Entre no Explorador do Graph como um Administrador Global de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="dcd1a-141">Se solicitado, conceder acesso para Olá permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="dcd1a-142">Clique em "Modificar permissões" e selecione a permissão de "Directory.ReadWrite.All" hello.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="dcd1a-143">Configure a solicitação de API do Graph Olá da seguinte maneira: versão do conjunto de muito "BETA", tipo de solicitação muito "GET" e a URL muito`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="dcd1a-144">Clique em "Executar consulta" toosee valores de bloqueio inteligente do locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="dcd1a-145">Se não tiver configurado os valores de seu locatário antes, você verá um conjunto vazio.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="dcd1a-146">Definir valores de Bloqueio Inteligente</span><span class="sxs-lookup"><span data-stu-id="dcd1a-146">Set Smart Lockout values</span></span>

<span data-ttu-id="dcd1a-147">Siga estas etapas tooset valores de bloqueio inteligente do locatário (para Olá apenas na primeira vez):</span><span class="sxs-lookup"><span data-stu-id="dcd1a-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="dcd1a-148">Entre no Explorador do Graph como um Administrador Global de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="dcd1a-149">Se solicitado, conceder acesso para Olá permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="dcd1a-150">Clique em "Modificar permissões" e selecione a permissão de "Directory.ReadWrite.All" hello.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="dcd1a-151">Configure a solicitação de API do Graph Olá da seguinte maneira: versão do conjunto de muito "BETA", tipo de solicitação muito "POST" e a URL muito`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="dcd1a-152">Copie e cole Olá solicitação JSON a seguir no campo de "Corpo da solicitação" hello.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="dcd1a-153">Alterar valores de bloqueio inteligente Olá conforme apropriado e use um GUID aleatório para `templateId`.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="dcd1a-154">Clique em "Executar consulta" tooset valores de bloqueio inteligente do locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="dcd1a-155">Se você não estiver usando-los, você pode deixar Olá **BannedPasswordList** e **EnableBannedPasswordCheck** valores como vazio ("") e "false" respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="dcd1a-156">Verifique se você definiu os valores do Bloqueio Inteligente de seu locatário corretamente usando [estas etapas](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="dcd1a-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="dcd1a-157">Atualizar valores de Bloqueio Inteligente</span><span class="sxs-lookup"><span data-stu-id="dcd1a-157">Update Smart Lockout values</span></span>

<span data-ttu-id="dcd1a-158">Siga essas etapas tooupdate valores de bloqueio inteligente do locatário (se você já tiver configurado antes):</span><span class="sxs-lookup"><span data-stu-id="dcd1a-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="dcd1a-159">Entre no Explorador do Graph como um Administrador Global de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="dcd1a-160">Se solicitado, conceder acesso para Olá permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="dcd1a-161">Clique em "Modificar permissões" e selecione a permissão de "Directory.ReadWrite.All" hello.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="dcd1a-162">[Siga estas etapas tooread valores de bloqueio inteligente do locatário](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="dcd1a-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="dcd1a-163">Saudação de cópia `id` valor (uma GUID) do item de saudação com "displayName" como "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="dcd1a-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="dcd1a-164">Configure a solicitação de API do Graph Olá da seguinte maneira: definir versão muito "BETA", tipo de solicitação muito "PATCH" e a URL muito`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -usar Olá GUID da etapa 3 para `<id>`.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="dcd1a-165">Copie e cole Olá solicitação JSON a seguir no campo de "Corpo da solicitação" hello.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="dcd1a-166">Altere os valores de bloqueio inteligente Olá conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="dcd1a-167">Clique em "Executar consulta" tooupdate valores de bloqueio inteligente do locatário.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="dcd1a-168">Verifique se você atualizou os valores do Bloqueio Inteligente de seu locatário corretamente usando [estas etapas](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="dcd1a-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcd1a-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dcd1a-169">Next steps</span></span>
- <span data-ttu-id="dcd1a-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="dcd1a-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
