---
title: "aaaLearn sobre os recursos em edições de Serviços BizTalk | Microsoft Docs"
description: "Comparar recursos Olá das edições de Serviços BizTalk Olá: gratuita, Developer, Basic, Standard e Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>Serviços BizTalk: gráfico de edições

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Os Serviços BizTalk do Azure oferecem várias edições. Use este toodetermine artigo qual edição é adequada para suas necessidades de negócios e cenário.

## <a name="compare-hello-editions"></a>Compare as edições do hello
**Free (Visualização)**

É possível criar e gerenciar Conexões Híbridas. Uma Conexão híbrida é uma maneira fácil de tooconnect tooan um site do Azure de sistema, como o SQL Server no local.

**Desenvolvedores**

Inclui Conexões Híbridas, processamento de mensagens EAI & EDI com um portal de gerenciamento de parceiro comercial fácil de usar e dá suporte a esquemas EDI comuns e a processamento sofisticado de EDI por x12 e AS2. Pode criar cenários comuns de EAI, conectando a serviços em nuvem Olá com qualquer tooread de protocolos HTTP/S, REST, FTP, SFTP e WCF e gravar mensagens.  Utilize sistemas LOB local tooon conectividade com os adaptadores SAP, Oracle eBusiness, banco de dados Oracle, Siebel e SQL Server prontos para uso. Use um ambiente centralizado no desenvolvedor com ferramentas do Visual Studio para permitir desenvolvimento e implantação fáceis. Limitado toodevelopment fins de teste e somente com nenhum serviço de nível de SLA (contrato).

**Básico**

Inclui a maioria dos recursos de desenvolvedor Olá com aumentos em conexões de conexões híbridas, pontes EAI, acordos EDI e BizTalk Adapter Pack. Também oferece alta disponibilidade e Olá opção tooscale com um contrato de nível de serviço (SLA).

**Standard**

Inclui todos os recursos básicos de saudação com aumentos em conexões de conexões híbridas, pontes EAI, acordos EDI e BizTalk Adapter Pack. Também oferece alta disponibilidade e Olá opção tooscale com um contrato de nível de serviço (SLA).

**Premium**

Inclui todos os recursos padrão do hello com aumentos em conexões de conexões híbridas, pontes EAI, acordos EDI e BizTalk Adapter Pack. Também inclui arquivamento, alta disponibilidade e Olá opção tooscale com um contrato de nível de serviço (SLA).

## <a name="editions-chart"></a>Tabela de edições
Olá tabela a seguir lista as diferenças de saudação.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Free (Visualização)</th>
        <th>Desenvolvedores</th>
        <th>Básico</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Preço inicial</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Preço dos Serviços BizTalk do Azure</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full"> Calculadora de preços do Azure</a></td>
</tr>
<tr>
<td><strong>Configuração mínima padrão</strong></td>
<td>1 Unidade Free</td>
<td>1 unidade Developer</td>
<td>1 unidade Basic</td>
<td>1 unidade Standard</td>
<td>1 unidade Premium</td>
</tr>
<tr>
<td><strong>Escala</strong></td>
<td>Sem escala</td>
<td>Sem escala</td>
<td>Sim, em incrementos de 1 unidade Basic</td>
<td>Sim, em incrementos de 1 unidade Standard</td>
<td>Sim, em incrementos de 1 unidade Premium</td>
</tr>
<tr>
<td><strong>Escala máxima permitida</strong></td>
<td>Sem escala</td>
<td>Sem escala</td>
<td>Unidades de too8</td>
<td>Unidades de too8</td>
<td>Unidades de too8</td>
</tr>
<tr>
<td><strong>Pontos EAI por unidade</strong></td>
<td>Não incluso</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Inclui Contratos TPM</td>
<td>Não incluso</td>
<td>Incluso. 10 contratos por unidade.</td>
<td>Incluso. 50 contratos por unidade.</td>
<td>Incluso. 250 contratos por unidade.</td>
<td>Incluso. 1000 contratos por unidade.</td>
</tr>
<tr>
<td><strong>Conexões híbridas por unidade</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Transferência de dados por conexões híbridas (GB) por unidade</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Sistemas LOB de tooon locais de conexões de serviço de adaptador do BizTalk</strong></td>
<td>Não incluso</td>
<td>1 conexão</td>
<td>2 conexões</td>
<td>5 conexões</td>
<td>25 conexões</td>
</tr>
<tr>
<td align="left"><strong>Protocolos/sistemas com suporte:</strong>
<ul>
<li>http</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Service Bus (SB)</li>
<li>Blob do Azure</li>
<li>APIs REST</li>
</ul>
</td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Alta disponibilidade</strong>
<br/><br/>
Para obter o Contrato de Nível de Serviço (SLA), consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Preços dos Serviços BizTalk do Azure</a>.
</td>
<td>Não incluso</td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Backup e restauração</strong></td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Acompanhamento</strong></td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Arquivamento</strong><br/><br/>
Inclui NRR (não repúdio de recebimento) e o download de mensagens rastreadas</td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Não incluso</td>
<td>Não incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Uso de código personalizado</strong></td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
<tr>
<td><strong>Uso de transformações, incluindo XSLT personalizado</strong></td>
<td>Não incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
<td>Incluso</td>
</tr>
</table>

> [!NOTE]
> Para resiliência contra falhas de hardware, a Alta Disponibilidade implica em ter várias VMs dentro de uma única Unidade do BizTalk.
> 
> 

