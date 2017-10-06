---
title: "Sincronização do Azure AD Connect: extensões do Directory | Microsoft Docs"
description: "Este tópico descreve o recurso de extensões de diretório Olá no Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Sincronização do Azure AD Connect: extensões do Directory
Extensões de diretório permite que você tooextend esquema de saudação no Azure AD com seus próprios atributos do Active Directory no local. Esse recurso permite que aplicativos LOB toobuild consumindo atributos continuar toomanage local. Esses atributos podem ser consumidos por meio de [extensões de diretório do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) ou [Microsoft Graph](https://graph.microsoft.io/). Você pode ver Olá atributos disponíveis usando [explorer do Azure AD Graph](https://graphexplorer.cloudapp.net) e [explorer Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivamente.

No momento, nenhuma carga de trabalho do Office 365 consome esses atributos.

Configurar quais atributos adicionais você deseja toosynchronize no caminho de configurações personalizadas de saudação no Assistente de instalação de saudação.
![Assistente de Extensão do Esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
instalação de saudação mostra Olá atributos, que são candidatas válidas a seguir:

* Tipos de objeto de Usuário e de Grupo
* Atributos de valor único: String, Boolean, Integer, Binary
* Atributos de vários valores: String, Binary

lista de saudação de atributos é lido no cache de esquema de saudação criado durante a instalação do Azure AD Connect. Se você tiver estendido o esquema do Active Directory Olá com atributos adicionais, Olá [esquema deve ser atualizado](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) antes que esses novos atributos são visíveis.

Um objeto no AD do Azure pode ter atributos de extensões de diretório too100. comprimento máximo de saudação é de 250 caracteres. Se um valor de atributo for maior, em seguida, ele será truncado pelo mecanismo de sincronização de saudação.

Durante a instalação do Azure AD Connect, é registrado um aplicativo no qual esses atributos estão disponíveis. Você pode ver este aplicativo no portal do Azure de saudação.  
![Aplicativo de extensão do esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Esses atributos agora estão disponíveis por meio do Graph:   
![Gráfico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

atributos de saudação são prefixados com extensão\_{AppClientId}\_. Olá AppClientId tem Olá mesmo valor para todos os atributos no seu locatário do AD do Azure.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
