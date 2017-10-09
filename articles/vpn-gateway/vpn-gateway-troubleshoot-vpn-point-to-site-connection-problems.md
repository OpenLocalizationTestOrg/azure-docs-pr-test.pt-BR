---
title: "problemas de conexão aaaTroubleshoot Azure ponto a site | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de conexão de ponto a site."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="bf699-103">Solução de problemas: problemas de conexão de ponto a site do Azure</span><span class="sxs-lookup"><span data-stu-id="bf699-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="bf699-104">Este artigo lista os problemas comuns de conexão de ponto a site que podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="bf699-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="bf699-105">Também discute as possíveis causas e soluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="bf699-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="bf699-106">Erro de cliente VPN: não foi possível encontrar um certificado</span><span class="sxs-lookup"><span data-stu-id="bf699-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-107">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-107">Symptom</span></span>

<span data-ttu-id="bf699-108">Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="bf699-109">**Não foi possível encontrar um certificado que possa ser usado com este protocolo EAP. (Erro 798)**</span><span class="sxs-lookup"><span data-stu-id="bf699-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-110">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-110">Cause</span></span>

<span data-ttu-id="bf699-111">Esse problema ocorre se o certificado de cliente hello está ausente no **certificados - certificados atual**.</span><span class="sxs-lookup"><span data-stu-id="bf699-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-112">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-112">Solution</span></span>

<span data-ttu-id="bf699-113">Verifique se que esse certificado de cliente hello está instalado no hello local do repositório de certificados da saudação (Certmgr.msc) a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf699-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="bf699-114">**Certificates - Current User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="bf699-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="bf699-115">Para obter mais informações sobre como tooinstall Olá certificado de cliente, consulte [gerar e exportar certificados para conexões ponto a site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="bf699-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bf699-116">Quando você importa o certificado de cliente hello, não selecione Olá **habilitar a proteção forte de chave privada** opção.</span><span class="sxs-lookup"><span data-stu-id="bf699-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="bf699-117">Erro de cliente VPN: mensagem de saudação recebida era inesperada ou formatada incorretamente</span><span class="sxs-lookup"><span data-stu-id="bf699-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-118">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-118">Symptom</span></span>

