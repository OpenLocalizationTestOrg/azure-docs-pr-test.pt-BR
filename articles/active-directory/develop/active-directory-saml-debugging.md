---
title: "aaaHow toodebug baseado no SAML único logon tooapplications no Active Directory do Azure | Microsoft Docs"
description: "Saiba como toodebug baseado no SAML único logon tooapplications no Active Directory do Azure "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Como toodebug baseado no SAML único logon tooapplications no Active Directory do Azure
Ao depurar uma integração de aplicativos baseados em SAML, é geralmente útil toouse uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) toosee Olá solicitação SAML, resposta SAML hello e token SAML real Olá emitido toohello aplicativo. Examinando o token SAML hello, certifique-se de que todos os Olá atributos necessários, Olá nome de usuário no assunto SAML hello e Olá emissor URI são provenientes conforme o esperado.

![][1]

Olá resposta do AD do Azure que contém o token SAML Olá é normalmente Olá que ocorre após um redirecionamento HTTP 302 de https://login.windows.net e toohello enviado configurado **URL de resposta** do aplicativo hello. 

Você pode exibir o token SAML Olá selecionando essa linha e, em seguida, selecionando Olá **inspetores > WebForms** guia no painel direito da saudação. A partir daí, clique com botão direito Olá **SAMLResponse** valor e selecione **enviar tooTextWizard**. Em seguida, selecione **de Base64** de saudação **transformar** menu toodecode Olá token e ver seu conteúdo.

**Observação**: solicitar conteúdo Olá toosee este HTTP, Fiddler pode solicitar que você tooconfigure descriptografia do tráfego HTTPS, o que você precisará toodo.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](../active-directory-apps-index.md)
* [Configurando um único logon tooapplications que não estão na Galeria de aplicativos do Active Directory do Azure Olá](../active-directory-saas-custom-apps.md)
* [Como tooCustomize as declarações emitidas no hello Token SAML para aplicativos Pre-Integrated](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png