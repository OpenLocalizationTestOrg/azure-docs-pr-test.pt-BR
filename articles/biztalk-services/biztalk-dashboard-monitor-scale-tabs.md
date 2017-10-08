---
title: "aaaDashboard, Monitor, escala, configurar e conexões híbridas nos Serviços BizTalk | Microsoft Docs"
description: "Saiba mais sobre os controles de saudação e monitorar o desempenho em guias de portal clássico Olá para Serviços BizTalk: painel, Monitor, escala, configurar e conexões híbridas. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Examine Olá guias painel, Monitor, escala, configurar e Conexão híbrida

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Depois de criar o BizTalk Service e implantar seu aplicativo, você pode alterar algumas das configurações de serviço BizTalk hello e monitorar o desempenho do aplicativo hello. 

Quando você abre Olá portal clássico do Azure, são colocados automaticamente em hello **todos os itens** guia tooview Service o BizTalk, selecione o BizTalk Service no hello **todos os itens** guia ou selecione hello **Serviços BIZTALK** guia; e, em seguida, selecione o nome do BizTalk Service.

Isso abre uma nova janela com hello guias a seguir. Este tópico descreve essas guias.

## <a name="quickstart-quickstartquickstart"></a>Início rápido (![Início rápido][Quickstart])
Dependendo da saudação BizTalk Services Edition, todas as opções listadas podem não estar disponíveis. 

<table border="1">
    <tr>
        <td><strong>Obter ferramentas Olá</strong></td>
        <td>Baixe Olá SDK dos Serviços BizTalk tooinstall Olá projeto modelos do Visual Studio no computador de desenvolvimento local. Esses modelos criam Olá <strong>Serviços BizTalk</strong> (ponte) e hello <strong>artefatos do serviço BizTalk</strong> projetos do Visual Studio de (transformação) que são implantado tooyour BizTalk Service.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure </a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">instalando Olá SDK dos Serviços BizTalk do Azure</a> listas Olá etapas tooget iniciado.
        </td>
    </tr>
    <tr>
        <td><strong>Criar contratos de parceiro</strong></td>
        <td>Abre Olá Portal de serviços do Azure BizTalk hospedado no Azure, onde você pode adicionar parceiros e cria X12, AS2 e EDIFACT EDI contratos.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar os componentes para mensagens EDI no Portal de Serviços BizTalk</a> listas Olá etapas tooget iniciado.
        </td>
    </tr>

<tr>
        <td><strong>Saiba mais sobre os Serviços BizTalk</strong></td>
        <td>Vá toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">Central de informações</a> toolearn mais sobre os Serviços BizTalk do Azure.</td>
</tr>
</table>


Na barra de tarefas de saudação na parte inferior do hello, você pode:

<table border="1">

<tr>
<td><strong>Gerenciar</strong> a implantação de seu aplicativo</td>
<td>Abre o portal de Serviços BizTalk do Azure hello. Olá Portal de Serviços BizTalk é a configuração de tooEDI de entrada hello, inclusive adicionar parceiros e criar X12, AS2 e acordos de EDIFACT.
<br/><br/>
Isso é Olá igual <strong>criar acordos de parceiro</strong> em Olá <strong>início rápido</strong> guia.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar os componentes para mensagens EDI no Portal de Serviços BizTalk</a> fornece mais informações sobre Olá Portal de Serviços BizTalk.</td>
</tr>

<tr>
<td><strong>Informações de Conexão</strong> de saudação Namespace de controle de acesso</td>
<td>Quando você seleciona as informações de Conexão, em seguida, Olá Namespace de controle de acesso, emissor padrão, e chave padrão são exibidos. Você pode copiar esses valores.
<br/><br/>
Você também pode abrir Olá Portal de controle de acesso. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Criar um Namespace de controle de acesso</a> fornece mais informações sobre Olá Portal de controle de acesso.</td>
</tr>

