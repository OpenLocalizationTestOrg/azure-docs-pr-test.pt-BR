---
title: 'Perguntas frequentes: SSPR do Azure AD | Microsoft Docs'
description: "Perguntas frequentes sobre o autoatendimento de redefinição de senha do Azure AD"
services: active-directory
keywords: "Gerenciamento de senhas do Active Directory, gerenciamento de senhas, autoatendimento de redefinição de senha do Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="8fea3-104">Perguntas frequentes sobre gerenciamento de senhas</span><span class="sxs-lookup"><span data-stu-id="8fea3-104">Password management frequently asked questions</span></span>

<span data-ttu-id="8fea3-105">Olá a seguir está algumas perguntas frequentes para tudo relacionado toopassword redefinir.</span><span class="sxs-lookup"><span data-stu-id="8fea3-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="8fea3-106">Se você tiver uma pergunta geral sobre o Azure AD e a senha de autoatendimento redefinição, que não foi respondida aqui, solicite comunidade Olá para obter assistência no hello [fóruns do Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="8fea3-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="8fea3-107">Membros da comunidade Olá incluem engenheiros, gerentes de produto, MVPs e colega profissionais de TI.</span><span class="sxs-lookup"><span data-stu-id="8fea3-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="8fea3-108">Perguntas Frequentes é dividido em Olá seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="8fea3-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="8fea3-109">**Perguntas sobre o registro de redefinição de senha**</span><span class="sxs-lookup"><span data-stu-id="8fea3-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="8fea3-110">**Perguntas sobre a redefinição de senha**</span><span class="sxs-lookup"><span data-stu-id="8fea3-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="8fea3-111">**Perguntas sobre alteração de senha**</span><span class="sxs-lookup"><span data-stu-id="8fea3-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="8fea3-112">**Perguntas sobre relatórios de gerenciamento de senha**</span><span class="sxs-lookup"><span data-stu-id="8fea3-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="8fea3-113">**Perguntas sobre o write-back de senha**</span><span class="sxs-lookup"><span data-stu-id="8fea3-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="8fea3-114">Registro de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="8fea3-114">Password reset registration</span></span>
* <span data-ttu-id="8fea3-115">**P: meus usuários podem registrar seus próprios dados de redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="8fea3-116">**R:** Sim, contanto que a redefinição de senha está habilitada e eles sejam licenciados, eles podem ir toohello portal de registro de redefinição de senha em http://aka.ms/ssprsetup tooregister suas informações de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8fea3-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="8fea3-117">Os usuários também podem registrar pelo painel de acesso vai toohello em http://myapps.microsoft.com, clicando em Guia do perfil hello e Olá registrar para a opção de redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="8fea3-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="8fea3-118">**P: posso definir dados de redefinição de senha em nome dos meus usuários?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="8fea3-119">**R:** Sim, você pode fazer isso com o Azure AD Connect, PowerShell, Olá [portal do Azure](https://portal.azure.com), ou o portal de administração do Office de hello.</span><span class="sxs-lookup"><span data-stu-id="8fea3-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="8fea3-120">Para obter mais informações, consulte o artigo Olá [dados usados pelo Azure AD autoatendimento de redefinição de senha](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="8fea3-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="8fea3-121">**P: posso sincronizar dados de perguntas de segurança do local?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="8fea3-122">**R:** isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="8fea3-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="8fea3-123">**P: meus usuários podem registrar dados de forma que outros usuários não possam ver esses dados?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="8fea3-124">**R:** Sim, quando os usuários registram dados usando Olá Portal redefinição de senha registro é salvo em campos de autenticação particulares que só são visíveis pelo usuário de administradores globais e hello.</span><span class="sxs-lookup"><span data-stu-id="8fea3-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="8fea3-125">Se um **conta de administrador do Azure** registra o número de telefone de autenticação ele também é preenchido no campo de telefone celular hello e é visível.</span><span class="sxs-lookup"><span data-stu-id="8fea3-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="8fea3-126">**P: meus usuários tem toobe registrado antes que eles podem usar a redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="8fea3-127">**R:** não, se você definir informações de autenticação suficientes em seu nome, os usuários não têm tooregister.</span><span class="sxs-lookup"><span data-stu-id="8fea3-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="8fea3-128">A redefinição de senha funciona enquanto você formatou corretamente os dados armazenados nos campos apropriados de saudação no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="8fea3-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="8fea3-129">**P: posso sincronizar ou definir campos de telefone de autenticação, Email de autenticação ou telefone de autenticação alternativo Olá em nome de meus usuários?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="8fea3-130">**R:** isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="8fea3-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="8fea3-131">**P: como portal de registro Olá sabe quais opções tooshow meus usuários?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="8fea3-132">**R:** portal de registro de redefinição de senha Olá somente mostra Olá opções que você habilitou para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="8fea3-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="8fea3-133">Essas opções são encontradas na seção de política de redefinição de senha de usuário da guia Configurar do diretório de saudação. Por exemplo, isso significa que se você não habilitar a perguntas de segurança, em seguida, os usuários não são tooregister possível para essa opção.</span><span class="sxs-lookup"><span data-stu-id="8fea3-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="8fea3-134">**P: quando um usuário é considerado registrado?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="8fea3-135">**R:** um usuário é considerado registrado para SSPR quando eles foram registrados pelo menos Olá **número de tooreset necessários métodos** que você definiu no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fea3-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="8fea3-136">Redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="8fea3-136">Password reset</span></span>
* <span data-ttu-id="8fea3-137">**P: quanto tempo deve esperar tooreceive um email, SMS ou chamada telefônica da redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="8fea3-138">**R:** Email, mensagens SMS e chamadas telefônicas devem chegar em menos de um minuto, com o caso comum hello, sendo 5 a 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="8fea3-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="8fea3-139">Se você não recebe a notificação de saudação nesse período de tempo:</span><span class="sxs-lookup"><span data-stu-id="8fea3-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="8fea3-140">Verifique a pasta Lixo Eletrônico.</span><span class="sxs-lookup"><span data-stu-id="8fea3-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="8fea3-141">Verifique o número de saudação ou email que está sendo contatado é hello um esperado.</span><span class="sxs-lookup"><span data-stu-id="8fea3-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="8fea3-142">Verifique se os dados de autenticação Olá no diretório hello estão formatados corretamente.</span><span class="sxs-lookup"><span data-stu-id="8fea3-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="8fea3-143">Exemplo: “+1 4255551234” ou “user@contoso.com”</span><span class="sxs-lookup"><span data-stu-id="8fea3-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="8fea3-144">**P: quais idiomas são compatíveis com a redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="8fea3-145">**R:** Olá IU de redefinição de senha, mensagens SMS e voz chamadas são localizadas no hello mesmos idiomas que têm suporte no Office 365.</span><span class="sxs-lookup"><span data-stu-id="8fea3-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="8fea3-146">**Guia Configurar do p: quais partes da experiência de redefinição de senha Olá obtenham marcadas quando defino organizacional de identidade visual no meu diretório?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="8fea3-147">**R:** Olá portal de redefinição de senha mostra o logotipo da sua organização e permite que você tooconfigure Olá entre em contato com seu email personalizado do administrador link toopoint tooa ou URL.</span><span class="sxs-lookup"><span data-stu-id="8fea3-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="8fea3-148">Nenhum email que é enviado pela redefinição de senha inclui o logotipo da sua organização, cores, o nome no corpo de saudação do email Olá e personalizadas a partir do nome.</span><span class="sxs-lookup"><span data-stu-id="8fea3-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="8fea3-149">**P: como eu posso instruir meus usuários sobre onde toogo tooreset suas senhas?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="8fea3-150">**R:** toohttps://passwordreset.microsoftonline.com seus usuários podem ser enviados diretamente ou instruir Olá tooclick **não é possível acessar o link de conta** encontrado em qualquer página entrar ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="8fea3-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="8fea3-151">Você também pode publicar esses links no lugar tooyour facilmente acessível aos usuários.</span><span class="sxs-lookup"><span data-stu-id="8fea3-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="8fea3-152">**P: posso usar essa página em um dispositivo móvel?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="8fea3-153">**R:** sim, essa página funciona em dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="8fea3-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="8fea3-154">**P: há suporte para desbloqueio das contas locais do active directory quando os usuários redefinirem as suas senhas?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="8fea3-155">**R:** Sim. Quando um usuário redefine a senha e o write-back de senha foi implantado usando o Azure AD Connect, a conta desse usuário é desbloqueada automaticamente quando ele redefine a senha.</span><span class="sxs-lookup"><span data-stu-id="8fea3-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="8fea3-156">**P: como posso integrar a redefinição de senha diretamente à experiência de entrada na área de trabalho do usuário?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="8fea3-157">**R:** se você for um cliente do Azure AD Premium, você pode instalar o Microsoft Identity Manager sem nenhum custo adicional e implantar Olá local senha redefinição solução toomeet esse requisito.</span><span class="sxs-lookup"><span data-stu-id="8fea3-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="8fea3-158">**P: posso definir perguntas de segurança diferentes para diferentes localidades?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="8fea3-159">**R:** isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="8fea3-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="8fea3-160">**P: quantas perguntas podemos configurar opção de autenticação de perguntas de segurança Olá?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="8fea3-161">**R:** você pode configurar as perguntas de segurança personalizada too20 em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fea3-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="8fea3-162">**P: qual o tamanho máximo das perguntas de segurança?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="8fea3-163">**R:** as perguntas de segurança podem ter entre 3 e 200 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8fea3-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="8fea3-164">**P: quanto tempo podem ter as respostas toosecurity perguntas?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="8fea3-165">**R:** respostas podem ser 3 too40 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8fea3-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="8fea3-166">**P: são rejeitadas respostas duplicadas toosecurity perguntas?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="8fea3-167">**R:** Sim, rejeitamos respostas duplicadas toosecurity perguntas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="8fea3-168">**P: maio um registro de usuário Olá mesma pergunta de segurança mais de uma vez?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="8fea3-169">**R:** Não. Quando um usuário registra uma pergunta específica, ele não pode se registrar nessa pergunta uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="8fea3-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="8fea3-170">**P: é possível tooset um limite mínimo de perguntas de segurança para registro e redefinição?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="8fea3-171">**R:** sim, um limite pode ser definido para o registro e outro para a redefinição.</span><span class="sxs-lookup"><span data-stu-id="8fea3-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="8fea3-172">Podem ser necessárias de três a cinco perguntas de segurança para o registro e de três a cinco perguntas para a redefinição.</span><span class="sxs-lookup"><span data-stu-id="8fea3-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="8fea3-173">**P: se um usuário tiver registrado mais do que o número máximo de saudação de tooreset necessário de perguntas, como perguntas de segurança são selecionadas durante a redefinição?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="8fea3-174">**R:** segurança N perguntas são selecionadas aleatoriamente sem o número total de saudação de perguntas que um usuário tiver registrado, onde N é hello **número de tooreset necessário perguntas**.</span><span class="sxs-lookup"><span data-stu-id="8fea3-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="8fea3-175">Por exemplo, se um usuário tiver 5 perguntas de segurança registradas, mas apenas 3 são necessário tooreset, 3 de saudação 5 são selecionado aleatoriamente e apresentadas na reinicialização.</span><span class="sxs-lookup"><span data-stu-id="8fea3-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="8fea3-176">Se o usuário Olá obtém respostas Olá toohello perguntas errado, o processo de seleção de saudação ocorrer tooprevent hammering da pergunta.</span><span class="sxs-lookup"><span data-stu-id="8fea3-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="8fea3-177">**P: vocês impedem os usuários de tentar redefinir a senha várias vezes em um curto período de tempo?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="8fea3-178">**R:** Sim, há recursos de segurança incorporados tooprotect de redefinição de senha de uso indevido.</span><span class="sxs-lookup"><span data-stu-id="8fea3-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="8fea3-179">Os usuários têm somente cinco tentativas de redefinição de senha em uma mesma hora antes de serem bloqueados por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="8fea3-180">Os usuários somente podem experimentar toovalidate um número de telefone 5 vezes dentro de uma hora antes do bloqueio por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="8fea3-181">Os usuários somente podem experimentar um único método de autenticação cinco vezes em uma mesma hora antes de serem bloqueados por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="8fea3-182">**P: por quanto tempo são email hello e a senha de uso único de SMS válido?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="8fea3-183">**R:** Olá a duração da sessão para redefinição de senha é 105 minutos.</span><span class="sxs-lookup"><span data-stu-id="8fea3-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="8fea3-184">Operação de redefinição de senha do início de saudação do hello, usuário Olá tem 105 minutos tooreset sua senha.</span><span class="sxs-lookup"><span data-stu-id="8fea3-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="8fea3-185">Hello email e senha de uso único de SMS são inválidos depois que esse período de tempo expira.</span><span class="sxs-lookup"><span data-stu-id="8fea3-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="8fea3-186">Alteração de senha</span><span class="sxs-lookup"><span data-stu-id="8fea3-186">Password change</span></span>
* <span data-ttu-id="8fea3-187">**P: onde meus usuários deveríamos toochange suas senhas?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="8fea3-188">**R:** os usuários podem alterar suas senhas em qualquer lugar, eles verão sua imagem do perfil ou ícone (como no canto superior direito de saudação do seu [Office 365](https://portal.office.com) ou [painel de acesso](https://myapps.microsoft.com) experiências.</span><span class="sxs-lookup"><span data-stu-id="8fea3-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="8fea3-189">Os usuários podem alterar suas senhas da saudação [página de perfil do painel de acesso](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="8fea3-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="8fea3-190">Os usuários também podem ser solicitado toochange suas senhas automaticamente na tela de entrada hello AD do Azure se suas senhas expiradas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="8fea3-191">Por fim, os usuários podem navegar toohello [Portal de alteração de senha do AD do Azure](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) diretamente se desejarem toochange suas senhas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="8fea3-192">**P: meus usuários notificados no Portal do Office de hello quando sua senha local expira?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="8fea3-193">**R:** hoje isso é possível se você estiver usando o AD FS, seguindo as instruções de saudação aqui: [enviar declarações de política de senha com o ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="8fea3-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="8fea3-194">Se você está usando a sincronização de hash de senha, isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="8fea3-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="8fea3-195">Isso é porque nós não sincronizar as políticas de senha local, portanto, não é possível para que possamos experiências toopost toocloud de notificações de expiração.</span><span class="sxs-lookup"><span data-stu-id="8fea3-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="8fea3-196">Em ambos os casos, também é possível muito[notificar os usuários cujas senhas estão sobre tooexpire usando PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fea3-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="8fea3-197">Relatórios de gerenciamento de senha</span><span class="sxs-lookup"><span data-stu-id="8fea3-197">Password management reports</span></span>
* <span data-ttu-id="8fea3-198">**P: quanto tempo leva para tooshow dados backup nos relatórios de gerenciamento de senha Olá?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="8fea3-199">**R:** dados devem ser exibidos nos relatórios de gerenciamento de senha hello dentro de 5 a 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="8fea3-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="8fea3-200">Ele algumas instâncias pode levar até tooan tooappear de hora.</span><span class="sxs-lookup"><span data-stu-id="8fea3-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="8fea3-201">**P: como posso filtrar Olá relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="8fea3-202">**R:** você pode filtrar relatórios de gerenciamento de senha Olá clicando Olá Lupa pequena toohello direita dos rótulos de coluna hello, superior de saudação do relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="8fea3-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="8fea3-203">Se você quiser toodo de filtragem mais avançada, você pode baixar Olá relatório tooexcel-lo e criar uma tabela dinâmica.</span><span class="sxs-lookup"><span data-stu-id="8fea3-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="8fea3-204">**P: qual é o número máximo de saudação de eventos são armazenados nos relatórios de gerenciamento de senha Olá?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="8fea3-205">**R:** backup too75, 000 senha senha ou redefinição redefinição registro eventos são armazenados nos relatórios de gerenciamento de senha hello, abrangendo backup too30 dias.</span><span class="sxs-lookup"><span data-stu-id="8fea3-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="8fea3-206">Estamos trabalhando tooexpand esse número tooinclude mais eventos.</span><span class="sxs-lookup"><span data-stu-id="8fea3-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="8fea3-207">**P: quanto vão Olá relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="8fea3-208">**R:** relatórios de gerenciamento de senha Olá Mostrar operações que ocorrem dentro Olá últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="8fea3-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="8fea3-209">Por enquanto, se você precisar tooarchive dos dados, você pode baixar relatórios de saudação periodicamente e salvá-los em um local separado.</span><span class="sxs-lookup"><span data-stu-id="8fea3-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="8fea3-210">**P: há um número máximo de linhas que podem ser exibidas nos relatórios de gerenciamento de senha Olá?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="8fea3-211">**R:** Sim, um máximo de 75.000 linhas pode aparecer em qualquer um dos relatórios de gerenciamento de senha hello, se elas estão sendo mostradas no hello interface do usuário ou que estão sendo baixadas.</span><span class="sxs-lookup"><span data-stu-id="8fea3-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="8fea3-212">**P: há uma API tooaccess Olá senha redefinição ou registro de dados de relatório?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="8fea3-213">**R:** Sim, consulte Olá toolearn documentação a seguir como você pode acessar a senha Olá redefinir o fluxo de dados de relatório.</span><span class="sxs-lookup"><span data-stu-id="8fea3-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="8fea3-214">[Saiba como tooaccess de redefinição de senha relatar eventos programaticamente](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="8fea3-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="8fea3-215">Write-back de senha</span><span class="sxs-lookup"><span data-stu-id="8fea3-215">Password writeback</span></span>
* <span data-ttu-id="8fea3-216">**P: como funciona em segundo plano de saudação do Write-back de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="8fea3-217">**R:** consulte [como funciona o write-back de senha](active-directory-passwords-writeback.md) para obter uma explicação sobre o que acontece quando você habilita o write-back de senha e como os dados fluem pelo sistema Olá volta para seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="8fea3-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="8fea3-218">**P: quanto tempo o write-back de senha leva toowork?  Há um atraso de sincronização como com a sincronização com hash de senha?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="8fea3-219">**R:** o write-back de senha é instantâneo.</span><span class="sxs-lookup"><span data-stu-id="8fea3-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="8fea3-220">É um pipeline síncrono que funciona de forma essencialmente diferente da sincronização com hash de senha.</span><span class="sxs-lookup"><span data-stu-id="8fea3-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="8fea3-221">Write-back de senha permite aos usuários tooget de comentários em tempo real sobre o êxito de saudação de sua senha redefinir ou alterar a operação.</span><span class="sxs-lookup"><span data-stu-id="8fea3-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="8fea3-222">tempo médio de saudação para um write-back bem-sucedido de uma senha é em 500 ms.</span><span class="sxs-lookup"><span data-stu-id="8fea3-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="8fea3-223">**P: Se minha conta local estiver desabilitada, como minha conta ou meu acesso na nuvem será afetado?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="8fea3-224">**R:** se sua ID de local estiver desabilitada, sua nuvem de ID/acesso também será desabilitado no próximo intervalo de sincronização Olá via conexão AAD byt padrão isso é a cada 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="8fea3-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="8fea3-225">**P: se a minha conta local é restrito por uma política de senha do Active Directory local, SSPR obedece a essa política ao alterar senha Olá?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="8fea3-226">**R:** Sim, SSPR depende e age de acordo com hello a política de senha do AD, incluindo a política de senha de domínio de AD típica, bem como as políticas de senha refinada definido tooa dado de usuário de destino no local.</span><span class="sxs-lookup"><span data-stu-id="8fea3-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="8fea3-227">**P: o write-back de senha funciona com quais tipos de conta?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="8fea3-228">**R:** O write-back de senha funciona com usuários Federados e Sincronizados com Hash de Senha.</span><span class="sxs-lookup"><span data-stu-id="8fea3-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="8fea3-229">**P: o write-back de senha impõe as políticas de senha do meu domínio?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="8fea3-230">**R:** Sim, o write-back de senha impõe a duração, o histórico e a complexidade da senha, filtros e qualquer outra restrição que você possa impor nas senhas no domínio local.</span><span class="sxs-lookup"><span data-stu-id="8fea3-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="8fea3-231">**P: o write-back de senha é seguro?  Como posso ter certeza de que não serei invadido por um hacker?**</span><span class="sxs-lookup"><span data-stu-id="8fea3-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="8fea3-232">**R:** Sim, o write-back de senha é seguro.</span><span class="sxs-lookup"><span data-stu-id="8fea3-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="8fea3-233">tooread mais informações sobre camadas Olá quatro de segurança implementado pelo serviço de write-back de senha Olá, confira o hello [modelo de segurança de write-back de senha](active-directory-passwords-writeback.md#password-writeback-security-model) seção como funciona o write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="8fea3-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="8fea3-234">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fea3-234">Next steps</span></span>

<span data-ttu-id="8fea3-235">Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8fea3-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8fea3-236">[**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fea3-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8fea3-237">[**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fea3-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="8fea3-238">[**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha</span><span class="sxs-lookup"><span data-stu-id="8fea3-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="8fea3-239">[**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui</span><span class="sxs-lookup"><span data-stu-id="8fea3-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="8fea3-240">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.</span><span class="sxs-lookup"><span data-stu-id="8fea3-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="8fea3-241">[**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR</span><span class="sxs-lookup"><span data-stu-id="8fea3-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8fea3-242">[**Política**](active-directory-passwords-policy.md) – entenda e defina políticas de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fea3-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="8fea3-243">[**Write-back de senha** ](active-directory-passwords-writeback.md) - Como o write-back de senha opera com o seu diretório local</span><span class="sxs-lookup"><span data-stu-id="8fea3-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="8fea3-244">[**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona</span><span class="sxs-lookup"><span data-stu-id="8fea3-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="8fea3-245">[**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR</span><span class="sxs-lookup"><span data-stu-id="8fea3-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
