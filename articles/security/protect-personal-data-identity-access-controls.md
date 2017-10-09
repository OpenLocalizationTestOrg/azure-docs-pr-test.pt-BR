---
title: dados pessoais de aaaProtect com controles de acesso e identidade do Azure | Microsoft Docs
description: "Usando toohelp de controles de acesso e identidade do Azure que você proteja seus dados pessoais"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="84d89-103">Azure Active Directory e Autenticação Multifator: proteger dados pessoais com controles de acesso e identidade</span><span class="sxs-lookup"><span data-stu-id="84d89-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="84d89-104">Este artigo fornece informações e procedimentos que você pode usar dados pessoais de tooprotect usando os serviços e recursos de segurança do Active Directory do Azure e multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="84d89-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="84d89-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="84d89-105">Scenario</span></span>

<span data-ttu-id="84d89-106">Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas.</span><span class="sxs-lookup"><span data-stu-id="84d89-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="84d89-107">toosupport os esforços adquiriu várias linhas de cruzeiro menores na Itália, Alemanha, Dinamarca e hello UK</span><span class="sxs-lookup"><span data-stu-id="84d89-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="84d89-108">empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="84d89-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="84d89-109">Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes.</span><span class="sxs-lookup"><span data-stu-id="84d89-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="84d89-110">Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="84d89-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="84d89-111">linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.</span><span class="sxs-lookup"><span data-stu-id="84d89-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="84d89-112">Os funcionários corporativos acesso Olá rede da empresa Olá escritórios remotos e agentes espalhados Olá, mundo têm acesso toosome recursos da empresa.</span><span class="sxs-lookup"><span data-stu-id="84d89-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="84d89-113">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="84d89-113">Problem statement</span></span>

<span data-ttu-id="84d89-114">empresa Olá deve proteger a privacidade de saudação dos dados pessoais dos funcionários e clientes contra invasores que buscam toouse comprometido identidades toogain acesso.</span><span class="sxs-lookup"><span data-stu-id="84d89-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="84d89-115">Eles também devem garantir que toopersonal de acesso a dados por usuários legítimos é restrito a somente aqueles que precisam de toodo seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="84d89-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="84d89-116">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="84d89-116">Company goal</span></span>

<span data-ttu-id="84d89-117">a meta da empresa Olá é tooensure que acessam dados toopersonal é estritamente controlada.</span><span class="sxs-lookup"><span data-stu-id="84d89-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="84d89-118">É essencial que as identidades de usuários com dados do access toopersonal ser protegidas por autenticação forte.</span><span class="sxs-lookup"><span data-stu-id="84d89-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="84d89-119">Uma política de [privilégio mínimo] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) devem ser impostas para que os usuários legítimos único nível de saudação de acesso necessário e nada mais.</span><span class="sxs-lookup"><span data-stu-id="84d89-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="84d89-120">Soluções</span><span class="sxs-lookup"><span data-stu-id="84d89-120">Solutions</span></span>

<span data-ttu-id="84d89-121">Microsoft Azure fornece ferramentas de gerenciamento de identidade e acesso toohelp empresas controlar acesso tooresources que contêm dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="84d89-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="84d89-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84d89-122">Azure Active Directory</span></span>

