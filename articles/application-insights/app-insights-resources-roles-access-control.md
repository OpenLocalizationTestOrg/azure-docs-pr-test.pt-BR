---
title: "Recursos, funções e controle de acesso no Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="32aba-103">Recursos, funções e controle de acesso no Application Insights</span><span class="sxs-lookup"><span data-stu-id="32aba-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="32aba-104">Você pode controlar quem tem acesso de leitura e atualização a seus dados no [Application Insights do Azure][start] usando o [Controle de acesso baseado em função no Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="32aba-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32aba-105">Atribua acesso aos usuários no **grupo de recursos ou assinatura** ao qual o recurso do aplicativo pertence, não no próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="32aba-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="32aba-106">Atribua a função **Colaborador de componente do Application Insights** .</span><span class="sxs-lookup"><span data-stu-id="32aba-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="32aba-107">Isso garante o controle uniforme de acesso a testes na Web e alertas, juntamente com o recurso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32aba-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="32aba-108">[Saiba mais](#access).</span><span class="sxs-lookup"><span data-stu-id="32aba-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="32aba-109">Recursos, grupos e assinaturas</span><span class="sxs-lookup"><span data-stu-id="32aba-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="32aba-110">Primeiro, algumas definições:</span><span class="sxs-lookup"><span data-stu-id="32aba-110">First, some definitions:</span></span>

* <span data-ttu-id="32aba-111">**Recurso** ‒ uma instância de um serviço do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="32aba-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="32aba-112">O recurso do Application Insights coleta, analisa e exibe os dados de telemetria enviados de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32aba-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="32aba-113">Outros tipos de recursos do Azure incluem aplicativos Web, bancos de dados e VMs.</span><span class="sxs-lookup"><span data-stu-id="32aba-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="32aba-114">Para ver seus recursos, abra o [portal do Azure][portal], conecte-se e clique em Todos os Recursos.</span><span class="sxs-lookup"><span data-stu-id="32aba-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="32aba-115">Para encontrar um recurso, digite uma parte de seu nome no campo de filtro.</span><span class="sxs-lookup"><span data-stu-id="32aba-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Lista de recursos do Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="32aba-117">[**Grupo de recursos**][group] ‒ cada recurso pertence a um grupo.</span><span class="sxs-lookup"><span data-stu-id="32aba-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="32aba-118">Um grupo é uma maneira conveniente de gerenciar recursos relacionados, particularmente para controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="32aba-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="32aba-119">Por exemplo, em um grupo de recursos, você pode colocar um aplicativo Web, um recurso do Application Insights para monitorar o aplicativo e um Recurso de armazenamento para manter os dados exportados.</span><span class="sxs-lookup"><span data-stu-id="32aba-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Escolha Procurar e Grupos de recursos e, em seguida, escolha um grupo](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="32aba-121">[**Assinatura**](https://manage.windowsazure.com) - para usar o Application Insights ou outros recursos do Azure, entre em uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="32aba-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="32aba-122">Cada grupo de recursos pertence a uma assinatura do Azure, em que você escolhe o pacote de preços e, se for uma assinatura de organização, escolhe os membros e suas permissões de acesso.</span><span class="sxs-lookup"><span data-stu-id="32aba-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="32aba-123">[**Conta da Microsoft**][account] - o nome de usuário e a senha que você usa para entrar nas assinaturas do Microsoft Azure, no XBox Live, no Outlook.com e em outros serviços da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32aba-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="32aba-124"><a name="access"></a> Controlar o acesso no grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="32aba-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="32aba-125">É importante entender que, além do recurso criado para seu aplicativo, também há recursos ocultos separados para alertas e testes na Web.</span><span class="sxs-lookup"><span data-stu-id="32aba-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="32aba-126">Eles estão conectados ao mesmo [grupo de recursos](#resource-group) do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32aba-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="32aba-127">Você também pode colocar outros serviços do Azure nele, como sites ou armazenamento.</span><span class="sxs-lookup"><span data-stu-id="32aba-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Recursos no Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="32aba-129">Portanto, para controlar o acesso a esses recursos, é recomendável:</span><span class="sxs-lookup"><span data-stu-id="32aba-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="32aba-130">Controlar o acesso no nível de **grupo de recursos ou assinatura** .</span><span class="sxs-lookup"><span data-stu-id="32aba-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="32aba-131">Atribuir a função **Colaborador de componente do Application Insights** aos usuários.</span><span class="sxs-lookup"><span data-stu-id="32aba-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="32aba-132">Isso permite editar testes na Web, alertas e recursos do Application Insights, sem fornecer acesso a qualquer outro serviço no grupo.</span><span class="sxs-lookup"><span data-stu-id="32aba-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="32aba-133">Para fornecer acesso a outro usuário</span><span class="sxs-lookup"><span data-stu-id="32aba-133">To provide access to another user</span></span>
<span data-ttu-id="32aba-134">Você deve ter direitos de Proprietário para a assinatura ou o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="32aba-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="32aba-135">O usuário deve ter uma [conta da Microsoft][account] ou acesso à sua [conta organizacional da Microsoft](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="32aba-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="32aba-136">Você pode fornecer acesso a indivíduos e também a grupos de usuários definidos no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32aba-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="32aba-137">Navegue até o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="32aba-137">Navigate to the resource group</span></span>
<span data-ttu-id="32aba-138">Adicione o usuário a ele.</span><span class="sxs-lookup"><span data-stu-id="32aba-138">Add the user there.</span></span>

![Na folha de recursos de seu aplicativo, abra Essentials, abra o grupo de recursos e selecione Configurações/Usuários.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="32aba-141">Ou então, você poderia ir para um nível acima e adicionar o usuário à Assinatura.</span><span class="sxs-lookup"><span data-stu-id="32aba-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="32aba-142">Selecione uma função</span><span class="sxs-lookup"><span data-stu-id="32aba-142">Select a role</span></span>
![Selecione uma função para o novo usuário](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="32aba-144">Função</span><span class="sxs-lookup"><span data-stu-id="32aba-144">Role</span></span> | <span data-ttu-id="32aba-145">No grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="32aba-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="32aba-146">Proprietário</span><span class="sxs-lookup"><span data-stu-id="32aba-146">Owner</span></span> |<span data-ttu-id="32aba-147">Pode alterar qualquer item, incluindo o acesso do usuário</span><span class="sxs-lookup"><span data-stu-id="32aba-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="32aba-148">Colaborador</span><span class="sxs-lookup"><span data-stu-id="32aba-148">Contributor</span></span> |<span data-ttu-id="32aba-149">Pode editar qualquer item, incluindo todos os recursos</span><span class="sxs-lookup"><span data-stu-id="32aba-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="32aba-150">Colaborador de componente do Application Insights</span><span class="sxs-lookup"><span data-stu-id="32aba-150">Application Insights Component contributor</span></span> |<span data-ttu-id="32aba-151">Pode editar recursos do Application Insights, testes na Web e alertas</span><span class="sxs-lookup"><span data-stu-id="32aba-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="32aba-152">Leitor</span><span class="sxs-lookup"><span data-stu-id="32aba-152">Reader</span></span> |<span data-ttu-id="32aba-153">Pode exibir, mas não pode alterar nada</span><span class="sxs-lookup"><span data-stu-id="32aba-153">Can view but not change anything</span></span> |

<span data-ttu-id="32aba-154">A 'edição' inclui a criação, a exclusão e a atualização:</span><span class="sxs-lookup"><span data-stu-id="32aba-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="32aba-155">Recursos</span><span class="sxs-lookup"><span data-stu-id="32aba-155">Resources</span></span>
* <span data-ttu-id="32aba-156">Testes da Web</span><span class="sxs-lookup"><span data-stu-id="32aba-156">Web tests</span></span>
* <span data-ttu-id="32aba-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="32aba-157">Alerts</span></span>
* <span data-ttu-id="32aba-158">Exportação contínua</span><span class="sxs-lookup"><span data-stu-id="32aba-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="32aba-159">Selecione o usuário</span><span class="sxs-lookup"><span data-stu-id="32aba-159">Select the user</span></span>

<span data-ttu-id="32aba-160">Se o usuário desejado não estiver no diretório, você poderá convidar qualquer pessoa com uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32aba-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="32aba-161">(Se ela usa serviços como Outlook.com, OneDrive, Windows Phone ou XBox Live, já tem uma conta da Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="32aba-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="32aba-162">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="32aba-162">Related content</span></span>

* [<span data-ttu-id="32aba-163">Controle de acesso baseado em função no Azure</span><span class="sxs-lookup"><span data-stu-id="32aba-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
