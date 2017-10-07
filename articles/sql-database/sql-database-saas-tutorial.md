---
title: "aaaDeploy e explore o aplicativo SaaS Wingtip do hello multilocatário que usa o banco de dados do SQL Azure | Microsoft Docs"
description: "Implantar e explore o aplicativo multilocatário Wingtip SaaS hello, que demonstra os padrões de SaaS usando o banco de dados do SQL Azure."
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Implantar e explorar um aplicativo SaaS multilocatário que usa o Banco de dados SQL do Azure

Neste tutorial, você pode implantar e explorar o aplicativo de SaaS Wingtip hello. aplicativo Hello usa um banco de dados-por locatário, padrão de aplicativo SaaS, tooservice vários locatários. aplicativo Hello é projetado tooshowcase recursos do banco de dados do SQL Azure que simplificam habilitar cenários de SaaS.

Olá cinco minutos depois de clicar em *implantar tooAzure* botão abaixo, você tem um aplicativo de SaaS multilocatário, usando o banco de dados SQL, até e em execução na nuvem hello. aplicativo Hello é implantado com três locatários de exemplo, cada qual com seu próprio banco de dados, todos implantado em um pool Elástico do SQL. Olá aplicativo é implantado tooyour assinatura do Azure, fornecendo acesso completo tooexplore e trabalhar com componentes de aplicativos individuais da saudação. scripts de gerenciamento e o código de origem de aplicativos do Hello estão disponíveis em Olá repositório WingtipSaaS GitHub.


Neste tutorial, você aprende:

> [!div class="checklist"]

> * Como toodeploy Olá aplicativo SaaS Wingtip
> * Onde tooget Olá código fonte do aplicativo e scripts de gerenciamento
> * Sobre servidores hello, pools e os bancos de dados que constituem o aplicativo hello
> * Como os locatários são mapeados tootheir dados com hello *catálogo*
> * Como tooprovision um novo locatário
> * Como toomonitor locatário atividade no aplicativo hello

tooexplore vários SaaS design e gerenciamento de padrões, um [série de tutoriais relacionados](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) está disponível que utilizam essa implantação inicial. Ao passar por tutoriais hello, aprofunde-se nos scripts de saudação fornecida e examine como padrões diferentes de SaaS Olá são implementadas. Percorrer os scripts de saudação em cada tutorial toogain uma compreensão mais profunda como tooimplement Olá banco de dados SQL muitos recursos que simplificam o desenvolvimento de aplicativos SaaS.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="deploy-hello-wingtip-saas-application"></a>Implantar o aplicativo de SaaS Wingtip hello

Implante o aplicativo de SaaS Wingtip Olá:

1. Olá clicando em **implantar tooAzure** botão abre o modelo de implantação de SaaS Wingtip Olá toohello portal do Azure. modelo de saudação requer dois valores de parâmetros; um nome para um novo grupo de recursos e um nome de usuário que distingue esta implantação de outras implantações de aplicativo de SaaS Wingtip hello. próxima etapa do Hello fornece detalhes para definir esses valores.

   Verifique se toonote Olá valores exatos que você usar, pois você precisará tooentê-los em uma configuração de arquivo mais tarde.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Insira valores de parâmetros necessários para a implantação de saudação:

    > [!IMPORTANT]
    > Algumas autenticações e firewalls de servidor estão intencionalmente desprotegidos para fins de demonstração. **Criar um novo grupo de recursos** e não usar grupos de recursos, servidores ou pools existentes. Não use este aplicativo ou todos os recursos que cria, para a produção. Excluir este recurso de grupo quando tiver terminado com hello aplicativo toostop relacionados a cobrança.

    * **Grupo de recursos** - selecione **criar novo** e fornecer um **nome** Olá para grupo de recursos. Selecione um **local** da lista suspensa de saudação.
    * **Usuário** - Alguns recursos exigem nomes que são globalmente exclusivos. exclusividade de tooensure, cada vez que você implantar o aplicativo hello fornecer um valor toodifferentiate recursos criar, de recursos criados por qualquer outra implantação de saudação aplicativo Wingtip. É recomendável toouse curto **usuário** nome, como suas iniciais mais um número (por exemplo, *bg1*) e, em seguida, usá-lo no nome do grupo de recursos de saudação (por exemplo, *wingtip-bg1*). O parâmetro **Usuário** só pode conter letras, números e hifens (sem espaços). primeiro e último caractere Hello deve ser uma letra ou um número (todas as minúsculas é recomendado).


