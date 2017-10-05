---
title: Executar tarefas em segundo plano com Trabalhos Web
description: Saiba como executar tarefas em segundo plano em aplicativos Web do Azure.
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="9dffa-103">Executar tarefas em segundo plano com Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="9dffa-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="9dffa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9dffa-104">Overview</span></span>
<span data-ttu-id="9dffa-105">Você pode executar programas ou scripts em WebJobs em seu aplicativo Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) de três maneiras: sob demanda, continuamente ou com base em uma agenda.</span><span class="sxs-lookup"><span data-stu-id="9dffa-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="9dffa-106">Não há nenhum custo adicional para usar Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="9dffa-107">Este artigo mostra como implantar Trabalhos Web utilizando o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9dffa-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="9dffa-108">Para obter informações sobre como implantar utilizando o Visual Studio ou um processo de entrega contínua, consulte [Como implantar Trabalhos Web do Azure em Aplicativos Web](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="9dffa-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="9dffa-109">O SDK de Trabalhos Web do Azure simplifica muitas tarefas de programação de Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="9dffa-110">Para obter mais informações, consulte [O que é o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9dffa-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="9dffa-111">O Azure Functions oferece outra maneira de executar programas e scripts de um ambiente sem servidor ou de um aplicativo do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dffa-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="9dffa-112">Para saber mais, consulte [Visão geral do Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dffa-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="9dffa-113"><a name="acceptablefiles"></a>Tipos de arquivo aceitáveis para scripts ou programas</span><span class="sxs-lookup"><span data-stu-id="9dffa-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="9dffa-114">Os seguintes tipos de arquivo são aceitos:</span><span class="sxs-lookup"><span data-stu-id="9dffa-114">The following file types are accepted:</span></span>

* <span data-ttu-id="9dffa-115">.cmd, .bat, .exe (usando o cmd do Windows)</span><span class="sxs-lookup"><span data-stu-id="9dffa-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="9dffa-116">.ps1 (usando o PowerShell)</span><span class="sxs-lookup"><span data-stu-id="9dffa-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="9dffa-117">.sh (usando bash)</span><span class="sxs-lookup"><span data-stu-id="9dffa-117">.sh (using bash)</span></span>
* <span data-ttu-id="9dffa-118">.php (usando php)</span><span class="sxs-lookup"><span data-stu-id="9dffa-118">.php (using php)</span></span>
* <span data-ttu-id="9dffa-119">.py (usando o python)</span><span class="sxs-lookup"><span data-stu-id="9dffa-119">.py (using python)</span></span>
* <span data-ttu-id="9dffa-120">.js (usando nó)</span><span class="sxs-lookup"><span data-stu-id="9dffa-120">.js (using node)</span></span>
* <span data-ttu-id="9dffa-121">.jar (usando java)</span><span class="sxs-lookup"><span data-stu-id="9dffa-121">.jar (using java)</span></span>

## <span data-ttu-id="9dffa-122"><a name="CreateOnDemand"></a>Criar um Trabalho Web sob demanda no portal</span><span class="sxs-lookup"><span data-stu-id="9dffa-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="9dffa-123">Na folha **Aplicativo Web** do [Portal do Azure](https://portal.azure.com), clique em **Todas as configurações > Trabalhos Web** para mostrar a folha **Trabalhos Web**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Lâmina do Trabalho Web](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="9dffa-125">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-125">Click **Add**.</span></span> <span data-ttu-id="9dffa-126">A caixa de diálogo **Adicionar Trabalho Web** aparece.</span><span class="sxs-lookup"><span data-stu-id="9dffa-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Adicionar lâmina do Trabalho Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="9dffa-128">Em **Nome**, forneça um nome para o Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="9dffa-129">O nome deve começar com uma letra ou um número e não pode conter caracteres especiais além de "-" e "_".</span><span class="sxs-lookup"><span data-stu-id="9dffa-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="9dffa-130">Na caixa **Como Executar**, escolha **Executar sob Demanda**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="9dffa-131">Na caixa **Carregamento de Arquivo** , clique no ícone de pasta e navegue até o arquivo zip que contém o script.</span><span class="sxs-lookup"><span data-stu-id="9dffa-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="9dffa-132">O arquivo zip deve conter o executável (.exe, .cmd, .bat, .sh, .php, .py, .js), bem como os arquivos de suporte necessários para executar o script ou o programa.</span><span class="sxs-lookup"><span data-stu-id="9dffa-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="9dffa-133">Marque **Criar** para carregar o script em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="9dffa-134">O nome especificado para o Trabalho Web é exibido na lista da folha **Trabalhos Web** .</span><span class="sxs-lookup"><span data-stu-id="9dffa-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="9dffa-135">Para executar o Trabalho Web, clique com o botão direito do mouse em seu nome na lista e clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Executar o Trabalho Web](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="9dffa-137"><a name="CreateContinuous"></a>Criar um Trabalho Web em execução contínua</span><span class="sxs-lookup"><span data-stu-id="9dffa-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="9dffa-138">Para criar um Trabalho Web em execução contínua, siga as mesmas etapas para criar um Trabalho Web que é executado uma vez, mas, na caixa **Como Executar**, escolha **Contínuo**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="9dffa-139">Para iniciar ou interromper um Trabalho Web contínuo, clique com o botão direito do mouse no Trabalho Web na lista e clique em **Iniciar** ou **Parar**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="9dffa-140">Se seu aplicativo Web for executado em mais de uma instância, um Trabalho Web em execução contínua será executado em todas as suas instâncias.</span><span class="sxs-lookup"><span data-stu-id="9dffa-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="9dffa-141">Trabalhos Web agendados e sob demanda são executados em uma única instância selecionada para o balanceamento de carga pelo Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9dffa-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="9dffa-142">Para que WebJobs contínuos sejam executados de forma confiável e em todas as instâncias, ative a configuração Sempre Ativado* para o aplicativo Web, caso contrário, ele poderá interromper a execução quando o site de host do SCM ficar ocioso por muito tempo.</span><span class="sxs-lookup"><span data-stu-id="9dffa-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="9dffa-143"><a name="CreateScheduledCRON"></a>Criar um WebJob agendado usando uma expressão CRON</span><span class="sxs-lookup"><span data-stu-id="9dffa-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="9dffa-144">Essa técnica está disponível para aplicativos Web em execução no modo Básico, Standard ou Premium e exige que a configuração **Sempre Ativado** esteja habilitada no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dffa-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="9dffa-145">Para transformar um Trabalho Web Sob Demanda em um Trabalho Web agendado, basta incluir um arquivo `settings.job` na raiz do arquivo .zip do Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="9dffa-146">Esse arquivo JSON deve incluir uma propriedade `schedule` com uma [expressão CRON](https://en.wikipedia.org/wiki/Cron), como mostrado no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="9dffa-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="9dffa-147">A expressão CRON é composta por 6 campos: `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="9dffa-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="9dffa-148">Por exemplo, para disparar o WebJob a cada 15 minutos, o `settings.job` teria:</span><span class="sxs-lookup"><span data-stu-id="9dffa-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="9dffa-149">Outros exemplos de agendamento CRON:</span><span class="sxs-lookup"><span data-stu-id="9dffa-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="9dffa-150">A cada hora (ou seja, sempre que a contagem de minutos for 0): `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="9dffa-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="9dffa-151">A cada hora entre 9h e 17h: `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="9dffa-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="9dffa-152">Às 9h30 todos os dias: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="9dffa-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="9dffa-153">Às 9h30 todos os dias de semana: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="9dffa-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="9dffa-154">**Observação**: ao implantar um Trabalho Web do Visual Studio, certifique-se de marcar as propriedades do arquivo `settings.job` como "Copiar se mais recente".</span><span class="sxs-lookup"><span data-stu-id="9dffa-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="9dffa-155"><a name="CreateScheduled"></a>Criar um Trabalho Web agendado usando o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="9dffa-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="9dffa-156">A técnica alternativa a seguir utiliza o Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dffa-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="9dffa-157">Nesse caso, seu Trabalho Web não tem nenhum conhecimento direto do agendamento.</span><span class="sxs-lookup"><span data-stu-id="9dffa-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="9dffa-158">Em vez disso, o Agendador do Azure é configurado para disparar o Trabalho Web em um agendamento.</span><span class="sxs-lookup"><span data-stu-id="9dffa-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="9dffa-159">O Portal do Azure ainda não tem a capacidade de criar um Trabalho Web agendado, mas até que esse recurso seja adicionado você pode fazê-lo usando o [portal clássico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9dffa-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="9dffa-160">No [portal clássico](http://manage.windowsazure.com) vá até a página do Trabalho Web e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="9dffa-161">Na caixa **Como Executar**, escolha **Executar em um agendamento**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Novo trabalho agendado][NewScheduledJob]
3. <span data-ttu-id="9dffa-163">Escolha a **Região do Agendador** para seu trabalho e, em seguida, clique na seta na parte inferior direita da caixa de diálogo para prosseguir para a próxima tela.</span><span class="sxs-lookup"><span data-stu-id="9dffa-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="9dffa-164">Na caixa de diálogo **Criar Trabalho**, escolha o tipo de **Recorrência** desejado: **Trabalho único** ou **Trabalho recorrente**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Agendar recorrência][SchdRecurrence]
5. <span data-ttu-id="9dffa-166">Escolha também uma hora **Inicial**: **Agora** ou **Em uma hora específica**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Agendar hora inicial][SchdStart]
6. <span data-ttu-id="9dffa-168">Se desejar iniciar em uma hora específica, escolha os valores da hora inicial em **Início em**.</span><span class="sxs-lookup"><span data-stu-id="9dffa-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Agendar o início em uma hora específica][SchdStartOn]
7. <span data-ttu-id="9dffa-170">Se escolher um trabalho recorrente, você tem a opção **Repetir a Cada** para especificar a frequência de ocorrência e a opção **Término em** para especificar uma hora de término.</span><span class="sxs-lookup"><span data-stu-id="9dffa-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Agendar recorrência][SchdRecurEvery]
8. <span data-ttu-id="9dffa-172">Se escolher **Semanas**, você poderá selecionar a caixa **Em uma agenda específica** e especificar os dias da semana em que deseja que o trabalho seja executado.</span><span class="sxs-lookup"><span data-stu-id="9dffa-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Agendar em dias da semana][SchdWeeksOnParticular]
9. <span data-ttu-id="9dffa-174">Se você escolher **Meses** e selecionar a caixa **Em uma Agenda Específica**, poderá definir o trabalho a ser executado em um determinado número de **Dias** do mês.</span><span class="sxs-lookup"><span data-stu-id="9dffa-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Agendar datas específicas no mês][SchdMonthsOnPartDays]
10. <span data-ttu-id="9dffa-176">Se você escolher **Dias da Semana**, poderá selecionar em qual dia ou dias da semana no mês deseja que o trabalho seja executado.</span><span class="sxs-lookup"><span data-stu-id="9dffa-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Agendar dias da semana específicos em um mês][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="9dffa-178">Finalmente, você também pode usar a opção **Ocorrências** para escolher em qual semana do mês (primeira, segunda, terceira etc.) deseja que o trabalho seja executado nos dias da semana especificados.</span><span class="sxs-lookup"><span data-stu-id="9dffa-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Agendar dias da semana específicos em semanas específicas em um mês][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="9dffa-180">Depois que você tiver criado um ou mais trabalhos, os nomes serão exibidos na guia Trabalhos Web com status, tipo de cronograma e outras informações.</span><span class="sxs-lookup"><span data-stu-id="9dffa-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="9dffa-181">As informações de histórico dos 30 últimos Trabalhos Web são mantidas.</span><span class="sxs-lookup"><span data-stu-id="9dffa-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Lista de trabalhos][WebJobsListWithSeveralJobs]

