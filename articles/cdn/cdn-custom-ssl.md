---
title: "AAA \"Habilitar HTTPS em um domínio personalizado CDN do Azure | Microsoft Docs\""
description: "Saiba como tooenable HTTPS no ponto de extremidade CDN do Azure com um domínio personalizado."
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
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="ae85b-103">Como ativar HTTPS em um domínio personalizado CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ae85b-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="ae85b-104">Suporte HTTPS para domínios personalizados do Azure CDN permite que você toodeliver o conteúdo seguro via SSL usando sua própria segurança de saudação do domínio nome tooimprove de dados em trânsito.</span><span class="sxs-lookup"><span data-stu-id="ae85b-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="ae85b-105">Olá fluxo de trabalho de ponta a ponta tooenable HTTPS para seu domínio personalizado foi simplificada por meio de um botão do mouse, gerenciamento de certificados completo e todos os sem nenhum custo adicional.</span><span class="sxs-lookup"><span data-stu-id="ae85b-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="ae85b-106">É privacidade de saudação tooensure crítico e integridade dos dados de todos os dados confidenciais de aplicativos web em trânsito.</span><span class="sxs-lookup"><span data-stu-id="ae85b-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="ae85b-107">Usando Olá protocolo HTTPS garante que seus dados confidenciais são criptografados quando ela é enviada pela Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="ae85b-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="ae85b-108">Ele fornece confiabilidade, autenticação e protege seus aplicativos Web contra ataques.</span><span class="sxs-lookup"><span data-stu-id="ae85b-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="ae85b-109">Atualmente, o CDN do Azure oferece suporte a HTTPS em um ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="ae85b-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="ae85b-110">Por exemplo, se você criar um ponto de extremidade CDN do CDN do Azure (por exemplo, https://contoso.azureedge.net), o HTTPS será habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ae85b-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="ae85b-111">Com HTTPS de domínio personalizado, você também pode habilitar a entrega segura para um domínio personalizado (por exemplo, https://www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="ae85b-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="ae85b-112">Estes são alguns dos atributos de chave de saudação do recurso HTTPS:</span><span class="sxs-lookup"><span data-stu-id="ae85b-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="ae85b-113">Sem custo adicional: não há custos de aquisição ou renovação do certificado e não há custo adicional para tráfego HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ae85b-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="ae85b-114">Você paga apenas GB de saída de hello CDN.</span><span class="sxs-lookup"><span data-stu-id="ae85b-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="ae85b-115">Habilitação Simple: um clique de provisionamento está disponível no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae85b-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ae85b-116">Você também pode usar a API REST ou outro recurso de saudação de tooenable de ferramentas de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="ae85b-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="ae85b-117">Gerenciamento de certificado completo: todos os certificados de aquisição e gerenciamento são manipulados para você.</span><span class="sxs-lookup"><span data-stu-id="ae85b-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="ae85b-118">Os certificados são automaticamente provisionados e renovados tooexpiration anterior.</span><span class="sxs-lookup"><span data-stu-id="ae85b-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="ae85b-119">Isso remove completamente os riscos de saudação de interrupção do serviço como resultado de um certificado expira.</span><span class="sxs-lookup"><span data-stu-id="ae85b-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="ae85b-120">Suporte a HTTPS tooenabling anterior, você já deve ter estabelecido um [domínio personalizado CDN do Azure](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ae85b-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="ae85b-121">Etapa 1: Habilitar o recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="ae85b-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="ae85b-122">Em Olá [portal do Azure](https://portal.azure.com), procure o perfil CDN tooyour Verizon padrão ou premium.</span><span class="sxs-lookup"><span data-stu-id="ae85b-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="ae85b-123">Na lista de saudação de pontos de extremidade, clique o ponto de extremidade de saudação que contém seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ae85b-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="ae85b-124">Clique em Olá domínio personalizado para o qual você deseja tooenable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ae85b-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Folha de ponto de extremidade](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="ae85b-126">Clique em **na** tooenable HTTPS e salvar a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae85b-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Caixa de diálogo personalizada HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="ae85b-128">Etapa 2: validação de domínio</span><span class="sxs-lookup"><span data-stu-id="ae85b-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="ae85b-129">Conclua a validação completa de domínio antes de ativar o HTTPS no seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ae85b-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="ae85b-130">Você tem 6 dias tooapprove Olá domínio de negócios.</span><span class="sxs-lookup"><span data-stu-id="ae85b-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="ae85b-131">A solicitação será cancelada se não tiver aprovação em 6 dias úteis.</span><span class="sxs-lookup"><span data-stu-id="ae85b-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="ae85b-132">Depois de habilitar HTTPS em seu domínio personalizado, nosso provedor do certificado HTTPS DigiCert validará a propriedade de seu domínio entrando em contato com o inscrito Olá para seu domínio, com base nas informações de inscrito WHOIS, por email (por padrão) ou telefone.</span><span class="sxs-lookup"><span data-stu-id="ae85b-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="ae85b-133">DigiCert também enviará Olá toohello de email de verificação abaixo endereços.</span><span class="sxs-lookup"><span data-stu-id="ae85b-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="ae85b-134">Se as informações de inscrito WHOIS forem privadas, verifique se é possível aprovar diretamente por meio de um desses endereços.</span><span class="sxs-lookup"><span data-stu-id="ae85b-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="ae85b-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="ae85b-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="ae85b-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="ae85b-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="ae85b-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="ae85b-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="ae85b-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="ae85b-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="ae85b-139">Ao receber o email de saudação, você tem duas opções de verificação:</span><span class="sxs-lookup"><span data-stu-id="ae85b-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="ae85b-140">Você pode aprovar todas as futuras pedidos feitos por meio de saudação mesma conta para Olá mesmo domínio de raiz, por exemplo, consoto.com. Essa é uma abordagem recomendada, se você estiver planejando tooadd personalizado domínios adicionais Olá futura para Olá mesmo domínio de raiz.</span><span class="sxs-lookup"><span data-stu-id="ae85b-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="ae85b-141">Assim, você pode aprovar usada nesta solicitação de nome de host específico hello.</span><span class="sxs-lookup"><span data-stu-id="ae85b-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="ae85b-142">Uma aprovação adicional será necessária para as solicitações seguintes.</span><span class="sxs-lookup"><span data-stu-id="ae85b-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="ae85b-143">Email de exemplo:</span><span class="sxs-lookup"><span data-stu-id="ae85b-143">Example email:</span></span>
    
    ![Caixa de diálogo personalizada HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="ae85b-145">Após a aprovação, DigiCert adicionará seu certificado de SAN de toohello de nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ae85b-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="ae85b-146">o certificado Olá será válido por um ano e será automaticamente renovado antes que ele expirou.</span><span class="sxs-lookup"><span data-stu-id="ae85b-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="ae85b-147">Etapa 3: Aguarde a propagação de saudação e começar a usar o recurso</span><span class="sxs-lookup"><span data-stu-id="ae85b-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="ae85b-148">Depois que o nome de domínio Olá é validado demorará too6 8 horas para toobe HTTPS de recurso do domínio personalizado Olá active.</span><span class="sxs-lookup"><span data-stu-id="ae85b-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="ae85b-149">Após a conclusão do processo de saudação, status de "HTTPS personalizado" hello em Olá portal do Azure será definido muito "Enabled".</span><span class="sxs-lookup"><span data-stu-id="ae85b-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="ae85b-150">O HTTPS com seu domínio personalizado está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="ae85b-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ae85b-151">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="ae85b-151">Frequently asked questions</span></span>

1. <span data-ttu-id="ae85b-152">*Quem é o provedor de certificado hello e que tipo de certificado é usado?*</span><span class="sxs-lookup"><span data-stu-id="ae85b-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="ae85b-153">Usamos o certificado de nomes de alternativos da entidade (SAN) fornecido pela DigiCert.</span><span class="sxs-lookup"><span data-stu-id="ae85b-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="ae85b-154">Um certificado SAN pode proteger vários nomes de domínio totalmente qualificados com um certificado.</span><span class="sxs-lookup"><span data-stu-id="ae85b-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="ae85b-155">*Posso usar o meu certificado dedicado?*</span><span class="sxs-lookup"><span data-stu-id="ae85b-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="ae85b-156">Não no momento, mas seu em Olá roteiro.</span><span class="sxs-lookup"><span data-stu-id="ae85b-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="ae85b-157">*Se não receber email de verificação de domínio de saudação do DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="ae85b-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="ae85b-158">Entre em contato com a Microsoft se você não receber um email dentro de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ae85b-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="ae85b-159">*Usar um certificado SAN é menos seguro do que um certificado dedicado?*</span><span class="sxs-lookup"><span data-stu-id="ae85b-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="ae85b-160">Um certificado SAN segue Olá mesmos padrões de criptografia e segurança, como um certificado dedicado. Todos os certificados SSL emitidos usam SHA-256 para uma maior segurança do servidor.</span><span class="sxs-lookup"><span data-stu-id="ae85b-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="ae85b-161">*Eu posso usar HTTPS do domínio personalizado com o CDN do Azure do Akamai?*</span><span class="sxs-lookup"><span data-stu-id="ae85b-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="ae85b-162">Atualmente, esse recurso só está disponível com o CDN do Azure da Verizon.</span><span class="sxs-lookup"><span data-stu-id="ae85b-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="ae85b-163">Estamos trabalhando em dar suporte a esse recurso com o Azure CDN do Akamai nos próximos meses de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae85b-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ae85b-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae85b-164">Next steps</span></span>

- <span data-ttu-id="ae85b-165">Saiba como tooset a um [domínio personalizado no ponto de extremidade CDN do Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="ae85b-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


