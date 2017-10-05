---
title: "Segurança de senha em camadas do Azure AD | Microsoft Docs"
description: "Explica como o Azure AD impõe senhas fortes e protege as senhas dos usuários contra os cibercriminosos."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="1ccda-103">Uma abordagem de várias camadas à segurança de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ccda-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="1ccda-104">Este artigo discute algumas práticas recomendadas que você pode seguir como um usuário ou como um administrador para proteger sua Conta da Microsoft ou do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1ccda-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="1ccda-105">Os administradores do Azure AD podem redefinir senhas de usuário usando as diretrizes neste artigo [Redefinir a senha de um usuário no Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1ccda-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="1ccda-106">Os usuários podem redefinir suas próprias senhas usando as diretrizes no artigo [Ajuda de Esqueci minha senha do Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="1ccda-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="1ccda-107">Requisitos de senha</span><span class="sxs-lookup"><span data-stu-id="1ccda-107">Password requirements</span></span>

<span data-ttu-id="1ccda-108">O Azure AD inclui as seguintes abordagens comuns para proteger senhas:</span><span class="sxs-lookup"><span data-stu-id="1ccda-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="1ccda-109">Requisitos de comprimento de senha</span><span class="sxs-lookup"><span data-stu-id="1ccda-109">Password length requirements</span></span>
* <span data-ttu-id="1ccda-110">Requisitos de complexidade de senha</span><span class="sxs-lookup"><span data-stu-id="1ccda-110">Password complexity requirements</span></span>
* <span data-ttu-id="1ccda-111">Expiração de senha regular e periódica</span><span class="sxs-lookup"><span data-stu-id="1ccda-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="1ccda-112">Para obter informações sobre a redefinição de senha no Azure Active Directory, consulte o tópico [Azure AD self-service password reset for the IT professional](active-directory-passwords.md) (Redefinição de senha de autoatendimento do Azure AD para o profissional de TI).</span><span class="sxs-lookup"><span data-stu-id="1ccda-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="1ccda-113">Proteções de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ccda-113">Azure AD password protections</span></span>

<span data-ttu-id="1ccda-114">O Azure AD e o Sistema de Contas da Microsoft usam abordagens comprovadas do setor para assegurar a proteção segura de senhas de usuário e administrador, incluindo:</span><span class="sxs-lookup"><span data-stu-id="1ccda-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="1ccda-115">Senhas banidas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="1ccda-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="1ccda-116">Bloqueio de Senha Inteligente</span><span class="sxs-lookup"><span data-stu-id="1ccda-116">Smart Password Lockout</span></span>

<span data-ttu-id="1ccda-117">Para obter informações sobre o gerenciamento de senha com base na pesquisa atual, confira o white paper [Password Guidance](http://aka.ms/passwordguidance) (Diretrizes de senha).</span><span class="sxs-lookup"><span data-stu-id="1ccda-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="1ccda-118">Senhas banidas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="1ccda-118">Dynamically banned passwords</span></span>

<span data-ttu-id="1ccda-119">As Contas da Microsoft e do Azure AD garantem a proteção por senha banindo dinamicamente as senhas comumente usadas.</span><span class="sxs-lookup"><span data-stu-id="1ccda-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="1ccda-120">A equipe de Proteção de Identidade do Azure ID analisa rotineiramente as listas de senhas proibidas, impedindo que os usuários selecionem senhas usadas comumente.</span><span class="sxs-lookup"><span data-stu-id="1ccda-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="1ccda-121">Este serviço está disponível para o Azure AD e os clientes do serviço de Conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1ccda-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="1ccda-122">Durante a criação de senhas, é importante que os administradores incentivem os usuários a escolher frases de senha que incluam uma combinação exclusiva de letras, números, caracteres ou palavras.</span><span class="sxs-lookup"><span data-stu-id="1ccda-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="1ccda-123">Essa abordagem ajuda a tornar as senhas de usuário praticamente impossíveis de serem comprometidas, mas mais fáceis de serem lembradas pelos usuários.</span><span class="sxs-lookup"><span data-stu-id="1ccda-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="1ccda-124">Violações de senha</span><span class="sxs-lookup"><span data-stu-id="1ccda-124">Password breaches</span></span>

<span data-ttu-id="1ccda-125">A Microsoft está sempre trabalhando para se manter um passo à frente dos cibercriminosos.</span><span class="sxs-lookup"><span data-stu-id="1ccda-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="1ccda-126">A equipe do Azure AD Identity Protection analisa continuamente as senhas que são usadas comumente.</span><span class="sxs-lookup"><span data-stu-id="1ccda-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="1ccda-127">Os cibercriminosos também usam estratégias semelhantes para preparar seus ataques, como criar uma [tabela rainbow](https://en.wikipedia.org/wiki/Rainbow_table) de violação de hashes de senha.</span><span class="sxs-lookup"><span data-stu-id="1ccda-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="1ccda-128">A Microsoft analisa continuamente as [violações de dados](https://www.privacyrights.org/data-breaches) para manter uma lista de senhas banidas atualizada dinamicamente, que garante que as senhas vulneráveis sejam banidas antes de se tornarem realmente uma ameaça para os clientes do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ccda-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="1ccda-129">Para obter mais informações sobre nossas iniciativas de segurança atuais, confira o [Relatório de inteligência de segurança da Microsoft](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ccda-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="1ccda-130">Bloqueio de Senha Inteligente</span><span class="sxs-lookup"><span data-stu-id="1ccda-130">Smart Password Lockout</span></span>

<span data-ttu-id="1ccda-131">Quando o Azure AD detecta que um cibercriminoso potencial está tentando invadir uma senha de usuário, bloqueamos a conta de usuário com o Bloqueio de Senha Inteligente.</span><span class="sxs-lookup"><span data-stu-id="1ccda-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="1ccda-132">O Azure AD foi projetado para determinar o risco associado a sessões de logon específico.</span><span class="sxs-lookup"><span data-stu-id="1ccda-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="1ccda-133">Usando os dados de segurança mais recentes, aplicamos semântica de bloqueio para parar ameaças cibernéticas.</span><span class="sxs-lookup"><span data-stu-id="1ccda-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="1ccda-134">Se um usuário estiver bloqueado do Azure AD, a tela será semelhante à abaixo:</span><span class="sxs-lookup"><span data-stu-id="1ccda-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Bloqueado no Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="1ccda-136">Para outras contas da Microsoft, a tela é semelhante à abaixo:</span><span class="sxs-lookup"><span data-stu-id="1ccda-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Bloqueado em uma conta da Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="1ccda-138">Para obter informações sobre a redefinição de senha no Azure Active Directory, consulte o tópico [Azure AD self-service password reset for the IT professional](active-directory-passwords.md) (Redefinição de senha de autoatendimento do Azure AD para o profissional de TI).</span><span class="sxs-lookup"><span data-stu-id="1ccda-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="1ccda-139">Se você é administrador do Azure AD, convém usar o [Windows Hello](https://www.microsoft.com/windows/windows-hello) para evitar que os usuários criem senhas tradicionais.</span><span class="sxs-lookup"><span data-stu-id="1ccda-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="1ccda-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ccda-140">Next steps</span></span>

* [<span data-ttu-id="1ccda-141">Como atualizar sua própria senha</span><span class="sxs-lookup"><span data-stu-id="1ccda-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="1ccda-142">Os fundamentos do gerenciamento de identidades do Azure</span><span class="sxs-lookup"><span data-stu-id="1ccda-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="1ccda-143">Relatório de atividade de registro de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="1ccda-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


