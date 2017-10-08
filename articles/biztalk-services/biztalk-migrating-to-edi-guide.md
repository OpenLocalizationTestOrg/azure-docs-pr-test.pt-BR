---
title: "aaaMigrating soluções de EDI do BizTalk Server tooBizTalk guia técnico de serviços | Microsoft Docs"
description: "Migrar EDI tooMABS; Serviços BizTalk do Microsoft Azure"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>Migrar Serviços de tooBizTalk soluções de EDI do BizTalk Server: guia técnico

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Autor: Tim Wieman e Nitin Mehrotra

Revisores: Karthik Bharthy

Escrito usando: Serviços BizTalk do Microsoft Azure – versão de fevereiro de 2014.

## <a name="introduction"></a>Introdução
Intercâmbio de dados eletrônico (EDI) é um dos meios mais utilizados hello, por que as empresas para trocar dados eletronicamente, também conhecido como transações Business-to-Business ou B2B. BizTalk Server teve suporte de EDI por mais de uma década, desde a versão saudação inicial BizTalk Server. Com os serviços do BizTalk, Microsoft continua oferecendo suporte Olá soluções EDI na plataforma do Microsoft Azure hello. Transações B2B são principalmente tooan externo organização e, portanto, é mais fácil tooimplement se ele foi implementado em uma plataforma de nuvem. O Microsoft Azure fornece essa funcionalidade por meio de Serviços BizTalk.

Embora alguns clientes considerem no BizTalk Services como uma plataforma de "intacto" para novas soluções EDI, vários clientes têm as soluções EDI do BizTalk Server atuais que pode ser toomigrate tooAzure. Como EDI do BizTalk Services é projetado Olá com base na mesma chave entidades como serviços de arquitetura de EDI do BizTalk Server (parceiros comerciais, entidades, acordos), é possível toomigrate tooBizTalk de artefatos de EDI do BizTalk Server.

