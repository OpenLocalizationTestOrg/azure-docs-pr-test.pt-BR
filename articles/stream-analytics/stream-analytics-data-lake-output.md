---
title: "aaaStream análise Data Lake repositório saída | Microsoft Docs"
description: "Configuração de autenticação e autorização de um Repositório Azure Data Lake em um trabalho do Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Saída do Repositório Data Lake do Stream Analytics
Trabalhos do Stream Analytics dão suporte a vários métodos de saída, sendo um deles um [Repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/). O Repositório Azure Data Lake é um repositório em hiper-escala corporativo para cargas de trabalho de análise de big data. Repositório data Lake permite toostore dados de qualquer velocidade de tamanho, tipo e inclusão para análise operacional e exploratória.

## <a name="authorize-a-data-lake-store-account"></a>Autorizar uma conta do Repositório Data Lake
1. Quando o repositório Data Lake é selecionado como uma saída de hello portal do Azure, você será solicitado tooauthorize uso do repositório existente do Data Lake ou toorequest acessar o repositório toohello Data Lake via Olá Portal clássico.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Se você já tiver acessar o repositório de Lake tooData, clique em 'Autorizar agora' e por um curto período uma página será exibida indicando "Redirecionando tooauthorization". página Olá automaticamente será fechado e você verá página Olá que lhe permitiria tooconfigure Olá repositório Data Lake saída.

Se você não estiver inscrito para repositório Data Lake, siga hello "Inscrever-se agora" link tooinitiate Olá solicitação ou siga Olá [obter instruções iniciadas](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Configurar propriedades de saída do repositório Data Lake Olá
Uma vez que a conta do repositório Data Lake Olá autenticado, você pode configurar propriedades de saudação para a saída do repositório Data Lake. tabela de saudação abaixo é a lista de saudação de nomes de propriedade e seu tooconfigure descrição que seu repositório Data Lake de saída.

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
<td>Conta do Repositório Data Lake</td>
<td>nome de Olá Olá da conta de armazenamento em que você está enviando a saída. Você verá uma lista de contas do repositório Data Lake Olá registrada no usuário tem acesso ao.</td>
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

## <a name="renew-data-lake-store-authorization"></a>Renovar autorização do Repositório Data Lake
Atualmente, há uma limitação de onde o token de autenticação Olá precisa toobe atualizada manualmente a cada 90 dias para todos os trabalhos com a saída do repositório Data Lake. Você também precisará toore-autenticar sua conta do repositório Data Lake se você alterou sua senha desde que o trabalho foi criado ou última autenticado. Um sintoma desse problema é nenhuma saída de trabalho e um erro nos Logs de operação Olá indicando a necessidade de autorização novamente.

tooresolve esse problema, interromper seu trabalho em execução e vá repositório tooyour Data Lake de saída. Clique o link de "Renovar autorização" Olá e por um curto período uma página será exibida indicando "Redirecionando tooauthorization...". página de saudação será fechada automaticamente e se for bem-sucedido, a indicação "Autorização foi renovada com êxito". Você precisa tooclick "Salvar" final Olá Olá página e pode continuar, reiniciar o trabalho de saudação perda de dados tooavoid hora da última interrupção.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