<tr>
<td><strong>Sincronizar chaves</strong> em Olá conta de armazenamento</td>
<td>Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente. Essas chaves de criptografia controlam acesso tooyour conta de armazenamento. O BizTalk Service usa automaticamente Olá chave primária. <strong>Sincronizar chaves</strong> habilitar usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.
<br/><br/>
Por exemplo, convém Olá BizTalk Service toouse uma nova chave primária para Olá conta de armazenamento. toodo isso:
<br/><br/>
<ol>
<li>Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>. Selecione Olá chave secundária. Quando você fizer isso, Olá BizTalk Service inicia usando Olá chave secundária.</li>
<li>Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave primária da saudação. Lembre-se de que o BizTalk Service está usando Olá chave secundária.</li>
<li>Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>. Agora, selecione Olá chave primária. Isso é Olá nova chave primária você regenerado.</li>
<li>Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave secundária da saudação.</li>
</ol>
<br/>
Esse processo é chamado de "chaves de substituição". finalidade de saudação é tooenable usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.</td>
</tr>

<tr>
<td><strong>Excluir</strong> seu aplicativo</td>
<td>Quando você seleciona excluir, o BizTalk Service e tooit de todos os itens implantados são removidos.</td>
</tr>
</table>


## <a name="dashboard"></a>Painel
Dependendo da saudação BizTalk Services Edition, todas as opções listadas podem não estar disponíveis. 

Quando você seleciona o nome do BizTalk Service, o guia do painel de saudação é exibido. No Painel, você pode:

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Visão geral de uso: Mostra o número de saudação de usadas as conexões híbridas
Também exibe o uso de dados de saudação em GB. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Gráfico de métrica: mostra uma lista fixa de métricas de desempenho
Essas métricas fornecem valores em tempo real sobre a integridade de saudação do hello BizTalk Service. Você também pode escolher Olá **relativo** ou **absoluto** hello e valores de intervalo de tempo **intervalo** de métricas de saudação que são exibidas no gráfico de saudação. 

