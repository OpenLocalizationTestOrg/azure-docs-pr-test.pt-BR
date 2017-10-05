---
title: "Relatórios de atividade de entrada no portal do Azure Active Directory | Microsoft Docs"
description: "Introdução aos relatórios de atividades de entrada no portal do Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="a3f7e-103">Relatórios de atividades de entrada no portal do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3f7e-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="a3f7e-104">Com os relatórios do Azure Active Directory (Azure AD) no [portal do Azure](https://portal.azure.com) você obtém todas as informações de que precisa para determinar como seu ambiente está se comportando.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="a3f7e-105">A arquitetura de relatório no Azure Active Directory consiste nos seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="a3f7e-106">**Atividade**</span><span class="sxs-lookup"><span data-stu-id="a3f7e-106">**Activity**</span></span> 
    - <span data-ttu-id="a3f7e-107">**Atividades de entrada** – informações sobre o uso de aplicativos gerenciados e de atividades de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="a3f7e-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="a3f7e-108">**Logs de auditoria** – informações de atividade do sistema sobre o gerenciamento de usuários e de grupos, sobre os aplicativos gerenciados e sobre as atividades de diretório.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="a3f7e-109">**Segurança**</span><span class="sxs-lookup"><span data-stu-id="a3f7e-109">**Security**</span></span> 
    - <span data-ttu-id="a3f7e-110">**Entradas arriscadas** - uma entrada arriscada é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é o proprietário legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="a3f7e-111">Para obter mais detalhes, veja Entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="a3f7e-112">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="a3f7e-113">Para obter mais detalhes, consulte Usuários sinalizados para risco.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="a3f7e-114">Este tópico fornece uma visão geral das atividades de entrada.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="a3f7e-115">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="a3f7e-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="a3f7e-116">Quem pode acessar os dados?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-116">Who can access the data?</span></span>
* <span data-ttu-id="a3f7e-117">Usuários na função de Administrador de segurança ou Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="a3f7e-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="a3f7e-118">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="a3f7e-118">Global Admins</span></span>
* <span data-ttu-id="a3f7e-119">Qualquer usuário (não administradores) pode acessar suas próprias entradas</span><span class="sxs-lookup"><span data-stu-id="a3f7e-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="a3f7e-120">Qual licença do Azure AD você precisa para acessar a atividade de entrada?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="a3f7e-121">Seu locatário deve ter uma licença do Azure AD Premium associada a ele para ver o relatório de atividade de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="a3f7e-122">Atividades de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-122">Signs-in activities</span></span>

<span data-ttu-id="a3f7e-123">Com as informações fornecidas pelo relatório de entrada de usuário, você encontra respostas para perguntas como:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="a3f7e-124">O que é o padrão de entrada de um usuário?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="a3f7e-125">Quantos usuários entraram em uma semana?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="a3f7e-126">Qual é o status dessas entradas?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="a3f7e-127">O seu primeiro ponto de entrada para todos os dados de atividades de entrada é **Entradas** na seção Atividade do **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="a3f7e-128">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/61.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="a3f7e-129">Um log de auditoria tem um modo de exibição de lista padrão que mostra:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="a3f7e-130">o usuário relacionado</span><span class="sxs-lookup"><span data-stu-id="a3f7e-130">the related user</span></span>
- <span data-ttu-id="a3f7e-131">o aplicativo no qual o usuário entrou</span><span class="sxs-lookup"><span data-stu-id="a3f7e-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="a3f7e-132">o status de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-132">the sign-in status</span></span>
- <span data-ttu-id="a3f7e-133">a hora de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-133">the sign-in time</span></span>

<span data-ttu-id="a3f7e-134">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/41.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-135">Você pode personalizar o modo de exibição de lista clicando em **Colunas** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="a3f7e-136">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/19.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-137">Isso permite a você exibir campos adicionais ou remover campos que já estão exibidos.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="a3f7e-138">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/42.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-139">Ao clicar em um item na exibição de lista, você obterá mais detalhes sobre ele.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="a3f7e-140">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/43.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="a3f7e-141">Filtragem de atividades de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-141">Filtering sign-in activities</span></span>

<span data-ttu-id="a3f7e-142">Para restringir os dados relatados a um nível que funciona para você, filtre os dados de entradas usando os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="a3f7e-143">Intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="a3f7e-143">Time interval</span></span>
- <span data-ttu-id="a3f7e-144">Usuário</span><span class="sxs-lookup"><span data-stu-id="a3f7e-144">User</span></span>
- <span data-ttu-id="a3f7e-145">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a3f7e-145">Application</span></span>
- <span data-ttu-id="a3f7e-146">Cliente</span><span class="sxs-lookup"><span data-stu-id="a3f7e-146">Client</span></span>
- <span data-ttu-id="a3f7e-147">Status de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-147">Sign-in status</span></span>

<span data-ttu-id="a3f7e-148">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/44.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="a3f7e-149">O filtro **intervalo de tempo** permite a você definir um período de tempo para os dados retornados.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="a3f7e-150">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-150">Possible values are:</span></span>

- <span data-ttu-id="a3f7e-151">1 mês</span><span class="sxs-lookup"><span data-stu-id="a3f7e-151">1 month</span></span>
- <span data-ttu-id="a3f7e-152">7 dias</span><span class="sxs-lookup"><span data-stu-id="a3f7e-152">7 days</span></span>
- <span data-ttu-id="a3f7e-153">24 horas</span><span class="sxs-lookup"><span data-stu-id="a3f7e-153">24 hours</span></span>
- <span data-ttu-id="a3f7e-154">Personalizado</span><span class="sxs-lookup"><span data-stu-id="a3f7e-154">Custom</span></span>

