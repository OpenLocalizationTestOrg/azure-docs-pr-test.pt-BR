---
title: "aaaWriting expressões para mapeamentos de atributos no Active Directory do Azure | Microsoft Docs"
description: "Saiba como toouse expressão mapeamentos tootransform valores de atributo em um formato aceitável durante o provisionamento automatizado de objetos de aplicativo SaaS no Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Escrevendo expressões para mapeamentos de atributo no Active Directory do Azure
Quando você configura o aplicativo de SaaS tooa provisionamento, um dos tipos de saudação de mapeamentos de atributos que você pode especificar é um mapeamento de expressões. Para isso, você deve gravar uma expressão como script que permite que você tootransform os dados dos usuários em formatos mais aceitáveis para o aplicativo de SaaS hello.

## <a name="syntax-overview"></a>Visão geral da sintaxe
sintaxe de saudação para expressões para mapeamentos de atributos é Aplications do Visual Basic para funções Applications (VBA).

* expressão inteira Olá deve ser definida em termos de funções, que consistem em um nome seguido por argumentos entre parênteses: <br>
  *FunctionName(<<argument 1>>,<<argument N>>)*
* Você pode aninhar funções dentro umas das outras. Por exemplo: <br> *FunctionOne(FunctionTwo(<<argument1>>))*
* Você pode passar três tipos diferentes de argumentos em funções:
  
  1. Atributos, que devem ser colocados entre colchetes. Por exemplo: [attributeName]
  2. Constantes de cadeia de caracteres, que devem ser colocadas entre aspas duplas. Por exemplo: "Estados Unidos"
  3. Outras funções. Por exemplo: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))
