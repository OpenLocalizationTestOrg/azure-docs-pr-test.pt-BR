---
title: "domínios de aaaCustom no Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Gerencie domínios personalizados no Proxy de aplicativo do Azure AD para essa URL Olá para o aplicativo hello é Olá mesmo, independentemente de onde os usuários acessá-lo."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="3eaa9-103">Trabalhando com domínios personalizados no Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3eaa9-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="3eaa9-104">Quando você publica um aplicativo por meio do Proxy de aplicativo do Azure Active Directory, você cria uma URL externa para seu toowhen de toogo de usuários que estão trabalhando remotamente.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="3eaa9-105">Essa URL é o domínio padrão de saudação *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="3eaa9-106">Por exemplo, se você publicou um aplicativo chamado despesas e seu locatário nomeado Contoso, URL externa Olá seria https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="3eaa9-107">Se você quiser toouse seu próprio nome de domínio, configure um domínio personalizado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="3eaa9-108">É recomendável que você configure domínios personalizados para seus aplicativos sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="3eaa9-109">Alguns dos benefícios de saudação de domínios personalizados incluem:</span><span class="sxs-lookup"><span data-stu-id="3eaa9-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="3eaa9-110">Os usuários podem obter aplicativos toohello com hello a mesma URL, se estiverem trabalhando dentro ou fora da sua rede.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="3eaa9-111">Se todos os aplicativos têm hello mesmo URLs internas e externas, links em um aplicativo que levam tooanother continuam toowork mesmo fora da rede corporativa hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="3eaa9-112">Você controla sua identidade visual e cria URLs de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="3eaa9-113">Configurar um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3eaa9-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3eaa9-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3eaa9-114">Prerequisites</span></span>

<span data-ttu-id="3eaa9-115">Antes de configurar um domínio personalizado, certifique-se de que você tenha Olá preparados de requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3eaa9-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="3eaa9-116">Um [domínio verificado adicionado tooAzure do Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3eaa9-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="3eaa9-117">Um certificado personalizado para o domínio hello, na forma de saudação de um arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="3eaa9-118">Um aplicativo local [publicado por meio do Proxy de Aplicativo](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3eaa9-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="3eaa9-119">Configurar seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3eaa9-119">Configure your custom domain</span></span>

<span data-ttu-id="3eaa9-120">Quando você tiver um desses três requisitos prontos, siga essas tooset etapas o seu domínio personalizado:</span><span class="sxs-lookup"><span data-stu-id="3eaa9-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="3eaa9-121">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3eaa9-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3eaa9-122">Navegue muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos** e escolha o aplicativo hello toomanage desejado.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="3eaa9-123">Selecione **Proxy de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="3eaa9-124">No campo de URL externa hello, use Olá suspensa lista tooselect seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="3eaa9-125">Se você não vir o seu domínio na lista de hello, em seguida, ele ainda não foi verificado ainda.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="3eaa9-126">Selecione **Salvar**</span><span class="sxs-lookup"><span data-stu-id="3eaa9-126">Select **Save**</span></span>
5. <span data-ttu-id="3eaa9-127">Olá **certificado** campo foi desabilitado se torne habilitado.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="3eaa9-128">Selecione esse campo.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-128">Select this field.</span></span> 

   ![Clique em tooupload um certificado](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="3eaa9-130">Se você já carregou um certificado para este domínio, o campo de certificado Olá exibe informações de certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="3eaa9-131">Carregar certificado PFX hello e digite a senha de saudação certificado hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="3eaa9-132">Selecione **salvar** toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="3eaa9-133">Adicionar um [registro DNS](../dns/dns-operations-recordsets-portal.md) redirecionamentos Olá novo domínio de msappproxy.net de toohello URL externo.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="3eaa9-134">Você só precisa de um certificado tooupload por domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="3eaa9-135">Quando você carregar um certificado, você pode escolher domínio personalizado hello quando você publica um novo aplicativo e não tem toodo a configuração adicional, exceto o registro DNS hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="3eaa9-136">Gerenciar certificados</span><span class="sxs-lookup"><span data-stu-id="3eaa9-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="3eaa9-137">Formato do certificado</span><span class="sxs-lookup"><span data-stu-id="3eaa9-137">Certificate format</span></span>
<span data-ttu-id="3eaa9-138">Não há nenhuma restrição sobre métodos de assinatura de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="3eaa9-139">A Criptografia de Curva Elíptica (ECC), o Nome Alternativo da Entidade (SAN) e outros tipos de certificado são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="3eaa9-140">Você pode usar um certificado curinga como curinga Olá coincide com a URL externa de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="3eaa9-141">Você também pode usar certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="3eaa9-142">Se você estiver usando uma autoridade de certificação privada, Olá CDP (ponto de distribuição do ponto de revogação de certificado) para o certificado de saudação deve ser pública.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="3eaa9-143">Alterar domínio Olá</span><span class="sxs-lookup"><span data-stu-id="3eaa9-143">Changing hello domain</span></span>
<span data-ttu-id="3eaa9-144">Todos os domínios verificados aparecem na lista de suspensa Olá URL externa para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="3eaa9-145">domínio de saudação toochange, apenas atualizar campo para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="3eaa9-146">Se o domínio Olá desejado não estiver na lista de hello, [adicioná-lo como um domínio verificado](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3eaa9-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="3eaa9-147">Se você selecionar um domínio que ainda não tiver um certificado associado, siga o certificado de saudação do tooadd as etapas 5 a 7.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="3eaa9-148">Em seguida, certifique-se de que atualizar tooredirect de registro de DNS Olá da saudação nova URL externa.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="3eaa9-149">Gerenciamento de certificados</span><span class="sxs-lookup"><span data-stu-id="3eaa9-149">Certificate management</span></span>
<span data-ttu-id="3eaa9-150">Você pode usar o mesmo certificado para vários aplicativos, a menos que os aplicativos de saudação compartilham um host externo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="3eaa9-151">Você receber um aviso quando um certificado expira, informando tooupload outro certificado por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="3eaa9-152">Se o certificado de saudação for revogado, os usuários podem ver um aviso de segurança ao acessar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="3eaa9-153">Nós não realizamos verificações de revogação de certificados.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="3eaa9-154">certificado de saudação tooupdate para um determinado aplicativo, navegue toohello aplicativo e siga as etapas 5 a 7 para configurar domínios personalizados em um novo certificado de tooupload de aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="3eaa9-155">Se o certificado antigo Olá não está sendo usado por outros aplicativos, ele será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="3eaa9-156">Atualmente todo o gerenciamento de certificado é por meio de páginas de aplicativos individuais para que você precisa de certificados toomanage no contexto de saudação do aplicativos relevantes hello.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3eaa9-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3eaa9-157">Next steps</span></span>
* <span data-ttu-id="3eaa9-158">[Habilitar logon único](active-directory-application-proxy-sso-using-kcd.md) tooyour publicado aplicativos com a autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="3eaa9-159">[Habilitar o acesso condicional](active-directory-application-proxy-conditional-access.md) aplicativos publicados do tooyour.</span><span class="sxs-lookup"><span data-stu-id="3eaa9-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="3eaa9-160">Adicionar seu nome de domínio personalizado tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="3eaa9-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


