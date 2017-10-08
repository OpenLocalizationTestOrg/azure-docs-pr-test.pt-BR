---
title: "controles de página de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os controles de página Olá disponíveis para uso em modelos de portal do desenvolvedor no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Controles de página do Gerenciamento de API do Azure
Gerenciamento de API do Azure fornece Olá controles para uso em modelos portal do desenvolvedor Olá a seguir.  
  
 toouse um controle, colocá-lo no local de saudação desejada no modelo de portal de desenvolvedor hello. Alguns controles, como Olá [ações de aplicativo](#app-actions) controlar, tiver parâmetros, conforme mostrado no exemplo a seguir de saudação.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 valores Hello para parâmetros de saudação são passados como parte do modelo de dados Olá para o modelo de saudação. Na maioria dos casos, você poderá simplesmente colar em Olá fornecido exemplo para cada controle para que ele toowork corretamente. Para obter mais informações sobre valores de parâmetro hello, você pode ver a seção de modelo de dados Olá para cada modelo no qual um controle pode ser usado.  
  
 Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Controles de página do modelo do portal do desenvolvedor  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [providers](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 Olá `app-actions` controle fornece uma interface do usuário para interagir com aplicativos na página de perfil de usuário Olá no portal do desenvolvedor hello.  
  
 ![controle app&#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "controle app-actions do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|appId|id de saudação do aplicativo hello.|  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `app-actions` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Aplicativos](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 Olá `basic-signin` controle fornece um controle de entrada do usuário coleta informações Olá entrar na página no portal do desenvolvedor hello.  
  
 ![controle basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "controle basic-signin do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `basic-signin` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Entrar](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 Olá `paging-control` fornece funcionalidade de paginação desenvolvedor páginas do portal que exibem uma lista de itens.  
  
 ![controle paging](./media/api-management-page-controls/APIM-paging-control.png "controle paging do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `paging-control` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Lista de APIs](api-management-api-templates.md#APIList)  
  
-   [Lista de problemas](api-management-issue-templates.md#IssueList)  
  
-   [Lista de produtos](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 Olá `providers` controle fornece um controle para seleção de provedores de autenticação na página no portal do desenvolvedor Olá Olá entrada.  
  
 ![controle providers](./media/api-management-page-controls/APIM-providers-control.png "controle providers do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `providers` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Entrar](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 Olá `search-control` fornece funcionalidade de pesquisa em desenvolvedor páginas do portal que exibem uma lista de itens.  
  
 ![controle search](./media/api-management-page-controls/APIM-search-control.png "controle search do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `search-control` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Lista de APIs](api-management-api-templates.md#APIList)  
  
-   [Lista de produtos](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 Olá `sign-up` controle fornece um controle para coletar informações de perfil do usuário na página no portal do desenvolvedor Olá de inscrição hello.  
  
 ![controle sign&#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "controle sign-up do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `sign-up` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Inscrever-se](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 Olá `subscribe-button` fornece um controle de assinatura de um produto de tooa do usuário.  
  
 ![controle subscribe&#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "controle subscribe-button do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `subscribe-button` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Produto](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 Olá `subscription-cancel` controle fornece um controle para cancelar um produto de tooa de assinatura na página de perfil de usuário Olá no portal do desenvolvedor hello.  
  
 ![controle subscription&#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "controle subscription-cancel do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|subscriptionId|id de saudação do hello toocancel de assinatura.|  
|cancelUrl|Cancelar a assinatura Olá URL.|  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 Olá `subscription-cancel` controle pode ser usado em Olá seguindo os modelos de portal do desenvolvedor.  
  
-   [Produto](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).
