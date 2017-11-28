---
title: "Serviços de Domínio do Azure AD: habilitar a sincronização de senha | Microsoft Docs"
description: "Introdução aos Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="d8940-103">Habilitar a sincronização de senha tooAzure serviços de domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8940-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="d8940-104">Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d8940-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="d8940-105">Olá próxima tarefa é tooenable sincronização de hashes de credenciais necessárias para tooAzure de autenticação NT LAN Manager (NTLM) e Kerberos dos serviços de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="d8940-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="d8940-106">Depois de configurar a sincronização de credenciais, os usuários possam entrar toohello o domínio gerenciado com suas credenciais corporativas.</span><span class="sxs-lookup"><span data-stu-id="d8940-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="d8940-107">etapas de Olá envolvidas são diferentes para o usuário somente em nuvem contas vs contas de usuário que são sincronizadas do seu diretório local usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8940-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="d8940-108">Se o seu locatário do AD do Azure tem uma combinação de nuvem apenas os usuários e usuários de seu local AD, você precisa tooperform as duas etapas.</span><span class="sxs-lookup"><span data-stu-id="d8940-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="d8940-109">**Contas de usuário somente em nuvem**: [sincronizar senhas para contas de usuário somente em nuvem domínio gerenciado tooyour](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="d8940-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="d8940-110">**Contas de usuário local**: [sincronizar senhas para contas de usuário sincronizadas a partir de suas instalações AD tooyour gerenciados domínio](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d8940-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="d8940-111">Tarefa 5: habilitar tooyour de sincronização de senha gerenciado domínio para as contas de usuário sincronizadas ao seu local AD</span><span class="sxs-lookup"><span data-stu-id="d8940-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="d8940-112">A sincronização do Azure locatário do AD está definido toosynchronize com o diretório de local da sua organização usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8940-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="d8940-113">Por padrão, o Azure AD Connect não sincronizar Kerberos e NTLM tooAzure de hashes de credencial AD.</span><span class="sxs-lookup"><span data-stu-id="d8940-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="d8940-114">toouse serviços de domínio do AD do Azure, você precisa tooconfigure do Azure AD Connect toosynchronize hashes de credenciais necessárias para a autenticação NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d8940-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="d8940-115">Olá, as etapas a seguir habilitam a sincronização de hashes de credencial Olá necessária do seu locatário de AD do Azure de tooyour de diretório local.</span><span class="sxs-lookup"><span data-stu-id="d8940-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="d8940-116">Se sua organização tiver contas de usuário que são sincronizadas do seu diretório local, você precisa habilitar a sincronização de hash NTLM e Kerberos em ordem toouse Olá gerenciado domínio.</span><span class="sxs-lookup"><span data-stu-id="d8940-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="d8940-117">Uma conta de usuário sincronizado é uma conta que foi criada em seu diretório local e é sincronizada tooyour locatário de AD do Azure usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8940-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="d8940-118">Instalar ou atualizar o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d8940-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="d8940-119">Instalar Olá recomendado mais recente versão do Azure AD Connect em um domínio ingressados no computador.</span><span class="sxs-lookup"><span data-stu-id="d8940-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="d8940-120">Se você tiver uma instância existente do programa de instalação do Azure AD Connect, será necessário tooupdate-toouse versão mais recente do hello do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8940-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="d8940-121">tooavoid conhecido problemas/erros que podem já ter sido corrigidos, verifique se você usar sempre a versão mais recente de saudação do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8940-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="d8940-122">**[Baixar o Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="d8940-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="d8940-123">Versão recomendada: **1.1.553.0** - publicada em 27 de junho de 2017.</span><span class="sxs-lookup"><span data-stu-id="d8940-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="d8940-124">Você deve instalar hello mais recente versão do Azure AD Connect tooenable Olá senha herdados credenciais (necessárias para a autenticação NTLM e Kerberos) toosynchronize tooyour AD do Azure locatário de recomendado.</span><span class="sxs-lookup"><span data-stu-id="d8940-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="d8940-125">Essa funcionalidade não está disponível em versões anteriores do Azure AD Connect ou com a ferramenta DirSync herdada de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8940-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="d8940-126">Instruções de instalação para o Azure AD Connect estão disponíveis no seguinte Olá artigo - [guia de Introdução ao Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="d8940-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="d8940-127">Habilitar a sincronização de Kerberos e NTLM tooAzure de hashes de credencial AD</span><span class="sxs-lookup"><span data-stu-id="d8940-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="d8940-128">Execute Olá script do PowerShell a seguir em cada floresta do AD, a sincronização de senha completo tooforce e habilitar o locatário do todos os usuários locais credencial hashes toosync tooyour AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8940-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="d8940-129">Esse script permite que os hashes de credenciais de saudação necessárias para o locatário do Kerberos/NTLM autenticação toobe tooyour sincronizado do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8940-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="d8940-130">Dependendo do tamanho de saudação do seu diretório (número de usuários, grupos etc.), a sincronização de credencial hashes tooAzure AD leva tempo.</span><span class="sxs-lookup"><span data-stu-id="d8940-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="d8940-131">senhas de saudação poderá ser usadas no domínio gerenciado por serviços de domínio do AD do Azure Olá logo após os hashes de credencial Olá sincronizaram tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="d8940-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="d8940-132">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="d8940-132">Related Content</span></span>
* [<span data-ttu-id="d8940-133">Habilitar a sincronização de senha tooAAD serviços de domínio para um Azure somente em nuvem diretório do AD</span><span class="sxs-lookup"><span data-stu-id="d8940-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="d8940-134">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8940-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="d8940-135">Ingressar em um domínio gerenciado do Windows máquina virtual tooan serviços de domínio do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d8940-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="d8940-136">Ingressar em um domínio gerenciado do Red Hat Enterprise Linux máquina virtual tooan serviços de domínio do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d8940-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
