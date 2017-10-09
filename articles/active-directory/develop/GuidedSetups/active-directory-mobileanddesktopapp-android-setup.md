---
title: "aaaAzure AD v2 Android Introdução - instalação | Microsoft Docs"
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
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="ec0fe-103">Configurar o seu projeto</span><span class="sxs-lookup"><span data-stu-id="ec0fe-103">Set up your project</span></span>

> <span data-ttu-id="ec0fe-104">Preferir toodownload Android Studio projeto desse exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="ec0fe-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="ec0fe-105">[Baixar um projeto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.</span><span class="sxs-lookup"><span data-stu-id="ec0fe-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="ec0fe-106">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="ec0fe-106">Create a new project</span></span> 
1.  <span data-ttu-id="ec0fe-107">Abra o Android Studio e acesse: `File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="ec0fe-108">Nomeie o aplicativo e clique em `Next`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="ec0fe-109">Certifique-se de que tooselect *21 de API ou mais recente (Android 5.0)* e clique em`Next`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="ec0fe-110">Mantenha `Empty Activity`, clique em `Next` e, em seguida, em `Finish`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="ec0fe-111">Adicionar projeto de tooyour Olá biblioteca de autenticação da Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="ec0fe-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="ec0fe-112">No Android Studio, acesse: `Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="ec0fe-113">Copiar e colar a seguir Olá código em `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="ec0fe-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="ec0fe-114">Sobre este pacote</span><span class="sxs-lookup"><span data-stu-id="ec0fe-114">About this package</span></span>

<span data-ttu-id="ec0fe-115">pacote de saudação acima instala Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="ec0fe-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="ec0fe-116">MSAL lida com a aquisição, cache e atualizar usuário tokens usados tooaccess APIs protegidos pelo ponto de extremidade do Active Directory do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="ec0fe-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="ec0fe-117">Criar a interface do usuário do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ec0fe-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="ec0fe-118">Abra `activity_main.xml` em `res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="ec0fe-119">Alterar o layout de atividade de saudação do `android.support.constraint.ConstraintLayout` ou outros muito`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="ec0fe-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="ec0fe-120">Adicionar `android:orientation="vertical"` propriedade muito`LinearLayout` nó</span><span class="sxs-lookup"><span data-stu-id="ec0fe-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="ec0fe-121">Copiar e colar a seguir Olá código em Olá `LinearLayout` nó, substituindo o conteúdo atual da saudação:</span><span class="sxs-lookup"><span data-stu-id="ec0fe-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

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

