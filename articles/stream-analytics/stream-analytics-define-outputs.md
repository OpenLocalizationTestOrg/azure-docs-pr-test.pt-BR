---
title: "Saídas do Stream Analytics: opções de armazenamento e análise | Microsoft Docs"
description: "Saiba mais sobre opções de saídas de dados do Stream Analytics, incluindo Power BI para resultados da análise."
keywords: "transformação de dados, resultados da análise, opções de armazenamento de dados"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Saídas do Stream Analytics: opções de armazenamento, análise
Ao criar um trabalho do Stream Analytics, considere como os dados resultantes hello serão consumidos. Como você exibir resultados de saudação do trabalho do Stream Analytics hello e onde você armazenará?

Em ordem tooenable uma variedade de padrões de aplicativo, Stream Analytics do Azure tem opções diferentes para armazenar a saída e exibir resultados da análise. Isso torna fácil tooview saída de trabalho e oferece flexibilidade no consumo de saudação e o armazenamento de saída do trabalho Olá para data warehouse e outros fins. Nenhuma saída configurada no trabalho Olá deve existir antes Olá trabalho é iniciado e eventos que fluem de início. Por exemplo, se você usar o armazenamento de Blob como uma saída, o trabalho de saudação não criará uma conta de armazenamento automaticamente. Ele precisa toobe criado pelo usuário Olá antes Olá ASA trabalho é iniciado.

