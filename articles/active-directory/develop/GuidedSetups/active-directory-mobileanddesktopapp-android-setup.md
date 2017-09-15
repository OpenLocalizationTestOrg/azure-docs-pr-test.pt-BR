---
title: "Introdução ao Android no Azure AD v2 – Instalação | Microsoft Docs"
description: Como um aplicativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2
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
ms.openlocfilehash: a43d7e30a6f4176afba27f0de2c2c116df741080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="7a656-103">Configurar o seu projeto</span><span class="sxs-lookup"><span data-stu-id="7a656-103">Set up your project</span></span>

> <span data-ttu-id="7a656-104">Prefere baixar este projeto do Android Studio de exemplo?</span><span class="sxs-lookup"><span data-stu-id="7a656-104">Prefer to download this sample's Android Studio project instead?</span></span> <span data-ttu-id="7a656-105">[Baixe um projeto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e vá para a [Etapa de configuração](#create-an-application-express) para configurar o exemplo de código antes de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="7a656-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="7a656-106">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="7a656-106">Create a new project</span></span> 
1.  <span data-ttu-id="7a656-107">Abra o Android Studio e acesse: `File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="7a656-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="7a656-108">Nomeie o aplicativo e clique em `Next`</span><span class="sxs-lookup"><span data-stu-id="7a656-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="7a656-109">Lembre-se de selecionar *API 21 ou mais nova (Android 5.0)* e clique em `Next`</span><span class="sxs-lookup"><span data-stu-id="7a656-109">Make sure to select *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="7a656-110">Mantenha `Empty Activity`, clique em `Next` e, em seguida, em `Finish`</span><span class="sxs-lookup"><span data-stu-id="7a656-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="7a656-111">Adicionar a MSAL (Biblioteca de Autenticação da Microsoft) ao projeto</span><span class="sxs-lookup"><span data-stu-id="7a656-111">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1.  <span data-ttu-id="7a656-112">No Android Studio, acesse: `Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="7a656-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="7a656-113">Copie e cole o seguinte código em `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="7a656-113">Copy and paste the following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="7a656-114">Sobre este pacote</span><span class="sxs-lookup"><span data-stu-id="7a656-114">About this package</span></span>

<span data-ttu-id="7a656-115">O pacote acima instala a MSAL (Biblioteca de Autenticação da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="7a656-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="7a656-116">A MSAL manipula a aquisição, o armazenamento em cache e a atualização de tokens de usuário usados para acessar APIs protegidas pelo ponto de extremidade do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="7a656-116">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="7a656-117">Criar a interface do usuário do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7a656-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="7a656-118">Abra `activity_main.xml` em `res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="7a656-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="7a656-119">Altere o layout de atividade de `android.support.constraint.ConstraintLayout` ou outro para `LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="7a656-119">Change the activity layout from `android.support.constraint.ConstraintLayout` or other to `LinearLayout`</span></span>
3.  <span data-ttu-id="7a656-120">Adicione a propriedade `android:orientation="vertical"` ao nó `LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="7a656-120">Add `android:orientation="vertical"` property to `LinearLayout` node</span></span>
4.  <span data-ttu-id="7a656-121">Copie e cole o seguinte código no nó `LinearLayout`, substituindo o conteúdo atual:</span><span class="sxs-lookup"><span data-stu-id="7a656-121">Copy and paste the following code into the `LinearLayout` node, replacing the current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

