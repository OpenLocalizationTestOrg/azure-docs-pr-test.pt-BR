---
title: aaaMonitor disponibilidade e capacidade de resposta de qualquer site da web | Microsoft Docs
description: "Configure testes da web no Application Insights. Obtenha alertas se um site fica indisponível ou responde lentamente."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>Monitorar a disponibilidade e a capacidade de resposta de qualquer site
Depois que você implantou o aplicativo web ou o servidor de tooany do site da web, você pode configurar testes toomonitor sua disponibilidade e capacidade de resposta. [Informações de aplicativo do Azure](app-insights-overview.md) envia solicitações da web aplicativo tooyour em intervalos regulares de pontos ao redor Olá, mundo. Ele o alertará se o aplicativo não responder ou responder lentamente.

Você pode configurar testes de disponibilidade para qualquer HTTP ou Olá de ponto de extremidade HTTPS que seja acessível pela internet pública. Você não tem tooadd nada toohello web site que você está testando. Ele não tem nem mesmo toobe seu site: você pode testar um serviço da API REST do qual você depende.

Há dois tipos de testes de disponibilidade:

* [Teste de ping de URL](#create): um teste simples que você pode criar no hello portal do Azure.
* [Teste da web de várias etapas](#multi-step-web-tests): que você cria no Visual Studio Enterprise e carregamento toohello portal.

Você pode criar até too25 testes de disponibilidade por recursos de aplicativo.

## <a name="create"></a>1. Abrir um recurso para os seus relatórios de teste de disponibilidade

**Se você já tiver configurado o Application Insights** para seu aplicativo web, abra o recurso do Application Insights no hello [portal do Azure](https://portal.azure.com).

**Ou, se você quiser toosee seus relatórios em um novo recurso,** inscrever-se muito[Microsoft Azure](http://azure.com), vá toohello [portal do Azure](https://portal.azure.com)e crie um recurso do Application Insights.

![Novo > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Clique em **todos os recursos** tooopen folha de visão geral de saudação para o novo recurso de saudação.

## <a name="setup"></a>2. Criar um teste de ping de URL
Abra a folha de disponibilidade hello e adicionar um teste.

![Preenchimento Olá pelo menos uma URL de seu site](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **Olá URL** pode ser qualquer página da web você deseja tootest, mas ele deve ser visível do hello internet pública. URL de saudação pode incluir uma cadeia de caracteres de consulta. Por exemplo, você pode utilizar um pouco seu banco de dados. Se a URL de saudação resolver tooa redirecionamento, podemos acompanhamento-too10 redirecionamentos.
* **Analisar solicitações dependentes**: se esta opção estiver marcada, o teste Olá solicitações imagens, scripts, arquivos de estilo e outros arquivos que fazem parte da página da web de saudação em teste. Olá tempo de resposta inclui Olá tempo tooget esses arquivos. teste de saudação falhará se todos esses recursos não podem ser baixados com êxito no tempo limite de saudação para teste inteira hello. 

    Se a opção de saudação não estiver marcada, teste Olá solicita somente arquivo Olá Olá URL especificado.
* **Habilitar novas tentativas**: se esta opção estiver marcada, quando Olá teste falhar, ele é repetido após um breve intervalo. Uma falha só será relatada se três tentativas sucessivas falharem. Testes subsequentes, em seguida, são executadas na frequência de teste normal hello. Repetição é suspenso temporariamente até obter êxito Avançar hello. Essa regra é aplicada independentemente em cada local de teste. Recomendamos essa opção. Em média, aproximadamente 80% das falhas desaparecem na repetição.
* **Frequência de teste**: define a frequência hello teste é executado em cada local de teste. Com uma frequência de cinco minutos e cinco locais de teste, seu site é testado em média a cada minuto.
* **Locais de teste** são Olá coloca de onde nossos servidores enviam URL de tooyour solicitações da web. Escolha dois ou três para que você possa diferenciar problemas no site de problemas da rede. Você pode selecionar os locais de too16.
* **Critérios de sucesso**:

    **Tempo limite do teste**: diminuir esse toobe valor alertado sobre respostas lentas. teste de saudação é contado como uma falha se as respostas de saudação do seu site não foram recebidas dentro desse período. Se você selecionou **analisar solicitações dependentes**, em seguida, todos os Olá imagens, arquivos de estilo, scripts e outros recursos dependentes devem ter sido recebidos dentro desse período.

    **Resposta HTTP**: Olá retornada o código de status que é considerado um sucesso. 200 é o código de saudação que indica que uma página da web normal foi retornado.

    **Correspondência de conteúdo**: uma cadeia de caracteres como "Bem-vindo!" Faremos o teste que uma correspondência exata de maiúsculas e minúsculas ocorre em todas as respostas. É necessário que seja uma cadeia de caracteres simples, sem curingas. Não se esqueça de que, se as alterações de conteúdo de página que você pode ter tooupdate-lo.
* **Alertas** são, por padrão, enviadas tooyou se houver falhas em três locais em cinco minutos. É uma falha em um local toobe provavelmente um problema de rede e não é um problema com seu site. Mas você pode alterar Olá limite toobe mais ou menos confidenciais e você pode também alterar quem Olá emails deve ser enviado para.

    Você pode configurar um [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) , que é chamado quando um alerta é gerado. (Mas observe que, no momento, os parâmetros de consulta não são passados como Propriedades.)

### <a name="test-more-urls"></a>Testar mais URLs
Adicione mais testes. Por exemplo, na inclusão tootesting sua home page, você pode verificar se que seu banco de dados está em execução testando Olá URL para uma pesquisa.


## <a name="monitor"></a>3. Ver os resultados de teste de disponibilidade

Depois de alguns minutos, clique em **atualizar** toosee resultados de teste. 

![Resumo de resultados na folha de saudação inicial](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Olá scatterplot mostra exemplos de saudação resultados de teste que possuem os detalhes de etapa de teste de diagnóstico. o mecanismo de teste Olá armazena detalhes de diagnóstico para testes que apresentam falhas. Para testes bem-sucedida, detalhes de diagnóstico é armazenado para um subconjunto de execuções de saudação. Passe o mouse sobre qualquer uma das Olá verde/vermelho pontos toosee Olá teste timestamp, duração do teste, local e nome do teste. Clique em qualquer ponto nos detalhes da saudação dispersão plotagem toosee Olá Olá do resultado de teste.  

Selecione um teste específico, local, ou reduza o tempo de saudação toosee período mais resultados em torno de saudação período de interesse. Usar os resultados da pesquisa Explorer toosee de todas as execuções ou usar relatórios personalizados da análise consultas toorun nesses dados.

Nos resultados brutos da adição toohello, existem duas métricas de disponibilidade no Metrics Explorer: 

1. Disponibilidade: Porcentagem de testes de saudação que foram bem-sucedidas em todas as execuções de teste. 
2. Duração do teste: duração média em todas as execuções de teste.

Você pode aplicar filtros em nome do teste hello, tendências de tooanalyze de local de um teste específico e/ou local.

## <a name="edit"></a>Como inspecionar e editar testes

Na página de resumo de hello, selecione um teste específico. Lá, você pode ver seus resultados específicos e editar ou desabilitá-los temporariamente.

![Editar ou desabilitar um teste na Web](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

Talvez você queira toodisable testes de disponibilidade ou alerta Olá regras associadas a eles enquanto você estiver executando manutenção em seu serviço. 

## <a name="failures"></a>Se você encontrar falhas
Clique em um ponto vermelho.

![Clique em um ponto vermelho](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


De um resultado do teste de disponibilidade, você pode:

* Inspecione a resposta Olá recebida do servidor.
* Abra a telemetria Olá enviada pelo seu aplicativo de servidor durante o processamento da instância de solicitação com falha hello.
* Faça um problema ou item de trabalho de problema de saudação tootrack Git ou VSTS. bug Olá conterá um evento de toothis de link.
* Abra o resultado do teste da web hello no Visual Studio.


*Parece correto, mas é relatado como uma falha?* Verifique todas as imagens de hello, scripts, folhas de estilo e outros arquivos carregados por página hello. Se qualquer um deles falhar, teste de saudação é reportado com falha, mesmo se a página de html principal Olá carrega Okey.

*Não há itens relacionados?* Se você o Application Insights está configurado para seu aplicativo do lado do servidor, talvez seja porque a [amostragem](app-insights-sampling.md) está em operação. 

## <a name="multi-step-web-tests"></a>Testes na Web com diversas etapas
Você pode monitorar um cenário que envolve uma sequência de URLs. Por exemplo, se você estiver monitorando um site de vendas, você pode testar que adicionar itens toohello carrinho de compras está funcionando corretamente.

> [!NOTE] 
> Há uma cobrança para testes na Web de várias etapas. [Esquema de preços](http://azure.microsoft.com/pricing/details/application-insights/).
> 

toocreate um teste de várias etapa, você registrar o cenário Olá usando o Visual Studio Enterprise e carregue Olá gravação tooApplication Insights. Repete o cenário de saudação em intervalos do Application Insights e verifica as respostas de saudação.

> [!NOTE]
> Não é possível usar funções codificadas nem loops nos seus testes. teste Olá deve estar contido no script de WebTest Olá completamente. No entanto, você pode usar plug-ins-padrão.
>

#### <a name="1-record-a-scenario"></a>1. Registrar um cenário
Use o Visual Studio Enterprise toorecord uma sessão de web.

1. Crie um projeto de teste de desempenho na Web.

    ![Na edição Enterprise do Visual Studio, crie um projeto de modelo de teste de carga e desempenho na Web hello.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Não consegue ver hello desempenho da Web e o modelo de teste de carga?* - Feche o Visual Studio Enterprise. Abra **instalador do Visual Studio** toomodify sua instalação do Visual Studio Enterprise. Em **Componentes Individuais**, selecione **Ferramentas de teste de carga e desempenho na Web**.

2. Abrir o arquivo de WebTest hello e começar a registrar.

    ![Abrir o arquivo de WebTest hello e clique em registro.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Olá ações do usuário que você deseja toosimulate em seu teste: Abra o seu site, adicione um carrinho de toohello do produto e assim por diante. Em seguida, interrompa seu teste.

    ![Olá web execuções de gravador de teste no Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    Não crie um cenário longo. Há um limite de 100 etapas e 2 minutos.
4. Edite o teste de saudação para:

   * Adicione validações toocheck códigos de texto e a resposta do hello recebida.
   * Remover todas as interações supérfluas. Você também pode remover solicitações dependentes para imagens ou tooad ou controle de sites.

     Lembre-se de que você só pode editar o script de teste Olá - você não pode adicionar código personalizado ou chamar outros testes da web. Não insira loops em teste hello. Você pode usar plug-ins de teste da Web padrão.
5. Execute o teste de saudação no Visual Studio toomake se que ele funciona.

    executor de testes da web Hello abre um navegador da web e repetições Olá ações gravadas. Verifique se ele funciona conforme o esperado.

    ![No Visual Studio, abra Olá webtest arquivo e clique em executar.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Carregar Olá web teste tooApplication Insights
1. No portal do Application Insights hello, crie um teste da web.

    ![Na folha de testes da web de saudação, escolha Adicionar.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Selecione várias etapa teste e carregar o arquivo. webtest hello.

    ![Selecione teste da Web em várias etapas.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Locais de teste de saudação do conjunto, a frequência e parâmetros de alerta no hello mesma forma para ping testa.

#### <a name="3-see-hello-results"></a>3. Ver os resultados de saudação

Exibir o teste de resultados e falhas em Olá mesmos testes de maneira como url única.

Além disso, você pode baixar tooview de resultados de teste Olá-los no Visual Studio.

#### <a name="too-many-failures"></a>Muitas falhas?

* Um motivo comum para a falha é que esse teste Olá é executado muito longo. Ele não deve ser executado por mais de dois minutos.

* Não se esqueça de que todos os recursos de saudação de uma página devem carregar corretamente para Olá toosucceed de teste, incluindo scripts, folhas de estilo, imagens e assim por diante.

* Olá teste da web deve estar totalmente contido no script de WebTest Olá: você não pode usar funções codificadas no teste de saudação.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Conectando a hora e números aleatórios em seu teste de várias etapas
Suponha que você está testando uma ferramenta que obtém dados dependentes de tempo, como estoques de um feed externo. Quando você registra seu teste da web, você tem horários específicos toouse, mas defini-los como parâmetros de saudação de teste, StartTime e EndTime.

![Um teste da Web com parâmetros.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Quando você executa o teste de saudação, você gostaria que EndTime sempre toobe Olá apresentar tempo e StartTime deve ser de 15 minutos atrás.

Plug-ins de teste da Web fornecem a maneira de saudação toodo parametrizar vezes.

1. Adicione um plug-in de teste na Web para cada valor de parâmetro variável desejado. Em ferramentas de teste de web hello, escolha **adicionar Web teste plug-in**.

    ![Escolha Adicionar plug-ins de teste da Web e selecione um tipo.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    Neste exemplo, podemos usar duas instâncias do hello plug-in de tempo de data. É uma instância de "15 minutos atrás" e outra de "agora".
2. Abra as propriedades de saudação de cada plug-in. Dê um nome e defina-Olá toouse hora atual. Para um deles, defina Add Minutes = -15.

    ![Definir nome, Usar hora atual e Adicionar minutos.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. Nos parâmetros de teste de web hello, use {{nome do plug-in}} tooreference um nome de plug-in.

    ![No parâmetro de teste de hello, use {{nome do plug-in}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

Agora, carregue o portal de toohello de teste. Ele usa valores dinâmicos Olá em cada execução de teste de saudação.

## <a name="dealing-with-sign-in"></a>Lidando com a entrada
Se seus usuários entrarem no aplicativo tooyour, você tem várias opções para simular entrar para que você possa testar páginas Olá entrar. abordagem de Olá que usar depende de tipo de saudação da segurança fornecida pelo aplicativo hello.

Em todos os casos, você deve criar uma conta no seu aplicativo para o objetivo de saudação do teste. Se possível, restrinja permissões de saudação dessa conta de teste para que não há nenhuma possibilidade de testes da web de saudação afetando usuários reais.

### <a name="simple-username-and-password"></a>Senha e nome de usuário simples
Gravar um teste da web no hello maneira normal. Exclua os cookies primeiro.

### <a name="saml-authentication"></a>Autenticação de SAML
Use Olá SAML plug-in que está disponível para testes da web.

### <a name="client-secret"></a>Segredo do cliente
Se seu aplicativo tiver uma rota de entrada que envolva um segredo do cliente, use-a. O AAD (Azure Active Directory) é um exemplo de um serviço que fornece uma entrada de segredo do cliente. No AAD, segredo do cliente Olá é hello chave do aplicativo.

Aqui está um teste na Web de exemplo de um aplicativo Web que usa uma chave de aplicativo:

![Exemplo de segredo do cliente](./media/app-insights-monitor-web-app-availability/110.png)

1. Obtenha o token do AAD usando o segredo do cliente (AppKey).
2. Extraia o token de portador da resposta.
3. Chame API usando o token de portador no cabeçalho de autorização de saudação.

Certifique-se de que o teste da web de saudação é um cliente real – ou seja, tem seu próprio aplicativo no AAD - e use seu clientId + appkey. O serviço em teste também tem seu próprio aplicativo no AAD: Olá appID URI desse aplicativo é refletido Olá em teste na web no campo de "recurso" hello.

### <a name="open-authentication"></a>Autenticação Aberta
Um exemplo de autenticação aberta é entrar com sua conta da Microsoft ou do Google. Muitos aplicativos que use OAuth fornecem Olá alternativa de segredo do cliente, portanto, sua primeira tática deve ser tooinvestigate, dessa possibilidade.

Se o teste deve se conectar usando o OAuth, é a abordagem geral de saudação:

* Use uma ferramenta como o tráfego de saudação do Fiddler tooexamine entre o navegador da web, o site de autenticação hello e seu aplicativo.
* Executar dois ou mais entradas usando máquinas diferentes ou navegadores, ou em intervalos de tempo (tooallow tokens tooexpire).
* Comparando sessões diferentes, identifique o token Olá passado de volta de saudação autenticação de site, que é então passado de servidor de aplicativo tooyour depois de entrar.
* Registre um teste na Web usando o Visual Studio.
* Parametrize tokens hello, definindo o parâmetro hello quando Olá token é retornado do autenticador de saudação e usá-lo no site de toohello consulta hello.
  (O visual Studio tentativas de teste de saudação tooparameterize, mas não parametriza tokens Olá corretamente.)


## <a name="performance-tests"></a>Testes de desempenho
Você pode executar um teste de carga em seu site. Como teste de disponibilidade hello, você pode enviar solicitações simples ou solicitações de várias etapas do nosso pontos ao redor Olá, mundo. Diferentemente de um teste de disponibilidade, muitas solicitações são enviadas, simulando vários usuários simultâneos.

Na folha de visão geral do hello, abra **configurações**, **testes de desempenho**. Quando você cria um teste, você está convidado tooconnect tooor criar uma conta do Visual Studio Team Services.

Quando o teste de saudação for concluído, serão exibidas tempos de resposta e taxas de sucesso.


![Teste de desempenho](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> efeitos de saudação tooobserve de um teste de desempenho, use [fluxo ao vivo](app-insights-live-stream.md) e [Profiler](app-insights-profiler.md).
>

## <a name="automation"></a>Automação
* [Use o PowerShell scripts tooset a um teste de disponibilidade](app-insights-powershell.md#add-an-availability-test) automaticamente.
* Configure um [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) , que é chamado quando um alerta é gerado.

## <a name="qna"></a>Dúvidas? Problemas?
* *Posso chamar o código através do meu teste na Web?*

    Não. etapas de saudação do teste Olá devem ser no arquivo de WebTest hello. E não é possível chamar outros testes da Web nem usar loops. Porém, há vários plug-ins que podem ser úteis.
* *Há suporte para HTTPS?*

    Damos suporte a TLS 1.1 e TLS 1.2.
* *Há diferença entre "testes na Web" e "testes de disponibilidade"?*

    Olá dois termos pode ser referenciado alternadamente. Testes de disponibilidade é um termo mais genérico que inclui o ping de URL única Olá além de testes toohello testes de web de várias etapas.
* *Eu gostaria de testes de disponibilidade toouse em nosso servidor interno que é executado atrás de um firewall.*

    Há duas soluções possíveis:
    
    * Configurar seu firewall toopermit as solicitações de entrada hello [agentes de teste de endereços IP dos nossos web](app-insights-ip-addresses.md).
    * Escreva seu próprio código tooperiodically teste interno do servidor. Execute o código de saudação como um processo em segundo plano em um servidor de teste por trás do firewall. O processo de teste pode enviar tooApplication ideias de seus resultados usando [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API no pacote do hello core SDK. Isso requer que seu teste server toohave saído acesso toohello Application Insights inclusão ponto de extremidade, mas isso é um risco de segurança muito menor do que a alternativa de saudação do permitir solicitações de entrada. resultados de saudação não serão exibidos no hello disponibilidade web testes folhas, mas aparecerá como resultados de disponibilidade no Explorer de métrica, pesquisa e análise.
* *Falha de carregamento de um teste na Web de várias etapas*

    Há um limite de tamanho de 300 K.

    Não há suporte para loops.

    Não há suporte para referências tooother web testes.

    Não há suporte para fontes de dados.
* *O teste de várias etapas não foi concluído*

    Há um limite de 100 solicitações por teste.

    teste de saudação será interrompido se ele for executado mais de dois minutos.
* *Como executar um teste com certificados de cliente*

    Não há suporte para isso, infelizmente.


## <a name="next"></a>Próximas etapas
[Pesquisar logs de diagnóstico][diagnostic]

[Solução de problemas][qna]

[Endereços IP de agentes de teste Web](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
