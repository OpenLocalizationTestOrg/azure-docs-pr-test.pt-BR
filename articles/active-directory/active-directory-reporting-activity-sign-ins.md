---
title: "relatórios de atividade aaaSign no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Relatórios de atividade toosign de Introdução no portal do Azure Active Directory Olá"
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
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="46cf4-103">Relatórios de atividade de entrada no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="46cf4-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="46cf4-104">Com o Azure Active Directory (AD do Azure) reporting em Olá [portal do Azure](https://portal.azure.com), você pode obter informações de saudação necessário toodetermine como seu ambiente está fazendo.</span><span class="sxs-lookup"><span data-stu-id="46cf4-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="46cf4-105">Olá arquitetura de relatórios no Active Directory do Azure consiste em Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cf4-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="46cf4-106">**Atividade**</span><span class="sxs-lookup"><span data-stu-id="46cf4-106">**Activity**</span></span> 
    - <span data-ttu-id="46cf4-107">**Atividades de entrada** – informações sobre o uso de saudação de aplicativos gerenciados e atividades de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="46cf4-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="46cf4-108">**Logs de auditoria** – informações de atividade do sistema sobre o gerenciamento de usuários e de grupos, sobre os aplicativos gerenciados e sobre as atividades de diretório.</span><span class="sxs-lookup"><span data-stu-id="46cf4-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="46cf4-109">**Segurança**</span><span class="sxs-lookup"><span data-stu-id="46cf4-109">**Security**</span></span> 
    - <span data-ttu-id="46cf4-110">**Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="46cf4-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="46cf4-111">Para obter mais detalhes, veja Entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="46cf4-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="46cf4-112">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="46cf4-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="46cf4-113">Para obter mais detalhes, consulte Usuários sinalizados para risco.</span><span class="sxs-lookup"><span data-stu-id="46cf4-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="46cf4-114">Este tópico fornece uma visão geral das atividades de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="46cf4-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="46cf4-115">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="46cf4-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="46cf4-116">Quem pode acessar dados Olá?</span><span class="sxs-lookup"><span data-stu-id="46cf4-116">Who can access hello data?</span></span>
* <span data-ttu-id="46cf4-117">Usuários na função de administrador de segurança ou segurança leitor Olá</span><span class="sxs-lookup"><span data-stu-id="46cf4-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="46cf4-118">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="46cf4-118">Global Admins</span></span>
* <span data-ttu-id="46cf4-119">Qualquer usuário (não administradores) pode acessar suas próprias entradas</span><span class="sxs-lookup"><span data-stu-id="46cf4-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="46cf4-120">Qual licença do AD do Azure precisa de atividade de entrada tooaccess?</span><span class="sxs-lookup"><span data-stu-id="46cf4-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="46cf4-121">Seu locatário deve ter uma licença Azure AD Premium associada a ele toosee Olá tudo sign-relatório de atividade</span><span class="sxs-lookup"><span data-stu-id="46cf4-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="46cf4-122">Atividades de entrada</span><span class="sxs-lookup"><span data-stu-id="46cf4-122">Signs-in activities</span></span>

<span data-ttu-id="46cf4-123">Com informações de saudação fornecidas pelo relatório de entrada do usuário de saudação, você encontrar respostas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="46cf4-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="46cf4-124">O que é Olá entrar padrão de um usuário?</span><span class="sxs-lookup"><span data-stu-id="46cf4-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="46cf4-125">Quantos usuários entraram em uma semana?</span><span class="sxs-lookup"><span data-stu-id="46cf4-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="46cf4-126">Qual é o status de saudação destas entradas?</span><span class="sxs-lookup"><span data-stu-id="46cf4-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="46cf4-127">Seu primeiro entrada tooall de ponto de entrada atividades dados **entradas** na seção de atividade de saudação do **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="46cf4-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="46cf4-128">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/61.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="46cf4-129">Um log de auditoria tem um modo de exibição de lista padrão que mostra:</span><span class="sxs-lookup"><span data-stu-id="46cf4-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="46cf4-130">usuário relacionado Olá</span><span class="sxs-lookup"><span data-stu-id="46cf4-130">hello related user</span></span>
- <span data-ttu-id="46cf4-131">Olá aplicativo hello tenha assinado do usuário para</span><span class="sxs-lookup"><span data-stu-id="46cf4-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="46cf4-132">status de entrada Hello</span><span class="sxs-lookup"><span data-stu-id="46cf4-132">hello sign-in status</span></span>
- <span data-ttu-id="46cf4-133">hora de entrada Hello</span><span class="sxs-lookup"><span data-stu-id="46cf4-133">hello sign-in time</span></span>

