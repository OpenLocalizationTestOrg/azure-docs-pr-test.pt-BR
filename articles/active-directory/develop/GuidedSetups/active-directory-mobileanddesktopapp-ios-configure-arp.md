---
title: "aaaAzure AD v2 iOS guia de Introdução - configurar ARP () | Microsoft Docs"
description: Como aplicativos iOS (Swift) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="73bda-103">Adicionar aplicativo de tooyour de informações de registro do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="73bda-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="73bda-104">Nesta etapa, você precisa de projeto de tooyour tooadd Olá Id do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="73bda-104">In this step, you need tooadd hello Application Id tooyour project:</span></span>

1.  <span data-ttu-id="73bda-105">Em `ViewController.swift`, substitua a linha hello começando com '`let kClientID`' com:</span><span class="sxs-lookup"><span data-stu-id="73bda-105">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="73bda-106">CTRL + clique <code>Info.plist</code> toobring até o menu contextual hello e, em seguida, clique em: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="73bda-106">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="73bda-107">Em Olá <code>dict</code> nó raiz, adicione o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="73bda-107">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
