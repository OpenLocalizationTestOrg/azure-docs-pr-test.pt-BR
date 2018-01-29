---
title: "Serviços de Domínio do Azure AD: habilitar a sincronização de senha | Microsoft Docs"
description: "Introdução aos Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/15/2017
ms.author: maheshu
ms.openlocfilehash: 0f6204e8f0f779809cd9c657acbcbcf39d57d481
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a>Habilitar a sincronização de senhas para o Azure Active Directory Domain Services
Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory). A próxima tarefa é habilitar a sincronização de hashes de credencial necessários para a autenticação Kerberos e NTLM para o Azure AD Domain Services. Depois que a sincronização de credenciais é configurada, os usuários podem entrar no domínio gerenciado com suas credenciais corporativas.

As etapas envolvidas são diferentes para as contas de usuário somente em nuvem versus contas de usuário sincronizadas do seu diretório local usando o Azure AD Connect.

<br>
| **Tipo de conta de usuário** | **Etapas a serem executadas** |
| --- | --- |
| **Contas de usuário sincronizadas de um diretório local** |**&#x2713;** [Siga as instruções deste artigo](active-directory-ds-getting-started-password-sync-synced-tenant.md#task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad) | 
| **Contas de usuário de nuvem criadas no Azure AD** |**&#x2713;** [Sincronizar senhas para contas de usuário somente em nuvem para seu domínio gerenciado](active-directory-ds-getting-started-password-sync.md) |
<br>

> [!TIP]
> **Talvez seja necessário concluir os dois conjuntos de etapas.**
> Se o seu locatário do AD do Azure tiver uma combinação de usuários somente em nuvem e os usuários do seu AD local, será necessário concluir ambos os conjuntos de etapas.
>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Tarefa 5: habilitar a sincronização de senha para seu domínio gerenciado para contas de usuário sincronizadas ao seu AD local
Um locatário do Azure AD sincronizado é configurado para ser sincronizado com o diretório do local de sua organização usando o Azure AD Connect. Por padrão, o Azure AD Connect não sincroniza hashes de credenciais NTLM e Kerberos com o Azure AD. Para usar os serviços de domínio do Azure AD, você precisa configurar o Azure AD Connect para sincronizar os hashes de credenciais necessários para a autenticação NTLM e Kerberos. As etapas a seguir habilitam a sincronização dos hashes de credenciais necessários do seu diretório local para seu locatário do Azure AD.

> [!NOTE]
> **Se sua organização tiver contas de usuário sincronizadas do seu diretório local, você deverá habilitar a sincronização de hashes Kerberos e NTLM para usar o domínio gerenciado.** Uma conta de usuário sincronizado é uma conta que foi criada em seu diretório local e será sincronizada com seu locatário do Azure AD usando o Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Instalar ou atualizar o Azure AD Connect
Você precisa instalar a versão mais recente do Azure AD Connect recomendada em um computador ingressado no domínio associado. Se tiver uma instância existente do programa de instalação do Azure AD Connect, você precisará atualizá-lo para usar a última versão do Azure AD Connect. Para evitar problemas/erros conhecidos que talvez já tenham sido corrigidos, use sempre a versão mais recente do Azure AD Connect.

**[Baixar o Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Versão recomendada: **1.1.614.0** - publicada em 5 de setembro de 2017.

> [!WARNING]
> Você DEVE instalar a versão GA do Azure AD Connect para habilitar as credenciais de senha herdadas (necessárias para a autenticação NTLM e Kerberos) para sincronizar seu locatário do Azure AD. Essa funcionalidade não está disponível em versões anteriores do Azure Connect AD ou com a ferramenta DirSync herdada.
>
>

Instruções de instalação para o AD do Azure Connect estão disponíveis no seguinte artigo - [Introdução ao AD do Azure Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a>Habilitar a sincronização dos hashes das credenciais NTLM e do Kerberos para o Azure AD
Execute o seguinte script do PowerShell em cada floresta do AD. O script permite que os hashes de senha NTLM e Kerberos de todos os usuários locais sejam sincronizados com seu locatário do Azure AD. O script também inicia uma sincronização completa no Azure AD Connect.

```powershell
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

Dependendo do tamanho do diretório (número de usuários, grupos etc.), a sincronização de credenciais com o Azure AD pode ser demorada. As senhas poderão ser usadas no domínio dos serviços de domínio do AD do Azure gerenciado logo após os hashes de credencial ter sincronizado ao AD do Azure.

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Habilitar a sincronização de senhas nos Serviços de Domínio do AAD para um diretório do AD do Azure somente na nuvem](active-directory-ds-getting-started-password-sync.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Ingressar em uma máquina virtual do Windows para um domínio gerenciado dos Serviços de Domínio do AD do Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Ingressar em uma máquina virtual do Red Hat Enterprise Linux para um domínio gerenciado dos Serviços de Domínio do AD do Azure](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
