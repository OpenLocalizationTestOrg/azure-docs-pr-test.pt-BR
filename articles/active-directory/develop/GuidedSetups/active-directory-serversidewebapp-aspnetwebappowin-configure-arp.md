---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - Config | Microsoft Docs"
description: "Implementando a opção Entrar com uma Conta da Microsoft em uma solução ASP.NET com um aplicativo tradicional baseado em navegador da Web usando o padrão OpenID Connect"
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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Configurar seu aplicativo da Web ASP.NET com informações de registro do aplicativo hello

Nesta etapa, você irá configurar seu projeto toouse SSL e use Olá SSL URL tooconfigure informações de registro do seu aplicativo. Depois disso, adicionar o aplicativo hello' solução de tooyour de informações de registro por meio de *Web. config*.

1.  No Solution Explorer, selecione o projeto hello e observe Olá `Properties` janela (se você não vir uma janela de propriedades, pressione F4)
2.  Alterar `SSL Enabled` muito`True`
3.  Copie o valor de saudação do `SSL URL` acima e cole-o no hello `Redirect URL` campo na parte superior da saudação desta página, clique em *atualização*:<br/><br/>![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Adicione a seguinte Olá em `web.config` arquivo localizado na pasta da raiz, na seção `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
