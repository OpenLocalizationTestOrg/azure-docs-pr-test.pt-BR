---
title: "Modelos de perfil de usuário no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como personalizar o conteúdo das páginas de Perfil de usuário no portal do desenvolvedor do Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="b68f1-103">Modelos de perfil de usuário no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="b68f1-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="b68f1-104">O Gerenciamento de API do Azure fornece a capacidade de personalizar o conteúdo das páginas do portal do desenvolvedor usando um conjunto de modelos que configura o respectivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b68f1-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="b68f1-105">Usando a sintaxe [DotLiquid](http://dotliquidmarkup.org/) e o editor de sua escolha, como o [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), bem como um conjunto fornecido de [Recursos de cadeia de caracteres](api-management-template-resources.md#strings), [Recursos do Glyph](api-management-template-resources.md#glyphs) e [Controles de página](api-management-page-controls.md) localizados, você tem grande flexibilidade para configurar o conteúdo das páginas, conforme a necessidade, usando esses modelos.</span><span class="sxs-lookup"><span data-stu-id="b68f1-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="b68f1-106">Os modelos desta seção permitem personalizar o conteúdo das páginas de perfil de usuário no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b68f1-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="b68f1-107">Perfil</span><span class="sxs-lookup"><span data-stu-id="b68f1-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="b68f1-108">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="b68f1-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="b68f1-109">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="b68f1-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="b68f1-110">Atualizar informações da conta</span><span class="sxs-lookup"><span data-stu-id="b68f1-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="b68f1-111">Os modelos de amostra padrão estão incluídos na documentação a seguir, mas estão sujeitos à alteração devido a melhorias contínuas.</span><span class="sxs-lookup"><span data-stu-id="b68f1-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="b68f1-112">Você pode exibir os modelos padrão em tempo real no portal do desenvolvedor, navegando até os modelos individuais desejados.</span><span class="sxs-lookup"><span data-stu-id="b68f1-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="b68f1-113">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="b68f1-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="b68f1-114"><a name="Profile"></a> Perfil</span><span class="sxs-lookup"><span data-stu-id="b68f1-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="b68f1-115">O modelo **perfil** permite que você personalize a seção de perfil do usuário da página correspondente no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b68f1-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b68f1-116">![Página de perfil do usuário](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Página de perfil do usuário de APIM")</span><span class="sxs-lookup"><span data-stu-id="b68f1-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b68f1-117">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="b68f1-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="b68f1-118">Controles</span><span class="sxs-lookup"><span data-stu-id="b68f1-118">Controls</span></span>  
 <span data-ttu-id="b68f1-119">Este modelo pode não usar nenhum [controle de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="b68f1-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="b68f1-120">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="b68f1-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b68f1-121">Os modelos [Perfil](#Profile), [Aplicativos](#Applications) e [Assinaturas](#Subscriptions) compartilham o mesmo modelo de dados e recebem os mesmos dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="b68f1-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="b68f1-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b68f1-122">Property</span></span>|<span data-ttu-id="b68f1-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="b68f1-123">Type</span></span>|<span data-ttu-id="b68f1-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="b68f1-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b68f1-125">firstName</span><span class="sxs-lookup"><span data-stu-id="b68f1-125">firstName</span></span>|<span data-ttu-id="b68f1-126">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-126">string</span></span>|<span data-ttu-id="b68f1-127">O primeiro nome do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-127">First name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-128">lastName</span><span class="sxs-lookup"><span data-stu-id="b68f1-128">lastName</span></span>|<span data-ttu-id="b68f1-129">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-129">string</span></span>|<span data-ttu-id="b68f1-130">O sobrenome do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-131">companyName</span><span class="sxs-lookup"><span data-stu-id="b68f1-131">companyName</span></span>|<span data-ttu-id="b68f1-132">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-132">string</span></span>|<span data-ttu-id="b68f1-133">O nome da empresa do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="b68f1-134">addresserEmail</span></span>|<span data-ttu-id="b68f1-135">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-135">string</span></span>|<span data-ttu-id="b68f1-136">Endereço de email do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="b68f1-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="b68f1-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="b68f1-138">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-138">string</span></span>|<span data-ttu-id="b68f1-139">URL relativa para exibir a análise para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="b68f1-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="b68f1-140">subscriptions</span></span>|<span data-ttu-id="b68f1-141">Coleção de entidades de [Assinatura](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="b68f1-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="b68f1-142">As assinaturas da usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="b68f1-143">de dimensionamento da Web</span><span class="sxs-lookup"><span data-stu-id="b68f1-143">applications</span></span>|<span data-ttu-id="b68f1-144">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="b68f1-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="b68f1-145">Os aplicativos do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="b68f1-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="b68f1-146">changePasswordUrl</span></span>|<span data-ttu-id="b68f1-147">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-147">string</span></span>|<span data-ttu-id="b68f1-148">A URL relativa para alterar a senha do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="b68f1-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="b68f1-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="b68f1-150">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-150">string</span></span>|<span data-ttu-id="b68f1-151">A URL relativa para alterar o nome e o email para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="b68f1-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="b68f1-152">canChangePassword</span></span>|<span data-ttu-id="b68f1-153">booleano</span><span class="sxs-lookup"><span data-stu-id="b68f1-153">boolean</span></span>|<span data-ttu-id="b68f1-154">Se o usuário atual pode alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="b68f1-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="b68f1-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="b68f1-155">isSystemUser</span></span>|<span data-ttu-id="b68f1-156">booleano</span><span class="sxs-lookup"><span data-stu-id="b68f1-156">boolean</span></span>|<span data-ttu-id="b68f1-157">Se o usuário atual é membro de um dos [grupos](api-management-key-concepts.md#groups) internos.</span><span class="sxs-lookup"><span data-stu-id="b68f1-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b68f1-158">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="b68f1-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="b68f1-159"><a name="Subscriptions"></a> Assinaturas</span><span class="sxs-lookup"><span data-stu-id="b68f1-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="b68f1-160">O modelo **Assinaturas** permite que você personalize a seção de assinaturas da página de perfil do usuário no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b68f1-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b68f1-161">![Página de assinatura de usuário](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Página de assinatura de usuário do APIM")</span><span class="sxs-lookup"><span data-stu-id="b68f1-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b68f1-162">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="b68f1-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="b68f1-163">Controles</span><span class="sxs-lookup"><span data-stu-id="b68f1-163">Controls</span></span>  
 <span data-ttu-id="b68f1-164">Este modelo pode usar os seguintes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="b68f1-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b68f1-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="b68f1-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="b68f1-166">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="b68f1-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b68f1-167">Os modelos [Perfil](#Profile), [Aplicativos](#Applications) e [Assinaturas](#Subscriptions) compartilham o mesmo modelo de dados e recebem os mesmos dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="b68f1-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="b68f1-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b68f1-168">Property</span></span>|<span data-ttu-id="b68f1-169">Tipo</span><span class="sxs-lookup"><span data-stu-id="b68f1-169">Type</span></span>|<span data-ttu-id="b68f1-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="b68f1-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b68f1-171">firstName</span><span class="sxs-lookup"><span data-stu-id="b68f1-171">firstName</span></span>|<span data-ttu-id="b68f1-172">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-172">string</span></span>|<span data-ttu-id="b68f1-173">O primeiro nome do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-173">First name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-174">lastName</span><span class="sxs-lookup"><span data-stu-id="b68f1-174">lastName</span></span>|<span data-ttu-id="b68f1-175">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-175">string</span></span>|<span data-ttu-id="b68f1-176">O sobrenome do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-177">companyName</span><span class="sxs-lookup"><span data-stu-id="b68f1-177">companyName</span></span>|<span data-ttu-id="b68f1-178">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-178">string</span></span>|<span data-ttu-id="b68f1-179">O nome da empresa do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="b68f1-180">addresserEmail</span></span>|<span data-ttu-id="b68f1-181">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-181">string</span></span>|<span data-ttu-id="b68f1-182">Endereço de email do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="b68f1-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="b68f1-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="b68f1-184">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-184">string</span></span>|<span data-ttu-id="b68f1-185">URL relativa para exibir a análise para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="b68f1-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="b68f1-186">subscriptions</span></span>|<span data-ttu-id="b68f1-187">Coleção de entidades de [Assinatura](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="b68f1-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="b68f1-188">As assinaturas da usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="b68f1-189">de dimensionamento da Web</span><span class="sxs-lookup"><span data-stu-id="b68f1-189">applications</span></span>|<span data-ttu-id="b68f1-190">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="b68f1-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="b68f1-191">Os aplicativos do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="b68f1-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="b68f1-192">changePasswordUrl</span></span>|<span data-ttu-id="b68f1-193">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-193">string</span></span>|<span data-ttu-id="b68f1-194">A URL relativa para alterar a senha do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="b68f1-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="b68f1-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="b68f1-196">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-196">string</span></span>|<span data-ttu-id="b68f1-197">A URL relativa para alterar o nome e o email para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="b68f1-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="b68f1-198">canChangePassword</span></span>|<span data-ttu-id="b68f1-199">booleano</span><span class="sxs-lookup"><span data-stu-id="b68f1-199">boolean</span></span>|<span data-ttu-id="b68f1-200">Se o usuário atual pode alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="b68f1-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="b68f1-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="b68f1-201">isSystemUser</span></span>|<span data-ttu-id="b68f1-202">booleano</span><span class="sxs-lookup"><span data-stu-id="b68f1-202">boolean</span></span>|<span data-ttu-id="b68f1-203">Se o usuário atual é membro de um dos [grupos](api-management-key-concepts.md#groups) internos.</span><span class="sxs-lookup"><span data-stu-id="b68f1-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b68f1-204">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="b68f1-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="b68f1-205"><a name="Applications"></a> Aplicativos</span><span class="sxs-lookup"><span data-stu-id="b68f1-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="b68f1-206">O modelo **Aplicativos** permite que você personalize a seção de aplicativos da página de perfil do usuário no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b68f1-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b68f1-207">![Página Aplicativos da conta de usuário](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Página Aplicativos da conta de usuário de APIM")</span><span class="sxs-lookup"><span data-stu-id="b68f1-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b68f1-208">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="b68f1-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="b68f1-209">Controles</span><span class="sxs-lookup"><span data-stu-id="b68f1-209">Controls</span></span>  
 <span data-ttu-id="b68f1-210">Este modelo pode usar os seguintes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="b68f1-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b68f1-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="b68f1-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="b68f1-212">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="b68f1-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b68f1-213">Os modelos [Perfil](#Profile), [Aplicativos](#Applications) e [Assinaturas](#Subscriptions) compartilham o mesmo modelo de dados e recebem os mesmos dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="b68f1-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="b68f1-214">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b68f1-214">Property</span></span>|<span data-ttu-id="b68f1-215">Tipo</span><span class="sxs-lookup"><span data-stu-id="b68f1-215">Type</span></span>|<span data-ttu-id="b68f1-216">Descrição</span><span class="sxs-lookup"><span data-stu-id="b68f1-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b68f1-217">firstName</span><span class="sxs-lookup"><span data-stu-id="b68f1-217">firstName</span></span>|<span data-ttu-id="b68f1-218">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-218">string</span></span>|<span data-ttu-id="b68f1-219">O primeiro nome do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-219">First name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-220">lastName</span><span class="sxs-lookup"><span data-stu-id="b68f1-220">lastName</span></span>|<span data-ttu-id="b68f1-221">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-221">string</span></span>|<span data-ttu-id="b68f1-222">O sobrenome do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-223">companyName</span><span class="sxs-lookup"><span data-stu-id="b68f1-223">companyName</span></span>|<span data-ttu-id="b68f1-224">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-224">string</span></span>|<span data-ttu-id="b68f1-225">O nome da empresa do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="b68f1-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="b68f1-226">addresserEmail</span></span>|<span data-ttu-id="b68f1-227">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-227">string</span></span>|<span data-ttu-id="b68f1-228">Endereço de email do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="b68f1-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="b68f1-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="b68f1-230">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-230">string</span></span>|<span data-ttu-id="b68f1-231">URL relativa para exibir a análise para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="b68f1-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="b68f1-232">subscriptions</span></span>|<span data-ttu-id="b68f1-233">Coleção de entidades de [Assinatura](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="b68f1-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="b68f1-234">As assinaturas da usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="b68f1-235">de dimensionamento da Web</span><span class="sxs-lookup"><span data-stu-id="b68f1-235">applications</span></span>|<span data-ttu-id="b68f1-236">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="b68f1-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="b68f1-237">Os aplicativos do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="b68f1-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="b68f1-238">changePasswordUrl</span></span>|<span data-ttu-id="b68f1-239">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-239">string</span></span>|<span data-ttu-id="b68f1-240">A URL relativa para alterar a senha do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="b68f1-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="b68f1-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="b68f1-242">string</span><span class="sxs-lookup"><span data-stu-id="b68f1-242">string</span></span>|<span data-ttu-id="b68f1-243">A URL relativa para alterar o nome e o email para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="b68f1-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="b68f1-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="b68f1-244">canChangePassword</span></span>|<span data-ttu-id="b68f1-245">booleano</span><span class="sxs-lookup"><span data-stu-id="b68f1-245">boolean</span></span>|<span data-ttu-id="b68f1-246">Se o usuário atual pode alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="b68f1-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="b68f1-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="b68f1-247">isSystemUser</span></span>|<span data-ttu-id="b68f1-248">booleano</span><span class="sxs-lookup"><span data-stu-id="b68f1-248">boolean</span></span>|<span data-ttu-id="b68f1-249">Se o usuário atual é membro de um dos [grupos](api-management-key-concepts.md#groups) internos.</span><span class="sxs-lookup"><span data-stu-id="b68f1-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b68f1-250">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="b68f1-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="b68f1-251"><a name="UpdateAccountInfo"></a> Atualizar informações da conta</span><span class="sxs-lookup"><span data-stu-id="b68f1-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="b68f1-252">O modelo **Atualizar informações da conta** permite que você personalize a página **Atualizar informações da conta** no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="b68f1-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="b68f1-253">![Modelos do portal do desenvolvedor da página de informações conta de usuário](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor da página de informações conta de usuário do APIM")</span><span class="sxs-lookup"><span data-stu-id="b68f1-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b68f1-254">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="b68f1-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="b68f1-255">Controles</span><span class="sxs-lookup"><span data-stu-id="b68f1-255">Controls</span></span>  
 <span data-ttu-id="b68f1-256">Este modelo pode não usar nenhum [controle de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="b68f1-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="b68f1-257">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="b68f1-257">Data model</span></span>  
 <span data-ttu-id="b68f1-258">Entidade [Informações de conta de usuário](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="b68f1-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="b68f1-259">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="b68f1-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="b68f1-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b68f1-260">Next steps</span></span>
<span data-ttu-id="b68f1-261">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b68f1-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>