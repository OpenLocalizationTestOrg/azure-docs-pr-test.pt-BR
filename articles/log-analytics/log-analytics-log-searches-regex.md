---
title: "pesquisas de log aaaRegular expressões na análise de Log do OMS | Microsoft Docs"
description: "Você pode usar a palavra-chave de RegEx Olá em análise de Log log pesquisas toohello filtro Olá resultados de expressão regular tooa de acordo com.  Este artigo fornece sintaxe de saudação para essas expressões com vários exemplos."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Usando expressões regulares toofilter pesquisa de log na análise de Log

[Pesquisas de log](log-analytics-log-searches.md) permitem que você tooextract informações do repositório de análise de Log de saudação.  [Expressões de filtro](log-analytics-search-reference.md#filter-expressions) permitem resultados de Olá toofilter da pesquisa de saudação de acordo com os critérios de toospecific.  Olá **RegEx** palavra-chave permite que você toospecify uma expressão regular para esse filtro.  

Este artigo fornece detalhes sobre a sintaxe de expressão regular Olá usado pela análise de Log.

> [!NOTE]
> Você só pode usar RegEx com campos pesquisáveis.  Para obter mais informações sobre campos de pesquisa, veja **tipos de campo** na [localizar os dados usando pesquisas de log na análise de Log](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>Palavra-chave RegEx

Olá Use Olá de toouse de sintaxe a seguir **RegEx** palavra-chave em uma pesquisa de log.  Você pode usar Olá outras seções nessa sintaxe do artigo toodetermine Olá Olá regular própria expressão.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Por exemplo, um alerta de tooreturn de expressão regular de toouse registra com um tipo de *aviso* ou *erro*, você usaria Olá pesquisa de log a seguir.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Correspondências parciais
Observe que a expressão regular Olá deve corresponder todo texto Olá propriedade hello.  Correspondências parciais não retornarão nenhum registro.  Por exemplo, se você estivesse tentando tooreturn registros de um computador denominado srv01.contoso.com, Olá pesquisa de log a seguir seria **não** retorna registros.

    Computer=RegEx("srv..")

Isso ocorre porque somente Olá primeira parte do nome de saudação corresponde à expressão regular hello.  Hello pesquisas de log dois seguintes retornaria registros neste computador porque eles correspondem a nome inteiro hello.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Caracteres
Especificar caracteres diferentes.

| Character | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| a | Uma ocorrência do caractere de saudação. | Computer=RegEx("srv01.contoso.com") | srv01.contoso.com |
| . | Qualquer caractere único. | Computer=RegEx("srv...contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| a? | Zero ou uma ocorrência do caractere de saudação. | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>srv01.contoso.com |
| a* | Zero ou mais ocorrências do caractere de saudação. | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Uma ou mais ocorrências do caractere de saudação. | Computer=RegEx("srv01+.contoso.com") | srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Corresponder qualquer caractere único entre colchetes Olá | Computer=RegEx("srv0[123].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [*a*-*z*] | Corresponde a um único caractere no intervalo de saudação.  Pode incluir vários intervalos. | Computer=RegEx("srv0[1-3].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Nenhum dos caracteres hello colchetes Olá | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^*a*-*z*] | Nenhum dos caracteres hello no intervalo de saudação. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Corresponde a um intervalo de caracteres numéricos. | Computer=RegEx("srv[01-03].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| @ | Qualquer cadeia de caracteres. | Computer=RegEx("srv@.contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Várias ocorrências do caractere
Especifique várias ocorrências de um determinado caractere.

| Character | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| a{n} |  *n*ocorrências do caractere de saudação. | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*ou mais ocorrências do caractere de saudação. | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*muito*m* ocorrências do caractere de saudação. | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Expressões lógicas
Selecione de diversos valores.

| Character | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| &#124; | OR Lógico.  Retornará o resultado se corresponder a qualquer expressão. | Type=Alert AlertSeverity=RegEx("Warning&#124;Error") | Aviso<br>Erro |
| & | AND Lógico.  Retornará o resultado se corresponder as duas expressões | EventData=regex("(Security.\*&.\*success.\*)") | Auditoria de segurança bem-sucedida |


## <a name="literals"></a>Literais
Converta caracteres especiais tooliteral caracteres.  Isso inclui os caracteres que fornecem funcionalidade tooregular expressões, como?-\*^\[\]{}\(\)+\|. &.

| Character | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| \\ | Converte um literal de tooa caractere especial. | Status_CF=\\[Error\\]@<br>Status_CF=Error\\-@ | [Erro] Arquivo não encontrado.<br>Erro-Arquivo não encontrado. |


## <a name="next-steps"></a>Próximas etapas

* Familiarize-se com [pesquisas de log](log-analytics-log-searches.md) tooview e analisar dados no repositório de análise de Log de saudação.