<span data-ttu-id="46cf4-134">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/41.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-135">Você pode personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="46cf4-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="46cf4-136">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/19.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-137">Isso permite que os campos adicionais toodisplay ou remover campos que já estão sendo exibidos.</span><span class="sxs-lookup"><span data-stu-id="46cf4-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="46cf4-138">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/42.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-139">Ao clicar em um item na exibição de lista Olá, você deve obter todos os detalhes disponíveis sobre ele.</span><span class="sxs-lookup"><span data-stu-id="46cf4-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="46cf4-140">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/43.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="46cf4-141">Filtragem de atividades de entrada</span><span class="sxs-lookup"><span data-stu-id="46cf4-141">Filtering sign-in activities</span></span>

<span data-ttu-id="46cf4-142">toonarrow inativo saudação relatados nível tooa de dados que funciona para você, você pode filtrar dados de entradas de saudação usando Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cf4-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="46cf4-143">Intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="46cf4-143">Time interval</span></span>
- <span data-ttu-id="46cf4-144">Usuário</span><span class="sxs-lookup"><span data-stu-id="46cf4-144">User</span></span>
- <span data-ttu-id="46cf4-145">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="46cf4-145">Application</span></span>
- <span data-ttu-id="46cf4-146">Cliente</span><span class="sxs-lookup"><span data-stu-id="46cf4-146">Client</span></span>
- <span data-ttu-id="46cf4-147">Status de entrada</span><span class="sxs-lookup"><span data-stu-id="46cf4-147">Sign-in status</span></span>

<span data-ttu-id="46cf4-148">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/44.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="46cf4-149">Olá **intervalo de tempo** filtro habilita tooyou toodefine um período de tempo para Olá retornou dados.</span><span class="sxs-lookup"><span data-stu-id="46cf4-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="46cf4-150">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="46cf4-150">Possible values are:</span></span>

- <span data-ttu-id="46cf4-151">1 mês</span><span class="sxs-lookup"><span data-stu-id="46cf4-151">1 month</span></span>
- <span data-ttu-id="46cf4-152">7 dias</span><span class="sxs-lookup"><span data-stu-id="46cf4-152">7 days</span></span>
- <span data-ttu-id="46cf4-153">24 horas</span><span class="sxs-lookup"><span data-stu-id="46cf4-153">24 hours</span></span>
- <span data-ttu-id="46cf4-154">Personalizado</span><span class="sxs-lookup"><span data-stu-id="46cf4-154">Custom</span></span>

<span data-ttu-id="46cf4-155">Quando você seleciona um período de tempo personalizado, pode configurar uma hora de início e uma hora de término.</span><span class="sxs-lookup"><span data-stu-id="46cf4-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="46cf4-156">Olá **usuário** filtro permite que nome de saudação toospecify ou Olá principal nome de usuário (UPN) do usuário Olá importantes para você.</span><span class="sxs-lookup"><span data-stu-id="46cf4-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="46cf4-157">Olá **aplicativo** filtro permite toospecify nome de saudação do aplicativo hello importantes para você.</span><span class="sxs-lookup"><span data-stu-id="46cf4-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="46cf4-158">Olá **cliente** filtro permite que você toospecify informações sobre o dispositivo Olá importantes para você.</span><span class="sxs-lookup"><span data-stu-id="46cf4-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="46cf4-159">Olá **status de entrada** filtro permite tooselect de saudação filtro a seguir:</span><span class="sxs-lookup"><span data-stu-id="46cf4-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="46cf4-160">Todos</span><span class="sxs-lookup"><span data-stu-id="46cf4-160">All</span></span>
- <span data-ttu-id="46cf4-161">Sucesso</span><span class="sxs-lookup"><span data-stu-id="46cf4-161">Success</span></span>
- <span data-ttu-id="46cf4-162">Failure</span><span class="sxs-lookup"><span data-stu-id="46cf4-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="46cf4-163">Atalhos de atividades de entrada</span><span class="sxs-lookup"><span data-stu-id="46cf4-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="46cf4-164">Além disso tooAzure do Active Directory, Olá portal do Azure oferece dois dados de toosign em atividades de pontos de entrada adicional:</span><span class="sxs-lookup"><span data-stu-id="46cf4-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="46cf4-165">Usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="46cf4-165">Users and groups</span></span>
- <span data-ttu-id="46cf4-166">Aplicativos empresariais</span><span class="sxs-lookup"><span data-stu-id="46cf4-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="46cf4-167">Atividades de entrada de usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="46cf4-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="46cf4-168">Com informações de saudação fornecidas pelo relatório de entrada do usuário de saudação, você encontrar respostas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="46cf4-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="46cf4-169">O que é Olá entrar padrão de um usuário?</span><span class="sxs-lookup"><span data-stu-id="46cf4-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="46cf4-170">Quantos usuários entraram em uma semana?</span><span class="sxs-lookup"><span data-stu-id="46cf4-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="46cf4-171">Qual é o status de saudação destas entradas?</span><span class="sxs-lookup"><span data-stu-id="46cf4-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="46cf4-172">Os dados de toothis de ponto de entrada são Olá usuário entrar no gráfico de saudação **visão geral** seção em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="46cf4-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="46cf4-173">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/45.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-174">Olá usuário entrar gráfico mostra agregações semanais do sinal ins para todos os usuários em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="46cf4-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="46cf4-175">padrão de saudação para Olá o período de tempo é 30 dias.</span><span class="sxs-lookup"><span data-stu-id="46cf4-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="46cf4-176">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/46.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-177">Quando você clica em um dia no gráfico de entrada hello, você obtém uma lista detalhada das atividades de entrada hello para esse dia.</span><span class="sxs-lookup"><span data-stu-id="46cf4-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="46cf4-178">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/41.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-179">Cada linha na permite de lista de atividades de entrada hello que Olá informações detalhadas sobre Olá selecionado entrar como:</span><span class="sxs-lookup"><span data-stu-id="46cf4-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="46cf4-180">Quem entrou?</span><span class="sxs-lookup"><span data-stu-id="46cf4-180">Who has signed in?</span></span>
* <span data-ttu-id="46cf4-181">O que foi Olá relacionadas UPN?</span><span class="sxs-lookup"><span data-stu-id="46cf4-181">What was hello related UPN?</span></span>
* <span data-ttu-id="46cf4-182">Qual aplicativo era o destino de saudação de saudação entrar?</span><span class="sxs-lookup"><span data-stu-id="46cf4-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="46cf4-183">O que é o endereço IP de saudação do hello entrar?</span><span class="sxs-lookup"><span data-stu-id="46cf4-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="46cf4-184">Qual era o status de saudação do hello entrar?</span><span class="sxs-lookup"><span data-stu-id="46cf4-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="46cf4-185">Olá **entradas** opção fornece uma visão geral completa de todas as entradas do usuário.</span><span class="sxs-lookup"><span data-stu-id="46cf4-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="46cf4-186">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/51.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="46cf4-187">Uso de aplicativos gerenciados</span><span class="sxs-lookup"><span data-stu-id="46cf4-187">Usage of managed applications</span></span>

