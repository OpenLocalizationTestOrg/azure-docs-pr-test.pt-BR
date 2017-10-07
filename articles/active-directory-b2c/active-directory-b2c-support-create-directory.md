---
title: "Azure Active Directory B2C: solucionar problemas criando locatários | Microsoft Docs"
description: "Problemas e resoluções para criar um Azure Active Directory ou um locatário do Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>Problemas e resoluções para criar um Azure Active Directory ou um locatário do Azure Active Directory B2C 

## <a name="create-an-azure-ad-tenant"></a>Criar um locatário do Azure AD
Se você não pode criar um locatário do Azure Active Directory (AD do Azure) na primeira tentativa de hello, tente novamente. Se Olá problema persistir, entre em contato com o suporte do Azure.

## <a name="create-an-azure-ad-b2c-tenant"></a>Criar um locatário do Azure AD B2C
Se você encontrar problemas quando você [criar um B2C do Azure Active Directory (Azure AD B2C) locatário](active-directory-b2c-get-started.md), tente Olá as opções a seguir:

* Se o locatário de saudação do Azure AD B2C não aparecer na lista de locatários, tente novamente toocreate locatário de saudação.
* Se o locatário hello Azure AD B2C aparecerão na lista de locatários e consulte Olá a seguinte mensagem de erro, exclua locatário hello e criá-la novamente:

    "Não foi possível concluir a criação de saudação do locatário de B2C Olá 'contosob2c'. Acesse este [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) para obter mais diretrizes".
* Há são problemas conhecidos quando você excluir um existente B2C de AD do Azure locatário e recriá-la usando Olá mesmo nome de domínio. Quando você criar um novo locatário do Azure AD B2C, você deverá usar um nome de domínio diferente.
* Se essas resoluções não funcionarem, entre em contato com o Suporte do Azure. Para obter mais informações, consulte [Arquivar solicitações de suporte para o Azure AD B2C](active-directory-b2c-support.md).