<span data-ttu-id="84d89-123">[Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/) (AAD) gerencia identidades e controla o acesso tooAzure bem como outros locais e outros recursos de nuvem, dados e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="84d89-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="84d89-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ajuda os administradores do Azure toominimize Olá várias pessoas têm acesso toocertain informações como dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="84d89-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="84d89-125">Ele permite toodiscover, restringir e monitorar seus tooresources e tooassign temporário, Just-in-(JIT) direitos administrativos tooeligible usuários de acesso e de identidades com privilégios.</span><span class="sxs-lookup"><span data-stu-id="84d89-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="84d89-126">Também fornece informações sobre aqueles que têm privilégios administrativos do AAD.</span><span class="sxs-lookup"><span data-stu-id="84d89-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="84d89-127">atividades de saudação envolvidas usando AAD PIM incluem:</span><span class="sxs-lookup"><span data-stu-id="84d89-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="84d89-128">Habilitar o Privileged Identity Management no diretório</span><span class="sxs-lookup"><span data-stu-id="84d89-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="84d89-129">Usando informações importantes do Privileged Identity Management admin painel toosee em um relance</span><span class="sxs-lookup"><span data-stu-id="84d89-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="84d89-130">Gerenciamento de identidades com privilégios de saudação (administradores) adicionando ou removendo a função de tooeach administradores permanentes ou qualificados</span><span class="sxs-lookup"><span data-stu-id="84d89-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="84d89-131">Definindo configurações de ativação de função hello</span><span class="sxs-lookup"><span data-stu-id="84d89-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="84d89-132">Ativar funções</span><span class="sxs-lookup"><span data-stu-id="84d89-132">Activating roles</span></span>

