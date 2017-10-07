---
title: "pré-requisitos de catálogo de dados aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os pré-requisitos de saudação que necessário tooget Introdução ao Data Catalog do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Pré-requisitos de Catálogo de Dados do Azure

Antes de configurar o catálogo de dados do Azure, você precisa tootake respeito algumas coisas. Não se preocupe, esse processo não demora.

## <a name="azure-subscription"></a>Assinatura do Azure
tooset o catálogo de dados, você deve ser o proprietário de saudação ou coproprietário de uma assinatura do Azure.

Assinaturas do Azure ajudam a organizar os recursos de serviço toocloud de acesso, como o catálogo de dados. As assinaturas também ajudam a controlar como o uso de recursos é relatado, cobrado e pago. Cada assinatura pode ter uma configuração de cobrança e pagamento separada para que você possa ter assinaturas e planos que variam por departamento, projeto, escritório regional e assim por diante. Cada serviço de nuvem pertence tooa assinatura e toohave uma assinatura é necessário antes de configurar o catálogo de dados. mais, consulte toolearn [gerenciar contas, assinaturas e funções administrativas](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset o catálogo de dados, você deve estar conectado com uma conta de usuário do Azure Active Directory (AD do Azure).

O AD do Azure fornece uma maneira fácil para sua identidade de toomanage de negócios e acesso, tanto na nuvem hello e local. Os usuários podem usar uma único conta do trabalho ou escola para nuvem tooany de logon único e o aplicativo da web local. Catálogo de dados usa o AD do Azure tooauthenticate entrar. mais, consulte toolearn [o que é o Active Directory do Azure?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> Usando Olá [portal do Azure](http://portal.azure.com/), você pode entrar com uma conta pessoal da Microsoft ou um Azure Active Directory ou de estudante conta. tooset o catálogo de dados usando tanto Olá Olá ou o portal do Azure [portal do catálogo de dados](http://www.azuredatacatalog.com), você deve entrar com uma conta do Active Directory do Azure, não uma conta pessoal.
>
>

## <a name="active-directory-policy-configuration"></a>Configuração de política do Active Directory
Você pode encontrar uma situação em que você pode entrar no portal do catálogo de dados toohello, mas quando você tenta toosign na ferramenta de registro de fonte de dados toohello, encontrar uma mensagem de erro que impede que você entrar. Esse comportamento de problema pode ocorrer somente quando você está na rede da empresa de hello, ou isso pode ocorrer apenas quando você está se conectando fora Olá rede da empresa.

ferramenta de registro de fonte de dados Olá usa autenticação de formulários toovalidate suas credenciais de usuário no Active Directory. toohelp que você entrar com êxito, um administrador do Active Directory deve habilitar autenticação de formulários Olá política de autenticação Global.

Na política de autenticação Global do hello, métodos de autenticação podem ser habilitadas separadamente para intranet e extranet conexões, conforme mostrado no hello captura de tela a seguir. Erros de entrada podem ocorrer se a autenticação de formulários não está habilitada para rede de saudação do qual você está se conectando.

 ![Política de Autenticação Global do Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte [Configurando políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).
