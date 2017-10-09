---
title: "Azure Active Directory Domain Services: guia de solução de problemas | Microsoft Docs"
description: "Guia de solução de problemas para os Serviços de Domínio do AD do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Azure AD Domain Services – Guia de solução de problemas
Este artigo fornece dicas de solução de problemas que você pode encontrar ao configurar ou administrar os Serviços de Domínio do AD (Active Directory do Azure).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Não é possível habilitar o Azure AD Domain Services para seu diretório do Azure AD
Esta seção ajuda você solucionar problemas de erros quando você tentar tooenable serviços de domínio do AD do Azure para seu diretório e ele falha ou obtém alternada too'Disabled back'.

Escolha Olá etapas que correspondem a mensagem de erro toohello que encontrar solução de problemas.

| **Mensagem de erro** | **Resolução** |
| --- |:--- |
| *Olá nome contoso100.com já está em uso na rede. Especifique um nome que não esteja em uso.* |[Conflito de nome de domínio na rede virtual Olá](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Não foi possível habilitar os serviços de domínio neste locatário do AD do Azure. Olá serviço não tem aplicativos de toohello as permissões adequadas chamado 'Sync de serviços de domínio do AD do Azure'. Excluir aplicativo hello chamado 'Sync de serviços de domínio do AD do Azure' e, em seguida, tente tooenable os serviços de domínio para seu locatário do AD do Azure.* |[Serviços de domínio não tem um aplicativo de sincronização de serviços de domínio do AD do Azure toohello as permissões adequadas](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Não foi possível habilitar os serviços de domínio neste locatário do AD do Azure. Olá serviços de domínio do aplicativo no seu locatário do AD do Azure não têm Olá necessárias permissões tooenable dos serviços de domínio. Excluir aplicativo hello com d87dcbc6-a371-462e-88e3-28ad15ec4e64 de identificador de aplicativo hello e, em seguida, tente tooenable serviços de domínio para seu locatário do AD do Azure.* |[Olá aplicativo dos serviços de domínio não está configurado corretamente em seu locatário](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Não foi possível habilitar os serviços de domínio neste locatário do AD do Azure. saudação de aplicativo do AD do Microsoft Azure está desabilitada no seu locatário do AD do Azure. Habilitar o aplicativo hello com hello 00000002-0000-0000-c000-000000000000 de identificador de aplicativo e depois tente tooenable serviços de domínio para seu locatário do AD do Azure.* |[Olá aplicativo Microsoft Graph está desabilitado em seu locatário do AD do Azure](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Conflito de Nome de Domínio
**Mensagem de erro:**

*Olá nome contoso100.com já está em uso na rede. Especifique um nome que não esteja em uso.*

**Correção:**

Certifique-se de que você não tem um domínio existente com hello mesmo nome de domínio disponível nessa rede virtual. Por exemplo, suponha que você tem um domínio denominado "contoso.com" já está disponível na rede virtual selecionada de saudação. Posteriormente, você pode tentar tooenable um domínio gerenciado de serviços de domínio do AD do Azure com hello mesmo nome de domínio (ou seja, ' contoso.com') no qual a rede virtual. Encontrar uma falha durante a tentativa de serviços de domínio tooenable AD do Azure.

Essa falha é devido a conflitos de tooname Olá nome de domínio no qual a rede virtual. Nessa situação, você deve usar tooset um nome diferente, o domínio gerenciado de serviços de domínio do AD do Azure. Como alternativa, você pode desprovisionar domínio existente hello e prossiga em serviços de domínio tooenable AD do Azure.

### <a name="inadequate-permissions"></a>Permissões inadequadas
**Mensagem de erro:**

*Não foi possível habilitar os serviços de domínio neste locatário do AD do Azure. Olá serviço não tem aplicativos de toohello as permissões adequadas chamado 'Sync de serviços de domínio do AD do Azure'. Excluir aplicativo hello chamado 'Sync de serviços de domínio do AD do Azure' e, em seguida, tente tooenable os serviços de domínio para seu locatário do AD do Azure.*

**Correção:**

Verifique toosee se houver um aplicativo com o nome de saudação 'Sync de serviços de domínio do AD do Azure' em seu diretório do AD do Azure. Se esse aplicativo existir, o exclua e habilite novamente os Serviços de Domínio do Azure AD.

Executar Olá seguindo as etapas toocheck presença de saudação do aplicativo hello e toodelete, se o aplicativo hello existe:

1. Navegue toohello **portal clássico do Azure** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Selecione Olá **do Active Directory** nó no painel esquerdo da saudação.
3. Serviços de domínio do AD do Azure locatário Olá selecione AD do Azure (diretório) para o qual você gostaria que tooenable.
4. Navegue toohello **aplicativos** guia.
5. Selecione Olá **aplicativos que minha empresa possui** opção na lista suspensa de saudação.
6. Verifique se há um aplicativo chamado **Sincronização dos Azure AD Domain Services**. Se o aplicativo hello existir, passe toodelete-lo.
7. Depois que você excluiu um aplicativo hello, tente novamente os serviços de domínio tooenable AD do Azure.

### <a name="invalid-configuration"></a>Configuração inválida
**Mensagem de erro:**

*Não foi possível habilitar os serviços de domínio neste locatário do AD do Azure. Olá serviços de domínio do aplicativo no seu locatário do AD do Azure não têm Olá necessárias permissões tooenable dos serviços de domínio. Excluir aplicativo hello com d87dcbc6-a371-462e-88e3-28ad15ec4e64 de identificador de aplicativo hello e, em seguida, tente tooenable serviços de domínio para seu locatário do AD do Azure.*

**Correção:**

Verifique toosee se você tiver um aplicativo com o nome de saudação AzureActiveDirectoryDomainControllerServices (com um identificador de aplicativo de d87dcbc6-a371-462e-88e3-28ad15ec4e64) em seu diretório do AD do Azure. Se esse aplicativo se existir, será necessário toodelete-lo e, em seguida, reabilitar o serviços de domínio do AD do Azure.

Use Olá após a aplicação de saudação do PowerShell script toofind e excluí-lo.

> [!NOTE]
> Esse script usa cmdlets do **Azure AD PowerShell versão 2**. Para obter uma lista completa de todos os cmdlets disponíveis e o módulo de saudação toodownload, leia Olá [documentação de referência do AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph desabilitado
**Mensagem de erro:**

Não foi possível habilitar os Serviços de Domínio neste locatário do Azure AD. saudação de aplicativo do AD do Microsoft Azure está desabilitada no seu locatário do AD do Azure. Habilitar o aplicativo hello com hello 00000002-0000-0000-c000-000000000000 de identificador de aplicativo e depois tente tooenable serviços de domínio para seu locatário do AD do Azure.

**Correção:**

Verifique toosee se você tiver desabilitado a um aplicativo com o identificador de saudação 00000002-0000-0000-c000-000000000000. Este aplicativo é o aplicativo do AD do Microsoft Azure hello e fornece o locatário de tooyour AD do Azure de acesso de API do Graph. Serviços de domínio do AD do Azure precisa toosynchronize de toobe habilitado esse aplicativo sua tooyour de locatário do AD do Azure gerenciado domínio.

tooresolve esse erro, habilitar este aplicativo e, em seguida, tente tooenable os serviços de domínio para seu locatário do AD do Azure.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Os usuários são toosign não é possível no toohello domínio gerenciado por serviços de domínio do AD do Azure
Se houver um ou mais usuários no seu locatário do AD do Azure não é possível toosign no domínio gerenciado toohello criado recentemente, execute Olá etapas de solução de problemas a seguir:

* **Usando o formato UPN:** tente toosign usando o formato UPN hello (por exemplo, 'joeuser@contoso.com') em vez do formato de SAMAccountName hello ('CONTOSO\joeuser'). Olá SAMAccountName pode ser gerado automaticamente para usuários cujo prefixo UPN é excessivamente longo ou Olá mesmo como outro usuário no domínio gerenciado hello. formato UPN Olá é garantido toobe exclusivo dentro de um locatário do AD do Azure.

> [!NOTE]
> É recomendável usar Olá UPN formato toosign em toohello domínio gerenciado por serviços de domínio do AD do Azure.
>
>

* Certifique-se de que você tenha [ativado a sincronização de senha](active-directory-ds-getting-started-password-sync.md) conforme Olá etapas descritas no guia de Introdução do hello.
* **Contas externas:** Certifique-se de que a conta de usuário de Olá afetado não é uma conta externa em locatário de saudação do AD do Azure. Exemplos de contas externas incluem as contas da Microsoft (por exemplo, “joe@live.com”) ou as contas de usuário de um diretório externo do Azure AD. Como os serviços de domínio do AD do Azure não tem credenciais para essas contas de usuário, esses usuários não podem entrar no domínio gerenciado toohello.
* **Sincronizar contas:** se Olá afetado contas de usuário são sincronizadas de um diretório local, verifique:

  * Ter implantado ou atualizado toohello [recomendado de mais recente versão do Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Você configurou o Azure AD Connect muito[executar uma sincronização completa](active-directory-ds-getting-started-password-sync.md).
  * Dependendo do tamanho de saudação do seu diretório, ele pode levar algum tempo para contas de usuário e credenciais hashes toobe disponível nos serviços de domínio do AD do Azure. Certifique-se de que você espera tempo suficiente antes de tentar autenticação (dependendo do tamanho de saudação do seu diretório - algumas horas tooa ou dois dias para diretórios grandes).
  * Se Olá persista após verificar Olá etapas anteriores, tente reiniciar Olá serviço de sincronização do AD do Microsoft Azure. Em seu computador de sincronização, inicie um prompt de comando e execute Olá comandos a seguir:

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **Contas de nuvem**: se a conta de usuário de saudação afetada é uma conta de usuário somente em nuvem, certifique-se de que o usuário Olá alterou sua senha após a habilitação dos serviços de domínio do AD do Azure. Esta etapa faz a credencial Olá hashes necessárias para serviços de domínio do AD do Azure toobe gerado.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Os usuários removidos do seu locatário do Azure AD não são removidos do seu domínio gerenciado
O Azure AD protege você contra a exclusão acidental de objetos de usuário. Quando você exclui uma conta de usuário do seu locatário do AD do Azure, o objeto de usuário correspondente Olá é movido toohello Lixeira. Quando essa operação de exclusão é um domínio gerenciado tooyour sincronizados, faz com que Olá correspondente toobe de conta de usuário marcado como desabilitado. Esse recurso ajuda a recuperar ou cancelar a exclusão de conta de usuário hello mais tarde.

Olá permanece na Olá desabilitado estado em seu domínio gerenciado de conta de usuário, mesmo se você recriar uma conta de usuário com hello mesmo UPN no seu diretório do AD do Azure. conta de usuário tooremove saudação do seu domínio gerenciado, você precisa tooforce excluí-lo do seu locatário do AD do Azure.

conta de usuário tooremove Olá completamente do seu domínio gerenciado, excluir usuário Olá permanentemente do seu locatário do AD do Azure. Use o cmdlet do PowerShell Remove-MsolUser Olá com hello '-RemoveFromRecycleBin' opção, conforme descrito neste [artigo do MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Entre em contato
Contate a equipe de produto do Azure Active Directory Domain Services Olá muito[compartilhar comentários ou suporte](active-directory-ds-contact-us.md).
