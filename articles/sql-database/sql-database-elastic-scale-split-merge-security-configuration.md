---
title: "configuração de segurança de mesclagem aaaSplit | Microsoft Docs"
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
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="70c7d-103">Configuração de segurança da divisão e mesclagem</span><span class="sxs-lookup"><span data-stu-id="70c7d-103">Split-merge security configuration</span></span>
<span data-ttu-id="70c7d-104">serviço de divisão/mesclagem de saudação toouse, você deve configurar corretamente segurança.</span><span class="sxs-lookup"><span data-stu-id="70c7d-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="70c7d-105">serviço de saudação é parte do recurso de escala elástica de saudação do banco de dados SQL do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="70c7d-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="70c7d-106">Para saber mais, confira o [Tutorial do serviço de divisão e mesclagem da escala elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="70c7d-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="70c7d-107">Configurando certificados</span><span class="sxs-lookup"><span data-stu-id="70c7d-107">Configuring certificates</span></span>
<span data-ttu-id="70c7d-108">Os certificados são configurados de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="70c7d-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="70c7d-109">Olá tooConfigure certificado SSL</span><span class="sxs-lookup"><span data-stu-id="70c7d-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="70c7d-110">tooConfigure certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="70c7d-111">tooobtain certificados</span><span class="sxs-lookup"><span data-stu-id="70c7d-111">tooobtain certificates</span></span>
<span data-ttu-id="70c7d-112">Certificados podem ser obtidos de autoridades de certificação pública (CAs) ou de saudação [o serviço de certificado do Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="70c7d-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="70c7d-113">Esses são Olá preferido métodos tooobtain certificados.</span><span class="sxs-lookup"><span data-stu-id="70c7d-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="70c7d-114">Se essas opções não estiverem disponíveis, você pode gerar **certificados autoassinados**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="70c7d-115">Certificados de toogenerate de ferramentas</span><span class="sxs-lookup"><span data-stu-id="70c7d-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="70c7d-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="70c7d-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="70c7d-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="70c7d-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="70c7d-118">ferramentas de saudação toorun</span><span class="sxs-lookup"><span data-stu-id="70c7d-118">toorun hello tools</span></span>
* <span data-ttu-id="70c7d-119">De um Prompt de Comando do Desenvolvedor para o Visual Studio, consulte o [Prompt de Comando do Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="70c7d-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="70c7d-120">Se instalado, vá para:</span><span class="sxs-lookup"><span data-stu-id="70c7d-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="70c7d-121">Obter Olá WDK do [Windows 8.1: baixar kits e ferramentas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="70c7d-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="70c7d-122">certificado SSL Olá tooconfigure</span><span class="sxs-lookup"><span data-stu-id="70c7d-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="70c7d-123">Um certificado SSL é necessário tooencrypt Olá comunicação e autenticar o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="70c7d-124">Escolha hello mais aplicável de saudação três cenários abaixo e execute todas as suas etapas:</span><span class="sxs-lookup"><span data-stu-id="70c7d-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="70c7d-125">Criar um Novo certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="70c7d-126">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="70c7d-127">Criar o arquivo PFX para o certificado SSL autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="70c7d-128">Carregar o certificado SSL tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="70c7d-129">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="70c7d-130">Importar a autoridade de certificação SSL</span><span class="sxs-lookup"><span data-stu-id="70c7d-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="70c7d-131">repositório de um certificado existente do certificado Olá toouse</span><span class="sxs-lookup"><span data-stu-id="70c7d-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="70c7d-132">Exportar o certificado SSL do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="70c7d-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="70c7d-133">Carregar o certificado SSL tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="70c7d-134">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="70c7d-135">toouse um certificado existente em um arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="70c7d-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="70c7d-136">Carregar o certificado SSL tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="70c7d-137">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="70c7d-138">certificados de cliente tooconfigure</span><span class="sxs-lookup"><span data-stu-id="70c7d-138">tooconfigure client certificates</span></span>
<span data-ttu-id="70c7d-139">Certificados de cliente são necessários na ordem tooauthenticate solicitações toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="70c7d-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="70c7d-140">Escolha hello mais aplicável de saudação três cenários abaixo e execute todas as suas etapas:</span><span class="sxs-lookup"><span data-stu-id="70c7d-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="70c7d-141">Desabilitar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="70c7d-142">Desabilitar a autenticação baseada em certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="70c7d-143">Emitir novos certificados de cliente autoassinados</span><span class="sxs-lookup"><span data-stu-id="70c7d-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="70c7d-144">Criar uma Autoridade de certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="70c7d-145">Carregar certificado de autoridade de certificação tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="70c7d-146">Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="70c7d-147">Emitir certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="70c7d-148">Criar arquivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="70c7d-149">Importar o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="70c7d-150">Copie as impressões digitais de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="70c7d-151">Configurar clientes permitido no hello arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="70c7d-152">Usar certificados de cliente existente</span><span class="sxs-lookup"><span data-stu-id="70c7d-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="70c7d-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="70c7d-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="70c7d-154">Carregar certificado de autoridade de certificação tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="70c7d-155">Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="70c7d-156">Copie as impressões digitais de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="70c7d-157">Configurar clientes permitido no hello arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="70c7d-158">Configurar a verificação de revogação de certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="70c7d-159">Endereços IP permitidos</span><span class="sxs-lookup"><span data-stu-id="70c7d-159">Allowed IP addresses</span></span>
<span data-ttu-id="70c7d-160">Pontos de extremidade de serviço de toohello acesso podem ser restrita toospecific intervalos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="70c7d-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="70c7d-161">criptografia tooconfigure para armazenamento de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="70c7d-162">Um certificado é necessário tooencrypt credenciais de Olá que são armazenadas no repositório de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="70c7d-163">Escolha hello mais aplicável de saudação três cenários abaixo e execute todas as suas etapas:</span><span class="sxs-lookup"><span data-stu-id="70c7d-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="70c7d-164">Usar um novo certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="70c7d-165">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="70c7d-166">Criar arquivo PFX de certificado de criptografia autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="70c7d-167">Carregar certificado de criptografia tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="70c7d-168">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="70c7d-169">Usar um certificado existente do repositório de certificados Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="70c7d-170">Exportar o certificado de criptografia do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="70c7d-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="70c7d-171">Carregar certificado de criptografia tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="70c7d-172">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="70c7d-173">Usar um certificado existente em um arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="70c7d-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="70c7d-174">Carregar certificado de criptografia tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="70c7d-175">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="70c7d-176">configuração padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-176">hello default configuration</span></span>
<span data-ttu-id="70c7d-177">configuração padrão de saudação nega o ponto de extremidade HTTP toohello de todos os acesso.</span><span class="sxs-lookup"><span data-stu-id="70c7d-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="70c7d-178">Isso é hello recomendado de configuração, como pontos de extremidade do hello solicitações toothese podem carregar informações confidenciais, como credenciais de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="70c7d-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="70c7d-179">configuração padrão de saudação permite que o ponto de extremidade HTTPS toohello de todos os acesso.</span><span class="sxs-lookup"><span data-stu-id="70c7d-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="70c7d-180">Essa configuração pode ser mais restrita.</span><span class="sxs-lookup"><span data-stu-id="70c7d-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="70c7d-181">Alterar configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-181">Changing hello Configuration</span></span>
<span data-ttu-id="70c7d-182">Olá grupo de regras de controle de acesso que se aplicam a tooand de ponto de extremidade são configurados no hello  **<EndpointAcls>**  seção Olá **arquivo de configuração do serviço**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="70c7d-183">regras de saudação em um grupo de controle de acesso são configuradas em um <AccessControl name=""> seção do arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="70c7d-184">formato de saudação é explicado na documentação de listas de controle de acesso à rede.</span><span class="sxs-lookup"><span data-stu-id="70c7d-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="70c7d-185">Por exemplo, tooallow apenas IPs em Olá intervalo 100.100.0.0 too100.100.255.255 tooaccess Olá ponto de extremidade HTTPS, regras de saudação teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="70c7d-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="70c7d-186">Negação de prevenção de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-186">Denial of service prevention</span></span>
<span data-ttu-id="70c7d-187">Há dois mecanismos diferentes suporte toodetect e evitar ataques de negação de serviço:</span><span class="sxs-lookup"><span data-stu-id="70c7d-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="70c7d-188">Restringir o número de solicitações simultâneas por host remoto (desativado por padrão)</span><span class="sxs-lookup"><span data-stu-id="70c7d-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="70c7d-189">Restringir a taxa de acesso por host remoto (em por padrão)</span><span class="sxs-lookup"><span data-stu-id="70c7d-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="70c7d-190">Eles se baseiam em recursos hello mais documentados na segurança de IP dinâmico no IIS.</span><span class="sxs-lookup"><span data-stu-id="70c7d-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="70c7d-191">Ao alterar essa configuração tenha cuidado com hello fatores a seguir:</span><span class="sxs-lookup"><span data-stu-id="70c7d-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="70c7d-192">comportamento de saudação de proxies e dispositivos de conversão de endereços de rede sobre informações de host remoto Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="70c7d-193">Cada recurso de tooany de solicitação em função da web de saudação é considerado (por exemplo, carregar scripts, imagens, etc)</span><span class="sxs-lookup"><span data-stu-id="70c7d-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="70c7d-194">Restringir o número de acessos simultâneos</span><span class="sxs-lookup"><span data-stu-id="70c7d-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="70c7d-195">configurações de saudação que configurar esse comportamento são:</span><span class="sxs-lookup"><span data-stu-id="70c7d-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="70c7d-196">Altere DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable essa proteção.</span><span class="sxs-lookup"><span data-stu-id="70c7d-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="70c7d-197">Restringindo a taxa de acesso</span><span class="sxs-lookup"><span data-stu-id="70c7d-197">Restricting rate of access</span></span>
<span data-ttu-id="70c7d-198">configurações de saudação que configurar esse comportamento são:</span><span class="sxs-lookup"><span data-stu-id="70c7d-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="70c7d-199">Configurar Olá resposta tooa negou a solicitação</span><span class="sxs-lookup"><span data-stu-id="70c7d-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="70c7d-200">Olá configuração a seguir configura Olá resposta tooa negada a solicitação:</span><span class="sxs-lookup"><span data-stu-id="70c7d-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="70c7d-201">Consulte a documentação do toohello para outros valores com suporte para segurança de IP dinâmico no IIS.</span><span class="sxs-lookup"><span data-stu-id="70c7d-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="70c7d-202">Operações para configurar certificados de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="70c7d-203">Este tópico é apenas para referência.</span><span class="sxs-lookup"><span data-stu-id="70c7d-203">This topic is for reference only.</span></span> <span data-ttu-id="70c7d-204">Siga etapas de configuração de saudação descritas no:</span><span class="sxs-lookup"><span data-stu-id="70c7d-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="70c7d-205">Configurar o certificado SSL Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="70c7d-206">Configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="70c7d-207">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-207">Create a self-signed certificate</span></span>
<span data-ttu-id="70c7d-208">Execute:</span><span class="sxs-lookup"><span data-stu-id="70c7d-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="70c7d-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="70c7d-209">toocustomize:</span></span>

* <span data-ttu-id="70c7d-210">URL do serviço - n com hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-210">-n with hello service URL.</span></span> <span data-ttu-id="70c7d-211">Há suporte para caracteres curinga ("CN=*.cloudapp .net") e nomes alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").</span><span class="sxs-lookup"><span data-stu-id="70c7d-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="70c7d-212">-e com data de validade do certificado Olá criar uma senha forte e especificá-lo quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="70c7d-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="70c7d-213">Criar o arquivo PFX para o certificado SSL autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="70c7d-214">Execute:</span><span class="sxs-lookup"><span data-stu-id="70c7d-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="70c7d-215">Digite a senha e, em seguida, exporte o certificado com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="70c7d-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="70c7d-216">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-216">Yes, export hello private key</span></span>
* <span data-ttu-id="70c7d-217">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="70c7d-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="70c7d-218">Exportar o certificado SSL do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="70c7d-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="70c7d-219">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-219">Find certificate</span></span>
* <span data-ttu-id="70c7d-220">Clique em Ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="70c7d-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="70c7d-221">Exportar o certificado em um arquivo .PFX com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="70c7d-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="70c7d-222">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="70c7d-223">Incluir todos os certificados no caminho de certificação Olá se possível * exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="70c7d-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="70c7d-224">Carregar o serviço de toocloud de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="70c7d-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="70c7d-225">Carregue o certificado com hello existente ou gerado. Arquivo PFX com hello par de chaves SSL:</span><span class="sxs-lookup"><span data-stu-id="70c7d-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="70c7d-226">Digite a senha de saudação protegendo informações de chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="70c7d-227">Atualizar o certificado SSL no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="70c7d-228">Atualize o valor de impressão digital de saudação do hello após a configuração no arquivo de configuração de serviço Olá com a impressão digital de Olá Olá certificado carregado toohello do serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="70c7d-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="70c7d-229">Importar a autoridade de certificação SSL</span><span class="sxs-lookup"><span data-stu-id="70c7d-229">Import SSL certification authority</span></span>
<span data-ttu-id="70c7d-230">Siga estas etapas em todas as contas/máquina que irá se comunicar com o serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="70c7d-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="70c7d-231">Clique duas vezes em hello. Arquivo CER no Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="70c7d-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="70c7d-232">Na caixa de diálogo de certificado hello, clique em Instalar certificado...</span><span class="sxs-lookup"><span data-stu-id="70c7d-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="70c7d-233">Importar o certificado para Olá que repositório de autoridades de certificação raiz confiáveis</span><span class="sxs-lookup"><span data-stu-id="70c7d-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="70c7d-234">Desabilitar a autenticação baseada em certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="70c7d-235">Somente o cliente baseada em certificado autenticação tem suporte e desabilitá-lo permitirá acesso público toohello pontos de extremidade, a menos que outros mecanismos estão em vigor (por exemplo, Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="70c7d-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="70c7d-236">Altere toofalse essas configurações no recurso de saudação tooturn do arquivo de configuração de serviço Olá:</span><span class="sxs-lookup"><span data-stu-id="70c7d-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="70c7d-237">Em seguida, copie Olá mesma impressão digital que Olá SSL de certificado na configuração da saudação da autoridade de certificação do certificado:</span><span class="sxs-lookup"><span data-stu-id="70c7d-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="70c7d-238">Criar uma Autoridade de certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="70c7d-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="70c7d-239">Execute Olá seguindo as etapas toocreate tooact um certificado autoassinado como uma autoridade de certificação:</span><span class="sxs-lookup"><span data-stu-id="70c7d-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="70c7d-240">toocustomize-lo</span><span class="sxs-lookup"><span data-stu-id="70c7d-240">toocustomize it</span></span>

* <span data-ttu-id="70c7d-241">-e com a data de expiração da certificação de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="70c7d-242">Localizar a chave pública da autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="70c7d-242">Find CA public key</span></span>
<span data-ttu-id="70c7d-243">Todos os certificados de cliente devem ter sido emitidos por uma autoridade de certificação confiável pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="70c7d-244">Localize toohello chave pública Olá autoridade de certificação que emitiu os certificados de cliente de saudação que serão toobe usado para autenticação no tooupload ordem-toohello serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="70c7d-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="70c7d-245">Se o arquivo hello com a chave pública Olá não estiver disponível, você deve exportá-lo saudação do repositório de certificados:</span><span class="sxs-lookup"><span data-stu-id="70c7d-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="70c7d-246">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-246">Find certificate</span></span>
  * <span data-ttu-id="70c7d-247">Olá de procurar por um certificado de cliente emitido pela mesma autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="70c7d-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="70c7d-248">Clique duas vezes no certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="70c7d-249">Selecione a guia de caminho de certificação de saudação na caixa de diálogo de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="70c7d-250">Clique duas vezes em entrada de autoridade de certificação Olá no caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="70c7d-251">Fazer anotações de propriedades do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="70c7d-252">Olá fechar **certificado** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70c7d-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="70c7d-253">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-253">Find certificate</span></span>
  * <span data-ttu-id="70c7d-254">Pesquisar Olá observada acima da autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="70c7d-255">Clique em Ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="70c7d-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="70c7d-256">Exportar o certificado em um .CER com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="70c7d-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="70c7d-257">**Não, não exportar chave privada Olá**</span><span class="sxs-lookup"><span data-stu-id="70c7d-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="70c7d-258">Inclua todos os certificados no caminho de certificação hello, se possível.</span><span class="sxs-lookup"><span data-stu-id="70c7d-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="70c7d-259">Exportar todas as propriedades estendidas.</span><span class="sxs-lookup"><span data-stu-id="70c7d-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="70c7d-260">Carregar o serviço de toocloud de certificado de autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="70c7d-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="70c7d-261">Carregue o certificado com hello existente ou gerado. Arquivo CER com a chave pública de saudação da autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="70c7d-262">Atualizar o Certificado de Autoridade de Certificação no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="70c7d-263">Atualize o valor de impressão digital de saudação do hello após a configuração no arquivo de configuração de serviço Olá com a impressão digital de Olá Olá certificado carregado toohello do serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="70c7d-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="70c7d-264">Atualizar o valor Olá Olá após a configuração com hello mesmo impressão digital:</span><span class="sxs-lookup"><span data-stu-id="70c7d-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="70c7d-265">Emitir certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-265">Issue client certificates</span></span>
<span data-ttu-id="70c7d-266">Cada serviço de saudação individuais tooaccess autorizados deve ter um certificado de cliente emitido para his/hers exclusivo a usar e deve escolher que HIS/hers possui senha forte tooprotect sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="70c7d-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="70c7d-267">Olá, as etapas a seguir deve ser executado no hello mesma máquina onde Olá autoassinado certificado de autoridade de certificação foi gerada e armazenada:</span><span class="sxs-lookup"><span data-stu-id="70c7d-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="70c7d-268">Personalizando:</span><span class="sxs-lookup"><span data-stu-id="70c7d-268">Customizing:</span></span>

* <span data-ttu-id="70c7d-269">-n com uma ID de cliente toohello que será autenticado com o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="70c7d-270">-e com data de validade do certificado Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="70c7d-271">MyID.pvk e MyID.cer com nomes de arquivo exclusivo para o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="70c7d-272">Esse comando solicitará um toobe senha criada e usada uma vez.</span><span class="sxs-lookup"><span data-stu-id="70c7d-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="70c7d-273">Use uma senha forte.</span><span class="sxs-lookup"><span data-stu-id="70c7d-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="70c7d-274">Criar arquivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="70c7d-275">Para cada certificado de cliente gerado, execute:</span><span class="sxs-lookup"><span data-stu-id="70c7d-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="70c7d-276">Personalizando:</span><span class="sxs-lookup"><span data-stu-id="70c7d-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="70c7d-277">Digite a senha e, em seguida, exporte o certificado com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="70c7d-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="70c7d-278">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-278">Yes, export hello private key</span></span>
* <span data-ttu-id="70c7d-279">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="70c7d-279">Export all extended properties</span></span>
* <span data-ttu-id="70c7d-280">Olá toowhom individuais que esse certificado está sendo emitido deve escolher uma senha de exportação Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="70c7d-281">Importar o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-281">Import client certificate</span></span>
<span data-ttu-id="70c7d-282">Cada pessoa para quem um certificado de cliente tiver sido emitido deve importar o par de chaves Olá máquinas hello, ele usará toocommunicate com o serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="70c7d-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="70c7d-283">Clique duas vezes em hello. Arquivo PFX no Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="70c7d-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="70c7d-284">Importar o certificado para Olá pessoal armazenar pelo menos essa opção:</span><span class="sxs-lookup"><span data-stu-id="70c7d-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="70c7d-285">Incluir todas as propriedades estendidas marcadas</span><span class="sxs-lookup"><span data-stu-id="70c7d-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="70c7d-286">Copie as impressões digitais de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="70c7d-287">Cada pessoa para quem um certificado de cliente tiver sido emitido deve seguir estas etapas na ordem tooobtain Olá impressão digital his/hers certificado que será adicionado toohello arquivo de configuração de serviço:</span><span class="sxs-lookup"><span data-stu-id="70c7d-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="70c7d-288">Executar certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="70c7d-288">Run certmgr.exe</span></span>
* <span data-ttu-id="70c7d-289">Selecione a guia pessoal Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-289">Select hello Personal tab</span></span>
* <span data-ttu-id="70c7d-290">Clique duas vezes no certificado do cliente Olá toobe usado para autenticação</span><span class="sxs-lookup"><span data-stu-id="70c7d-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="70c7d-291">Olá certificado caixa de diálogo que é aberta, selecione a guia de detalhes de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="70c7d-292">Certifique-se de que mostrar está exibindo todos</span><span class="sxs-lookup"><span data-stu-id="70c7d-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="70c7d-293">Campo de saudação selecione denominado impressão digital na lista de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="70c7d-294">Copiar valor Olá da impressão digital de saudação do * * excluir os caracteres Unicode não visíveis na frente do primeiro dígito de hello * * excluir todos os espaços</span><span class="sxs-lookup"><span data-stu-id="70c7d-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="70c7d-295">Configurar clientes de permitido no arquivo de configuração de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="70c7d-296">Atualize o valor de saudação do hello configuração no arquivo de configuração de serviço Olá com uma lista separada por vírgulas de impressões digitais de Olá Olá certificados de cliente permitidos acesso toohello serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="70c7d-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="70c7d-297">Configurar a verificação de revogação de certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="70c7d-298">não verifica a configuração padrão de saudação com hello autoridade de certificação para o status de revogação de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="70c7d-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="70c7d-299">tooturn em Olá verifica se Olá autoridade de certificação que emitiu os certificados de cliente Olá dá suporte a essas verificações, altere Olá após a configuração com um dos valores hello definidos no hello enumeração X509RevocationMode:</span><span class="sxs-lookup"><span data-stu-id="70c7d-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="70c7d-300">Criar arquivo PFX para certificados de criptografia autoassinados</span><span class="sxs-lookup"><span data-stu-id="70c7d-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="70c7d-301">Para um certificado de criptografia, execute:</span><span class="sxs-lookup"><span data-stu-id="70c7d-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="70c7d-302">Personalizando:</span><span class="sxs-lookup"><span data-stu-id="70c7d-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="70c7d-303">Digite a senha e, em seguida, exporte o certificado com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="70c7d-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="70c7d-304">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-304">Yes, export hello private key</span></span>
* <span data-ttu-id="70c7d-305">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="70c7d-305">Export all extended properties</span></span>
* <span data-ttu-id="70c7d-306">Você precisará senha Olá ao carregar o serviço de nuvem Olá certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="70c7d-307">Exportar o certificado de criptografia do repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="70c7d-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="70c7d-308">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-308">Find certificate</span></span>
* <span data-ttu-id="70c7d-309">Clique em Ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="70c7d-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="70c7d-310">Exportar o certificado em um arquivo .PFX com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="70c7d-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="70c7d-311">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="70c7d-312">Incluir todos os certificados no caminho de certificação hello, se possível</span><span class="sxs-lookup"><span data-stu-id="70c7d-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="70c7d-313">Exportar todas as propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="70c7d-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="70c7d-314">Carregar o serviço de toocloud de certificado de criptografia</span><span class="sxs-lookup"><span data-stu-id="70c7d-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="70c7d-315">Carregue o certificado com hello existente ou gerado. Arquivo PFX com o par de chaves de criptografia de saudação:</span><span class="sxs-lookup"><span data-stu-id="70c7d-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="70c7d-316">Digite a senha de saudação protegendo informações de chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="70c7d-317">Atualizar o certificado de criptografia no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="70c7d-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="70c7d-318">Atualize o valor de impressão digital de saudação do hello configurações no arquivo de configuração de serviço Olá com a impressão digital de Olá Olá certificado carregado toohello do serviço de nuvem a seguir:</span><span class="sxs-lookup"><span data-stu-id="70c7d-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="70c7d-319">Operações comuns de certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-319">Common certificate operations</span></span>
* <span data-ttu-id="70c7d-320">Configurar o certificado SSL Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="70c7d-321">Configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="70c7d-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="70c7d-322">Localize o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-322">Find certificate</span></span>
<span data-ttu-id="70c7d-323">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="70c7d-323">Follow these steps:</span></span>

1. <span data-ttu-id="70c7d-324">Execute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="70c7d-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="70c7d-325">Arquivo -> Adicionar/Remover Snap-in...</span><span class="sxs-lookup"><span data-stu-id="70c7d-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="70c7d-326">Selecione **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="70c7d-327">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-327">Click **Add**.</span></span>
5. <span data-ttu-id="70c7d-328">Escolha o local de repositório de certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="70c7d-329">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-329">Click **Finish**.</span></span>
7. <span data-ttu-id="70c7d-330">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-330">Click **OK**.</span></span>
8. <span data-ttu-id="70c7d-331">Expanda **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="70c7d-332">Expanda o nó de armazenamento de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="70c7d-333">Expanda Olá certificado filho.</span><span class="sxs-lookup"><span data-stu-id="70c7d-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="70c7d-334">Selecione um certificado na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="70c7d-335">Exportar o certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-335">Export certificate</span></span>
<span data-ttu-id="70c7d-336">Em Olá **Assistente para exportação de certificados**:</span><span class="sxs-lookup"><span data-stu-id="70c7d-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="70c7d-337">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-337">Click **Next**.</span></span>
2. <span data-ttu-id="70c7d-338">Selecione **Sim**, em seguida, **chave privada de saudação de exportação**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="70c7d-339">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-339">Click **Next**.</span></span>
4. <span data-ttu-id="70c7d-340">Selecione o formato de arquivo de saída desejada hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="70c7d-341">Verifique as opções de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="70c7d-341">Check hello desired options.</span></span>
6. <span data-ttu-id="70c7d-342">Marque a **Senha**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-342">Check **Password**.</span></span>
7. <span data-ttu-id="70c7d-343">Digite uma senha forte e confirme-a.</span><span class="sxs-lookup"><span data-stu-id="70c7d-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="70c7d-344">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-344">Click **Next**.</span></span>
9. <span data-ttu-id="70c7d-345">Digite ou procure um nome de arquivo onde toostore Olá certificado (use um. Extensão PFX).</span><span class="sxs-lookup"><span data-stu-id="70c7d-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="70c7d-346">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-346">Click **Next**.</span></span>
11. <span data-ttu-id="70c7d-347">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-347">Click **Finish**.</span></span>
12. <span data-ttu-id="70c7d-348">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="70c7d-349">Importar certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-349">Import certificate</span></span>
<span data-ttu-id="70c7d-350">Em Olá Assistente de importação de certificado:</span><span class="sxs-lookup"><span data-stu-id="70c7d-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="70c7d-351">Selecione o local do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="70c7d-352">Selecione **usuário atual** se apenas os processos em execução em usuário atual serão acessar o serviço de saudação</span><span class="sxs-lookup"><span data-stu-id="70c7d-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="70c7d-353">Selecione **Máquina Local** se outros processos no computador acessará o serviço Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="70c7d-354">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-354">Click **Next**.</span></span>
3. <span data-ttu-id="70c7d-355">Se estiver importando de um arquivo, confirme o caminho do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="70c7d-356">Se estiver importando um arquivo .PFX:</span><span class="sxs-lookup"><span data-stu-id="70c7d-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="70c7d-357">Digite a senha de saudação proteger a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="70c7d-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="70c7d-358">Selecione as opções de importação</span><span class="sxs-lookup"><span data-stu-id="70c7d-358">Select import options</span></span>
5. <span data-ttu-id="70c7d-359">Selecionar certificados de "Local" em Olá repositório a seguir</span><span class="sxs-lookup"><span data-stu-id="70c7d-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="70c7d-360">Clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-360">Click **Browse**.</span></span>
7. <span data-ttu-id="70c7d-361">Selecione repositório de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="70c7d-361">Select hello desired store.</span></span>
8. <span data-ttu-id="70c7d-362">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="70c7d-363">Se o repositório de autoridade de certificação raiz confiável Olá foi escolhido, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="70c7d-364">Clique em **OK** em todas as janelas de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70c7d-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="70c7d-365">Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="70c7d-365">Upload certificate</span></span>
<span data-ttu-id="70c7d-366">Em Olá [Portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="70c7d-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="70c7d-367">Selecione os **Serviços de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="70c7d-368">Selecione o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="70c7d-369">Clique no menu superior Olá **certificados**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="70c7d-370">Na barra inferior de saudação, clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="70c7d-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="70c7d-371">Selecione o arquivo de certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c7d-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="70c7d-372">Se é um. PFX do arquivo, digite a senha de saudação para a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="70c7d-373">Depois de concluído, copie impressão digital do certificado Olá da nova entrada na lista de saudação de hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="70c7d-374">Outras considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="70c7d-374">Other security considerations</span></span>
<span data-ttu-id="70c7d-375">configurações de SSL Olá descritas neste documento criptografar a comunicação entre Olá serviço e seus clientes quando o ponto de extremidade HTTPS Olá é usado.</span><span class="sxs-lookup"><span data-stu-id="70c7d-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="70c7d-376">Isso é importante, pois as credenciais para acesso de banco de dados e possivelmente, outras informações confidenciais estão contidos na comunicação hello.</span><span class="sxs-lookup"><span data-stu-id="70c7d-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="70c7d-377">No entanto, observe que o serviço Olá persista status interno, incluindo credenciais, em suas tabelas internas no banco de dados de SQL do Microsoft Azure de saudação que você forneceu para o armazenamento de metadados na sua assinatura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="70c7d-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="70c7d-378">Esse banco de dados foi definido como parte da saudação após a configuração no arquivo de configuração do serviço (. Arquivo CSCFG):</span><span class="sxs-lookup"><span data-stu-id="70c7d-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="70c7d-379">As credenciais armazenadas neste banco de dados são criptografadas.</span><span class="sxs-lookup"><span data-stu-id="70c7d-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="70c7d-380">No entanto, como uma prática recomendada, verifique se as funções web e de trabalho de suas implantações de serviço são atualizadas toodate e seguro como eles têm acesso toohello metadados hello e banco de dados do certificado usado para criptografia e descriptografia de credenciais armazenadas.</span><span class="sxs-lookup"><span data-stu-id="70c7d-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

