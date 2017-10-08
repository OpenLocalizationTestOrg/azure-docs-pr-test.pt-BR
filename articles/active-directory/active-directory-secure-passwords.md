---
title: "aaaAzure AD em camadas de segurança de senha | Microsoft Docs"
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
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="73dfb-103">Uma abordagem várias camadas de segurança de senha de tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="73dfb-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="73dfb-104">Este artigo discute algumas práticas recomendadas que você pode seguir como um usuário ou como um administrador tooprotect seu Azure Active Directory (AD do Azure) ou Account da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="73dfb-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="73dfb-105">Administradores do AD do Azure podem redefinir senhas de usuário usando diretrizes Olá Olá artigo [Olá redefinição da senha de um usuário no Active Directory do Azure](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73dfb-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="73dfb-106">Os usuários podem redefinir suas próprias senhas usando diretrizes Olá Olá artigo [ajuda esqueci minha senha do AD do Azure](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="73dfb-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="73dfb-107">Requisitos de senha</span><span class="sxs-lookup"><span data-stu-id="73dfb-107">Password requirements</span></span>

<span data-ttu-id="73dfb-108">O AD do Azure incorpora Olá senhas comuns de toosecuring abordagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="73dfb-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="73dfb-109">Requisitos de comprimento de senha</span><span class="sxs-lookup"><span data-stu-id="73dfb-109">Password length requirements</span></span>
* <span data-ttu-id="73dfb-110">Requisitos de complexidade de senha</span><span class="sxs-lookup"><span data-stu-id="73dfb-110">Password complexity requirements</span></span>
* <span data-ttu-id="73dfb-111">Expiração de senha regular e periódica</span><span class="sxs-lookup"><span data-stu-id="73dfb-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="73dfb-112">Para obter informações sobre a redefinição de senha no Active Directory do Azure, consulte o tópico de saudação [senha de autoatendimento do AD do Azure Redefinir para Olá profissionais de TI](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="73dfb-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="73dfb-113">Proteções de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="73dfb-113">Azure AD password protections</span></span>

<span data-ttu-id="73dfb-114">O AD do Azure e Olá usar o sistema de conta Microsoft comprovados abordagens tooensure segura proteção de senhas de usuário e administrador incluindo:</span><span class="sxs-lookup"><span data-stu-id="73dfb-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="73dfb-115">Senhas banidas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="73dfb-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="73dfb-116">Bloqueio de Senha Inteligente</span><span class="sxs-lookup"><span data-stu-id="73dfb-116">Smart Password Lockout</span></span>

<span data-ttu-id="73dfb-117">Para obter informações sobre o gerenciamento de senha com base na pesquisa atual, consulte o white paper de saudação [diretrizes de senha](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="73dfb-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="73dfb-118">Senhas banidas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="73dfb-118">Dynamically banned passwords</span></span>

<span data-ttu-id="73dfb-119">As Contas da Microsoft e do Azure AD garantem a proteção por senha banindo dinamicamente as senhas comumente usadas.</span><span class="sxs-lookup"><span data-stu-id="73dfb-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="73dfb-120">equipe de proteção de identidade do Azure ID Olá analisa rotineiramente senha banido listas, impedindo que os usuários selecionem as senhas usadas.</span><span class="sxs-lookup"><span data-stu-id="73dfb-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="73dfb-121">Este serviço está disponível tooAzure AD e os clientes do serviço de conta Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="73dfb-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="73dfb-122">Durante a criação de senhas, é importante para os administradores tooencourage usuários toochoose senha frases que incluem uma combinação exclusiva de letras, números, caracteres ou palavras.</span><span class="sxs-lookup"><span data-stu-id="73dfb-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="73dfb-123">Essa abordagem ajuda toomake toobe praticamente impossível comprometido mas mais fácil para os usuários tooremember as senhas de usuário.</span><span class="sxs-lookup"><span data-stu-id="73dfb-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="73dfb-124">Violações de senha</span><span class="sxs-lookup"><span data-stu-id="73dfb-124">Password breaches</span></span>

<span data-ttu-id="73dfb-125">Sempre, a Microsoft está trabalhando toostay um passo à frente de criminosos.</span><span class="sxs-lookup"><span data-stu-id="73dfb-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="73dfb-126">equipe do Azure AD Identity Protection Olá continuamente analisa as senhas que são normalmente usadas.</span><span class="sxs-lookup"><span data-stu-id="73dfb-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="73dfb-127">Criminosos também usam semelhante tooinform de estratégias seus ataques, como criando um [tabela arco-íris](https://en.wikipedia.org/wiki/Rainbow_table) de violação de hashes de senha.</span><span class="sxs-lookup"><span data-stu-id="73dfb-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="73dfb-128">A Microsoft continuamente analisa [violações de dados](https://www.privacyrights.org/data-breaches) toomaintain uma lista de senha banido dinamicamente atualizada, o que garante que as senhas vulneráveis são proibidas antes de se tornarem um real de ameaças tooAzure AD clientes.</span><span class="sxs-lookup"><span data-stu-id="73dfb-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="73dfb-129">Para obter mais informações sobre nossos esforços de segurança atual, consulte Olá [relatório de inteligência de segurança do Microsoft](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="73dfb-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="73dfb-130">Bloqueio de Senha Inteligente</span><span class="sxs-lookup"><span data-stu-id="73dfb-130">Smart Password Lockout</span></span>

<span data-ttu-id="73dfb-131">Quando o AD do Azure detecta um potencial toohack de tentar criminoso virtuais em uma senha de usuário, podemos bloquear a conta de usuário de Olá com bloqueio de senha inteligente.</span><span class="sxs-lookup"><span data-stu-id="73dfb-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="73dfb-132">O AD do Azure é projetado risco de saudação toodetermine associado a sessões de logon específico.</span><span class="sxs-lookup"><span data-stu-id="73dfb-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="73dfb-133">Em seguida, usando dados de segurança mais recentes de saudação, aplicamos bloqueio semântica toostop ameaças.</span><span class="sxs-lookup"><span data-stu-id="73dfb-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="73dfb-134">Se um usuário estiver bloqueado do AD do Azure, sua tela parece semelhante toohello que segue:</span><span class="sxs-lookup"><span data-stu-id="73dfb-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Bloqueado no Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="73dfb-136">Para outras contas da Microsoft, sua tela parece semelhante toohello que segue:</span><span class="sxs-lookup"><span data-stu-id="73dfb-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Bloqueado em uma conta da Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="73dfb-138">Para obter informações sobre a redefinição de senha no Active Directory do Azure, consulte o tópico de saudação [senha de autoatendimento do AD do Azure Redefinir para Olá profissionais de TI](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="73dfb-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="73dfb-139">Se você for um administrador do AD do Azure, talvez você queira toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid com os usuários crie senhas tradicionais completamente.</span><span class="sxs-lookup"><span data-stu-id="73dfb-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="73dfb-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73dfb-140">Next steps</span></span>

* [<span data-ttu-id="73dfb-141">Como tooupdate sua própria senha</span><span class="sxs-lookup"><span data-stu-id="73dfb-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="73dfb-142">conceitos básicos de saudação do gerenciamento de identidades do Azure</span><span class="sxs-lookup"><span data-stu-id="73dfb-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="73dfb-143">Relatório de atividade de registro de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="73dfb-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


