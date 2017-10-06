---
title: "Aplicativo de extensões – Azure AD B2C | Microsoft Docs"
description: "Restaurando Olá b2c extensões de aplicativo"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: aplicativo de extensões

Quando um diretório do Azure AD B2C é criado, um aplicativo chamado `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` é criado automaticamente dentro de saudação novo diretório. Este aplicativo, Olá chamado tooas **b2c de extensões de aplicativo**, está visível no *registros do aplicativo*. Ele é usado por Olá informações de toostore de serviço do Azure AD B2C sobre usuários e atributos personalizados. Se o aplicativo hello for excluído, Azure AD B2C não funcionará corretamente e seu ambiente de produção será afetado.

> [!IMPORTANT]
> Não exclua Olá b2c extensões de aplicativo, a menos que você pretende excluir tooimmediately seu locatário. Se o aplicativo hello permaneça excluído por mais de 30 dias, informações do usuário será permanentemente perdidas.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Verificando o aplicativo hello extensões está presente

tooverify que Olá b2c de extensões de aplicativo está presente:

1. Dentro de seu locatário do Azure AD B2C, clique em **mais serviços** no menu de navegação à esquerda de saudação.
1. Procure e abra **Registros de aplicativo**.
1. Procure um aplicativo que comece com **b2c-extensions-app**

## <a name="recover-hello-extensions-app"></a>Recuperar o aplicativo de extensões de saudação

Se você excluiu acidentalmente Olá b2c extensões de aplicativo, você tem 30 dias toorecovê-lo. Você pode restaurar o aplicativo hello usando Olá API do Graph:

1. Procurar muito[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Faça logon no site toohello como um administrador global para o diretório do Azure AD B2C Olá que você deseja toorestore Olá excluído aplicativo para.
1. Emitir um HTTP GET em relação a URL de saudação `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` com api-version = 1.6. Certifique-se de que tooreplace `{tenantName}` com o nome do locatário. Esta operação irá listar todos os aplicativos de saudação que tenham sido excluídos no hello últimos 30 dias.
1. Encontre o aplicativo hello na lista de saudação onde nome hello começa com 'aplicativo de extensão b2c' e copie seu `objectid` o valor da propriedade.
1. Emitir um HTTP POST com relação à URL Olá `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Substituir saudação `{OBJECTID}` parte da URL Olá Olá `objectid` da etapa anterior hello. 

Você poderá muito[consulte aplicativo hello restaurado](#verifying-that-the-extensions-app-is-present) em Olá portal do Azure.

> [!NOTE]
> Um aplicativo só pode ser restaurado se ele foi excluído no hello últimos 30 dias. Se tiverem se passado mais de 30 dias, os dados serão permanentemente perdidos. Para obter mais ajuda, abra um tíquete de suporte.
