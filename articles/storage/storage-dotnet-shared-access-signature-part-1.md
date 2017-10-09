---
title: aaaUsing compartilhado (SAS) de assinaturas de acesso no armazenamento do Azure | Microsoft Docs
description: Saiba toouse compartilhado acesso assinaturas (SAS) toodelegate acesso tooAzure recursos de armazenamento, incluindo blobs, filas, tabelas e arquivos.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 53e06c78fbfdaa5fd209add719995ef2a6bc8f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Usando SAS (Assinaturas de Acesso Compartilhado)

Uma assinatura de acesso compartilhado (SAS) fornece um tooobjects de acesso do modo toogrant limitado em sua conta de armazenamento tooother clientes, sem expor sua chave de conta. Neste artigo, nós fornecem uma visão geral do modelo SAS hello, analisar as práticas recomendadas SAS e ver alguns exemplos.

Para exemplos de código adicionais usando a SAS além daquelas apresentadas aqui, consulte [guia de Introdução ao armazenamento de BLOBs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) e outros exemplos disponíveis em Olá [exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?service=storage) biblioteca. Você pode baixar aplicativos de exemplo hello e executá-los ou procurar Olá código no GitHub.

## <a name="what-is-a-shared-access-signature"></a>O que é uma assinatura de acesso compartilhado?
Uma assinatura de acesso compartilhado fornece acesso delegado tooresources na sua conta de armazenamento. Com uma SAS, você pode conceder a clientes acessam tooresources na sua conta de armazenamento sem compartilhar suas chaves de conta. Este é o ponto-chave saudação do uso de assinaturas de acesso compartilhado em seus aplicativos – uma SAS é uma maneira segura tooshare seus recursos de armazenamento sem comprometer as chaves da conta.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

Uma SAS fornece controle granular sobre o tipo de saudação do access que conceder tooclients com hello SAS, incluindo:

* intervalo de saudação sobre quais Olá SAS é válido, incluindo hora de início do hello e tempo de expiração de saudação.
* Olá permissões por Olá SAS. Por exemplo, um SAS para um blob pode conceder ler e gravar permissões toothat blob, mas não excluir permissões.
* Um endereço IP opcional ou intervalo de endereços IP dos quais o armazenamento do Azure aceitará Olá SAS. Por exemplo, você pode especificar um intervalo de endereços IP que pertencem a organização tooyour.
* protocolo de saudação durante o qual o armazenamento do Azure aceitará Olá SAS. Você pode usar este parâmetro opcional toorestrict acesso tooclients que usando HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Quando você deve usar uma assinatura de acesso compartilhado?
Você pode usar uma SAS quando desejar tooprovide acesso tooresources no seu cliente de tooany de conta de armazenamento que não possui chaves de acesso da sua conta de armazenamento. Sua conta de armazenamento inclui tanto uma chave de acesso primária e secundária, que conceder a conta de acesso administrativo a tooyour e todos os recursos nele. Exposição de qualquer uma dessas chaves abre sua possibilidade de toohello de conta de uso mal-intencionado ou negligente. Assinaturas de acesso compartilhado fornecem uma alternativa segura que permite que os clientes tooread, gravação e exclusão de dados em sua conta de armazenamento de acordo com as permissões de toohello concedido explicitamente e sem necessidade de uma chave de conta.

Um cenário comum em que uma SAS é útil é um serviço em que os usuários ler e gravar sua própria conta de armazenamento do tooyour de dados. Em um cenário em que uma conta de armazenamento armazena dados do usuário, há dois padrões de design comuns:

1. Os clientes carregam e baixam dados por meio de um serviço de proxy front-end, que executa a autenticação. Esse serviço de proxy de front-end tem a vantagem de saudação de permitir que a validação de regras de negócio, mas para grandes quantidades de dados ou alto volume de transações, criando um serviço que pode ser dimensionado toomatch demanda pode ser difícil ou cara.

  ![Diagrama do cenário: serviço de proxy front-end][sas-storage-fe-proxy-service]