<span data-ttu-id="a3f7e-155">Quando você seleciona um período de tempo personalizado, pode configurar uma hora de início e uma hora de término.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="a3f7e-156">O filtro **usuário** permite que você especifique o nome ou o UPN (nome principal do usuário) do usuário desejado.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="a3f7e-157">O filtro **aplicativo** permite que você especifique o nome do aplicativo desejado.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="a3f7e-158">O filtro **cliente** permite que você especifique informações sobre o dispositivo desejado.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="a3f7e-159">O filtro **status de entrada** permite que você selecione um dos filtros abaixo:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="a3f7e-160">Todos</span><span class="sxs-lookup"><span data-stu-id="a3f7e-160">All</span></span>
- <span data-ttu-id="a3f7e-161">Sucesso</span><span class="sxs-lookup"><span data-stu-id="a3f7e-161">Success</span></span>
- <span data-ttu-id="a3f7e-162">Failure</span><span class="sxs-lookup"><span data-stu-id="a3f7e-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="a3f7e-163">Atalhos de atividades de entrada</span><span class="sxs-lookup"><span data-stu-id="a3f7e-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="a3f7e-164">Além do Azure Active Directory, o portal do Azure fornece dois pontos de entrada adicionais para dados de atividade de entrada:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="a3f7e-165">Usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="a3f7e-165">Users and groups</span></span>
- <span data-ttu-id="a3f7e-166">Aplicativos empresariais</span><span class="sxs-lookup"><span data-stu-id="a3f7e-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="a3f7e-167">Atividades de entrada de usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="a3f7e-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="a3f7e-168">Com as informações fornecidas pelo relatório de entrada de usuário, você encontra respostas para perguntas como:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="a3f7e-169">O que é o padrão de entrada de um usuário?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="a3f7e-170">Quantos usuários entraram em uma semana?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="a3f7e-171">Qual é o status dessas entradas?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="a3f7e-172">O ponto de entrada para esses dados é o gráfico de entrada do usuário na seção **Visão geral** em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="a3f7e-173">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/45.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-174">O gráfico de entrada do usuário mostra agregações semanais de entradas para todos os usuários em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="a3f7e-175">O padrão para o período é de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="a3f7e-176">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/46.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-177">Quando você clica em um dia no gráfico de entradas, obtém uma lista detalhada das atividades de entrada do dia.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="a3f7e-178">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/41.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-179">Cada linha na lista de atividades de entrada oferece as informações detalhadas sobre a entrada selecionada, como:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="a3f7e-180">Quem entrou?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-180">Who has signed in?</span></span>
* <span data-ttu-id="a3f7e-181">Qual era o UPN relacionado?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-181">What was the related UPN?</span></span>
* <span data-ttu-id="a3f7e-182">Qual aplicativo era o destino da entrada?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="a3f7e-183">Qual é o endereço IP da entrada?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="a3f7e-184">Qual era o status da entrada?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="a3f7e-185">A opção **entradas** fornece uma visão geral completa de todas as entradas de usuário.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="a3f7e-186">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/51.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="a3f7e-187">Uso de aplicativos gerenciados</span><span class="sxs-lookup"><span data-stu-id="a3f7e-187">Usage of managed applications</span></span>

<span data-ttu-id="a3f7e-188">Com uma exibição centrada no aplicativo de seus dados de entrada, você pode responder a perguntas como:</span><span class="sxs-lookup"><span data-stu-id="a3f7e-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="a3f7e-189">Quem está usando meus aplicativos?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-189">Who is using my applications?</span></span>
* <span data-ttu-id="a3f7e-190">Quais são os três principais aplicativos em sua organização?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="a3f7e-191">Recentemente, eu implantei um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-191">I have recently rolled out an application.</span></span> <span data-ttu-id="a3f7e-192">Como ele está se saindo?</span><span class="sxs-lookup"><span data-stu-id="a3f7e-192">How is it doing?</span></span>

<span data-ttu-id="a3f7e-193">Seu ponto de entrada para esses dados é composto pelos três principais aplicativos em sua organização no relatório dos 30 últimos dias, presente na seção **Visão geral**, em **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="a3f7e-194">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/64.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-195">As agregações semanais ao gráfico de uso do aplicativo de entradas para seus três principais aplicativos em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="a3f7e-196">O padrão para o período é de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="a3f7e-197">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/47.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="a3f7e-198">Se desejar, você pode definir o foco em um aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="a3f7e-199">![Relatórios](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Relatórios")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="a3f7e-200">Quando você clica em um dia no gráfico de uso do aplicativo, pode obter uma lista detalhada das atividades de entrada.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="a3f7e-201">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/48.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="a3f7e-202">A opção **Entradas** oferece uma visão geral completa de todos os eventos de entrada para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a3f7e-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="a3f7e-203">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/49.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="a3f7e-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="a3f7e-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3f7e-204">Next steps</span></span>

<span data-ttu-id="a3f7e-205">Se você quiser saber mais sobre os códigos de erro da atividade de entrada, confira o [Códigos de erro do relatório de atividade de entrada no portal do Azure Active Directory](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a3f7e-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

