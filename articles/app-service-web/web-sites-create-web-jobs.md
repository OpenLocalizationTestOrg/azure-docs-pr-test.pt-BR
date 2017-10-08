---
title: tarefas do plano de fundo aaaRun com o WebJobs
description: Saiba como tarefas do plano de fundo toorun no Azure de aplicativos web.
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="d41f2-103">Executar tarefas em segundo plano com Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="d41f2-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="d41f2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d41f2-104">Overview</span></span>
<span data-ttu-id="d41f2-105">Você pode executar programas ou scripts em WebJobs em seu aplicativo Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) de três maneiras: sob demanda, continuamente ou com base em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="d41f2-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="d41f2-106">Não há nenhum custo adicional de toouse WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d41f2-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="d41f2-107">Este artigo mostra como toodeploy WebJobs usando Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d41f2-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="d41f2-108">Para obter informações sobre como toodeploy usando o Visual Studio ou um processo de entrega contínua, consulte [como tooDeploy do Azure WebJobs tooWeb aplicativos](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="d41f2-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="d41f2-109">Olá SDK do Azure WebJobs simplifica muitas tarefas de programação dos WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d41f2-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="d41f2-110">Para obter mais informações, consulte [novidades Olá SDK do WebJobs](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d41f2-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="d41f2-111">As funções do Azure fornece outra maneira como os programas toorun e scripts de um ambiente sem servidor ou de um aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d41f2-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="d41f2-112">Para saber mais, consulte [Visão geral do Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d41f2-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="d41f2-113"><a name="acceptablefiles"></a>Tipos de arquivo aceitáveis para scripts ou programas</span><span class="sxs-lookup"><span data-stu-id="d41f2-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="d41f2-114">Olá, tipos de arquivo a seguir é aceitas:</span><span class="sxs-lookup"><span data-stu-id="d41f2-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="d41f2-115">.cmd, .bat, .exe (usando o cmd do Windows)</span><span class="sxs-lookup"><span data-stu-id="d41f2-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="d41f2-116">.ps1 (usando o PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d41f2-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="d41f2-117">.sh (usando bash)</span><span class="sxs-lookup"><span data-stu-id="d41f2-117">.sh (using bash)</span></span>
* <span data-ttu-id="d41f2-118">.php (usando php)</span><span class="sxs-lookup"><span data-stu-id="d41f2-118">.php (using php)</span></span>
* <span data-ttu-id="d41f2-119">.py (usando o python)</span><span class="sxs-lookup"><span data-stu-id="d41f2-119">.py (using python)</span></span>
* <span data-ttu-id="d41f2-120">.js (usando nó)</span><span class="sxs-lookup"><span data-stu-id="d41f2-120">.js (using node)</span></span>
* <span data-ttu-id="d41f2-121">.jar (usando java)</span><span class="sxs-lookup"><span data-stu-id="d41f2-121">.jar (using java)</span></span>

## <span data-ttu-id="d41f2-122"><a name="CreateOnDemand"></a>Criar um relatório sob demanda WebJob no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="d41f2-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="d41f2-123">Em Olá **aplicativo Web** folha de saudação [Portal do Azure](https://portal.azure.com), clique em **todas as configurações > WebJobs** tooshow Olá **WebJobs** folha.</span><span class="sxs-lookup"><span data-stu-id="d41f2-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Lâmina do Trabalho Web](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="d41f2-125">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-125">Click **Add**.</span></span> <span data-ttu-id="d41f2-126">Olá **WebJob adicionar** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="d41f2-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Adicionar lâmina do Trabalho Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="d41f2-128">Em **nome**, forneça um nome para Olá WebJob.</span><span class="sxs-lookup"><span data-stu-id="d41f2-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="d41f2-129">nome da saudação deve começar com uma letra ou um número e não pode conter caracteres especiais diferentes de "-" e "_".</span><span class="sxs-lookup"><span data-stu-id="d41f2-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="d41f2-130">Em Olá **como tooRun** caixa, escolha **executados sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="d41f2-131">Em Olá **carregamento de arquivo** , clique o ícone de pasta hello e procurar toohello arquivo. zip que contém o script.</span><span class="sxs-lookup"><span data-stu-id="d41f2-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="d41f2-132">arquivo zip de saudação deve conter o executável (.exe. cmd. bat. sh. php. py. js), bem como quaisquer arquivos de suporte necessários toorun Olá programa ou script.</span><span class="sxs-lookup"><span data-stu-id="d41f2-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="d41f2-133">Verificar **criar** tooupload Olá script tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="d41f2-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="d41f2-134">Olá nome especificado para Olá WebJob aparece na lista Olá Olá **WebJobs** folha.</span><span class="sxs-lookup"><span data-stu-id="d41f2-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="d41f2-135">Olá toorun WebJob, clique o nome na lista de saudação e clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Executar o Trabalho Web](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="d41f2-137"><a name="CreateContinuous"></a>Criar um Trabalho Web em execução contínua</span><span class="sxs-lookup"><span data-stu-id="d41f2-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="d41f2-138">toocreate um WebJob de execução contínua, siga Olá mesmas etapas para criar um trabalho Web que é executado uma vez, mas em Olá **como tooRun** caixa, escolha **contínuo**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="d41f2-139">toostart ou parar um trabalho Web contínuo, clique com botão direito Olá WebJob na lista de saudação e clique em **iniciar** ou **parar**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="d41f2-140">Se seu aplicativo Web for executado em mais de uma instância, um Trabalho Web em execução contínua será executado em todas as suas instâncias.</span><span class="sxs-lookup"><span data-stu-id="d41f2-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="d41f2-141">Trabalhos Web agendados e sob demanda são executados em uma única instância selecionada para o balanceamento de carga pelo Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d41f2-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="d41f2-142">Para trabalhos Web contínuos toorun confiável e em todas as instâncias, habilitar Olá AlwaysOn * configuração Olá aplicativo web caso contrário, eles podem interromper a execução quando o site de host SCM Olá ficar ocioso por muito tempo.</span><span class="sxs-lookup"><span data-stu-id="d41f2-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="d41f2-143"><a name="CreateScheduledCRON"></a>Criar um WebJob agendado usando uma expressão CRON</span><span class="sxs-lookup"><span data-stu-id="d41f2-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="d41f2-144">Essa técnica é tooWeb disponíveis aplicativos em execução no modo básico, Standard ou Premium e requer Olá **AlwaysOn** configuração toobe habilitado no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="d41f2-145">tooturn um WebJob na demanda em um trabalho Web agendado, basta incluir um `settings.job` arquivo na raiz de saudação do arquivo zip WebJob.</span><span class="sxs-lookup"><span data-stu-id="d41f2-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="d41f2-146">Esse arquivo JSON deve incluir uma propriedade `schedule` com uma [expressão CRON](https://en.wikipedia.org/wiki/Cron), como mostrado no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="d41f2-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="d41f2-147">Olá expressão CRON é composto de 6 campos: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="d41f2-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="d41f2-148">Por exemplo, tootrigger seu trabalho Web a cada 15 minutos, o `settings.job` teria:</span><span class="sxs-lookup"><span data-stu-id="d41f2-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="d41f2-149">Outros exemplos de agendamento CRON:</span><span class="sxs-lookup"><span data-stu-id="d41f2-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="d41f2-150">Cada hora (ou seja, sempre que a contagem de saudação de minutos é 0):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="d41f2-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="d41f2-151">Cada hora de too5 9: 00 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="d41f2-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="d41f2-152">Às 9h30 todos os dias: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="d41f2-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="d41f2-153">Às 9h30 todos os dias de semana: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="d41f2-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="d41f2-154">**Observação**: ao implantar um trabalho Web do Visual Studio, verifique se toomark seu `settings.job` propriedades de arquivo como 'Copiar se mais recente'.</span><span class="sxs-lookup"><span data-stu-id="d41f2-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="d41f2-155"><a name="CreateScheduled"></a>Criar um WebJob agendado usando Olá Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="d41f2-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="d41f2-156">Olá técnica alternativa a seguir faz uso de saudação do Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="d41f2-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="d41f2-157">Nesse caso, seu trabalho Web não tem qualquer conhecimento direto da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="d41f2-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="d41f2-158">Em vez disso, Olá Agendador do Azure obtém tootrigger configurado seu trabalho Web em um agendamento.</span><span class="sxs-lookup"><span data-stu-id="d41f2-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="d41f2-159">Olá Portal do Azure ainda não tiver Olá capacidade toocreate um trabalho Web agendado, mas até que esse recurso seja adicionado você pode fazer isso usando Olá [portal clássico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d41f2-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="d41f2-160">Em Olá [portal clássico](http://manage.windowsazure.com) toohello WebJob página e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="d41f2-161">Em Olá **como tooRun** caixa, escolha **executados em um agendamento**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Novo trabalho agendado][NewScheduledJob]
3. <span data-ttu-id="d41f2-163">Escolha Olá **região Agendador** para seu trabalho e, em seguida, clique em seta Olá Olá canto direito inferior da tela do diálogo tooproceed toohello próxima hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="d41f2-164">Em Olá **criar trabalho de** caixa de diálogo, escolha o tipo de saudação do **recorrência** desejado: **trabalho único** ou **trabalho recorrente**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Agendar recorrência][SchdRecurrence]
5. <span data-ttu-id="d41f2-166">Escolha também uma hora **Inicial**: **Agora** ou **Em uma hora específica**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Agendar hora inicial][SchdStart]
6. <span data-ttu-id="d41f2-168">Se você quiser toostart em um momento específico, escolha os valores de tempo inicial em **iniciando em**.</span><span class="sxs-lookup"><span data-stu-id="d41f2-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Agendar o início em uma hora específica][SchdStartOn]
7. <span data-ttu-id="d41f2-170">Se você escolher um trabalho recorrente, você terá Olá **repetir cada** opção toospecify Olá frequência de ocorrência e Olá **terminando em** opção toospecify uma hora de término.</span><span class="sxs-lookup"><span data-stu-id="d41f2-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Agendar recorrência][SchdRecurEvery]
8. <span data-ttu-id="d41f2-172">Se você escolher **semanas**, você pode selecionar Olá **em uma agenda específica** caixa e especifique dias Olá da semana Olá que você deseja Olá toorun de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d41f2-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Dias de agendamento da saudação semana][SchdWeeksOnParticular]
9. <span data-ttu-id="d41f2-174">Se você escolher **meses** e selecione hello **em uma agenda específica** caixa, você pode definir Olá trabalho toorun em determinada numerada **dias** no mês de saudação.</span><span class="sxs-lookup"><span data-stu-id="d41f2-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Agendar determinado de datas no mês de saudação][SchdMonthsOnPartDays]
10. <span data-ttu-id="d41f2-176">Se você escolher **dias da semana**, você pode selecionar qual dia ou dias da semana Olá no mês de saudação desejado Olá toorun de trabalho no.</span><span class="sxs-lookup"><span data-stu-id="d41f2-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Agendar dias da semana específicos em um mês][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="d41f2-178">Por fim, você também pode usar Olá **ocorrências** toochoose opção qual semana do mês de saudação (primeiro, segundo, terceiro etc) deseja Olá trabalho toorun em Olá dias da semana especificado.</span><span class="sxs-lookup"><span data-stu-id="d41f2-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Agendar dias da semana específicos em semanas específicas em um mês][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="d41f2-180">Depois de criar um ou mais trabalhos, seus nomes serão exibidos na guia de WebJobs Olá com seu status, tipo de agenda e outras informações.</span><span class="sxs-lookup"><span data-stu-id="d41f2-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="d41f2-181">Informações de histórico para Olá últimos 30 WebJobs são mantidas.</span><span class="sxs-lookup"><span data-stu-id="d41f2-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Lista de trabalhos][WebJobsListWithSeveralJobs]

