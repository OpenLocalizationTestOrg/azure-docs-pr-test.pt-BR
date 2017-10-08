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
# <a name="run-background-tasks-with-webjobs"></a>Executar tarefas em segundo plano com Trabalhos Web
## <a name="overview"></a>Visão geral
Você pode executar programas ou scripts em WebJobs em seu aplicativo Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) de três maneiras: sob demanda, continuamente ou com base em uma agenda. Não há nenhum custo adicional de toouse WebJobs.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Este artigo mostra como toodeploy WebJobs usando Olá [Portal do Azure](https://portal.azure.com). Para obter informações sobre como toodeploy usando o Visual Studio ou um processo de entrega contínua, consulte [como tooDeploy do Azure WebJobs tooWeb aplicativos](websites-dotnet-deploy-webjobs.md).

Olá SDK do Azure WebJobs simplifica muitas tarefas de programação dos WebJobs. Para obter mais informações, consulte [novidades Olá SDK do WebJobs](websites-dotnet-webjobs-sdk.md).

 As funções do Azure fornece outra maneira como os programas toorun e scripts de um ambiente sem servidor ou de um aplicativo de serviço de aplicativo. Para saber mais, consulte [Visão geral do Azure Functions](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Tipos de arquivo aceitáveis para scripts ou programas
Olá, tipos de arquivo a seguir é aceitas:

* .cmd, .bat, .exe (usando o cmd do Windows)
* .ps1 (usando o PowerShell)
* .sh (usando bash)
* .php (usando php)
* .py (usando o python)
* .js (usando nó)
* .jar (usando java)

## <a name="CreateOnDemand"></a>Criar um relatório sob demanda WebJob no portal de saudação
1. Em Olá **aplicativo Web** folha de saudação [Portal do Azure](https://portal.azure.com), clique em **todas as configurações > WebJobs** tooshow Olá **WebJobs** folha.
   
    ![Lâmina do Trabalho Web](./media/web-sites-create-web-jobs/wjblade.png)
2. Clique em **Adicionar**. Olá **WebJob adicionar** caixa de diálogo é exibida.
   
    ![Adicionar lâmina do Trabalho Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. Em **nome**, forneça um nome para Olá WebJob. nome da saudação deve começar com uma letra ou um número e não pode conter caracteres especiais diferentes de "-" e "_".
4. Em Olá **como tooRun** caixa, escolha **executados sob demanda**.
5. Em Olá **carregamento de arquivo** , clique o ícone de pasta hello e procurar toohello arquivo. zip que contém o script. arquivo zip de saudação deve conter o executável (.exe. cmd. bat. sh. php. py. js), bem como quaisquer arquivos de suporte necessários toorun Olá programa ou script.
6. Verificar **criar** tooupload Olá script tooyour web app. 
   
    Olá nome especificado para Olá WebJob aparece na lista Olá Olá **WebJobs** folha.
7. Olá toorun WebJob, clique o nome na lista de saudação e clique em **executar**.
   
    ![Executar o Trabalho Web](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Criar um Trabalho Web em execução contínua
1. toocreate um WebJob de execução contínua, siga Olá mesmas etapas para criar um trabalho Web que é executado uma vez, mas em Olá **como tooRun** caixa, escolha **contínuo**.
2. toostart ou parar um trabalho Web contínuo, clique com botão direito Olá WebJob na lista de saudação e clique em **iniciar** ou **parar**.

> [!NOTE]
> Se seu aplicativo Web for executado em mais de uma instância, um Trabalho Web em execução contínua será executado em todas as suas instâncias. Trabalhos Web agendados e sob demanda são executados em uma única instância selecionada para o balanceamento de carga pelo Microsoft Azure.
> 
> Para trabalhos Web contínuos toorun confiável e em todas as instâncias, habilitar Olá AlwaysOn * configuração Olá aplicativo web caso contrário, eles podem interromper a execução quando o site de host SCM Olá ficar ocioso por muito tempo.
> 
> 

## <a name="CreateScheduledCRON"></a>Criar um WebJob agendado usando uma expressão CRON
Essa técnica é tooWeb disponíveis aplicativos em execução no modo básico, Standard ou Premium e requer Olá **AlwaysOn** configuração toobe habilitado no aplicativo hello.

tooturn um WebJob na demanda em um trabalho Web agendado, basta incluir um `settings.job` arquivo na raiz de saudação do arquivo zip WebJob. Esse arquivo JSON deve incluir uma propriedade `schedule` com uma [expressão CRON](https://en.wikipedia.org/wiki/Cron), como mostrado no exemplo abaixo.

Olá expressão CRON é composto de 6 campos: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Por exemplo, tootrigger seu trabalho Web a cada 15 minutos, o `settings.job` teria:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Outros exemplos de agendamento CRON:

* Cada hora (ou seja, sempre que a contagem de saudação de minutos é 0):`0 0 * * * *` 
* Cada hora de too5 9: 00 PM:`0 0 9-17 * * *` 
* Às 9h30 todos os dias: `0 30 9 * * *`
* Às 9h30 todos os dias de semana: `0 30 9 * * 1-5`

**Observação**: ao implantar um trabalho Web do Visual Studio, verifique se toomark seu `settings.job` propriedades de arquivo como 'Copiar se mais recente'.

## <a name="CreateScheduled"></a>Criar um WebJob agendado usando Olá Agendador do Azure
Olá técnica alternativa a seguir faz uso de saudação do Agendador do Azure. Nesse caso, seu trabalho Web não tem qualquer conhecimento direto da agenda de saudação. Em vez disso, Olá Agendador do Azure obtém tootrigger configurado seu trabalho Web em um agendamento. 

Olá Portal do Azure ainda não tiver Olá capacidade toocreate um trabalho Web agendado, mas até que esse recurso seja adicionado você pode fazer isso usando Olá [portal clássico](http://manage.windowsazure.com).

1. Em Olá [portal clássico](http://manage.windowsazure.com) toohello WebJob página e clique em **adicionar**.
2. Em Olá **como tooRun** caixa, escolha **executados em um agendamento**.
   
    ![Novo trabalho agendado][NewScheduledJob]
3. Escolha Olá **região Agendador** para seu trabalho e, em seguida, clique em seta Olá Olá canto direito inferior da tela do diálogo tooproceed toohello próxima hello.
4. Em Olá **criar trabalho de** caixa de diálogo, escolha o tipo de saudação do **recorrência** desejado: **trabalho único** ou **trabalho recorrente**.
   
    ![Agendar recorrência][SchdRecurrence]
5. Escolha também uma hora **Inicial**: **Agora** ou **Em uma hora específica**.
   
    ![Agendar hora inicial][SchdStart]
6. Se você quiser toostart em um momento específico, escolha os valores de tempo inicial em **iniciando em**.
   
    ![Agendar o início em uma hora específica][SchdStartOn]
7. Se você escolher um trabalho recorrente, você terá Olá **repetir cada** opção toospecify Olá frequência de ocorrência e Olá **terminando em** opção toospecify uma hora de término.
   
    ![Agendar recorrência][SchdRecurEvery]
8. Se você escolher **semanas**, você pode selecionar Olá **em uma agenda específica** caixa e especifique dias Olá da semana Olá que você deseja Olá toorun de trabalho.
   
    ![Dias de agendamento da saudação semana][SchdWeeksOnParticular]
9. Se você escolher **meses** e selecione hello **em uma agenda específica** caixa, você pode definir Olá trabalho toorun em determinada numerada **dias** no mês de saudação. 
   
    ![Agendar determinado de datas no mês de saudação][SchdMonthsOnPartDays]
10. Se você escolher **dias da semana**, você pode selecionar qual dia ou dias da semana Olá no mês de saudação desejado Olá toorun de trabalho no.
    
     ![Agendar dias da semana específicos em um mês][SchdMonthsOnPartWeekDays]
11. Por fim, você também pode usar Olá **ocorrências** toochoose opção qual semana do mês de saudação (primeiro, segundo, terceiro etc) deseja Olá trabalho toorun em Olá dias da semana especificado.
    
    ![Agendar dias da semana específicos em semanas específicas em um mês][SchdMonthsOnPartWeekDaysOccurences]
12. Depois de criar um ou mais trabalhos, seus nomes serão exibidos na guia de WebJobs Olá com seu status, tipo de agenda e outras informações. Informações de histórico para Olá últimos 30 WebJobs são mantidas.
    
    ![Lista de trabalhos][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Trabalhos agendados e o Agendador do Azure
Trabalhos agendados também podem ser configurados nas páginas de Agendador do Azure de saudação do hello [portal clássico](http://manage.windowsazure.com).

1. Na página de trabalhos Web hello, clique em do trabalho Olá **agenda** página de portal do link toonavigate toohello Agendador do Azure. 
   
   ![Link tooAzure Agendador][LinkToScheduler]
2. Na página do Agendador hello, clique em trabalho hello.
   
    ![Trabalho na página de portal saudação do Agendador][SchedulerPortal]
3. Olá **ação do trabalho** página é aberta, onde você pode configurar adicionalmente trabalho hello. 
   
    ![Ação de trabalho PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Exibir histórico de trabalho Olá
1. histórico de execução de saudação tooview de um trabalho, inclusive os trabalhos criados com hello SDK do WebJobs, clique no link correspondente em Olá **Logs** coluna da folha de WebJobs hello. (Você pode usar saudação da área de transferência ícone toocopy Olá URL da área de transferência do hello log arquivo página toohello se desejar.)
   
    ![Link Logs](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Clicar em links de saudação abre a página de detalhes de saudação para Olá WebJob. Esta página mostra Olá nome da execução do comando hello, Olá últimas vezes em que ele foi executado, e seu êxito ou falha. Em **execuções recentes do trabalho**, clique em um detalhes adicionais de toosee de tempo.
   
    ![WebJobDetails][WebJobDetails]
3. Olá **detalhes da execução do WebJob** página será exibida. Clique em **alternar saída** toosee texto de saudação do conteúdo do log hello. log de saída de Hello está no formato de texto. 
   
    ![Detalhes da execução do trabalho Web][WebJobRunDetails]
4. texto de saída de hello toosee em uma janela separada do navegador, clique em Olá **baixar** link. texto de saudação toodownload em si, clique o link hello e usar o conteúdo do arquivo de navegador opções toosave hello.
   
    ![Baixar saída do log][DownloadLogOutput]
5. Olá **WebJobs** link na parte superior de saudação da página Olá fornece uma lista de tooa de tooget de maneira conveniente de WebJobs no painel de histórico de saudação.
   
    ![Lista de tooWebJobs de link][WebJobsLinkToDashboardList]
   
    ![Lista de Trabalhos Web no painel de histórico][WebJobsListInJobsDashboard]
   
    Clicando em um desses links usa página de detalhes do trabalho Web toohello para trabalho Olá selecionado.

## <a name="WHPNotes"></a>Observações
* Aplicativos Web no modo gratuito podem atingir o tempo limite após 20 minutos, se não há nenhum site de scm (implantação) toohello solicitações e portal do aplicativo da web de saudação não está aberto no Azure. Site real de toohello solicitações não redefinirá a isso.
* Código para um trabalho contínuo precisa toobe gravado toorun em um loop infinito.
* Trabalhos contínuos são executados continuamente somente quando o aplicativo de web hello está ativo.
* Básico e padrão modos oferta hello sempre no recurso que, quando ativada, impede que os aplicativos web se tornam ociosos.
* Só é possível depurar continuamente os Trabalhos Web em execução. Não há suporte para a depuração Trabalhos Web agendados ou sob demanda.

## <a name="NextSteps"></a>Próximas etapas
Para saber mais, confira [Recursos de documentação do Azure WebJobs][WebJobsRecommendedResources].

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

