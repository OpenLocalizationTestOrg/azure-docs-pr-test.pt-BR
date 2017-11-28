---
title: "aaaResources, funções e controle de acesso no Azure Application Insights | Microsoft Docs"
description: "Proprietários, colaboradores e leitores de percepções de sua organização."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="4fbad-103">Recursos, funções e controle de acesso no Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fbad-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="4fbad-104">Você pode controlar quem tem ler e atualizar dados do access tooyour no Azure [Application Insights][start], usando [controle de acesso baseado em função no Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4fbad-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fbad-105">Atribuir acesso toousers em Olá **grupo de recursos ou assinatura** toowhich pertence o recurso de aplicativo - não no próprio recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fbad-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="4fbad-106">Atribuir Olá **Colaborador de componente do Application Insights** função.</span><span class="sxs-lookup"><span data-stu-id="4fbad-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="4fbad-107">Isso garante uniforme controle de acesso tooweb testes e alertas juntamente com o recurso de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fbad-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="4fbad-108">[Saiba mais](#access).</span><span class="sxs-lookup"><span data-stu-id="4fbad-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="4fbad-109">Recursos, grupos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="4fbad-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="4fbad-110">Primeiro, algumas definições:</span><span class="sxs-lookup"><span data-stu-id="4fbad-110">First, some definitions:</span></span>

* <span data-ttu-id="4fbad-111">**Recurso** ‒ uma instância de um serviço do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbad-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="4fbad-112">O recurso do Application Insights coleta, analisa e exibe dados de telemetria saudação enviados do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fbad-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="4fbad-113">Outros tipos de recursos do Azure incluem aplicativos Web, bancos de dados e VMs.</span><span class="sxs-lookup"><span data-stu-id="4fbad-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="4fbad-114">toosee seus recursos, abra Olá [Portal do Azure][portal], entre e clique em todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="4fbad-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="4fbad-115">toofind um recurso, tipo de parte de seu nome no campo de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fbad-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Lista de recursos do Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="4fbad-117">[**Grupo de recursos** ] [ group] -cada recurso pertence tooone grupo.</span><span class="sxs-lookup"><span data-stu-id="4fbad-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="4fbad-118">Um grupo é uma maneira toomanage relacionadas a recursos, particularmente para controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="4fbad-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="4fbad-119">Por exemplo, em um recurso de grupo, você pode colocar um aplicativo Web, um aplicativo de saudação do Application Insights recursos toomonitor e um tookeep de recursos de armazenamento dados exportados.</span><span class="sxs-lookup"><span data-stu-id="4fbad-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Escolha Procurar e Grupos de recursos e, em seguida, escolha um grupo](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="4fbad-121">[**Assinatura** ](https://manage.windowsazure.com) -toouse Application Insights ou outros recursos do Azure, você entrar tooan assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbad-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="4fbad-122">Cada grupo de recursos pertence tooone assinatura do Azure, onde você escolha seu pacote de preços e, se for uma assinatura de organização, escolha Olá membros e suas permissões de acesso.</span><span class="sxs-lookup"><span data-stu-id="4fbad-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="4fbad-123">[**Conta da Microsoft** ] [ account] -Olá, nome de usuário e senha que você use toosign em tooMicrosoft Azure assinaturas, XBox Live, Outlook.com e outros serviços da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4fbad-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="4fbad-124"><a name="access"></a>Controlar o acesso no grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="4fbad-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="4fbad-125">É importante toounderstand que o recurso de toohello adição que você criou para seu aplicativo, há também separar recursos ocultos para alertas e testes da web.</span><span class="sxs-lookup"><span data-stu-id="4fbad-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="4fbad-126">Eles são anexado toohello mesmo [grupo de recursos](#resource-group) como seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fbad-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="4fbad-127">Você também pode colocar outros serviços do Azure nele, como sites ou armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4fbad-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Recursos no Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="4fbad-129">toocontrol acessar recursos de toothese, portanto, é recomendável:</span><span class="sxs-lookup"><span data-stu-id="4fbad-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="4fbad-130">Controlar o acesso no hello **grupo de recursos ou assinatura** nível.</span><span class="sxs-lookup"><span data-stu-id="4fbad-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="4fbad-131">Atribuir Olá **Colaborador de componente do Application Insights** toousers de função.</span><span class="sxs-lookup"><span data-stu-id="4fbad-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="4fbad-132">Isso permite que os testes de web tooedit, alertas e recursos do Application Insights, sem fornecer acesso tooany outros serviços no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fbad-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="4fbad-133">tooprovide tooanother usuário</span><span class="sxs-lookup"><span data-stu-id="4fbad-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="4fbad-134">Você deve ter a assinatura de toohello de direitos de proprietário ou grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fbad-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="4fbad-135">saudação de usuário deve ter uma [Account da Microsoft][account], ou acessar tootheir [organizacional Microsoft Account](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="4fbad-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="4fbad-136">Você pode fornecer acesso tooindividuals e toouser grupos definidos no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbad-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="4fbad-137">Navegue toohello grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4fbad-137">Navigate toohello resource group</span></span>
<span data-ttu-id="4fbad-138">Adicione usuário Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="4fbad-138">Add hello user there.</span></span>

![Na folha de recursos do aplicativo, abra o Essentials, abra o grupo de recursos de saudação e nele, selecione configurações/usuários.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="4fbad-141">Ou você pode ir para cima outro nível e adicionar Olá usuário toohello assinatura.</span><span class="sxs-lookup"><span data-stu-id="4fbad-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="4fbad-142">Selecione uma função</span><span class="sxs-lookup"><span data-stu-id="4fbad-142">Select a role</span></span>
![Selecione uma função de usuário nova Olá](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="4fbad-144">Função</span><span class="sxs-lookup"><span data-stu-id="4fbad-144">Role</span></span> | <span data-ttu-id="4fbad-145">No grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="4fbad-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="4fbad-146">Proprietário</span><span class="sxs-lookup"><span data-stu-id="4fbad-146">Owner</span></span> |<span data-ttu-id="4fbad-147">Pode alterar qualquer item, incluindo o acesso do usuário</span><span class="sxs-lookup"><span data-stu-id="4fbad-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="4fbad-148">Colaborador</span><span class="sxs-lookup"><span data-stu-id="4fbad-148">Contributor</span></span> |<span data-ttu-id="4fbad-149">Pode editar qualquer item, incluindo todos os recursos</span><span class="sxs-lookup"><span data-stu-id="4fbad-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="4fbad-150">Colaborador de componente do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fbad-150">Application Insights Component contributor</span></span> |<span data-ttu-id="4fbad-151">Pode editar recursos do Application Insights, testes na Web e alertas</span><span class="sxs-lookup"><span data-stu-id="4fbad-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="4fbad-152">Leitor</span><span class="sxs-lookup"><span data-stu-id="4fbad-152">Reader</span></span> |<span data-ttu-id="4fbad-153">Pode exibir, mas não pode alterar nada</span><span class="sxs-lookup"><span data-stu-id="4fbad-153">Can view but not change anything</span></span> |

<span data-ttu-id="4fbad-154">A 'edição' inclui a criação, a exclusão e a atualização:</span><span class="sxs-lookup"><span data-stu-id="4fbad-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="4fbad-155">Recursos</span><span class="sxs-lookup"><span data-stu-id="4fbad-155">Resources</span></span>
* <span data-ttu-id="4fbad-156">Testes da Web</span><span class="sxs-lookup"><span data-stu-id="4fbad-156">Web tests</span></span>
* <span data-ttu-id="4fbad-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="4fbad-157">Alerts</span></span>
* <span data-ttu-id="4fbad-158">Exportação contínua</span><span class="sxs-lookup"><span data-stu-id="4fbad-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="4fbad-159">Selecione o usuário Olá</span><span class="sxs-lookup"><span data-stu-id="4fbad-159">Select hello user</span></span>

<span data-ttu-id="4fbad-160">Se o usuário Olá desejado não estiver no diretório hello, você pode convidar qualquer pessoa com uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4fbad-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="4fbad-161">(Se ela usa serviços como Outlook.com, OneDrive, Windows Phone ou XBox Live, já tem uma conta da Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="4fbad-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="4fbad-162">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="4fbad-162">Related content</span></span>

* [<span data-ttu-id="4fbad-163">Controle de acesso baseado em função no Azure</span><span class="sxs-lookup"><span data-stu-id="4fbad-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
