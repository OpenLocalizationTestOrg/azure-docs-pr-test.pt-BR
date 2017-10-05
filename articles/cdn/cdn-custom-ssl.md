---
title: "Como habilitar HTTPS em um domínio personalizado CDN do Azure | Microsoft Docs"
description: "Saiba como habilitar HTTPS em seu ponto de extremidade CDN do Azure com um domínio personalizado."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="150c3-103">Como ativar HTTPS em um domínio personalizado CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="150c3-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="150c3-104">O suporte a HTTPS para domínios personalizados CDN do Azure permite distribuir conteúdo seguro via SSL usando seu nome de domínio próprio para aumentar a segurança dos dados em trânsito.</span><span class="sxs-lookup"><span data-stu-id="150c3-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="150c3-105">O fluxo de trabalho de ponta a ponta para habilitar HTTPS para o seu domínio personalizado é simplificado com a habilitação de apenas um clique e o gerenciamento do certificado completo, sem nenhum custo adicional.</span><span class="sxs-lookup"><span data-stu-id="150c3-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="150c3-106">É fundamental para garantir a privacidade e a integridade dos dados de todos os seus dados confidenciais de aplicativos Web em trânsito.</span><span class="sxs-lookup"><span data-stu-id="150c3-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="150c3-107">Usar o protocolo HTTPS garante que os seus dados confidenciais são criptografados quando enviados através da internet.</span><span class="sxs-lookup"><span data-stu-id="150c3-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="150c3-108">Ele fornece confiabilidade, autenticação e protege seus aplicativos Web contra ataques.</span><span class="sxs-lookup"><span data-stu-id="150c3-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="150c3-109">Atualmente, o CDN do Azure oferece suporte a HTTPS em um ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="150c3-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="150c3-110">Por exemplo, se você criar um ponto de extremidade CDN do CDN do Azure (por exemplo, https://contoso.azureedge.net), o HTTPS será habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="150c3-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="150c3-111">Com HTTPS de domínio personalizado, você também pode habilitar a entrega segura para um domínio personalizado (por exemplo, https://www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="150c3-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="150c3-112">Estes são alguns dos atributos principais do recurso HTTPS:</span><span class="sxs-lookup"><span data-stu-id="150c3-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="150c3-113">Sem custo adicional: não há custos de aquisição ou renovação do certificado e não há custo adicional para tráfego HTTPS.</span><span class="sxs-lookup"><span data-stu-id="150c3-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="150c3-114">Você paga apenas por GB de saída do CDN.</span><span class="sxs-lookup"><span data-stu-id="150c3-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="150c3-115">Ativação simples: o provisionamento com um clique está disponível no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="150c3-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="150c3-116">Você também pode usar a API REST ou outras ferramentas de desenvolvedor para habilitar o recurso.</span><span class="sxs-lookup"><span data-stu-id="150c3-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="150c3-117">Gerenciamento de certificado completo: todos os certificados de aquisição e gerenciamento são manipulados para você.</span><span class="sxs-lookup"><span data-stu-id="150c3-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="150c3-118">Certificados são automaticamente provisionados e renovados antes da expiração.</span><span class="sxs-lookup"><span data-stu-id="150c3-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="150c3-119">Isso remove completamente os riscos de interrupção do serviço como resultado de uma expiração do certificado.</span><span class="sxs-lookup"><span data-stu-id="150c3-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="150c3-120">Antes de habilitar o suporte a HTTPS, você deve estabelecer uma [domínio personalizado CDN do Azure ](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="150c3-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="150c3-121">Etapa 1: habilitação do recurso</span><span class="sxs-lookup"><span data-stu-id="150c3-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="150c3-122">No [portal do Azure](https://portal.azure.com), navegue até o seu perfil CDN Verizon padrão ou premium.</span><span class="sxs-lookup"><span data-stu-id="150c3-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="150c3-123">Na lista de pontos de extremidade, clique no ponto de extremidade que contém seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="150c3-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="150c3-124">Clique no domínio personalizado que deseja habilitar o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="150c3-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Folha de ponto de extremidade](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="150c3-126">Clique em **Ligar** para habilitar o HTTPS e salvar a alteração.</span><span class="sxs-lookup"><span data-stu-id="150c3-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Caixa de diálogo personalizada HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="150c3-128">Etapa 2: validação de domínio</span><span class="sxs-lookup"><span data-stu-id="150c3-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="150c3-129">Conclua a validação completa de domínio antes de ativar o HTTPS no seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="150c3-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="150c3-130">Você tem 6 dias úteis para aprovar o domínio.</span><span class="sxs-lookup"><span data-stu-id="150c3-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="150c3-131">A solicitação será cancelada se não tiver aprovação em 6 dias úteis.</span><span class="sxs-lookup"><span data-stu-id="150c3-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="150c3-132">Depois de habilitar o HTTPS em seu domínio personalizado, o nosso provedor de certificado HTTPS DigiCert validará a propriedade do seu domínio entrando em contato, com base nas informações de registro WHOIS, com o solicitante através de email (por padrão) ou telefone.</span><span class="sxs-lookup"><span data-stu-id="150c3-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="150c3-133">DigiCert também enviará o email de verificação para os endereços abaixo.</span><span class="sxs-lookup"><span data-stu-id="150c3-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="150c3-134">Se as informações de inscrito WHOIS forem privadas, verifique se é possível aprovar diretamente por meio de um desses endereços.</span><span class="sxs-lookup"><span data-stu-id="150c3-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="150c3-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="150c3-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="150c3-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="150c3-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="150c3-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="150c3-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="150c3-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="150c3-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="150c3-139">Ao receber o email, você tem duas opções de verificação:</span><span class="sxs-lookup"><span data-stu-id="150c3-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="150c3-140">Aprovar todos os pedidos futuros feitos com a mesma conta para o mesmo domínio raiz, por exemplo, consoto.com.</span><span class="sxs-lookup"><span data-stu-id="150c3-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="150c3-141">Essa é uma abordagem recomendada se você planeja adicionar mais domínios personalizados no futuro para o mesmo domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="150c3-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="150c3-142">Você pode aprovar apenas o nome do host específico usado nesta solicitação.</span><span class="sxs-lookup"><span data-stu-id="150c3-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="150c3-143">Uma aprovação adicional será necessária para as solicitações seguintes.</span><span class="sxs-lookup"><span data-stu-id="150c3-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="150c3-144">Email de exemplo:</span><span class="sxs-lookup"><span data-stu-id="150c3-144">Example email:</span></span>
    
    ![Caixa de diálogo personalizada HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="150c3-146">Após a aprovação, o DigiCert adicionará seu nome de domínio personalizado ao certificado SAN.</span><span class="sxs-lookup"><span data-stu-id="150c3-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="150c3-147">O certificado será válido por um ano e será automaticamente renovado antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="150c3-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="150c3-148">Etapa 3: aguarde a propagação e comece a usar o recurso</span><span class="sxs-lookup"><span data-stu-id="150c3-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="150c3-149">Depois da validação do nome de domínio, leva de 6 a 8 horas para a ativação do recurso HTTPS de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="150c3-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="150c3-150">Depois da conclusão do processo, o status "HTTPS personalizado" no portal do Azure é definido para "Habilitado".</span><span class="sxs-lookup"><span data-stu-id="150c3-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="150c3-151">O HTTPS com seu domínio personalizado está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="150c3-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="150c3-152">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="150c3-152">Frequently asked questions</span></span>

1. <span data-ttu-id="150c3-153">*Quem é o provedor de certificado e que tipo de certificado é usado?*</span><span class="sxs-lookup"><span data-stu-id="150c3-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="150c3-154">Usamos o certificado de nomes de alternativos da entidade (SAN) fornecido pela DigiCert.</span><span class="sxs-lookup"><span data-stu-id="150c3-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="150c3-155">Um certificado SAN pode proteger vários nomes de domínio totalmente qualificados com um certificado.</span><span class="sxs-lookup"><span data-stu-id="150c3-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="150c3-156">*Posso usar o meu certificado dedicado?*</span><span class="sxs-lookup"><span data-stu-id="150c3-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="150c3-157">Atualmente não, mas está previsto.</span><span class="sxs-lookup"><span data-stu-id="150c3-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="150c3-158">*E se eu não receber o email de verificação de domínio do DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="150c3-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="150c3-159">Entre em contato com a Microsoft se você não receber um email dentro de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="150c3-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="150c3-160">*Usar um certificado SAN é menos seguro do que um certificado dedicado?*</span><span class="sxs-lookup"><span data-stu-id="150c3-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="150c3-161">Um certificado SAN segue os mesmos padrões de criptografia e segurança que um certificado dedicado.</span><span class="sxs-lookup"><span data-stu-id="150c3-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="150c3-162">Todos os certificados SSL emitidos usam SHA-256 para uma maior segurança do servidor.</span><span class="sxs-lookup"><span data-stu-id="150c3-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="150c3-163">*Eu posso usar HTTPS do domínio personalizado com o CDN do Azure do Akamai?*</span><span class="sxs-lookup"><span data-stu-id="150c3-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="150c3-164">Atualmente, esse recurso só está disponível com o CDN do Azure da Verizon.</span><span class="sxs-lookup"><span data-stu-id="150c3-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="150c3-165">Estamos trabalhando para oferecer suporte a esse recurso com o CDN do Azure do Akamai nos próximos meses.</span><span class="sxs-lookup"><span data-stu-id="150c3-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="150c3-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="150c3-166">Next steps</span></span>

- <span data-ttu-id="150c3-167">Saiba como configurar um [domínio personalizado no seu ponto de extremidade do CDN do Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="150c3-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


