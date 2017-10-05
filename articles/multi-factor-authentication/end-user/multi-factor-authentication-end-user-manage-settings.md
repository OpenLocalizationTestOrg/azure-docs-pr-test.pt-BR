---
title: "Gerenciar as configurações de verificação em duas etapas | Microsoft Docs"
description: "Gerencie como usar Autenticação Multifator do Azure incluindo alterar suas informações de contato ou configurar seus dispositivos."
services: multi-factor-authentication
keywords: "cliente do multifactor authentication, problema de autenticação, ID de correlação"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="767d3-104">Gerenciar as configurações de verificação em duas etapas</span><span class="sxs-lookup"><span data-stu-id="767d3-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="767d3-105">Este artigo responde a perguntas sobre como atualizar as configurações de autenticação multifator ou de verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="767d3-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="767d3-106">Se você estiver tendo problemas ao se conectar à sua conta, confira [Tendo problemas com a verificacão em duas etapas](multi-factor-authentication-end-user-troubleshoot.md) para a resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="767d3-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="767d3-107">Onde encontrar a página de configurações</span><span class="sxs-lookup"><span data-stu-id="767d3-107">Where to find the settings page</span></span>
<span data-ttu-id="767d3-108">Dependendo de como a sua empresa usa a Autenticação Multifator do Azure, há alguns lugares onde você pode alterar as configurações, como o número de seu telefone.</span><span class="sxs-lookup"><span data-stu-id="767d3-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="767d3-109">Se o seu administrador de TI envia uma URL específica ou etapas para gerenciar a verificação em duas etapas, siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="767d3-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="767d3-110">Caso contrário, as instruções a seguir devem funcionar para todos os outros.</span><span class="sxs-lookup"><span data-stu-id="767d3-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="767d3-111">Se você seguir estas etapas, mas não vê as mesmas opções, isso significa que sua empresa ou escola personalizaram o próprio portal.</span><span class="sxs-lookup"><span data-stu-id="767d3-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="767d3-112">Peça ao administrador o link para o portal de Autenticação Multifator do Azure.</span><span class="sxs-lookup"><span data-stu-id="767d3-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="767d3-113">Entre em [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="767d3-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="767d3-114">Selecione o nome da conta no canto superior direito e selecione **perfil**.</span><span class="sxs-lookup"><span data-stu-id="767d3-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="767d3-115">Escolha **Verificação de segurança adicional**.</span><span class="sxs-lookup"><span data-stu-id="767d3-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="767d3-117">A página de Verificação de segurança adicional carrega com suas configurações.</span><span class="sxs-lookup"><span data-stu-id="767d3-117">The Additional security verification page loads with your settings.</span></span>

    ![Prova](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="767d3-119">Desejo alterar meu número de telefone ou adicionar um número secundário</span><span class="sxs-lookup"><span data-stu-id="767d3-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="767d3-120">É importante configurar um número de telefone de autenticação secundário.</span><span class="sxs-lookup"><span data-stu-id="767d3-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="767d3-121">Como seu número de telefone principal e seu aplicativo móvel provavelmente estão no mesmo telefone, o número de telefone secundário é a única maneira de poder retornar à sua conta caso seu telefone seja roubado ou você o perca.</span><span class="sxs-lookup"><span data-stu-id="767d3-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="767d3-122">Se você não tem acesso ao seu número de telefone principal e precisa de ajuda para entrar em sua conta, confira os tópicos de Ajuda em [Tendo problemas com a verificação em duas etapas](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="767d3-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="767d3-123">**Para alterar o número de telefone principal:**</span><span class="sxs-lookup"><span data-stu-id="767d3-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="767d3-124">Na página de Verificação de segurança adicional, marque a caixa de texto com seu número de telefone atual e edite com o seu novo número de telefone.</span><span class="sxs-lookup"><span data-stu-id="767d3-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="767d3-125">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="767d3-125">Select **Save**.</span></span>  
3. <span data-ttu-id="767d3-126">Se este é o número que você usa para a opção de verificação preferencial, você precisa verificar o novo número antes de salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="767d3-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="767d3-127">**Para adicionar um número de telefone secundário:**</span><span class="sxs-lookup"><span data-stu-id="767d3-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="767d3-128">Na página de Verificação de segurança adicional, marque a caixa ao lado de **Telefone de autenticação alternativo.**</span><span class="sxs-lookup"><span data-stu-id="767d3-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="767d3-129">Insira o número de telefone secundário na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="767d3-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="767d3-130">Selecione **Salvar** e suas alterações são concluídas.</span><span class="sxs-lookup"><span data-stu-id="767d3-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="767d3-131">Exigir verificação em duas etapas novamente em um dispositivo que você marcou como confiável</span><span class="sxs-lookup"><span data-stu-id="767d3-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="767d3-132">Dependendo das configurações de sua organização, uma caixa de seleção "Não pergunte novamente por **X** dias" pode ser exibida quando você executa a verificação em duas etapas em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="767d3-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="767d3-133">Se você marcar essa caixa de seleção e perder seu dispositivo ou achar que sua conta foi comprometida, restaure a verificação em duas etapas para todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="767d3-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="767d3-134">Na página Verificação de segurança adicional, selecione **Restaurar autenticação multifator em dispositivos anteriormente confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="767d3-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="767d3-135">Na próxima vez que você entrar em qualquer dispositivo, receberá uma solicitação para executar a verificação de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="767d3-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="767d3-136">Como limpar o Microsoft Authenticator de meu dispositivo antigo e movê-lo para um novo?</span><span class="sxs-lookup"><span data-stu-id="767d3-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="767d3-137">Quando você desinstala o aplicativo do dispositivo ou reinicia o dispositivo, ele não remove a ativação no back-end.</span><span class="sxs-lookup"><span data-stu-id="767d3-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="767d3-138">Para saber mais, veja [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="767d3-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="767d3-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="767d3-139">Next steps</span></span>
* <span data-ttu-id="767d3-140">Obter dicas de solução de problemas e ajuda em [Tendo problemas com a verificação em duas etapas](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="767d3-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="767d3-141">Configure [senhas de aplicativo](multi-factor-authentication-end-user-app-passwords.md) para quaisquer aplicativos que não dão suporte à verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="767d3-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
