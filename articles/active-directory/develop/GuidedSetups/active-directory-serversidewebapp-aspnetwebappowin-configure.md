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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar um aplicativo (Expresso)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Insira um nome para o aplicativo e seu email
3.  Verifique se a opção Olá para a instalação interativa está marcada
4.  Siga as instruções de saudação tooadd um aplicativo de tooyour URL de redirecionamento

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo
2. Insira um nome para o aplicativo e seu email 
3.  Verifique se a opção Olá para a instalação interativa está desmarcada
4.  Clique em `Add Platform` e selecione `Web`
5.  Voltar tooVisual Studio e, no Gerenciador de soluções, selecione o projeto de saudação e examinar a janela de propriedades de saudação (se você não vir uma janela de propriedades, pressione F4)
6.  Alterar também o SSL habilitado`True`
7.  Copiar URL de SSL da saudação e adicionar esta lista de toohello URL de URLs de redirecionamento lista do Portal de registro Olá de URLs de redirecionamento:<br/><br/>![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Adicione a seguinte Olá em `web.config` localizado na pasta raiz de saudação na seção Olá `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Substituir `ClientId` com hello Id de aplicativo que você acabou de registrar
</li>
<li>
Substituir `redirectUri` com hello SSL URL de seu projeto
</li>
</ol>
<!-- End Docs -->
