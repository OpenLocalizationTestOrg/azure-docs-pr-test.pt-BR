---
title: "Solucionar problemas de conexão de ponto a site do Azure | Microsoft Docs"
description: "Saiba como solucionar problemas de conexão de ponto a site."
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
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="98c8c-103">Solução de problemas: problemas de conexão de ponto a site do Azure</span><span class="sxs-lookup"><span data-stu-id="98c8c-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="98c8c-104">Este artigo lista os problemas comuns de conexão de ponto a site que podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="98c8c-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="98c8c-105">Também discute as possíveis causas e soluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="98c8c-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="98c8c-106">Erro de cliente VPN: não foi possível encontrar um certificado</span><span class="sxs-lookup"><span data-stu-id="98c8c-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-107">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-107">Symptom</span></span>

<span data-ttu-id="98c8c-108">Quando você tenta conectar-se à rede virtual do Azure usando o cliente VPN, recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="98c8c-109">**Não foi possível encontrar um certificado que possa ser usado com este protocolo EAP. (Erro 798)**</span><span class="sxs-lookup"><span data-stu-id="98c8c-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-110">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-110">Cause</span></span>

<span data-ttu-id="98c8c-111">Esse problema ocorrerá se o certificado do cliente estiver ausente em **Certificates – Current User\Personal\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-112">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-112">Solution</span></span>

