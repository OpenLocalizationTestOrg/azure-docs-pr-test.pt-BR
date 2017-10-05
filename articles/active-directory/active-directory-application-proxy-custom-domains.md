---
title: "Domínios Personalizados no Proxy de Aplicativo do Azure AD | Microsoft Docs"
description: "Gerencie domínios personalizados no Proxy de Aplicativo do Azure AD para que a URL do aplicativo seja a mesma, independentemente de onde os usuários a acessam."
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="ffc06-103">Trabalhando com domínios personalizados no Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ffc06-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="ffc06-104">Ao publicar um aplicativo por meio do Proxy de Aplicativo do Azure Active Directory, você cria uma URL externa para seus usuários acessarem quando estiverem trabalhando remotamente.</span><span class="sxs-lookup"><span data-stu-id="ffc06-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="ffc06-105">Essa URL obtém o domínio padrão *seulocatário.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="ffc06-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="ffc06-106">Por exemplo, se você tiver publicado um aplicativo chamado Despesas e seu locatário chamar-se Contoso, a URL externa será https://despesas-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="ffc06-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="ffc06-107">Se quiser usar seu próprio nome de domínio, configure um domínio personalizado para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc06-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="ffc06-108">É recomendável que você configure domínios personalizados para seus aplicativos sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="ffc06-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="ffc06-109">Alguns dos benefícios dos domínios personalizados incluem:</span><span class="sxs-lookup"><span data-stu-id="ffc06-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="ffc06-110">Os usuários podem acessar o aplicativo com a mesma URL se estiverem trabalhando dentro ou fora da sua rede.</span><span class="sxs-lookup"><span data-stu-id="ffc06-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="ffc06-111">Se todos os seus aplicativos têm as mesmas URLs internas e externas, os links em um aplicativo que apontam para outro continuam a funcionar até mesmo fora da rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="ffc06-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="ffc06-112">Você controla sua identidade visual e cria as URLs que quiser.</span><span class="sxs-lookup"><span data-stu-id="ffc06-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="ffc06-113">Configurar um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ffc06-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ffc06-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ffc06-114">Prerequisites</span></span>