## <a name="faqs"></a>Perguntas frequentes
#### <a name="what-is-a-biztalk-unit"></a>O que é uma Unidade do BizTalk?
Uma unidade de"" é o nível atômico de saudação de uma implantação de Serviços BizTalk do Azure. Cada edição é fornecida com uma unidade que tem capacidade e memória de computação diferentes. Por exemplo, uma Unidade Básica tem mais computação do que a Developer, a Standard tem mais computação do que a Basic e assim por diante. Quando você dimensiona um Serviço BizTalk, você o faz em termos de Unidades.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Qual é a diferença de saudação entre os serviços do BizTalk e a VM do Azure BizTalk?
Os serviços do BizTalk fornece uma arquitetura de plataforma-como-um-serviço (PaaS) verdadeira para criar soluções de integração na nuvem hello. Com o modelo de PaaS hello, você completamente concentrar na lógica do aplicativo hello e deixar todos Olá tooMicrosoft de gerenciamento de infraestrutura, incluindo:

* Não há necessidade toomanage ou patch máquinas virtuais.
* A Microsoft garante a disponibilidade
* Você controla a escala sob demanda simplesmente solicitando mais ou menos capacidade por meio de saudação portal do Azure.

O BizTalk Server em Máquinas Virtuais do Azure fornece uma arquitetura de IaaS (Infraestrutura como Serviço). Criar máquinas virtuais e configurá-los exatamente como seu ambiente local, tornando mais fácil toorun os aplicativos existentes na nuvem Olá sem alterações de código. Com o IaaS, você ainda é responsáveis por configuração de máquinas virtuais de hello, gerenciamento de máquinas virtuais de saudação (por exemplo, instalar software e patches do sistema operacional) e a arquitetura de aplicativo hello para alta disponibilidade.

Se você estiver planejando criar novas soluções de integração que minimizem seu esforço de gerenciamento da infraestrutura, use os Serviços BizTalk. Se você estiver procurando tooquickly migrar suas soluções existentes do BizTalk ou procurando um ambiente sob demanda toodevelop e teste do BizTalk Server aplicativos, usar o BizTalk Server em uma máquina Virtual do Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Qual é a diferença Olá entre o serviço de adaptador do BizTalk e conexões híbridas?
Olá serviço de adaptador BizTalk é usado por um serviço de BizTalk do Azure. Olá serviço de adaptador do BizTalk usa Olá BizTalk Adapter Pack tooconnect tooan no sistema local da linha de negócios (LOB). Uma Conexão híbrida fornece uma maneira fácil e conveniente tooconnect aplicativos do Azure, como recursos de aplicativos Web Olá no serviço de aplicativo do Azure e o Azure Mobile Services tooan recurso local.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>O que significa “Transferência de dados por conexões híbridas (GB) por unidade”? Isso é por minuto/hora/dia/semana/mês? O que acontece quando Olá limite é atingido?
Olá custo da Conexão híbrida por unidade depende da edição de Serviços BizTalk hello. Resumindo, o custo depende de quantos dados você transfere. Por exemplo, a transferência de 10 GB de dados diariamente custa menos do que a transferência de 100 GB diariamente. Saudação de uso [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/?scenario=full) de custos específicos de toodetermine de Serviços BizTalk. Normalmente, os limites de saudação são impostos diariamente. Se você exceder o limite de hello, qualquer excedente é cobrado na taxa de saudação de US $1 por GB.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Ao criar um contrato de serviços do BizTalk, por que número Olá de pontes subir por dois, em vez de apenas um?
Cada contrato é composto de duas pontes diferentes, uma ponte de comunicação do lado do envio e outra do lado do recebimento.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>O que acontece quando eu atinge o limite de cota de Olá no número de saudação de pontes ou contratos?
Você não é possível toodeploy qualquer nova pontes ou crie novos contratos. toodeploy mais, você precisa tooscale toomore unidades de serviço do BizTalk Olá ou edição superior tooa atualização.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Como migrar de uma camada de Serviços BizTalk tooanother?
edição gratuita Olá não pode ser migrado ou 'expandidos' tooanother camada e não pode ser feita e restaurado tooanother camada. Se você precisar de outra camada, crie um BizTalk Service novo usando a nova camada de saudação. Qualquer artefato criado usando a edição gratuita do hello, incluindo conexões híbridas, toobe necessidade recriada no hello novo BizTalk Service. 

Para edições restantes do hello, use Olá backup e restauração para migrar seus artefatos de tooanother de uma camada. Por exemplo, fazer backup de seus artefatos na camada padrão hello e, em seguida, restaurá-los a camada do toohello Premium. [Serviços BizTalk: Backup e restauração](biztalk-backup-restore.md) descreve Olá suporte para caminhos de migração e lista quais artefatos de backup. Observe que não é feito backup das Conexões Híbridas. Depois de fazer backup e restaurar tooa nova camada, em seguida, recriar as conexões híbridas hello.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Olá serviço de adaptador BizTalk está incluído no serviço Olá? Como receber o software Olá?
Sim, Olá serviço de adaptador BizTalk com hello BizTalk Adapter Pack são incluídos com hello SDK dos Serviços BizTalk do Azure [baixar](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Próximas etapas
Serviços de BizTalk do Azure toocreate em Olá do Azure, acesse muito[Serviços BizTalk: provisionamento usando o portal do Azure de Olá](biztalk-provision-services.md). toostart criação de aplicativos, vá muito[Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Recursos adicionais
* [Serviços BizTalk: Provisionamento usando Olá portal do Azure](biztalk-provision-services.md)<br/>
* [Serviços BizTalk: gráfico do status do provisionamento](biztalk-service-state-chart.md)<br/>
* [Serviços BizTalk: guias Painel, Monitor e Escala](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [Serviços BizTalk: limitação](biztalk-throttling-thresholds.md)<br/>
* [Serviços BizTalk: nome e chave do emissor](biztalk-issuer-name-issuer-key.md)<br/>
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

