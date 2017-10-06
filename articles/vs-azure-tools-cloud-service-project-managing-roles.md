---
title: "serviços com o Visual Studio em nuvem aaaManaging funções no Azure | Microsoft Docs"
description: "Saiba como tooadd e remover funções no Azure cloud services com o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="8d18a-103">Gerenciando funções nos serviços de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d18a-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="8d18a-104">Depois que você criou seu serviço de nuvem do Azure, você pode adicionar novos tooit de funções ou remova funções existentes ele.</span><span class="sxs-lookup"><span data-stu-id="8d18a-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="8d18a-105">Você também pode importar um projeto existente e convertê-la tooa função.</span><span class="sxs-lookup"><span data-stu-id="8d18a-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="8d18a-106">Por exemplo, você pode importar um aplicativo Web ASP.NET e designá-lo como uma função web.</span><span class="sxs-lookup"><span data-stu-id="8d18a-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="8d18a-107">Adicionando um tooan de função serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="8d18a-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="8d18a-108">Olá etapas a seguir orientam você na adição de um web ou trabalho função tooan nuvem do Azure serviço projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d18a-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8d18a-109">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d18a-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8d18a-110">Em **Solution Explorer**, expanda o nó do projeto Olá</span><span class="sxs-lookup"><span data-stu-id="8d18a-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="8d18a-111">Saudação de atalho **funções** menu de contexto do nó toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="8d18a-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="8d18a-112">No menu de contexto hello, selecione **adicionar**, em seguida, selecione uma função web existente ou uma função de trabalho na solução atual Olá ou criar um projeto de função web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d18a-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="8d18a-113">Também é possível selecionar um projeto apropriado, como um projeto de aplicativo Web ASP.NET e associá-lo a um projeto de função.</span><span class="sxs-lookup"><span data-stu-id="8d18a-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Menu Opções tooadd um projeto de serviço de nuvem do Azure de tooan de função](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="8d18a-115">Removendo uma função de um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="8d18a-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="8d18a-116">Olá etapas a seguir orientam você na remoção de uma função web ou de trabalho de um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d18a-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8d18a-117">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d18a-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8d18a-118">Em **Solution Explorer**, expanda o nó do projeto Olá</span><span class="sxs-lookup"><span data-stu-id="8d18a-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="8d18a-119">Expanda Olá **funções** nó.</span><span class="sxs-lookup"><span data-stu-id="8d18a-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="8d18a-120">Nó de Olá atalho deseja tooremove e, no menu de contexto hello, selecione **remover**.</span><span class="sxs-lookup"><span data-stu-id="8d18a-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Menu Opções tooadd um tooan de função serviço de nuvem do Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="8d18a-122">Lendo um projeto de serviço de nuvem do Azure de tooan de função</span><span class="sxs-lookup"><span data-stu-id="8d18a-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="8d18a-123">Se você remove uma função de seu projeto de serviço de nuvem, mas decide posteriormente função volta do tooadd Olá toohello projeto, somente a declaração de função hello e os atributos básicos, como pontos de extremidade e informações de diagnóstico, são adicionados.</span><span class="sxs-lookup"><span data-stu-id="8d18a-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="8d18a-124">Não há recursos adicionais ou referências são adicionadas toohello `ServiceDefinition.csdef` arquivo ou toohello `ServiceConfiguration.cscfg` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8d18a-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="8d18a-125">Se você quiser tooadd essas informações, você precisa toomanually adicioná-lo de volta para esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="8d18a-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="8d18a-126">Por exemplo, você pode remover uma função de serviço web e posteriormente decidir tooadd fazer essa função em sua solução.</span><span class="sxs-lookup"><span data-stu-id="8d18a-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="8d18a-127">Se você fizer isso, ocorrerá um erro.</span><span class="sxs-lookup"><span data-stu-id="8d18a-127">If you do this, an error occurs.</span></span> <span data-ttu-id="8d18a-128">tooprevent esse erro, ter Olá tooadd `<LocalResources>` elemento mostrado Olá seguir XML novamente no hello `ServiceDefinition.csdef` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8d18a-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="8d18a-129">Use o nome de função de serviço web de saudação que você adicionou no project hello como parte do atributo name Olá Olá Olá  **<LocalStorage>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="8d18a-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="8d18a-130">Neste exemplo, o nome de saudação da função de serviço da web hello é **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="8d18a-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="8d18a-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d18a-131">Next steps</span></span>
- [<span data-ttu-id="8d18a-132">Configurar as funções de saudação para um serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d18a-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
