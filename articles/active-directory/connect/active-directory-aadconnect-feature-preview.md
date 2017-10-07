---
title: "Azure AD Connect: recursos em visualização | Microsoft Docs"
description: "Este tópico descreve em mais detalhes os recursos que estão na visualização no Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Mais detalhes sobre os recursos no modo de visualização
Este tópico descreve como toouse recursos atualmente na visualização.

## <a name="group-writeback"></a>Write-back de grupo
opção de saudação para write-back de grupo de recursos opcionais permite toowriteback **grupos do Office 365** tooa floresta com o Exchange instalado. Esse é um grupo que é sempre controlado na nuvem hello. Se você tiver o Exchange no local, em seguida, você pode write-back esses grupos tooon local para enviar e receber emails destes grupos de usuários com uma caixa de correio do Exchange no local.

Para obter mais informações sobre grupos do Office 365 e como toouse-los podem ser encontrados [aqui](http://aka.ms/O365g).

Um grupo do Office 365 é representado como um grupo de distribuição no AD DS local. Seu Exchange server local deve ser no Exchange 2013 atualização cumulativa 8 (lançado em março de 2015) ou Exchange 2016 toorecognize esse novo tipo de grupo.

**Anotações durante a visualização de saudação**

* atributo de catálogo de endereço Olá não é populado atualmente na visualização de saudação. Sem esse atributo, o grupo de saudação não está visível no hello GAL. Olá toopopulate de maneira mais fácil esse atributo é um cmdlet de PowerShell do Exchange Olá toouse `update-recipient`.
* Somente as florestas com o esquema de saudação do Exchange são destinos válidos para grupos. Se nenhum Exchange for detectado, Write-back de grupo não é possível tooenable.
* Somente implantações de floresta única de organização do Exchange terão suporte atualmente. Se você tiver mais de uma organização de Exchange no local, em seguida, você precisa uma solução GALSync de local para tooappear esses grupos em sua outras florestas.
* recurso de write-back de grupo Olá não lida com grupos de segurança ou grupos de distribuição.

> [!NOTE]
> TooAzure uma assinatura Premium do AD é necessária para write-back de grupo.
> 
>

## <a name="user-writeback"></a>Write-back de usuário
> [!IMPORTANT]
> Olá recurso de visualização de write-back de usuário foi removido na tooAzure de atualização de agosto de 2015 Olá AD Connect. Se você tiver habilitado, você deve desabilitar esse recurso.
>
>

## <a name="next-steps"></a>Próximas etapas
Continuar a [Instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Saiba mais sobre a [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md).