### <span data-ttu-id="9dffa-183"><a name="Scheduler"></a>Trabalhos agendados e o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="9dffa-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="9dffa-184">Os trabalhos agendados podem ser configurados mais detalhadamente nas páginas do Agendador do Azure do [portal clássico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9dffa-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="9dffa-185">Na página Trabalhos Web, clique no link **cronograma** do trabalho para navegar até a página do portal do Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dffa-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Link para Agendador do Azure][LinkToScheduler]
2. <span data-ttu-id="9dffa-187">Na página do Agendador, clique no trabalho.</span><span class="sxs-lookup"><span data-stu-id="9dffa-187">On the Scheduler page, click the job.</span></span>
   
    ![Trabalho na página do portal do Agendador][SchedulerPortal]
3. <span data-ttu-id="9dffa-189">A página **Ação de Trabalho** é aberta, para que você possa configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="9dffa-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Ação de trabalho PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="9dffa-191"><a name="ViewJobHistory"></a>Exibir o histórico do trabalho</span><span class="sxs-lookup"><span data-stu-id="9dffa-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="9dffa-192">Para exibir o histórico de execução de um trabalho, incluindo trabalhos criados com o SDK de Trabalhos Web, clique no link correspondente na coluna **Logs** da folha Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="9dffa-193">(Se quiser, você poderá usar o ícone da área de transferência para copiar a URL da página do arquivo de log para a área de transferência.)</span><span class="sxs-lookup"><span data-stu-id="9dffa-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Link Logs](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="9dffa-195">Clicar no link abre a página de detalhes para o Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="9dffa-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="9dffa-196">Esta página mostra o nome do comando executado, os horários das execuções mais recentes, além do sucesso ou da falha.</span><span class="sxs-lookup"><span data-stu-id="9dffa-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="9dffa-197">Em **Execuções de trabalho recentes**, clique em uma hora para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9dffa-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="9dffa-199">A página **Detalhes da Execução do Trabalho Web** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9dffa-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="9dffa-200">Clique em **Alternar Saída** para ver o texto do conteúdo do log.</span><span class="sxs-lookup"><span data-stu-id="9dffa-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="9dffa-201">O log de saída está em formato de texto.</span><span class="sxs-lookup"><span data-stu-id="9dffa-201">The output log is in text format.</span></span> 
   
    ![Detalhes da execução do trabalho Web][WebJobRunDetails]
