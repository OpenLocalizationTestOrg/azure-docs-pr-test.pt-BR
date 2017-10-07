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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Habilitar a sincronização de senha tooAzure serviços de domínio do Active Directory
Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory). Olá próxima tarefa é tooenable sincronização de hashes de credenciais necessárias para tooAzure de autenticação NT LAN Manager (NTLM) e Kerberos dos serviços de domínio do AD. Depois de configurar a sincronização de credenciais, os usuários possam entrar toohello o domínio gerenciado com suas credenciais corporativas.

etapas de Olá envolvidas são diferentes para o usuário somente em nuvem contas vs contas de usuário que são sincronizadas do seu diretório local usando o Azure AD Connect. Se o seu locatário do AD do Azure tem uma combinação de nuvem apenas os usuários e usuários de seu local AD, você precisa tooperform as duas etapas.

<br>

> [!div class="op_single_selector"]
> * **Contas de usuário somente em nuvem**: [sincronizar senhas para contas de usuário somente em nuvem domínio gerenciado tooyour](active-directory-ds-getting-started-password-sync.md)
> * **Contas de usuário local**: [sincronizar senhas para contas de usuário sincronizadas a partir de suas instalações AD tooyour gerenciados domínio](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Tarefa 5: habilitar tooyour de sincronização de senha gerenciado domínio para as contas de usuário sincronizadas ao seu local AD
A sincronização do Azure locatário do AD está definido toosynchronize com o diretório de local da sua organização usando o Azure AD Connect. Por padrão, o Azure AD Connect não sincronizar Kerberos e NTLM tooAzure de hashes de credencial AD. toouse serviços de domínio do AD do Azure, você precisa tooconfigure do Azure AD Connect toosynchronize hashes de credenciais necessárias para a autenticação NTLM e Kerberos. Olá, as etapas a seguir habilitam a sincronização de hashes de credencial Olá necessária do seu locatário de AD do Azure de tooyour de diretório local.

> [!NOTE]
> Se sua organização tiver contas de usuário que são sincronizadas do seu diretório local, você precisa habilitar a sincronização de hash NTLM e Kerberos em ordem toouse Olá gerenciado domínio. Uma conta de usuário sincronizado é uma conta que foi criada em seu diretório local e é sincronizada tooyour locatário de AD do Azure usando o Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Instalar ou atualizar o Azure AD Connect
Instalar Olá recomendado mais recente versão do Azure AD Connect em um domínio ingressados no computador. Se você tiver uma instância existente do programa de instalação do Azure AD Connect, será necessário tooupdate-toouse versão mais recente do hello do Azure AD Connect. tooavoid conhecido problemas/erros que podem já ter sido corrigidos, verifique se você usar sempre a versão mais recente de saudação do Azure AD Connect.

**[Baixar o Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Versão recomendada: **1.1.553.0** - publicada em 27 de junho de 2017.

> [!WARNING]
> Você deve instalar hello mais recente versão do Azure AD Connect tooenable Olá senha herdados credenciais (necessárias para a autenticação NTLM e Kerberos) toosynchronize tooyour AD do Azure locatário de recomendado. Essa funcionalidade não está disponível em versões anteriores do Azure AD Connect ou com a ferramenta DirSync herdada de saudação.
>
>

Instruções de instalação para o Azure AD Connect estão disponíveis no seguinte Olá artigo - [guia de Introdução ao Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Habilitar a sincronização de Kerberos e NTLM tooAzure de hashes de credencial AD
Execute Olá script do PowerShell a seguir em cada floresta do AD, a sincronização de senha completo tooforce e habilitar o locatário do todos os usuários locais credencial hashes toosync tooyour AD do Azure. Esse script permite que os hashes de credenciais de saudação necessárias para o locatário do Kerberos/NTLM autenticação toobe tooyour sincronizado do AD do Azure.

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

Dependendo do tamanho de saudação do seu diretório (número de usuários, grupos etc.), a sincronização de credencial hashes tooAzure AD leva tempo. senhas de saudação poderá ser usadas no domínio gerenciado por serviços de domínio do AD do Azure Olá logo após os hashes de credencial Olá sincronizaram tooAzure AD.

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Habilitar a sincronização de senha tooAAD serviços de domínio para um Azure somente em nuvem diretório do AD](active-directory-ds-getting-started-password-sync.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Ingressar em um domínio gerenciado do Windows máquina virtual tooan serviços de domínio do AD do Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Ingressar em um domínio gerenciado do Red Hat Enterprise Linux máquina virtual tooan serviços de domínio do AD do Azure](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
