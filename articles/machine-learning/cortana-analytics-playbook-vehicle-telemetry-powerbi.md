---
title: "aaaPower painel BI para integridade de veículo e orientar hábitos - Azure | Microsoft Docs"
description: "Usar recursos de saudação do insights de previsão e em tempo real de inteligência Cortana toogain na integridade do veículo e orientar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Instruções de instalação do Painel de Power BI do modelo de solução de análise de telemetria do veículo
Isso **menu** toohello capítulos neste guia estratégico de links. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Olá solução de análise de telemetria do veículo demonstra como revendedores de carro, automóveis fabricantes e companhias podem aproveitar os recursos de saudação do Cortana Intelligence toogain em tempo real e previsão visões e integridade de veículo e orientar melhorias de toodrive hábitos na área de saudação do cliente experiência, R & D e campanhas de marketing. Este documento contém instruções passo a passo de como você pode configurar relatórios do Power BI hello e painel depois Olá solução é implantada em sua assinatura. 

## <a name="prerequisites"></a>Pré-requisitos
1. Implantar Olá [telemetria análise](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solução  
2. [Instalar o Microsoft Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331)
3. Uma [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/). Se você não tiver uma assinatura do Azure, comece com uma assinatura gratuita do Azure
4. Conta do Microsoft Power BI

## <a name="cortana-intelligence-suite-components"></a>Componentes do Cortana Intelligence Suite
Como parte do modelo de solução de análise de telemetria do veículo hello, Olá serviços Cortana Intelligence a seguir é implantado na sua assinatura.

* **Hubs de Eventos** para ingerir milhões de eventos de telemetria do veículos no Azure.
* **Stream Analytics** para obter informações em tempo real sobre a integridade do veículo e persistir esses dados no armazenamento de longo prazo para uma análise de lote mais avançada.
* **Aprendizado de máquina** para detecção de anomalias em tempo real e insights previsão toogain de processamento em lotes.
* **HDInsight** tootransform utilizou dados em grande escala
* **Fábrica de dados** manipula orquestração, agendamento, gerenciamento de recursos e o monitoramento do pipeline de processamento de lote hello.

**PowerBI** fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva. 

solução de saudação usa duas fontes de dados diferentes: **simulados veículo sinais e o conjunto de dados de diagnóstico** e **catálogo veículo**.

Um simulador de telemática do veículo é incluído como parte desta solução. Ele emite informações de diagnóstico e sinaliza o estado toohello correspondente de veículo hello e um padrão em um determinado ponto no tempo. 

Olá veículo catálogo é um mapeamento de toomodel Referência dataset contendo VIN

## <a name="power-bi-dashboard-preparation"></a>Preparação do Painel do Power BI
### <a name="setup-power-bi-real-time-dashboard"></a>Instalação do Painel do Power BI em tempo real

**Iniciar o aplicativo de painel em tempo real de hello** concluída a implantação hello, você deve seguir instruções de operação Olá Manual

* Baixe o aplicativo de painel em tempo real RealtimeDashboardApp.zip e descompacte-o.
*  Na pasta de descompactado hello, abra o arquivo de configuração do aplicativo 'RealtimeDashboardApp.exe.config' appSettings de substituição para Eventhub, armazenamento de Blob e ML conexões de serviço com valores hello no hello Manual de instruções de operação e salvar suas alterações.
* Execute o aplicativo RealtimeDashboardApp.exe. Uma janela de logon será pop-up, forneça suas credenciais do Power BI válidas e clique em Olá **aceitar** botão. Em seguida, o aplicativo hello iniciará toorun.

   ![Entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Permissões do Painel do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Site de tooPowerBI de logon e criar um painel em tempo real.

Agora, você painel do Power BI Olá tooconfigure pronto com visualizações avançadas toogain em tempo real e hábitos de previsão ideias sobre a integridade de veículo e referências. Leva aproximadamente 45 minutos tooan horas toocreate hello todos os relatórios e configurar Olá painel. 

### <a name="configure-power-bi-reports"></a>Configurar relatórios do Power BI
relatórios em tempo real Hello e painel Olá levar cerca de 30 a 45 minutos toocomplete. Procurar muito[http://powerbi.com](http://powerbi.com) e logon.

![Entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Um novo conjunto de dados é gerado no Power BI. Clique em Olá **ConnectedCarsRealtime** conjunto de dados.

![Selecionar conjunto de dados de carros conectados em tempo real](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Salvar a saudação de relatório em branco usando **Ctrl + s**.

![Salvar relatório em branco](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Forneça o nome de relatório *Análise em tempo real de telemetria do veículo - Relatórios*.

![Forneça o nome do relatório](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Relatórios em tempo real
Há três relatórios em tempo real nesta solução:

1. Veículos em operação
2. Veículos que precisam de manutenção
3. Estatísticas de integridade de veículos

Você pode escolher tooconfigure todos os relatórios em tempo real de três de saudação ou parar depois de qualquer estágio e continuar toohello próxima seção de configuração relatórios de lote de saudação. Recomendamos que você toocreate todos os Olá três relatórios insights completo do toovisualize saudação do caminho de saudação em tempo real de solução de saudação.  

### <a name="1-vehicles-in-operation"></a>1. Veículos em operação
Clique duas vezes em **página 1** e renomeá-lo muito "Veículos na operação"  
    ![Carros conectados - Veículos em operação](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Selecione o campo **vin** em **Campos** e escolha o tipo de visualização como **"Placa"**.  

A visualização de placa é criada como mostrado na figura.  
    ![Carros conectados - Selecione vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Clique em nova visualização do hello área em branco tooadd.  

Selecione **Cidade** e **vin** nos campos. Alterar a visualização muito**"Mapa"**. Arraste o **vin** na área de valores. Arraste **city** de campos muito**legenda** área.   
    ![Carros conectados - Visualização da placa](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Selecione **formato** seção de **visualizações**, clique em **título** e alterar Olá **texto** muito**"veículos em operação por cidade"**.  
    ![Carros conectados - Veículos em operação por cidade](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

A visualização final será como mostrado na figura.    
    ![Carros conectados - Visualização final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Clique em nova visualização do hello área em branco tooadd.  

Selecione **City** e **vin**, altere o tipo de visualização muito**gráfico de coluna clusterizado**. Certifique-se de que o campo **Cidade** está na **Área do eixo** e o **vin** está na **Área do valor**  

Classificar gráfico por **"Contagem de vin"**  
    ![Carros conectados - Contagem de vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Gráfico de alteração **título** muito**"Veículos em operação por cidade"**  

Clique Olá **formato** seção e, em seguida, selecione **cores de dados**, clique em Olá **"Em"** muito**Mostrar tudo**  
    ![Carros conectados - Mostrar todas as cores de dados](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Alterar a cor de saudação de cidade individual, clicando no ícone de cor.  
    ![Carros conectados - Alterar cores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Clique em nova visualização do hello área em branco tooadd.  

Selecione a visualização **Gráfico de Coluna Clusterizada** nas visualizações, arraste o campo **cidade** para a área do **Eixo**, **Modelo** para a área de **Legenda** e **vin** para a área **Valor**.  
    ![Carros conectados - Gráfico de colunas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Carros conectados - Renderização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Reorganize todas as visualizações nesta página conforme mostrado na figura.  
    ![Carros conectados - Visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Você configurou com êxito o relatório em tempo real do hello "Veículos na operação". Você pode continuar relatório em tempo real do toocreate Olá Avançar ou parar aqui e configurar Olá painel. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Veículos que precisam de manutenção
Clique em ![adicionar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd um novo relatório, renomeá-lo muito**"Veículos necessidade de manutenção"**

![Carros conectados - Veículos que precisam de manutenção](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Selecione **vin** campo e altere o tipo de visualização muito**cartão**.  
    ![Carros conectados - Visualização da placa do vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Temos um campo chamado "MaintenanceLabel" no conjunto de dados de saudação. Esse campo pode ter um valor “0” ou “1”. Ele é definido pelo modelo de aprendizado de máquina do Azure Olá provisionado como parte da solução e integrados com caminho de saudação em tempo real. o valor de Hello "1" indica que um veículo exige manutenção. 

tooadd um **nível de página** filtro para mostrar dados de veículos, que exigem manutenção: 

1. Saudação de arrastar **"MaintenanceLabel"** para **filtros em nível de página**.  
   ![Carros conectados - Filtros de página](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Clique no menu **Filtragem Básica** presente na parte inferior do Filtro de página MaintenanceLabel.  
   ![Carros conectados - Filtragem básica](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Definir o valor de filtro muito**"1"**    
   ![Carros conectados - Valor do filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Clique em nova visualização do hello área em branco tooadd.  

Selecione o **Gráfico de Coluna Clusterizada** das visualizações  
![Carros conectados - Visualização da placa do vind](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Carros conectados - Gráfico de colunas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Campo de arrastar **modelo** em **eixo** área, **Vin** muito**valor** área. Em seguida, classifique visualização por **Contagem de vin**.  Gráfico de alteração **título** muito**"Veículos que exigem manutenção pelo modelo"**  

Arraste os campos **vin** para a **Saturação da cor** presente na seção **Campos**![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) da guia **Visualização**  
![Carros conectados - Saturação de cor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Alterar **Cores dos Dados** nas visualizações na seção **Formato**  
Alterar a cor do Mínimo para: **F2C812**  
Alterar a cor do Máximo para: **FF6300**  
![Carros conectados - Alterações de cor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Carros conectados - Novas cores de visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Clique em nova visualização do hello área em branco tooadd.  

Selecione **Gráfico de colunas clusterizado** das visualizações, arraste o campo **vin** para a área **Valor**, arraste o campo **Cidade** para a área **Eixo**. Classificar gráfico por **"Contagem de vin"**. Gráfico de alteração **título** muito**"Veículos que necessitam de manutenção por cidade"**   
![Carros conectados - Veículos que precisam de manutenção por cidade](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Clique em nova visualização do hello área em branco tooadd.  

Selecione **cartão de várias linhas** visualização de visualizações, arraste **modelo** e **vin** em Olá **campos** área.  
![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Esse relatório final Olá reorganizar todos visualização hello, tem a seguinte aparência:  
![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Você configurou com êxito o relatório em tempo real do hello "Veículos necessidade de manutenção". Você pode continuar relatório em tempo real do toocreate Olá Avançar ou parar aqui e configurar Olá painel. 

### <a name="3-vehicles-health-statistics"></a>3. Estatísticas de integridade de veículos
Clique em ![adicionar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd novo relatório, renomeá-lo muito**"Estatísticas de integridade veículos"**  

Selecione **medidor** visualização de visualizações, em seguida, arraste Olá **velocidade** para **, valor mínimo, máximo** áreas.  
![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Alterar a agregação padrão de saudação do **velocidade** na **valor área** muito**médio** 

Alterar a agregação padrão de saudação do **velocidade** na **área mínima** muito**mínimo**

Alterar a agregação padrão de saudação do **velocidade** na **área máximo** muito**máximo**

![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Renomear Olá **medidor título** muito**"Velocidade média"** 

![Carros conectados - Medidor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Clique em nova visualização do hello área em branco tooadd.  

Da mesma forma, adicione um **Medidor** para **média de óleo do motor**, **média de combustível** e **temperatura média do motor**.  

Alterar saudação padrão agregação dos campos em cada medidor conforme descrito acima etapas **"Velocidade média"** do medidor.

![Carros conectados - Medidores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Clique em nova visualização do hello área em branco tooadd.

Selecione **clusterizado gráfico de coluna e linha** de visualizações, em seguida, arraste **City** para **eixo compartilhado**, arraste **velocidade**, **campos tirepressure e engineoil** em **valores de coluna** área, alterar seu tipo de agregação também**médio**. 

Saudação de arrastar **engineTemperature** para **valores de linha** área, alterar o tipo de agregação de saudação muito**médio**. 

![Carros conectados - Campos de visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Gráfico de saudação de alteração **título** muito**"Média de velocidade, pneu pressão, petróleo mecanismo e temperatura de mecanismo"**.  

![Carros conectados - Campos de visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Clique em nova visualização do hello área em branco tooadd.

Selecione **Treemap** visualização de visualizações, arraste Olá **modelo** para Olá **grupo** área e arraste Olá campo ** MaintenanceProbability** em Olá **valores** área.

Gráfico de saudação de alteração **título** muito**"Modelos de veículo que necessitam de manutenção"**.

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Clique em nova visualização do hello área em branco tooadd.

Selecione **gráfico de barras empilhadas 100%** de visualização, arraste Olá **city** para Olá **eixo** área e arraste Olá **MaintenanceProbability**, **RecallProbability** campos em Olá **valor** área.

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Clique em **formato**, selecione **cores de dados**e conjunto hello **MaintenanceProbability** toohello valor de cor **"F2C80F"**.

Saudação de alteração **título** de saudação do gráfico muito**"Probabilidade de veículo manutenção e lembre-se por cidade"**.

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Clique em nova visualização do hello área em branco tooadd.

Selecione **gráfico de área** de visualização de visualizações, arraste Olá **modelo** para Olá **eixo** área e arraste Olá **engineOil, tirepressure, velocidade e MaintenanceProbability** campos em Olá **valores** área. Alterar o tipo de agregação muito**"Médio"**. 

![Carros conectados - Alterar tipo de agregação](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Alterar o título de saudação do gráfico de saudação muito**"Média petróleo mecanismo, tire pressão, velocidade e manutenção de probabilidade pelo modelo"**.

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Clique em nova visualização do hello área em branco tooadd:

1. Selecione a visualização **Gráfico de Dispersão** em visualizações.
2. Saudação de arrastar **modelo** para Olá **detalhes** e **legenda** área.
3. Saudação de arrastar **combustível** para Olá **eixo x** área, altere a agregação de saudação muito**médio**.
4. Arraste **engineTemparature** em **área de eixo y**, altere a agregação de saudação muito**médio**
5. Saudação de arrastar **vin** para Olá **tamanho** área.

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Gráfico de saudação de alteração **título** muito**"Médias de combustível, temperatura mecanismo por modelo"**.

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

Esse relatório final Olá se parecerá com conforme mostrado abaixo.

![Carros conectados-Relatório final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Visualizações de PIN de painel em tempo real do hello relatórios toohello
Crie um painel em branco clicando no ícone de adição Olá tooDashboards Avançar. Você pode chamá-lo de "Painel de análise de telemetria do veículo"

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Visualização de fixar Olá da saudação acima do painel de toohello de relatórios. 

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

Painel de saudação se assemelhar ao seguinte quando todos os Olá três relatórios são criados e Olá correspondente visualizações são fixados toohello painel. Se você não tiver criado todos os relatórios de saudação, seu painel pode ser diferente. 

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Parabéns! Você criou com êxito o dashboard em tempo real de saudação. Enquanto você continua tooexecute CarEventGenerator.exe e RealtimeDashboardApp.exe, você deve ver atualizações dinâmicas no painel de saudação. Ele deve levar Olá de toocomplete minutos too15 10 etapas a seguir.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Instalação do painel de processamento em lote do Power BI
> [!NOTE]
> Ele leva cerca de duas horas (de conclusão bem-sucedida de saudação da implantação Olá) para Olá final tooend processamento em lotes a execução do pipeline toofinish e processe a partir de um ano de dados gerados. Portanto, aguarde Olá processamento toofinish antes de continuar com as próximas etapas hello. 
> 
> 

**Baixe o arquivo de designer Olá Power BI**

* Um arquivo de designer do Power BI pré-configurado é incluído como parte da implantação de saudação instruções de operação Manual
* Procure por 2. Painel de processamento em lote instalação Power BI você pode baixar o modelo do Power BI Olá para o painel de processamento em lotes chamado **ConnectedCarsPbiReport.pbix**.
* Salve localmente

**Configurar relatórios do Power BI**

* Arquivo de designer Olá aberto '**ConnectedCarsPbiReport.pbix**' usando o Power BI Desktop. Se você já não tiver, instale Olá Power BI Desktop de [instalação do Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331). 
* Clique em Olá **editar consultas**.

![Editar consulta do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Clique duas vezes em Olá **fonte**.

![Definir origem do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Atualize a cadeia de caracteres de conexão de servidor com hello Azure SQL server que foi configurado como parte da implantação de saudação.  Procure nas instruções de operação Olá Manual em 

    4. Banco de Dados SQL do Azure
    
    * Servidor: somethingsrv.database.windows.net
    * Banco de dados: connectedcar
    * Nome de usuário: username
    * Senha: gerencie sua senha do SQL Server no Portal do Azure

* Deixe **Banco de dados** como *connectedcar*.

![Definir banco de dados do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Clique em **OK**.
* Você verá **credencial do Windows** guia é selecionada por padrão, alterá-la muito**credenciais de banco de dados** clicando em **banco de dados** guia à direita.
* Fornecer Olá **Username** e **senha** do seu banco de dados de SQL do Azure que foi especificada durante a instalação de sua implantação.

![Forneça as credenciais do banco de dados](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Clique em **Conectar**
* Repita Olá acima etapas para cada Olá três restantes consultas presentes no painel direito e, em seguida, atualizar detalhes de conexão de fonte de dados de saudação.
* Clique em **Fechar e Carregar**. Conjuntos de dados de arquivo do Power BI Desktop são tabelas de banco de dados do Azure tooSQL conectado.
* **Fechar** arquivo do Power BI Desktop.

![Fechar o Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Clique em **salvar** botão toosave alterações de saudação. 

Você configurou agora todos os relatórios de saudação correspondente do caminho de processamento de lote toohello na solução de saudação. 

## <a name="upload-toopowerbicom"></a>Carregar muito*powerbi.com*
1. Navegue toohello portal de web do Power BI em http://powerbi.com e logon.
2. Clique em **Obter Dados**  
3. Carregar Olá arquivo do Power BI Desktop.  
4. tooupload, clique em **obter dados -> obter arquivos -> arquivo Local**  
5. Navegue toohello **"**ConnectedCarsPbiReport.pbix**"**  
6. Uma vez carregado o arquivo hello, será navegado tooyour back espaço de trabalho do Power BI.  

Um conjunto de dados, relatórios e um painel em branco serão criados para você.  

Fixar gráficos tooa novo painel chamado **painel de análise de telemetria do veículo** na **Power BI**. Clique em Olá painel em branco criado acima e, em seguida, navegue toohello **relatórios** seção clique Olá carregado recentemente o relatório.  

![Telemetria do veículo Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Observação Olá relatório tem seis páginas:**  
Página 1: densidade do veículo  
Página 2: integridade do veículo em tempo real  
Página 3: veículos com direção agressiva   
Página 4: veículos que sofreram recall  
Página 5: veículos com uso eficiente de combustível  
Página 6: logotipo da Contoso  

![Carros conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**Na página 3**, fixar seguinte hello:  

1. Contagem de vin  
   ![Carros conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Veículos de direção agressiva por modelo – Gráfico de cascata   
   ![Telemetria de veículo - Fixar gráficos 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**Na página 5**, fixar seguinte hello: 

1. Contagem de vin    
   ![Telemetria de veículo - Fixar gráficos 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Veículos com eficiência de combustível: Gráfico de colunas agrupadas   
   ![Telemetria de veículo - Fixar gráficos 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**Na página 4**, fixar seguinte hello:  

1. Contagem de vin  
   ![Telemetria de veículo - Fixar gráficos 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Veículos que tiveram recall por cidade, modelo : Treemap   
   ![Telemetria de veículo - Fixar gráficos 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**Na página 6**, fixar seguinte hello:  

1. Logotipo da Contoso Motors   
   ![Telemetria de veículo - Fixar gráficos 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Organizar Olá painel**  

1. Navegue toohello painel
2. Passe o mouse sobre cada gráfico e renomear com base na nomenclatura Olá fornecido na imagem do painel completa Olá abaixo. Também mova gráficos Olá em torno de toolook como Olá painel abaixo.  
   ![Telemetria de veículo - Organizar painel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Telemetria do veículo Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Se você tiver criado todos os relatórios de saudação mencionados neste documento, hello painel concluído final deve ter aparência Olá figura a seguir. 

![Telemetria de veículo - Organizar painel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Parabéns! Você criou com êxito o hello relatórios e Olá toogain painel em tempo real, previsão e ideias de lote de integridade de veículo e orientar hábitos.  
