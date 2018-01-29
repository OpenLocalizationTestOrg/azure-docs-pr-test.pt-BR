---
title: "Controles de página do Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre os controles de página disponíveis para uso em modelos de portal do desenvolvedor no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/20/2017
ms.author: apimpm
ms.openlocfilehash: 4fd91ae079ff054932f4572874001dd69dd848e7
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="azure-api-management-page-controls"></a>Controles de página do Gerenciamento de API do Azure
O Gerenciamento de API do Azure fornece os controles a seguir para uso em modelos de portal do desenvolvedor.  
  
Para usar um controle, coloque-o no local desejado no modelo do portal do desenvolvedor. Alguns controles, como o [app-actions](#app-actions), têm parâmetros, como mostrado no exemplo a seguir:  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 Os valores para os parâmetros são passados como parte do modelo de dados do modelo. Na maioria dos casos, você pode simplesmente colar o exemplo fornecido para cada controle para que ele funcione corretamente. Para obter mais informações sobre os valores de parâmetro, você pode ver a seção de modelo de dados de cada modelo no qual um controle pode ser usado.  
  
 Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
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
 O controle `app-actions` fornece uma interface de usuário para interação com aplicativos na página de perfil do usuário no portal do desenvolvedor.  
  
 ![controle app&#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "controle app-actions do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|appId|A ID do aplicativo.|  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `app-actions` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Aplicativos](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 O controle `basic-signin` fornece um controle para coletar informações de entrada do usuário na página de entrada do portal do desenvolvedor.  
  
 ![controle basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "controle basic-signin do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `basic-signin` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Entrar](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 O `paging-control` fornece funcionalidade de paginação nas páginas do portal do desenvolvedor que exibem uma lista de itens.  
  
 ![controle paging](./media/api-management-page-controls/APIM-paging-control.png "controle paging do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `paging-control` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Lista de APIs](api-management-api-templates.md#APIList)  
  
-   [Lista de problemas](api-management-issue-templates.md#IssueList)  
  
-   [Lista de produtos](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 O controle `providers` fornece um controle para seleção de provedores de autenticação na página de entrada do portal do desenvolvedor.  
  
 ![controle providers](./media/api-management-page-controls/APIM-providers-control.png "controle providers do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `providers` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Entrar](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 O `search-control` fornece funcionalidade de pesquisa nas páginas do portal do desenvolvedor que exibem uma lista de itens.  
  
 ![controle search](./media/api-management-page-controls/APIM-search-control.png "controle search do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `search-control` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Lista de APIs](api-management-api-templates.md#APIList)  
  
-   [Lista de produtos](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 O controle `sign-up` fornece um controle para coletar informações de perfil do usuário na página de entrada do portal do desenvolvedor.  
  
 ![controle sign&#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "controle sign-up do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `sign-up` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Inscrever-se](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 O `subscribe-button` fornece um controle de assinatura de um usuário para um produto.  
  
 ![controle subscribe&#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "controle subscribe-button do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>parâmetros  
 Nenhuma.  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `subscribe-button` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Produto](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 O controle `subscription-cancel` fornece um controle para cancelar uma assinatura de um produto na página de perfil do usuário no portal do desenvolvedor.  
  
 ![controle subscription&#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "controle subscription-cancel do APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|subscriptionId|A ID da assinatura a ser cancelada.|  
|cancelUrl|A assinatura cancela a URL.|  
  
### <a name="developer-portal-templates"></a>Modelos de portal do desenvolvedor  
 O controle `subscription-cancel` pode ser usado nos modelos de portal do desenvolvedor a seguir:  
  
-   [Produto](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).