* Para constantes de cadeia de caracteres, se você precisar de uma barra invertida (\) ou aspas (") na cadeia de caracteres hello, ela deverá ser substituída com o símbolo de barra invertida (\) hello. Por exemplo: "Nome da empresa: \"Contoso\""

## <a name="list-of-functions"></a>Lista de funções
[Acrescentar](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Substitua](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)

- - -
### <a name="append"></a>Acrescentar
**Função:**<br> Append(source, suffix)

**Descrição:**<br> Usa um valor de cadeia de caracteres de origem e acrescenta Olá sufixo toohello final.

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres |Geralmente o nome do atributo de saudação do objeto de origem Olá |
| **suffix** |Obrigatório |Cadeia de caracteres |cadeia de caracteres de saudação que você deseja tooappend toohello final do valor de origem hello. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Função:**<br> FormatDateTime(source, inputFormat, outputFormat)

**Descrição:**<br> obtém uma cadeia de caracteres de data de um formato e a converte em um formato diferente.

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres |Geralmente o nome do atributo de saudação do objeto de origem de saudação. |
| **inputFormat** |Obrigatório |Cadeia de caracteres |Formato esperado do valor de origem hello. Para conhecer os formatos com suporte, confira [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Obrigatório |Cadeia de caracteres |Formato da data de saída de hello. |

- - -
### <a name="join"></a>Ingressar
**Função:**<br> Join(separator, source1, source2, …)

**Descrição:**<br> JOIN () é tooAppend() semelhante, exceto que pode combinar vários **fonte** valores de cadeia de caracteres em uma única cadeia de caracteres, e cada valor será separado por um **separador** cadeia de caracteres.

Se um dos valores de saudação de origem é um atributo com vários valores, todos os valores de atributo será o valor de separador de saudação Unidos juntos, separados.

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **separator** |Obrigatório |Cadeia de caracteres |Cadeia de caracteres usada tooseparate valores de origem quando eles são concatenados em uma cadeia de caracteres. Pode ser "" se não for necessário nenhum separador. |
| **source1  … sourceN ** |Obrigatório, número de vezes variável |Cadeia de caracteres |Valores de cadeia de caracteres toobe unida. |

- - -
### <a name="mid"></a>Mid
**Função:**<br> Mid(source, start, length)

**Descrição:**<br> Retorna uma subcadeia de caracteres do valor de origem hello. Uma subcadeia de caracteres é uma cadeia de caracteres que contém apenas alguns dos caracteres de saudação de cadeia de caracteres de origem hello.

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres |Geralmente o nome do atributo de saudação. |
| **iniciar** |Obrigatório |inteiro |Índice em Olá **fonte** cadeia de caracteres onde a subcadeia de caracteres deve começar. Primeiro caractere na cadeia de caracteres hello terá o índice de 1, o segundo caractere de índice 2 e assim por diante. |
| **length** |Obrigatório |inteiro |Comprimento da subcadeia de caracteres de saudação. Se o comprimento terminar Olá fora **fonte** cadeia de caracteres, a função retornará a subcadeia de caracteres de **iniciar** índice até o final da **fonte** cadeia de caracteres. |

- - -
### <a name="not"></a>não
**Função:**<br> Not(source)

**Descrição:**<br> Inverte Olá valor booliano da saudação **fonte**. Se o valor de **source** for "*True*", retorna "*False*". Caso contrário, retorna "*True*".

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres booliana |Os valores de **source** esperados são "True" ou "False". |

- - -
### <a name="replace"></a>Substitua
**Função:**<br> ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**Descrição:**<br>
substitui valores dentro de uma cadeia de caracteres. Funciona de forma diferente dependendo parâmetros Olá fornecidos:

* Quando **oldValue** e **replacementValue** são fornecidos:
  
  * Substitui todas as ocorrências de oldValue na fonte de saudação com valor de substituição
* Quando **oldValue** e **template** são fornecidos:
  
  * Substitui todas as ocorrências de saudação **oldValue** em Olá **modelo** com hello **fonte** valor
* Quando **oldValueRegexPattern**, **oldValueRegexGroupName** e **replacementValue** são fornecidos:
  
  * Substitui todos os valores correspondentes oldValueRegexPattern na cadeia de caracteres de origem de saudação com valor de substituição
* Quando **oldValueRegexPattern**, **oldValueRegexGroupName** e **replacementPropertyName** são fornecidos:
  
  * Se **source** tiver um valor, **source** será retornado
  * Se **fonte** não tem nenhum valor, usa **oldValueRegexPattern** e **oldValueRegexGroupName** tooextract o valor de substituição da propriedade Olá com  **replacementPropertyName**. Valor de substituição é retornado como resultado de saudação

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres |Geralmente o nome do atributo de saudação do objeto de origem de saudação. |
| **oldValue** |Opcional |Cadeia de caracteres |Valor toobe substituído no **fonte** ou **modelo**. |
| **regexPattern** |Opcional |Cadeia de caracteres |Padrão regex para Olá valor toobe substituído no **fonte**. Ou, quando replacementPropertyName é usado, tooextract o valor da propriedade de substituição de padrões. |
| **regexGroupName** |Opcional |Cadeia de caracteres |Nome do grupo de saudação dentro de **regexPattern**. Somente quando replacementPropertyName for usado, extrairemos o valor desse grupo como replacementValue da propriedade de substituição. |
| **replacementValue** |Opcional |Cadeia de caracteres |Novo valor tooreplace antigo com. |
| **replacementAttributeName** |Opcional |Cadeia de caracteres |Nome da saudação atributo toobe usado para o valor de substituição, quando a origem não tem nenhum valor. |
| **template** |Opcional |Cadeia de caracteres |Quando **modelo** valor for fornecido, será procurado **oldValue** Olá modelo dentro e substituí-lo com o valor de origem. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Função:**<br> StripSpaces(source)

**Descrição:**<br> Remove todo o espaço ("") cadeia de caracteres de saudação da fonte.

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres |**origem** tooupdate de valor. |

- - -
### <a name="switch"></a>Switch
**Função:**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**Descrição:**<br> Quando o valor de **source** corresponde a um parâmetro **key**, retorna **value** para esse parâmetro **key**. Se o valor de **source** não corresponder a nenhum parâmetro key, **defaultValue** será retornado.  Os parâmetros **key** e **value** devem sempre ocorrer em pares. função Hello sempre espera um número par de parâmetros.

**Parâmetros:**<br> 

| Nome | Obrigatório/repetição | Tipo | Observações |
| --- | --- | --- | --- |
| **fonte** |Obrigatório |Cadeia de caracteres |**Origem** tooupdate de valor. |
| **defaultValue** |Opcional |Cadeia de caracteres |Toobe de valor padrão usado quando a origem não corresponde a nenhuma chave. Pode ser uma cadeia de caracteres vazia (""). |
| **chave** |Obrigatório |Cadeia de caracteres |**Chave** toocompare **fonte** valor com. |
| **valor** |Obrigatório |Cadeia de caracteres |Valor de substituição para Olá **fonte** chave Olá correspondente. |

## <a name="examples"></a>Exemplos
### <a name="strip-known-domain-name"></a>Retirar o nome de domínio conhecido
É necessário toostrip um nome de domínio conhecido do tooobtain de email do usuário um nome de usuário. <br>
Por exemplo, se o domínio de saudação for "contoso.com", você pode usar Olá expressão a seguir:

**Expressão:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Entrada/saída de exemplo:**  <br>

* **INPUT** (mail): "john.doe@contoso.com"
* **SAÍDA**: "davi.barros"

### <a name="append-constant-suffix-toouser-name"></a>Acrescentar sufixo constante toouser nome
Se você estiver usando uma área restrita do Salesforce, talvez seja necessário tooappend tooall um sufixo adicional seus nomes de usuário antes de sincronizá-los.

**Expressão:** <br>
`Append([userPrincipalName], ".test"))`

**Entrada/saída de exemplo:** <br>

* **INPUT**: (userPrincipalName): "John.Doe@contoso.com"
* **OUTPUT**:  "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Gerar o alias de usuário concatenando partes do nome e do sobrenome
É necessário toogenerate um alias do usuário realizando primeiro 3 letras do nome do usuário e 5 primeiras letras do sobrenome do usuário.

**Expressão:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Entrada/saída de exemplo:** <br>

* **ENTRADA** (givenName): "Davi"
* **ENTRADA** (sobrenome): "Barros"
* **SAÍDA**: "DaviBarros"

### <a name="output-date-as-a-string-in-a-certain-format"></a>Gerar data como uma cadeia de caracteres em um determinado formato
Deseja que o aplicativo de SaaS de tooa toosend datas em um determinado formato. <br>
Por exemplo, você deseja tooformat datas para ServiceNow.

**Expressão:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Entrada/saída de exemplo:**

* **ENTRADA** (extensionAttribute1): "20150123105347.1Z"
* **SAÍDA**:  "2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Substituir um valor com base em um conjunto predefinido de opções
Você precisa de fuso horário Olá toodefine do usuário de saudação com base no código de estado de saudação armazenado no AD do Azure. <br>
Se o código de estado de saudação não corresponde a qualquer uma das opções de saudação predefinida, use o valor padrão de "Austrália/Sydney".

**Expressão:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Entrada/saída de exemplo:**

* **ENTRADA** (estado): "QLD"
* **SAÍDA**: "Australia/Brisbane"

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos](active-directory-saas-app-provisioning.md)
* [Personalizando os mapeamentos de atributos para provisionamento de usuários](active-directory-saas-customizing-attribute-mappings.md)
* [Filtros de escopo para provisionamento de usuários](active-directory-saas-scoping-filters.md)
* [Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications](active-directory-scim-provisioning.md)
* [Notificações de provisionamento de conta](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS](active-directory-saas-tutorial-list.md)

