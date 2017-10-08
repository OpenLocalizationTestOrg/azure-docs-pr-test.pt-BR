---
title: "aaaAzure AD v2 Windows Desktop Introdução - Config | Microsoft Docs"
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
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Adicionar aplicativo de tooyour de informações de registro do aplicativo hello
Nesta etapa, você precisa de projeto de tooyour tooadd Olá Id do aplicativo.

1.  Abra `App.xaml.cs` e substitua a linha hello contendo Olá `ClientId` com:

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a>Próximas etapas

[Testar e validar](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
