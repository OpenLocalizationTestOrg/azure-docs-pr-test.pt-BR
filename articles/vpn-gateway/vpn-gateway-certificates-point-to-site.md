---
title: 'Gerar e exportar certificados para o Ponto a Site: PowerShell: Azure | Microsoft Docs'
description: "Este artigo contém etapas toocreate um certificado auto-assinado, exportar a chave pública hello e gerar os certificados de cliente usando o PowerShell no Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="6018e-103">Gerar e exportar certificados para conexões Ponto a Site utilizando o PowerShell no Windows 10</span><span class="sxs-lookup"><span data-stu-id="6018e-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="6018e-104">Conexões ponto a Site usam certificados tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="6018e-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="6018e-105">Este artigo mostra como o certificado de raiz toocreate um autoassinado e gerar os certificados de cliente usando o PowerShell no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6018e-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="6018e-106">Se você estiver procurando para etapas de configuração de ponto a Site, como como listam certificados de raiz tooupload, selecione um dos artigos de saudação ' Configure ponto a Site' de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6018e-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6018e-107">Criar certificados autoassinados – PowerShell</span><span class="sxs-lookup"><span data-stu-id="6018e-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="6018e-108">Criar certificados autoassinados - MakeCert</span><span class="sxs-lookup"><span data-stu-id="6018e-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="6018e-109">Configurar Ponto a Site – Resource Manager – portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6018e-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="6018e-110">Configurar o Point-to-Site - Gerenciador de recursos - Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6018e-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="6018e-111">Configurar Ponto a Site – Clássico – portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6018e-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="6018e-112">Você deve executar etapas de saudação neste artigo em um computador executando o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6018e-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="6018e-113">Olá cmdlets do PowerShell que você use certificados toogenerate fazem parte do sistema operacional de saudação Windows 10 e não funcionam em outras versões do Windows.</span><span class="sxs-lookup"><span data-stu-id="6018e-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="6018e-114">computador Olá Windows 10 é apenas os certificados necessários toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="6018e-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="6018e-115">Depois que os certificados de saudação são gerados, você pode carregá-los ou instalá-los em qualquer sistema operacional de cliente com suporte.</span><span class="sxs-lookup"><span data-stu-id="6018e-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="6018e-116">Se você não tiver acesso tooa Windows 10 computador, você pode usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificados.</span><span class="sxs-lookup"><span data-stu-id="6018e-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="6018e-117">Olá certificados que você gerar usando qualquer método podem ser instalados em qualquer [suporte](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operacional do cliente.</span><span class="sxs-lookup"><span data-stu-id="6018e-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="6018e-118"><a name="rootcert"></a>Criar um certificado raiz autoassinado</span><span class="sxs-lookup"><span data-stu-id="6018e-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="6018e-119">Use Olá New-SelfSignedCertificate cmdlet toocreate um certificado raiz autoassinado.</span><span class="sxs-lookup"><span data-stu-id="6018e-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="6018e-120">Para obter informações adicionais sobre os parâmetros, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="6018e-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="6018e-121">Em um computador com Windows 10, abra um console do Windows PowerShell com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="6018e-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="6018e-122">Use Olá certificado auto-assinado do exemplo toocreate Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="6018e-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="6018e-123">Olá, exemplo a seguir cria um certificado raiz autoassinado chamado 'P2SRootCert' que é instalado automaticamente em 'Certificados de certificados atual'.</span><span class="sxs-lookup"><span data-stu-id="6018e-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="6018e-124">Você pode exibir certificado Olá abrindo *certmgr.msc*, ou *gerenciar certificados de usuário*.</span><span class="sxs-lookup"><span data-stu-id="6018e-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="6018e-125"><a name="cer"></a>Exportar a chave pública da saudação (. cer)</span><span class="sxs-lookup"><span data-stu-id="6018e-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="6018e-126">arquivo de exported.cer Olá deve ser carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6018e-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="6018e-127">Para obter instruções, consulte [Configurar uma conexão ponto a site](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="6018e-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="6018e-128">tooadd um certificado de raiz confiável, [nesta seção](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) artigo hello.</span><span class="sxs-lookup"><span data-stu-id="6018e-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="6018e-129">Exportar o certificado raiz autoassinado de saudação e toostore de chave pública (opcional)</span><span class="sxs-lookup"><span data-stu-id="6018e-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="6018e-130">Talvez você queira tooexport Olá certificado raiz autoassinado e armazená-la com segurança.</span><span class="sxs-lookup"><span data-stu-id="6018e-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="6018e-131">Se precisar, você pode instalá-lo depois em outro computador e gerar mais certificados de cliente, ou exportar outro arquivo .cer.</span><span class="sxs-lookup"><span data-stu-id="6018e-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="6018e-132">Olá tooexport raiz certificado autoassinado como um. pfx, certificado de raiz Olá selecione e use Olá mesmas etapas conforme descrito em [exportar um certificado de cliente](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="6018e-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="6018e-133"><a name="clientcert"></a>Gerar um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="6018e-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="6018e-134">Cada computador cliente que se conecta tooa VNet usando ponto a Site deve ter um certificado de cliente instalado.</span><span class="sxs-lookup"><span data-stu-id="6018e-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="6018e-135">Gere um certificado de cliente de certificado raiz autoassinado de Olá e, em seguida, exportar e instalar o certificado de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="6018e-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="6018e-136">Se o certificado de cliente Olá não estiver instalado, a autenticação falhará.</span><span class="sxs-lookup"><span data-stu-id="6018e-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="6018e-137">Olá etapas a seguir orientam você durante a geração de um certificado de cliente de um certificado raiz autoassinado.</span><span class="sxs-lookup"><span data-stu-id="6018e-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="6018e-138">Você pode gerar vários certificados de cliente de saudação mesmo certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="6018e-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="6018e-139">Quando você gerar os certificados de cliente usando Olá etapas abaixo, o certificado de cliente Olá é instalado automaticamente no computador de saudação que você usou o certificado de saudação toogenerate.</span><span class="sxs-lookup"><span data-stu-id="6018e-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="6018e-140">Se você quiser tooinstall um certificado de cliente em outro computador cliente, você pode exportar o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="6018e-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="6018e-141">exemplos de saudação usam Olá New-SelfSignedCertificate cmdlet toogenerate um certificado de cliente que expira dentro de um ano.</span><span class="sxs-lookup"><span data-stu-id="6018e-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="6018e-142">Para obter informações de parâmetros adicionais, como definir um valor diferente de expiração Olá certificado de cliente, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="6018e-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="6018e-143">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="6018e-143">Example 1</span></span>

<span data-ttu-id="6018e-144">Este exemplo usa Olá declarado '$cert' variável da seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6018e-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="6018e-145">Se você fechar o console do PowerShell Olá depois criando Olá certificado raiz autoassinado, ou são adicional de cliente certificados em uma nova sessão de console do PowerShell, use as etapas de saudação em [exemplo 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="6018e-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="6018e-146">Modifique e execute toogenerate de exemplo hello um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="6018e-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="6018e-147">Se você executar Olá exemplo a seguir sem modificá-lo, o resultado de saudação é um certificado de cliente chamado 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="6018e-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="6018e-148">Se desejar que o certificado do filho Olá tooname algo mais, modifique o valor CN de saudação.</span><span class="sxs-lookup"><span data-stu-id="6018e-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="6018e-149">Não altere Olá TextExtension ao executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="6018e-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="6018e-150">certificado de cliente Olá gerado é instalado automaticamente em 'Certificados - certificados atual' em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6018e-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="6018e-151"><a name="ex2"></a>Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="6018e-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="6018e-152">Se você está criando certificados de cliente adicional ou está usando não Olá mesma sessão do PowerShell que você usou toocreate seu certificado raiz autoassinado, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6018e-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="6018e-153">Identifica o certificado raiz autoassinado Olá que está instalado no computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="6018e-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="6018e-154">Esse cmdlet retorna uma lista de certificados instalados no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6018e-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="6018e-155">Localize o nome do assunto de saudação de saudação retornados da lista, em seguida, impressão digital de saudação de cópia que está localizado próximo texto de tooa tooit arquivo.</span><span class="sxs-lookup"><span data-stu-id="6018e-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="6018e-156">Saudação de exemplo a seguir, há dois certificados.</span><span class="sxs-lookup"><span data-stu-id="6018e-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="6018e-157">nome CN de saudação é o nome de saudação do certificado raiz autoassinado de saudação do qual você deseja toogenerate um certificado filho.</span><span class="sxs-lookup"><span data-stu-id="6018e-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="6018e-158">Nesse caso, 'P2SRootCert'.</span><span class="sxs-lookup"><span data-stu-id="6018e-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="6018e-159">Declare uma variável para o certificado de raiz hello usando a impressão digital de saudação da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6018e-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="6018e-160">Substitua a impressão digital pela Olá Olá do certificado de raiz do qual você deseja toogenerate um certificado filho.</span><span class="sxs-lookup"><span data-stu-id="6018e-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="6018e-161">Por exemplo, usando a impressão digital de saudação para P2SRootCert na etapa anterior Olá, variável Olá tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="6018e-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="6018e-162">Modifique e execute toogenerate de exemplo hello um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="6018e-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="6018e-163">Se você executar Olá exemplo a seguir sem modificá-lo, o resultado de saudação é um certificado de cliente chamado 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="6018e-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="6018e-164">Se desejar que o certificado do filho Olá tooname algo mais, modifique o valor CN de saudação.</span><span class="sxs-lookup"><span data-stu-id="6018e-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="6018e-165">Não altere Olá TextExtension ao executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="6018e-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="6018e-166">certificado de cliente Olá gerado é instalado automaticamente em 'Certificados - certificados atual' em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6018e-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="6018e-167"><a name="clientexport"></a>Exportar um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="6018e-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="6018e-168"><a name="install"></a>Instalar um certificado do cliente exportado</span><span class="sxs-lookup"><span data-stu-id="6018e-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6018e-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6018e-169">Next steps</span></span>

<span data-ttu-id="6018e-170">Continue com a configuração de Ponto a Site.</span><span class="sxs-lookup"><span data-stu-id="6018e-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="6018e-171">Para **Gerenciador de recursos de** etapas do modelo de implantação, consulte [configurar uma conexão de ponto para Site tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6018e-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="6018e-172">Para **clássico** etapas do modelo de implantação, consulte [configurar uma conexão de VPN ponto a Site tooa VNet (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6018e-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