Este documento aborda algumas das diferenças de saudação envolvidas na migração tooBizTalk de artefatos EDI do BizTalk Server Services. Este documento presume um conhecimento prático do processamento de EDI do BizTalk Server e dos acordos entre parceiros comerciais. Para obter mais informações sobre o EDI do BizTalk Server, consulte [Gerenciamento de parceiros comerciais usando o BizTalk Server](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>Qual versão dos artefatos EDI do BizTalk Server pode ser migrados tooBizTalk serviços?
módulo de EDI do BizTalk Server Olá foi significativamente aprimorado para o BizTalk Server 2010, quando foi remodelado tooinclude parceiros, perfis e contratos. Os usos de Serviços BizTalk Olá Olá de tooorganize mesmo modelo parceiros comerciais e Olá divisões de negócios em esses parceiros comerciais. Como resultado, migrar EDI serviços de artefatos do BizTalk Server 2010 e tooBizTalk de versões posterior, é um processo muito mais simples. artefatos EDI toomigrate associados com versões anteriores tooBizTalk Server 2010, você deve primeiro atualizar tooBizTalk Server 2010 e, em seguida, migre os artefatos EDI tooBizTalk serviços.

## <a name="scenariosmessage-flow"></a>Cenários/fluxo de mensagens
Assim como com o BizTalk Server, o processamento de EDI nos Serviços BizTalk é criado com base em uma solução de gerenciamento de parceiros comerciais (TPM). Olá solução TPM tem Olá componentes-chave a seguir:

* Parceiros comerciais, que representam a organização em uma transação B2B.
* Perfis, que representam divisões em um parceiro comercial.
* Comerciais acordos de parceiro (ou acordos), que representa o contrato de negócios de saudação entre os dois parceiros/perfis.

Olá ilustração a seguir descreve as semelhanças Olá, e as diferenças entre uma solução EDI do BizTalk Server e a solução EDI do BizTalk Services:

![][EDImessageflow]

Olá principais diferenças e semelhanças entre um fluxo de solução EDI no BizTalk Server e os serviços do BizTalk são:

* Assim como o BizTalk Server usa um tooreceive de pipeline EDIReceive uma mensagem EDI e um toosend de pipeline EDISend uma mensagem EDI, os serviços do BizTalk usa um tooreceive de ponte de recebimento de EDI e toosend de ponte EDI enviar mensagens EDI. No BizTalk Server, Olá pipelines estão associados com um contrato usando enviar ou recebem portas. Nos serviços do BizTalk, o contrato de saudação próprio denota Olá envio ou ponte de recebimento.
* No BizTalk Server, depois de processos de pipeline EDIReceive Olá Olá mensagem EDI, mensagem de saudação é despejada tooa banco de dados do SQL Server. Olá EdiSend pipeline, em seguida, seleciona a mensagem de saudação do banco de dados do SQL Server hello, processa e envia toohello parceiro comercial.
  
    Nos serviços do BizTalk, depois Olá EDI mensagem ponte processos Olá EDI, ele encaminha o processo externo de tooan de mensagem de saudação. processo externo Olá pode ser executado no Microsoft Azure ou no local. processo externo Olá deve encaminhar toohello de mensagem de saudação EDI enviar ponte; ponte de envio de saudação não efetua pull inerentemente a mensagem de saudação. Depois de processar a mensagem de saudação, Olá ponte de envio EDI encaminha parceiro comercial de toohello de mensagem de saudação.

Os serviços do BizTalk fornece um tooquickly de experiência de configuração fácil de usar criar e implantar um acordo de B2B entre parceiros comerciais sem configurar qualquer computação do Microsoft Azure instâncias (funções Web ou de trabalho), qualquer banco de dados de SQL do Microsoft Azure ou qualquer Contas de armazenamento do Microsoft Azure. Cenários mais complexos exigirão a associação em fluxos de trabalho ou outro processamento de serviço "em torno da saudação bordas" de um acordo entre parceiros comerciais, ou seja, antes ou após o processamento de ponte EDI do acordo. Em detalhes, hello sequências de eventos a seguir ocorrem durante uma mensagem EDI processamento nos Serviços BizTalk.

1. Uma mensagem EDI é recebida do parceiro comercial Fabrikam.  Para receber mensagens EDI de parceiros comerciais, os Serviços BizTalk dão suporte a protocolos de transporte como FTP, SFTP, AS2 e HTTP/S.
2. Olá comerciais de processamento do lado do recebimento de contrato de parceiro desmonta tooXML formato da mensagem EDI hello.  Você pode rotear os pontos de extremidade do hello desmontada EDI mensagem (no formato XML) tooService barramento como um ponto de extremidade de retransmissão de barramento de serviço, o tópico de barramento de serviço, fila do barramento de serviço ou uma ponte de Serviços BizTalk.
3. Olá mensagens XML desmontadas poderiam ser recebidas do ponto de extremidade Olá para processamento personalizado posterior.  Esses pontos de extremidade podem ser processados por um componente no local ou uma computação do Microsoft Azure instância toofurther processo mensagem de saudação em um serviço Windows Workflow (WF) ou o Windows Communication Foundation (WCF), por exemplo.
4. Hello "processamento no lado de envio" do acordo entre parceiros comerciais hello, em seguida, monta a mensagem de saudação do XML no formato EDI e o envia tootrading parceiro, Contoso.  Para enviar mensagens EDI de parceiros tootrading, os serviços do BizTalk dá suporte a saudação mesmos protocolos usados para receber mensagens EDI.

Este documento fornece mais orientações conceituais sobre migração de alguns dos diferente tooBizTalk de artefatos EDI do BizTalk Server Olá serviços.

## <a name="sendreceive-ports-tootrading-partners"></a>Portas de envio/recebimento tooTrading parceiros
No BizTalk Server configurar locais de recebimento e mensagens EDI/XML tooreceive portas de recebimento de parceiros comerciais e configurar o parceiro de tootrading portas de envio toosend EDI/XML mensagens. Em seguida, você associa essas tooa portas usando o console de administração do BizTalk Server saudação do acordo de parceiro comercial. Nos serviços do BizTalk, Olá locais onde você recebe as mensagens de parceiros comerciais e para onde enviar a parceiros de tootrading de mensagens são configurados como parte da saudação em si (como parte das configurações de transporte) acordo de parceiro comercial em Olá Portal de Serviços BizTalk .  Portanto você não realmente têm Olá conceito de "portas de envio" e "locais de recebimento", propriamente dita, nos Serviços BizTalk. Para obter mais informações, consulte [Criando contratos](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Pipelines (pontes)
No EDI do BizTalk Server, os pipelines são entidades de processamento de mensagem que também podem incluir lógica personalizada para recursos específicos de processamento, conforme exigido pelo aplicativo hello. Para os serviços do BizTalk, Olá equivalente seria uma ponte EDI. No entanto nos serviços do BizTalk, por enquanto, Olá pontes EDI estão "fechadas".  Ou seja, você não pode adicionar sua própria ponte EDI tooan atividades personalizadas. Qualquer processamento personalizado deve ser feito fora Olá ponte EDI em seu aplicativo, antes ou depois da mensagem de saudação insere ponte Olá configurado como parte da saudação acordo entre parceiros comerciais. Pontes EAI tem processamento personalizado do hello opção toodo. Se você quiser um processamento personalizado, você pode usar pontes EAI antes ou depois da mensagem de saudação é processada pela ponte EDI de saudação. Para obter mais informações, consulte [como tooInclude de código personalizado em pontes](https://msdn.microsoft.com/library/azure/dn232389.aspx).

Você pode inserir um fluxo de publicação/assinatura com código personalizado e/ou usando mensagens de filas e tópicos antes de saudação acordo de parceiro comercial recebe a mensagem de saudação ou após contrato Olá processa a mensagem de saudação e encaminha o ponto de extremidade do tooa barramento de serviço do Service Bus.

Consulte **cenários/fluxo de mensagens** neste tópico para o padrão de fluxo de mensagens de saudação.

## <a name="agreements"></a>Contratos
Se você estiver familiarizado com hello que acordos de parceiros comerciais do BizTalk Server 2010 usados para processamento do EDI, os serviços do BizTalk acordos entre parceiros comerciais ser bastante familiares. A maioria do contrato Olá configurações são Olá mesmo e use Olá mesma terminologia. Em alguns casos, Olá configurações de acordo é muito mais simples toohello comparado mesmas configurações no BizTalk Server. Os Serviços BizTalk do Microsoft Azure dão suporte ao transporte X12, EDIFACT e AS2.

Serviços BizTalk do Microsoft Azure também fornece um **TPM Data Migration** ferramenta toomigrate os parceiros comerciais e acordos de parceiros comerciais do BizTalk Server módulo tooBizTalk Portal de serviços. Olá a ferramenta TPM Data Migration está disponível como parte de um pacote de ferramentas, que pode ser baixado da saudação [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). pacote de saudação também inclui um arquivo Leiame que fornece instruções sobre como toouse Olá ferramenta e informações básicas de solução de problemas para Olá ferramenta.

## <a name="schemas"></a>Esquemas
Os Serviços BizTalk oferecem esquemas EDI que podem ser usados em soluções de Serviços BizTalk.  Além disso, esquemas EDI do BizTalk Server também podem ser usados com Serviços BizTalk porque o nó raiz de saudação do esquema EDI Olá é o mesmo através do BizTalk Server, bem como os serviços do BizTalk. Assim, você será toodirectly capaz de realizar os esquemas EDI do BizTalk Server e usá-los em soluções EDI Olá que você desenvolver usando os serviços do BizTalk. Você também pode baixar esquemas de saudação do hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Mapas (transformações)
Mapas no BizTalk Server são chamados de transformações nos Serviços BizTalk. Migrar mapas do BizTalk Server tooBizTalk que Services pode ser um dos Olá tooachieve de tarefas mais complexa (dependendo da complexidade do mapa). ferramenta de mapeamento de saudação usada para os Serviços BizTalk é diferente do Mapeador do BizTalk hello. Mesmo que o mapeador de saudação parece principalmente Olá mesmo, formato subjacente do mapa Olá é diferente. Olá functoids (chamado **operações de mapa** nos Serviços BizTalk) disponível toohello usuários também são diferentes.  Na prática, você não pode usar diretamente um mapa do BizTalk nos Serviços BizTalk. Além disso, nem todas as functoids de saudação disponíveis no BizTalk Server estão disponíveis como operações de mapa nos Serviços BizTalk.

### <a name="new-transform-operations"></a>Novas operações de transformação
Enquanto a lista de saudação de operações de mapa transformação disponíveis possa ser bastante diferente do hello Mapeador do BizTalk Server, BizTalk Services transforma têm novas maneiras de realizar a Olá mesmas tarefas. Por exemplo, as transformações dos Serviços BizTalk têm **operações de lista** disponíveis. Isso não estava disponível no mapeador do BizTalk hello.  Olá **liste as operações** permitem que você toocreate e operar uma "lista", onde uma lista é um conjunto de itens (também conhecido como "linhas") e cada item pode ter vários membros (também conhecido como "colunas").  Você pode classificar a lista de saudação, selecione os itens com base em uma condição, etc.

Outro exemplo da nova funcionalidade do BizTalk Services transforma são Olá **operações Loop**.  É difícil toocreate aninhado loops em Olá Mapeador do BizTalk Server.  Portanto, operações Loop do mapa Olá são adicionadas para Olá BizTalk Services transforma.

Outro exemplo é Olá **If-Then-Else** a operação de expressão.  Realizando uma operação de if-then-else era possível no mapeador do BizTalk hello, mas exigia várias functoids tooaccomplish uma tarefa aparentemente simples.

### <a name="migrating-biztalk-server-maps"></a>Migrar mapas do BizTalk Server
Serviços BizTalk do Microsoft Azure fornece que uma ferramenta toomigrate do BizTalk Server mapeia tooBizTalk transformações de serviços. Olá **BTMMigrationTool** está disponível como parte da saudação **ferramentas** pacote fornecido com hello [download do SDK dos Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkId=235057). Para obter mais informações sobre a ferramenta hello, consulte [converter um tooa de mapa do BizTalk transformador de Serviços BizTalk](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

Você também pode examinar uma amostra por Sandro Pereira, MVP da BizTalk, em como muito[migrar transformações de serviços do BizTalk Server mapas tooBizTalk](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Orquestrações
Se você precisar toomigrate tooMicrosoft de processamento de orquestração do BizTalk Server do Azure, orquestrações Olá precisaria toobe regravada porque o Microsoft Azure não oferece suporte a orquestrações do BizTalk Server em execução.  Você poderia reescrever a funcionalidade de orquestração de saudação em um serviço do Windows Workflow Foundation 4.0 (WF4).  Essa seria uma regravação completa, pois não há nenhuma migração de tooWF4 de orquestrações do BizTalk Server. Aqui estão alguns recursos do Windows Workflow:

* [*Como toointegrate um fluxo de trabalho WCF serviço com tópicos e filas do barramento de serviço* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) por Paolo Salvatori. 
* [*Criando aplicativos com o Windows Workflow Foundation e o Azure* sessão](http://go.microsoft.com/fwlink/p/?LinkId=237314) da conferência Olá Build 2011.
* [*Centro de Desenvolvedores do Windows Workflow Foundation*](http://go.microsoft.com/fwlink/p/?LinkId=237315) no MSDN.
* [*Documentação do Windows Workflow Foundation 4 (WF4)*](https://msdn.microsoft.com/library/dd489441.aspx) no MSDN.

## <a name="other-considerations"></a>Outras considerações
A seguir estão algumas considerações que você deve fazer ao usar os Serviços BizTalk.

### <a name="fallback-agreements"></a>Acordos de fallback
Processamento de EDI do BizTalk Server tem o conceito de saudação de "Acordos Fallback".  Os Serviços BizTalk ainda **não** têm um conceito de acordo de fallback.  Consulte os tópicos da documentação BizTalk [Olá função dos acordos no processamento de EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) e [configuração Global ou Fallback contrato propriedades](https://msdn.microsoft.com/library/bb245981.aspx) para obter informações sobre como os acordos de Fallback são usados no BizTalk Servidor.

### <a name="routing-toomultiple-destinations"></a>Destinos de roteamento toomultiple
Pontes de serviços do BizTalk, em seu estado atual não suporta roteamento destinos de toomultiple mensagens usando uma publicação-inscrever-se o modelo. Em vez disso, você pode encaminhar mensagens do tópico de barramento de serviço BizTalk Services bridge tooa, que, em seguida, pode ter vários mensagem de saudação tooreceive assinaturas em mais de um ponto de extremidade.

## <a name="conclusion"></a>Conclusão
Serviços BizTalk do Microsoft Azure é atualizado em etapas regulares tooadd mais recursos e funcionalidades. Com cada atualização, esperamos toosupporting maior funcionalidade toofacilitate criar soluções de ponta a ponta usando os serviços do BizTalk e outras tecnologias do Azure.

## <a name="see-also"></a>Consulte também
[Desenvolvimento de aplicativos empresariais com o Azure](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