<span data-ttu-id="ffc06-115">Antes de configurar um domínio personalizado, verifique se você tem os seguintes requisitos preparados:</span><span class="sxs-lookup"><span data-stu-id="ffc06-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="ffc06-116">Um [domínio verificado adicionado ao Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffc06-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="ffc06-117">Um certificado personalizado para o domínio, no formato de um arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="ffc06-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="ffc06-118">Um aplicativo local [publicado por meio do Proxy de Aplicativo](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffc06-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="ffc06-119">Configurar seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ffc06-119">Configure your custom domain</span></span>

<span data-ttu-id="ffc06-120">Quando você tiver esses três requisitos prontos, siga estas etapas para configurar o domínio personalizado:</span><span class="sxs-lookup"><span data-stu-id="ffc06-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="ffc06-121">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffc06-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ffc06-122">Navegue até **Azure Active Directory** > **Aplicativos empresariais** > **Todos os aplicativos** e escolha o aplicativo que deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="ffc06-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="ffc06-123">Selecione **Proxy de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="ffc06-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="ffc06-124">No campo URL Externa, use a lista suspensa para selecionar seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="ffc06-125">Se você não vir o seu domínio na lista, ele ainda não foi verificado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="ffc06-126">Selecione **Salvar**</span><span class="sxs-lookup"><span data-stu-id="ffc06-126">Select **Save**</span></span>
5. <span data-ttu-id="ffc06-127">O campo **Certificado**, que estava desabilitado, fica habilitado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="ffc06-128">Selecione esse campo.</span><span class="sxs-lookup"><span data-stu-id="ffc06-128">Select this field.</span></span> 

   ![Clique para carregar um certificado](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="ffc06-130">Se você já tiver carregado um certificado para este domínio, o campo de certificado exibirá as informações do certificado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="ffc06-131">Carregue o certificado PFX e digite a senha do certificado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="ffc06-132">Selecione **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="ffc06-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="ffc06-133">Adicione um [registro DNS](../dns/dns-operations-recordsets-portal.md) que redirecione a nova URL externa para o domínio msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="ffc06-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="ffc06-134">Você só precisa carregar um certificado por domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="ffc06-135">Assim que carregar um certificado, você poderá escolher o domínio personalizado ao publicar um novo aplicativo e não precisará fazer configurações adicionais, exceto o registro DNS.</span><span class="sxs-lookup"><span data-stu-id="ffc06-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="ffc06-136">Gerenciar certificados</span><span class="sxs-lookup"><span data-stu-id="ffc06-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="ffc06-137">Formato do certificado</span><span class="sxs-lookup"><span data-stu-id="ffc06-137">Certificate format</span></span>
<span data-ttu-id="ffc06-138">Não há nenhuma restrição em relação aos métodos de assinatura do certificado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="ffc06-139">A Criptografia de Curva Elíptica (ECC), o Nome Alternativo da Entidade (SAN) e outros tipos de certificado são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="ffc06-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="ffc06-140">Você pode usar um certificado curinga, desde que o curinga corresponda à URL externa desejada.</span><span class="sxs-lookup"><span data-stu-id="ffc06-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="ffc06-141">Você também pode usar certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="ffc06-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="ffc06-142">Se você estiver usando uma autoridade de certificação privada, o CDP (ponto de distribuição do ponto de revogação de certificado) para o certificado deverá ser público.</span><span class="sxs-lookup"><span data-stu-id="ffc06-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="ffc06-143">Alterando o domínio</span><span class="sxs-lookup"><span data-stu-id="ffc06-143">Changing the domain</span></span>
<span data-ttu-id="ffc06-144">Todos os domínios verificados aparecem na lista suspensa de URL Externa do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc06-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="ffc06-145">Para alterar o domínio, apenas atualize esse campo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc06-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="ffc06-146">Se o domínio desejado não estiver na lista, [adicione-o como um domínio verificado](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffc06-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="ffc06-147">Se você selecionar um domínio que não tenha um certificado associado, siga as etapas 5 a 7 para adicionar o certificado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="ffc06-148">Em seguida, certifique-se de atualizar o registro DNS para redirecionar da nova URL externa.</span><span class="sxs-lookup"><span data-stu-id="ffc06-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="ffc06-149">Gerenciamento de certificados</span><span class="sxs-lookup"><span data-stu-id="ffc06-149">Certificate management</span></span>
<span data-ttu-id="ffc06-150">Você pode usar o mesmo certificado para vários aplicativos, a menos que os aplicativos compartilhem um host externo.</span><span class="sxs-lookup"><span data-stu-id="ffc06-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="ffc06-151">Você recebe um aviso quando um certificado expira, informando para que você carregue outro certificado por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="ffc06-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="ffc06-152">Se o certificado for revogado, os usuários poderão ver um aviso de segurança ao acessarem o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ffc06-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="ffc06-153">Nós não realizamos verificações de revogação de certificados.</span><span class="sxs-lookup"><span data-stu-id="ffc06-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="ffc06-154">Para atualizar o certificado de um determinado aplicativo, navegue até o aplicativo e siga as etapas 5 a 7 para configurar domínios personalizados em aplicativos publicados a fim de carregar um novo certificado.</span><span class="sxs-lookup"><span data-stu-id="ffc06-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="ffc06-155">Se o certificado antigo não estiver sendo usado por outros aplicativos, ele será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ffc06-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="ffc06-156">Atualmente, todo o gerenciamento de certificados é feito por meio de páginas de aplicativos individuais, portanto você precisa gerenciar os certificados no contexto dos aplicativos relevantes.</span><span class="sxs-lookup"><span data-stu-id="ffc06-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ffc06-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ffc06-157">Next steps</span></span>
* <span data-ttu-id="ffc06-158">[Habilite o logon único](active-directory-application-proxy-sso-using-kcd.md) aos seus aplicativos publicados com a autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffc06-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="ffc06-159">[Habilite o acesso condicional](active-directory-application-proxy-conditional-access.md) aos seus aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="ffc06-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="ffc06-160">Adicionar seu nome de domínio personalizado ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffc06-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