1. **Implantar o aplicativo hello**.

    * Clique em tooagree toohello termos e condições.
    * Clique em **Comprar**.

1. Monitorar o status da implantação clicando **notificações** (ícone de sino saudação à direita da caixa de pesquisa de saudação). Implantando aplicativos de SaaS Wingtip Olá leva aproximadamente cinco minutos.

   ![implantação bem-sucedida](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Baixe e desbloquear scripts de SaaS Wingtip Olá

Ao implantar o aplicativo hello, baixe scripts de gerenciamento e o código de origem hello.

> [!IMPORTANT]
> Conteúdos executáveis (scripts, dlls) podem ser bloqueados pelo Windows quando arquivos zip são baixados de uma fonte externa e extraídos. Ao extrair os scripts de saudação de um arquivo zip, siga as etapas de saudação abaixo de arquivo do toounblock hello. zip antes da extração. Isso garante que o script hello pode toorun.

1. Procurar muito[do repositório github Olá Wingtip SaaS](https://github.com/Microsoft/WingtipSaaS).
1. Clique em **Clonar ou baixar**.
1. Clique em **baixar ZIP** e salve o arquivo hello.
1. Saudação de atalho **WingtipSaaS master.zip** de arquivo e selecione **propriedades**.
1. Em Olá **geral** guia, selecione **desbloquear**e clique em **aplicar**.
1. Clique em **OK**.
1. Extraia os arquivos de saudação.

Os scripts estão localizados em Olá *... \\WingtipSaaS mestre\\módulos de aprendizado* pasta.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Arquivo de configuração de saudação de atualização para essa implantação

Antes de executar os scripts, definir Olá *grupo de recursos* e *usuário* valores em **UserConfig.psm1**. Defina essas variáveis toohello valores definidos durante a implantação.

1. Abrir... \\Módulos de aprendizado\\*UserConfig.psm1* em Olá *PowerShell ISE*
1. Atualização *ResourceGroupName* e *nome* com valores específicos de saudação para sua implantação (em linhas 10 e 11 somente).
1. Salve alterações de Olá!

Essa configuração aqui simplesmente evita a necessidade de ter tooupdate esses valores específicos de implantação em cada script.

## <a name="run-hello-application"></a>Executar o aplicativo hello

aplicativo Hello apresenta locais, como corredores conjunto, jazz paus, tem paus, que hospedam os eventos. Locais de registrem como clientes (ou locatários) da plataforma de Wingtip hello, para eventos de toolist um modo fácil e vendem ingressos. Cada local obtém um toomanage de aplicativo da web personalizado e lista os eventos e vender ingressos, independentes e isolados de outros locatários. Sob Olá coberturas, cada locatário obtém um banco de dados SQL implantado em um pool Elástico do SQL.

Um centro **Hub de eventos** fornece uma lista de locatário URLs específicas tooyour implantação.

1. Olá abrir _Hub de eventos_ no navegador da web: http://events.wtp.&lt; USUÁRIO&gt;. trafficmanager.net (Substituir pelo nome de usuário de implantação):

    ![hub de eventos](media/sql-database-saas-tutorial/events-hub.png)

1. Clique em **Fabrikam Jazz Club** no *Hub de Eventos*.

   ![Eventos](./media/sql-database-saas-tutorial/fabrikam.png)


distribuição de saudação toocontrol de solicitações de entrada, Olá aplicativo usa [ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). páginas de eventos Hello, que são específicos de locatário, exigem que os nomes de locatário são incluídos em URLs de saudação. Todos os Olá locatário URLs incluem específicos *usuário* valor e o seguinte formato: http://events.wtp.&lt; USUÁRIO&gt;.trafficmanager.net/*fabrikamjazzclub*. Olá eventos aplicativo analisa o nome do locatário Olá da URL de saudação e usa uma chave tooaccess usando um catálogo de toocreate [ *gerenciamento de mapa do fragmento*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). mapas de catálogo Olá Olá local do banco de dados do locatário toohello chave. Olá **Hub de eventos** usa metadados estendido nome do locatário do hello catálogo tooretrieve Olá associado a cada lista de saudação do banco de dados tooprovide de URLs.

Em um ambiente de produção, você normalmente criaria um registro DNS CNAME para [ *apontar um domínio de internet da empresa* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) para o perfil do Gerenciador de tráfego de saudação.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Iniciar a geração de carga em bancos de dados de locatário de saudação

Agora que hello aplicativo é implantado, vamos analisá-lo toowork! Olá *LoadGenerator demonstração* script do PowerShell inicia uma carga de trabalho em execução em todos os bancos de dados de locatário. carga do Olá mundo real em muitos aplicativos SaaS normalmente é esporádica e imprevisível. toosimulate esse tipo de carga, gerador hello gera uma carga distribuída em todos os locatários com intermitências aleatórias em cada locatário que ocorrem em intervalos aleatórias. Por isso leva vários minutos para Olá tooemerge de padrão de carga, portanto, é melhor gerador de saudação toolet executado pelo menos três ou quatro minutos antes de monitorar Olá carga.

1. Em Olá *PowerShell ISE*, abra hello... \\Módulos de aprendizado\\utilitários\\*demonstração LoadGenerator.ps1* script.
1. Pressione **F5** para executar o script hello e iniciar o gerador de carga hello (deixe Olá valores de parâmetro padrão para agora).

> [!IMPORTANT]
> toorun outros scripts, abra uma nova janela do PowerShell ISE. Gerador de carga Hello está em execução como uma série de trabalhos na sessão do PowerShell local. Olá *LoadGenerator.ps1 demonstração* script inicia o script do gerador de carga real hello, que é executado como uma tarefa de primeiro plano mais de uma série de trabalhos de geração de carregamento em segundo plano. Um trabalho do gerador de carga é chamado para cada banco de dados registrado no catálogo de saudação. trabalhos de saudação estão em execução na sua sessão do PowerShell local, para que fechar a sessão do PowerShell hello interrompe todos os trabalhos. Se você suspender seu computador, a geração de carga será pausada e continuará quando você ativá-lo novamente.

Depois que o gerador de carga Olá invoca os trabalhos de geração de carga para cada locatário, tarefa de primeiro plano Olá permanece em um estado de invocação de trabalho, onde ele inicia trabalhos de plano de fundo adicional para quaisquer novos locatários que são provisionados subsequentemente. Você pode usar *Ctrl-C* ou pressione hello *parar* tarefa de primeiro plano do botão toostop hello, mas o plano de fundo existente trabalhos continuarão a geração de carga em cada banco de dados. Se você precisar toomonitor e controla os trabalhos de plano de fundo hello, use *Get-Job*, *Receive-Job* e *Stop-Job*. Durante execução da tarefa em primeiro plano Olá você não pode usar Olá mesmo tooexecute de sessão do PowerShell outros scripts. toorun outros scripts, abra uma nova janela do PowerShell ISE.

Se você quiser toorestart Olá carga gerador sessão, por exemplo com parâmetros diferentes, você pode interromper tarefa de primeiro plano hello e, em seguida, executar novamente a saudação *demonstração LoadGenerator.ps1* script. Executar novamente *LoadGenerator.ps1 demonstração* primeiro interrompe quaisquer trabalhos em execução e, em seguida, gerador de saudação reinicializações, que inicia um novo conjunto de trabalhos usando os parâmetros atuais do hello.

Por enquanto, deixe o gerador de carga Olá sendo executado no estado de trabalho-invocar Olá.


## <a name="provision-a-new-tenant"></a>Provisionar um novo locatário

implantação inicial Olá cria três locatários de exemplo, mas vamos criar outra toosee de locatário como isso afeta o aplicativo hello implantado. fluxo de trabalho Olá Wingtip SaaS locatários provisionamento é detalhado no hello [tutorial provisionar e catálogo](sql-database-saas-tutorial-provision-and-catalog.md). Nesta etapa, você cria rapidamente um novo locatário.

1. Abrir... \\Modules\Provision de aprendizado e catálogo\\*demonstração ProvisionAndCatalog.ps1* em Olá *PowerShell ISE*.
1. Pressione **F5** para executar o script hello (deixe saudação padrão valores agora).

   > [!NOTE]
   > Usam vários scripts de SaaS Wingtip *$PSScriptRoot* tooallow navegando funções de toocall pastas em outros scripts. Essa variável é avaliada apenas quando Olá script é executado, pressionando **F5**.  Realçar e executar uma seleção (**F8**) pode resultar em erros, então pressione **F5** ao executar scripts.

Olá novo locatário banco de dados é criado em um pool Elástico do SQL, inicializado e registrado no catálogo de saudação. Após a configuração bem-sucedida, novo locatário de saudação do tíquete de venda *eventos* site é exibido no navegador:

![Novo locatário](./media/sql-database-saas-tutorial/red-maple-racing.png)

Atualizar Olá *Hub de eventos* e locatário novo Olá agora aparece na lista de saudação.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Explorar servidores hello, pools e bancos de dados de locatário

Agora que você já começou a ser executado um carregamento em relação a coleção de saudação de locatários, vamos dar uma olhada em alguns dos recursos de saudação que foram implantados:

1. No [portal do Azure](http://portal.azure.com), procurar tooyour lista de servidores SQL e abra o **catálogo -&lt;usuário&gt;**  server. o servidor de catálogo Olá contém dois bancos de dados. Olá **tenantcatalog**e hello **basetenantdb** (vazio *dourada* ou banco de dados de modelo que é copiado toocreate novos locatários).

   ![databases](./media/sql-database-saas-tutorial/databases.png)

1. Voltar tooyour lista de servidores SQL e abra Olá **tenants1 -&lt;usuário&gt;**  servidor que hospeda os bancos de dados de locatário hello. Cada banco de dados de locatário é um banco de dados _elástico padrão_ em um pool padrão de 50 eDTU. Também Observe que há um _vermelho bordo corrida_ banco de dados, o banco de dados do locatário Olá você provisionados anteriormente.

   ![server](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Pool de saudação do monitor

Se o gerador de carga Olá esteve em execução por vários minutos, dados suficientes devem ser toostart disponível examinar alguns Olá criados em bancos de dados e pools de recursos de monitoramento.

1. Procurar servidor toohello **tenants1 -&lt;usuário&gt;**e clique em **Pool1** para exibir a utilização de recursos para o pool de saudação (gerador de carga Olá foi executado para uma hora no hello gráficos a seguir) :

   ![monitorar pool](./media/sql-database-saas-tutorial/monitor-pool.png)

O que esses dois gráficos bem ilustram, é como os pools elásticos e o Banco de Dados SQL são bem adequados para cargas de trabalho de aplicativos SaaS. Quatro bancos de dados que são cada a intermitência tooas quanto 40 eDTUs facilmente suportados em um pool de 50 eDTU. Se eles foram provisionados como bancos de dados independentes, eles gostariam de cada toobe necessidade um S2 (DTU 50) toosupport Olá intermitências. custo de saudação de 4 bancos de dados independentes S2 seria preço de saudação de quase 3 vezes de pool hello e pool Olá ainda há bastante espaço para muitos bancos de dados mais. Em situações reais, os clientes do banco de dados SQL estão executando backup too500 bancos de dados em pools de eDTU 200. Para obter mais informações, consulte Olá [tutorial de monitoramento de desempenho](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu:

> [!div class="checklist"]

> * Como toodeploy Olá aplicativo SaaS Wingtip
> * Sobre servidores hello, pools e os bancos de dados que constituem o aplicativo hello
> * Locatários são mapeadas tootheir dados com hello *catálogo*
> * Como tooprovision novos locatários
> * Como toomonitor de utilização do pool de tooview locatário atividade
> * Como toodelete exemplo recursos toostop relacionados a cobrança

Agora tente Olá [tutorial provisionar e catálogo](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais em Olá aplicativo SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* toolearn sobre pools Elásticos, consulte [ *o que é um pool Elástico do SQL Azure*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn sobre Elásticos trabalhos, consulte [ *Gerenciando bancos de dados de nuvem expandido*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn sobre aplicativos de SaaS multilocatários, consulte [ *padrões para aplicativos de SaaS multilocatários de Design*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
