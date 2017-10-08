---
title: aaaWeb clonagem de aplicativo usando o Portal do Azure
description: Saiba como tooclone toonew seus aplicativos Web aplicativos Web usando o Portal do Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="3680e-103">Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3680e-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="3680e-104">Olá clonagem recurso no [aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) permite que você facilmente clonar o aplicativo web existente aplicativos tooa recentemente criado em uma região diferente ou em Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="3680e-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="3680e-105">Isso permitirá que os clientes toodeploy um número de aplicativos em regiões diferentes rapidamente e facilmente.</span><span class="sxs-lookup"><span data-stu-id="3680e-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="3680e-106">A clonagem de aplicativo atualmente só tem suporte para planos de serviço de aplicativos de camada Premium.</span><span class="sxs-lookup"><span data-stu-id="3680e-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="3680e-107">novos usos de recurso Olá Olá mesmo limitações de recurso de Backup de aplicativos da Web, consulte [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="3680e-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="3680e-108">Clonagem de um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="3680e-108">Cloning an existing App</span></span>
<span data-ttu-id="3680e-109">Olá web aplicativo deve estar em execução Olá **Premium** modo para que você toocreate um clone do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="3680e-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="3680e-110">Em Olá [Portal do Azure](https://portal.azure.com/), abra a folha do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="3680e-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="3680e-111">Clique em **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="3680e-111">Click **Tools**.</span></span> <span data-ttu-id="3680e-112">Em seguida, no hello **ferramentas** folha, clique em **aplicativo Clone**.</span><span class="sxs-lookup"><span data-stu-id="3680e-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="3680e-113">Se Olá web app não estiver no hello **Premium** modo, você receberá uma mensagem indicando modos Olá tem suportada para clonagem de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3680e-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="3680e-114">Neste ponto, você tem Olá opção tooselect **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="3680e-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="3680e-115">Em Olá **aplicativo Clone** folha forneça um nome do novo aplicativo de web hello, o grupo de recursos e o plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3680e-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="3680e-116">Também Olá usuário será capaz de toochoose se tooclone um número de configurações do aplicativo de web de origem ou não.</span><span class="sxs-lookup"><span data-stu-id="3680e-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="3680e-117">Depois de clicar em **criar** plataforma Olá começará a funcionar sobre como criar um clone do aplicativo de web de origem hello.</span><span class="sxs-lookup"><span data-stu-id="3680e-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="3680e-118">Clonagem de um tooan de aplicativo ambiente de serviço de aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="3680e-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="3680e-119">Em Olá **aplicativo Clone** cliente de saudação de folha terá Olá opção toochoose um pool de aplicativos em um ambiente de serviço de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="3680e-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="3680e-120">Restrições atuais</span><span class="sxs-lookup"><span data-stu-id="3680e-120">Current Restrictions</span></span>
<span data-ttu-id="3680e-121">Este recurso está atualmente em visualização, estamos trabalhando tooadd novos recursos ao longo do tempo, Olá lista a seguir são Olá restrições conhecidas na suporte atual Olá de clonagem de aplicativo no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="3680e-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="3680e-122">As configurações do Gerenciador de Tráfego do Azure não são clonadas</span><span class="sxs-lookup"><span data-stu-id="3680e-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="3680e-123">As configurações de escala automática não são clonadas</span><span class="sxs-lookup"><span data-stu-id="3680e-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="3680e-124">As configurações de agendamento de backup não são clonadas.</span><span class="sxs-lookup"><span data-stu-id="3680e-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="3680e-125">As configurações da rede virtual não são clonadas</span><span class="sxs-lookup"><span data-stu-id="3680e-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="3680e-126">Ideias de aplicativo não são automaticamente definidas no aplicativo de web de destino Olá</span><span class="sxs-lookup"><span data-stu-id="3680e-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="3680e-127">As configurações de Autenticação Fácil não são clonadas</span><span class="sxs-lookup"><span data-stu-id="3680e-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="3680e-128">A extensão Kudu não é clonada</span><span class="sxs-lookup"><span data-stu-id="3680e-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="3680e-129">As regras de TiP não são clonadas</span><span class="sxs-lookup"><span data-stu-id="3680e-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="3680e-130">O conteúdo do banco de dados não é clonado</span><span class="sxs-lookup"><span data-stu-id="3680e-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="3680e-131">Referências</span><span class="sxs-lookup"><span data-stu-id="3680e-131">References</span></span>
* [<span data-ttu-id="3680e-132">Clonagem de Aplicativo Web usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3680e-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="3680e-133">Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="3680e-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="3680e-134">Como tooCreate um ambiente de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="3680e-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="3680e-135">Criar um aplicativo Web em um Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="3680e-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="3680e-136">Introdução tooApp ambiente de serviço</span><span class="sxs-lookup"><span data-stu-id="3680e-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
