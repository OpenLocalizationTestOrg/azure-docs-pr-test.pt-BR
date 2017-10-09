---
title: "recursos e a configuração de serviço aaaAzure AD Connect sincronização | Microsoft Docs"
description: "Descreve os recursos do serviço de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Recursos do serviço de sincronização do Azure AD Connect
recurso de sincronização de saudação do Azure AD Connect tem dois componentes:

* componente de local de saudação denominado **sincronização do Azure AD Connect**, também chamado **mecanismo de sincronização**.
* serviço Olá residentes no AD do Azure, também conhecido como **o serviço de sincronização do Azure AD Connect**

Este tópico explica como os recursos a seguir de saudação do hello **o serviço de sincronização do Azure AD Connect** funcionam e como você pode configurá-los usando o Windows PowerShell.

Essas configurações são definidas por Olá [Azure módulo Active Directory para Windows PowerShell](http://aka.ms/aadposh). Baixe e instale-o separadamente do Azure AD Connect. cmdlets de saudação documentadas neste tópico foram introduzidos no hello [versão de março de 2016 (compilação 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Se você não tem os cmdlets de saudação documentados neste tópico ou eles não produzem Olá mesmo resultado, em seguida, certifique-se de você executar a versão mais recente do hello.

configuração de saudação toosee em seu diretório do AD do Azure, execute `Get-MsolDirSyncFeatures`.  
![Resultado de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Muitas dessas configurações podem ser alteradas somente pelo Azure AD Connect.

Olá configurações a seguir podem ser configuradas por `Set-MsolDirSyncFeature`:

| DirSyncFeature | Comentário |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Permite que objetos toojoin userPrincipalName no endereço de tooprimary SMTP de adição. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Permite atributo do hello sincronização mecanismo tooupdate Olá userPrincipalName gerenciados/licenciado usuários (não federados). |

Depois que você habilitar um recurso, ele não poderá ser desabilitado novamente.

> [!NOTE]
> De 24 de agosto de 2016 Olá recurso *duplicado resiliência do atributo* é habilitado por padrão para o novo Azure diretórios do AD. Este recurso também será distribuído e habilitado em diretórios criados antes dessa data. Você receberá uma notificação por email quando o diretório é sobre tooget esse recurso habilitado.
> 
> 

Olá configurações a seguir são configuradas pelo Azure AD Connect e não pode ser modificadas por `Set-MsolDirSyncFeature`:

| DirSyncFeature | Comentário |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: habilitando o write-back do dispositivo](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Sincronização do Azure AD Connect: extensões do Directory](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Permite que um toobe de atributo em quarentena quando ele é uma duplicata de outro objeto, em vez de falha do objeto inteiro Olá durante a exportação. |
| PasswordSync |[Implementação de sincronização de senha com a sincronização do Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Visualização: write-back de grupo](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Não há suporte no momento. |

## <a name="duplicate-attribute-resiliency"></a>Duplicar a resiliência do atributo
Em vez de falhar tooprovision objetos com UPNs duplicados / proxyAddresses, atributo duplicado Olá é "em quarentena" e um valor temporário é atribuído. Quando a saudação conflito é resolvido, Olá temporário UPN é alterada automaticamente o valor adequado toohello. Para obter mais detalhes, consulte [Sincronização de identidades e resiliência do atributo duplicado](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>Correspondência suave de UserPrincipalName
Quando esse recurso está habilitado, correspondência de software está habilitada para UPN na adição toohello [endereço SMTP primário](https://support.microsoft.com/kb/2641663), que está sempre habilitado. Soft-match é usado toomatch usuários de nuvem existente no AD do Azure com usuários locais.

Se você precisar toomatch contas com contas existentes criadas na nuvem de saudação do AD local e você não estiver usando o Exchange Online, esse recurso é útil. Nesse cenário, você geralmente não tem um atributo de SMTP do motivo tooset Olá na nuvem de saudação.

O recurso fica ativado por padrão para diretórios recém-criados do Azure AD. Você pode ver se este recurso está habilitado executando:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Se o recurso não estiver habilitado para seu diretório do Azure AD, você poderá habilitá-lo executando:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Sincronizar atualizações de userPrincipalName
Historicamente, atributo de UserPrincipalName toohello atualizações usando o serviço de sincronização de saudação do local foi bloqueado, a menos que as duas condições forem verdadeiras:

* usuário Olá é gerenciado (não federados).
* não foi atribuído uma licença ao usuário Hello.

Para obter mais detalhes, consulte [usuário nomes no Office 365, Azure ou Intune não correspondem Olá UPN local ou ID de logon alternativo](https://support.microsoft.com/kb/2523192).

Habilitar esse recurso permite Olá sincronização mecanismo tooupdate Olá userPrincipalName quando ele for alterado no local e você usar a sincronização de senha. Se você usar a federação, não haverá suporte pra este recurso.

O recurso fica ativado por padrão para diretórios recém-criados do Azure AD. Você pode ver se este recurso está habilitado executando:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Se o recurso não estiver habilitado para seu diretório do Azure AD, você poderá habilitá-lo executando:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Depois de habilitar esse recurso, os valores existentes de userPrincipalName permanecerão os mesmos. Na próxima alteração de saudação userPrincipalName atributo local, sincronização de delta normal de saudação em usuários atualizará Olá UPN.  

## <a name="see-also"></a>Consulte também
* [Sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).

