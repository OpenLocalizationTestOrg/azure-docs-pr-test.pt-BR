---
title: "Azure Active Directory B2C: autoatendimento de redefinição de senha | Microsoft Docs"
description: "Um tópico demonstra como a redefinição de tooset a senha de autoatendimento para seus consumidores no Azure Active Directory B2C"
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="9342f-103">Azure Active Directory B2C: configurar a redefinição de senha por autoatendimento para seus consumidores</span><span class="sxs-lookup"><span data-stu-id="9342f-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="9342f-104">Olá com o recurso de redefinição de senha de autoatendimento, seus consumidores (que se inscreveram para contas locais) podem redefinir suas senhas em seus próprios.</span><span class="sxs-lookup"><span data-stu-id="9342f-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="9342f-105">Isso reduz significativamente carga Olá em sua equipe de suporte, especialmente se seu aplicativo tiver milhões de consumidores usá-lo regularmente.</span><span class="sxs-lookup"><span data-stu-id="9342f-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="9342f-106">Atualmente, só há suporte para usar um endereço de email verificado como um método de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9342f-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="9342f-107">Vamos adicionar métodos de recuperação adicionais (número de telefone verificado, perguntas de segurança, etc.) em um futuro hello.</span><span class="sxs-lookup"><span data-stu-id="9342f-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="9342f-108">Este artigo se aplica a senha de serviço tooself usada no contexto de saudação de uma política de redefinição.</span><span class="sxs-lookup"><span data-stu-id="9342f-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="9342f-109">Se precisar de políticas de redefinição de senha totalmente personalizáveis invocadas por meio de seu aplicativo, veja [este artigo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="9342f-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="9342f-110">Por padrão, o diretório não terá a redefinição de senha por autoatendimento ativada.</span><span class="sxs-lookup"><span data-stu-id="9342f-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="9342f-111">Use Olá seguindo as etapas tooturn-lo em:</span><span class="sxs-lookup"><span data-stu-id="9342f-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="9342f-112">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) como Olá administrador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="9342f-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="9342f-113">Isso é hello mesmo trabalho ou conta escolar ou Olá a mesma conta da Microsoft que você usou toocreate seu diretório.</span><span class="sxs-lookup"><span data-stu-id="9342f-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="9342f-114">Navegue a extensão do Active Directory toohello na barra de navegação Olá no lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="9342f-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="9342f-115">Localizar seu diretório de saudação **diretório** guia e clique nele.</span><span class="sxs-lookup"><span data-stu-id="9342f-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="9342f-116">Clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="9342f-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="9342f-117">Role para baixo toohello **política de redefinição de senha do usuário** seção e alternar Olá **usuários habilitados para redefinição de senha** opção muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="9342f-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="9342f-118">Observe que Olá **endereço de Email alternativo** opção estiver marcada; deixe-o como está.</span><span class="sxs-lookup"><span data-stu-id="9342f-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Redefinição de senha de autoatendimento](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="9342f-120">Clique em **salvar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="9342f-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="9342f-121">Pronto!</span><span class="sxs-lookup"><span data-stu-id="9342f-121">You're done!</span></span>

<span data-ttu-id="9342f-122">tootest, o recurso de "Executar agora" hello use em qualquer política de entrada que tem as contas locais como um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="9342f-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="9342f-123">Na saudação conta local entrar página (em que você inserir um endereço de email e senha, ou um nome de usuário e senha), clique em **não é possível acessar sua conta?** experiência do consumidor Olá tooverify.</span><span class="sxs-lookup"><span data-stu-id="9342f-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="9342f-124">Olá páginas de redefinição de senha de autoatendimento podem ser personalizadas usando Olá [marca do recurso da empresa](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="9342f-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