4. <span data-ttu-id="9dffa-203">Para ver o texto de saída em uma janela separada do navegador, clique no link **download** .</span><span class="sxs-lookup"><span data-stu-id="9dffa-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="9dffa-204">Para baixar o texto propriamente dito, com o botão direito do mouse no link e use as opções do navegador para salvar o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9dffa-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Baixar saída do log][DownloadLogOutput]
5. <span data-ttu-id="9dffa-206">O link **Trabalhos Web** na parte superior da página oferece uma maneira prática de obter a uma lista de Trabalhos Web no painel de histórico.</span><span class="sxs-lookup"><span data-stu-id="9dffa-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Vincular à lista de Trabalhos Web][WebJobsLinkToDashboardList]
   
    ![Lista de Trabalhos Web no painel de histórico][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="9dffa-209">O clique em um desses links leva você até a página Detalhes do Trabalho Web do trabalho selecionado.</span><span class="sxs-lookup"><span data-stu-id="9dffa-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="9dffa-210"><a name="WHPNotes"></a>Observações</span><span class="sxs-lookup"><span data-stu-id="9dffa-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="9dffa-211">Os aplicativos Web no modo Gratuito podem atingir tempo limite depois de 20 minutos se não houver solicitações para o site do scm (implantação) e o portal do aplicativo Web não estiver aberto no Azure.</span><span class="sxs-lookup"><span data-stu-id="9dffa-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="9dffa-212">As solicitações para o site real não redefinirão isso.</span><span class="sxs-lookup"><span data-stu-id="9dffa-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="9dffa-213">O código para um trabalho contínuo precisa ser escrito para ser executado em um loop infinito.</span><span class="sxs-lookup"><span data-stu-id="9dffa-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="9dffa-214">Trabalhos contínuos só são executados continuamente quando o aplicativo Web estiver funcionando.</span><span class="sxs-lookup"><span data-stu-id="9dffa-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="9dffa-215">Os modos Básico e Padrão oferecem o recurso Sempre Ativo que, quando habilitado, evita que os aplicativos Web fiquem ociosos.</span><span class="sxs-lookup"><span data-stu-id="9dffa-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="9dffa-216">Só é possível depurar continuamente os Trabalhos Web em execução.</span><span class="sxs-lookup"><span data-stu-id="9dffa-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="9dffa-217">Não há suporte para a depuração Trabalhos Web agendados ou sob demanda.</span><span class="sxs-lookup"><span data-stu-id="9dffa-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="9dffa-218"><a name="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dffa-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="9dffa-219">Para saber mais, confira [Recursos de documentação do Azure WebJobs][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="9dffa-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

