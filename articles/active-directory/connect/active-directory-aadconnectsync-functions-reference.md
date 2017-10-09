---
title: "Sincronização do Azure AD Connect: referência de funções | Microsoft Docs"
description: "Referência de expressões de provisionamento declarativo na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD Connect Sync: referência de funções
No Azure AD Connect, funções são toomanipulate usado um valor de atributo durante a sincronização.  
Olá sintaxe de funções de saudação é expressa usando Olá formato a seguir:  
`<output type> FunctionName(<input type> <position name>, ..)`

Se uma função está sobrecarregada e aceita diversas sintaxes, todas as sintaxes válidas são listadas.  
Olá funções são fortemente tipadas e verificam que tipo de saudação passado no tipo de Olá documentado de correspondências.  
Se o tipo de saudação não corresponder, um erro será lançado.

Olá tipos são expressos com hello sintaxe a seguir:

* **bin** - binário
* **bool** - booliano
* **dt** - data/hora UTC
* **enum** - enumeração das constantes conhecidas
* **EXP** – expressão, que é esperado tooevaluate tooa booliano
* **mvbin** - Binário de Valores Múltiplos
* **mvstr** - Cadeia de Caracteres de Valores Múltiplos
* **mvstr** - Referência de Valores Múltiplos
* **num** - numérico
* **ref** – Referência
* **str** – Cadeia de Caracteres
* **var** - uma variante de (quase) qualquer outro tipo
* **void** - não retorna um valor

Olá funções com tipos de saudação **mvbin**, **mvstr**, e **mvref** funciona somente em atributos com valores múltiplos. As funções com **bin**, **str** e **ref** funcionam nos atributos de valor único e valores múltiplos.

