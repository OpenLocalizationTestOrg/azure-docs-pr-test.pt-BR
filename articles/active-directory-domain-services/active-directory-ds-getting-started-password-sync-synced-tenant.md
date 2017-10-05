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
ms.openlocfilehash: 947ea3c9d789ecf5a754001aafcda6f8bcd41047
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="d893a-103">Habilitar a sincronização de senhas para o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d893a-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="d893a-104">Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d893a-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="d893a-105">A próxima tarefa é habilitar a sincronização de hashes de credencial necessários para a autenticação Kerberos e NTLM para o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d893a-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="d893a-106">Depois que a sincronização de credenciais é configurada, os usuários podem entrar no domínio gerenciado com suas credenciais corporativas.</span><span class="sxs-lookup"><span data-stu-id="d893a-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="d893a-107">As etapas envolvidas são diferentes para as contas de usuário somente em nuvem versus contas de usuário sincronizadas do seu diretório local usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d893a-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="d893a-108">Se o seu locatário do AD do Azure tiver uma combinação de usuários somente em nuvem e os usuários do seu AD local, será necessário executar as duas etapas.</span><span class="sxs-lookup"><span data-stu-id="d893a-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="d893a-109">**Contas de usuário somente em nuvem**: [sincronize senhas para contas de usuário somente em nuvem para seu domínio gerenciado](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="d893a-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="d893a-110">**Contas de usuário local**: [sincronize senhas para as contas de usuário sincronizadas de seu AD local para seu domínio gerenciado](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d893a-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="d893a-111">Tarefa 5: habilitar a sincronização de senha para seu domínio gerenciado para contas de usuário sincronizadas ao seu AD local</span><span class="sxs-lookup"><span data-stu-id="d893a-111">Task 5: enable password synchronization to your managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="d893a-112">Um locatário do Azure AD sincronizado é configurado para ser sincronizado com o diretório do local de sua organização usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d893a-112">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="d893a-113">Por padrão, o Azure AD Connect não sincroniza hashes de credenciais NTLM e Kerberos com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d893a-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD.</span></span> <span data-ttu-id="d893a-114">Para usar os serviços de domínio do Azure AD, você precisa configurar o Azure AD Connect para sincronizar os hashes de credenciais necessários para a autenticação NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d893a-114">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="d893a-115">As etapas a seguir habilitam a sincronização dos hashes de credenciais necessários do seu diretório local para seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d893a-115">The following steps enable synchronization of the required credential hashes from your on-premises directory to your Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="d893a-116">Se sua organização tiver contas de usuário sincronizadas do seu diretório local, você deverá habilitar a sincronização de hashes Kerberos e NTLM para usar o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d893a-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order to use the managed domain.</span></span> <span data-ttu-id="d893a-117">Uma conta de usuário sincronizado é uma conta que foi criada em seu diretório local e será sincronizada com seu locatário do Azure AD usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d893a-117">A synced user account is an account that was created in your on-premises directory and is synchronized to your Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="d893a-118">Instalar ou atualizar o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d893a-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="d893a-119">Você precisa instalar a versão mais recente do Azure AD Connect recomendada em um computador ingressado no domínio associado.</span><span class="sxs-lookup"><span data-stu-id="d893a-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="d893a-120">Se tiver uma instância existente do programa de instalação do Azure AD Connect, você precisará atualizá-lo para usar a última versão do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d893a-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span></span> <span data-ttu-id="d893a-121">Para evitar problemas/erros conhecidos que talvez já tenham sido corrigidos, use sempre a versão mais recente do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d893a-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span></span>

<span data-ttu-id="d893a-122">**[Baixar o Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="d893a-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="d893a-123">Versão recomendada: **1.1.553.0** - publicada em 27 de junho de 2017.</span><span class="sxs-lookup"><span data-stu-id="d893a-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="d893a-124">Você DEVE instalar a versão GA do Azure AD Connect para habilitar as credenciais de senha herdadas (necessárias para a autenticação NTLM e Kerberos) para sincronizar seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d893a-124">You MUST install the latest recommended release of Azure AD Connect to enable the legacy password credentials (required for NTLM and Kerberos authentication) to synchronize to your Azure AD tenant.</span></span> <span data-ttu-id="d893a-125">Essa funcionalidade não está disponível em versões anteriores do Azure Connect AD ou com a ferramenta DirSync herdada.</span><span class="sxs-lookup"><span data-stu-id="d893a-125">This functionality is not available in prior releases of Azure AD Connect or with the legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="d893a-126">Instruções de instalação para o AD do Azure Connect estão disponíveis no seguinte artigo - [Introdução ao AD do Azure Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="d893a-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a><span data-ttu-id="d893a-127">Habilitar a sincronização dos hashes das credenciais NTLM e do Kerberos para o Azure AD</span><span class="sxs-lookup"><span data-stu-id="d893a-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span></span>
<span data-ttu-id="d893a-128">Execute o seguinte script PowerShell em cada floresta do AD, para forçar a sincronização de senhas completa e habilitar os hashes de credenciais de todos os usuários locais para sincronização com seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d893a-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span></span> <span data-ttu-id="d893a-129">Esse script permite que os hashes de credenciais necessários para a autenticação Kerberos/NTLM sejam sincronizados com seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d893a-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span></span>

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

<span data-ttu-id="d893a-130">Dependendo do tamanho do diretório (número de usuários, grupos etc.), a sincronização de credenciais com o Azure AD pode ser demorada.</span><span class="sxs-lookup"><span data-stu-id="d893a-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span></span> <span data-ttu-id="d893a-131">As senhas poderão ser usadas no domínio dos serviços de domínio do AD do Azure gerenciado logo após os hashes de credencial ter sincronizado ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d893a-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="d893a-132">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="d893a-132">Related Content</span></span>
* [<span data-ttu-id="d893a-133">Habilitar a sincronização de senhas nos Serviços de Domínio do AAD para um diretório do AD do Azure somente na nuvem</span><span class="sxs-lookup"><span data-stu-id="d893a-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="d893a-134">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d893a-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="d893a-135">Ingressar em uma máquina virtual do Windows para um domínio gerenciado dos Serviços de Domínio do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d893a-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="d893a-136">Ingressar em uma máquina virtual do Red Hat Enterprise Linux para um domínio gerenciado dos Serviços de Domínio do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d893a-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
