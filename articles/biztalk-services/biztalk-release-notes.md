---
title: "aaaRelease observações para os Serviços BizTalk | Microsoft Docs"
description: "Saudação de listas de problemas conhecidos para Serviços BizTalk do Azure"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Notas de versão dos Serviços BizTalk do Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Notas de versão de saudação para os Microsoft hello Serviços BizTalk contêm Olá problemas nesta versão.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Novidades na atualização de novembro de saudação dos serviços do BizTalk
* Criptografia em repouso pode ser habilitada em Olá Portal de Serviços BizTalk. Confira [Habilitar a Criptografia em Repouso no Portal dos Serviços BizTalk](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Histórico de atualizações
### <a name="october-update"></a>Atualização de outubro
* Suporte para contas organizacionais:  
  * **Cenário**: você registrou uma implantação do Serviço BizTalk usando uma conta da Microsoft (como user@live.com). Nesse cenário, somente Account Microsoft os usuários podem gerenciar Olá BizTalk Service usando o portal de Serviços BizTalk hello. Não é possível usar uma conta organizacional.  
  * **Cenário**: você registrou uma implantação do Serviço BizTalk usando uma conta organizacional no Azure Active Directory (como user@fabrikam.com ou user@contoso.com). Nesse cenário, somente os usuários do Active Directory do Azure em Olá mesma organização pode gerenciar Olá BizTalk Service usando o portal de Serviços BizTalk hello. Não é possível usar uma conta da Microsoft.  
* Quando você cria um BizTalk Service no hello portal clássico do Azure, em Olá Portal de Serviços BizTalk é registrado automaticamente.
  * **Cenário**: você entrar no hello portal clássico do Azure, criar um BizTalk Service e, em seguida, selecione **gerenciar** para Olá pela primeira vez. Quando abre o portal de Serviços BizTalk hello, Olá BizTalk Service registra automaticamente e está pronto para suas implantações.  
    Consulte [Registrando e atualizando uma implantação do serviço BizTalk no Portal de Serviços BizTalk de Olá](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>Atualização de 14 de agosto
* De acordo e ponte desacoplamento – comerciais acordos entre parceiros e pontes agora estão dissociados Olá Portal de Serviços BizTalk. Agora você cria acordos e pontes separadamente e em tempo de execução pontes resolver tooan contrato com base nos valores de saudação na mensagem de saudação do EDI. Confira [Criar contratos nos Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/hh689908.aspx), [Criar uma ponte EDI usando o Portal dos Serviços BizTalk](https://msdn.microsoft.com/library/azure/dn793986.aspx), [Criar uma ponte AS2 usando o Portal dos Serviços BizTalk](https://msdn.microsoft.com/library/azure/dn793993.aspx) e [Como as pontes resolvem contratos em tempo de execução?](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* modelos de toocreate opção Olá para acordos foi descontinuado.  
* Olá acordo de envio, agora você pode especificar diferentes conjuntos de delimitadores para cada esquema. Essa configuração é especificada nas configurações de protocolo do contrato do lado de envio. Para saber mais, confira [Criar um contrato X12 nos Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/hh689847.aspx) e [Criar um contrato EDIFACT nos Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/dn606267.aspx). Duas novas entidades também são adicionadas toohello API OM TPM para Olá mesmo propósito. Confira [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) e [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Agora há suporte para construtores XSD padrão, incluindo tipos derivados. Confira [Usar construtores XSD padrão em seus mapas](https://msdn.microsoft.com/library/azure/dn793987.aspx) e [Usar tipos derivados nos exemplos e cenários de mapeamento](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* O AS2 dá suporte a novos algoritmos MIC para assinatura de mensagens e a novos algoritmos de criptografia. Veja [Criar um contrato AS2 nos Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Problemas conhecidos

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Problemas de conectividade após a atualização do Portal dos Serviços BizTalk
  Se você tiver Olá abrir o Portal de Serviços BizTalk durante a atualização de Serviços BizTalk tooroll no serviço toohello é alterado, você poderá enfrentar problemas de conectividade com hello Portal de Serviços BizTalk.  
  Como alternativa, você pode reiniciar o navegador hello, excluir o cache do navegador hello ou iniciar o portal Olá em modo privado.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Visual Studio IDE não é possível localizar o artefato de saudação se você clicar em um erro ou aviso em um projeto de Serviços BizTalk
Instale o problema de saudação toofix Olá Visual Studio 2012 Update 3 RC 1.  

### <a name="custom-binding-project-reference"></a>Referência de projeto de associação personalizada
Considere Olá seguintes situações com um projeto de serviços do BizTalk em uma solução do Visual Studio:  

* Em Olá mesma solução do Visual Studio, há um projeto de Serviços BizTalk e um projeto de associação personalizada. Olá projeto BizTalk Service tem um arquivo de projeto referência toothis associação personalizada.
* Olá projeto BizTalk Service tem um referência tooa vinculação/comportamento personalizado DLL.

Você 'Compilar' hello solução no Visual Studio com êxito. Em seguida, você 'Rebuild' ou 'Limpa' solução hello. Depois disso, quando você recompila ou Olá limpeza novamente, após o erro ocorre:  
  Não é possível toocopy arquivo <Path tooDLL> too"bin\Debug\FileName.dll". processo de saudação não pode acessar o arquivo hello 'bin\Debug\FileName.dll' porque ele está sendo usado por outro processo.  

#### <a name="workaround"></a>Solução alternativa
* Se [atualização 3 do Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=39305) é instalado, você terá Olá duas opções a seguir:
  
  * Reiniciar o Visual Studio ou
  * Solução de saudação de reinicialização. Em seguida, execute somente uma compilação na solução de saudação.  
* Se [atualização 3 do Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=39305) não é estiver instalado, abra o Gerenciador de tarefas, clique guia processos de saudação, clique Olá MSBuild.exe processo e Olá Finalizar processo botão.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Roteamento de pontos de extremidade tooBasicHttpRelay não tem suporte de pontes e o Portal de Serviços BizTalk se os caracteres não imprimíveis forem promovidos como cabeçalhos HTTP
Se você usar caracteres não imprimíveis como parte das propriedades promovidas para mensagens, essas mensagens não podem ser roteado toorelay destinos que usam a vinculação BasicHttpRelay de saudação. Além disso, Olá promovido propriedades que estão disponíveis como parte do rastreamento serão codificadas de URL para blobs e decodificadas para destinos.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>MDN é enviada assincronamente, mesmo se Olá enviar opção MDN assíncrona está desmarcada
Considere este cenário – se você selecionar Olá **enviar MDN assíncrona** caixa de seleção e especifique um MDN do URL toosend Olá assíncrona e, em seguida, desmarque Olá **enviar MDN assíncrona** caixa de seleção novamente, Olá MDN ainda é toohello enviado especificou a URL, embora Olá opção toosend async MDNs não estiver selecionada.  
Como alternativa, você deve limpar Olá especificou a URL antes de desmarcar Olá **enviar MDN assíncrona** caixa de seleção e, em seguida, implantar contrato Olá AS2.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Caracteres de espaço em branco além de uma causa de intercâmbio válido toohello de toobe enviada uma mensagem vazia suspender o ponto de extremidade
Se houver espaços em branco depois de um segmento IEA, o desmontador Olá trata isso como fim do intercâmbio atual e examina o próximo conjunto de espaços em branco como uma próxima mensagem de saudação. Como este não é um intercâmbio válido, você pode observar que uma mensagem bem-sucedida é enviada toohello destino da rota e uma mensagem vazia é enviada Olá suspender o ponto de extremidade.  

### <a name="tracking-in-biztalk-services-portal"></a>Rastreamento no Portal dos Serviços BizTalk
Eventos de rastreamento são capturados toohello processamento de mensagem EDI e qualquer correlação. Se uma mensagem falhar fora Olá estágio protocolo, o rastreamento será mostrado como bem-sucedido. Nessa situação, consulte a seção LOG de toohello em Olá **detalhes** coluna **controle** para obter detalhes do erro.
Olá X12 configurações de envio e recebimento ([Create X12 contrato de Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/hh689847.aspx)) fornecem informações sobre Olá estágio de protocolo.  

### <a name="update-agreement"></a>Atualização do contrato
Olá Portal de Serviços BizTalk permite toomodify Olá qualificador de uma identidade quando um contrato é configurado. Isso pode resultar em propriedades inconsistentes. Por exemplo, há um acordo com zz: 1234567 e zz: 7654321 Olá qualificador. Configurações de perfil do Portal de Serviços BizTalk Olá, você altere zz: 1234567 toobe 01:ChangedValue. Abra o contrato de saudação e 01:ChangedValue é exibido em vez de zz: 1234567.
Olá toomodify qualificador de uma identidade, exclua Olá contrato, atualize **identidades** em Olá perfil do parceiro e, em seguida, recrie o contrato de saudação.  

> AZURE.WARNING Esse comportamento afeta o X12 e o AS2.  
> 
> 

### <a name="as2-attachments"></a>Anexos AS2
Não há suporte para anexos de mensagens AS2 nos envios ou recebimentos. Especificamente, os anexos são silenciosamente ignorados e corpo da mensagem de saudação é processado como uma mensagem regular AS2.  

### <a name="resources-remembering-path"></a>Recursos: lembrar o caminho
Ao adicionar **recursos**, janela de diálogo Olá pode não lembrar Olá tooadd de caminho utilizado anteriormente um recurso. caminho de usadas anteriormente do tooremember hello, tente adicionar o site de Portal de Serviços BizTalk-Olá muito**Sites confiáveis** no Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Se você renomear o nome da entidade de saudação de uma ponte e o projeto de saudação fechar sem salvar as alterações, abrir entidade Olá novamente resulta em erro
Considere um cenário em Olá ordem a seguir:  

* Adicionar um projeto BizTalk Service de tooa de ponte (por exemplo uma ponte unidirecional XML)  
* Renomear ponte hello, especificando um valor para Olá propriedade de nome de entidade. Isso renomeia o arquivo. bridgeconfig associado de saudação com nome hello especificado.  
* Feche o arquivo. BCS de saudação (fechando a guia Olá no Visual Studio) sem salvar as alterações de saudação.  
* Abra novamente o arquivo. BCS de saudação da saudação Gerenciador de soluções.  
  Você observará que enquanto o arquivo. bridgeconfig associado Olá tem nome de novo Olá especificado, nome da entidade Olá na superfície de design Olá ainda é nome antigo da saudação. Se você tentar tooopen Olá configuração da ponte, clicando duas vezes o componente de ponte hello, você obtém Olá erro a seguir:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid executando este cenário, certifique-se de salvar as alterações depois de renomear entidades Olá em um projeto do BizTalk Service.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>O projeto do Serviço BizTalk é compilado com êxito mesmo que um artefato tenha sido excluído de um projeto do Visual Studio
Considere um cenário onde você adicionar um projeto do BizTalk Service de tooa de artefato (por exemplo, um arquivo XSD), inclua esse artefato na Olá configuração da ponte (por exemplo, especificando-o como um tipo de mensagem de solicitação) e, em seguida, excluí-la do projeto do Visual Studio hello. Nesse caso, compilar o projeto de saudação não fornecerá qualquer erro enquanto o artefato Olá excluído está disponível no disco Olá Olá mesmo local de onde foi incluído no projeto do Visual Studio hello.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Olá projeto BizTalk Service não verificar disponibilidade do esquema ao configurar pontes Olá
Em um projeto do BizTalk Service, se um esquema que é adicionado toohello projeto importar outro esquema, Olá projeto BizTalk Service não verifica se o esquema importado Olá é adicionada toohello projeto. Se você tentar toobuild esse projeto, você não obtiver os erros de compilação.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>mensagem de resposta de saudação de uma ponte de solicitação-resposta XML é sempre do conjunto de caracteres UTF-8
Para esta versão, Olá charset de mensagem de resposta de saudação de uma ponte de solicitação-resposta XML é sempre definido tooUTF-8.
  
### <a name="user-defined-datatypes"></a>Tipos de dados definidos pelo usuário
adaptadores do BizTalk Adapter Pack Olá no recurso de serviço de adaptador BizTalk Olá podem utilizar tipos de dados definidos pelo usuário para operações do adaptador.
Ao usar tipos de dados definidos pelo usuário, copie arquivos (. dll) de saudação toodrive:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ ou toohello Cache de Assembly Global (GAC) no servidor de saudação Olá serviço de adaptador BizTalk serviço de hospedagem. Caso contrário, Olá seguinte erro pode ocorrer no cliente hello:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> É recomendado toouse GACUtil.exe tooinstall um arquivo em Olá Cache de Assembly Global. Documentos GACUtil.exe como toouse essa opções de linha de comando do Visual Studio ferramenta e hello.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Reiniciar Olá Site do serviço de adaptador do BizTalk
Olá instalar **o tempo de execução de serviço de adaptador BizTalk*** cria Olá **serviço de adaptador BizTalk** site no IIS que contém Olá **BAService** aplicativo. **BAService** aplicativo usa internamente o alcance de saudação do retransmissão associação tooextend da nuvem de toohello de ponto de extremidade de serviço local. Para um serviço hospedado no local, ponto de extremidade de retransmissão correspondente Olá estará registrado no hello barramento de serviço somente durante a saudação início do serviço local.  

Se você parar e iniciar um aplicativo, a configuração de saudação para iniciar automaticamente um aplicativo não é cumprida. Portanto, quando **BAService** é interrompido, você sempre deve reiniciar Olá **serviço de adaptador BizTalk** web site em vez disso. Não iniciar ou parar Olá **BAService** aplicativo.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>Caracteres especiais não devem ser usados para nomes de endereços e entidades de componentes LOB
Você não deve usar caracteres especiais para nomes de endereços e entidades de componentes LOB. Se você fizer isso, você obterá um erro durante a implantação Olá projeto BizTalk Service. Para certos caracteres como '% s', site do serviço de adaptador BizTalk Olá pode entram em um estado parado e toomanually será necessário iniciá-lo.

### <a name="test-map-with-get-context-property"></a>Mapa de teste com a propriedade Get Context
Se uma Transformação contiver uma **Operação de Mapeamento da Propriedade Get Context**, o **Mapa de Teste** falhará. Como solução temporária, substitua Olá **propriedade obter contexto** a operação com uma cadeia de caracteres de concatenação de operação de mapeamento contendo dados fictícios. Isso popular o esquema de destino hello e permitirá que testar outras funcionalidades de transformação.

### <a name="test-map-property-does-not-display"></a>A propriedade do mapa de teste não é exibida
Olá **mapa de teste** propriedades não são exibidos no Visual Studio. Isso pode ocorrer se hello **propriedades** janela e hello **Solution Explorer** janela não forem encaixadas simultaneamente. tooresolve hello, encaixe **propriedades** e hello **Solution Explorer** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>O menu suspenso de Reformatação de Data/Hora está esmaecido
Quando uma operação de mapeamento de reformatação DateTime é adicionada toohello design Olá superfície e configurado, formato de lista suspensa pode ser esmaecida. Isso pode acontecer se o computador de saudação exibição estiver definido **médio – 125%** ou **maior – 150%**. tooresolve, defina a exibição de saudação muito**pequeno – 100% (padrão)** usando Olá etapas abaixo:  

1. Olá abrir **painel de controle** e clique em **aparência e personalização**.
2. Clique em **Tela**.
3. Clique em **Menor – 100% (padrão**) e clique em **Aplicar**.

Olá **formato** lista suspensa deveria agora funcionar como esperado.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Contratos duplicados no hello Portal de Serviços BizTalk
Considere Olá cenário a seguir:

1. Crie um contrato usando a API de OM de gerenciamento de parceiros Olá comerciais.
2. Abra o contrato Olá no Portal de Serviços BizTalk de saudação em duas guias diferentes.
3. Implante o contrato de saudação de ambas as guias hello.
4. Como resultado, ambos os contratos Olá obtêm resultados implantados em entradas duplicadas no hello Portal de Serviços BizTalk

**Solução alternativa**. Abra qualquer um dos contratos duplicados Olá no hello Portal de Serviços BizTalk e desfaça a implantação.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>As pontes não usam certificados atualizados mesmo depois que um certificado foi atualizado no repositório de artefato Olá
Considere Olá os seguintes cenários:  

**Cenário 1: Usar certificados com base em impressão digital para transferência segura de mensagem de um ponto de extremidade do serviço de tooa ponte**  
Considere um cenário em que você usa certificados baseados em impressão digital no seu projeto do Serviço BizTalk. Você atualiza o certificado Olá Olá Portal de Serviços BizTalk com hello o mesmo nome mas uma impressão digital diferente, mas não atualizar Olá projeto BizTalk Service adequadamente. Nesse cenário, a ponte Olá pode continuar tooprocess mensagens de saudação porque os dados antigos de certificado Olá ainda podem estar em cache do canal de saudação. Após isso, o processamento de mensagens falha.  

**Solução alternativa**: atualizar o certificado Olá Olá projeto BizTalk Service e reimplantar o projeto de saudação.  

**Cenário 2: Uso de certificados de tooidentify de comportamentos baseados em nome para transferência segura de mensagem de um ponto de extremidade do serviço de tooa ponte**

Considere um cenário onde você usa certificados de tooidentify comportamentos baseados em nome em seu projeto do BizTalk Service. Atualizar o certificado Olá Olá Portal de Serviços BizTalk mas não atualizar Olá projeto BizTalk Service adequadamente. Nesse cenário, a ponte Olá pode continuar tooprocess mensagens de saudação porque os dados antigos de certificado Olá ainda podem estar em cache do canal de saudação. Após isso, o processamento de mensagens falha.  

**Solução alternativa**: atualizar o certificado Olá Olá projeto BizTalk Service e reimplantar o projeto de saudação.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>As pontes continuam tooprocess mensagens mesmo quando o banco de dados SQL hello está offline
pontes de Serviços BizTalk Olá continuam tooprocess mensagens por um tempo, mesmo se Olá Microsoft Azure SQL Database (que armazena Olá executando informações como artefatos implantados e pipelines), está offline. Isso ocorre porque os serviços do BizTalk usa artefatos Olá armazenado em cache e a configuração de ponte.
Se não desejar Olá pontes tooprocess todas as mensagens quando Olá banco de dados SQL está offline, você pode usar toostop de cmdlets do PowerShell de serviços do BizTalk hello ou suspender Olá BizTalk Service. Consulte [exemplo de gerenciamento de serviço do Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=329019) para operações de toomanage saudação do Windows PowerShell cmdlets.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Mensagem de XML de saudação de leitura no componente de código personalizado da ponte inclui um caractere extra BOM
Considere um cenário onde você deseja tooread uma mensagem XML em código personalizado da ponte. Se você usar o hello .NET API System.Text.Encoding.UTF8.GetString(bytes) um caractere extra BOM é incluído na saída de hello no início de saudação da mensagem de saudação. Portanto, se você não quiser Olá Olá de tooinclude saída caractere extra BOM, você deve usar ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>Enviar mensagens tooa ponte usando o WCF não dimensiona
As mensagens enviadas a ponte tooa usando o WCF não dimensiona. Em vez disso, você deve usar HttpWebRequest se desejar ter um cliente escalonável.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>ATUALIZAÇÃO: Erro do provedor de Token após a atualização do BizTalk Services visualização tooGeneral GA (disponibilidade)
Há um Contrato AS2 ou EDI com lotes ativos. Quando Olá BizTalk Service é atualizado de visualização tooGA, seguinte Olá pode ocorrer:

* Erro: o provedor de token Olá foi tooprovide não é possível um token de segurança. O provedor de token retornado a mensagem: não foi possível resolver o nome do remoto hello.
* As tarefas em lote são canceladas.

**Solução alternativa**: após Olá BizTalk Service é atualizada tooGeneral GA (disponibilidade), reimplante o contrato de saudação.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>ATUALIZAÇÃO: Caixa de ferramentas mostra Olá ícones da ponte antigos depois de atualizar Olá SDK dos Serviços BizTalk
Depois de atualizar uma versão anterior do hello SDK dos Serviços BizTalk, que tinha ícones antigos representando as pontes hello, caixa de ferramentas de saudação continua ícones antigos do tooshow Olá para pontes hello. No entanto, se você adicionar uma ponte tooBizTalk serviço projeto superfície do designer, superfície Olá mostra o ícone novo hello.  

**Solução alternativa**. Você pode contornar esse problema excluindo arquivos. TBD Olá <system drive>: \Users\<usuário > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>ATUALIZAÇÃO: Atualização do Portal do BizTalk de visualização tooGA pode mostrar um erro indicando que Olá capacidade do EDI não está disponível
Se você está conectado ao Olá Portal de Serviços BizTalk, enquanto os serviços do BizTalk Olá é atualizado de visualização tooGA, você pode obter Olá erro a seguir no portal de saudação:  

Este recurso não está disponível como parte desta edição dos Serviços BizTalk do Microsoft Azure. toouse esses recursos alternar a edição apropriada do tooan.  

**Resolução**: ao fazer logoff do portal hello, Olá fechar e abrir navegador e, em seguida, faça logon no portal de saudação.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>ATUALIZAÇÃO: Novos dados de rastreamento não aparecem depois que os serviços do BizTalk é atualizado tooGA
Imagine um cenário no qual você tem uma ponte XML implantada na assinatura de Visualização dos Serviços BizTalk. Enviar mensagens toohello ponte e os dados de rastreamento correspondentes hello estão disponíveis em Olá Portal de Serviços BizTalk. Agora, se os bits de tempo de execução de Portal de Serviços BizTalk e os serviços do BizTalk Olá são tooGA atualizado e enviar um toohello mensagem mesmo ponto de extremidade da ponte implantado anteriormente, Olá dados de rastreamento não mostra as mensagens enviadas depois da atualização.  

### <a name="pipelines-versus-bridges"></a>Pipelines versus pontes
Ao longo deste documento, o termo de saudação 'pipelines"' e 'pontes' são intercambiáveis. Ambos essencialmente significam Olá a mesma coisa, que é uma unidade de processamento de mensagem implantada nos serviços do BizTalk.  

### <a name="concepts"></a>Conceitos
[Serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