1. Um serviço simples autentica o cliente Olá conforme necessário e, em seguida, gera um SAS. Depois que o cliente Olá recebe Olá SAS, eles podem acessar recursos da conta de armazenamento diretamente com permissões de saudação definidas por Olá SAS e para o intervalo de saudação permitido pelo Olá SAS. Olá SAS reduz a necessidade de saudação para roteamento de todos os dados por meio do serviço de proxy de front-end de saudação.

  ![Diagrama do cenário: serviço do provedor de SAS][sas-storage-provider-service]

Muitos serviços reais podem usar uma combinação dessas duas abordagens. Por exemplo, alguns dados podem processados e validados por meio do proxy de front-end hello, enquanto outros dados é salvo e/ou ler diretamente usando a SAS.

Além disso, você precisará toouse um objeto de fonte de saudação tooauthenticate SAS em uma operação de cópia em determinados cenários:

* Quando você copia um blob de tooanother de blob que reside em uma conta de armazenamento diferente, você deve usar um blob de origem SAS tooauthenticate hello. Opcionalmente, você pode usar um SAS tooauthenticate Olá blob de destino também.
* Quando você copia um arquivo de tooanother que reside em uma conta de armazenamento diferente, você deve usar um arquivo de origem do SAS tooauthenticate hello. Opcionalmente, você pode usar um SAS tooauthenticate Olá arquivo de destino também.
* Quando você copia um arquivo de blob tooa ou um blob de tooa de arquivo, você deve usar um objeto de origem do SAS tooauthenticate hello, mesmo se os objetos de origem e destino Olá residem dentro de saudação mesma conta de armazenamento.

## <a name="types-of-shared-access-signatures"></a>Tipos de assinaturas de Acesso compartilhado.
É possível criar dois tipos de assinaturas de acesso compartilhado:

