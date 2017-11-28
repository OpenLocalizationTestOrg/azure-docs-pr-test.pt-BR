---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
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
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="0b2cb-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0b2cb-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="0b2cb-104">Este artigo mostra como você pode habilitar o protocolo LDAPS para seu domínio gerenciado dos Serviços de Domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="0b2cb-105">O LDAP Seguro também é conhecido como “LDAP sobre protocolo SSL/TLS”.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0b2cb-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0b2cb-106">Before you begin</span></span>
<span data-ttu-id="0b2cb-107">tarefas de saudação tooperform listadas neste artigo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="0b2cb-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="0b2cb-108">Uma **assinatura do Azure**válida.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="0b2cb-109">Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="0b2cb-110">**Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="0b2cb-111">Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0b2cb-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="0b2cb-112">Um **LDAP seguro de certificados toobe usado tooenable**.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="0b2cb-113">**Recomendado** - Obtenha um certificado da uma autoridade de certificação pública confiável.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="0b2cb-114">Essa opção de configuração é a mais segura.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="0b2cb-115">Como alternativa, você também pode escolher muito[criar um certificado autoassinado](#task-1---obtain-a-certificate-for-secure-ldap) conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="0b2cb-116">Requisitos de certificado LDAP seguro Olá</span><span class="sxs-lookup"><span data-stu-id="0b2cb-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="0b2cb-117">Adquira um certificado válido por Olá seguindo as diretrizes, antes de ativar o LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="0b2cb-118">Você encontrar falhas, se você tentar tooenable LDAP seguro para seu domínio gerenciado com um certificado inválido/incorreto.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="0b2cb-119">**Emissor confiável** -Olá certificado deve ser emitido por uma autoridade confiada por computadores que se conectam toohello domínio gerenciado usando o LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="0b2cb-120">Essa autoridade pode ser uma autoridade de certificação pública de confiança nesses computadores.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="0b2cb-121">**Tempo de vida** -certificado Olá deve ser válido para pelo menos Olá próximos 3 a 6 meses.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="0b2cb-122">Seguro LDAP acesso tooyour domínio gerenciado será interrompido quando Olá certificado expira.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="0b2cb-123">**Nome da entidade** -nome de requerente Olá certificado Olá deve ser um caractere curinga para o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="0b2cb-124">Por exemplo, se seu domínio é denominado 'contoso100.com', nome da entidade do certificado Olá deve ser ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="0b2cb-125">Definir Olá DNS (nome alternativo da entidade) toothis curinga nome.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="0b2cb-126">**Uso de chave** - certificado Olá deve ser configurado para Olá a seguir usa - assinaturas digitais e codificação de chave.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="0b2cb-127">**Finalidade do certificado** -certificado Olá deve ser válido para autenticação de servidor SSL.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="0b2cb-128">**Autoridades de Certificação Corporativas:** o Azure AD Domain Services não dá suporte ao uso de certificados LDAP seguros emitidos pela autoridade de certificação corporativa de sua organização.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="0b2cb-129">Essa restrição é porque o serviço de saudação não confia em sua autoridade de certificação como uma autoridade de certificação raiz.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="0b2cb-130">Tarefa 1 – obter um certificado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="0b2cb-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="0b2cb-131">tarefa de primeiro Olá envolve obtendo um certificado usado para proteger LDAP acesso toohello domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="0b2cb-132">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="0b2cb-132">You have two options:</span></span>

* <span data-ttu-id="0b2cb-133">Obtenha um certificado de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="0b2cb-134">autoridade Olá pode ser uma autoridade de certificação pública.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="0b2cb-135">Crie um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="0b2cb-136">Opção A (recomendada) - obter um certificado LDAP seguro de uma autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="0b2cb-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="0b2cb-137">Se sua organização obtém seus certificados de uma autoridade de certificação pública, será necessário tooobtain Olá seguro LDAP de certificados de autoridade de certificação pública.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="0b2cb-138">Ao solicitar um certificado, certifique-se de que você atenda a todos os requisitos de saudação descritos na [requisitos de certificado LDAP seguro Olá](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="0b2cb-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="0b2cb-139">Computadores cliente que precisam tooconnect toohello domínio gerenciado usando o LDAP seguro devem confiar emissor de saudação do certificado LDAP seguro hello.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="0b2cb-140">Opção B - criar um certificado autoassinado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="0b2cb-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="0b2cb-141">Se você não espera toouse um certificado de uma autoridade de certificação pública, você pode escolher toocreate um certificado autoassinado para LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="0b2cb-142">**Criar um certificado autoassinado usando o PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0b2cb-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="0b2cb-143">No seu computador Windows, abra uma nova janela do PowerShell como **administrador** e Olá tipo seguindo comandos, toocreate um novo certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="0b2cb-144">Olá anterior de exemplo, substitua '*. contoso100.com' com o nome de domínio DNS Olá do seu domínio gerenciado. Por exemplo, se você criou um domínio gerenciado chamado 'contoso100.onmicrosoft.com', substitua '*. contoso100.com' em Olá acima script com ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="0b2cb-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="0b2cb-146">certificado autoassinado Olá recém-criado é colocado no repositório de certificados do computador local hello.</span><span class="sxs-lookup"><span data-stu-id="0b2cb-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="0b2cb-147">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="0b2cb-147">Next step</span></span>
[<span data-ttu-id="0b2cb-148">Tarefa 2: exportar Olá seguro LDAP certificado tooa. Arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="0b2cb-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
