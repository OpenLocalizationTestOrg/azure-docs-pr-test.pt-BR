---
title: Requisitos de aplicativo para o Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre os requisitos para aplicativos que você deseja usar no RemoteApp do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a><span data-ttu-id="5c4bf-103">Requisitos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c4bf-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5c4bf-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5c4bf-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5c4bf-106">O RemoteApp do Azure dá suporte a streaming de aplicativos baseados em Windows 32 bits ou 64 bits de uma imagem do Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="5c4bf-107">A maioria dos aplicativos baseados em Windows de 32 bits ou 64 bits é executada "como está" no ambiente RemoteApp do Azure (Serviços de Área de Trabalho Remota, anteriormente conhecido como Serviços de Terminal).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="5c4bf-108">No entanto, há uma diferença entre executar e executar bem – alguns aplicativos funcionam corretamente e executam bem, enquanto outros, não.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="5c4bf-109">As informações a seguir fornecem diretrizes para o desenvolvimento de aplicativos em um ambiente de Serviços de Área de Trabalho Remota e os testes para garantir a compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="5c4bf-110">Dica: estamos trabalhando na criação de alguns exemplos práticos dos aplicativos para você.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="5c4bf-111">Você verá os novos tópicos que abordam o uso do Microsoft Access, do QuickBooks e do App-V no RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="5c4bf-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="5c4bf-112">Requirements</span></span>
<span data-ttu-id="5c4bf-113">Esses três requisitos, se seguidos, ajudam o aplicativo a ser executado corretamente no RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="5c4bf-114">Aplicativos que atenderem a todos os [Requisitos de certificação para aplicativos de área de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) e cumprirem as [Diretrizes de programação dos Serviços de Área de Trabalho Remota](https://msdn.microsoft.com/library/aa383490.aspx) terão total compatibilidade com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="5c4bf-115">Os aplicativos nunca devem armazenar dados localmente na imagem ou em instâncias do RemoteApp que possam ser perdidas.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="5c4bf-116">Depois de criar uma coleção do RemoteApp, as instâncias são clonadas e sem monitoração de estado, devendo conter apenas aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="5c4bf-117">Armazenar dados em uma fonte externa ou no perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="5c4bf-118">Imagens personalizadas nunca devem conter dados que possam ser perdidos.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="5c4bf-119">Testando seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="5c4bf-119">Testing your apps</span></span>
<span data-ttu-id="5c4bf-120">Siga estas etapas para testar aplicativos:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="5c4bf-121">Instale o Windows Server 2012 R2 e o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c4bf-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="5c4bf-122">Habilite a Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="5c4bf-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="5c4bf-123">Crie duas contas de usuário, UserA e UserB, adicionando ambas ao grupo de segurança da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="5c4bf-124">Verifique a compatibilidade multissessões estabelecendo duas sessões RDS simultâneas para o PC durante a inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="5c4bf-125">Validar o comportamento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c4bf-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="5c4bf-126">Diretrizes para desenvolvimento de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5c4bf-126">Application development guidelines</span></span>
<span data-ttu-id="5c4bf-127">Siga as diretrizes apresentadas para desenvolver aplicativos para o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="5c4bf-128">Vários usuários</span><span class="sxs-lookup"><span data-stu-id="5c4bf-128">Multiple users</span></span>
* <span data-ttu-id="5c4bf-129">Instalar um [aplicativo para um único usuário ](https://msdn.microsoft.com/library/aa380661.aspx)pode criar problemas em um ambiente multiusuário.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="5c4bf-130">Aplicativos devem [armazenar informações específicas do usuário](https://msdn.microsoft.com/library/aa383452.aspx) em locais específicos do usuário, separadamente de informações globais que se aplicam a todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="5c4bf-131">O RemoteApp usa vários [namespaces para objetos kernel](https://msdn.microsoft.com/library/aa382954.aspx); um namespace global é usado principalmente por serviços de aplicativos cliente/servidor.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="5c4bf-132">Não é seguro pressupor que o nome do computador ou o [endereço IP](https://msdn.microsoft.com/library/aa382942.aspx) atribuído ao computador está associados um único usuário, pois vários usuários podem ser conectados simultaneamente a um servidor de Host da Sessão da Área de Trabalho Remota (Host da Sessão RD).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="5c4bf-133">Desempenho</span><span class="sxs-lookup"><span data-stu-id="5c4bf-133">Performance</span></span>
* <span data-ttu-id="5c4bf-134">Desabilite [efeitos gráficos](https://msdn.microsoft.com/library/aa380822.aspx) antes de adicionar seu aplicativo para o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="5c4bf-135">Para maximizar a disponibilidade de CPU para todos os usuários, desabilite [tarefas em segundo plano ](https://msdn.microsoft.com/library/aa380665.aspx) ou crie tarefas em segundo plano eficientes que não façam uso intenso de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="5c4bf-136">Você deve ajustar e balancear o [uso de thread](https://msdn.microsoft.com/library/aa383520.aspx) do aplicativo para um ambiente multiusuário com vários processadores.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="5c4bf-137">Para otimizar o desempenho, é recomendável que os aplicativos [detectem](https://msdn.microsoft.com/library/aa380798.aspx) se estão sendo executados em uma sessão de cliente.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

