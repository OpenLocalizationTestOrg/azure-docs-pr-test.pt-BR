---
title: "Habilitar a Afinidade de Sessão usando o Kit de Ferramentas do Azure para o Eclipse"
description: "Saiba como habilitar a afinidade de sessão usando o Kit de Ferramentas do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="221ca-103">Habilitar a afinidade de sessão</span><span class="sxs-lookup"><span data-stu-id="221ca-103">Enable Session Affinity</span></span>
<span data-ttu-id="221ca-104">No Kit de Ferramentas do Azure para o Eclipse, é possível habilitar a afinidade de sessão HTTP, ou “sessões adesivas”, para suas funções.</span><span class="sxs-lookup"><span data-stu-id="221ca-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="221ca-105">A seguinte imagem mostra o diálogo de propriedades **Balanceamento de Carga** usado para habilitar o recurso de afinidade de sessão:</span><span class="sxs-lookup"><span data-stu-id="221ca-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="221ca-106">Para habilitar a afinidade de sessão para sua função</span><span class="sxs-lookup"><span data-stu-id="221ca-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="221ca-107">Clique com o botão direito do mouse na função no Explorador de Projetos do Eclipse, clique em **Azure** e em **Balanceamento de Carga**.</span><span class="sxs-lookup"><span data-stu-id="221ca-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="221ca-108">No diálogo **Propriedades de balanceamento de carga de WorkerRole1** :</span><span class="sxs-lookup"><span data-stu-id="221ca-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="221ca-109">a.</span><span class="sxs-lookup"><span data-stu-id="221ca-109">a.</span></span> <span data-ttu-id="221ca-110">Verifique **Habilitar a afinidade de sessão HTTP (sessões autoadesivas) para esta função.**</span><span class="sxs-lookup"><span data-stu-id="221ca-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="221ca-111">b.</span><span class="sxs-lookup"><span data-stu-id="221ca-111">b.</span></span> <span data-ttu-id="221ca-112">Para **Ponto de extremidade de entrada a ser usado**, selecione um ponto de extremidade de entrada a ser usado, por exemplo, **http (pública: 80, privada: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="221ca-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="221ca-113">Seu aplicativo deve usar esse ponto de extremidade como seu ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="221ca-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="221ca-114">Você pode habilitar vários pontos de extremidade para a sua função, mas selecionar apenas um para dar suporte às sessões adesivas.</span><span class="sxs-lookup"><span data-stu-id="221ca-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="221ca-115">c.</span><span class="sxs-lookup"><span data-stu-id="221ca-115">c.</span></span> <span data-ttu-id="221ca-116">Recompile seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="221ca-116">Rebuild your application.</span></span>

<span data-ttu-id="221ca-117">Quando habilitadas, se você tiver mais de uma instância de função, as solicitações HTTP provenientes de um determinado cliente continuarão sendo manipuladas pela mesma instância de função.</span><span class="sxs-lookup"><span data-stu-id="221ca-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="221ca-118">O Kit de Ferramentas para o Eclipse permite isso instalando um módulo IIS especial chamado ARR (Roteamento de Solicitação do Aplicativo) em cada uma de suas instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="221ca-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="221ca-119">O ARR redireciona as solicitações HTTP para a instância de função apropriada.</span><span class="sxs-lookup"><span data-stu-id="221ca-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="221ca-120">O kit de ferramentas reconfigura automaticamente o ponto de extremidade selecionado para que o tráfego HTTP de entrada seja primeiramente roteado para o software ARR.</span><span class="sxs-lookup"><span data-stu-id="221ca-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="221ca-121">O Kit de Ferramentas também cria um novo ponto de extremidade interno que o servidor Java está configurado para escutar.</span><span class="sxs-lookup"><span data-stu-id="221ca-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="221ca-122">Esse é o ponto de extremidade usado pelo ARR para redirecionar o tráfego HTTP para a instância de função apropriada.</span><span class="sxs-lookup"><span data-stu-id="221ca-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="221ca-123">Dessa forma, cada instância de função em sua implantação de várias instâncias serve como um proxy reverso para todas as outras instâncias, habilitando as sessões adesivas.</span><span class="sxs-lookup"><span data-stu-id="221ca-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="221ca-124">Observações sobre a afinidade de sessão</span><span class="sxs-lookup"><span data-stu-id="221ca-124">Notes about session affinity</span></span>
* <span data-ttu-id="221ca-125">A afinidade de sessão não funciona no emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="221ca-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="221ca-126">As configurações podem ser aplicadas no emulador de computação sem interferir no processo de compilação ou na execução do emulador de computação, mas o recurso em si não funciona no emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="221ca-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="221ca-127">Habilitar a afinidade de sessão resultará em um aumento na quantidade de espaço em disco ocupada pela sua implantação no Azure, já que um software adicional será baixado e instalado em suas instâncias de função quando o serviço for iniciado na nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="221ca-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="221ca-128">O tempo para inicializar cada função levará mais tempo.</span><span class="sxs-lookup"><span data-stu-id="221ca-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="221ca-129">Um ponto de extremidade interno, para funcionar como um novo roteador de tráfego, como mencionado acima, será adicionado.</span><span class="sxs-lookup"><span data-stu-id="221ca-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="221ca-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="221ca-130">See Also</span></span>
<span data-ttu-id="221ca-131">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="221ca-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="221ca-132">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="221ca-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="221ca-133">[Instalar o Kit de Ferramentas do Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="221ca-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="221ca-134">Para saber mais sobre como usar o Azure com o Java, confira o [Centro de Desenvolvedores Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="221ca-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
