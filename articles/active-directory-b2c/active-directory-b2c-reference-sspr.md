---
title: "Azure Active Directory B2C: autoatendimento de redefinição de senha | Microsoft Docs"
description: "Um tópico que demonstra como configurar a redefinição de senha por autoatendimento para seus consumidores no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="b8d01-103">Azure Active Directory B2C: configurar a redefinição de senha por autoatendimento para seus consumidores</span><span class="sxs-lookup"><span data-stu-id="b8d01-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="b8d01-104">Com o recurso de redefinição de senha por autoatendimento, seus consumidores (que tenham se registrado com contas locais) poderão redefinir as respectivas senhas por conta própria.</span><span class="sxs-lookup"><span data-stu-id="b8d01-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="b8d01-105">Isso reduz significativamente a sobrecarga da equipe de suporte, principalmente se milhões de consumidores usarem seu aplicativo regularmente.</span><span class="sxs-lookup"><span data-stu-id="b8d01-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="b8d01-106">Atualmente, só há suporte para usar um endereço de email verificado como um método de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b8d01-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="b8d01-107">Vamos incluir mais métodos de recuperação (número de telefone verificado, perguntas de segurança, etc.) futuramente.</span><span class="sxs-lookup"><span data-stu-id="b8d01-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="b8d01-108">Este artigo se aplica ao autoatendimento de redefinição de senha usado no contexto de uma política de entrada.</span><span class="sxs-lookup"><span data-stu-id="b8d01-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="b8d01-109">Se precisar de políticas de redefinição de senha totalmente personalizáveis invocadas por meio de seu aplicativo, veja [este artigo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="b8d01-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="b8d01-110">Por padrão, o diretório não terá a redefinição de senha por autoatendimento ativada.</span><span class="sxs-lookup"><span data-stu-id="b8d01-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="b8d01-111">Use as etapas a seguir para ativá-la:</span><span class="sxs-lookup"><span data-stu-id="b8d01-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="b8d01-112">Entre no [portal clássico do Azure](https://manage.windowsazure.com/) como o Administrador da Assinatura.</span><span class="sxs-lookup"><span data-stu-id="b8d01-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="b8d01-113">Essa é a mesma conta corporativa, de estudante ou da Microsoft que você usou para criar o diretório.</span><span class="sxs-lookup"><span data-stu-id="b8d01-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="b8d01-114">Navegue até a extensão do Active Directory na barra de navegação do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="b8d01-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="b8d01-115">Localize o diretório na guia **Diretório** e clique nele.</span><span class="sxs-lookup"><span data-stu-id="b8d01-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="b8d01-116">Clique na guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="b8d01-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="b8d01-117">Role para baixo até a seção **Política de redefinição de senha do usuário** e alterne a opção **Usuários habilitados para redefinição de senha** para **SIM**.</span><span class="sxs-lookup"><span data-stu-id="b8d01-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="b8d01-118">Observe que a opção **Endereço de Email Alternativo** está marcada; deixe-a como está.</span><span class="sxs-lookup"><span data-stu-id="b8d01-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Redefinição de senha de autoatendimento](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="b8d01-120">Na parte inferior da página, clique em **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b8d01-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="b8d01-121">Pronto!</span><span class="sxs-lookup"><span data-stu-id="b8d01-121">You're done!</span></span>

<span data-ttu-id="b8d01-122">Para testar, use o recurso "Executar agora" em qualquer política de entrada que tenha contas locais como um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b8d01-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="b8d01-123">Na página de entrada da conta local (na qual você insere um endereço de email e a senha ou um nome de usuário e a senha), clique em **Não consegue acessar sua conta?** para verificar a experiência do consumidor.</span><span class="sxs-lookup"><span data-stu-id="b8d01-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="b8d01-124">As páginas do autoatendimento de redefinição de senha podem ser personalizadas usando o [recurso de identidade visual da empresa](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="b8d01-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