## <a name="azure-data-lake-store"></a>Repositório Azure Data Lake
O Stream Analytics dá suporte ao [Repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/). Esse armazenamento permite que você toostore dados de qualquer velocidade de tamanho, tipo e inclusão para análise operacional e exploratória. Além disso, toobe de necessidades de análise de fluxo autorizado repositório Data Lake do tooaccess hello. Obter detalhes sobre como toosign para Olá repositório Data Lake (se necessário) são discutidos em hello e autorização [Data Lake saída artigo](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Autorizar um Azure Data Lake Store
Quando o armazenamento do Data Lake é selecionado como uma saída de hello portal do Azure, será solicitado tooauthorize um repositório conexão tooan existente Data Lake.  

![Autorizar o Repositório Data Lake](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

Em seguida, preencha as propriedades Olá Olá repositório Data Lake saída conforme mostrado abaixo:

![Autorizar o Repositório Data Lake](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

Olá tabela a seguir lista os nomes de propriedade hello e sua descrição necessário para criar uma saída de repositório Data Lake.

<table>
<tbody>
<tr>
<td><B>NOME DA PROPRIEDADE</B></td>
<td><B>DESCRIÇÃO</B></td>
</tr>
<tr>
<td>Alias de saída</td>
<td>Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis repositório Data Lake.</td>
</tr>
<tr>
<td>Nome da conta</td>
<td>nome de saudação do hello conta Data Lake armazenamento em que você está enviando a saída. Você verá uma lista suspensa de contas do repositório Data Lake toowhich Olá usuário conectado no portal de toohello tem acesso.</td>
</tr>
<tr>
<td>Padrão de prefixo do caminho [<I>opcional</I>]</td>
<td>Olá arquivo caminho usado toowrite seus arquivos no hello especificado conta do repositório Data Lake. <BR>{data}, {hora}<BR>Exemplo 1: pasta1/logs/{data}/{hora}<BR>Exemplo 2: pasta1/logs/{data}</td>
</tr>
<tr>
<td>Formato de data [<I>opcional</I>]</td>
<td>Se o token de data de saudação é usado no caminho de prefixo hello, você pode selecionar o formato de data de saudação na qual os arquivos são organizados. Exemplo: AAAA/MM/DD</td>
</tr>
<tr>
<td>Formato de hora [<I>opcional</I>]</td>
<td>Se o token de tempo de saudação é usado no caminho de prefixo Olá, especifique o formato de tempo de saudação na qual os arquivos são organizados. Atualmente, o valor de saudação só tem suportada é HH.</td>
</tr>
<tr>
<td>Formato de serialização do evento</td>
<td>Formato de serialização para dados de saída. Há suporte para JSON, CSV e Avro.</td>
</tr>
<tr>
<td>Codificação</td>
<td>Se o formato for CSV ou JSON, uma codificação deve ser especificada. UTF-8 é Olá somente suporte para formato de codificação no momento.</td>
</tr>
<tr>
<td>Delimitador</td>
<td>Aplicável somente à serialização de CSV. O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados CSV. Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical.</td>
</tr>
<tr>
<td>Formatar</td>
<td>Aplicável somente para serialização JSON. Linha separada Especifica que a saída de hello será formatada tendo cada objeto JSON separado por uma nova linha. Matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Renovar autorização do Repositório Data Lake
Você precisará toore-autenticar sua conta do repositório Data Lake se sua senha foi alterado desde que o trabalho foi criado ou última autenticado.

![Autorizar o Repositório Data Lake](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>Banco de Dados SQL
[banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/) pode ser usado como saída para os dados que sejam relacionais por natureza ou para aplicativos que dependam de o conteúdo ser hospedado em um banco de dados relacional. Trabalhos do Stream Analytics gravará tabela existente tooan em um banco de dados do SQL Azure.  Observe que esse esquema de tabela Olá deve corresponder exatamente ao campos hello e seus tipos sendo a saída do seu trabalho. Um [Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) também pode ser especificado como uma saída via Olá banco de dados SQL opção de saída também (esse é um recurso de visualização). Olá tabela a seguir lista os nomes de propriedade hello e sua descrição para a criação de um banco de dados SQL de saída.

| Nome da Propriedade | Descrição |
| --- | --- |
| Alias de saída |Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis banco de dados. |
| Banco de dados |nome de saudação do banco de dados de saudação em que você está enviando a saída |
| Nome do Servidor |nome do servidor de banco de dados SQL Olá |
| Nome de Usuário |Olá, nome de usuário que tem o banco de dados do access toowrite toohello |
| Senha |o banco de dados do Hello senha tooconnect toohello |
| Tabela |nome da tabela Olá onde Olá saída será gravada. nome da tabela Olá diferencia maiusculas de minúsculas e esquema Olá desta tabela deve corresponder exatamente toohello número de campos e seus tipos que está sendo gerados pela sua saída de trabalho. |

> [!NOTE]
> Oferta de banco de dados do Azure SQL Olá é suportada para uma saída de trabalho do Stream Analytics. No entanto, não há suporte para a execução de uma Máquina Virtual do Azure que executa o SQL Server com um banco de dados anexado. Este é o assunto toochange em versões futuras.
> 
> 

## <a name="blob-storage"></a>Armazenamento de blob
Armazenamento de blob oferece uma solução econômica e dimensionável para armazenar grandes quantidades de dados não estruturados em nuvem hello.  Para obter uma introdução sobre o armazenamento de BLOBs do Azure e seu uso, consulte a documentação de saudação em [como Blobs de toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

Olá tabela a seguir lista os nomes de propriedade hello e sua descrição para a criação de uma saída de blob.

<table>
<tbody>
<tr>
<td>Nome da Propriedade</td>
<td>Descrição</td>
</tr>
<tr>
<td>Alias de saída</td>
<td>Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis o armazenamento de blob.</td>
</tr>
<tr>
<td>Conta de armazenamento</td>
<td>nome de Olá Olá da conta de armazenamento em que você está enviando a saída.</td>
</tr>
<tr>
<td>Chave da conta de armazenamento</td>
<td>chave de segredo do Hello associado à conta de armazenamento hello.</td>
</tr>
<tr>
<td>Contêiner de armazenamento</td>
<td>Os contêineres fornecem um agrupamento lógico para os blobs armazenados no hello serviço Blob do Microsoft Azure. Quando você carregar um blob de toohello serviço Blob, você deve especificar um contêiner de blob.</td>
</tr>
<tr>
<td>Padrão de prefixo do caminho [opcional]</td>
<td>caminho do arquivo Hello usado toowrite seus blobs dentro do contêiner especificado hello.<BR>No caminho hello, você pode escolher toouse uma ou mais instâncias de saudação 2 variáveis toospecify Olá frequência com que blobs são gravados a seguir:<BR>{data}, {hora}<BR>Exemplo 1: cluster1/logs /{data}/{hora}<BR>Exemplo 2: cluster1/logs/{data}</td>
</tr>
<tr>
<td>Formato de data [opcional]</td>
<td>Se o token de data de saudação é usado no caminho de prefixo hello, você pode selecionar o formato de data de saudação na qual os arquivos são organizados. Exemplo: AAAA/MM/DD</td>
</tr>
<tr>
<td>Formato de hora [opcional]</td>
<td>Se o token de tempo de saudação é usado no caminho de prefixo Olá, especifique o formato de tempo de saudação na qual os arquivos são organizados. Atualmente, o valor de saudação só tem suportada é HH.</td>
</tr>
<tr>
<td>Formato de serialização do evento</td>
<td>Formato de serialização para dados de saída.  Há suporte para JSON, CSV e Avro.</td>
</tr>
<tr>
<td>Codificação</td>
<td>Se o formato for CSV ou JSON, uma codificação deve ser especificada. UTF-8 é Olá somente suporte para formato de codificação no momento.</td>
</tr>
<tr>
<td>Delimitador</td>
<td>Aplicável somente à serialização de CSV. O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados CSV. Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical.</td>
</tr>
<tr>
<td>Formatar</td>
<td>Aplicável somente para serialização JSON. Linha separada Especifica que a saída de hello será formatada tendo cada objeto JSON separado por uma nova linha. Matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON. Essa matriz somente quando Olá trabalho será interrompido ou Stream Analytics foi movido na próxima janela de tempo toohello será fechada. Em geral, é preferível toouse linha JSON separado, já que não exige nenhuma manipulação especial ao arquivo de saída de hello ainda está sendo gravado.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Hub de evento
[Hubs de Eventos](https://azure.microsoft.com/services/event-hubs/) são um ingestor de eventos altamente escalonável de publicação/assinatura. Ele pode coletar milhões de eventos por segundo.  Um uso de um Hub de eventos como saída é quando a saída de hello de um trabalho de análise de fluxo entrada hello de outro fluxo de trabalho.

Há alguns parâmetros que são necessários tooconfigure fluxos de dados de Hub de eventos como saída.

| Nome da Propriedade | Descrição |
| --- | --- |
| Alias de saída |Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis Hub de eventos. |
| Namespace do Barramento de Serviço |Um namespace Barramento de Serviço é um contêiner para um conjunto de entidades de mensagens. Ao criar um novo Hub de Eventos, você também criou um namespace Barramento de Serviço. |
| Hub de evento |nome de saudação do seu Hub de eventos de saída |
| Nome da política do Hub de Eventos. |Olá política de acesso compartilhado, que pode ser criada na guia Configurar do Hub de eventos de saudação. Cada política de acesso compartilhado terá um nome, as permissões definidas por você e as chaves de acesso. |
| Chave de política do Hub de eventos |chave de acesso compartilhado Olá usado namespace de barramento de serviço do tooauthenticate acesso toohello |
| Coluna de chave de partição [opcional] |Esta coluna contém a chave de partição de saudação de saída do Hub de eventos. |
| Formato de serialização do evento |Formato de serialização para dados de saída.  Há suporte para JSON, CSV e Avro. |
| Codificação |Para CSV e JSON, UTF-8 é Olá somente suporte para formato de codificação no momento |
| Delimitador |Aplicável somente à serialização de CSV. O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados no formato CSV. Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical. |
| Formatar |Aplicável somente para o tipo JSON. Linha separada Especifica que a saída de hello será formatada tendo cada objeto JSON separado por uma nova linha. Matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) pode ser usado como uma saída para um tooprovide de trabalho de análise de fluxo para uma experiência de visualização sofisticada dos resultados da análise. Essa funcionalidade pode ser usada para painéis operacionais, geração de relatórios e relatórios orientados por métricas.

### <a name="authorize-a-power-bi-account"></a>Autorizar uma conta do Power BI
1. Quando o Power BI é selecionado como uma saída de hello portal do Azure, você vai ser solicitado tooauthorize um usuário existente do Power BI ou toocreate uma nova conta do Power BI.  
   
   ![Autorizar usuário do Power BI](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Crie uma nova conta se você não ainda tiver uma e, em seguida, clique em Autorizar agora.  Uma tela semelhante Olá seguinte é exibida.  
   
   ![Conta do Azure Power BI](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. Nesta etapa, forneça o trabalho de saudação ou de estudante conta para autorizar a saída do Power BI hello. Se você não se inscreveu ainda no Power BI, escolha a opção Inscreva-se agora. Olá conta corporativa ou escolar, que você pode usar para o Power BI pode ser diferente da saudação conta de assinatura do Azure que você está conectado no momento.

### <a name="configure-hello-power-bi-output-properties"></a>Configurar propriedades de saída do Power BI Olá
Uma vez que a conta do Power BI Olá autenticada, você pode configurar propriedades de saudação para a saída do Power BI. tabela de saudação abaixo é lista Olá de nomes de propriedade e sua descrição tooconfigure a saída do Power BI.

| Nome da Propriedade | Descrição |
| --- | --- |
| Alias de saída |Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis saída do Power BI. |
| Agrupar o espaço de trabalho |tooenable compartilhamento de dados com outros usuários do Power BI, você pode selecionar grupos dentro de seu Power BI conta ou escolher "Meu espaço de trabalho" se não quiser toowrite tooa grupo.  Atualizar um grupo existente exige a autenticação do Power BI Olá de renovação. |
| Nome do conjunto de dados |Forneça um nome de conjunto de dados que é desejado pela Olá Power BI toouse de saída |
| Nome da tabela |Forneça um nome de tabela no conjunto de dados de saudação de saudação saída do Power BI. Atualmente, a saída do Power BI de trabalhos do Stream Analytics só podem ter uma tabela em um conjunto de dados. |

Para obter instruções de como configurar uma saída do Power BI e o painel, consulte Olá [Stream Analytics do Azure e Power BI](stream-analytics-power-bi-dashboard.md) artigo.

> [!NOTE]
> Não crie explicitamente Olá conjunto de dados e tabela no painel do Power BI hello. Olá conjunto de dados e tabela serão preenchidos automaticamente quando Olá trabalho é iniciado e Olá inicia bombeamento de saída para o Power BI. Observe que, se a consulta de trabalho Olá não gera qualquer resultados, o conjunto de dados de saudação e a tabela não será criada. Além disso, esteja ciente de que, se o Power BI já tem um conjunto de dados e uma tabela com hello mesmo nome hello um fornecido neste trabalho de análise de fluxo, Olá os dados existentes serão substituídos.
> 
> 

### <a name="schema-creation"></a>Criação de Esquema
Análise de fluxo do Azure cria um conjunto de dados do Power BI e uma tabela em nome de usuário de saudação se ainda não existir. Em todos os outros casos, a tabela de saudação é atualizada com novos valores. Atualmente, há uma limitação de saudação que somente uma tabela pode existir dentro de um conjunto de dados.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>Conversão de ASA tooPower BI de tipo de dados
O Azure Stream Analytics atualiza o modelo de dados de saudação dinamicamente em tempo de execução se Olá saída alterações de esquema. Alterações de nome de coluna, as alterações de tipo de coluna e Olá adição ou remoção de colunas são todos rastreadas.

Esta tabela abrange Olá conversões de tipo de dados de [tipos de dados de análise de fluxo](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [tipos de modelo de dados de entidade (EDM)](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) se um conjunto de dados do POWER BI e a tabela não existe.


Do Stream Analytics | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | Cadeia de caracteres
datetime | DateTime
flutuante | Duplo
Matriz de registro | Tipo de cadeia de caracteres, Valor da constante “IRecord” ou “IArray”

### <a name="schema-update"></a>Atualização do Esquema
Análise de fluxo infere o esquema de modelo de dados de saudação com base no primeiro o conjunto de eventos na saída Olá Olá. Posteriormente, se necessário, esquema de modelo de dados de saudação é atualizada tooaccommodate eventos de entrada que não se encaixam no esquema original hello.

Olá `SELECT *` consulta deve ser evitada tooprevent a atualização de esquema dinâmico entre linhas. Além disso toopotential implicações de desempenho, ele também resultaria em indeterminacy de tempo Olá para resultados de saudação. campos Olá exato necessário toobe mostrada no painel do Power BI devem ser selecionados. Além disso, os valores de dados Olá devem ser compatíveis com hello escolhido o tipo de dados.


Anterior/Atual | Int64 | Cadeia de caracteres | DateTime | Duplo
-----------------|-------|--------|----------|-------
Int64 | Int64 | Cadeia de caracteres | Cadeia de caracteres | Duplo
Duplo | Duplo | Cadeia de caracteres | Cadeia de caracteres | Duplo
Cadeia de caracteres | Cadeia de caracteres | Cadeia de caracteres | Cadeia de caracteres |  | Cadeia de caracteres | 
DateTime | Cadeia de caracteres | Cadeia de caracteres |  DateTime | Cadeia de caracteres


### <a name="renew-power-bi-authorization"></a>Renovar a autorização do Power BI
Você precisará toore-autenticar sua conta do Power BI se sua senha foi alterado desde que o trabalho foi criado ou última autenticado. Se a autenticação multifator (MFA) é configurado no seu locatário do Azure Active Directory (AAD) também será necessário autorização do Power BI de toorenew cada 2 semanas. Um sintoma desse problema é nenhuma saída de trabalho e um "Erro de usuário autenticar" nos Logs de operação hello:

  ![Erro de token de atualização do Power BI](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve esse problema, interromper seu trabalho em execução e vá tooyour saída do Power BI.  Clique o link de "Renovar autorização" Olá e reinicie o trabalho de saudação perda de dados tooavoid hora da última interrupção.

  ![Autorização de renovação do Power BI](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Armazenamento de tabela
[Armazenamento de tabela do Azure](../storage/common/storage-introduction.md) oferece armazenamento altamente disponível e altamente escalonável, para que um aplicativo pode dimensionar automaticamente toomeet demanda do usuário. Armazenamento de tabela é repositório de chave/atributos de NoSQL da Microsoft que pode aproveitar para dados estruturados com menos restrições no esquema de saudação. Armazenamento de tabela do Azure pode ser dados de toostore usado para persistência e recuperação eficiente.

Olá tabela a seguir lista os nomes de propriedade hello e sua descrição para a criação de uma saída de tabela.

| Nome da Propriedade | Descrição |
| --- | --- |
| Alias de saída |Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis o armazenamento de tabela. |
| Conta de armazenamento |nome de Olá Olá da conta de armazenamento em que você está enviando a saída. |
| Chave da conta de armazenamento |chave de acesso Olá associada à conta de armazenamento hello. |
| Nome da tabela |nome de saudação da tabela de saudação. tabela de saudação será obter criada se não existir. |
| Chave de partição |nome de Olá Olá saída coluna contendo Olá chave de partição. chave de partição Olá é um identificador exclusivo para a partição hello dentro de uma determinada tabela que constitui Olá primeira parte da chave primária da entidade. É um valor de cadeia de caracteres que pode ser up too1 KB de tamanho. |
| Chave de linha |nome de Olá Olá saída contendo Olá linha da chave de coluna. chave de linha de saudação é um identificador exclusivo para uma entidade em uma determinada partição. Constitui a segunda parte Olá de chave primária da entidade. chave de linha de saudação é um valor de cadeia de caracteres que pode ser up too1 KB de tamanho. |
| Tamanho do lote |número de saudação de registros para uma operação em lote. Normalmente padrão Olá é suficiente para a maioria dos trabalhos, consulte toohello [especificações de operação de lote de tabela](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) para obter mais detalhes sobre como modificar essa configuração. |

## <a name="service-bus-queues"></a>Filas de barramento de serviço
[Filas do barramento de serviço](https://msdn.microsoft.com/library/azure/hh367516.aspx) oferecem um primeiro a entrar, tooone de entrega de mensagem PEPS (primeiro) ou mais consumidores concorrentes. Normalmente, as mensagens são esperado toobe recebidas e processadas pelos destinatários de saudação na Olá ordem temporal em que eles foram adicionados toohello fila, e cada mensagem é recebida e processada por apenas um cliente de mensagem.

Olá tabela a seguir lista os nomes de propriedade hello e sua descrição para a criação de uma saída de fila.

| Nome da Propriedade | Descrição |
| --- | --- |
| Alias de saída |Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis fila do barramento de serviço. |
| Namespace do Barramento de Serviço |Um namespace Barramento de Serviço é um contêiner para um conjunto de entidades de mensagens. |
| Nome da fila |nome de saudação do hello fila do barramento de serviço. |
| Nome da política da fila |Quando você criar uma fila, você também pode criar políticas de acesso compartilhado na guia Configurar fila de saudação. Cada política de acesso compartilhado terá um nome, as permissões definidas por você e as chaves de acesso. |
| Chave de política de fila |chave de acesso compartilhado Olá usado namespace de barramento de serviço do tooauthenticate acesso toohello |
| Formato de serialização do evento |Formato de serialização para dados de saída.  Há suporte para JSON, CSV e Avro. |
| Codificação |Para CSV e JSON, UTF-8 é Olá somente suporte para formato de codificação no momento |
| Delimitador |Aplicável somente à serialização de CSV. O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados no formato CSV. Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical. |
| Formatar |Aplicável somente para o tipo JSON. Linha separada Especifica que a saída de hello será formatada tendo cada objeto JSON separado por uma nova linha. Matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON. |

## <a name="service-bus-topics"></a>Tópicos do Service Bus
Enquanto as filas do Service Bus fornecem um método de comunicação de tooone um do remetente tooreceiver, [tópicos do barramento de serviço](https://msdn.microsoft.com/library/azure/hh367516.aspx) fornecem uma forma de um-para-muitos de comunicação.

Olá tabela a seguir lista os nomes de propriedade hello e sua descrição para a criação de uma saída de tabela.

| Nome da Propriedade | Descrição |
| --- | --- |
| Alias de saída |Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis tópico do barramento de serviço. |
| Namespace do Barramento de Serviço |Um namespace Barramento de Serviço é um contêiner para um conjunto de entidades de mensagens. Ao criar um novo Hub de Eventos, você também criou um namespace Barramento de Serviço. |
| Nome do tópico |Tópicos são mensagens entidades, hubs de tooevent semelhante e filas. Eles são projetados toocollect fluxos de eventos de um número de diferentes dispositivos e serviços. Quando um tópico é criado, ele também recebe um nome específico. mensagens de saudação enviadas tooa tópico não estará disponível a menos que uma assinatura é criada, para garantir que há uma ou mais assinaturas no tópico Olá |
| Nome da política de tópico |Quando você cria um tópico, você também pode criar políticas de acesso compartilhado na guia Configurar tópico de saudação. Cada política de acesso compartilhado terá um nome, as permissões definidas por você e as chaves de acesso. |
| Chave de política do tópico |chave de acesso compartilhado Olá usado namespace de barramento de serviço do tooauthenticate acesso toohello |
| Formato de serialização do evento |Formato de serialização para dados de saída.  Há suporte para JSON, CSV e Avro. |
| Codificação |Se o formato for CSV ou JSON, uma codificação deve ser especificada. UTF-8 é Olá somente suporte para formato de codificação no momento |
| Delimitador |Aplicável somente à serialização de CSV. O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados no formato CSV. Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
O [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) é um serviço de banco de dados de documentos NoSQL totalmente gerenciado que oferece consulta e transações de dados sem esquemas, com desempenho previsível e confiável e desenvolvimento rápido.

Olá abaixo nomes de propriedade lista detalhes hello e sua descrição para a criação de uma saída de banco de dados do Azure Cosmos.

* **Alias de saída** – um toorefer alias esta saída em sua consulta ASA  
* **O nome da conta** – nome hello ou ponto de extremidade URI da saudação conta de banco de dados do Cosmos.  
* **Chave de conta** – chave de acesso compartilhado Olá para Olá conta de banco de dados do Cosmos.  
* **Banco de dados** – nome de banco de dados do banco de dados do Cosmos hello.  
* **Padrão de nome** – nome da coleção hello ou seu padrão para Olá coleções toobe usado. formato de nome de coleção Olá pode ser construído usando o token {partition} opcional de hello, onde as partições começam do 0. A seguir estão as entradas válidas de exemplo:  
  1\) MyCollection – uma coleção denominada “MyCollection” deve existir.  
  2\) MyCollection{partition} – estas coleções devem existir – "MyCollection0”, “MyCollection1”, “MyCollection2” e assim por diante.  
* **Chave de Partição** — opcional. Isso só será necessário se você estiver usando um token {partition} no seu padrão de nome de coleção. nome de saudação do campo de saudação na saída eventos usados toospecify Olá chave para particionamento de saída por coleções. Para uma saída de coleção única, nenhuma coluna de saída arbitrária pode ser usada, por exemplo, PartitionId.  
* **ID do Documento** : opcional. nome de saudação do campo Olá em eventos de saída usado chave primária de saudação toospecify nas quais insert ou update operações são baseadas.  


## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
Foi introduzido tooStream Analytics, um serviço gerenciado para streaming de análise de dados de saudação Internet das coisas. toolearn mais informações sobre esse serviço, consulte:

* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
