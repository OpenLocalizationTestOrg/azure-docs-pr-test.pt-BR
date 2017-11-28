---
title: "uso de afinidade de sessão aaaEnable Olá Kit de ferramentas do Azure para Eclipse"
description: "Saiba como o uso de afinidade de sessão tooenable Olá Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="6d774-103">Habilitar a afinidade de sessão</span><span class="sxs-lookup"><span data-stu-id="6d774-103">Enable Session Affinity</span></span>
<span data-ttu-id="6d774-104">Dentro de Olá Kit de ferramentas do Azure para Eclipse, você pode habilitar a afinidade de sessão HTTP ou "sessões Autoadesivas", para suas funções.</span><span class="sxs-lookup"><span data-stu-id="6d774-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="6d774-105">Olá, imagem a seguir mostra Olá **balanceamento de carga** recurso de afinidade de sessão propriedades diálogo usado tooenable hello:</span><span class="sxs-lookup"><span data-stu-id="6d774-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="6d774-106">afinidade de sessão tooenable para sua função</span><span class="sxs-lookup"><span data-stu-id="6d774-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="6d774-107">Função hello no Explorador de projeto do Eclipse, clique **Azure**e, em seguida, clique em **balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="6d774-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="6d774-108">Em Olá **propriedades de balanceamento de carga de WorkerRole1** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="6d774-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="6d774-109">a.</span><span class="sxs-lookup"><span data-stu-id="6d774-109">a.</span></span> <span data-ttu-id="6d774-110">Verifique **Habilitar a afinidade de sessão HTTP (sessões autoadesivas) para esta função.**</span><span class="sxs-lookup"><span data-stu-id="6d774-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="6d774-111">b.</span><span class="sxs-lookup"><span data-stu-id="6d774-111">b.</span></span> <span data-ttu-id="6d774-112">Para **toouse de ponto de extremidade de entrada**, selecione toouse um ponto de extremidade de entrada, por exemplo, **http (public: 80, private: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="6d774-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="6d774-113">Seu aplicativo deve usar esse ponto de extremidade como seu ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="6d774-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="6d774-114">Você pode habilitar vários pontos de extremidade para sua função, mas você pode selecionar apenas um deles toosupport sessões Autoadesivas.</span><span class="sxs-lookup"><span data-stu-id="6d774-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="6d774-115">c.</span><span class="sxs-lookup"><span data-stu-id="6d774-115">c.</span></span> <span data-ttu-id="6d774-116">Recompile seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d774-116">Rebuild your application.</span></span>

<span data-ttu-id="6d774-117">Uma vez habilitada, se você tiver mais de uma instância de função, solicitações de HTTP vindo de um determinado cliente continuarão sendo manipuladas pelo Olá mesmo instância de função.</span><span class="sxs-lookup"><span data-stu-id="6d774-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="6d774-118">Olá Kit de ferramentas do Eclipse permite isso instalando um módulo IIS especial chamado roteamento ARR (Application Request) em cada uma de suas instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="6d774-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="6d774-119">O ARR redireciona as instância de função apropriada de toohello de solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="6d774-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="6d774-120">Olá Kit de ferramentas reconfigura automaticamente o ponto de extremidade de saudação selecionado para que o tráfego HTTP de entrada hello está primeiro roteado toohello ARR software.</span><span class="sxs-lookup"><span data-stu-id="6d774-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="6d774-121">saudação de kit de ferramentas também cria um ponto de extremidade interno novo que o servidor de Java é configurado toolisten para.</span><span class="sxs-lookup"><span data-stu-id="6d774-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="6d774-122">Que é o ponto de extremidade de saudação usado pela instância de função apropriada do ARR tooreroute Olá HTTP tráfego toohello.</span><span class="sxs-lookup"><span data-stu-id="6d774-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="6d774-123">Dessa forma, cada instância de função em sua implantação de várias instâncias serve como um proxy reverso para todos os Olá outras instâncias, habilitando as sessões Autoadesivas.</span><span class="sxs-lookup"><span data-stu-id="6d774-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="6d774-124">Observações sobre a afinidade de sessão</span><span class="sxs-lookup"><span data-stu-id="6d774-124">Notes about session affinity</span></span>
* <span data-ttu-id="6d774-125">Afinidade de sessão não funciona no emulador de computação hello.</span><span class="sxs-lookup"><span data-stu-id="6d774-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="6d774-126">configurações Olá podem ser aplicadas no emulador de computação Olá sem interferir no processo de compilação ou execução do emulador de computação, mas o recurso Olá em si não funciona no emulador de computação hello.</span><span class="sxs-lookup"><span data-stu-id="6d774-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="6d774-127">Habilitar a afinidade de sessão resultará em um aumento na quantidade de saudação do espaço em disco ocupada por sua implantação no Azure, como o software adicional será baixado e instalado em suas instâncias de função quando o serviço é iniciado no hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d774-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="6d774-128">Olá tempo tooinitialize cada função levará mais tempo.</span><span class="sxs-lookup"><span data-stu-id="6d774-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="6d774-129">Ponto de extremidade interno, toofunction como um rerouter de tráfego, como mencionado acima, será adicionado.</span><span class="sxs-lookup"><span data-stu-id="6d774-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="6d774-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6d774-130">See Also</span></span>
<span data-ttu-id="6d774-131">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6d774-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="6d774-132">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6d774-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="6d774-133">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6d774-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="6d774-134">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="6d774-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