<span data-ttu-id="46cf4-188">Com uma exibição centrada no aplicativo de seus dados de entrada, você pode responder a perguntas como:</span><span class="sxs-lookup"><span data-stu-id="46cf4-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="46cf4-189">Quem está usando meus aplicativos?</span><span class="sxs-lookup"><span data-stu-id="46cf4-189">Who is using my applications?</span></span>
* <span data-ttu-id="46cf4-190">Quais são os principais 3 aplicativos Olá em sua organização?</span><span class="sxs-lookup"><span data-stu-id="46cf4-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="46cf4-191">Recentemente, eu implantei um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46cf4-191">I have recently rolled out an application.</span></span> <span data-ttu-id="46cf4-192">Como ele está se saindo?</span><span class="sxs-lookup"><span data-stu-id="46cf4-192">How is it doing?</span></span>

<span data-ttu-id="46cf4-193">Os dados de toothis de ponto de entrada são maiores 3 aplicativos Olá em sua organização no último relatório de 30 dias Olá no hello **visão geral** seção em **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="46cf4-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="46cf4-194">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/64.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-195">Olá aplicativo uso gráfico semanal agregações de entradas para seus aplicativos de 3 principais em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="46cf4-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="46cf4-196">padrão de saudação para Olá o período de tempo é 30 dias.</span><span class="sxs-lookup"><span data-stu-id="46cf4-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="46cf4-197">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/47.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="46cf4-198">Se desejar, você pode definir o foco de saudação em um aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="46cf4-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="46cf4-199">![Relatórios](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Relatórios")</span><span class="sxs-lookup"><span data-stu-id="46cf4-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="46cf4-200">Quando você clica em um dia no gráfico de uso do aplicativo hello, você pode obter uma lista detalhada das atividades de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="46cf4-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="46cf4-201">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/48.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="46cf4-202">Olá **entradas** opção fornece uma visão geral completa de todos os aplicativos de tooyour de eventos de entrada.</span><span class="sxs-lookup"><span data-stu-id="46cf4-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="46cf4-203">![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/49.png "Atividade de entrada")</span><span class="sxs-lookup"><span data-stu-id="46cf4-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="46cf4-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46cf4-204">Next steps</span></span>

<span data-ttu-id="46cf4-205">Se você quiser tooknow mais informações sobre códigos de erro de atividade de entrada, consulte Olá [entrar códigos de erro do atividade relatórios no portal do Azure Active Directory Olá](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="46cf4-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

