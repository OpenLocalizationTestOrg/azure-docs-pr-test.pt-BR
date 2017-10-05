---
title: "Introdução à Área de Trabalho do Windows no Azure AD v2 – Configuração | Microsoft Docs"
description: "Como um aplicativo .NET da Área de Trabalho do Windows (XAML) pode obter um token de acesso e chamar uma API protegida pelo ponto de extremidade do Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="050c1-103">Adicionar as informações de registro do aplicativo ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="050c1-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="050c1-104">Nesta etapa, você precisa adicionar a ID do Aplicativo ao projeto.</span><span class="sxs-lookup"><span data-stu-id="050c1-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="050c1-105">Abra `App.xaml.cs` e substitua a linha que contém a `ClientId` por:</span><span class="sxs-lookup"><span data-stu-id="050c1-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="050c1-106">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="050c1-106">What is Next</span></span>

[<span data-ttu-id="050c1-107">Testar e validar</span><span class="sxs-lookup"><span data-stu-id="050c1-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
