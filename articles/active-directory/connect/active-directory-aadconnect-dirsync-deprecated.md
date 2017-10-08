---
title: "aaaUpgrade do DirSync e sincronização do AD do Azure | Microsoft Docs"
description: "Descreve como tooupgrade de tooAzure DirSync e sincronização do AD do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Atualizar o Windows Azure Active Directory Sync e o Azure Active Directory Sync
Conexão do AD do Azure é Olá tooconnect de maneira melhor seu diretório local com o Azure AD e Office 365. Este é um tooAzure de tooupgrade bastante AD Connect de sincronização de diretório ativo (DirSync) do Windows Azure ou Azure AD Sync, essas ferramentas são preteridos-los agora e chegará ao fim do suporte em 13 de abril de 2017.

Olá dois identidade ferramentas de sincronização que são substituídas foram oferecidas para clientes de floresta única (DirSync) em várias florestas e outros clientes avançados (Azure AD Sync). Essas ferramentas mais antigas foram substituídas por uma solução única que está disponível para todos os cenários: o Azure AD Connect. Ele oferece nova funcionalidade, aprimoramentos de recursos e suporte a novos cenários. toobe capaz de toocontinue toosynchronize sua tooAzure de dados de identidade local AD e Office 365, é altamente recomendável que você atualize tooAzure AD Connect.

última versão de saudação do DirSync foi lançado em julho de 2014 e a última versão de saudação do Azure AD Sync foi lançado em maio de 2015.

## <a name="what-is-azure-ad-connect"></a>O que é o Azure AD Connect
Conexão do AD do Azure é Olá sucessor tooDirSync e sincronização do AD do Azure. Ele combina todos os cenários aos quais essas duas ferramentas prestavam suporte. Você pode ler mais a respeito em [Como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Agenda de preterição
| Data | Comentário |
| --- | --- |
| 13 de abril de 2016 |O Windows Azure Active Directory Sync ("DirSync") e o Microsoft Azure Active Directory Sync ("Azure AD Sync") são anunciados como preteridos. |
| 13 de abril de 2017 |O suporte termina. Os clientes não será capaz de tooopen um caso de suporte sem atualizar tooAzure AD se conectar pela primeira vez. |
|31 de dezembro de 2017|O Azure AD deixará de aceitar comunicações da Sincronização do Microsoft Azure Active Directory (“DirSync”) e da Sincronização do Microsoft Azure Active Directory (“Azure AD Sync”).

## <a name="how-tootransition-tooazure-ad-connect"></a>Como tootransition tooAzure AD Connect
Se você está executando o DirSync, há duas maneiras de atualizar: atualização in-loco e implantação paralela. Uma atualização in-loco é recomendada para a maioria dos clientes e se você tem um sistema operacional recente e com menos de 50.000 objetos. Em outros casos, é recomendável toodo uma implantação paralela em que a configuração do DirSync é movido tooa novo servidor executando o Azure AD Connect.

Se você usa o Azure AD Sync, recomenda-se uma atualização in-loco. Se desejar, é possível tooinstall um novo servidor do Azure AD Connect em paralelo e fazer uma migração de giro do seu tooAzure de servidor de sincronização do AD do Azure AD Connect.

| Solução | Cenário |
| --- | --- |
| [Atualização do DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Se você tiver um servidor DirSync existente já em execução.</li> |
| [Atualização do Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>Se você estiver migrando do Azure AD Sync.</li> |

Se você quiser toosee como toodo uma in-loco atualizar do DirSync tooAzure AD Connect, em seguida, consulte este vídeo do Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Perguntas frequentes
**P: recebeu uma notificação por email de Olá, equipe do Azure e/ou em uma mensagem do Centro de mensagens do Office 365 hello, mas usando o Connect.**  
notificação de saudação também foi enviada toocustomers usando o Azure AD Connect com um número de versão 1.0. \*.0 (usando uma versão pre-1.1). A Microsoft recomenda que os clientes libera toostay atual com o Azure AD Connect. Olá [atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) recurso introduzido no 1.1 torna fácil tooalways tem uma versão recente do Azure AD Connect instalado.

**P: O DirSync/Azure AD Sync deixarão de funcionar em 13 de abril de 2017?**  
Sincronização do AD do Azure/DirSync continuará toowork em 13 de abril de 2017.  No entanto, o Azure AD deixará de aceitar comunicações do DirSync e do Azure AD Sync em 31 de dezembro de 2017.

**P: A partir de quais versões do DirSync eu posso atualizar?**  
É tooupgrade com suporte de qualquer versão do DirSync está sendo usado atualmente.

**P: como hello conector AD do Azure para FIM/MIM?**  
Olá conector AD do Azure para MIM/FIM tem **não** foram anunciados como substituídos. Ele se encontra no **estado de congelamento de recursos**. Nenhuma funcionalidade nova foi adicionada e ele não recebe correções de bug. A Microsoft recomenda a clientes que usam o toomove tooplan dele tooAzure AD Connect. É altamente recomendável toonot iniciar todas as novas implantações usá-lo. Este conector será anunciado preterido no hello futuras.

## <a name="additional-resources"></a>Recursos adicionais
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