<span data-ttu-id="bf699-119">Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="bf699-120">**mensagem de saudação recebida era inesperada ou formatada incorretamente. (Erro 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="bf699-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-121">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-121">Cause</span></span>

<span data-ttu-id="bf699-122">Esse problema ocorre se a chave pública do certificado de raiz de saudação não é carregada no gateway de VPN do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="bf699-123">Ele também pode ocorrer se a chave hello está corrompido ou expirado.</span><span class="sxs-lookup"><span data-stu-id="bf699-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-124">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-124">Solution</span></span>

<span data-ttu-id="bf699-125">tooresolve esse problema, verificar o status de saudação da raiz de saudação do certificado em Olá toosee portal do Azure se ele foi revogado.</span><span class="sxs-lookup"><span data-stu-id="bf699-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="bf699-126">Se não for revogado, tente reupload e certificado de raiz toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="bf699-127">Para saber mais, confira [Criar certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="bf699-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="bf699-128">Erro de cliente VPN: uma cadeia de certificados foi processada, mas fechada</span><span class="sxs-lookup"><span data-stu-id="bf699-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="bf699-129">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-129">Symptom</span></span> 

<span data-ttu-id="bf699-130">Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="bf699-131">**Uma cadeia de certificados processada, mas terminou em um certificado raiz que não é confiável pelo provedor de confiança de saudação.**</span><span class="sxs-lookup"><span data-stu-id="bf699-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-132">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-132">Solution</span></span>

1. <span data-ttu-id="bf699-133">Certifique-se de que Olá certificados a seguir estão no local correto hello:</span><span class="sxs-lookup"><span data-stu-id="bf699-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="bf699-134">Certificado</span><span class="sxs-lookup"><span data-stu-id="bf699-134">Certificate</span></span> | <span data-ttu-id="bf699-135">Local padrão</span><span class="sxs-lookup"><span data-stu-id="bf699-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="bf699-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="bf699-136">AzureClient.pfx</span></span>  | <span data-ttu-id="bf699-137">Current User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="bf699-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="bf699-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="bf699-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="bf699-139">Current User\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="bf699-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="bf699-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="bf699-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="bf699-141">Local Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="bf699-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="bf699-142">Se certificados Olá já estão no local de hello, tente certificados de saudação toodelete e reinstalá-los.</span><span class="sxs-lookup"><span data-stu-id="bf699-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="bf699-143">Olá  **azuregateway -*GUID*. cloudapp.net** certificado está no hello configuração pacote do cliente VPN que você baixou da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf699-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="bf699-144">Você pode usar archivers tooextract Olá arquivos do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="bf699-145">Erro no download do arquivo: o URI de destino não foi especificado</span><span class="sxs-lookup"><span data-stu-id="bf699-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-146">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-146">Symptom</span></span>

<span data-ttu-id="bf699-147">Você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-147">You receive hello following error message:</span></span>

<span data-ttu-id="bf699-148">**Erro de download do arquivo. O URI de destino não foi especificado.**</span><span class="sxs-lookup"><span data-stu-id="bf699-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-149">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-149">Cause</span></span> 

<span data-ttu-id="bf699-150">Esse problema ocorre devido ao tipo de gateway incorreto.</span><span class="sxs-lookup"><span data-stu-id="bf699-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="bf699-151">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-151">Solution</span></span>

<span data-ttu-id="bf699-152">Olá tipo de gateway VPN deve ser **VPN**, e deve ser Olá tipo VPN **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="bf699-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="bf699-153">Erro de cliente VPN: falha de script personalizado do VPN Azure</span><span class="sxs-lookup"><span data-stu-id="bf699-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="bf699-154">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-154">Symptom</span></span>

<span data-ttu-id="bf699-155">Quando você tenta tooconnect tooan rede virtual do Azure usando saudação do cliente VPN, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="bf699-156">**Script personalizado (tooupdate sua tabela de roteamento) falhou. (Erro 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="bf699-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-157">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-157">Cause</span></span>

<span data-ttu-id="bf699-158">Esse problema pode ocorrer se você estiver tentando conexão de VPN tooopen Olá ponto a site usando um atalho.</span><span class="sxs-lookup"><span data-stu-id="bf699-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-159">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-159">Solution</span></span> 

<span data-ttu-id="bf699-160">Abra o pacote VPN de saudação diretamente, em vez de abri-lo do atalho hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="bf699-161">Não é possível instalar o cliente VPN Olá</span><span class="sxs-lookup"><span data-stu-id="bf699-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-162">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-162">Cause</span></span> 

<span data-ttu-id="bf699-163">Um certificado adicional será necessária tootrust gateway VPN Olá para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="bf699-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="bf699-164">Olá certificado está incluído no pacote configuração de cliente VPN de saudação que é gerado em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf699-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-165">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-165">Solution</span></span>

<span data-ttu-id="bf699-166">Extraia o pacote de configuração de cliente VPN hello e localizar o arquivo. cer de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="bf699-167">Olá tooinstall do certificado, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="bf699-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="bf699-168">Abra mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="bf699-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="bf699-169">Adicionar Olá **certificados** snap-in.</span><span class="sxs-lookup"><span data-stu-id="bf699-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="bf699-170">Selecione Olá **computador** de conta de computador local hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="bf699-171">Saudação de atalho **autoridades de certificação raiz confiáveis** nó.</span><span class="sxs-lookup"><span data-stu-id="bf699-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="bf699-172">Clique em **todas as tarefas** > **importação**e procurar toohello. cer arquivos extraídos do pacote de configuração de cliente VPN hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="bf699-173">Reinicie o computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="bf699-174">Tente tooinstall do cliente VPN hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="bf699-175">Erro de portal do Azure: falha do gateway VPN toosave hello e dados saudação são inválidos</span><span class="sxs-lookup"><span data-stu-id="bf699-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-176">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-176">Symptom</span></span>

<span data-ttu-id="bf699-177">Quando você tenta toosave alterações de saudação de gateway VPN Olá Olá portal do Azure, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="bf699-178">**Gateway de rede virtual com falha toosave &lt;* nome do gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="bf699-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="bf699-179">Os dados para o certificado &lt;*ID do certificado*&gt; são inválidos.**</span><span class="sxs-lookup"><span data-stu-id="bf699-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-180">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-180">Cause</span></span> 

<span data-ttu-id="bf699-181">Esse problema pode ocorrer se Olá raiz chave pública de certificado que você carregou contém um caractere inválido, como um espaço.</span><span class="sxs-lookup"><span data-stu-id="bf699-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-182">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-182">Solution</span></span>

<span data-ttu-id="bf699-183">Certifique-se de que dados Olá no certificado de saudação não contém caracteres inválidos, como quebras de linha (retorno de carro).</span><span class="sxs-lookup"><span data-stu-id="bf699-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="bf699-184">valor inteiro Olá deve ser uma linha longa.</span><span class="sxs-lookup"><span data-stu-id="bf699-184">hello entire value should be one long line.</span></span> <span data-ttu-id="bf699-185">Olá texto a seguir está um exemplo de certificado hello:</span><span class="sxs-lookup"><span data-stu-id="bf699-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="bf699-186">Erro de portal do Azure: falha do gateway VPN toosave hello e Olá nome do recurso é inválido</span><span class="sxs-lookup"><span data-stu-id="bf699-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-187">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-187">Symptom</span></span>

<span data-ttu-id="bf699-188">Quando você tenta toosave alterações de saudação de gateway VPN Olá Olá portal do Azure, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="bf699-189">**Gateway de rede virtual com falha toosave &lt;* nome do gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="bf699-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="bf699-190">Nome do recurso &lt; *nome do certificado que você tente tooupload* &gt; é inválido * *.</span><span class="sxs-lookup"><span data-stu-id="bf699-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-191">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-191">Cause</span></span>

<span data-ttu-id="bf699-192">Esse problema ocorre porque o nome de saudação do certificado Olá contém um caractere inválido, como um espaço.</span><span class="sxs-lookup"><span data-stu-id="bf699-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="bf699-193">Erro 503 de portal do Azure: erro de download do arquivo do pacote VPN</span><span class="sxs-lookup"><span data-stu-id="bf699-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-194">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-194">Symptom</span></span>

<span data-ttu-id="bf699-195">Ao testar o pacote de configuração de cliente VPN do toodownload hello, você recebe Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="bf699-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="bf699-196">**Falha ao arquivo de saudação toodownload. Detalhes do erro: erro 503. Olá servidor está ocupado.**</span><span class="sxs-lookup"><span data-stu-id="bf699-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="bf699-197">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-197">Solution</span></span>

<span data-ttu-id="bf699-198">Esse erro pode ser causado por um problema de rede temporário.</span><span class="sxs-lookup"><span data-stu-id="bf699-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="bf699-199">Tente o pacote VPN Olá toodownload novamente após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="bf699-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="bf699-200">A atualização de Gateway VPN do Azure: P2S todos os clientes são tooconnect não é possível</span><span class="sxs-lookup"><span data-stu-id="bf699-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-201">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-201">Cause</span></span>

<span data-ttu-id="bf699-202">Se o certificado Olá é mais de 50 por cento por meio de seu ciclo de vida, o certificado de saudação é rodado.</span><span class="sxs-lookup"><span data-stu-id="bf699-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-203">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-203">Solution</span></span>

<span data-ttu-id="bf699-204">tooresolve esse problema, crie e redistribuir novos clientes VPN toohello de certificados.</span><span class="sxs-lookup"><span data-stu-id="bf699-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="bf699-205">Muitos clientes VPN conectados ao mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="bf699-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="bf699-206">Para cada gateway VPN, o número máximo de saudação de conexões permitidas é 128.</span><span class="sxs-lookup"><span data-stu-id="bf699-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="bf699-207">Você pode ver o número total de saudação de clientes conectados em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf699-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="bf699-208">VPN ponto a site incorretamente adiciona uma rota para a tabela de rotas toohello 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="bf699-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-209">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-209">Symptom</span></span>

<span data-ttu-id="bf699-210">Quando você discar Olá conexão VPN no cliente de ponto para site Olá, do cliente VPN Olá deve adicionar uma rota de rede virtual do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="bf699-211">serviço do auxiliar de IP Hello deve adicionar uma rota para a sub-rede de saudação de clientes VPN de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="bf699-212">Olá intervalo de cliente VPN pertence a menor sub-rede tooa 10.0.0.0/8 como 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="bf699-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="bf699-213">Em vez de uma rota para 10.0.12.0/24, é adicionada uma rota para 10.0.0.0/8 que tem prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="bf699-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="bf699-214">Essa rota incorreta quebras de conectividade com outras redes locais que podem pertencer a sub-rede tooanother dentro do intervalo de 10.0.0.0/8 hello, como 10.50.0.0/24, que não têm uma rota específica de definidos.</span><span class="sxs-lookup"><span data-stu-id="bf699-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="bf699-215">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-215">Cause</span></span>

<span data-ttu-id="bf699-216">Esse comportamento ocorre por padrão para clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="bf699-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="bf699-217">Quando Olá cliente usa o protocolo PPP IPCP Olá, ele obtém o endereço IP de Olá para interface de túnel de saudação do servidor de saudação (gateway VPN Olá neste caso).</span><span class="sxs-lookup"><span data-stu-id="bf699-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="bf699-218">No entanto, devido a uma limitação no protocolo hello, o cliente de saudação não tem máscara de sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="bf699-219">Porque não há nenhum outro tooget de maneira, cliente Olá tenta tooguess máscara de sub-rede de saudação com base na classe de saudação do endereço IP da interface de túnel hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="bf699-220">Portanto, é adicionada uma rota com base em Olá mapeamento estático a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf699-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="bf699-221">Se o endereço pertence A tooclass--> Aplicar /8</span><span class="sxs-lookup"><span data-stu-id="bf699-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="bf699-222">Se o endereço pertence tooclass--> B aplicar /16</span><span class="sxs-lookup"><span data-stu-id="bf699-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="bf699-223">Se o endereço pertence tooclass--> C aplicar /24</span><span class="sxs-lookup"><span data-stu-id="bf699-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="bf699-224">O cliente VPN não pode acessar compartilhamentos de arquivos de rede</span><span class="sxs-lookup"><span data-stu-id="bf699-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-225">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-225">Symptom</span></span>

<span data-ttu-id="bf699-226">cliente VPN Olá conectou toohello rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf699-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="bf699-227">No entanto, o cliente Olá não pode acessar compartilhamentos de rede.</span><span class="sxs-lookup"><span data-stu-id="bf699-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="bf699-228">Causa</span><span class="sxs-lookup"><span data-stu-id="bf699-228">Cause</span></span>

<span data-ttu-id="bf699-229">Olá protocolo SMB é usado para acesso de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="bf699-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="bf699-230">Quando a conexão de saudação for iniciada, cliente VPN Olá adiciona credenciais de sessão de saudação e Olá falha ocorre.</span><span class="sxs-lookup"><span data-stu-id="bf699-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="bf699-231">Depois de estabelecer conexão hello, cliente Olá é forçado toouse Olá cache as credenciais de autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="bf699-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="bf699-232">Esse processo inicia consultas toohello Key Distribution Center (um controlador de domínio) tooget um token.</span><span class="sxs-lookup"><span data-stu-id="bf699-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="bf699-233">Como cliente Olá se conecta de saudação à Internet, não pode ser tooreach capaz de controlador de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf699-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="bf699-234">Portanto, cliente Olá não é possível realizar failover da tooNTLM Kerberos.</span><span class="sxs-lookup"><span data-stu-id="bf699-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="bf699-235">Olá apenas tempo que o cliente Olá é solicitado para uma credencial é quando ele tem um certificado válido (com SAN = UPN) emitido por Olá toowhich de domínio está associado.</span><span class="sxs-lookup"><span data-stu-id="bf699-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="bf699-236">cliente Olá também deve ser conectada fisicamente toohello rede de domínio.</span><span class="sxs-lookup"><span data-stu-id="bf699-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="bf699-237">Nesse caso, o cliente de Olá tenta toouse certificado de saudação e atinge toohello controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="bf699-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="bf699-238">Olá Key Distribution Center retorna um erro de "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="bf699-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="bf699-239">cliente de saudação é forçado toofail tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="bf699-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="bf699-240">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-240">Solution</span></span>

<span data-ttu-id="bf699-241">toowork problema hello, desabilitar o cache de saudação de credenciais de domínio de saudação seguinte subchave do registro:</span><span class="sxs-lookup"><span data-stu-id="bf699-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="bf699-242">Não é possível localizar a conexão de VPN de ponto para site Olá no Windows após a reinstalação do cliente VPN Olá</span><span class="sxs-lookup"><span data-stu-id="bf699-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="bf699-243">Sintoma</span><span class="sxs-lookup"><span data-stu-id="bf699-243">Symptom</span></span>

<span data-ttu-id="bf699-244">Remover conexão de VPN de ponto para site hello e, em seguida, reinstalar o cliente VPN hello.</span><span class="sxs-lookup"><span data-stu-id="bf699-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="bf699-245">Nessa situação, Olá conexão VPN não está configurado com êxito.</span><span class="sxs-lookup"><span data-stu-id="bf699-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="bf699-246">Você não vir a conexão de VPN Olá no hello **conexões de rede** configurações do Windows.</span><span class="sxs-lookup"><span data-stu-id="bf699-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="bf699-247">Solução</span><span class="sxs-lookup"><span data-stu-id="bf699-247">Solution</span></span>

<span data-ttu-id="bf699-248">problema de saudação tooresolve, excluir Olá antigo VPN cliente arquivos de configuração de **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, e execute o instalador do cliente VPN Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="bf699-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