- <span data-ttu-id="84d89-133">Examinar a atividade de função</span><span class="sxs-lookup"><span data-stu-id="84d89-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="84d89-134">Como fazer para habilitar o AAD PIM?</span><span class="sxs-lookup"><span data-stu-id="84d89-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="84d89-135">toostart usando PIM para seu diretório, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="84d89-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="84d89-136">Entre em toohello portal do Azure como um administrador global do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="84d89-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="84d89-137">Se sua organização tiver mais de um diretório, selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84d89-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="84d89-138">Selecione o diretório de saudação onde você usará o Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="84d89-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="84d89-139">Selecione **mais serviços** e usar Olá **filtro** toosearch da caixa de texto para o Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="84d89-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="84d89-140">Verificar **Pin toodashboard** e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="84d89-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="84d89-141">Olá aplicativo Privileged Identity Management é aberto.</span><span class="sxs-lookup"><span data-stu-id="84d89-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="84d89-142">Depois de configurar o Azure AD Privileged Identity Management, você verá blade de navegação Olá sempre que você abrir o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="84d89-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="84d89-143">Para obter mais informações e instruções sobre como começar a usar o AAD PIM, consulte [Começar a usar o Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="84d89-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="84d89-144">Controle de Acesso Baseado em Função do Azure</span><span class="sxs-lookup"><span data-stu-id="84d89-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="84d89-145">[Controle de acesso baseado em função do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ajuda a administradores do Azure gerenciar acesso tooAzure recursos habilitando o Olá concessão de acesso baseado em função do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="84d89-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="84d89-146">Você pode separar tarefas dentro de uma equipe e conceder apenas Olá total acesso toousers, grupos e aplicativos que precisam tooperform seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="84d89-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="84d89-147">Acesso baseado em função pode ser concedido toousers usando Olá portal do Azure, as ferramentas de linha de comando do Azure ou APIs de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="84d89-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="84d89-148">Para obter mais informações sobre aspectos básicos de RBAC do Azure, consulte [começar com controle de acesso baseado em função no hello Portal do Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="84d89-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="84d89-149">Como fazer para gerenciar o RBAC do Azure com o PowerShell?</span><span class="sxs-lookup"><span data-stu-id="84d89-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="84d89-150">Você pode usar os cmdlets de PowerShell toomanage RBAC do Azure, incluindo Olá tarefas de gerenciamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="84d89-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="84d89-151">Listar funções</span><span class="sxs-lookup"><span data-stu-id="84d89-151">List roles</span></span>

- <span data-ttu-id="84d89-152">Veja quem tem acesso</span><span class="sxs-lookup"><span data-stu-id="84d89-152">See who has access</span></span>

- <span data-ttu-id="84d89-153">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="84d89-153">Grant access</span></span>

- <span data-ttu-id="84d89-154">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="84d89-154">Remove access</span></span>

- <span data-ttu-id="84d89-155">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="84d89-155">Create a custom role</span></span>

- <span data-ttu-id="84d89-156">Obter ações para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="84d89-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="84d89-157">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="84d89-157">Modify a custom role</span></span>

- <span data-ttu-id="84d89-158">Excluir uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="84d89-158">Delete a custom role</span></span>

- <span data-ttu-id="84d89-159">Listar funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="84d89-159">List custom roles</span></span>

<span data-ttu-id="84d89-160">Para obter instruções sobre como toomanage RBAC do Azure com o PowerShell, consulte [acesso baseado em função gerenciar com o Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="84d89-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="84d89-161">Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="84d89-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="84d89-162">[Autenticação multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) é uma solução de verificação de duas etapas que ajuda a proteger acesso toodata e aplicativos, enquanto atende a demanda do usuário para um processo de logon simple.</span><span class="sxs-lookup"><span data-stu-id="84d89-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="84d89-163">Ele fornece autenticação forte por meio de uma variedade de métodos de verificação, incluindo chamada telefônica, mensagem de texto ou verificação de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="84d89-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="84d89-164">toodeploy MFA Olá nuvem do Azure, você precisa toofirst habilitá-lo e, em seguida, ativar a verificação em duas etapas para os usuários.</span><span class="sxs-lookup"><span data-stu-id="84d89-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="84d89-165">Como habilitar o Azure toouse MFA?</span><span class="sxs-lookup"><span data-stu-id="84d89-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="84d89-166">Se os usuários tiverem licenças que incluem autenticação multifator do Azure, não há nada que você precisa tooturn toodo no Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="84d89-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="84d89-167">Caso contrário, você precisa toocreate um provedor de multi-Factor Auth em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="84d89-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="84d89-168">toodo isso, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="84d89-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="84d89-169">Selecione **do Active Directory** em Olá portal clássico do Azure (conectado como administrador).</span><span class="sxs-lookup"><span data-stu-id="84d89-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="84d89-170">Selecione **Provedores de Autenticação Multifator.**</span><span class="sxs-lookup"><span data-stu-id="84d89-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="84d89-171">Selecione **Novo** e, em seguida, em **Serviços de Aplicativos**, selecione **Provedor de Autenticação Multifator.**</span><span class="sxs-lookup"><span data-stu-id="84d89-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="84d89-172">Selecione **Criação Rápida.**</span><span class="sxs-lookup"><span data-stu-id="84d89-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="84d89-173">Preencha o campo de nome hello e selecione um modelo de uso (por autenticação ou por usuário habilitado).</span><span class="sxs-lookup"><span data-stu-id="84d89-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="84d89-174">Designa um diretório ao qual Olá provedor MFA está associado.</span><span class="sxs-lookup"><span data-stu-id="84d89-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="84d89-175">Clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="84d89-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="84d89-176">Para obter mais instruções sobre como toomanage seu provedor de autenticação multifator, consulte [guia de Introdução com um provedor de autenticação multifator do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="84d89-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="84d89-177">Como fazer para ativar a verificação em duas etapas para os usuários?</span><span class="sxs-lookup"><span data-stu-id="84d89-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="84d89-178">Você pode impor a verificação em duas etapas para todas as entradas ou você pode criar a verificação de duas etapas de toorequire de políticas de acesso condicional somente quando condições específicas.</span><span class="sxs-lookup"><span data-stu-id="84d89-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="84d89-179">Habilitar o Azure MFA alterando estados do usuário é a abordagem tradicional Olá para exigir a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="84d89-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="84d89-180">Todos os usuários de saudação que permitem que você terá Olá verificacao do mesmo requisito tooperform toda vez que entrar.</span><span class="sxs-lookup"><span data-stu-id="84d89-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="84d89-181">A habilitação de um usuário substitui qualquer política de acesso condicional que possa afetar esse usuário.</span><span class="sxs-lookup"><span data-stu-id="84d89-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="84d89-182">A habilitação do MFA do Azure com uma política de acesso condicional é uma abordagem mais flexível para exigir a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="84d89-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="84d89-183">Você pode criar políticas de acesso condicional que se aplicam a toogroups, bem como para usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="84d89-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="84d89-184">Grupos de alto risco podem receber mais restrições do que grupos de baixo risco, ou a verificação em duas etapas pode ser exigida apenas para aplicativos de nuvem de alto risco e ignorada para os de baixo risco.</span><span class="sxs-lookup"><span data-stu-id="84d89-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="84d89-185">No entanto, o acesso condicional um recurso pago do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84d89-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="84d89-186">tooenable MFA por meio da alteração de estado do usuário, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="84d89-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="84d89-187">Entre toohello portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="84d89-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="84d89-188">Vá muito**Active Directory do Azure \> usuários e grupos \> todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="84d89-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="84d89-189">Selecione **Autenticação Multifator**.</span><span class="sxs-lookup"><span data-stu-id="84d89-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="84d89-190">Localizar Olá usuário que você deseja tooenable para o Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="84d89-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="84d89-191">Talvez seja necessário toochange Olá exibição na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="84d89-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="84d89-192">Verifique o nome da saudação caixa próxima toohello do usuário.</span><span class="sxs-lookup"><span data-stu-id="84d89-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="84d89-193">Olá à direita, em etapas rápidas, escolha **habilitar**.</span><span class="sxs-lookup"><span data-stu-id="84d89-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="84d89-194">Confirme sua seleção na janela pop-up de saudação que é aberta.</span><span class="sxs-lookup"><span data-stu-id="84d89-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="84d89-195">Os usuários para quem o MFA tiver sido habilitado deverá Olá tooregister próxima vez que entrar.</span><span class="sxs-lookup"><span data-stu-id="84d89-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="84d89-196">tooenable MFA do Azure com uma política de acesso condicional, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="84d89-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="84d89-197">Entre toohello portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="84d89-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="84d89-198">Vá muito**Active Directory do Azure \> acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="84d89-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="84d89-199">Selecione **Nova política**.</span><span class="sxs-lookup"><span data-stu-id="84d89-199">Select **New policy**.</span></span>

4. <span data-ttu-id="84d89-200">Em **Atribuições**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="84d89-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="84d89-201">Saudação de uso **incluir** e **excluir** guias toospecify quais usuários e grupos que será gerenciado pela política de saudação.</span><span class="sxs-lookup"><span data-stu-id="84d89-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="84d89-202">Em **Atribuições**, selecione **Aplicativos de nuvem.**</span><span class="sxs-lookup"><span data-stu-id="84d89-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="84d89-203">Escolha muito**incluem todos os aplicativos de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="84d89-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="84d89-204">Em **Controles de acesso**, selecione **Grant**.</span><span class="sxs-lookup"><span data-stu-id="84d89-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="84d89-205">Escolha **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="84d89-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="84d89-206">Ativar **habilitar política** muito**na** e, em seguida, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="84d89-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="84d89-207">Para obter informações sobre como tooconfigure Azure MFA configurações tooset os alertas de fraude, criar um bypass avulso, usar mensagens de voz personalizadas, configurar o cache, especifique IPs confiáveis, criar senhas de aplicativo, habilitar a MFA para dispositivos que os usuários de confiança e selecione lembrar-se métodos de verificação, consulte [definir configurações de autenticação de multifator do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="84d89-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="84d89-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84d89-208">Next steps</span></span>

- [<span data-ttu-id="84d89-209">Protegendo o acesso privilegiado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d89-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="84d89-210">Perguntas frequentes sobre a Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="84d89-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="84d89-211">Solução de problemas do Controle de Acesso Baseado em Função</span><span class="sxs-lookup"><span data-stu-id="84d89-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="84d89-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="84d89-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