### <span data-ttu-id="d41f2-183"><a name="Scheduler"></a>Trabalhos agendados e o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="d41f2-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="d41f2-184">Trabalhos agendados também podem ser configurados nas páginas de Agendador do Azure de saudação do hello [portal clássico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d41f2-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="d41f2-185">Na página de trabalhos Web hello, clique em do trabalho Olá **agenda** página de portal do link toonavigate toohello Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="d41f2-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Link tooAzure Agendador][LinkToScheduler]
2. <span data-ttu-id="d41f2-187">Na página do Agendador hello, clique em trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Trabalho na página de portal saudação do Agendador][SchedulerPortal]
3. <span data-ttu-id="d41f2-189">Olá **ação do trabalho** página é aberta, onde você pode configurar adicionalmente trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Ação de trabalho PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="d41f2-191"><a name="ViewJobHistory"></a>Exibir histórico de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="d41f2-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="d41f2-192">histórico de execução de saudação tooview de um trabalho, inclusive os trabalhos criados com hello SDK do WebJobs, clique no link correspondente em Olá **Logs** coluna da folha de WebJobs hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="d41f2-193">(Você pode usar saudação da área de transferência ícone toocopy Olá URL da área de transferência do hello log arquivo página toohello se desejar.)</span><span class="sxs-lookup"><span data-stu-id="d41f2-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Link Logs](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="d41f2-195">Clicar em links de saudação abre a página de detalhes de saudação para Olá WebJob.</span><span class="sxs-lookup"><span data-stu-id="d41f2-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="d41f2-196">Esta página mostra Olá nome da execução do comando hello, Olá últimas vezes em que ele foi executado, e seu êxito ou falha.</span><span class="sxs-lookup"><span data-stu-id="d41f2-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="d41f2-197">Em **execuções recentes do trabalho**, clique em um detalhes adicionais de toosee de tempo.</span><span class="sxs-lookup"><span data-stu-id="d41f2-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="d41f2-199">Olá **detalhes da execução do WebJob** página será exibida.</span><span class="sxs-lookup"><span data-stu-id="d41f2-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="d41f2-200">Clique em **alternar saída** toosee texto de saudação do conteúdo do log hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="d41f2-201">log de saída de Hello está no formato de texto.</span><span class="sxs-lookup"><span data-stu-id="d41f2-201">hello output log is in text format.</span></span> 
   
    ![Detalhes da execução do trabalho Web][WebJobRunDetails]
4. <span data-ttu-id="d41f2-203">texto de saída de hello toosee em uma janela separada do navegador, clique em Olá **baixar** link.</span><span class="sxs-lookup"><span data-stu-id="d41f2-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="d41f2-204">texto de saudação toodownload em si, clique o link hello e usar o conteúdo do arquivo de navegador opções toosave hello.</span><span class="sxs-lookup"><span data-stu-id="d41f2-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Baixar saída do log][DownloadLogOutput]
5. <span data-ttu-id="d41f2-206">Olá **WebJobs** link na parte superior de saudação da página Olá fornece uma lista de tooa de tooget de maneira conveniente de WebJobs no painel de histórico de saudação.</span><span class="sxs-lookup"><span data-stu-id="d41f2-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Lista de tooWebJobs de link][WebJobsLinkToDashboardList]
   
    ![Lista de Trabalhos Web no painel de histórico][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="d41f2-209">Clicando em um desses links usa página de detalhes do trabalho Web toohello para trabalho Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="d41f2-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="d41f2-210"><a name="WHPNotes"></a>Observações</span><span class="sxs-lookup"><span data-stu-id="d41f2-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="d41f2-211">Aplicativos Web no modo gratuito podem atingir o tempo limite após 20 minutos, se não há nenhum site de scm (implantação) toohello solicitações e portal do aplicativo da web de saudação não está aberto no Azure.</span><span class="sxs-lookup"><span data-stu-id="d41f2-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="d41f2-212">Site real de toohello solicitações não redefinirá a isso.</span><span class="sxs-lookup"><span data-stu-id="d41f2-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="d41f2-213">Código para um trabalho contínuo precisa toobe gravado toorun em um loop infinito.</span><span class="sxs-lookup"><span data-stu-id="d41f2-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="d41f2-214">Trabalhos contínuos são executados continuamente somente quando o aplicativo de web hello está ativo.</span><span class="sxs-lookup"><span data-stu-id="d41f2-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="d41f2-215">Básico e padrão modos oferta hello sempre no recurso que, quando ativada, impede que os aplicativos web se tornam ociosos.</span><span class="sxs-lookup"><span data-stu-id="d41f2-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="d41f2-216">Só é possível depurar continuamente os Trabalhos Web em execução.</span><span class="sxs-lookup"><span data-stu-id="d41f2-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="d41f2-217">Não há suporte para a depuração Trabalhos Web agendados ou sob demanda.</span><span class="sxs-lookup"><span data-stu-id="d41f2-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="d41f2-218"><a name="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d41f2-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d41f2-219">Para saber mais, confira [Recursos de documentação do Azure WebJobs][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="d41f2-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

