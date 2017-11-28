---
title: "Introdução à Área de Trabalho do Windows no Azure AD v2 – Configuração | Microsoft Docs"
description: "Como um aplicativo .NET da Área de Trabalho do Windows (XAML) pode obter um token de acesso e chamar uma API protegida pelo ponto de extremidade do Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 1dfaa7ade664e43dcb9aa788b0197ca17e6ec4cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="ef3eb-104">Criar um aplicativo (Expresso)</span><span class="sxs-lookup"><span data-stu-id="ef3eb-104">Create an application (Express)</span></span>
<span data-ttu-id="ef3eb-105">Agora você precisa registrar seu aplicativo no *Portal de Registro de Aplicativos da Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ef3eb-105">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ef3eb-106">Registre o aplicativo por meio do [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="ef3eb-106">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="ef3eb-107">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="ef3eb-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="ef3eb-108">Verifique se a opção Instalação Guiada está marcada</span><span class="sxs-lookup"><span data-stu-id="ef3eb-108">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="ef3eb-109">Siga as instruções para obter a ID do aplicativo e colá-lo no código</span><span class="sxs-lookup"><span data-stu-id="ef3eb-109">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="ef3eb-110">Adicionar as informações de registro do aplicativo à sua solução (Avançado)</span><span class="sxs-lookup"><span data-stu-id="ef3eb-110">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="ef3eb-111">Agora você precisa registrar seu aplicativo no *Portal de Registro de Aplicativos da Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ef3eb-111">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ef3eb-112">Acesse o [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/portal/register-app) para registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="ef3eb-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="ef3eb-113">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="ef3eb-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="ef3eb-114">Verifique se a opção Instalação Guiada está desmarcada</span><span class="sxs-lookup"><span data-stu-id="ef3eb-114">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="ef3eb-115">Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="ef3eb-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="ef3eb-116">Copie o GUID da ID do Aplicativo, volte ao Visual Studio, abra `App.xaml.cs` e substitua `your_client_id_here` pela ID do Aplicativo que você acabou de registrar:</span><span class="sxs-lookup"><span data-stu-id="ef3eb-116">Copy the GUID in Application ID, go back to Visual Studio, open `App.xaml.cs` and replace `your_client_id_here` with the Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
