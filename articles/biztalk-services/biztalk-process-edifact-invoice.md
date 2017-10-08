---
title: "Tutorial: Processar faturas EDIFACT usando os Serviços BizTalk do Azure | Microsoft Docs"
description: "Como toocreate e configurar o aplicativo de API ou conector de caixa hello e usá-lo em um aplicativo lógico no serviço de aplicativo do Azure"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Tutorial: Processar faturas EDIFACT usando os Serviços BizTalk do Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Você pode usar tooconfigure do Portal de Serviços BizTalk hello e implantar acordos X12 e EDIFACT. Neste tutorial, examinaremos como toocreate um acordo EDIFACT para a troca de faturas entre parceiros comerciais. Este tutorial foi escrito em torno de uma solução comercial de ponta a ponta envolvendo dois parceiros comerciais, Northwind e Contoso, que trocam mensagens EDIFACT.  

## <a name="sample-based-on-this-tutorial"></a>Exemplo baseado neste tutorial
Este tutorial foi escrito em torno de uma amostra, **enviar EDIFACT faturas usando serviços do BizTalk**, que é toodownload disponível da saudação [Galeria de códigos do MSDN](http://go.microsoft.com/fwlink/?LinkId=401005). Você pode usar o exemplo hello e percorrer este tutorial toounderstand como exemplo hello foi criado. Ou, você pode usar este tutorial toocreate sua própria solução de início. Este tutorial é destinado a saudação segunda abordagem para que você entenda como esta solução foi criada. Além disso, tanto quanto possível, o tutorial Olá é consistente com o exemplo hello e usa Olá os mesmos nomes para artefatos (por exemplo, esquemas, transformações) conforme usado no exemplo hello.  

> [!NOTE]
> Como esta solução envolve o envio de uma mensagem de uma ponte EDI de tooan de ponte EAI, ele reutiliza Olá [BizTalk Services Bridge chaining exemplo](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) exemplo.  
> 
> 

## <a name="what-does-hello-solution-do"></a>O que a solução Olá fazer?
Nesta solução, a Northwind recebe faturas EDIFACT da Contoso. As faturas não estão em formato EDI padrão. Portanto, antes de enviar Olá fatura tooNorthwind, deve ser transformado tooan documento de fatura (também chamado INVOIC) de EDIFACT. Após o recebimento, Northwind deve processar a fatura EDIFACT de saudação e retornar um tooContoso de mensagem (também chamada CONTRL) do controle.

![][1]  

tooachieve neste cenário de negócios, a Contoso usa recursos de saudação fornecidos com Serviços BizTalk do Microsoft Azure.

* A Contoso utiliza EAI pontes tootransform Olá original da fatura tooEDIFACT INVOIC.
* ponte EAI Olá envia tooan de mensagem de saudação EDI enviar ponte implantada como parte de um acordo configurado no hello Portal de Serviços BizTalk.
* ponte de envio EDI Olá processa Olá EDIFACT INVOIC e encaminha tooNorthwind.
* Após o recebimento da fatura hello, a Northwind devolve uma toohello de mensagem CONTRL implantado como parte do contrato de saudação de ponte de recebimento EDI.  

> [!NOTE]
> Opcionalmente, essa solução também demonstra como toouse envio em lote toosend Olá faturas em lotes, em vez de enviar cada fatura separadamente.  
> 
> 

cenário de saudação toocomplete, usamos filas do barramento de serviço toosend fatura da Contoso tooNorthwind ou receber a confirmação da Northwind. Essas filas podem ser criadas usando um aplicativo cliente, que está disponível como um download e está incluído no pacote de exemplo hello que está disponível como parte deste tutorial.  

## <a name="prerequisites"></a>Pré-requisitos
* Você deve ter um namespace do Barramento de Serviço. Para obter instruções sobre como criar um namespace, confira [Como criar ou modificar um namespace do Barramento de Serviço](https://msdn.microsoft.com/library/azure/hh674478.aspx). Vamos supor que você já tenha um namespace de Barramento de serviço provisionado, chamado **edifactbts**.
* Você deve ter uma assinatura dos Serviços BizTalk. Para obter instruções, confira [Criar um Serviço BizTalk usando o portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=302280). Para este tutorial, suponhamos que você tenha uma assinatura dos Serviços BizTalk chamada **contosowabs**.
* Registre sua assinatura do BizTalk Services Olá Portal de Serviços BizTalk. Para obter instruções, consulte [registrar uma implantação do serviço BizTalk no hello Portal de Serviços BizTalk](https://msdn.microsoft.com/library/hh689837.aspx)
* Você deve ter o Visual Studio instalado.
* Você deve ter o SDK dos Serviços BizTalk instalado. Você pode baixar Olá SDK em [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Etapa 1: Criar hello filas do barramento de serviço
Esta solução usa mensagens de tooexchange de filas do barramento de serviço entre parceiros comerciais. Contoso e Northwind enviam mensagens de filas de toohello de onde as pontes EAI e/ou EDI de saudação consumam-los. Para essa solução, você precisa de três filas do Barramento de Serviço:

* **northwindreceive** – a Northwind recebe faturas Olá da Contoso através desta fila.
* **contosoreceive** – Contoso recebe a confirmação de saudação da Northwind através desta fila.
* **suspenso** – todas as mensagens suspensas são roteadas toothis fila. As mensagens são suspensas quando falham durante o processamento.

Você pode criar essas filas do barramento de serviço usando um aplicativo cliente incluído no pacote de exemplo hello.  

1. Saudação do local de onde você baixou o exemplo hello, abra **Tutorial enviando faturas usando BizTalk Services EDI Bridges.sln**.
2. Pressione **F5** toobuild e início Olá **Tutorial do cliente** aplicativo.
3. Na tela hello, insira o namespace de barramento de serviço ACS Olá, nome do emissor e chave do emissor.
   
   ![][2]  
4. Uma caixa de mensagem solicitará a criação de três filas no namespace do Barramento de Serviço. Clique em **OK**.
5. Deixe Olá Tutorial cliente está em execução. Abra hello, clique em **Service Bus** > ***seu namespace do barramento de serviço*** > **filas**e verifique se que as filas de saudação três são criadas.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Etapa 2: Criar e implantar o acordo entre parceiros comerciais
Crie um acordo entre os parceiros comerciais Contoso e Northwind. Um contrato de parceiro comercial define um contrato comercial entre os parceiros de negócios Olá dois, como quais toouse do esquema de mensagem, que mensagens toouse de protocolo, etc. Um acordo entre parceiros comerciais inclui duas pontes EDI, um toosend mensagens tootrading parceiros (chamado hello **ponte de envio EDI**) e um tooreceive mensagens dos parceiros comerciais (chamado hello **ponte de recebimento de EDI**).

No contexto de saudação dessa solução, ponte de envio EDI Olá corresponde toohello no lado de envio do contrato hello e é usado toosend Olá EDIFACT fatura da Contoso tooNorthwind. Da mesma forma, ponte de recebimento Olá EDI corresponde toohello do lado receptor do contrato hello e é usado tooreceive confirmações da Northwind.  

### <a name="create-hello-trading-partners"></a>Criar hello parceiros comerciais
toostart, crie parceiros comerciais para a Contoso e Northwind.  

1. Em Olá Portal de serviços do BizTalk em Olá **parceiros** , clique em **adicionar**.
2. Na página Olá novo parceiro, insira **Contoso** como um nome de parceiro e clique **salvar**.
3. Olá repetição etapa toocreate Olá segundo parceiro, **Northwind**.  

### <a name="create-hello-agreement"></a>Criar contrato Olá
Acordos entre parceiros comerciais são criados entre os perfis comerciais dos parceiros comerciais. Esta solução usa perfis de parceiros do saudação padrão que são criados automaticamente quando criamos os parceiros de saudação.  

1. No Portal de Serviços BizTalk do hello, clique em **contratos** > **adicionar**.
2. Do Olá novo contrato **configurações gerais** página, especifique valores hello, conforme mostrado na imagem de saudação abaixo e, em seguida, clique em **continuar**.
   
   ![][3]  
   
   Depois de clicar em **Continuar**, duas guias, **Configurações de Recebimento** e **Configurações de Envio**, se tornarem disponíveis.
3. Crie contrato de envio de saudação entre a Contoso e Northwind. Este acordo regulamenta a forma como a Contoso envia tooNorthwind de fatura EDIFACT hello.
   
   1. Clique em **Configurações de Envio**.
   2. Manter valores padrão Olá Olá **URL de entrada**, **transformação**, e **lote** guias.
   3. Em Olá **protocolo** guia, em Olá **esquemas** seção, carregue Olá **EFACT_D93A_INVOIC.xsd** esquema. Esse esquema está disponível com o pacote de exemplo hello.
      
      ![][4]  
   4. Em Olá **transporte** guia, especifique os detalhes de saudação para filas de barramento de serviço hello. Olá acordo de envio, usamos Olá **northwindreceive** toosend Olá EDIFACT fatura tooNorthwind da fila e Olá **suspenso** fila tooroute quaisquer mensagens que falham durante o processamento e são suspenso. Criar estas filas em **etapa 1: criar hello filas do barramento de serviço** (neste tópico).
      
      ![][5]  
      
      Em **configurações de transporte > tipo de transporte** e **configurações de suspensão de mensagem > tipo de transporte**, selecione o barramento de serviço do Azure e fornecem valores hello conforme mostrado na imagem de saudação.
4. Criar hello receber contrato entre a Contoso e Northwind. Este acordo regulamenta a forma como a Contoso recebe a confirmação de saudação da Northwind.
   
   1. Clique em **Configurações de Recebimento**.
   2. Manter valores padrão Olá Olá **transporte** e **transformação** guias.
   3. Em Olá **protocolo** guia, em Olá **esquemas** seção, carregue Olá **EFACT_4.1_CONTRL.xsd** esquema. Esse esquema está disponível com o pacote de exemplo hello.
   4. Em Olá **rota** guia, crie um filtro tooensure que somente as confirmações da Northwind são roteada tooContoso. Em **configurações de rota**, clique em **adicionar** toocreate Olá filtro de roteamento.
      
      ![][6]  
      
      1. Forneça valores para o **o nome da regra**, **regra de rota**, e **destino da rota** conforme mostrado na imagem de saudação.
      2. Clique em **Salvar**.
   5. Em Olá **rota** guia novamente, especifique onde as confirmações suspensas (confirmações que apresentaram falha durante o processamento) são roteadas. Definido tooAzure de tipo de transporte Olá barramento de serviço, tipo de destino de rota muito**fila**, tipo de autenticação muito**assinatura de acesso compartilhado** (SAS), fornecem a cadeia de conexão SAS Olá para Olá barramento de serviço namespace e, em seguida, digite o nome de fila de saudação como **suspenso**.
5. Por fim, clique em **implantar** toodeploy contrato de saudação. Observação Olá pontos de extremidade onde Olá enviar e receber contratos implantados.
   
   * Em Olá **configurações de envio** guia em **URL de entrada**, observe o ponto de extremidade de saudação. toosend uma mensagem da Contoso tooNorthwind usando Olá ponte de envio de EDI, você deve enviar um ponto de extremidade de toothis de mensagem.
   * Em Olá **configurações de recebimento** guia em **transporte**, observe o ponto de extremidade de saudação. ponte de recebimento toosend uma mensagem da Northwind tooContoso usando Olá EDI, você deve enviar um ponto de extremidade de toothis de mensagem.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Etapa 3: Criar e implantar o projeto de Serviços BizTalk Olá
Na etapa anterior de saudação, você implantou Olá EDI enviar e receber contratos tooprocess faturas e confirmações EDIFACT. Esses contratos podem processar apenas mensagens em conformidade com o esquema de mensagem EDIFACT padrão toohello. No entanto, por cenário Olá para esta solução, a Contoso envia um tooNorthwind fatura em um esquema de propriedade in-house. Portanto, antes de mensagem de saudação é enviada toohello ponte de envio de EDI, ela deve ser transformada do esquema de fatura do hello esquema in-house toohello padrão EDIFACT. projeto do BizTalk Services EAI Olá faz isso.

projeto de Serviços BizTalk Hello, **InvoiceProcessingBridge**, transformações Olá mensagem também é incluído como parte do exemplo hello baixado. projeto de saudação inclui Olá artefatos a seguir:

* **INHOUSEINVOICE. XSD** – esquema da fatura in-house de saudação enviada tooNorthwind.
* **EFACT_D93A_INVOIC. XSD** – esquema da fatura padrão do EDIFACT hello.
* **EFACT_4.1_CONTRL. XSD** – esquema da confirmação do EDIFACT Olá Northwind envia tooContoso.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** – Olá transformação que mapeia Olá fatura in-house toohello padrão EDIFACT fatura esquema.  

### <a name="create-hello-biztalk-services-project"></a>Criar projeto de Serviços BizTalk Olá
1. Em Olá solução do Visual Studio, expanda o projeto InvoiceProcessingBridge de saudação e abra Olá **MessageFlowItinerary.bcs** arquivo.
2. Clique em qualquer lugar na tela hello e defina Olá **URL do serviço BizTalk** em Olá toospecify da caixa de propriedade nome da sua assinatura dos Serviços BizTalk. Por exemplo: `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Na caixa de ferramentas hello, arraste um **Xml One-Way Bridge** toohello tela. Saudação de conjunto **nome da entidade** e **endereço relativo** ligar as propriedades de saudação muito**ProcessInvoiceBridge**. Clique duas vezes em **ProcessInvoiceBridge** tooopen superfície de configuração de ponte de saudação.
4. Dentro de saudação **tipos de mensagem** , clique em Olá adição (**+**) esquema de saudação do botão toospecify da mensagem de entrada hello. Porque a mensagem de entrada hello para Olá ponte EAI é sempre fatura in-house hello, defina muito**INHOUSEINVOICE**.
   
   ![][8]  
5. Clique Olá **transformação Xml** forma e na caixa de propriedade hello, para Olá **mapas** propriedade, clique botão de reticências hello (**...** ) botão. Em Olá **seleção de mapas** caixa de diálogo, selecione Olá **INHOUSEINVOICE_to_D93AINVOIC** arquivo de transformação e, em seguida, clique em **Okey**.
   
   ![][9]  
6. Voltar muito**MessageFlowItinerary.bcs**e na caixa de ferramentas hello, arraste um **ponto de extremidade de serviço externo bidirecional** toohello direito da saudação **ProcessInvoiceBridge**. Definir seu **nome da entidade** propriedade muito**EDIBridge**.
7. No hello Gerenciador de soluções, expanda Olá **MessageFlowItinerary.bcs** e clique duas vezes em Olá **edibridge. config** arquivo. Substituir conteúdo Olá Olá **edibridge. config** com os seguintes hello.
   
   > [!NOTE]
   > Por que preciso de arquivo do tooedit hello. config? ponto de extremidade de serviço externo de saudação que adicionamos toohello tela do designer de ponte representa pontes EDI Olá que foi implantada anteriormente. As pontes EDI são bidirecionais, com lado de envio e de recebimento. No entanto, hello ponte EAI que adicionamos toohello designer de ponte é uma ponte unidirecional. Então, padrões de troca de toohandle Olá mensagem diferente de duas pontes de hello, usamos um comportamento de ponte personalizado, incluindo sua configuração no arquivo. config de saudação. Além disso, o comportamento personalizado Olá também lida com hello toohello EDI enviar ponte do ponto de extremidade. Este comportamento personalizado está disponível como uma amostra individual no [BizTalk Services Bridge chaining sample - EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Esta solução reutiliza o exemplo hello.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Atualizar detalhes de configuração do hello edibridge. config arquivo tooinclude
   
   * Em  *<behaviors>* , forneça Olá namespace do ACS e chave associada a saudação assinatura dos Serviços BizTalk.
   * Em  *<client>* , fornecer Olá de ponto de extremidade onde Olá contrato de envio de EDI é implantado.
   
   Salvar as alterações e feche o arquivo de configuração de saudação.
9. De saudação da caixa de ferramentas, clique em Olá **conector** e junção hello **ProcessInvoiceBridge** e **EDIBridge** componentes. Selecione o conector hello e na caixa de propriedades, defina **condição de filtro** muito**corresponder tudo**. Isso garante que todas as mensagens processadas por Olá ponte EAI sejam roteadas toohello ponte EDI.
   
   ![][10]  
10. Salve alterações toohello solução.  

### <a name="deploy-hello-project"></a>Implantar projeto Olá
1. No computador de saudação em que você criou o projeto de Serviços BizTalk hello, baixe e instale o certificado SSL da saudação para sua assinatura dos Serviços BizTalk. Em Serviços BizTalk, clique em **Painel** e em **Baixar Certificado SSL**. Clique duas vezes no certificado hello e siga Olá toocomplete prompt Olá instalação. Certifique-se de instalar o certificado Olá sob **autoridades de certificação raiz confiáveis** repositório de certificados.
2. No Gerenciador de soluções do Visual Studio, clique com botão direito Olá **InvoiceProcessingBridge** do projeto e, em seguida, clique em **implantar**.
3. Forneça valores hello conforme mostrado na imagem hello e, em seguida, clique em **implantar**. Você pode obter credenciais Olá ACS para os serviços do BizTalk clicando **informações de Conexão** do painel de controle de Serviços BizTalk hello.
   
   ![][11]  
   
   No painel de saída de hello, copiar o ponto de extremidade de saudação onde Olá ponte EAI é implantado, por exemplo, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. Você precisará dessa URL de ponto de extremidade mais tarde.  

## <a name="step-4-test-hello-solution"></a>Etapa 4: Testar a solução de saudação
Neste tópico, vamos examinar como tootest Olá solução usando Olá **Tutorial do cliente** aplicativo fornecido como parte do exemplo hello.  

1. No Visual Studio, pressione F5 toostart Olá **Tutorial do cliente**.
2. tela Hello deve ter valores hello pré-populadas da etapa Olá onde criamos Olá filas do barramento de serviço. Clique em **Avançar**.
3. Na próxima janela de hello, forneça as credenciais do ACS para assinatura de Serviços BizTalk e Olá pontos de extremidade onde EAI e EDI (recebimento) pontes implantadas.
   
   Ponto de extremidade de ponte EAI Olá foi copiado na etapa anterior hello. Para o ponto de extremidade de ponte, de recebimento de EDI em Olá Portal de Serviços BizTalk, vá toohello contrato > configurações de recebimento > transporte > ponto de extremidade.
   
   ![][12]  
4. Na próxima janela de hello, em Contoso, clique em Olá **enviar a fatura In-house** botão. No arquivo de saudação abrir a caixa de diálogo, abra o arquivo INHOUSEINVOICE.txt de saudação. Examine o conteúdo de saudação do arquivo hello e, em seguida, clique em **Okey** toosend fatura de saudação.
   
   ![][13]  
5. Em alguns Olá de segundos a fatura será recebida na Northwind. Clique em Olá **Exibir mensagem** fatura de saudação do link toosee recebida pela Northwind. Observe como a fatura Olá recebida pela Northwind está no esquema padrão EDIFACT durante a saudação aquela enviada por Contoso estava no esquema in-house.
   
   ![][14]  
6. Selecione a fatura hello e, em seguida, clique em **enviar confirmação**. Na caixa de diálogo Olá pop-up, observe que intercâmbio Olá que ID é a mesma Olá recebida da fatura e hello confirmação enviada. Clique em Okey em Olá **enviar confirmação** caixa de diálogo.
   
   ![][15]  
7. Em alguns segundos, Olá fatura será recebida na Contoso.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Etapa 5 (opcional): Enviar fatura EDIFACT em lotes
As pontes EDI dos Serviços BizTalk também dão suporte ao processamento em lotes de mensagens de saída. Esse recurso é útil para parceiros receptores que preferem tooreceive um lote de mensagens (atendendo a um determinado critério) em vez de mensagens individuais.

aspecto mais importante de saudação ao trabalhar com lotes é real de lançamento de lote hello, também chamado de critérios de liberação Olá Olá. critérios de liberação de saudação podem ser baseados em como o parceiro receptor Olá quer tooreceive mensagens. Se o lote estiver ativado, Olá ponte EDI não enviará Olá saída mensagem toohello recebendo parceiro até hello critérios de liberação é atendido. Por exemplo, um critério de lote baseado no tamanho da mensagem liberará um lote somente quando ' n' mensagens estiverem agrupadas. Um critério de lote também pode ser um baseado em tempo, para que um lote seja enviado em uma hora fixa todo dia. Nesta solução, tentamos Olá critérios de acordo com tamanho de mensagem.

1. No Portal de Serviços BizTalk do hello, clique em contrato Olá criado anteriormente. Clique em Configurações de Envio > Em lote > Adicionar Lotes.
2. Para o nome do lote, digite **InvoiceBatch**, forneça uma descrição e clique em **Avançar**.
3. Especifique os critérios de lote, que definem quais mensagens devem ser agrupadas. Nesta solução, agrupamos todas as mensagens. Portanto, selecione a opção usar definições avançadas de saudação e digite **1 = 1**. Essa é uma condição que será sempre verdadeira e, portanto, todas as mensagens serão agrupadas. Clique em **Avançar**.
   
   ![][17]  
4. Especifique um critério de liberação de lote. Na caixa suspensa do hello, selecione **MessageCountBased**e para **contagem**, especifique **3**. Isso significa que um lote de três mensagens será enviado tooNorthwind. Clique em **Avançar**.
   
   ![][18]  
5. Revise o resumo de saudação e, em seguida, clique em **salvar**. Clique em **implantar** tooredeploy contrato de saudação.
6. Voltar toohello **Tutorial do cliente**, clique em **enviar a fatura In-house**e siga Olá prompts toosend Olá fatura. Você observará que nenhuma fatura foi recebida na Northwind, porque o tamanho de lote de saudação não for atendido. Repita essa etapa mais duas vezes, para que você tenha três mensagens de faturas enviadas tooNorthwind. Isso atende Olá critérios de liberação de lote de 3 mensagens e agora você verá uma fatura na Northwind.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