<span data-ttu-id="98c8c-113">Verifique se o certificado do cliente está instalado no seguinte local do repositório de certificados (Certmgr.msc):</span><span class="sxs-lookup"><span data-stu-id="98c8c-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="98c8c-114">**Certificates - Current User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="98c8c-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="98c8c-115">Para saber mais sobre como instalar o certificado do cliente, confira [Gerar e exportar certificados para conexões ponto a site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="98c8c-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="98c8c-116">Quando você importar o certificado do cliente, não selecione a opção **Habilitar a proteção de chave privada forte**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="98c8c-117">Erro de cliente VPN: a mensagem recebida foi inesperada ou formatada incorretamente</span><span class="sxs-lookup"><span data-stu-id="98c8c-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-118">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-118">Symptom</span></span>

<span data-ttu-id="98c8c-119">Quando você tenta conectar-se à rede virtual do Azure usando o cliente VPN, recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="98c8c-120">**A mensagem recebida era inesperada ou estava formatada incorretamente. (Erro 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="98c8c-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-121">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-121">Cause</span></span>

<span data-ttu-id="98c8c-122">Esse problema ocorre se a chave pública do certificado raiz não é carregada para o gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="98c8c-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="98c8c-123">Também poderá ocorrer se a chave estiver corrompida ou expirada.</span><span class="sxs-lookup"><span data-stu-id="98c8c-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-124">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-124">Solution</span></span>

<span data-ttu-id="98c8c-125">Para resolver esse problema, verifique o status do certificado raiz no portal do Azure para ver se ele foi revogado.</span><span class="sxs-lookup"><span data-stu-id="98c8c-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="98c8c-126">Se não foi revogado, tente excluir o certificado raiz e carregá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="98c8c-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="98c8c-127">Para saber mais, confira [Criar certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="98c8c-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="98c8c-128">Erro de cliente VPN: uma cadeia de certificados foi processada, mas fechada</span><span class="sxs-lookup"><span data-stu-id="98c8c-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="98c8c-129">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-129">Symptom</span></span> 

<span data-ttu-id="98c8c-130">Quando você tenta conectar-se à rede virtual do Azure usando o cliente VPN, recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="98c8c-131">**Uma cadeia de certificados foi processada, mas terminou em um certificado raiz em que o provedor de confiabilidade não confia.**</span><span class="sxs-lookup"><span data-stu-id="98c8c-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-132">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-132">Solution</span></span>

1. <span data-ttu-id="98c8c-133">Verifique se os certificados abaixo estão no local correto:</span><span class="sxs-lookup"><span data-stu-id="98c8c-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="98c8c-134">Certificado</span><span class="sxs-lookup"><span data-stu-id="98c8c-134">Certificate</span></span> | <span data-ttu-id="98c8c-135">Local padrão</span><span class="sxs-lookup"><span data-stu-id="98c8c-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="98c8c-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="98c8c-136">AzureClient.pfx</span></span>  | <span data-ttu-id="98c8c-137">Current User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="98c8c-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="98c8c-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="98c8c-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="98c8c-139">Current User\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="98c8c-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="98c8c-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="98c8c-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="98c8c-141">Local Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="98c8c-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="98c8c-142">Se os certificados estiverem no local, tente excluir os certificados e reinstalá-los.</span><span class="sxs-lookup"><span data-stu-id="98c8c-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="98c8c-143">O certificado **azuregateway-*GUID*.cloudapp.net** está no pacote de configuração de cliente VPN que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="98c8c-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="98c8c-144">Você pode usar arquivadores para extrair os arquivos do pacote.</span><span class="sxs-lookup"><span data-stu-id="98c8c-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="98c8c-145">Erro no download do arquivo: o URI de destino não foi especificado</span><span class="sxs-lookup"><span data-stu-id="98c8c-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-146">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-146">Symptom</span></span>

<span data-ttu-id="98c8c-147">Você vê a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-147">You receive the following error message:</span></span>

<span data-ttu-id="98c8c-148">**Erro de download do arquivo. O URI de destino não foi especificado.**</span><span class="sxs-lookup"><span data-stu-id="98c8c-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-149">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-149">Cause</span></span> 

<span data-ttu-id="98c8c-150">Esse problema ocorre devido ao tipo de gateway incorreto.</span><span class="sxs-lookup"><span data-stu-id="98c8c-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="98c8c-151">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-151">Solution</span></span>

<span data-ttu-id="98c8c-152">O tipo de gateway de VPN deve ser **VPN**, enquanto o tipo de VPN deve ser **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="98c8c-153">Erro de cliente VPN: falha de script personalizado do VPN Azure</span><span class="sxs-lookup"><span data-stu-id="98c8c-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="98c8c-154">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-154">Symptom</span></span>

<span data-ttu-id="98c8c-155">Quando você tenta conectar-se à rede virtual do Azure usando o cliente VPN, recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="98c8c-156">**Falha de script personalizado (para atualizar sua tabela de roteamento). (Erro 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="98c8c-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-157">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-157">Cause</span></span>

<span data-ttu-id="98c8c-158">Esse problema poderá ocorrer se você estiver tentando abrir a conexão VPN site a ponto usando um atalho.</span><span class="sxs-lookup"><span data-stu-id="98c8c-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-159">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-159">Solution</span></span> 

<span data-ttu-id="98c8c-160">Abra o pacote VPN diretamente em vez de abri-lo pelo atalho.</span><span class="sxs-lookup"><span data-stu-id="98c8c-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="98c8c-161">Não é possível instalar o cliente VPN</span><span class="sxs-lookup"><span data-stu-id="98c8c-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-162">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-162">Cause</span></span> 

<span data-ttu-id="98c8c-163">Um certificado adicional é necessário para confiar no gateway de VPN da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="98c8c-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="98c8c-164">O certificado está incluído no pacote de configuração de cliente VPN que é gerado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="98c8c-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-165">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-165">Solution</span></span>

<span data-ttu-id="98c8c-166">Extraia o pacote de configuração do cliente VPN e localize o arquivo .cer.</span><span class="sxs-lookup"><span data-stu-id="98c8c-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="98c8c-167">Para instalar o certificado, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="98c8c-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="98c8c-168">Abra mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="98c8c-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="98c8c-169">Adicione o snap-in **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="98c8c-170">Selecione a conta **Computador** para o computador local.</span><span class="sxs-lookup"><span data-stu-id="98c8c-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="98c8c-171">Clique com botão direito do mouse no nó **Autoridades de Certificação Confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="98c8c-172">Clique em **All-Task** > **Import** e navegue até o arquivo .cer que você extraiu do pacote de configuração do cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="98c8c-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="98c8c-173">Reinicie o computador.</span><span class="sxs-lookup"><span data-stu-id="98c8c-173">Restart the computer.</span></span> 
6. <span data-ttu-id="98c8c-174">Tente instalar o cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="98c8c-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="98c8c-175">Erro de portal do Azure: falha ao salvar o gateway de VPN e os dados são inválidos</span><span class="sxs-lookup"><span data-stu-id="98c8c-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-176">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-176">Symptom</span></span>

<span data-ttu-id="98c8c-177">Quando você tenta salvar as alterações do gateway de VPN no portal do Azure, recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="98c8c-178">**Falha ao salvar o gateway de rede virtual &lt;*nome do gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="98c8c-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="98c8c-179">Os dados para o certificado &lt;*ID do certificado*&gt; são inválidos.**</span><span class="sxs-lookup"><span data-stu-id="98c8c-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-180">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-180">Cause</span></span> 

<span data-ttu-id="98c8c-181">Esse problema poderá ocorrer se a chave pública do certificado raiz que você carregou contiver caracteres inválidos, como espaço.</span><span class="sxs-lookup"><span data-stu-id="98c8c-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-182">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-182">Solution</span></span>

<span data-ttu-id="98c8c-183">Verifique se os dados no certificado não contêm caracteres inválidos, como quebras de linha (retornos de carro).</span><span class="sxs-lookup"><span data-stu-id="98c8c-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="98c8c-184">O valor inteiro deve estar em uma linha longa.</span><span class="sxs-lookup"><span data-stu-id="98c8c-184">The entire value should be one long line.</span></span> <span data-ttu-id="98c8c-185">O texto abaixo é um exemplo de certificado:</span><span class="sxs-lookup"><span data-stu-id="98c8c-185">The following text is a sample of the certificate:</span></span>

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

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="98c8c-186">Erro do portal do Azure: falha ao salvar gateway de VPN e o nome do recurso é inválido</span><span class="sxs-lookup"><span data-stu-id="98c8c-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-187">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-187">Symptom</span></span>

<span data-ttu-id="98c8c-188">Quando você tenta salvar as alterações do gateway de VPN no portal do Azure, recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="98c8c-189">**Falha ao salvar o gateway de rede virtual &lt;*nome do gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="98c8c-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="98c8c-190">Nome do recurso &lt;*o nome do certificado que você tenta carregar*&gt; é inválido**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-191">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-191">Cause</span></span>

<span data-ttu-id="98c8c-192">Esse problema ocorre porque o nome do certificado contém um caractere inválido, como um espaço.</span><span class="sxs-lookup"><span data-stu-id="98c8c-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="98c8c-193">Erro 503 de portal do Azure: erro de download do arquivo do pacote VPN</span><span class="sxs-lookup"><span data-stu-id="98c8c-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-194">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-194">Symptom</span></span>

<span data-ttu-id="98c8c-195">Ao tentar baixar o pacote de configuração de cliente VPN, você recebe a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="98c8c-196">**Falha ao baixar o arquivo. Detalhes do erro: erro 503. O servidor está ocupado.**</span><span class="sxs-lookup"><span data-stu-id="98c8c-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="98c8c-197">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-197">Solution</span></span>

<span data-ttu-id="98c8c-198">Esse erro pode ser causado por um problema de rede temporário.</span><span class="sxs-lookup"><span data-stu-id="98c8c-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="98c8c-199">Tente baixar o pacote VPN novamente após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="98c8c-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="98c8c-200">Atualização de Gateway de VPN do Azure: nenhum dos clientes P2S consegue se conectar</span><span class="sxs-lookup"><span data-stu-id="98c8c-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-201">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-201">Cause</span></span>

<span data-ttu-id="98c8c-202">Se o certificado passou de 50% de seu tempo de vida, o certificado é substituído.</span><span class="sxs-lookup"><span data-stu-id="98c8c-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-203">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-203">Solution</span></span>

<span data-ttu-id="98c8c-204">Para resolver esse problema, crie e redistribua os novos certificados para os clientes VPN.</span><span class="sxs-lookup"><span data-stu-id="98c8c-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="98c8c-205">Muitos clientes VPN conectados ao mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="98c8c-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="98c8c-206">Para cada gateway de VPN, o número máximo de conexões permitidas é de 128.</span><span class="sxs-lookup"><span data-stu-id="98c8c-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="98c8c-207">Você pode ver o número total de clientes conectados no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="98c8c-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="98c8c-208">A VPN ponto a site adiciona incorretamente uma rota para 10.0.0.0/8 à tabela de rotas</span><span class="sxs-lookup"><span data-stu-id="98c8c-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-209">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-209">Symptom</span></span>

<span data-ttu-id="98c8c-210">Quando você disca a conexão VPN no cliente ponto a site, o cliente VPN deve adicionar uma rota para a rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="98c8c-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="98c8c-211">O serviço auxiliar de IP deve adicionar uma rota para a sub-rede dos clientes VPN.</span><span class="sxs-lookup"><span data-stu-id="98c8c-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="98c8c-212">O intervalo de cliente VPN pertence a uma sub-rede menor de 10.0.0.0/8, como 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="98c8c-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="98c8c-213">Em vez de uma rota para 10.0.12.0/24, é adicionada uma rota para 10.0.0.0/8 que tem prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="98c8c-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="98c8c-214">Essa rota incorreta interrompe a conectividade com outras redes locais que podem pertencer a outra sub-rede dentro no intervalo 10.0.0.0/8, como 10.50.0.0/24, que não tenham uma rota específica definida.</span><span class="sxs-lookup"><span data-stu-id="98c8c-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="98c8c-215">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-215">Cause</span></span>

<span data-ttu-id="98c8c-216">Esse comportamento ocorre por padrão para clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="98c8c-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="98c8c-217">Quando o cliente usa o protocolo PPP IPCP, ele obtém o endereço IP para a interface de túnel do servidor (gateway de VPN, neste caso).</span><span class="sxs-lookup"><span data-stu-id="98c8c-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="98c8c-218">No entanto, devido a uma limitação no protocolo, o cliente não tem a máscara de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="98c8c-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="98c8c-219">Como não há nenhuma outra forma de obtê-la, o cliente tenta adivinhar a máscara de sub-rede com base na classe do endereço IP da interface do túnel.</span><span class="sxs-lookup"><span data-stu-id="98c8c-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="98c8c-220">Portanto, uma rota é adicionada com base no seguinte mapeamento estático:</span><span class="sxs-lookup"><span data-stu-id="98c8c-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="98c8c-221">Se o endereço pertence à classe A--> aplicar /8</span><span class="sxs-lookup"><span data-stu-id="98c8c-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="98c8c-222">Se o endereço pertencer à classe B --> aplicar /16</span><span class="sxs-lookup"><span data-stu-id="98c8c-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="98c8c-223">Se o endereço pertence à classe C--> aplicar /24</span><span class="sxs-lookup"><span data-stu-id="98c8c-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="98c8c-224">O cliente VPN não pode acessar compartilhamentos de arquivos de rede</span><span class="sxs-lookup"><span data-stu-id="98c8c-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-225">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-225">Symptom</span></span>

<span data-ttu-id="98c8c-226">O cliente VPN foi conectado à rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="98c8c-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="98c8c-227">No entanto, o cliente não pode acessar compartilhamentos de rede.</span><span class="sxs-lookup"><span data-stu-id="98c8c-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="98c8c-228">Causa</span><span class="sxs-lookup"><span data-stu-id="98c8c-228">Cause</span></span>

<span data-ttu-id="98c8c-229">O protocolo SMB é usado para acesso de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="98c8c-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="98c8c-230">Quando a conexão é iniciada, o cliente VPN adiciona as credenciais da sessão e a falha ocorre.</span><span class="sxs-lookup"><span data-stu-id="98c8c-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="98c8c-231">Depois que a conexão é estabelecida, o cliente é forçado a usar as credenciais de cache para a autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="98c8c-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="98c8c-232">Esse processo inicia consultas para o Centro de Distribuição de Chaves (um controlador de domínio) para obter um token.</span><span class="sxs-lookup"><span data-stu-id="98c8c-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="98c8c-233">Uma vez que o cliente conecta-se pela Internet, ele pode não conseguir alcançar o controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="98c8c-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="98c8c-234">Portanto, o cliente não pode fazer failover do Kerberos para NTLM.</span><span class="sxs-lookup"><span data-stu-id="98c8c-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="98c8c-235">A única vez em que o cliente é solicitado a fornecer uma credencial é quando ele tem um certificado válido (com SAN = UPN) emitido pelo domínio ao qual ele está associado.</span><span class="sxs-lookup"><span data-stu-id="98c8c-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="98c8c-236">O cliente também deve estar fisicamente conectado à rede de domínio.</span><span class="sxs-lookup"><span data-stu-id="98c8c-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="98c8c-237">Nesse caso, o cliente tenta usar o certificado e busca o controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="98c8c-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="98c8c-238">Então o Centro de distribuição de chaves retorna um erro de "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="98c8c-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="98c8c-239">O cliente é forçado a fazer failover para NTLM.</span><span class="sxs-lookup"><span data-stu-id="98c8c-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="98c8c-240">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-240">Solution</span></span>

<span data-ttu-id="98c8c-241">Para contornar o problema, desabilite o cache de credenciais de domínio da seguinte subchave do registro:</span><span class="sxs-lookup"><span data-stu-id="98c8c-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="98c8c-242">Não é possível localizar a conexão VPN ponto a site no Windows após a reinstalação do cliente VPN</span><span class="sxs-lookup"><span data-stu-id="98c8c-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="98c8c-243">Sintoma</span><span class="sxs-lookup"><span data-stu-id="98c8c-243">Symptom</span></span>

<span data-ttu-id="98c8c-244">Você remove a conexão VPN ponto a site e reinstala o cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="98c8c-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="98c8c-245">Nessa situação, a conexão VPN não foi configurada com êxito.</span><span class="sxs-lookup"><span data-stu-id="98c8c-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="98c8c-246">Você não vê a conexão VPN nas configurações **Conexões de rede** do Windows.</span><span class="sxs-lookup"><span data-stu-id="98c8c-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="98c8c-247">Solução</span><span class="sxs-lookup"><span data-stu-id="98c8c-247">Solution</span></span>

<span data-ttu-id="98c8c-248">Para resolver o problema, exclua os arquivos de configuração de cliente VPN antigos de **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections** e execute novamente o instalador do cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="98c8c-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
