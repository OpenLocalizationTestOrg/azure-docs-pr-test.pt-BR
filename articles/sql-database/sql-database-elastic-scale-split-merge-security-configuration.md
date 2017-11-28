---
title: "Configuração de segurança da divisão e mesclagem | Microsoft Docs"
description: Configurar certificados x409 para criptografia
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="26947-103">Configuração de segurança da divisão e mesclagem</span><span class="sxs-lookup"><span data-stu-id="26947-103">Split-merge security configuration</span></span>
<span data-ttu-id="26947-104">Para usar o serviço de divisão/mesclagem, você deve configurar corretamente a segurança.</span><span class="sxs-lookup"><span data-stu-id="26947-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="26947-105">O serviço é parte do recurso de Dimensionamento Elástico do Banco de Dados SQL do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="26947-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="26947-106">Para saber mais, confira o [Tutorial do serviço de divisão e mesclagem da escala elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="26947-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="26947-107">Configurando certificados</span><span class="sxs-lookup"><span data-stu-id="26947-107">Configuring certificates</span></span>
<span data-ttu-id="26947-108">Os certificados são configurados de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="26947-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="26947-109">Para configurar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="26947-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="26947-110">Para configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="26947-111">Para obter certificados</span><span class="sxs-lookup"><span data-stu-id="26947-111">To obtain certificates</span></span>
<span data-ttu-id="26947-112">Certificados podem ser obtidos por meio de autoridades de certificação públicas (CAs) ou do [Serviço de Certificado do Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="26947-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="26947-113">Esses são os métodos preferenciais para obter certificados.</span><span class="sxs-lookup"><span data-stu-id="26947-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="26947-114">Se essas opções não estiverem disponíveis, você pode gerar **certificados autoassinados**.</span><span class="sxs-lookup"><span data-stu-id="26947-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="26947-115">Ferramentas para gerar certificados</span><span class="sxs-lookup"><span data-stu-id="26947-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="26947-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="26947-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="26947-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="26947-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="26947-118">Para executar as ferramentas</span><span class="sxs-lookup"><span data-stu-id="26947-118">To run the tools</span></span>
* <span data-ttu-id="26947-119">De um Prompt de Comando do Desenvolvedor para o Visual Studio, consulte o [Prompt de Comando do Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="26947-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="26947-120">Se instalado, vá para:</span><span class="sxs-lookup"><span data-stu-id="26947-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="26947-121">Obter o WDK do [Windows 8.1: baixar kits e ferramentas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="26947-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="26947-122">Para configurar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="26947-122">To configure the SSL certificate</span></span>
<span data-ttu-id="26947-123">É necessário um certificado SSL para criptografar a comunicação e autenticar o servidor.</span><span class="sxs-lookup"><span data-stu-id="26947-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="26947-124">Escolha um dos três cenários abaixo mais aplicável e execute todas as suas etapas:</span><span class="sxs-lookup"><span data-stu-id="26947-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="26947-125">Criar um Novo certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="26947-126">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="26947-127">Criar o arquivo PFX para o certificado SSL autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="26947-128">Carregar certificado SSL para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="26947-129">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="26947-130">Importar a autoridade de certificação SSL</span><span class="sxs-lookup"><span data-stu-id="26947-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="26947-131">Para usar um certificado existente do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="26947-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="26947-132">Exportar o certificado SSL do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="26947-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="26947-133">Carregar certificado SSL para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="26947-134">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="26947-135">Para usar um certificado existente em um arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="26947-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="26947-136">Carregar certificado SSL para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="26947-137">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="26947-138">Para configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-138">To configure client certificates</span></span>
<span data-ttu-id="26947-139">Certificados de cliente são necessários para autenticar solicitações ao serviço.</span><span class="sxs-lookup"><span data-stu-id="26947-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="26947-140">Escolha um dos três cenários abaixo mais aplicável e execute todas as suas etapas:</span><span class="sxs-lookup"><span data-stu-id="26947-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="26947-141">Desabilitar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="26947-142">Desabilitar a autenticação baseada em certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="26947-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="26947-143">Emitir novos certificados de cliente autoassinados</span><span class="sxs-lookup"><span data-stu-id="26947-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="26947-144">Criar uma Autoridade de certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="26947-145">Carregar o Certificado de Autoridade de Certificação no serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="26947-146">Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="26947-147">Emitir certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="26947-148">Criar arquivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="26947-149">Importar o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="26947-150">Copie as impressões digitais de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="26947-151">Configurar clientes permitidos no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="26947-152">Usar certificados de cliente existente</span><span class="sxs-lookup"><span data-stu-id="26947-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="26947-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="26947-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="26947-154">Carregar o Certificado de Autoridade de Certificação no serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="26947-155">Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="26947-156">Copie as impressões digitais de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="26947-157">Configurar clientes permitidos no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="26947-158">Configurar a verificação de revogação de certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="26947-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="26947-159">Endereços IP permitidos</span><span class="sxs-lookup"><span data-stu-id="26947-159">Allowed IP addresses</span></span>
<span data-ttu-id="26947-160">Acesso aos pontos de extremidade de serviço pode ser restrito a intervalos específicos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="26947-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="26947-161">Configurar a criptografia para o armazenamento</span><span class="sxs-lookup"><span data-stu-id="26947-161">To configure encryption for the store</span></span>
<span data-ttu-id="26947-162">É necessário um certificado para criptografar as credenciais que são armazenadas no repositório de metadados.</span><span class="sxs-lookup"><span data-stu-id="26947-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="26947-163">Escolha um dos três cenários abaixo mais aplicável e execute todas as suas etapas:</span><span class="sxs-lookup"><span data-stu-id="26947-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="26947-164">Usar um novo certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="26947-165">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="26947-166">Criar arquivo PFX de certificado de criptografia autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="26947-167">Carregar o certificado de criptografia para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="26947-168">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="26947-169">Usar um certificado existente no repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="26947-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="26947-170">Exportar o certificado de criptografia do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="26947-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="26947-171">Carregar o certificado de criptografia para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="26947-172">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="26947-173">Usar um certificado existente em um arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="26947-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="26947-174">Carregar o certificado de criptografia para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="26947-175">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="26947-176">A configuração padrão</span><span class="sxs-lookup"><span data-stu-id="26947-176">The default configuration</span></span>
<span data-ttu-id="26947-177">A configuração padrão nega todo os acessos ao ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="26947-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="26947-178">Esta é a configuração recomendada, pois as solicitações para esses pontos de extremidade podem carregar informações confidenciais, como credenciais de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="26947-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="26947-179">A configuração padrão permite todo os acessos ao ponto de extremidade HTTPS.</span><span class="sxs-lookup"><span data-stu-id="26947-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="26947-180">Essa configuração pode ser mais restrita.</span><span class="sxs-lookup"><span data-stu-id="26947-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="26947-181">Alterando a configuração</span><span class="sxs-lookup"><span data-stu-id="26947-181">Changing the Configuration</span></span>
<span data-ttu-id="26947-182">O grupo de regras de controle de acesso que são aplicadas e o ponto de extremidade são configurados na seção **<EndpointAcls>** no **arquivo de configuração de serviço**.</span><span class="sxs-lookup"><span data-stu-id="26947-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="26947-183">As regras em um grupo de controle de acesso são configuradas em uma seção de <AccessControl name=""> do arquivo de configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="26947-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="26947-184">O formato é explicado na documentação de listas de controle de acesso à rede.</span><span class="sxs-lookup"><span data-stu-id="26947-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="26947-185">Por exemplo, para permitir que apenas IPs no intervalo 100.100.0.0 para 100.100.255.255 acessem o ponto de extremidade HTTPS, as regras teriam esta aparência:</span><span class="sxs-lookup"><span data-stu-id="26947-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="26947-186">Negação de prevenção de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-186">Denial of service prevention</span></span>
<span data-ttu-id="26947-187">Há dois mecanismos diferentes com suporte para detectar e impedir ataques de negação de serviço:</span><span class="sxs-lookup"><span data-stu-id="26947-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="26947-188">Restringir o número de solicitações simultâneas por host remoto (desativado por padrão)</span><span class="sxs-lookup"><span data-stu-id="26947-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="26947-189">Restringir a taxa de acesso por host remoto (em por padrão)</span><span class="sxs-lookup"><span data-stu-id="26947-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="26947-190">Eles se baseiam nos recursos documentados mais adiante na segurança de IP dinâmico no IIS.</span><span class="sxs-lookup"><span data-stu-id="26947-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="26947-191">Ao alterar essa configuração Lembre-se dos seguintes fatores:</span><span class="sxs-lookup"><span data-stu-id="26947-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="26947-192">O comportamento de proxies e dispositivos de conversão de endereços de rede sobre as informações do host remoto</span><span class="sxs-lookup"><span data-stu-id="26947-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="26947-193">Cada solicitação para qualquer recurso na função web é considerada (por exemplo, carregamento de scripts, imagens, etc)</span><span class="sxs-lookup"><span data-stu-id="26947-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="26947-194">Restringir o número de acessos simultâneos</span><span class="sxs-lookup"><span data-stu-id="26947-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="26947-195">As configurações que configuram esse comportamento são:</span><span class="sxs-lookup"><span data-stu-id="26947-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="26947-196">Alterar DynamicIpRestrictionDenyByConcurrentRequests como verdadeiro (true) para habilitar essa proteção.</span><span class="sxs-lookup"><span data-stu-id="26947-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="26947-197">Restringindo a taxa de acesso</span><span class="sxs-lookup"><span data-stu-id="26947-197">Restricting rate of access</span></span>
<span data-ttu-id="26947-198">As configurações que configuram esse comportamento são:</span><span class="sxs-lookup"><span data-stu-id="26947-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="26947-199">Configurando a resposta para uma solicitação negada</span><span class="sxs-lookup"><span data-stu-id="26947-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="26947-200">A configuração a seguir configura a resposta para uma solicitação negada:</span><span class="sxs-lookup"><span data-stu-id="26947-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="26947-201">Consulte a documentação de segurança de IP dinâmico no IIS para outros valores com suporte.</span><span class="sxs-lookup"><span data-stu-id="26947-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="26947-202">Operações para configurar certificados de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="26947-203">Este tópico é apenas para referência.</span><span class="sxs-lookup"><span data-stu-id="26947-203">This topic is for reference only.</span></span> <span data-ttu-id="26947-204">Siga as etapas de configuração descritas em:</span><span class="sxs-lookup"><span data-stu-id="26947-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="26947-205">Configurar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="26947-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="26947-206">Configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="26947-207">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-207">Create a self-signed certificate</span></span>
<span data-ttu-id="26947-208">Execute:</span><span class="sxs-lookup"><span data-stu-id="26947-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="26947-209">Para personalizar:</span><span class="sxs-lookup"><span data-stu-id="26947-209">To customize:</span></span>

* <span data-ttu-id="26947-210">-n com a URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="26947-210">-n with the service URL.</span></span> <span data-ttu-id="26947-211">Há suporte para caracteres curinga ("CN=*.cloudapp .net") e nomes alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").</span><span class="sxs-lookup"><span data-stu-id="26947-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="26947-212">-e com a data de validade do certificado Criar uma senha forte e especifique-a quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="26947-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="26947-213">Criar o arquivo PFX para o certificado SSL autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="26947-214">Execute:</span><span class="sxs-lookup"><span data-stu-id="26947-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="26947-215">Digite a senha e, em seguida, exporte o certificado com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="26947-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="26947-216">Sim, exportar a chave privada</span><span class="sxs-lookup"><span data-stu-id="26947-216">Yes, export the private key</span></span>
* <span data-ttu-id="26947-217">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="26947-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="26947-218">Exportar o certificado SSL do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="26947-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="26947-219">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-219">Find certificate</span></span>
* <span data-ttu-id="26947-220">Clique em Ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="26947-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="26947-221">Exportar o certificado em um arquivo .PFX com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="26947-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="26947-222">Sim, exportar a chave privada</span><span class="sxs-lookup"><span data-stu-id="26947-222">Yes, export the private key</span></span>
  * <span data-ttu-id="26947-223">Incluir todos os certificados no caminho de certificação, se possível *Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="26947-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="26947-224">Carregar certificado SSL para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="26947-225">Carregar certificado com o arquivo .PFX existente ou gerado com o par de chaves SSL:</span><span class="sxs-lookup"><span data-stu-id="26947-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="26947-226">Digite a senha que protege as informações da chave privadas</span><span class="sxs-lookup"><span data-stu-id="26947-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="26947-227">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="26947-228">Atualize o valor de impressão digital da seguinte configuração no arquivo de configuração de serviço com a impressão digital do certificado carregado para o serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="26947-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="26947-229">Importar a autoridade de certificação SSL</span><span class="sxs-lookup"><span data-stu-id="26947-229">Import SSL certification authority</span></span>
<span data-ttu-id="26947-230">Siga estas etapas em todas as contas/computadores que se comunicarão com o serviço:</span><span class="sxs-lookup"><span data-stu-id="26947-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="26947-231">Clique duas vezes no arquivo .CER no Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="26947-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="26947-232">Na caixa de diálogo do certificado, clique em Instalar certificado...</span><span class="sxs-lookup"><span data-stu-id="26947-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="26947-233">Importar certificados para o armazenamento de Autoridades de Certificação Confiáveis</span><span class="sxs-lookup"><span data-stu-id="26947-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="26947-234">Desabilitar a autenticação baseada em certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="26947-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="26947-235">Há suporte somente para autenticação com base em certificado de cliente e desabilitá-la permitirá acesso público para os pontos de extremidade do serviço, a menos que outros mecanismos estão em vigor (por exemplo, Rede Virtual do Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="26947-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="26947-236">Altere essas configurações para false no arquivo de configuração de serviço para desativar o recurso:</span><span class="sxs-lookup"><span data-stu-id="26947-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="26947-237">Em seguida, copie a mesma impressão digital do certificado SSL na configuração do Certificado de Autoridade de Certificação:</span><span class="sxs-lookup"><span data-stu-id="26947-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="26947-238">Criar uma Autoridade de certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="26947-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="26947-239">Execute as seguintes etapas para criar um certificado autoassinado para atuar como uma autoridade de certificação:</span><span class="sxs-lookup"><span data-stu-id="26947-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="26947-240">Para personalizá-lo</span><span class="sxs-lookup"><span data-stu-id="26947-240">To customize it</span></span>

* <span data-ttu-id="26947-241">-e com a data de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="26947-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="26947-242">Localizar a chave pública da autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="26947-242">Find CA public key</span></span>
<span data-ttu-id="26947-243">Todos os certificados de cliente devem ter sido emitidos por uma autoridade de certificação confiável pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="26947-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="26947-244">Localize a chave pública para a autoridade de certificação que emitiu o cliente certificados a ser usado para autenticação para carregá-lo ao serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="26947-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="26947-245">Se o arquivo com a chave pública não estiver disponível, você deve exportá-lo a partir do repositório de certificados:</span><span class="sxs-lookup"><span data-stu-id="26947-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="26947-246">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-246">Find certificate</span></span>
  * <span data-ttu-id="26947-247">Pesquise um certificado de cliente emitido pela mesma autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="26947-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="26947-248">Clique duas vezes no certificado.</span><span class="sxs-lookup"><span data-stu-id="26947-248">Double-click the certificate.</span></span>
* <span data-ttu-id="26947-249">Selecione a guia do Caminho de Certificação na caixa de diálogo de Certificado.</span><span class="sxs-lookup"><span data-stu-id="26947-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="26947-250">Clique duas vezes na entrada de AC no caminho.</span><span class="sxs-lookup"><span data-stu-id="26947-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="26947-251">Anote as propriedades do certificado.</span><span class="sxs-lookup"><span data-stu-id="26947-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="26947-252">Feche a caixa de diálogo do **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="26947-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="26947-253">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-253">Find certificate</span></span>
  * <span data-ttu-id="26947-254">Pesquise pela AC anotada acima.</span><span class="sxs-lookup"><span data-stu-id="26947-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="26947-255">Clique em Ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="26947-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="26947-256">Exportar o certificado em um .CER com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="26947-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="26947-257">**Não, não exportar a chave privada**</span><span class="sxs-lookup"><span data-stu-id="26947-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="26947-258">Incluir todos os certificados no caminho de certificação, se possível.</span><span class="sxs-lookup"><span data-stu-id="26947-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="26947-259">Exportar todas as propriedades estendidas.</span><span class="sxs-lookup"><span data-stu-id="26947-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="26947-260">Carregar o Certificado de Autoridade de Certificação no serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="26947-261">Carregar certificado com o arquivo .CER existente ou gerado com a chave pública da autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="26947-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="26947-262">Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="26947-263">Atualize o valor de impressão digital da seguinte configuração no arquivo de configuração de serviço com a impressão digital do certificado carregado para o serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="26947-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="26947-264">Atualize o valor de configuração a seguir com a mesma impressão digital:</span><span class="sxs-lookup"><span data-stu-id="26947-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="26947-265">Emitir certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-265">Issue client certificates</span></span>
<span data-ttu-id="26947-266">Cada pessoa autorizada a acessar o serviço deve ter um certificado de cliente emitido para seu uso exclusivo e deve escolher que sua própria senha forte para proteger sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="26947-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="26947-267">As etapas a seguir devem ser executadas no mesmo computador onde o Certificado de Autoridade de Certificação autoassinado foi gerado e armazenado:</span><span class="sxs-lookup"><span data-stu-id="26947-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="26947-268">Personalizando:</span><span class="sxs-lookup"><span data-stu-id="26947-268">Customizing:</span></span>

* <span data-ttu-id="26947-269">-n com uma ID para o cliente será autenticado com o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="26947-270">-e com a data de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="26947-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="26947-271">MyID.pvk e MyID.cer com nomes de arquivo exclusivo para o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="26947-272">Esse comando solicitará uma senha a ser criada e usada uma vez.</span><span class="sxs-lookup"><span data-stu-id="26947-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="26947-273">Use uma senha forte.</span><span class="sxs-lookup"><span data-stu-id="26947-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="26947-274">Criar arquivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="26947-275">Para cada certificado de cliente gerado, execute:</span><span class="sxs-lookup"><span data-stu-id="26947-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="26947-276">Personalizando:</span><span class="sxs-lookup"><span data-stu-id="26947-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="26947-277">Digite a senha e, em seguida, exporte o certificado com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="26947-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="26947-278">Sim, exportar a chave privada</span><span class="sxs-lookup"><span data-stu-id="26947-278">Yes, export the private key</span></span>
* <span data-ttu-id="26947-279">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="26947-279">Export all extended properties</span></span>
* <span data-ttu-id="26947-280">A pessoa para quem o certificado foi emitido deve escolher a senha de exportação</span><span class="sxs-lookup"><span data-stu-id="26947-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="26947-281">Importar o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-281">Import client certificate</span></span>
<span data-ttu-id="26947-282">Cada pessoa para quem um certificado cliente tiver sido emitido deve importar o par de chaves nas máquinas que ele usará para se comunicar com o serviço:</span><span class="sxs-lookup"><span data-stu-id="26947-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="26947-283">Clique duas vezes no arquivo .PFX no Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="26947-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="26947-284">Importar o certificado para o pessoal armazenar pelo menos essa opção:</span><span class="sxs-lookup"><span data-stu-id="26947-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="26947-285">Incluir todas as propriedades estendidas marcadas</span><span class="sxs-lookup"><span data-stu-id="26947-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="26947-286">Copie as impressões digitais de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="26947-287">Cada pessoa para quem um certificado cliente tiver sido emitido deve seguir estas etapas para obter a impressão digital do seu certificado que será adicionado ao arquivo de configuração de serviço:</span><span class="sxs-lookup"><span data-stu-id="26947-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="26947-288">Executar certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="26947-288">Run certmgr.exe</span></span>
* <span data-ttu-id="26947-289">Selecione a guia pessoal</span><span class="sxs-lookup"><span data-stu-id="26947-289">Select the Personal tab</span></span>
* <span data-ttu-id="26947-290">Clique duas vezes no certificado do cliente para ser usado para autenticação</span><span class="sxs-lookup"><span data-stu-id="26947-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="26947-291">Na caixa de diálogo certificado é aberta, selecione a guia Detalhes</span><span class="sxs-lookup"><span data-stu-id="26947-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="26947-292">Certifique-se de que mostrar está exibindo todos</span><span class="sxs-lookup"><span data-stu-id="26947-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="26947-293">Selecione o campo denominado impressão digital na lista</span><span class="sxs-lookup"><span data-stu-id="26947-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="26947-294">Copie o valor da impressão digital ** Exclua caracteres Unicode não visíveis na frente do primeiro dígito ** Exclua todos os espaços</span><span class="sxs-lookup"><span data-stu-id="26947-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="26947-295">Configurar clientes permitidos no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="26947-296">Atualize o valor da configuração a seguir no arquivo de configuração de serviço com uma lista separada por vírgulas das impressões digitais dos certificados do cliente pode acessar o serviço:</span><span class="sxs-lookup"><span data-stu-id="26947-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="26947-297">Configurar a verificação de revogação de certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="26947-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="26947-298">A configuração padrão não verifica a autoridade de certificação para o status de revogação de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="26947-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="26947-299">Para ativar as verificações, se a autoridade de certificação que emitiu os certificados de cliente oferece suporte a essas verificações, altere a configuração a seguir com um dos valores definidos na enumeração X509RevocationMode:</span><span class="sxs-lookup"><span data-stu-id="26947-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="26947-300">Criar arquivo PFX para certificados de criptografia autoassinados</span><span class="sxs-lookup"><span data-stu-id="26947-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="26947-301">Para um certificado de criptografia, execute:</span><span class="sxs-lookup"><span data-stu-id="26947-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="26947-302">Personalizando:</span><span class="sxs-lookup"><span data-stu-id="26947-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="26947-303">Digite a senha e, em seguida, exporte o certificado com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="26947-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="26947-304">Sim, exportar a chave privada</span><span class="sxs-lookup"><span data-stu-id="26947-304">Yes, export the private key</span></span>
* <span data-ttu-id="26947-305">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="26947-305">Export all extended properties</span></span>
* <span data-ttu-id="26947-306">Você precisará da senha ao carregar o certificado para o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="26947-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="26947-307">Exportar o certificado de criptografia do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="26947-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="26947-308">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-308">Find certificate</span></span>
* <span data-ttu-id="26947-309">Clique em Ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="26947-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="26947-310">Exportar o certificado em um arquivo .PFX com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="26947-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="26947-311">Sim, exportar a chave privada</span><span class="sxs-lookup"><span data-stu-id="26947-311">Yes, export the private key</span></span>
  * <span data-ttu-id="26947-312">Incluir todos os certificados no caminho de certificação, se possível</span><span class="sxs-lookup"><span data-stu-id="26947-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="26947-313">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="26947-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="26947-314">Carregar o certificado de criptografia para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="26947-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="26947-315">Carregar certificado com o arquivo .PFX existente ou gerado com o par de chaves de criptografia:</span><span class="sxs-lookup"><span data-stu-id="26947-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="26947-316">Digite a senha que protege as informações da chave privadas</span><span class="sxs-lookup"><span data-stu-id="26947-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="26947-317">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="26947-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="26947-318">Atualize o valor de impressão digital das seguintes configurações no arquivo de configuração de serviço com a impressão digital do certificado carregado para o serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="26947-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="26947-319">Operações comuns de certificado</span><span class="sxs-lookup"><span data-stu-id="26947-319">Common certificate operations</span></span>
* <span data-ttu-id="26947-320">Configurar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="26947-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="26947-321">Configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="26947-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="26947-322">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-322">Find certificate</span></span>
<span data-ttu-id="26947-323">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="26947-323">Follow these steps:</span></span>

1. <span data-ttu-id="26947-324">Execute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="26947-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="26947-325">Arquivo -> Adicionar/Remover Snap-in...</span><span class="sxs-lookup"><span data-stu-id="26947-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="26947-326">Selecione **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="26947-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="26947-327">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="26947-327">Click **Add**.</span></span>
5. <span data-ttu-id="26947-328">Escolha o local do repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="26947-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="26947-329">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="26947-329">Click **Finish**.</span></span>
7. <span data-ttu-id="26947-330">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="26947-330">Click **OK**.</span></span>
8. <span data-ttu-id="26947-331">Expanda **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="26947-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="26947-332">Expanda o nó do repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="26947-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="26947-333">Expanda o nó filho Certificado.</span><span class="sxs-lookup"><span data-stu-id="26947-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="26947-334">Selecione um certificado na lista.</span><span class="sxs-lookup"><span data-stu-id="26947-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="26947-335">Exportar o certificado</span><span class="sxs-lookup"><span data-stu-id="26947-335">Export certificate</span></span>
<span data-ttu-id="26947-336">No **Assistente para Exportação de Certificados**:</span><span class="sxs-lookup"><span data-stu-id="26947-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="26947-337">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26947-337">Click **Next**.</span></span>
2. <span data-ttu-id="26947-338">Selecione **Sim** e **Exportar a chave privada**.</span><span class="sxs-lookup"><span data-stu-id="26947-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="26947-339">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26947-339">Click **Next**.</span></span>
4. <span data-ttu-id="26947-340">Selecione o formato de arquivo de saída desejado.</span><span class="sxs-lookup"><span data-stu-id="26947-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="26947-341">Marque as opções desejadas.</span><span class="sxs-lookup"><span data-stu-id="26947-341">Check the desired options.</span></span>
6. <span data-ttu-id="26947-342">Marque a **Senha**.</span><span class="sxs-lookup"><span data-stu-id="26947-342">Check **Password**.</span></span>
7. <span data-ttu-id="26947-343">Digite uma senha forte e confirme-a.</span><span class="sxs-lookup"><span data-stu-id="26947-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="26947-344">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26947-344">Click **Next**.</span></span>
9. <span data-ttu-id="26947-345">Digite ou procure um nome de arquivo onde o certificado deverá ser armazenado (use uma extensão .PFX).</span><span class="sxs-lookup"><span data-stu-id="26947-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="26947-346">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26947-346">Click **Next**.</span></span>
11. <span data-ttu-id="26947-347">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="26947-347">Click **Finish**.</span></span>
12. <span data-ttu-id="26947-348">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="26947-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="26947-349">Importar certificado</span><span class="sxs-lookup"><span data-stu-id="26947-349">Import certificate</span></span>
<span data-ttu-id="26947-350">No Assistente para importação de certificados:</span><span class="sxs-lookup"><span data-stu-id="26947-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="26947-351">Selecione o local do repositório.</span><span class="sxs-lookup"><span data-stu-id="26947-351">Select the store location.</span></span>
   
   * <span data-ttu-id="26947-352">Selecione **Usuário Atual** somente se processos em execução no atual usuário acessarão o serviço</span><span class="sxs-lookup"><span data-stu-id="26947-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="26947-353">Selecione **Computador Local** se outros processos no computador acessarão o serviço</span><span class="sxs-lookup"><span data-stu-id="26947-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="26947-354">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26947-354">Click **Next**.</span></span>
3. <span data-ttu-id="26947-355">Se estiver importando um arquivo, verifique seu caminho.</span><span class="sxs-lookup"><span data-stu-id="26947-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="26947-356">Se estiver importando um arquivo .PFX:</span><span class="sxs-lookup"><span data-stu-id="26947-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="26947-357">Digite a senha que protege as informações da chave privada</span><span class="sxs-lookup"><span data-stu-id="26947-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="26947-358">Selecione as opções de importação</span><span class="sxs-lookup"><span data-stu-id="26947-358">Select import options</span></span>
5. <span data-ttu-id="26947-359">Selecione para “Colocar” os certificados no repositório a seguir</span><span class="sxs-lookup"><span data-stu-id="26947-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="26947-360">Clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="26947-360">Click **Browse**.</span></span>
7. <span data-ttu-id="26947-361">Selecione o repositório desejado.</span><span class="sxs-lookup"><span data-stu-id="26947-361">Select the desired store.</span></span>
8. <span data-ttu-id="26947-362">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="26947-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="26947-363">Se o repositório da autoridade de certificação raiz confiável foi escolhido, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="26947-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="26947-364">Clique em **OK** em todas as janelas de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26947-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="26947-365">Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="26947-365">Upload certificate</span></span>
<span data-ttu-id="26947-366">No [Portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="26947-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="26947-367">Selecione os **Serviços de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="26947-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="26947-368">Selecione o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="26947-368">Select the cloud service.</span></span>
3. <span data-ttu-id="26947-369">Na parte superior do menu, clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="26947-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="26947-370">Na barra inferior, clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="26947-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="26947-371">Selecione o arquivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="26947-371">Select the certificate file.</span></span>
6. <span data-ttu-id="26947-372">Se for um arquivo .PFX, digite a senha da chave privada.</span><span class="sxs-lookup"><span data-stu-id="26947-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="26947-373">Depois de concluído, copie a impressão digital do certificado da nova entrada na lista.</span><span class="sxs-lookup"><span data-stu-id="26947-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="26947-374">Outras considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="26947-374">Other security considerations</span></span>
<span data-ttu-id="26947-375">As configurações de SSL descritas neste documento criptografar a comunicação entre o serviço e seus clientes quando o ponto de extremidade HTTPS é usado.</span><span class="sxs-lookup"><span data-stu-id="26947-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="26947-376">Isso é importante já que as credenciais para acesso ao banco de dados e potencialmente outras informações confidenciais estão contidos na comunicação.</span><span class="sxs-lookup"><span data-stu-id="26947-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="26947-377">No entanto, observe que o serviço persista status interno, incluindo credenciais, em suas tabelas internas no banco de dados SQL do Microsoft Azure que você forneceu para o armazenamento de metadados em sua assinatura do Microsoft Azurre.</span><span class="sxs-lookup"><span data-stu-id="26947-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="26947-378">Esse banco de dados foi definido como parte da seguinte configuração no arquivo de configuração de serviço (arquivo .CSCFG):</span><span class="sxs-lookup"><span data-stu-id="26947-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="26947-379">As credenciais armazenadas neste banco de dados são criptografadas.</span><span class="sxs-lookup"><span data-stu-id="26947-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="26947-380">No entanto, como uma prática recomendada, certifique-se de que funções da web e de trabalho de suas implantações de serviço sejam atualizadas e protegidas, visto que elas têm acesso ao banco de dados de metadados e o certificado usado para criptografia e descriptografia de credenciais armazenadas.</span><span class="sxs-lookup"><span data-stu-id="26947-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

