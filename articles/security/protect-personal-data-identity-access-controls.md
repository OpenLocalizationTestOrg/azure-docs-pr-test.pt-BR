---
title: Proteger dados pessoais com controles de acesso e identidade do Azure | Microsoft Docs
description: Usando os controles de acesso e identidade do Azure para ajudar a proteger dados pessoais
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
ms.openlocfilehash: b43754efd207679dbe08710f44f56454a5fd20ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="fb4c3-103">Azure Active Directory e Autenticação Multifator: proteger dados pessoais com controles de acesso e identidade</span><span class="sxs-lookup"><span data-stu-id="fb4c3-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="fb4c3-104">Este artigo fornece informações e procedimentos que podem ser usados para proteger dados pessoais, usando os serviços e recursos de segurança do Azure Active Directory e da Autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-104">This article provides information and procedures you can use to protect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="fb4c3-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="fb4c3-105">Scenario</span></span>

<span data-ttu-id="fb4c3-106">Uma empresa de cruzeiro de grande porte, com sede nos Estados Unidos, está expandindo suas operações para oferecer roteiros nos mares Mediterrâneo, Adriático e Báltico, bem como nas Ilhas Britânicas.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="fb4c3-107">Para dar suporte a esses esforços, ela adquiriu várias linhas de cruzeiro menores localizadas na Itália, na Alemanha, na Dinamarca e no Reino Unido.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-107">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="fb4c3-108">A empresa usa o Microsoft Azure para armazenar dados corporativos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="fb4c3-109">Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="fb4c3-110">Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="fb4c3-111">A linha de cruzeiro também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que inclui informações pessoais para acompanhamento das relações com os clientes atuais e anteriores.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-111">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="fb4c3-112">Os funcionários corporativos acessam a rede de escritórios remotos da empresa e os agentes de viagem localizados no mundo todo têm acesso a alguns recursos da empresa.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-112">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="fb4c3-113">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="fb4c3-113">Problem statement</span></span>

<span data-ttu-id="fb4c3-114">A empresa deve proteger a privacidade dos dados pessoais de clientes e funcionários contra invasores que buscam usar as identidades comprometidas para obter acesso.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-114">The company must protect the privacy of customers’ and employees’ personal data from attackers seeking to use compromised identities to gain access.</span></span> <span data-ttu-id="fb4c3-115">Ela também deve garantir que o acesso aos dados pessoais por usuários legítimos seja restrito somente àqueles que precisam deles para realizar seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-115">They also must ensure that access to personal data by legitimate users is restricted to only those who need it to do their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="fb4c3-116">Meta da empresa</span><span class="sxs-lookup"><span data-stu-id="fb4c3-116">Company goal</span></span>

<span data-ttu-id="fb4c3-117">A meta da empresa é garantir que o acesso a dados pessoais seja estritamente controlado.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-117">The company’s goal is to ensure that access to personal data is strictly controlled.</span></span> <span data-ttu-id="fb4c3-118">É essencial que as identidades de usuários com acesso a dados pessoais sejam protegidas pela autenticação forte.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-118">It is essential that identities of users with access to personal data be protected by strong authentication.</span></span> <span data-ttu-id="fb4c3-119">Uma política de [privilégio mínimo] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) deve ser imposta, de modo que os usuários legítimos tenham apenas o nível de acesso necessário e nada mais.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only the level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="fb4c3-120">Soluções</span><span class="sxs-lookup"><span data-stu-id="fb4c3-120">Solutions</span></span>

<span data-ttu-id="fb4c3-121">O Microsoft Azure fornece ferramentas de gerenciamento de identidade e acesso para ajudar as empresas a controlar quem tem acesso aos recursos que contêm dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-121">Microsoft Azure provides identity and access management tools to help companies control who has access to resources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="fb4c3-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb4c3-122">Azure Active Directory</span></span>

