---
title: "Introdução ao Azure AD em projetos WebApi do Visual Studio | Microsoft Docs"
description: "Como começar a usar o Active Directory do Azure em projetos da API Web após a conexão ou criação de um AD do Azure usando os serviços conectados do Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: mtillman
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 3d510c193ab8c7e65340275017cb2dcd4c76def0
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a>Introdução ao Active Directory do Azure e aos serviços conectados do Visual Studio (projetos da API Web)
> [!div class="op_single_selector"]
> * [Introdução](vs-active-directory-webapi-getting-started.md)
> * [O que aconteceu](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a>Exigir autenticação para acessar os controladores
Todos os controladores em seu projeto foram marcados com o atributo **Autorizar** . Este atributo exige que o usuário seja autenticado antes de acessar as APIs definidas por esses controladores. Para permitir que o controlador seja acessado anonimamente, remova este atributo do controlador. Se desejar definir as permissões em um nível mais granular, aplique o atributo a cada método que necessita de autorização em vez de aplicá-lo à classe do controlador.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre o Active Directory do Azure](https://azure.microsoft.com/services/active-directory/)

