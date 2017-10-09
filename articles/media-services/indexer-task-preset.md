---
title: "aaaTask predefinido para indexador de mídia do Azure"
description: "Este tópico apresenta uma visão geral das tarefas predefinidas para o Azure Media Indexer."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Predefinição de tarefa para o Azure Media Indexer

Indexador de mídia do Azure é um processador de mídia que você use Olá tooperform tarefas a seguir: tornar arquivos de mídia e conteúdo pesquisável, gerar fechada rastreia codificadas e palavras-chave, indexar arquivos de ativo que fazem parte do seu ativo.

Este tópico descreve Olá predefinidos de tarefa que você precisa tooyour toopass trabalho de indexação. Para um exemplo completo, consulte [Indexar arquivos de mídia com o Azure Media Indexer](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>XML de configuração do Azure Media Indexer

Olá tabela a seguir explica elementos e atributos do XML de configuração de saudação.

|Nome|Exigência|Descrição|
|---|---|---|
|Entrada|verdadeiro|Arquivos de ativo que você deseja tooindex.<br/>Indexador de mídia do Azure oferece suporte a saudação formatos de arquivo de mídia a seguir: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>Você pode especificar o nome do arquivo hello (s) em Olá **nome** ou **lista** atributo de saudação **entrada** elemento (conforme mostrado abaixo). Se você não especificar qual tooindex de arquivo ativo, o arquivo primário Olá é escolhido. Se nenhum arquivo de ativo primário for definido, o primeiro arquivo hello ativo de entrada hello é indexado.<br/><br/>tooexplicitly especificar nome de arquivo de ativo hello, faça:<br/>```<input name="TestFile.wmv" />```<br/><br/>Você também pode indexar vários arquivos de ativo de uma vez (backup de arquivos de too10). toodo isso:<br/>– Crie um arquivo de texto (arquivo de manifesto) e dê a ele uma extensão .lst.<br/>-Adicione uma lista de todos os nomes de arquivo de ativo de saudação em seu arquivo de manifesto toothis ativo de entrada.<br/>-Adicione (carregue) ativo de toohello de arquivo de manifesto.<br/>-Especifique o nome de Olá Olá do arquivo de manifesto no atributo de lista de entrada hello.<br/>```<input list="input.lst">```<br/><br/>**Observação:** se você adicionar mais de 10 arquivos toohello o arquivo de manifesto, o trabalho de indexação Olá falhará com o código de erro Olá 2006.|
|metadata|false|Os metadados para Olá especificados arquivos de ativo.<br/>```<metadata key="..." value="..." />```<br/><br/>Você pode fornecer valores para chaves predefinidas. <br/><br/>Atualmente, há suporte para Olá chaves a seguir:<br/><br/>**título** e **descrição** -usadas a precisão do reconhecimento tooupdate Olá idioma modelo tooimprove fala.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**nome de usuário** e **senha** – usados para autenticação ao baixar arquivos da Internet via http ou https.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Olá nome de usuário e valores de senha se aplicam a URLs de mídia tooall no manifesto de entrada hello.|
|recursos<br/><br/>Adicionado na versão 1.2. Atualmente, o recurso Olá só tem suportada é o reconhecimento de fala ("ASR").|false|recurso de reconhecimento de fala Olá tem Olá chaves de configurações a seguir:<br/><br/>Linguagem:<br/>-Olá toobe de linguagem natural reconhecido no arquivo de multimídia hello.<br/>– Inglês, espanhol<br/><br/>CaptionFormats:<br/>-uma lista separada por ponto e vírgula de saudação desejado formatos de legenda de saída (se houver)<br/>- ttml;sami;webvtt<br/><br/><br/>GenerateAIB:<br/>-Um sinalizador booliano que especifica se um arquivo AIB é necessário (para uso com o SQL Server e hello IFilter do indexador cliente). Para obter mais informações, consulte Como usar arquivos AIB com o Azure Media Indexer e o SQL Server.<br/>- True; False<br/><br/>GenerateKeywords:<br/>– Um sinalizador booliano que especifica se um arquivo XML de palavras-chave é necessário ou não.<br/>- True; False.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Exemplo de XML de configuração do Azure Media Indexer

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Próximas etapas

Consulte [Como indexar arquivos de mídia com o Azure Media Indexer](media-services-index-content.md).