<span data-ttu-id="fb4c3-123">O [AAD](https://docs.microsoft.com/azure/active-directory/) (Azure Active Directory) gerencia identidades e controla o acesso ao Azure, bem como outros recursos locais e outros recursos, dados e aplicativos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access to Azure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="fb4c3-124">O [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ajuda os administradores do Azure a minimizar o número de pessoas que têm acesso a determinadas informações como dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators to minimize the number of people who have access to certain information such as personal data.</span></span> <span data-ttu-id="fb4c3-125">Ele permite que eles descubram, restrinjam e monitorem identidades com privilégios e seu acesso a recursos, além de atribuir direitos administrativos JIT (Just-In-Time) temporários aos usuários qualificados.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-125">It enables them to discover, restrict, and monitor privileged identities and their access to resources, and to assign temporary, Just-In-Time (JIT) administrative rights to eligible users.</span></span> <span data-ttu-id="fb4c3-126">Também fornece informações sobre aqueles que têm privilégios administrativos do AAD.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="fb4c3-127">As atividades envolvidas no uso do AAD PIM incluem:</span><span class="sxs-lookup"><span data-stu-id="fb4c3-127">The activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="fb4c3-128">Habilitar o Privileged Identity Management no diretório</span><span class="sxs-lookup"><span data-stu-id="fb4c3-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="fb4c3-129">Usar o painel de administração do Privileged Identity Management para ver informações importantes rapidamente</span><span class="sxs-lookup"><span data-stu-id="fb4c3-129">Using Privileged Identity Management admin dashboard to see important information at a glance</span></span>

- <span data-ttu-id="fb4c3-130">Gerenciar as identidades com privilégios (administradores) adicionando ou removendo os administradores permanentes ou qualificados para cada função</span><span class="sxs-lookup"><span data-stu-id="fb4c3-130">Managing the privileged identities (administrators) by adding or removing permanent or eligible administrators to each role</span></span>

- <span data-ttu-id="fb4c3-131">Definir as configurações de ativação de função</span><span class="sxs-lookup"><span data-stu-id="fb4c3-131">Configuring the role activation settings</span></span>

- <span data-ttu-id="fb4c3-132">Ativar funções</span><span class="sxs-lookup"><span data-stu-id="fb4c3-132">Activating roles</span></span>

- <span data-ttu-id="fb4c3-133">Examinar a atividade de função</span><span class="sxs-lookup"><span data-stu-id="fb4c3-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="fb4c3-134">Como fazer para habilitar o AAD PIM?</span><span class="sxs-lookup"><span data-stu-id="fb4c3-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="fb4c3-135">Para começar a usar o PIM no diretório, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fb4c3-135">To start using PIM for your directory, do the following:</span></span>

1. <span data-ttu-id="fb4c3-136">Entre no portal do Azure como administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-136">Sign in to the Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="fb4c3-137">Se sua organização tiver mais de um diretório, selecione seu nome de usuário no canto superior direito do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-137">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="fb4c3-138">Selecione o diretório em que você usará o Privileged Identity Management do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-138">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="fb4c3-139">Selecione **Mais serviços** e use a caixa de texto **Filtrar** para pesquisar o Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-139">Select **More services** and use the **Filter** textbox to search for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="fb4c3-140">Marque **Fixar no painel** e então clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-140">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="fb4c3-141">O aplicativo Privileged Identity Management é aberto.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-141">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="fb4c3-142">Depois que o Azure AD Privileged Identity Management estiver configurado, você verá a folha de navegação sempre que abrir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-142">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="fb4c3-143">Para obter mais informações e instruções sobre como começar a usar o AAD PIM, consulte [Começar a usar o Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="fb4c3-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="fb4c3-144">Controle de Acesso Baseado em Função do Azure</span><span class="sxs-lookup"><span data-stu-id="fb4c3-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="fb4c3-145">O [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (Controle de Acesso Baseado em Função do Azure) ajuda os administradores do Azure a gerenciar o acesso aos recursos do Azure, permitindo a concessão de acesso de acordo com a função atribuída do usuário.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access to Azure resources by enabling the granting of access based on the user’s assigned role.</span></span> <span data-ttu-id="fb4c3-146">Segregue as tarefas dentro de uma equipe e conceda somente a quantidade de acesso que os usuários, os grupos e os aplicativos precisam para realizar seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-146">You can segregate duties within a team and grant only the amount of access to users, groups and applications that they need to perform their jobs.</span></span>

<span data-ttu-id="fb4c3-147">O acesso baseado em função pode ser concedido aos usuários que usam o portal do Azure, as ferramentas de Linha de Comando do Azure ou as APIs de Gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-147">Role-based access can be granted to users using the Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="fb4c3-148">Para obter mais informações sobre os conceitos básicos do RBAC do Azure, consulte [Introdução ao Controle de Acesso Baseado em Função no Portal do Azure](https://docs.microsoft.com/active-directory/role-based-access-control-what-is).</span><span class="sxs-lookup"><span data-stu-id="fb4c3-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in the Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="fb4c3-149">Como fazer para gerenciar o RBAC do Azure com o PowerShell?</span><span class="sxs-lookup"><span data-stu-id="fb4c3-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="fb4c3-150">Use os cmdlets do PowerShell para gerenciar o RBAC do Azure, incluindo as seguintes tarefas de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="fb4c3-150">You can use PowerShell cmdlets to manage Azure RBAC, including the following management tasks:</span></span>

- <span data-ttu-id="fb4c3-151">Listar funções</span><span class="sxs-lookup"><span data-stu-id="fb4c3-151">List roles</span></span>

- <span data-ttu-id="fb4c3-152">Veja quem tem acesso</span><span class="sxs-lookup"><span data-stu-id="fb4c3-152">See who has access</span></span>

- <span data-ttu-id="fb4c3-153">Conceder acesso</span><span class="sxs-lookup"><span data-stu-id="fb4c3-153">Grant access</span></span>

- <span data-ttu-id="fb4c3-154">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="fb4c3-154">Remove access</span></span>

- <span data-ttu-id="fb4c3-155">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="fb4c3-155">Create a custom role</span></span>

- <span data-ttu-id="fb4c3-156">Obter ações para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="fb4c3-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="fb4c3-157">Modificar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="fb4c3-157">Modify a custom role</span></span>

- <span data-ttu-id="fb4c3-158">Excluir uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="fb4c3-158">Delete a custom role</span></span>

- <span data-ttu-id="fb4c3-159">Listar funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="fb4c3-159">List custom roles</span></span>

<span data-ttu-id="fb4c3-160">Para obter instruções sobre como gerenciar o RBAC do Azure com o PowerShell, consulte [Gerenciar o Acesso Baseado em Função com o Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="fb4c3-160">For instructions on how to manage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="fb4c3-161">Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="fb4c3-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="fb4c3-162">O [Azure MFA](https://docs.microsoft.com/azure/multi-factor-authentication/) (Autenticação Multifator do Azure) é uma solução de verificação em duas etapas que ajuda a proteger o acesso a dados e aplicativos, enquanto atende às exigências do usuário por um processo de conexão simples.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access to data and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="fb4c3-163">Ele fornece autenticação forte por meio de uma variedade de métodos de verificação, incluindo chamada telefônica, mensagem de texto ou verificação de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="fb4c3-164">Para implantar o MFA na nuvem do Azure, você precisa habilitá-lo primeiro e, em seguida, ativar a verificação em duas etapas para os usuários.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-164">To deploy MFA in the Azure cloud, you need to first enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-to-use-mfa"></a><span data-ttu-id="fb4c3-165">Como fazer para habilitar o Azure a usar o MFA?</span><span class="sxs-lookup"><span data-stu-id="fb4c3-165">How do I enable Azure to use MFA?</span></span>

<span data-ttu-id="fb4c3-166">Se os usuários tiverem licenças que incluem a Autenticação Multifator do Azure, nada precisará ser feito para ativar o MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="fb4c3-167">Caso contrário, você precisará criar um provedor de Autenticação Multifator no diretório.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-167">If not, you need to create a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="fb4c3-168">Para fazer isso, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fb4c3-168">To do this, follow these steps:</span></span>

1. <span data-ttu-id="fb4c3-169">Selecione **Active Directory** no portal clássico do Azure (conectado como administrador).</span><span class="sxs-lookup"><span data-stu-id="fb4c3-169">Select **Active Directory** in the Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="fb4c3-170">Selecione **Provedores de Autenticação Multifator.**</span><span class="sxs-lookup"><span data-stu-id="fb4c3-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="fb4c3-171">Selecione **Novo** e, em seguida, em **Serviços de Aplicativos**, selecione **Provedor de Autenticação Multifator.**</span><span class="sxs-lookup"><span data-stu-id="fb4c3-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="fb4c3-172">Selecione **Criação Rápida.**</span><span class="sxs-lookup"><span data-stu-id="fb4c3-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="fb4c3-173">Preencha o campo de nome e selecione um modelo de uso (por autenticação ou por usuário habilitado).</span><span class="sxs-lookup"><span data-stu-id="fb4c3-173">Fill in the name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="fb4c3-174">Designe um diretório ao qual o Provedor de MFA está associado.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-174">Designate a directory with which the MFA Provider is associated.</span></span>

7. <span data-ttu-id="fb4c3-175">Selecione o botão **Criar** .</span><span class="sxs-lookup"><span data-stu-id="fb4c3-175">Click the **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="fb4c3-176">Para obter mais instruções sobre como gerenciar o Provedor de Autenticação Multifator, consulte [Introdução a um Provedor de Autenticação Multifator do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="fb4c3-176">For more instructions on how to manage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="fb4c3-177">Como fazer para ativar a verificação em duas etapas para os usuários?</span><span class="sxs-lookup"><span data-stu-id="fb4c3-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="fb4c3-178">Imponha a verificação em duas etapas para todas as entradas ou crie políticas de acesso condicional para exigir uma verificação em duas etapas somente quando condições específicas forem aplicáveis.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="fb4c3-179">A habilitação do MFA do Azure com a alteração de estados do usuário é a abordagem tradicional para exigir a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-179">Enabling Azure MFA by changing user states is the traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="fb4c3-180">Todos os usuários habilitados terão o mesmo requisito de executar a verificação em duas etapas sempre que se conectarem.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-180">All the users that you enable will have the same requirement to perform two-step verification every time they sign in.</span></span> <span data-ttu-id="fb4c3-181">A habilitação de um usuário substitui qualquer política de acesso condicional que possa afetar esse usuário.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="fb4c3-182">A habilitação do MFA do Azure com uma política de acesso condicional é uma abordagem mais flexível para exigir a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="fb4c3-183">Você pode criar políticas de acesso condicional que se aplicam a grupos, bem como a usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-183">You can create conditional access policies that apply to groups as well as individual users.</span></span> <span data-ttu-id="fb4c3-184">Grupos de alto risco podem receber mais restrições do que grupos de baixo risco, ou a verificação em duas etapas pode ser exigida apenas para aplicativos de nuvem de alto risco e ignorada para os de baixo risco.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="fb4c3-185">No entanto, o acesso condicional um recurso pago do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="fb4c3-186">Para habilitar o MFA alterando o estado do usuário, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fb4c3-186">To enable MFA by changing user state, do the following:</span></span>

1. <span data-ttu-id="fb4c3-187">Entre no portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-187">Sign in to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="fb4c3-188">Acesse **Azure Active Directory \> Usuários e grupos \> Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-188">Go to **Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="fb4c3-189">Selecione **Autenticação Multifator**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="fb4c3-190">Localize o usuário que você deseja habilitar para a MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-190">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="fb4c3-191">Talvez seja necessário alterar o modo de exibição na parte superior.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-191">You may need to change the view at the top.</span></span>
5. <span data-ttu-id="fb4c3-192">Marque a caixa ao lado do nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-192">Check the box next to the user’s name.</span></span>
6. <span data-ttu-id="fb4c3-193">À direita, em etapas rápidas, escolha **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-193">On the right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="fb4c3-194">Confirme sua seleção na janela pop-up que é aberta.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-194">Confirm your selection in the pop-up window that opens.</span></span>  <span data-ttu-id="fb4c3-195">Os usuários para os quais o MFA foi habilitado deverão se registrar na próxima vez que se conectarem.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-195">Users for whom MFA has been enabled will be asked to register the next time they sign in.</span></span>

<span data-ttu-id="fb4c3-196">Para habilitar o MFA do Azure com uma política de acesso condicional, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fb4c3-196">To enable Azure MFA with a conditional access policy, do the following:</span></span>

1. <span data-ttu-id="fb4c3-197">Entre no portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-197">Sign in to the Azure portal as an administrator.</span></span>

2. <span data-ttu-id="fb4c3-198">Acesse **Azure Active Directory \> Acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-198">Go to **Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="fb4c3-199">Selecione **Nova política**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-199">Select **New policy**.</span></span>

4. <span data-ttu-id="fb4c3-200">Em **Atribuições**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="fb4c3-201">Use as guias **Incluir** e **Excluir** para especificar quais usuários e grupos serão gerenciados pela política.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-201">Use the **Include** and     **Exclude** tabs to specify which users and groups will be managed by the policy.</span></span>

5. <span data-ttu-id="fb4c3-202">Em **Atribuições**, selecione **Aplicativos de nuvem.**</span><span class="sxs-lookup"><span data-stu-id="fb4c3-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="fb4c3-203">Opte por **incluir Todos os aplicativos de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-203">Choose to **include All cloud apps**.</span></span>
6.  <span data-ttu-id="fb4c3-204">Em **Controles de acesso**, selecione **Grant**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="fb4c3-205">Escolha **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="fb4c3-206">Alterne **Habilitar política** para **Ativado** e selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fb4c3-206">Turn **Enable policy** to **On** and then select **Save**.</span></span>

<span data-ttu-id="fb4c3-207">Para obter informações sobre como definir as configurações do MFA do Azure para configurar alertas de fraudes, criar um bypass avulso, usar mensagens de voz personalizadas, configurar o cache, especificar IPs confiáveis, criar senhas de aplicativo, habilitar o reconhecimento do MFA de dispositivos de confiança para os usuários e selecionar métodos de verificação, consulte [Definir as configurações da Autenticação Multifator do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="fb4c3-207">For information on how to configure Azure MFA settings to set up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb4c3-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb4c3-208">Next steps</span></span>

- [<span data-ttu-id="fb4c3-209">Protegendo o acesso privilegiado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb4c3-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="fb4c3-210">Perguntas frequentes sobre a Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="fb4c3-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="fb4c3-211">Solução de problemas do Controle de Acesso Baseado em Função</span><span class="sxs-lookup"><span data-stu-id="fb4c3-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="fb4c3-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="fb4c3-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