* **SAS de Serviço.** delegados SAS do serviço Olá acessam o recurso de tooa em apenas um dos serviços de armazenamento Olá: Olá serviço Blob, fila, tabela ou arquivo. Consulte [construindo uma SAS do serviço](https://msdn.microsoft.com/library/dn140255.aspx) e [exemplos de SAS do serviço](https://msdn.microsoft.com/library/dn140256.aspx) para obter informações detalhadas sobre como construir o token SAS do serviço de saudação.
* **SAS de Conta.** delegados de SAS conta Olá acessar tooresources em um ou mais dos serviços de armazenamento de saudação. Todas as operações de saudação disponíveis por meio de um serviço SAS também estão disponíveis por meio de uma conta de SAS. Além disso, com a conta de saudação SAS, você pode delegar acesso toooperations que se aplicam a tooa fornecido como o serviço, **propriedades do serviço de Get/Set** e **obter status do serviço**. Você também pode delegar acesso tooread, gravação e operações de exclusão em contêineres de blob, tabelas, filas e compartilhamentos de arquivos que não são permitidos com um serviço de SAS. Consulte [construindo uma SAS da conta](https://msdn.microsoft.com/library/mt584140.aspx) para obter informações detalhadas sobre como construir o token SAS Olá conta.

## <a name="how-a-shared-access-signature-works"></a>Como funciona uma assinatura de acesso compartilhado
Uma assinatura de acesso compartilhado é um URI assinado que aponta tooone ou mais recursos de armazenamento e inclui um token que contém um conjunto especial de parâmetros de consulta. token de saudação indica como os recursos de saudação podem ser acessados pelo cliente hello. Um dos parâmetros de consulta hello, Olá assinatura, é construído a partir de parâmetros de SAS hello e assinado com a chave da conta hello. Esta assinatura é usada pelo Olá tooauthenticate de armazenamento do Azure SAS.

Aqui está um exemplo de um URI de SAS, URI de recurso Olá mostrando e token SAS hello:

![Componentes de um URI de SAS][sas-storage-uri]

Olá, token SAS é uma cadeia de caracteres que você gera Olá *cliente* lado (consulte Olá [exemplos SAS](#sas-examples) seção para obter exemplos de código). Um token SAS que gerar com biblioteca de cliente de armazenamento hello, por exemplo, não será controlado pelo armazenamento do Azure de qualquer forma. Você pode criar um número ilimitado de tokens SAS no lado do cliente de saudação.

Quando um cliente fornece um tooAzure URI SAS armazenamento como parte de uma solicitação, o serviço de saudação verifica parâmetros de SAS hello e tooverify de assinatura é válida para autenticar a solicitação de saudação. Se o serviço Olá verifica a que assinatura Olá é válida, solicitação de saudação é autenticada. Caso contrário, a solicitação de saudação é recusada com o código de erro 403 (proibido).

## <a name="shared-access-signature-parameters"></a>Parâmetros de assinatura de acesso compartilhado
conta Olá SAS e tokens SAS do serviço incluem alguns parâmetros comuns e também levar alguns parâmetros que são diferentes.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Parâmetros comuns tooaccount SAS e tokens SAS do serviço
* **Versão da API** um parâmetro opcional que especifica a solicitação de Olá Olá armazenamento serviço versão toouse tooexecute.
* **Versão do serviço** um parâmetro obrigatório que especifica a solicitação de Olá Olá armazenamento serviço versão toouse tooauthenticate.
* **Hora de início.** Este é o tempo de saudação na qual Olá SAS se torna válida. hora de início de saudação para uma assinatura de acesso compartilhado é opcional. Se uma hora de início for omitida, Olá SAS é imediatamente efetivada. Olá hora de início deve ser expressa em UTC (Universal Coordenado), com um designador de UTC especial ("Z"), por exemplo `1994-11-05T13:15:30Z`.
* **Hora de expiração.** Este é Olá tempo após o qual hello SAS não é mais válido. As melhores práticas sugerem que você especifique uma hora de expiração para uma SAS ou associe-a a uma política de acesso armazenada. Olá tempo de expiração deve ser expressa em UTC (Universal Coordenado), com um designador de UTC especial ("Z"), por exemplo `1994-11-05T13:15:30Z` (consulte mais abaixo).
* **Permissões.** permissões de saudação especificadas em Olá SAS indicam quais operações cliente Olá pode executar em relação a recurso de armazenamento hello usando Olá SAS. As permissões disponíveis são diferentes entre SAS de conta e de serviço.
* **IP.** Um parâmetro opcional que especifica um endereço IP ou um intervalo de endereços IP fora do Azure (consulte a seção Olá [estado de configuração de sessão de roteamento](../expressroute/expressroute-workflows.md#routing-session-configuration-state) de rota expressa) do que as solicitações tooaccept.
* **Protocolo.** Um parâmetro opcional que especifica o protocolo de saudação permitido para uma solicitação. Os valores possíveis são HTTP e HTTPS (`https,http`), que é valor padrão de hello, ou HTTPS apenas (`https`). Observe que somente HTTP não é um valor permitido.
* **Assinatura.** Olá assinatura é construída de saudação outros parâmetros especificados como parte de token e, em seguida, criptografado. Ele usou tooauthenticate Olá SAS.

### <a name="parameters-for-a-service-sas-token"></a>Parâmetros para um token SAS de serviço
* **Recurso de armazenamento.** Os recursos de armazenamento para os quais é possível delegar acesso com SAS de serviço incluem:
  * Contêineres e blobs
  * Compartilhamentos de arquivos e arquivos
  * Filas
  * Tabelas e intervalos de entidades de tabela.

### <a name="parameters-for-an-account-sas-token"></a>Parâmetros para um token SAS de conta
* **Serviço ou serviços.** Uma conta SAS pode delegar acesso tooone ou mais dos serviços de armazenamento de saudação. Por exemplo, você pode criar uma conta SAS delegados acessar toohello serviço de Blob e o arquivo. Ou você pode criar uma SAS delegados acessar tooall quatro serviços (Blob, fila, tabela e arquivo).
* **Tipos de recurso de armazenamento.** Aplica-se uma conta SAS tooone ou mais classes de recursos de armazenamento, em vez de um recurso específico. Você pode criar uma conta SAS toodelegate acesso a:
  * APIs de nível de serviço, que são chamados no recurso de conta de armazenamento hello. Os exemplos incluem **Obter/Definir Propriedades do Serviço**, **Obter Estatísticas do Serviço** e **Listar Contêineres/Filas/Tabelas/Compartilhamentos**.
  * APIs de nível de contêiner, que são chamados em objetos de contêiner de saudação para cada serviço: tabelas, filas, contêineres de blob e compartilhamentos de arquivos. Os exemplos incluem **Criar/Excluir Contêiner**, **Criar/Excluir Fila**, **Criar/Excluir Tabela**, **Criar/Excluir Compartilhamento** e **Listar Blobs/Arquivos e Diretórios**.
  * APIs de nível de objeto, que são chamadas em relação a blobs, mensagens de fila, entidades de tabela e arquivos. Por exemplo, **Colocar Blob**, **Consultar Entidade**, **Obter Mensagens** e **Criar Arquivo**.

## <a name="examples-of-sas-uris"></a>Exemplos de URIs de SAS

### <a name="service-sas-uri-example"></a>Exemplo de URI de SAS de serviço

Aqui está um exemplo de um serviço de URI de SAS que fornece de leitura e gravação de blob de tooa de permissões. tabela Olá divide cada parte da saudação URI toounderstand como contribui toohello SAS:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Nome | Parte SAS | Descrição |
| --- | --- | --- |
| URI do blob |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |endereço de saudação do blob hello. Observe que o uso de HTTPS é altamente recomendável. |
| Versão dos serviços de armazenamento |`sv=2015-04-05` |Para serviços de armazenamento versão 2012-02-12 e mais tarde, esse parâmetro indica Olá versão toouse. |
| Hora de início |`st=2015-04-29T22%3A18%3A26Z` |Especificado no horário UTC. Se você quiser Olá SAS toobe válido imediatamente, omita a hora de início da saudação. |
| Hora de expiração |`se=2015-04-30T02%3A23%3A26Z` |Especificado no horário UTC. |
| Recurso |`sr=b` |recurso de saudação é um blob. |
| Permissões |`sp=rw` |permissões de saudação concedidas por Olá SAS incluem Read (r) e gravação (w). |
| Intervalo IP |`sip=168.1.5.60-168.1.5.70` |Olá intervalo de endereços IP do qual uma solicitação será aceita. |
| Protocolo |`spr=https` |São permitidas somente solicitações usando HTTPS. |
| Signature |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Usado tooauthenticate blob de toohello de acesso. assinatura de saudação é um HMAC computado em uma cadeia de caracteres de entrada e uma chave usando o algoritmo SHA256 de saudação e, em seguida, codificados usando a codificação de Base64. |

### <a name="account-sas-uri-example"></a>Exemplo de URI de SAS de conta

Aqui está um exemplo de uma conta de SAS que usa Olá mesmo parâmetros comuns no token de saudação. Como esses parâmetros estão descritos acima, eles não serão descritos aqui. Apenas os parâmetros de saudação que são específico tooaccount que SAs são descritos na tabela de saudação abaixo.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Nome | Parte SAS | Descrição |
| --- | --- | --- |
| URI de recurso |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Olá serviço ponto de extremidade Blob, com parâmetros para obter as propriedades de serviço (quando chamado com GET) ou definindo propriedades de serviço (quando chamado com conjunto). |
| Serviços |`ss=bf` |Olá SAS aplica toohello Blob e serviços de arquivo |
| Tipos de recurso |`srt=s` |Olá SAS se aplica a operações de tooservice. |
| Permissões |`sp=rw` |permissões de saudação conceder acesso tooread e operações de gravação. |

Considerando que as permissões são restritas toohello de nível de serviço, operações acessíveis com esse SAS são **obter propriedades do serviço Blob** (leitura) e **definir propriedades do serviço Blob** (gravação). No entanto, com um URI de recurso diferente, hello mesmo token SAS também pode ser usado toodelegate acesso muito**obter status do serviço Blob** (leitura).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Controlando uma SAS com uma política de acesso armazenada
Uma assinatura de acesso compartilhado pode assumir uma destas duas formas:

* **SAS ad hoc:** quando você criar um SAS ad hoc, a hora de início de saudação, o tempo de expiração e permissões para Olá SAS são especificadas no hello URI SAS (ou implícita, no caso de Olá onde a hora de início é omitida). Esse tipo de SAS pode ser criada como uma SAS de conta ou de serviço.
* **SAS com a política de acesso armazenada:** uma política de acesso armazenada é definido em um contêiner de recursos – um contêiner de blob, tabela, fila, ou arquivo compartilhamento – e pode ser usado toomanage restrições para uma ou mais assinaturas de acesso compartilhado. Quando você associa uma SAS com uma política de acesso armazenada, Olá SAS herda restrições hello – hora de início da saudação, tempo de expiração e permissões – definidas para a política de acesso Olá armazenado.

> [!NOTE]
> Atualmente, uma SAS de conta deve ser uma SAS ad hoc. As SAS de conta ainda não dão suporte a políticas de acesso armazenadas.

Olá diferença entre formulários Olá dois é importante para um cenário de chave: revogação. Como um URI de SAS é uma URL, qualquer pessoa que obtém Olá SAS pode usá-lo, independentemente de quem o criou originalmente. Se uma SAS é publicada publicamente, ele pode ser usado por qualquer pessoa no Olá, mundo. Uma SAS concede acesso tooresources tooanyone que possui-lo até que uma das quatro situações ocorra:

1. tempo de expiração de saudação especificado em Olá que SAS é atingido.
2. tempo de expiração de saudação especificado na política de acesso de saudação armazenada referenciada por Olá que SAS é atingido (se uma política de acesso armazenada for referenciada e se ela especifica uma hora de expiração). Isso pode ocorrer porque o intervalo de saudação expira, ou porque você modificou a política de acesso de saudação armazenada com um tempo de expiração em Olá anterior, que é uma maneira toorevoke hello SAS.
3. Olá armazenado referenciada por Olá que SAS é excluído, que é Olá toorevoke de outra maneira SAS de política de acesso. Observe que se você recriar a política de acesso de saudação armazenada com exatamente Olá SAS existentes de mesmo nome os tokens serão novamente ser válido acordo toohello permissões associadas a essa política de acesso armazenada (supondo que essa hora de expiração Olá em Olá SAS não passou). Se você estiver pretendendo toorevoke Olá SAS, ser toouse se um nome diferente se você recriar a política de acesso de saudação com um tempo de expiração em Olá futuras.
4. Olá a chave de conta que foi usado toocreate Olá SAS é regenerada. Regenerar uma chave de conta fará com que todos os componentes de aplicativo usando essa chave toofail tooauthenticate até que sejam atualizados toouse hello ou outra tecla de conta válida ou Olá conta acabou de ser gerada.

> [!IMPORTANT]
> Um URI de assinatura de acesso compartilhado é associado à assinatura de Olá Olá conta chave toocreate usado e Olá associados a política de acesso armazenada (se houver). Se nenhuma política de acesso armazenada for especificada, hello toorevoke de maneira somente uma assinatura de acesso compartilhado é toochange Olá conta chave.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Autenticação de um aplicativo cliente com uma SAS
Um cliente que está em posse de um SAS pode usar Olá SAS tooauthenticate uma solicitação em relação a uma conta de armazenamento para o qual não possuem chaves de conta hello. Uma SAS pode ser incluída em uma cadeia de conexão ou usada diretamente do construtor apropriado hello ou método.

### <a name="using-a-sas-in-a-connection-string"></a>Usando uma SAS em uma cadeia de conexão
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Usar uma SAS em um construtor ou método
Vários construtores de biblioteca de cliente de armazenamento do Azure e as sobrecargas do método oferecem um parâmetro SAS, para que você possa autenticar uma solicitação de serviço toohello com uma SAS.

Por exemplo, aqui um URI de SAS é usado toocreate um blob de blocos de tooa de referência. Olá SAS fornece credenciais de somente Olá necessárias para a solicitação de saudação. referência de blob de bloco Hello, em seguida, é usada para uma operação de gravação:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Práticas recomendadas ao usar SAS
Quando você usar assinaturas de acesso compartilhado em seus aplicativos, você precisa toobe ciente dos riscos potenciais dois:

* Se ocorrer perda de uma SAS, ela poderá ser usada por qualquer pessoa que a obtiver, o que poderá comprometer a sua conta de armazenamento.
* Se uma SAS fornecido expira tooa aplicativo de cliente e aplicativo hello é tooretrieve não é possível uma nova SAS do seu serviço, a funcionalidade do aplicativo hello pode ser prejudicada.

Olá seguintes recomendações para usar assinaturas de acesso compartilhado podem ajudar a reduzir esses riscos:

1. **Sempre usar HTTPS** toocreate ou distribua uma SAS. Se uma SAS é passada sobre HTTP e interceptada, um invasor executando um ataque man-in-the-middle é capaz de tooread hello SAS e, em seguida, usá-lo como Olá destinada a usuário poderia ter comprometer potencialmente a dados confidenciais ou permitindo a corrupção de dados por Olá usuário mal-intencionado.
2. **Faça referência às políticas de acesso armazenadas sempre que possível.** Armazenado acesso políticas fornecem Olá permissões de toorevoke opção sem ter chaves de conta de armazenamento tooregenerate hello. Definir a expiração de saudação no hello muito distante futura (ou infinita) e verifique se ela foi atualizada regularmente toomove muito em Olá futuras.
3. **Use horas de expiração de curto prazo em uma SAS ad hoc.** Dessa forma, mesmo se uma SAS for comprometida, ela será válida apenas por um breve período. Esta prática será especialmente importante se você não puder fazer referência a uma política de acesso armazenada. Tempos de expiração curto prazo também limitam a quantidade de saudação de dados que podem ser gravados tooa blob limitando Olá tempo disponível tooupload tooit.
4. **Ter clientes renovar automaticamente Olá SAS, se necessário.** Os clientes devem renovar Olá SAS bem antes do vencimento do hello, no tempo de tooallow de ordem de tentativas se o serviço Olá fornecendo Olá SAS não está disponível. Se seu SAS deve toobe usado para um número pequeno de imediato, operações de curta duração que são esperados toobe concluída dentro do período de validade Olá, isso pode ser desnecessário Olá que SAS não é esperado toobe renovado. No entanto, se você tiver o cliente que normalmente está fazendo solicitações por meio de SAS, possibilidade de saudação de expiração entra em cena. Olá consideração importante é toobalance Olá necessidade para Olá SAS toobe curta duração (mencionado anteriormente) com hello necessidade tooensure que Olá cliente está solicitando a renovação antecipada suficiente (interrupção tooavoid devido a renovação toohello SAS expirando toosuccessful anterior).
5. **Tenha cuidado com a hora de início da SAS.** Se você definir a hora de início Olá um SAS muito**agora**, em seguida, devido a distorção tooclock (as diferenças na hora atual de acordo com o toodifferent máquinas), falhas podem ser observadas intermitentemente para Olá primeiro alguns minutos. Em geral, defina Olá toobe de hora de início pelo menos 15 minutos no hello anterior. Ou então, simplesmente não a defina, o que a tornará imediatamente válida em todos os casos. Olá mesmo geralmente se aplica a tempo tooexpiry também - Lembre-se de que você pode observar o too15 minutos do relógio distorção em ambas as direções em qualquer solicitação. Para clientes usando um REST versão anterior too2012-02-12, a duração máxima Olá uma SAS que não faz referência a uma política de acesso armazenada é 1 hora e as políticas de especificação de longo prazo que o que irá falhar.
6. **Ser específico com hello toobe de recurso acessado.** Uma prática recomendada de segurança é tooprovide um usuário com privilégios necessários mínimos de saudação. Se um usuário só precisa de acesso de leitura tooa única entidade, em seguida, conceda a eles acesso de leitura toothat única entidade e acesso não leitura/gravação/exclusão tooall entidades. Isso também ajuda a reduzir danos Olá se uma SAS estiver comprometida porque Olá SAS tem menos energia nas mãos de saudação do invasor.
7. **É importante que você entenda que a sua conta será cobrada por qualquer uso, incluindo o realizado com a SAS.** Se você fornecer acesso de gravação tooa blob, um usuário pode escolher tooupload um blob de 200GB. Se você fornecer acesso de leitura, eles podem escolher toodownload 10 vezes, gera 2 TB em saída custa para você. Novamente, forneça permissões limitadas toohelp reduzir possíveis ações Olá de usuários mal-intencionados. Use essa ameaça de curta duração tooreduce SAS (mas lembre-se do relógio distorção na hora de término hello).
8. **Valide os dados gravados com a SAS.** Quando um aplicativo cliente grava a conta de armazenamento tooyour dados, tenha em mente que pode haver problemas com esses dados. Se seu aplicativo requer que esses dados ser validados ou autorizados antes de ser toouse pronto, você deve executar essa validação após a gravação de dados de saudação e antes de ser usada pelo seu aplicativo. Essa prática também protege contra dados corrompidos ou mal-intencionado gravados tooyour conta, por um usuário que adquiriu corretamente Olá SAS ou por um usuário explorando uma SAS vazou.
9. **Não use sempre SAS.** Às vezes, o riscos de saudação associados a uma determinada operação em sua conta de armazenamento superam os benefícios de saudação da SAS. Para essas operações, criar um serviço de camada intermediária que grava tooyour conta de armazenamento após a realização de negócios de regras de validação, autenticação e auditoria. Além disso, às vezes é mais simples acesso toomanage de outras maneiras. Por exemplo, se você quiser o toomake todos os blobs em um contêiner podem ser lidos publicamente, você pode fazer Olá contêiner público, em vez de fornecer um cliente de tooevery SAS para acesso.
10. **Use a análise de armazenamento toomonitor seu aplicativo.** Você pode usar o registro em log e métricas tooobserve qualquer um pico em falhas de autenticação devido a interrupção tooan seu SAS provedor serviço ou toohello inadvertida remoção de uma política de acesso armazenada. Consulte Olá [Blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) para obter informações adicionais.

## <a name="sas-examples"></a>Exemplos de SAS
Abaixo estão alguns exemplos de ambos os tipos de assinatura de acesso compartilhado: SAS de conta e SAS de serviço.

toorun esses exemplos de c#, você precisa tooreference Olá pacotes do NuGet em seu projeto a seguir:

* [Biblioteca de cliente de armazenamento do Azure para .NET](http://www.nuget.org/packages/WindowsAzure.Storage), versão 6. x ou posterior (toouse conta SAS).
* [Azure Configuration Manager](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Para obter exemplos adicionais que mostram como toocreate e teste uma SAS, consulte [exemplos de código do Azure para armazenamento](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Exemplo: Criar e usar uma conta de SAS
Olá, exemplo de código a seguir cria uma conta de SAS que é válido para hello Blob e serviços de arquivo e fornece Olá permissões de cliente de leitura, gravação e as permissões de lista tooaccess nível de serviço APIs. conta Olá SAS restringe Olá protocolo tooHTTPS, para a solicitação de saudação deve ser feita com HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse Olá conta SAS tooaccess APIs de nível de serviço para o serviço de Blob hello, construir um objeto de cliente de Blob usando Olá SAS e Olá ponto de extremidade de armazenamento de Blob para sua conta de armazenamento.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Exemplo: Criar uma política de acesso armazenada
Olá código a seguir cria uma política de acesso armazenada em um contêiner. Você pode usar restrições de toospecify de política de acesso de saudação para um serviço de SAS no contêiner de saudação ou seus blobs.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Exemplo: Criar um serviço SAS em um contêiner
saudação de código a seguir cria uma SAS em um contêiner. Se o nome de saudação de uma política de acesso armazenada existente é fornecido, essa política está associada a Olá SAS. Se nenhuma política de acesso armazenada for fornecida, o código de saudação cria um SAS ad hoc no contêiner de saudação.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Exemplo: Criar um serviço SAS em um blob
saudação de código a seguir cria uma SAS em um blob. Se o nome de saudação de uma política de acesso armazenada existente é fornecido, essa política está associada a Olá SAS. Se nenhuma política de acesso armazenada for fornecida, o código de saudação cria um SAS ad hoc no blob de saudação.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Conclusão
Assinaturas de acesso compartilhado são úteis para fornecer permissões limitadas tooyour tooclients de conta de armazenamento que não deve ter a chave da conta hello. Assim, eles são uma parte essencial do modelo de segurança Olá para qualquer aplicativo usando o armazenamento do Azure. Se você seguir as práticas recomendadas de saudação listadas aqui, você pode usar a SAS tooprovide maior flexibilidade de tooresources de acesso em sua conta de armazenamento, sem comprometer a segurança de saudação do seu aplicativo.

## <a name="next-steps"></a>Próximas etapas
* [Gerenciar blobs e acesso de leitura anônimo toocontainers](storage-manage-access-to-resources.md)
* [Delegando acesso com uma assinatura de acesso compartilhado](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introdução à Tabela e à Fila SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png
