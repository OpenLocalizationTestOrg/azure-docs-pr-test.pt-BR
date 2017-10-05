---
title: "Configurar o LDAP Seguro (LDAPS) nos Serviços de Domínio do Azure AD |Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="0c1f8-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0c1f8-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="0c1f8-104">Este artigo mostra como você pode habilitar o protocolo LDAPS para seu domínio gerenciado dos Serviços de Domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="0c1f8-105">O LDAP Seguro também é conhecido como “LDAP sobre protocolo SSL/TLS”.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0c1f8-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0c1f8-106">Before you begin</span></span>
<span data-ttu-id="0c1f8-107">Para executar as tarefas listadas neste artigo, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c1f8-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="0c1f8-108">Uma **assinatura do Azure**válida.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="0c1f8-109">Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="0c1f8-110">**Serviços de Domínio do Azure AD** devem ser habilitados para o diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="0c1f8-111">Se você ainda não tiver feito isso, execute todas as tarefas descritas no [guia de Introdução](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c1f8-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="0c1f8-112">Um **certificado a ser usado para habilitar o LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="0c1f8-113">**Recomendado** - Obtenha um certificado da uma autoridade de certificação pública confiável.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="0c1f8-114">Essa opção de configuração é a mais segura.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="0c1f8-115">Como alternativa, você também pode optar por [criar um certificado autoassinado](#task-1---obtain-a-certificate-for-secure-ldap) como mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="0c1f8-116">Requisitos para o certificado LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="0c1f8-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="0c1f8-117">Obtenha um certificado válido que esteja de acordo com as diretrizes a seguir, antes de habilitar o LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="0c1f8-118">Você encontrará falhas se tentar habilitar o LDAP seguro para seu domínio gerenciado com um certificado inválido/incorreto.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="0c1f8-119">**Emissor confiável** – o certificado deve ser emitido por uma autoridade confiável para os computadores que se conectarem ao domínio gerenciado usando LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="0c1f8-120">Essa autoridade pode ser uma autoridade de certificação pública de confiança nesses computadores.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="0c1f8-121">**Tempo de vida** : o certificado deve ser válido por, pelo menos, os próximos três a seis meses.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="0c1f8-122">O acesso LDAP seguro para seu domínio gerenciado é interrompido quando o certificado expira.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="0c1f8-123">**Nome da entidade** : o nome da entidade do certificado deve ser um caractere curinga para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="0c1f8-124">Por exemplo, se o domínio se chamar “contoso100.com”, o nome da entidade do certificado deverá ser “*.contoso100.com”.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="0c1f8-125">Defina o nome DNS (nome alternativo da entidade) como esse nome curinga.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="0c1f8-126">**Uso de chave** : o certificado deve ser configurado para estas utilizações - assinaturas digitais e codificação de chave.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="0c1f8-127">**Finalidade do certificado** : o certificado deve ser válido para autenticação de servidor SSL.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="0c1f8-128">**Autoridades de Certificação Corporativas:** o Azure AD Domain Services não dá suporte ao uso de certificados LDAP seguros emitidos pela autoridade de certificação corporativa de sua organização.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="0c1f8-129">Essa restrição ocorre porque o serviço não confia em sua autoridade de certificação corporativa como uma autoridade de certificação raiz.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="0c1f8-130">Tarefa 1 – obter um certificado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="0c1f8-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="0c1f8-131">A primeira tarefa envolve a obtenção de um certificado que será usado para acesso LDAP seguro ao domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="0c1f8-132">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="0c1f8-132">You have two options:</span></span>

* <span data-ttu-id="0c1f8-133">Obtenha um certificado de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="0c1f8-134">A autoridade pode ser uma autoridade de certificação pública.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="0c1f8-135">Crie um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="0c1f8-136">Opção A (recomendada) - obter um certificado LDAP seguro de uma autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="0c1f8-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="0c1f8-137">Se sua organização obtiver seus certificados de uma autoridade de certificação pública, será necessário obter o certificado LDAP seguro da autoridade de certificação pública.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="0c1f8-138">Ao solicitar um certificado, verifique se você satisfaz todos os requisitos descritos em [Requisitos para o certificado LDAP seguro](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="0c1f8-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="0c1f8-139">Computadores cliente que precisam se conectar ao domínio gerenciado usando o LDAP seguro devem confiar no emissor do certificado LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="0c1f8-140">Opção B - criar um certificado autoassinado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="0c1f8-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="0c1f8-141">Se você não pretende usar um certificado de uma autoridade de certificação pública, crie um certificado autoassinado para LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="0c1f8-142">**Criar um certificado autoassinado usando o PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0c1f8-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="0c1f8-143">No computador Windows, abra uma nova janela do PowerShell como **Administrador** e digite os comandos a seguir para criar um novo certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="0c1f8-144">No exemplo anterior, substitua "*.contoso100.com" pelo nome do domínio DNS de seu domínio gerenciado. Por exemplo, se você tiver criado um domínio gerenciado chamado “contoso100.onmicrosoft.com”, substitua “*.contoso100.com” no script acima por “*.contoso100.onmicrosoft.com”).</span><span class="sxs-lookup"><span data-stu-id="0c1f8-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selecionar um diretório do Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="0c1f8-146">O certificado autoassinado recém-criado é colocado no repositório de certificados do computador local.</span><span class="sxs-lookup"><span data-stu-id="0c1f8-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="0c1f8-147">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="0c1f8-147">Next step</span></span>
[<span data-ttu-id="0c1f8-148">Tarefa 2 – exportar o certificado LDAP seguro para um arquivo .PFX</span><span class="sxs-lookup"><span data-stu-id="0c1f8-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