Para obter uma descrição dessas métricas de desempenho, vá muito[métricas disponíveis](#Metrics) neste tópico.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Visão Rápida: lista as propriedades do Serviço BizTalk
<table border="1">

<tr>
<td><strong>Atualizar as credenciais do banco de dados de acompanhamento</strong></td>
<td>Olá de alterações de nome de usuário e senha usados toolog em Olá banco de dados de rastreamento.</td>
</tr>
<tr>
<td><strong>Atualizar o certificado de SSL</strong></td>
<td>Pode atualizar Olá BizTalk Service toouse um certificado SSL diferente. Um certificado SSL autoassinado é automaticamente criado quando você <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">criar hello BizTalk Service</a>.</td>
</tr>
<tr>
<td><strong>Baixar certificado</strong></td>
<td>Você pode baixar o certificado SSL Olá usado pelo computador local tooa BizTalk Service.</td>
</tr>
<tr>
<td><strong>Status</strong></td>
<td>Exibe o status atual de saudação do BizTalk Service. Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Serviços BizTalk: gráfico de estado do serviço</a>. </td>
</tr>
<tr>
<td><strong>URL do serviço</strong></td>
<td>Olá URL para o BizTalk Service. Isso é Olá mesmo como Olá <strong>URL do domínio</strong> inserido quando o BizTalk Service é criado.</td>
</tr>
<tr>
<td><strong>Endereço VIP (IP virtual público)</strong></td>
<td>endereço IP de saudação atribuído tooyour BizTalk Service. Ele é usado para todos os pontos de extremidade de entrada e é o endereço de origem Olá para tráfego de saída. Esse endereço IP pertence tooyour BizTalk Service desde que ele é criado. Se você excluir Olá BizTalk Service, o endereço IP de saudação é atribuído tooanother BizTalk Service.</td>
</tr>
<tr>
<td><strong>Namespace do ACS</strong></td>
<td>Autentica com hello BizTalk Service.</td>
</tr>
<tr>
<td><strong>Edição</strong></td>
<td>Lista Olá que edição inserida quando Olá BizTalk Service é criado.</td>
</tr>
<tr>
<td><strong>Localidade</strong></td>
<td>Exibe Olá região geográfica que hospeda o BizTalk Service.</td>
</tr>
<tr>
<td><strong>Criado</strong></td>
<td>Olá Olá de data e hora exibe o BizTalk Service foi criado.</td>
</tr>
<tr>
<td><strong>Banco de dados de acompanhamento</strong></td>
<td>nome de banco de dados do Azure SQL Olá que armazena Olá controle tabelas usadas pelo seu BizTalk Service. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos Explained</a> fornece detalhes sobre Olá banco de dados de rastreamento.</td>
</tr>
<tr>
<td><strong>Armazenamento de monitoramento/arquivamento</strong></td>
<td>Olá armazenamento do Azure nome da conta que armazena Olá monitoramento saída o BizTalk Service.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos Explained</a> fornece detalhes sobre Olá conta de armazenamento.</td>
</tr>
<tr>
<td><strong>Nome da assinatura</strong></td>
<td>Lista de assinatura de saudação que hospeda o BizTalk Service. assinatura de saudação controla acesso toohello portal clássico do Azure.</td>
</tr>
<tr>
<td><strong>ID da assinatura</strong></td>
<td>Quando uma assinatura é criada, uma ID da assinatura é gerada automaticamente. Ao usar APIs REST, talvez seja necessário Olá tooenter ID de assinatura.</td>
</tr>
</table>

[Serviços BizTalk: Portal clássico do Azure usando o provisionamento](http://go.microsoft.com/fwlink/p/?LinkID=302280) listas Olá etapas toocreate um BizTalk Service.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Gerenciar informações de Conexão, sincronizar as chaves e excluir na barra de tarefas de saudação:
<table border="1">

<tr>
<td><strong>Gerenciar</strong> a implantação de seu aplicativo</td>
<td>Abre Olá Portal de Serviços BizTalk do Azure. Olá Portal de Serviços BizTalk é a configuração de tooEDI de entrada hello, inclusive adicionar parceiros e criar X12, AS2 e acordos de EDIFACT.
<br/><br/>
Isso é Olá igual <strong>criar acordos de parceiro</strong> em Olá <strong>início rápido</strong> guia.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar os componentes para mensagens EDI no Portal de Serviços BizTalk</a> fornece mais informações sobre Olá Portal de Serviços BizTalk.</td>
</tr>
<tr>
<td><strong>Informações de Conexão</strong> de saudação Namespace de controle de acesso</td>
<td>Exibe Olá Namespace de controle de acesso, o emissor padrão e valores de chave padrão. que podem ser copiado.
<br/><br/>
Você também pode abrir Olá Portal de controle de acesso. Este Portal de controle de acesso é Olá mesmo que usar a opção do Active Directory de saudação no painel de navegação esquerdo hello.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Gerenciando seu Namespace do ACS</a> fornece mais informações sobre Olá Portal de controle de acesso.</td>
</tr>
<tr>
<td><strong>Sincronizar chaves</strong> em Olá conta de armazenamento</td>
<td>Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente. Essas chaves de criptografia controlam acesso tooyour conta de armazenamento. O BizTalk Service usa automaticamente Olá chave primária. <strong>Sincronizar chaves</strong> habilitar usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.
<br/><br/>
Por exemplo, convém Olá BizTalk Service toouse uma nova chave primária para Olá conta de armazenamento. toodo isso:
<br/><br/>
<ol>
<li>Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>. Selecione Olá chave secundária. Quando você fizer isso, Olá BizTalk Service inicia usando Olá chave secundária.</li>
<li>Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave primária da saudação. Lembre-se de que o BizTalk Service está usando Olá chave secundária.</li>
<li>Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>. Agora, selecione Olá chave primária. Isso é Olá nova chave primária você regenerado.</li>
<li>Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave secundária da saudação.</li>
</ol>
<br/>
Esse processo é chamado de "chaves de substituição". finalidade de saudação é tooenable usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.</td>
</tr>

<tr>
<td><strong>Excluir</strong> seu aplicativo</td>
<td>O BizTalk Service e tooit de todos os itens serão removidos.</td>
</tr>
</table>


## <a name="monitor"></a>Monitoramento
Não se aplica a toohello edição gratuita.

Quando você seleciona o nome do BizTalk Service, da guia monitorar hello está disponível e exibe Olá seguinte:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Gráfico de métrico: Olá exibe selecionado métricas de desempenho
Essas métricas fornecem valores em tempo real sobre a integridade de saudação do hello BizTalk Service. Você escolhe quais métricas de desempenho são exibidas. No máximo seis métricas de desempenho podem ser exibidas simultaneamente. 

Você também pode escolher Olá **relativo** ou **absoluto** hello e valores de intervalo de tempo **intervalo** das métricas de saudação que são exibidas. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>tooremove ou exibir as métricas no gráfico de saudação:
1. Selecione Olá **Monitor** guia.
2. Selecione **adicionar métricas** na barra de tarefas de saudação:  
   ![Selecione Adicionar Métricas][AddMetrics]
3. Verifique se deseja toodisplay de métricas de desempenho de saudação.
4. Selecione Olá marca de seleção tooreturn toohello **Monitor** guia.
5. Selecione Olá círculo próxima toohello métrica toodisplay valor da métrica no gráfico de saudação.  
   
    Por exemplo, Olá **uso da CPU** métrica está esmaecida; sua saída não é exibida no gráfico de saudação:  
   ![A métrica Uso de CPU fica esmaecida][GrayedMetric]  
   
    Selecione Olá esmaecidas saudação do círculo tooenable **uso da CPU** toodisplay métrica sua saída em gráfico hello:  
   ![A métrica Uso de CPU está habilitada][EnabledMetric]
6. Selecione tooremove uma métrica do gráfico de exibição hello e lista hello, **excluir métrica** na barra de tarefas de saudação. lista de métrica toohello back Olá tooadd, selecione **adicionar métricas** na barra de tarefas hello, verificar métrica hello e selecione Olá marca de seleção tooreturn toohello **Monitor** guia. Selecione Olá esmaecidas métrica de saudação do círculo tooenable.

## <a name="Metrics"></a>Métricas disponíveis
Olá, contadores de desempenho/métricas a seguir está disponível:

<table border="1">

<tr>
<td><strong>Latência de viagem de ida e volta</strong></td>
<td>Exibe o saudação tempo médio em milissegundos (ms) tooprocess que é recebida uma mensagem da mensagem de saudação do hello tempo até que a mensagem de saudação é totalmente processada pelo Olá BizTalk Service em todas as pontes. São contadas apenas mensagens processadas com êxito.<br/><br/>
Quando ocorre Olá eventos a seguir, um carimbo de hora é criado:
<ul>
<li>Mensagem entrar gateway Olá</li>
<li>Mensagem é roteada toohello destino</li>
<li>A resposta do destino é recebida</li>
<li>Gateway de toohello de resposta enviada de confirmação de destino</li>
</ul>
<br/>
Esta métrica mostra o resultado de saudação de saudação cálculo a seguir:
<br/><br/>
[Destino confirmação resposta enviada toohello gateway] - [mensagem entrar gateway Olá]</td>
</tr>
<tr>
<td><strong>Falhas na origem</strong></td>
<td>Exibe o número total de saudação de mensagens que falharam por Olá BizTalk Service quando recebendo mensagens de pontos de extremidade de origem hello.</td>
</tr>
<tr>
<td><strong>Uso da CPU</strong></td>
<td>Lista Olá % tempo do processador médio de todas as instâncias de função.</td>
</tr>
<tr>
<td><strong>Latência de processamento</strong></td>
<td>Exibe o saudação tempo médio em milissegundos (ms) tooprocess uma mensagem de saudação BizTalk Service em todas as pontes, excluindo o tempo de saudação gasto em destinos. São contadas apenas mensagens processadas com êxito.<br/><br/>
Quando cada Olá eventos a seguir ocorrem, é criado um carimbo de hora:

<ul>
<li>Mensagem entrar gateway Olá</li>
<li>Mensagem é roteada toohello destino</li>
<li>A resposta do destino é recebida</li>
<li>Gateway de toohello de resposta enviada de confirmação de destino</li>
</ul>
<br/>Esta métrica mostra o resultado de saudação de saudação cálculo a seguir:<br/><br/>
[Destino confirmação resposta enviada toohello gateway] - [mensagem entrar gateway Olá] - [resposta de destino é recebida] + [mensagem é roteada toohello destino]</td>
</tr>
<tr>
<td><strong>Falhas no processo</strong></td>
<td>Exibe o número total de saudação de mensagens que falharam durante o processamento por Olá BizTalk Service em todas as pontes de saudação em um intervalo de tempo.</td>
</tr>
<tr>
<td><strong>Mensagens Enviadas</strong></td>
<td>Exibe Olá o número total de mensagens enviadas por Olá BizTalk Service em todas as pontes dentro de um intervalo de tempo. Essa métrica é incrementada quando uma mensagem enviada de um pipeline alcança o destino da rota hello. Essa métrica não indica se uma mensagem foi processada com êxito.<br/><br/>
Em um cenário de solicitação-resposta, a métrica de saudação é incrementada quando o destino da rota Olá envia um pipeline de toohello voltar de confirmação de recebimento.</td>
</tr>
<tr>
<td><strong>Mensagens recebidas</strong></td>
<td>Exibe Olá o número total de mensagens recebidas por Olá BizTalk Service em todas as pontes dentro de um intervalo de tempo. Essa métrica é incrementada quando uma nova mensagem é recebida pelo pipeline de saudação.</td>
</tr>
<tr>
<td><strong>Mensagens em processamento</strong></td>
<td>Exibe Olá número total de mensagens que estão sendo processadas pelo Olá BizTalk Service dentro de um intervalo de tempo.</td>
</tr>
<tr>
<td><strong>Mensagens processadas</strong></td>
<td>Exibe Olá número total de mensagens processadas com êxito pelo Olá BizTalk Service em todas as pontes dentro de um intervalo de tempo. Essa métrica é incrementada quando uma mensagem é recebida com êxito pelo pipeline hello e destino toohello roteado com êxito.</td>
</tr>
</table>


## <a name="scale"></a>Escala
Na guia dimensionamento de saudação, você pode adicionar ou subtrair Olá número de unidades usadas pelo seu BizTalk Service. Por padrão, há uma unidade configurada. Unidades adicionais podem ser adicionadas tooscale o BizTalk Service. Quando você aumenta a escala hello, você está aumentando a taxa de transferência. Olá quantidade de recursos também aumenta, incluindo pontes implantadas, contratos, conexões de LOB e a capacidade de processamento. Por exemplo, você aumentar a escala de saudação de unidades de 1 unidade too2. Nessa situação, você pode implantar Olá duplo número de pontes, double contratos hello, double Olá LOB conexões e potência de processamento de saudação duplo.

Algumas edições do BizTalk não oferecem uma opção de escala. Nesta situação, uma unidade é permitida. toodetermine quantas unidades sua edição pode ser dimensionada, consulte muito[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md).

Aumentar Olá número de unidades pode afetar os preços. Se você aumentar Olá unidades, selecionando **salvar** exibe uma mensagem que informa se a cobrança é afetada. Você, em seguida, escolha toocontinue. Quando você aumenta o número de saudação de unidades, Olá status do BizTalk Service muda de ativo tooUpdating. Olá estado de atualização, o BizTalk Service continua toorun.

[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md) define uma “Unidade”.

## <a name="configure"></a>Configurar
Não se aplica a conexões de tooHybrid.

Define Olá tooNone de Status de Backup ou automático. Quando definido como tooNone, não há backups são criados automaticamente. Quando definido como tooAutomatic, configurar o local de backup hello, frequência de saudação de backup hello e quanto tempo tookeep Olá os arquivos de backup. 

[Serviços BizTalk: Backup e restauração](biztalk-backup-restore.md) fornece detalhes de saudação. 

## <a name="HybridConnections"></a>Conexões Híbridas
As conexões híbridas conectam a um aplicativo do Azure, como aplicativos Web ou aplicativos móveis no serviço de aplicativo do Azure, recurso de local de tooan que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP e mais serviços da Web personalizados. Conexões híbridas são gerenciadas nos Serviços BizTalk no hello portal clássico do Azure.

toocreate conexões híbridas no serviço de aplicativo do Azure, consulte [acessar recursos usando conexões híbridas no serviço de aplicativo do Azure locais](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate ou gerenciar conexões híbridas Serviços BizTalk do Azure, consulte [conexões híbridas](integration-hybrid-connection-overview.md).

## <a name="next"></a>Avançar
Agora que você está familiarizado com guias diferentes hello, você pode aprender mais sobre os recursos de Serviços BizTalk do Azure hello:

* [Serviços BizTalk: limitação](biztalk-throttling-thresholds.md)  
* [Serviços BizTalk: nome e chave do emissor](biztalk-issuer-name-issuer-key.md)  
* [Serviços BizTalk: backup e restauração](biztalk-backup-restore.md)

## <a name="see-also"></a>Consulte também
* [Conexões Híbridas](integration-hybrid-connection-overview.md)  
* [Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium](biztalk-editions-feature-chart.md)  
* [Serviços BizTalk: provisionamento usando o portal clássico do Azure](biztalk-provision-services.md)  
* [Serviços BizTalk: gráfico de estado do Serviço do BizTalk (a página pode estar em inglês)](biztalk-service-state-chart.md)  
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

