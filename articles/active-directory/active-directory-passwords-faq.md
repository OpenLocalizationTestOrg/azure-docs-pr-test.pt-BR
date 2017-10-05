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
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="b5128-104">Perguntas frequentes sobre gerenciamento de senhas</span><span class="sxs-lookup"><span data-stu-id="b5128-104">Password management frequently asked questions</span></span>

<span data-ttu-id="b5128-105">Veja abaixo algumas perguntas frequentes sobre tudo relativo à redefinição de senhas.</span><span class="sxs-lookup"><span data-stu-id="b5128-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="b5128-106">Caso você tenha uma pergunta geral sobre o Azure AD e o autoatendimento de redefinição de senha que não foi respondida aqui, peça ajuda à comunidade nos [fóruns do Azure AD](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="b5128-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="b5128-107">Os membros da comunidade incluem Engenheiros, Gerentes de Produto, MVPs e colegas Profissionais de TI.</span><span class="sxs-lookup"><span data-stu-id="b5128-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="b5128-108">Esta seção de perguntas frequentes é dividida nas seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="b5128-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="b5128-109">**Perguntas sobre o registro de redefinição de senha**</span><span class="sxs-lookup"><span data-stu-id="b5128-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="b5128-110">**Perguntas sobre a redefinição de senha**</span><span class="sxs-lookup"><span data-stu-id="b5128-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="b5128-111">**Perguntas sobre alteração de senha**</span><span class="sxs-lookup"><span data-stu-id="b5128-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="b5128-112">**Perguntas sobre relatórios de gerenciamento de senha**</span><span class="sxs-lookup"><span data-stu-id="b5128-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="b5128-113">**Perguntas sobre o write-back de senha**</span><span class="sxs-lookup"><span data-stu-id="b5128-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="b5128-114">Registro de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="b5128-114">Password reset registration</span></span>
* <span data-ttu-id="b5128-115">**P: meus usuários podem registrar seus próprios dados de redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="b5128-116">**R:** Sim, desde que a redefinição de senha esteja habilitada e eles sejam licenciados, eles podem ir para o portal de Registro de Redefinição de Senha em http://aka.ms/ssprsetup para registrar as informações de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b5128-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="b5128-117">Os usuários também podem se registrar se conectando ao painel de acesso em http://myapps.microsoft.com, clicando na guia perfil e clicando na opção Registrar-se para a redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="b5128-118">**P: posso definir dados de redefinição de senha em nome dos meus usuários?**</span><span class="sxs-lookup"><span data-stu-id="b5128-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="b5128-119">**R:** Sim, você pode fazer isso com o Azure AD Connect, PowerShell, [portal do Azure](https://portal.azure.com) ou o Portal de Administração do Office.</span><span class="sxs-lookup"><span data-stu-id="b5128-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="b5128-120">Para obter mais informações, consulte o artigo [Dados usados pelo Autoatendimento de Redefinição de Senha do Azure AD](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="b5128-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="b5128-121">**P: posso sincronizar dados de perguntas de segurança do local?**</span><span class="sxs-lookup"><span data-stu-id="b5128-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="b5128-122">**R:** isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="b5128-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="b5128-123">**P: meus usuários podem registrar dados de forma que outros usuários não possam ver esses dados?**</span><span class="sxs-lookup"><span data-stu-id="b5128-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="b5128-124">**R:** Sim. Quando os usuários registram dados usando o Portal de Registro de Redefinição de Senha, eles são salvos em campos de autenticação privada visíveis apenas por Administradores Globais e pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="b5128-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="b5128-125">Se uma **conta do Administrador do Azure** registrar o número de telefone de autenticação, ela também será populada no campo de telefone celular e ficará visível.</span><span class="sxs-lookup"><span data-stu-id="b5128-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="b5128-126">**P: meus usuários precisam ser registrados antes de poder usar a redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="b5128-127">**R:** Não. Se você definir informações de autenticação suficientes em nome deles, os usuários não precisarão se registrar.</span><span class="sxs-lookup"><span data-stu-id="b5128-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="b5128-128">A redefinição de senha funcionará desde que você tenha formatado corretamente os dados armazenados nos campos apropriados no diretório.</span><span class="sxs-lookup"><span data-stu-id="b5128-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="b5128-129">**P: posso sincronizar ou definir os campos Telefone de autenticação, Autenticação de email ou Telefone alternativo em nome dos meus usuários?**</span><span class="sxs-lookup"><span data-stu-id="b5128-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="b5128-130">**R:** isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="b5128-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="b5128-131">**P: como o portal de registro sabe quais opções mostrar aos meus usuários?**</span><span class="sxs-lookup"><span data-stu-id="b5128-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="b5128-132">**R:** O portal de registro de redefinição de senha só mostra as opções que você habilitou para os usuários.</span><span class="sxs-lookup"><span data-stu-id="b5128-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="b5128-133">Essas opções estão localizadas na seção Política de Redefinição de Senha de Usuário da guia Configurar do diretório.</span><span class="sxs-lookup"><span data-stu-id="b5128-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="b5128-134">Por exemplo, isso significa que, se você não habilitar perguntas de segurança, os usuários não poderão se registrar nessa opção.</span><span class="sxs-lookup"><span data-stu-id="b5128-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="b5128-135">**P: quando um usuário é considerado registrado?**</span><span class="sxs-lookup"><span data-stu-id="b5128-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="b5128-136">**R:** Um usuário é considerado registrado para o SSPR quando ele registrou, pelo menos, o **Número de métodos obrigatórios para a redefinição** que você definiu no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5128-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="b5128-137">Redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="b5128-137">Password reset</span></span>
* <span data-ttu-id="b5128-138">**P: quanto tempo deve levar até que eu receba uma chamada telefônica, um SMS ou um email de redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="b5128-139">**R:** Emails, mensagens SMS e chamadas telefônicas devem ser recebidas em menos de um minuto, normalmente de 5 a 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="b5128-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="b5128-140">Se você não receber a notificação nesse período:</span><span class="sxs-lookup"><span data-stu-id="b5128-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="b5128-141">Verifique a pasta Lixo Eletrônico.</span><span class="sxs-lookup"><span data-stu-id="b5128-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="b5128-142">Verifique se o número ou o email de contato é aquele que você espera.</span><span class="sxs-lookup"><span data-stu-id="b5128-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="b5128-143">Verifique se os dados de autenticação no diretório estão formatados corretamente.</span><span class="sxs-lookup"><span data-stu-id="b5128-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="b5128-144">Exemplo: “+1 4255551234” ou “user@contoso.com”</span><span class="sxs-lookup"><span data-stu-id="b5128-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="b5128-145">**P: quais idiomas são compatíveis com a redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="b5128-146">**R:** A interface do usuário de redefinição de senha, as mensagens SMS e as chamadas de voz estão localizadas nos mesmos idiomas com suporte no Office 365.</span><span class="sxs-lookup"><span data-stu-id="b5128-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="b5128-147">**P: que partes da experiência de redefinição de senha ficam personalizadas com a marca quando eu definir marcas organizacionais na guia Configurar no meu diretório?**</span><span class="sxs-lookup"><span data-stu-id="b5128-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="b5128-148">**R:** O portal de redefinição de senha mostra o logotipo de sua organização e também permite que você configure o link Contate o administrador para apontar para uma URL ou um email personalizado.</span><span class="sxs-lookup"><span data-stu-id="b5128-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="b5128-149">Todos os emails enviados pela redefinição de senha incluem o logotipo de sua organização, as cores, o nome no corpo do email e o nome De personalizado.</span><span class="sxs-lookup"><span data-stu-id="b5128-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="b5128-150">**P: como eu instruo os usuários sobre onde acessar para redefinir as suas senhas?**</span><span class="sxs-lookup"><span data-stu-id="b5128-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="b5128-151">**R:** Você pode enviar os usuários diretamente para https://passwordreset.microsoftonline.com ou instruí-los a clicar no **link Não consegue acessar sua conta** encontrado em qualquer tela de conexão de Conta Corporativa ou de Estudante.</span><span class="sxs-lookup"><span data-stu-id="b5128-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="b5128-152">Você também pode publicar esses links em um local acessível aos usuários.</span><span class="sxs-lookup"><span data-stu-id="b5128-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="b5128-153">**P: posso usar essa página em um dispositivo móvel?**</span><span class="sxs-lookup"><span data-stu-id="b5128-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="b5128-154">**R:** sim, essa página funciona em dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="b5128-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="b5128-155">**P: há suporte para desbloqueio das contas locais do active directory quando os usuários redefinirem as suas senhas?**</span><span class="sxs-lookup"><span data-stu-id="b5128-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="b5128-156">**R:** Sim. Quando um usuário redefine a senha e o write-back de senha foi implantado usando o Azure AD Connect, a conta desse usuário é desbloqueada automaticamente quando ele redefine a senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="b5128-157">**P: como posso integrar a redefinição de senha diretamente à experiência de entrada na área de trabalho do usuário?**</span><span class="sxs-lookup"><span data-stu-id="b5128-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="b5128-158">**R:** Se você for um cliente do Azure AD Premium, poderá instalar o Microsoft Identity Manager sem custo adicional e implantar a solução de redefinição de senha local para atender a esse requisito.</span><span class="sxs-lookup"><span data-stu-id="b5128-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="b5128-159">**P: posso definir perguntas de segurança diferentes para diferentes localidades?**</span><span class="sxs-lookup"><span data-stu-id="b5128-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="b5128-160">**R:** isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="b5128-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="b5128-161">**P: quantas perguntas podemos configurar para a opção de autenticação com perguntas de segurança?**</span><span class="sxs-lookup"><span data-stu-id="b5128-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="b5128-162">**R:** Você pode configurar até 20 perguntas de segurança personalizadas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5128-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="b5128-163">**P: qual o tamanho máximo das perguntas de segurança?**</span><span class="sxs-lookup"><span data-stu-id="b5128-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="b5128-164">**R:** as perguntas de segurança podem ter entre 3 e 200 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b5128-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="b5128-165">**P: qual o tamanho máximo das respostas às perguntas de segurança?**</span><span class="sxs-lookup"><span data-stu-id="b5128-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="b5128-166">**R:** as respostas podem ter entre 3 e 40 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b5128-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="b5128-167">**P: as respostas duplicadas para perguntas de segurança são rejeitadas?**</span><span class="sxs-lookup"><span data-stu-id="b5128-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="b5128-168">**R:** sim, rejeitamos respostas duplicadas para perguntas de segurança.</span><span class="sxs-lookup"><span data-stu-id="b5128-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="b5128-169">**P: Um usuário pode registrar a mesma pergunta de segurança mais de uma vez?**</span><span class="sxs-lookup"><span data-stu-id="b5128-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="b5128-170">**R:** Não. Quando um usuário registra uma pergunta específica, ele não pode se registrar nessa pergunta uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="b5128-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="b5128-171">**P: é possível definir um limite mínimo de perguntas de segurança para registro e redefinição?**</span><span class="sxs-lookup"><span data-stu-id="b5128-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="b5128-172">**R:** sim, um limite pode ser definido para o registro e outro para a redefinição.</span><span class="sxs-lookup"><span data-stu-id="b5128-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="b5128-173">Podem ser necessárias de três a cinco perguntas de segurança para o registro e de três a cinco perguntas para a redefinição.</span><span class="sxs-lookup"><span data-stu-id="b5128-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="b5128-174">**P: se um usuário tiver registrado mais do que o número máximo de perguntas obrigatórias para a redefinição, como as perguntas de segurança são selecionadas durante a redefinição?**</span><span class="sxs-lookup"><span data-stu-id="b5128-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="b5128-175">**R:** X perguntas de segurança são selecionadas aleatoriamente do número total de perguntas nas quais um usuário se registrou, em que X é o **Número de perguntas obrigatórias para a redefinição**.</span><span class="sxs-lookup"><span data-stu-id="b5128-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="b5128-176">Por exemplo, se um usuário tem 5 perguntas de segurança registradas, mas apenas 3 são obrigatórias para a redefinição, 3 das 5 são selecionadas aleatoriamente e apresentadas no momento da redefinição.</span><span class="sxs-lookup"><span data-stu-id="b5128-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="b5128-177">Se o usuário der respostas erradas, o processo de seleção ocorrerá novamente para evitar hammering de perguntas.</span><span class="sxs-lookup"><span data-stu-id="b5128-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="b5128-178">**P: vocês impedem os usuários de tentar redefinir a senha várias vezes em um curto período de tempo?**</span><span class="sxs-lookup"><span data-stu-id="b5128-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="b5128-179">**R:** Sim, existem recursos de segurança internos na redefinição de senha para proteção contra uso indevido.</span><span class="sxs-lookup"><span data-stu-id="b5128-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="b5128-180">Os usuários têm somente cinco tentativas de redefinição de senha em uma mesma hora antes de serem bloqueados por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b5128-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="b5128-181">Os usuários somente podem tentar validar um número de telefone cinco vezes em uma mesma hora antes de serem bloqueados por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b5128-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="b5128-182">Os usuários somente podem experimentar um único método de autenticação cinco vezes em uma mesma hora antes de serem bloqueados por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b5128-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="b5128-183">**P: por quanto tempo vale a senha de uso único por email e SMS?**</span><span class="sxs-lookup"><span data-stu-id="b5128-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="b5128-184">**R:** a duração da sessão para a redefinição de senha é de 105 minutos.</span><span class="sxs-lookup"><span data-stu-id="b5128-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="b5128-185">Desde o início da operação de redefinição de senha, o usuário tem 105 minutos para redefinir sua senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="b5128-186">A senha de uso único por email e SMS perde a validade depois que esse período de tempo expira.</span><span class="sxs-lookup"><span data-stu-id="b5128-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="b5128-187">Alteração de senha</span><span class="sxs-lookup"><span data-stu-id="b5128-187">Password change</span></span>
* <span data-ttu-id="b5128-188">**P: onde os usuários devem ir para alterar suas senhas?**</span><span class="sxs-lookup"><span data-stu-id="b5128-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="b5128-189">**R:** Os usuários podem alterar suas senhas em qualquer lugar em que veem seus ícones ou imagens de perfil (como no canto superior direito das experiências do [Office 365](https://portal.office.com) ou do [Painel de Acesso](https://myapps.microsoft.com)).</span><span class="sxs-lookup"><span data-stu-id="b5128-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="b5128-190">Os usuários podem alterar suas senhas na [página de perfil do Painel de Acesso](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="b5128-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="b5128-191">Os usuários também poderão ser solicitados a alterar suas senhas automaticamente na tela de conexão do Azure AD se elas expirarem.</span><span class="sxs-lookup"><span data-stu-id="b5128-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="b5128-192">Por fim, os usuários podem navegar até o [Portal de alteração de senha do Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) diretamente se desejarem alterar suas senhas.</span><span class="sxs-lookup"><span data-stu-id="b5128-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="b5128-193">**P: meus usuários podem ser notificados no Portal do Office quando uma senha local expirar?**</span><span class="sxs-lookup"><span data-stu-id="b5128-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="b5128-194">**R:** isso é possível no momento se você está usando o ADFS, seguindo as instruções aqui: [Enviando declarações de política de senha com o ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="b5128-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="b5128-195">Se você está usando a sincronização de hash de senha, isso não é possível atualmente.</span><span class="sxs-lookup"><span data-stu-id="b5128-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="b5128-196">Isso ocorre porque nós não sincronizamos políticas de senha locais e, portanto, não é possível postar as notificações de expiração para experiências de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b5128-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="b5128-197">Em ambos os casos, também é possível [notificar os usuários cujas senhas estejam prestes a expirar usando o PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5128-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="b5128-198">Relatórios de gerenciamento de senha</span><span class="sxs-lookup"><span data-stu-id="b5128-198">Password management reports</span></span>
* <span data-ttu-id="b5128-199">**P: quanto tempo leva para que os dados sejam exibidos nos relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="b5128-200">**R:** os dados devem ser exibidos nos relatórios de gerenciamento de senha entre 5 e 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="b5128-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="b5128-201">Em algumas instâncias, pode levar até uma hora para que sejam exibidos.</span><span class="sxs-lookup"><span data-stu-id="b5128-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="b5128-202">**P: como posso filtrar os relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="b5128-203">**R:** Você pode filtrar os relatórios de gerenciamento de senhas clicando na lupa pequena na extremidade direita dos rótulos de coluna, próximo ao início do relatório.</span><span class="sxs-lookup"><span data-stu-id="b5128-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="b5128-204">Se você quiser fazer uma filtragem mais avançada, pode baixar o relatório do Excel e criar uma tabela dinâmica.</span><span class="sxs-lookup"><span data-stu-id="b5128-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="b5128-205">**P: Qual é o número máximo de eventos armazenados nos relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="b5128-206">**R:** até 75 mil redefinições de senha ou eventos de registro de redefinição de senha são armazenados nos relatórios de gerenciamento de senha relativo ao período de 30 dias anteriores.</span><span class="sxs-lookup"><span data-stu-id="b5128-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="b5128-207">Estamos trabalhando para expandir esse número e incluir mais eventos.</span><span class="sxs-lookup"><span data-stu-id="b5128-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="b5128-208">**P: qual o período mais antigo coberto pelos relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="b5128-209">**R:** os relatórios de gerenciamento de senha mostram operações ocorridas nos últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="b5128-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="b5128-210">Por enquanto, se você precisar arquivar esses dados, pode baixar os relatórios periodicamente e salvá-los em um local separado.</span><span class="sxs-lookup"><span data-stu-id="b5128-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="b5128-211">**P: existe um número máximo de linhas que podem ser exibidas nos relatórios de gerenciamento de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="b5128-212">**R:** sim, um máximo de 75 mil linhas pode aparecer nos relatórios de gerenciamento de senha, quer seja mostrado na interface do usuário ou baixado.</span><span class="sxs-lookup"><span data-stu-id="b5128-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="b5128-213">**P: Existe uma API para acessar os dados do relatório de redefinição de senha ou de registro de redefinição de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="b5128-214">**R:** Sim. Consulte a documentação a seguir para saber como você pode acessar o fluxo de dados do relatório de redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="b5128-215">[Saiba como acessar programaticamente os eventos de relatório de redefinição de senha](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="b5128-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="b5128-216">Write-back de senha</span><span class="sxs-lookup"><span data-stu-id="b5128-216">Password writeback</span></span>
* <span data-ttu-id="b5128-217">**P: como funciona os bastidores do write-back de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="b5128-218">**R:** Consulte [Como funciona o write-back de senha](active-directory-passwords-writeback.md) para obter uma explicação detalhada do que acontece quando você habilita o write-back de senha e como os dados fluem pelo sistema novamente ao seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="b5128-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="b5128-219">**P: quanto tempo demora para o write-back de senha funcionar?  Há um atraso de sincronização como com a sincronização com hash de senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="b5128-220">**R:** o write-back de senha é instantâneo.</span><span class="sxs-lookup"><span data-stu-id="b5128-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="b5128-221">É um pipeline síncrono que funciona de forma essencialmente diferente da sincronização com hash de senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="b5128-222">O write-back de senha permite aos usuários obter comentários em tempo real sobre o sucesso da operação de redefinição ou de alteração de senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="b5128-223">O tempo médio para um write-back bem-sucedido de uma senha é abaixo de 500 ms.</span><span class="sxs-lookup"><span data-stu-id="b5128-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="b5128-224">**P: Se minha conta local estiver desabilitada, como minha conta ou meu acesso na nuvem será afetado?**</span><span class="sxs-lookup"><span data-stu-id="b5128-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="b5128-225">**R:** Se sua ID local estiver desabilitada, a ID ou o acesso na nuvem também estará desabilitado no próximo intervalo de sincronização por meio do AAD Connect. Por padrão, isso ocorre a cada 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="b5128-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="b5128-226">**P: Se minha conta local for restrita por uma política de senha do Active Directory local, o SSPR respeitará essa política quando eu alterar a senha?**</span><span class="sxs-lookup"><span data-stu-id="b5128-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="b5128-227">**R:** Sim, o SSPR se baseia e respeita a política de senha do AD local, incluindo a política de senha típica do domínio do AD, bem como as políticas de senha refinadas e definidas, direcionadas a determinado usuário.</span><span class="sxs-lookup"><span data-stu-id="b5128-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="b5128-228">**P: o write-back de senha funciona com quais tipos de conta?**</span><span class="sxs-lookup"><span data-stu-id="b5128-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="b5128-229">**R:** O write-back de senha funciona com usuários Federados e Sincronizados com Hash de Senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="b5128-230">**P: o write-back de senha impõe as políticas de senha do meu domínio?**</span><span class="sxs-lookup"><span data-stu-id="b5128-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="b5128-231">**R:** Sim, o write-back de senha impõe a duração, o histórico e a complexidade da senha, filtros e qualquer outra restrição que você possa impor nas senhas no domínio local.</span><span class="sxs-lookup"><span data-stu-id="b5128-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="b5128-232">**P: o write-back de senha é seguro?  Como posso ter certeza de que não serei invadido por um hacker?**</span><span class="sxs-lookup"><span data-stu-id="b5128-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="b5128-233">**R:** Sim, o write-back de senha é seguro.</span><span class="sxs-lookup"><span data-stu-id="b5128-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="b5128-234">Para ler mais sobre as quatro camadas de segurança implementadas pelo serviço de write-back de senha, confira a seção [Modelo de segurança do write-back de senha](active-directory-passwords-writeback.md#password-writeback-security-model) em Como funciona o write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="b5128-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="b5128-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5128-235">Next steps</span></span>

<span data-ttu-id="b5128-236">Os links a seguir fornecem informações adicionais sobre a redefinição de senha usando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5128-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="b5128-237">[**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5128-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="b5128-238">[**Licenciamento**](active-directory-passwords-licensing.md): configure o licenciamento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5128-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="b5128-239">[**Dados**](active-directory-passwords-data.md): entenda os dados que são necessários e como eles são usados para o gerenciamento de senhas</span><span class="sxs-lookup"><span data-stu-id="b5128-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="b5128-240">[**Distribuição**](active-directory-passwords-best-practices.md): planeje e implante o SSPR para seus usuários usando as diretrizes descritas aqui</span><span class="sxs-lookup"><span data-stu-id="b5128-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="b5128-241">[**Personalizar**](active-directory-passwords-customize.md): personalize a aparência da experiência do SSPR em sua empresa.</span><span class="sxs-lookup"><span data-stu-id="b5128-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="b5128-242">[**Relatórios**](active-directory-passwords-reporting.md) – descubra se, quando e onde os usuários estão acessando a funcionalidade do SSPR</span><span class="sxs-lookup"><span data-stu-id="b5128-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="b5128-243">[**Política**](active-directory-passwords-policy.md) – entenda e defina políticas de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5128-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="b5128-244">[**Write-back de Senha**](active-directory-passwords-writeback.md) – como o write-back de senha funciona com o diretório local</span><span class="sxs-lookup"><span data-stu-id="b5128-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="b5128-245">[**Aprofundamento Técnico**](active-directory-passwords-how-it-works.md) – vá para os bastidores para entender como ele funciona</span><span class="sxs-lookup"><span data-stu-id="b5128-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="b5128-246">[**Resolver problemas**](active-directory-passwords-troubleshoot.md) – saiba como resolver problemas comuns encontrados no SSPR</span><span class="sxs-lookup"><span data-stu-id="b5128-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
