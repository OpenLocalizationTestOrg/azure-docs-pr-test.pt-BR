---
title: "Sobre os Laboratórios de Desenvolvimento/Teste | Microsoft Azure"
description: "Saiba como os Laboratórios de Desenvolvimento/Teste podem facilitar criar, gerenciar e monitorar as máquinas virtuais do Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="fced1-103">Sobre os Laboratórios de Desenvolvimento/Teste do Azure</span><span class="sxs-lookup"><span data-stu-id="fced1-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="fced1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fced1-104">Overview</span></span>
<span data-ttu-id="fced1-105">Os desenvolvedores e testadores estão tentando resolver os atrasos na criação e gerenciamento de seus ambientes indo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="fced1-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="fced1-106">O Azure resolve o problema de atrasos de ambiente e permite autoatendimento dentro de uma nova estrutura com boa relação custo-benefício.</span><span class="sxs-lookup"><span data-stu-id="fced1-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="fced1-107">No entanto, os desenvolvedores e testadores ainda precisam gastar um tempo considerável configurando seus ambientes de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="fced1-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="fced1-108">Além disso, os tomadores de decisão não estão certos sobre como utilizar a nuvem para maximizar suas economias sem acrescentar muita sobrecarga de processo.</span><span class="sxs-lookup"><span data-stu-id="fced1-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="fced1-109">Os Laboratórios de Desenvolvimento/Teste do Azure são um serviço que ajuda os desenvolvedores e testadores a rapidamente criar ambientes no Azure, minimizando o desperdício e o controle de custos.</span><span class="sxs-lookup"><span data-stu-id="fced1-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="fced1-110">Você pode testar a versão mais recente do seu aplicativo, provisionamento ambientes Windows e Linux rapidamente usando modelos reutilizáveis e artefatos.</span><span class="sxs-lookup"><span data-stu-id="fced1-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="fced1-111">Integre facilmente seu pipeline de implantação dos Laboratórios de Teste/Desenvolvimento para provisionar ambientes sob demanda.</span><span class="sxs-lookup"><span data-stu-id="fced1-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="fced1-112">Dimensione seu teste de carga provisionando vários agentes de teste e crie ambientes previamente provisionados para treinamento e demonstrações.</span><span class="sxs-lookup"><span data-stu-id="fced1-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="fced1-113">Os Laboratórios de Teste/Desenvolvimento oferecem os seguintes benefícios na criação, configuração e gerenciamento ambientes de teste e de desenvolvedor na nuvem</span><span class="sxs-lookup"><span data-stu-id="fced1-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="fced1-114">Autoatendimento sem preocupações</span><span class="sxs-lookup"><span data-stu-id="fced1-114">Worry-free self-service</span></span>
<span data-ttu-id="fced1-115">Os Laboratórios de Teste/Desenvolvimento facilitam o controle de custos, permitindo que você defina diretivas em seu laboratório - como o número de máquinas virtuais (VM) por usuário e o número de VMs por laboratório.</span><span class="sxs-lookup"><span data-stu-id="fced1-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="fced1-116">Os Laboratórios de Teste/Desenvolvimento também permitem que você crie políticas para desligar e iniciar automaticamente as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="fced1-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="fced1-117">Chegue rapidamente ao estado Pronto para teste</span><span class="sxs-lookup"><span data-stu-id="fced1-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="fced1-118">Os Laboratório de Teste/Desenvolvimento permitem que você crie ambientes pré-provisionados com tudo o que a sua equipe precisa para começar a desenvolver e testar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fced1-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="fced1-119">Basta declarar os ambientes onde a última compilação boa do seu aplicativo foi instalada e começar a trabalhar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="fced1-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="fced1-120">Ou use os contêineres para uma criação de ambiente mais rápida e descomplicada.</span><span class="sxs-lookup"><span data-stu-id="fced1-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="fced1-121">Crie uma vez, use em qualquer lugar</span><span class="sxs-lookup"><span data-stu-id="fced1-121">Create once, use everywhere</span></span>
<span data-ttu-id="fced1-122">Capture e compartilhe modelos e artefatos de ambiente com sua equipe ou organização, tudo no controle do código-fonte, para criar ambientes de desenvolvedor e de teste facilmente.</span><span class="sxs-lookup"><span data-stu-id="fced1-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="fced1-123">Integra-se com a sua cadeia de ferramentas existente</span><span class="sxs-lookup"><span data-stu-id="fced1-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="fced1-124">Aproveite plug-ins pré-fabricados ou nossa API para provisionar ambientes de Desenvolvimento/Teste diretamente da sua ferramenta de CI (integração contínua), IDE (ambiente de desenvolvimento integrado) ou pipeline de liberação automatizada preferido.</span><span class="sxs-lookup"><span data-stu-id="fced1-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="fced1-125">Você também pode usar nossa ferramenta de linha de comando abrangente.</span><span class="sxs-lookup"><span data-stu-id="fced1-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="fced1-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fced1-126">Next steps</span></span>
[<span data-ttu-id="fced1-127">Conceitos dos Laboratórios de Desenvolvimento/Teste</span><span class="sxs-lookup"><span data-stu-id="fced1-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