## <a name="functions-reference"></a>Referência de funções
| Lista de funções |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certificate** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[ CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Conversão** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Data / hora** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Diretório** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Avaliação** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Matemática** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **De valores múltiplos** | | | | |
| [Contém:](#contains) |[Contagem](#count) |[Item](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[Divisão](#split) | | |
| **Fluxo do Programa** | | | | |
| [Erro](#error) |[IIF](#iif) |[Seleção](#select) |[Switch](#switch) | |
| [Onde](#where) |[With](#with) | | | |
| **Texto** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Substitua](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Descrição:**  
Olá função BitAnd define bits específicos em um valor.

**Sintaxe:**  
`num BitAnd(num value1, num value2)`

* value1, value2: os valores numéricos que devem ser agrupados com AND

**Comentários:**  
Esta função converte ambos os representação binária de toohello parâmetros e define um bit:

* 0 - se uma ou ambas Olá bits correspondentes em *máscara* e *sinalizador* são 0
* 1 - se dois bits correspondentes Olá são 1.

Em outras palavras, ele retorna 0 em todos os casos, exceto quando o bits correspondentes de saudação de ambos os parâmetros são 1.

**Exemplo:**  
`BitAnd(&HF, &HF7)`  
Retorna 7 porque hexadecimal "F" e "F7" avaliam o valor de toothis.

- - -
### <a name="bitor"></a>BitOr
**Descrição:**  
Olá função BitOr define bits específicos em um valor.

**Sintaxe:**  
`num BitOr(num value1, num value2)`

* value1, value2: valores numéricos que devem ser agrupados com OR

**Comentários:**  
Esta função converte ambos os representação binária de toohello parâmetros e define um bit too1 se um ou os dois bits correspondentes de saudação da máscara e o sinalizador são 1 e too0 se os dois bits correspondentes Olá são 0. Em outras palavras, ele retornará 1 em todos os casos, exceto onde os bits correspondentes de saudação de ambos os parâmetros são 0.

- - -
### <a name="cbool"></a>CBool
**Descrição:**  
Olá Função CBool retorna que um valor booleano com base na expressão Olá avaliada

**Sintaxe:**  
`bool CBool(exp Expression)`

**Comentários:**  
Se Olá avalia tooa de valor diferente de zero, então o CBool retorna True, caso contrário retornará False.

**Exemplo:**  
`CBool([attrib1] = [attrib2])`  

Retorna True se ambos os atributos têm Olá mesmo valor.

- - -
### <a name="cdate"></a>CDate
**Descrição:**  
Olá função CDate retorna um DateTime UTC de uma cadeia de caracteres. DateTime não é um tipo de atributo nativo no Sync, mas é usado por algumas funções.

**Sintaxe:**  
`dt CDate(str value)`

* Value: uma cadeia de caracteres com uma data, hora e opcionalmente um fuso horário

**Comentários:**  
Olá retornou uma cadeia de caracteres é sempre UTC.

**Exemplo:**  
`CDate([employeeStartTime])`  
Retorna um DateTime com base na hora de início do funcionário Olá

`CDate("2013-01-10 4:00 PM -8")`  
Retorna um DateTime que representa "11/01/2013 12:00"








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Descrição:**  
Retorna Olá valores de Oid de todas as extensões críticas de saudação de um objeto de certificado.

**Sintaxe:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certformat"></a>CertFormat
**Descrição:**  
Retorna Olá nome do formato de saudação do certificado x. 509v3.

**Sintaxe:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Descrição:**  
Retorna a saudação alias associada um certificado.

**Sintaxe:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certhashstring"></a>CertHashString
**Descrição:**  
Retorna Olá valor de hash SHA1 para certificado de x. 509v3 hello como uma cadeia de caracteres hexadecimal.

**Sintaxe:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certissuer"></a>CertIssuer
**Descrição:**  
Retorna Olá nome da autoridade de certificação de saudação que emitiu o certificado x. 509v3 de saudação.

**Sintaxe:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Descrição:**  
Retorna Olá nome diferenciado do emissor do certificado hello.

**Sintaxe:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Descrição:**  
Retorna Olá Oid de emissor do certificado hello.

**Sintaxe:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Descrição:**  
Retorna informações de algoritmo de chave de saudação do certificado x. 509v3 como uma cadeia de caracteres.

**Sintaxe:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Descrição:**  
Retorna os parâmetros de algoritmo de chave de saudação do certificado x. 509v3 de saudação como uma cadeia de caracteres hexadecimal.

**Sintaxe:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Descrição:**  
Retorna emissor e assunto Olá nomes de um certificado.

**Sintaxe:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.
*   X509NameType: Olá valor X509NameType assunto hello.
*   includesIssuerName: nome do emissor Olá tooinclude true; Caso contrário, false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Descrição:**  
Retorna a data de saudação na hora local depois que um certificado não é válido.

**Sintaxe:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Descrição:**  
Retorna a data de saudação na hora local no qual o certificado é validado.

**Sintaxe:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Descrição:**  
Retorna Olá Oid de chave pública Olá certificado x. 509v3 de saudação.

**Sintaxe:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Descrição:**  
Retorna Olá Oid de parâmetros de chave pública Olá para o certificado x. 509v3 de saudação.

**Sintaxe:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Descrição:**  
Retorna o número de série de saudação do certificado x. 509v3 de saudação.

**Sintaxe:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Descrição:**  
Olá retorna Oid do algoritmo Olá usado toocreate assinatura de saudação de um certificado.

**Sintaxe:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certsubject"></a>CertSubject
**Descrição:**  
Obtém Olá nome diferenciado do assunto de um certificado.

**Sintaxe:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Descrição:**  
Retorna Olá nome diferenciado do assunto de um certificado.

**Sintaxe:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Descrição:**  
Retorna Olá Oid do nome da entidade de saudação de um certificado.

**Sintaxe:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certthumbprint"></a>CertThumbprint
**Descrição:**  
Retorna Olá impressão digital de um certificado.

**Sintaxe:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="certversion"></a>CertVersion
**Descrição:**  
Retorna Olá x. 509 versão de formato de um certificado.

**Sintaxe:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.

- - -
### <a name="cguid"></a>CGuid
**Descrição:**  
Olá função CGuid converte a representação de cadeia de caracteres de saudação de uma representação binária do GUID tooits.

**Sintaxe:**  
`bin CGuid(str GUID)`

* Uma cadeia de caracteres formatada nesse padrão: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contém:
**Descrição:**  
função do Hello Contains localiza uma cadeia de caracteres dentro de um atributo com vários valores

**Sintaxe:**  
`num Contains (mvstring attribute, str search)` - diferencia letras maiúsculas de minúsculas  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` - diferencia letras maiúsculas de minúsculas

* atributo: Olá toosearch de atributo com vários valores.
* pesquisa: toofind no atributo de saudação de cadeia de caracteres.
* Casetype: CaseInsensitive ou CaseSensitive.

Retorna o índice no atributo de múltiplos Olá onde a cadeia de caracteres de saudação foi encontrada. Se a cadeia de caracteres de saudação não for encontrada, será retornado 0.

**Comentários:**  
Para atributos com vários valores de cadeia de caracteres, pesquisa Olá localiza subcadeias de caracteres em valores hello.  
Para atributos de referência, hello cadeia de caracteres pesquisada deve corresponder exatamente ao Olá valor toobe considerado uma correspondência.

**Exemplo:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Se o atributo proxyAddresses de saudação tem um endereço de email primário (indicado por letras maiusculas "SMTP:"), em seguida, retornar o atributo proxyAddress de saudação, caso contrário, retornará um erro.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Descrição:**  
Olá ConvertFromBase64 função converte Olá especificado codificado na base64 valor tooa cadeia de caracteres regulares.

**Sintaxe:**  
`str ConvertFromBase64(str source)` - adota Unicode para codificação  
`str ConvertFromBase64(str source, enum Encoding)`

* source: cadeia de caracteres codificada em Base64  
* Codificação: Unicode, ASCII, UTF8

**Exemplo**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Ambos os exemplos retornam "*Hello world!*"

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Descrição:**  
Olá ConvertFromUTF8Hex função converte Olá especificado a cadeia de caracteres hexadecimal UTF8 codificado valor tooa.

**Sintaxe:**  
`str ConvertFromUTF8Hex(str source)`

* source: cadeia de caracteres codificada em UTF8 de 2 bytes

**Comentários:**  
Olá diferença entre esta função e ConvertFromBase64([],UTF8) que resultam de saudação é amigável para o atributo DN de saudação.  
Esse formato é usado pelo Active Directory do Azure como DN.

**Exemplo:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
retorna "*Hello world!*"

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Descrição:**  
Olá função ConvertToBase64 converte uma cadeia de caracteres de base64 Unicode de tooa de cadeia de caracteres.  
Converte o valor de saudação de uma matriz de representação de cadeia de caracteres equivalente de tooits inteiros que é codificada com dígitos de base 64.

**Sintaxe:**  
`str ConvertToBase64(str source)`

**Exemplo:**  
`ConvertToBase64("Hello world!")`  
retorna "SABlAGwAbABvACAAdwBvAHIAbABkACEA"

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Descrição:**  
Olá função ConvertToUTF8Hex converte uma cadeia de caracteres de tooa valor hexadecimal UTF8 codificado.

**Sintaxe:**  
`str ConvertToUTF8Hex(str source)`

**Comentários:**  
saudação de formato de saída dessa função é usado pelo Active Directory do Azure como o formato do atributo DN.

**Exemplo:**  
`ConvertToUTF8Hex("Hello world!")`  
retorna 48656C6C6F20776F726C6421

- - -
### <a name="count"></a>Contagem
**Descrição:**  
Olá função Count retorna o número de saudação de elementos em um atributo com valores múltiplos

**Sintaxe:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Descrição:**  
Olá função CNum usa uma cadeia de caracteres e retorna um tipo de dados numérico.

**Sintaxe:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Descrição:**  
Converte um atributo de cadeia de caracteres de referência tooa

**Sintaxe:**  
`ref CRef(str value)`

**Exemplo:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Descrição:**  
Olá função CStr converte o tipo de dados de cadeia de caracteres tooa.

**Sintaxe:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* valor: pode ser um valor numérico, o atributo de referência ou booliano.

**Exemplo:**  
`CStr([dn])`  
poderia retornar "cn=Joe,dc=contoso,dc=com"

- - -
### <a name="dateadd"></a>DateAdd
**Descrição:**  
Retorna uma data que contém um toowhich data que um intervalo de tempo especificado foi adicionado.

**Sintaxe:**  
`dt DateAdd(str interval, num value, dt date)`

* intervalo: expressão que é o intervalo de tempo que deseja tooadd de saudação de cadeia de caracteres. cadeia de caracteres de saudação deve ter uma saudação valores a seguir:
  * aaaa Ano
  * q - Trimestre
  * m - Mês
  * y - Dia do ano
  * d - Dia
  * w - Dia da semana
  * ww - Semana
  * h - Hora
  * m - Minuto
  * s - Segundo
* valor: Olá o número de unidades que você deseja tooadd. Pode ser positivo (tooget datas em Olá futuro) ou negativo (tooget datas em Olá anterior).
* Data: DateTime representando data toowhich Olá intervalo é adicionado.

**Exemplo:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
adiciona três meses e retorna um DateTime que representa "01/04/2001".

- - -
### <a name="datefromnum"></a>DateFromNum
**Descrição:**  
Olá função DateFromNum converte um valor em tooa de formato de data do AD tipo DateTime.

**Sintaxe:**  
`dt DateFromNum(num value)`

**Exemplo:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
retorna um DateTime que representa 01/01/2012 23:00:00

- - -
### <a name="dncomponent"></a>DNComponent
**Descrição:**  
Olá função DNComponent retorna o valor de saudação de um componente DN especificado vindo da esquerda.

**Sintaxe:**  
`str DNComponent(ref dn, num ComponentNumber)`

* DN: Olá toointerpret de atributo de referência
* ComponentNumber: componente Olá Olá DN tooreturn

**Exemplo:**  
`DNComponent([dn],1)`  
se dn é “cn=Joe,ou=…,” ele retorna Joe

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Descrição:**  
Olá função DNComponentRev retorna o valor de saudação de um componente DN especificado vindo da direita (fim Olá).

**Sintaxe:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* DN: Olá toointerpret de atributo de referência
* ComponentNumber - componente Olá Olá DN tooreturn
* Opções: DC – ignorar todos os componentes com “dc=”

**Exemplo:**  
Se dn for "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" então  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
ambos retornam US.

- - -
### <a name="error"></a>Erro
**Descrição:**  
Olá função Error é usada tooreturn um erro personalizado.

**Sintaxe:**  
`void Error(str ErrorMessage)`

**Exemplo:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Se Olá atributo accountName não estiver presente, gera um erro no objeto de saudação.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Descrição:**  
Olá função EscapeDNComponent usa um componente de um DN e foge de forma que ele pode ser representado no LDAP.

**Sintaxe:**  
`str EscapeDNComponent(str value)`

**Exemplo:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Verifica se o objeto de saudação pode ser criado em um diretório LDAP, mesmo se o atributo de displayName Olá tem caracteres que devem ser substituídos no LDAP.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Descrição:**  
função FormatDateTime de saudação é usado tooformat uma cadeia de caracteres de tooa DateTime com um formato especificado

**Sintaxe:**  
`str FormatDateTime(dt value, str format)`

* valor: um valor no formato de data e hora Olá
* formato: uma cadeia de caracteres que representa a saudação formato tooconvert para.

**Comentários:**  
Olá os valores possíveis para o formato de saudação pode ser encontrado aqui: [definida pelo usuário (função Format) de formatos de data/hora](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Exemplo:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
resulta em "25/12/2007".

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
pode resultar em "20140905081453.0Z"

- - -
### <a name="guid"></a>GUID
**Descrição:**  
GUID da função Hello gera um novo GUID aleatório

**Sintaxe:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Descrição:**  
Olá função IIF retorna um de um conjunto de valores possíveis com base em uma condição especificada.

**Sintaxe:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* condição: qualquer valor ou expressão que pode ser avaliada tootrue ou false.
* ValorSeVerdadeiro: se a condição de saudação avalia tootrue, Olá retornou o valor.
* ValorSeFalso: se a condição de saudação avalia toofalse, Olá retornou o valor.

**Exemplo:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Se o usuário Olá for um estagiário, retorna Olá alias de um usuário com"t" adicionado toohello a partir dele, else retorna o alias do usuário hello como é.

- - -
### <a name="instr"></a>InStr
**Descrição:**  
Olá função InStr localiza a primeira ocorrência de saudação de uma subcadeia de caracteres em uma cadeia de caracteres

**Sintaxe:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* stringcheck: toobe pesquisado de cadeia de caracteres
* stringmatch: cadeia de caracteres toobe encontrado
* Iniciar: Iniciando posição toofind Olá substring
* compare: vbTextCompare ou vbBinaryCompare

**Comentários:**  
Posição de saudação retorna onde a subcadeia de caracteres hello foi encontrada ou 0 se não encontrado.

**Exemplo:**  
`InStr("hello quick brown fox","quick")`  
/ / Avalia too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Avalia too7

- - -
### <a name="instrrev"></a>InStrRev
**Descrição:**  
Olá função InStrRev localiza a última ocorrência de saudação de uma subcadeia de caracteres em uma cadeia de caracteres

**Sintaxe:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* stringcheck: toobe pesquisado de cadeia de caracteres
* stringmatch: cadeia de caracteres toobe encontrado
* Iniciar: Iniciando posição toofind Olá substring
* compare: vbTextCompare ou vbBinaryCompare

**Comentários:**  
Posição de saudação retorna onde a subcadeia de caracteres hello foi encontrada ou 0 se não encontrado.

**Exemplo:**  
`InStrRev("abbcdbbbef","bb")`  
retorna 7

- - -
### <a name="isbitset"></a>IsBitSet
**Descrição:**  
função Hello IsBitSet testa se um bit é definida ou não

**Sintaxe:**  
`bool IsBitSet(num value, num flag)`

* valor: um valor numérico que é evaluated. Flag: um valor numérico que tem Olá bit toobe avaliada

**Exemplo:**  
`IsBitSet(&HF,4)`  
Retorna True porque o bit "4" está definido no valor hexadecimal da saudação "F"

- - -
### <a name="isdate"></a>IsDate
**Descrição:**  
Se Olá expressão pode ser é avaliada como um tipo DateTime, Olá função IsDate avalia tooTrue.

**Sintaxe:**  
`bool IsDate(var Expression)`

**Comentários:**  
Usado toodetermine se CDate () pode ser bem-sucedida.

- - -
### <a name="iscert"></a>IsCert
**Descrição:**  
Retorna true se os dados brutos Olá podem ser serializados para o objeto de certificado X509Certificate2 .NET.

**Sintaxe:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: representação de matriz de bytes de um certificado X.509. matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.
- - -
### <a name="isempty"></a>IsEmpty
**Descrição:**  
Se o atributo hello está presente no hello CS ou MV mas é avaliada tooan cadeia de caracteres vazia, função do hello IsEmpty avalia tooTrue.

**Sintaxe:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Descrição:**  
Se a cadeia de caracteres hello pode ser convertido tooa GUID, função de isguid avalia Olá avaliada tootrue.

**Sintaxe:**  
`bool IsGuid(str GUID)`

**Comentários:**  
um GUID é definido como uma cadeia de caracteres seguindo um destes padrões: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

Usado toodetermine se cguid () pode ser bem-sucedida.

**Exemplo:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Se Olá StrAttribute tem um formato GUID, retorna uma representação binária, caso contrário, retornará um valor nulo.

- - -
### <a name="isnull"></a>IsNull
**Descrição:**  
Se a expressão Olá avalia tooNull, a função IsNull de saudação retorna true.

**Sintaxe:**  
`bool IsNull(var Expression)`

**Comentários:**  
Para um atributo, um valor nulo é expressa pela ausência de saudação do atributo hello.

**Exemplo:**  
`IsNull([displayName])`  
Retornará True se o atributo de saudação não está presente no hello CS ou MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Descrição:**  
Se a expressão de saudação é nulo ou uma cadeia de caracteres vazia, a função IsNullOrEmpty de saudação retorna true.

**Sintaxe:**  
`bool IsNullOrEmpty(var Expression)`

**Comentários:**  
Para um atributo, isso seria avaliado tooTrue se Olá atributo está ausente ou está presente, mas uma cadeia de caracteres vazia.  
Olá inverso dessa função é chamado IsPresent.

**Exemplo:**  
`IsNullOrEmpty([displayName])`  
Retornará True se o atributo de saudação não está presente ou é uma cadeia de caracteres vazia Olá CS ou MV.

- - -
### <a name="isnumeric"></a>IsNumeric
**Descrição:**  
Olá função IsNumeric retorna um valor booliano que indica se uma expressão pode ser avaliada como um tipo numérico.

**Sintaxe:**  
`bool IsNumeric(var Expression)`

**Comentários:**  
Usado toodetermine se cnum () pode ser uma expressão de saudação tooparse com êxito.

- - -
### <a name="isstring"></a>IsString
**Descrição:**  
Se a expressão Olá pode ser avaliada tooa tipo string, função IsString de saudação avalia tooTrue.

**Sintaxe:**  
`bool IsString(var expression)`

**Comentários:**  
Usado toodetermine se CStr () pode ser uma expressão de saudação tooparse com êxito.

- - -
### <a name="ispresent"></a>IsPresent
**Descrição:**  
Se Olá avalia tooa de cadeia de caracteres que não seja nulo e não está vazio, em seguida, Olá IsPresent função retorna true.

**Sintaxe:**  
`bool IsPresent(var expression)`

**Comentários:**  
Olá inverso dessa função é chamado IsNullOrEmpty.

**Exemplo:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Item
**Descrição:**  
Olá função Item Retorna um item de um cadeia de caracteres/atributo com vários valores.

**Sintaxe:**  
`var Item(mvstr attribute, num index)`

* attribute: atributo com valores múltiplos
* índice: índice tooan item da cadeia de caracteres com valores múltiplos hello.

**Comentários:**  
Olá função Item é útil junto com hello função Contains como função último hello retorna Olá índice tooan item no atributo de múltiplos hello.

Gera um erro se o índice está fora dos limites.

**Exemplo:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Retorna Olá endereço de email principal.

- - -
### <a name="itemornull"></a>ItemOrNull
**Descrição:**  
Olá função ItemOrNull retorna um item de um cadeia de caracteres/atributo com vários valores.

**Sintaxe:**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute: atributo com valores múltiplos
* índice: índice tooan item da cadeia de caracteres com valores múltiplos hello.

**Comentários:**  
Olá função ItemOrNull é útil junto com hello função Contains, como função último hello retorna Olá índice tooan item no atributo de múltiplos hello.

Se o índice estiver fora dos limites, retornará um valor Null.

- - -
### <a name="join"></a>Join
**Descrição:**  
função Hello usa uma cadeia de caracteres com valores múltiplos e retorna uma cadeia de caracteres de valor único com o separador especificado inserido entre cada item.

**Sintaxe:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* atributo: atributo com valores múltiplos contendo cadeias de caracteres toobe associado.
* delimitador: qualquer cadeia de caracteres, tooseparate usado Olá subcadeias de caracteres em Olá retornou uma cadeia. Se omitido, Olá caractere de espaço ("") é usado. Se o delimitador é uma cadeia de caracteres de comprimento zero ("") ou nada, todos os itens na lista de saudação são concatenados sem delimitadores.

**Comentários**  
Há uma paridade entre hello associação e funções de divisão. Olá função Join pega uma matriz de cadeias de caracteres e associa usando uma cadeia de caracteres delimitadora, tooreturn uma única cadeia de caracteres. Olá função Split usa uma cadeia de caracteres e separa no delimitador hello, tooreturn uma matriz de cadeias de caracteres. No entanto, uma diferença importante é que a Join pode concatenar cadeias de caracteres com qualquer cadeia de caracteres delimitadora, enquanto Split só pode separar cadeias de caracteres usando um único caractere delimitador.

**Exemplo:**  
`Join([proxyAddresses],",")`  
Poderia retornar: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**Descrição:**  
Olá Função LCase converte todos os caracteres no caso de toolower cadeia de caracteres.

**Sintaxe:**  
`str LCase(str value)`

**Exemplo:**  
`LCase("TeSt")`  
retorna "test".

- - -
### <a name="left"></a>Left
**Descrição:**  
função Left Olá retorna um número especificado de caracteres da esquerda de saudação de uma cadeia de caracteres.

**Sintaxe:**  
`str Left(str string, num NumChars)`

* cadeia de caracteres: Olá tooreturn caracteres de
* NumChars: um número que identifica Olá número de caracteres tooreturn desde o início de saudação (à esquerda) da cadeia de caracteres

**Comentários:**  
Uma cadeia de caracteres que contém a saudação primeiro os caracteres numChars na cadeia de caracteres:

* Se numChars = 0, retorne a cadeia de caracteres vazia.
* Se numChars < 0, retorne a cadeia de caracteres de entrada.
* Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.

Se a cadeia de caracteres contém caracteres menores do que o número de saudação especificado em numChars, uma toostring idênticos de cadeia de caracteres (isto é, que contém todos os caracteres no parâmetro 1) será retornado.

**Exemplo:**  
`Left("John Doe", 3)`  
retorna "Joh".

- - -
### <a name="len"></a>Len
**Descrição:**  
Olá função Len retorna o número de caracteres em uma cadeia de caracteres.

**Sintaxe:**  
`num Len(str value)`

**Exemplo:**  
`Len("John Doe")`  
retorna 8

- - -
### <a name="ltrim"></a>LTrim
**Descrição:**  
Olá função LTrim remove espaços em branco à esquerda de uma cadeia de caracteres.

**Sintaxe:**  
`str LTrim(str value)`

**Exemplo:**  
`LTrim(" Test ")`  
retorna "Test"

- - -
### <a name="mid"></a>Mid
**Descrição:**  
Olá Mid função retorna um número especificado de caracteres de uma posição especificada em uma cadeia de caracteres.

**Sintaxe:**  
`str Mid(str string, num start, num NumChars)`

* cadeia de caracteres: Olá tooreturn caracteres de
* Iniciar: um número que identifica a saudação em caracteres de tooreturn de cadeia de caracteres do início
* NumChars: um número que identifica Olá número de caracteres tooreturn da posição na cadeia de caracteres

**Comentários:**  
retorna os caracteres numChars começando na posição inicial da cadeia de caracteres.  
Uma cadeia de caracteres contendo caracteres numChars desde a posição inicial na cadeia de caracteres:

* Se numChars = 0, retorne a cadeia de caracteres vazia.
* Se numChars < 0, retorne a cadeia de caracteres de entrada.
* Se Iniciar > Olá comprimento da cadeia de caracteres, retorna a cadeia de caracteres de entrada.
* Se start <= 0, retorne a cadeia de caracteres de entrada.
* Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.

Se não houver nenhum caractere numChar restante na cadeia de caracteres a partir da posição inicial, o máximo possível de caracteres será retornado.

**Exemplo:**  
`Mid("John Doe", 3, 5)`  
retorna "hn Do".

`Mid("John Doe", 6, 999)`  
retorna "Doe"

- - -
### <a name="now"></a>Now
**Descrição:**  
Olá agora função retorna um DateTime especifico Olá atual data e hora, tooyour data do sistema do computador e a hora de acordo com.

**Sintaxe:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Descrição:**  
Olá função NumFromDate retorna uma data no formato de data do AD.

**Sintaxe:**  
`num NumFromDate(dt value)`

**Exemplo:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
retorna 129699324000000000

- - -
### <a name="padleft"></a>PadLeft
**Descrição:**  
Olá PadLeft preenche à esquerda de função um tooa de cadeia de caracteres especificada comprimento usando um caractere de preenchimento fornecido.

**Sintaxe:**  
`str PadLeft(str string, num length, str padCharacter)`

* cadeia de caracteres: Olá toopad de cadeia de caracteres.
* comprimento: um inteiro que representa a saudação desejado comprimento da cadeia de caracteres.
* padCharacter: uma cadeia de caracteres que consiste em toouse um único caractere como caractere de preenchimento de saudação

**Comentários:**

* Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, padCharacter é repetidamente anexado toohello início (à esquerda) da cadeia de caracteres até que tenha uma toolength de comprimento igual.
* PadCharacter pode ser um caractere de espaço, mas não pode ser um valor nulo.
* Se o comprimento de Olá de cadeia de caracteres for maior que o comprimento de tooor igual, a cadeia de caracteres é retornada inalterada.
* Se a cadeia de caracteres tem um comprimento maior que ou igual toolength, será retornado um toostring idênticos de cadeia de caracteres.
* Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, uma nova cadeia de caracteres de saudação desejado comprimento é retornado que contém a cadeia de caracteres preenchida com um padCharacter.
* Se a cadeia de caracteres for nula, a função hello retorna uma cadeia de caracteres vazia.

**Exemplo:**  
`PadLeft("User", 10, "0")`  
retorna "000000User".

- - -
### <a name="padright"></a>PadRight
**Descrição:**  
Olá PadRight preenche à direita de função um tooa de cadeia de caracteres especificada comprimento usando um caractere de preenchimento fornecido.

**Sintaxe:**  
`str PadRight(str string, num length, str padCharacter)`

* cadeia de caracteres: Olá toopad de cadeia de caracteres.
* comprimento: um inteiro que representa a saudação desejado comprimento da cadeia de caracteres.
* padCharacter: uma cadeia de caracteres que consiste em toouse um único caractere como caractere de preenchimento de saudação

**Comentários:**

* Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, padCharacter é repetidamente anexado toohello final (à direita) da cadeia de caracteres até que tenha uma toolength de comprimento igual.
* PadCharacter pode ser um caractere de espaço, mas não pode ser um valor nulo.
* Se o comprimento de Olá de cadeia de caracteres for maior que o comprimento de tooor igual, a cadeia de caracteres é retornada inalterada.
* Se a cadeia de caracteres tem um comprimento maior que ou igual toolength, será retornado um toostring idênticos de cadeia de caracteres.
* Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, uma nova cadeia de caracteres de saudação desejado comprimento é retornado que contém a cadeia de caracteres preenchida com um padCharacter.
* Se a cadeia de caracteres for nula, a função hello retorna uma cadeia de caracteres vazia.

**Exemplo:**  
`PadRight("User", 10, "0")`  
retorna "User000000".

- - -
### <a name="pcase"></a>PCase
**Descrição:**  
Olá função PCase converte Olá primeiro caractere de cada palavra delimitada por espaço em um caso de tooupper de cadeia de caracteres, e todos os outros caracteres são convertidos toolower caso.

**Sintaxe:**  
`String PCase(string)`

**Comentários:**

* Essa função no momento não oferece tooconvert de maiusculas e minúsculas adequadas uma palavra que está totalmente em letras maiusculas, como um acrônimo.

**Exemplo:**  
`PCase("TEsT")`  
retorna "test".

`PCase(LCase("TEST"))`  
Retorna "Test"

- - -
### <a name="randomnum"></a>RandomNum
**Descrição:**  
Olá função RandomNum retorna um número aleatório entre um intervalo especificado.

**Sintaxe:**  
`num RandomNum(num start, num end)`

* Iniciar: um número identificação Olá limite inferior de saudação valor aleatório toogenerate
* fim: um número identificação Olá limite superior de saudação valor aleatório toogenerate

**Exemplo:**  
`Random(100,999)`  
pode retornar 734.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Descrição:**  
Olá função RemoveDuplicates usa uma cadeia de caracteres com valores múltiplos e certificar-se de que cada valor é exclusivo.

**Sintaxe:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Exemplo:**  
`RemoveDuplicates([proxyAddresses])`  
retorna um atributo proxyAddress corrigido no qual todos os valores duplicados foram removidos.

- - -
### <a name="replace"></a>Substitua
**Descrição:**  
Olá função Replace substitui todas as ocorrências de uma cadeia de caracteres de tooanother de cadeia de caracteres.

**Sintaxe:**  
`str Replace(str string, str OldValue, str NewValue)`

* cadeia de caracteres: uma cadeia de caracteres tooreplace valores em.
* OldValue: Olá toosearch de cadeia de caracteres para e tooreplace.
* NewValue: Olá tooreplace de cadeia de caracteres para.

**Comentários:**  
função Hello reconhece Olá monikers especiais a seguir:

* \n - Nova linha
* \r - Retorno de carro
* \t - Guia

**Exemplo:**  
`Replace([address],"\r\n",", ")`  
Substitui CRLF com uma vírgula e um espaço e pode levar muito "One Microsoft maneira, Redmond, WA, EUA"

- - -
### <a name="replacechars"></a>ReplaceChars
**Descrição:**  
Olá função ReplaceChars substitui todas as ocorrências de caracteres encontradas na cadeia de caracteres ReplacePattern de saudação.

**Sintaxe:**  
`str ReplaceChars(str string, str ReplacePattern)`

* cadeia de caracteres: caracteres tooreplace uma cadeia de caracteres.
* ReplacePattern: uma cadeia de caracteres que contém um dicionário com caracteres tooreplace.

Olá formato é {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN} em que a fonte é Olá caractere toofind e destino Olá cadeia de caracteres tooreplace com.

**Comentários:**

* função Hello usa cada ocorrência de fontes definidas e substitui-los com os destinos de saudação.
* fonte de saudação deve estar exatamente um caractere (unicode).
* origem de saudação não pode ser vazio ou maior que o caractere (erro de análise).
* destino de saudação pode ter vários caracteres, por exemplo, OE, β: ss.
* Olá destino pode ser vazio, indicando que o caractere de saudação deve ser removida.
* origem de saudação diferencia maiusculas de minúsculas e deve ser uma correspondência exata.
* Olá, (vírgula) e: (dois-pontos) são caracteres reservados e não podem ser substituídos usando essa função.
* Espaços e outros caracteres em branco na cadeia de caracteres ReplacePattern de saudação é ignorado.

**Exemplo:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
retorna Raksmorgas

`ReplaceChars("O’Neil",%ReplaceString%)`  
Retorna "ONeil", o único tique de saudação é definido toobe removido.

- - -
### <a name="right"></a>Right
**Descrição:**  
função Right Olá retorna um número especificado de caracteres de saudação à direita (fim) de uma cadeia de caracteres.

**Sintaxe:**  
`str Right(str string, num NumChars)`

* cadeia de caracteres: Olá tooreturn caracteres de
* NumChars: um número que identifica Olá número de caracteres tooreturn de término hello (à direita) da cadeia de caracteres

**Comentários:**  
Os caracteres NumChars são retornados da última posição Olá de cadeia de caracteres.

Uma cadeia de caracteres que contém os últimos caracteres numChars Olá na cadeia de caracteres:

* Se numChars = 0, retorne a cadeia de caracteres vazia.
* Se numChars < 0, retorne a cadeia de caracteres de entrada.
* Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.

Se a cadeia de caracteres contiver menos caracteres que Olá número especificado no NumChars, uma toostring idênticos de cadeia de caracteres é retornado.

**Exemplo:**  
`Right("John Doe", 3)`  
retorna "Doe".

- - -
### <a name="rtrim"></a>RTrim
**Descrição:**  
Olá função RTrim remove espaços em branco à direita de uma cadeia de caracteres.

**Sintaxe:**  
`str RTrim(str value)`

**Exemplo:**  
`RTrim(" Test ")`  
retorna "Test".

- - -
### <a name="select"></a>Selecionar
**Descrição:**  
Processa todos os valores em um atributo de valores múltiplos (ou a saída de uma expressão) com base na função especificada.

**Sintaxe:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* item: representa um elemento no atributo de múltiplos Olá
* atributo: atributo de múltiplos Olá
* expression: uma expressão que retorna uma coleção de valores
* condição: qualquer função que pode processar um item no atributo Olá

**Exemplos:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Retorne todos os valores de Olá no otherPhone de atributo com vários valores hello depois hifens (-) foram removidos.

- - -
### <a name="split"></a>Divisão
**Descrição:**  
Olá função Split usa uma cadeia de caracteres separada por um delimitador e facilita uma cadeia de caracteres com valores múltiplos.

**Sintaxe:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* valor: Olá a cadeia de caracteres com um tooseparate de caractere delimitador.
* delimitador: único toobe caractere usado como Olá delimitador.
* limite: o número máximo de valores que podem ser retornados.

**Exemplo:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Retorna uma cadeia de caracteres com valores múltiplos com 2 elementos úteis para o atributo proxyAddress de saudação.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Descrição:**  
Olá função StringFromGuid usa um GUID binário e converte-a cadeia de caracteres tooa

**Sintaxe:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Descrição:**  
Olá função StringFromSid converte uma matriz de bytes que contém uma cadeia de caracteres de tooa de identificador de segurança.

**Sintaxe:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**Descrição:**  
função de comutador Hello é tooreturn usado um único valor com base nas condições avaliadas.

**Sintaxe:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr: expressão Variant que você deseja tooevaluate.
* valor: toobe do valor retornado se a expressão correspondente Olá é True.

**Comentários:**  
Olá argumento da função Switch consiste em pares de expressões e valores. Olá expressões são avaliadas da esquerda tooright e valor Olá associado Olá primeira expressão tooevaluate tooTrue será retornado. Se partes da saudação não tiverem pares adequados, ocorrerá um erro de tempo de execução.

Por exemplo, se expr1 for True, o comutador retornará valor1. Se expr-1 for False, mas expr-2 for True, Switch retorna valor-2 e assim por diante.

Switch retorna um Nothing se:

* Nenhuma das expressões Olá forem True.
* primeira expressão True de saudação tem um valor correspondente que é Null.

Switch avalia todas as expressões, mesmo que retorne apenas uma delas. Por essa razão, você deve tomar cuidado com efeitos colaterais indesejáveis. Por exemplo, se a avaliação de saudação de qualquer expressão resulta em uma divisão por zero, ocorrerá um erro.

Valor também pode ser a função de erro hello, que retorna uma cadeia de caracteres personalizada.

**Exemplo:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Retorna Olá idioma falado em algumas cidades, caso contrário, retornará um erro.

- - -
### <a name="trim"></a>Trim
**Descrição:**  
função Trim Olá remove espaços à direita e branco de uma cadeia de caracteres.

**Sintaxe:**  
`str Trim(str value)`  

**Exemplo:**  
`Trim(" Test ")`  
retorna "test".

`Trim([proxyAddresses])`  
Remove espaços à direita e para cada valor no atributo proxyAddress de saudação.

- - -
### <a name="ucase"></a>UCase
**Descrição:**  
Olá função UCase converte todos os caracteres no caso de tooupper cadeia de caracteres.

**Sintaxe:**  
`str UCase(str string)`

**Exemplo:**  
`UCase("TeSt")`  
retorna "test".

- - -
### <a name="where"></a>Where

**Descrição:**  
Retorna um subconjunto de valores de um atributo de valores múltiplos (ou a saída de uma expressão) com base em uma condição específica.

**Sintaxe:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* item: representa um elemento no atributo de múltiplos Olá
* atributo: atributo de múltiplos Olá
* condição: qualquer expressão que pode ser avaliada tootrue ou false
* expression: uma expressão que retorna uma coleção de valores

**Exemplo:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Retorne valores de certificado Olá Olá userCertificate de atributo com vários valores que não estão expiradas.

- - -
### <a name="with"></a>With
**Descrição:**  
Olá com função fornece uma maneira toosimplify uma expressão complexa usando uma variável toorepresent uma subexpressão que aparece uma ou mais vezes na expressão complexa hello.

**Sintaxe:**
`With(var variable, exp subExpression, exp complexExpression)`  
* variável: representa Olá subexpressão.
* subExpression: a subexpressão representada pela variável.
* complexExpression: uma expressão complexa.

**Exemplo:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
É funcionalmente equivalente à:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Que retorna apenas os valores de certificado não expirados no atributo de userCertificate hello.


- - -
### <a name="word"></a>Word
**Descrição:**  
Olá função Word retorna uma palavra contida em uma cadeia de caracteres, com base nos parâmetros que descrevem Olá delimitadores toouse e hello word número tooreturn.

**Sintaxe:**  
`str Word(str string, num WordNumber, str delimiters)`

* cadeia de caracteres: Olá tooreturn de cadeia de caracteres de uma palavra.
* WordNumber: um número que identifica qual número de palavras deve retornar.
* delimitadores: uma cadeia de caracteres que representa a saudação delimiter(s) que deve ser usado tooidentify palavras

**Comentários:**  
Cada cadeia de caracteres na cadeia de caracteres separados por Olá um Olá caracteres delimitadores são identificados como palavras:

* Se number < 1, retorna uma cadeia de caracteres vazia.
* Se a cadeia de caracteres for nula, retorna a cadeia de caracteres vazia.

Se a cadeia de caracteres for menor que o número de palavras ou a cadeia não contiver nenhuma palavra identificada por delimitadores, uma cadeia de caracteres vazia será retornada.

**Exemplo:**  
`Word("hello quick brown fox",3," ")`  
retorna "brown"

`Word("This,string!has&many separators",3,",!&#")`  
retornaria "has"

## <a name="additional-resources"></a>Recursos adicionais
* [Noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect Sync: personalizando opções de sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
