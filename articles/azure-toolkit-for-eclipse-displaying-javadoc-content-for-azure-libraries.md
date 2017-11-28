---
title: "aaaDisplaying conteúdo do Javadoc no Eclipse para Olá pacote de bibliotecas do Azure para Java"
description: "Como toodisplay hello conteúdo do Javadoc para bibliotecas do Azure Olá no Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="bb931-103">Exibindo o conteúdo do Javadoc no Eclipse para Olá pacote de bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="bb931-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="bb931-104">Olá conteúdo do Javadoc para Olá bibliotecas do Azure para Java pode ser exibido em seu ambiente do Eclipse associando toohello conteúdo do Javadoc de saudação bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="bb931-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="bb931-105">Olá etapas a seguir mostram como toouse essa funcionalidade no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bb931-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="bb931-106">Este procedimento pressupõe que você já adicionou hello Azure da biblioteca para o caminho de compilação Java tooyour.</span><span class="sxs-lookup"><span data-stu-id="bb931-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="bb931-107">toodisplay conteúdo do Javadoc no Eclipse para Olá bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="bb931-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="bb931-108">No Explorador de projeto do Eclipse, no hello **bibliotecas referenciadas** seção do projeto, no menu de contexto de saudação aberto para Olá biblioteca do Azure para Java JAR.</span><span class="sxs-lookup"><span data-stu-id="bb931-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="bb931-109">Por exemplo, **windowsazure microsoft-0.1.0.jar api** (número de versão de hello pode ser diferente, depende de qual versão você instalou).</span><span class="sxs-lookup"><span data-stu-id="bb931-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="bb931-110">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="bb931-110">Click **Properties**.</span></span>

* <span data-ttu-id="bb931-111">Dentro de saudação **propriedades** caixa de diálogo, no painel esquerdo do hello, clique em **local do Javadoc**.</span><span class="sxs-lookup"><span data-stu-id="bb931-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="bb931-112">Olá **local do Javadoc** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="bb931-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="bb931-113">Você pode especificar uma **URL Javadoc**, ou um **Javadoc no arquivo**.</span><span class="sxs-lookup"><span data-stu-id="bb931-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="bb931-114">Se você escolher toospecify um **URL do Javadoc**, use Olá URLs como **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="bb931-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="bb931-115">Se você escolher toouse **Javadoc no arquivo**, você pode especificar um arquivo externo ou um arquivo de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bb931-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="bb931-116">Faça sua escolha e procure/valide conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="bb931-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="bb931-117">Olá exemplo a seguir associa Olá bibliotecas do Azure para Java Olá Javadoc JAR correspondente que foi baixado localmente tooa pasta denominada **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="bb931-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="bb931-118">*Etapa Opcional*: clique em **Validar**.</span><span class="sxs-lookup"><span data-stu-id="bb931-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="bb931-119">Problemas potenciais com hello Javadoc JAR podem ser exibidos aqui.</span><span class="sxs-lookup"><span data-stu-id="bb931-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="bb931-120">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb931-120">Click **OK**.</span></span>

<span data-ttu-id="bb931-121">Uma vez associado biblioteca hello, Olá conteúdo do Javadoc deve exibir seu IDE do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bb931-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="bb931-122">Por exemplo, se `blob` é definido como o tipo `CloudBlockBlob` dentro de seu código, a seguinte Olá é um exemplo de conteúdo do Javadoc que aparece quando você digita `blob.acquireLease` no código:</span><span class="sxs-lookup"><span data-stu-id="bb931-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="bb931-123">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bb931-123">See Also</span></span>
<span data-ttu-id="bb931-124">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bb931-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="bb931-125">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bb931-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="bb931-126">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bb931-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="bb931-127">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="bb931-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
