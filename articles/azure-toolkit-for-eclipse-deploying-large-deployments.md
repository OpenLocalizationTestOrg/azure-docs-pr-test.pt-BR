---
title: "aaaDeploying grandes implantações"
description: "Saiba como toodeploy grandes implantações usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="d376a-103">Implantando Grandes Implantações</span><span class="sxs-lookup"><span data-stu-id="d376a-103">Deploying Large Deployments</span></span>
<span data-ttu-id="d376a-104">Se sua implantação for muito grande toobe contida na pasta de approot saudação padrão, você pode usar um recurso de armazenamento local como a pasta raiz de implantação das Olá para o seu JDK e servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d376a-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="d376a-105">um recurso de armazenamento local como pasta Olá de raiz de implantação para grandes implantações de toouse</span><span class="sxs-lookup"><span data-stu-id="d376a-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="d376a-106">Crie um recurso de armazenamento local novo.</span><span class="sxs-lookup"><span data-stu-id="d376a-106">Create a new local storage resource.</span></span> <span data-ttu-id="d376a-107">nome de saudação do recurso de saudação não importa.</span><span class="sxs-lookup"><span data-stu-id="d376a-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="d376a-108">Recursos de armazenamento são definidos no nível de função hello.</span><span class="sxs-lookup"><span data-stu-id="d376a-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="d376a-109">Hello mais rápida maneira tooaccess Olá armazenamento local configuração caixa de diálogo, na qual você pode criar um novo recurso de armazenamento local, é usando Olá etapas a seguir: função de saudação com o botão direito no hello **Explorador de projeto** exibição (expandir seu Nó do projeto Azure se você não vir a função hello), clique em **Azure**e, em seguida, clique em **armazenamento Local**.</span><span class="sxs-lookup"><span data-stu-id="d376a-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="d376a-110">Dentro de saudação **armazenamento Local** caixa de diálogo, clique em **adicionar** toocreate um novo recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="d376a-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="d376a-111">Olá conjunto desejado tooat de tamanho mínimo 2048 MB (nada menor pode causar Olá mesmos problemas de tamanho de arquivo como haveria na approot Olá).</span><span class="sxs-lookup"><span data-stu-id="d376a-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="d376a-112">Certifique-se de que **Limpar conteúdo hello quando Olá instância de função é reciclada** é verificada; isso ajuda a impedir que Olá lógica de inicialização seja executada em conflitos com os arquivos pré-existentes no recurso Olá Olá quando a função instância é reciclada.</span><span class="sxs-lookup"><span data-stu-id="d376a-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="d376a-113">Certifique-se de que Olá **armazenar variável do ambiente Olá o caminho do diretório do recurso após a implantação** valor é definido de cadeia de caracteres toohello **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="d376a-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="d376a-114">A caixa de diálogo do recurso de armazenamento local será a aparência a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="d376a-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="d376a-115">Como alternativa, se você usar **DEPLOYROOT** como Olá *nome* de seus recursos locais e você não alterar o nome de variável de ambiente gerada automaticamente hello (que será definido muito **DEPLOYROOT_PATH** nesse caso), isso funcionaria para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d376a-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="d376a-116">Informações adicionais sobre como criar um recurso de armazenamento local podem ser encontradas em [Propriedades de armazenamento local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="d376a-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="d376a-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d376a-117">See Also</span></span>
<span data-ttu-id="d376a-118">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d376a-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="d376a-119">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d376a-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="d376a-120">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d376a-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="d376a-121">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="d376a-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
