---
title: "Azure AD Connect: expressões de provisionamento declarativo | Microsoft Docs"
description: "Explica as expressões de provisionamento declarativo hello."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Sincronização do Azure AD Connect: noções básicas sobre expressões de provisionamento declarativo
A sincronização do Azure AD Connect criada com base em provisionamento declarativo foi introduzida pela primeira vez no Forefront Identity Manager 2010. Ele permite tooimplement código compilado de sua lógica de negócios de integração de identidade completa sem Olá necessidade toowrite.

Uma parte essencial do provisionamento declarativo é a linguagem de expressão Olá usada em fluxos de atributo. linguagem de saudação usada é um subconjunto do Microsoft® Visual Basic® for Applications (VBA). Essa linguagem é usada no Microsoft Office e os usuários com experiência em VBScript também a reconhecerão. Olá linguagem de expressão do provisionamento declarativo usa somente funções e não é uma linguagem estruturada. Não existem métodos nem instruções. Funções são aninhadas em vez disso, tooexpress o fluxo de programa.

Para obter mais detalhes, consulte [toohello Visual Basic para referência de linguagem de aplicativos para Office 2013 de boas-vindas](https://msdn.microsoft.com/library/gg264383.aspx).

atributos de saudação são fortemente tipados. Uma função aceita somente atributos do tipo correto de saudação. Ela também diferencia maiúsculas de minúsculas. Tanto nomes de função, quanto nomes de atributo devem ter a capitalização apropriada, ou um erro será gerado.

## <a name="language-definitions-and-identifiers"></a>Identificadores e definições de idioma
* As funções têm um nome seguido por argumentos entre parênteses: FunctionName(argumento 1, argumento N).
* Os atributos são identificados por colchetes, [NomeDoAtributo]
* Parâmetros são identificados por sinais de porcentagem: %NomeDoParâmetro%
* Constantes de cadeia de caracteres estão entre aspas: por exemplo, "Contoso" (Observação: deve-se usar aspas normais "", e não inglesas “”)
* Valores numéricos são expressos sem aspas e esperado toobe decimal. Valores hexadecimais são prefixados com &H. Por exemplo, 98052, &HFF
* Valores boolianos são expressos com constantes: True, False.
* Literais e constantes internas são expressos apenas com seu nome: NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>Funções
Provisionamento declarativo usa muitas funções tooenable Olá possibilidade tootransform valores do atributo. Essas funções podem ser aninhadas para que Olá resultado de uma função é passado na função tooanother.

`Function1(Function2(Function3()))`

lista completa de saudação de funções pode ser encontrada no hello [referência de função](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>parâmetros
Um parâmetro é definido por um Connector ou por um administrador usando o PowerShell. Parâmetros geralmente contêm valores diferentes do sistema toosystem, por exemplo, nome de saudação do usuário de saudação do domínio hello está localizado em. Esses parâmetros podem ser usados em fluxos de atributo.

Olá Active Directory Connector fornecido Olá parâmetros a seguir para regras de sincronização de entrada:

| Nome do Parâmetro | Comentário |
| --- | --- |
| Domain.Netbios |Formato de NetBIOS do domínio Olá sendo importado, por exemplo FABRIKAMSALES |
| Domain.FQDN |Formato FQDN do domínio Olá sendo importado, por exemplo sales.fabrikam.com |
| Domain.LDAP |Formato LDAP do domínio Olá sendo importado, por exemplo, DC = vendas, DC = fabrikam, DC = com |
| Forest.Netbios |Formato de NetBIOS de nome de floresta de saudação sendo importado, por exemplo FABRIKAMCORP |
| Forest.FQDN |Formato FQDN do nome de floresta de saudação sendo importado, por exemplo, fabrikam.com |
| Forest.LDAP |Formato LDAP do nome de floresta de saudação sendo importado, por exemplo, DC = fabrikam, DC = com |

sistema de saudação fornece Olá seguinte parâmetro, que é usado tooget Olá identificador de saudação conector em execução no momento:  
`Connector.ID`

Aqui está um exemplo que preenche o domínio do atributo de metaverso Olá com nome de netbios de saudação do domínio Olá onde Olá usuário está localizado:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Operadores
Olá operadores a seguir pode ser usado:

* **Comparação**: <, <=, <>, =, >, >=
* **Matemática**: +, -, \*, -
* **Cadeia de caracteres**: & (concatenado)
* **Lógica**: && (e), || (ou)
* **Ordem de avaliação**: ( )

Os operadores são avaliado tooright esquerdo e têm Olá mesma prioridade de avaliação. Ou seja, Olá \* (multiplicador) não é avaliado antes - (subtração). 2\*(5 + 3) não é mesmo Olá como 2\*5 + 3. Olá parênteses () são usados avaliação de saudação toochange pedido for deixado tooright ordem de avaliação não é apropriado.

## <a name="multi-valued-attributes"></a>Atributos de vários valores
funções Hello podem operar em atributos de valor único e valores múltiplos. Para atributos com valores múltiplos, função hello opera em todos os valores e se aplica a saudação mesma função tooevery valor.

Por exemplo:  
`Trim([proxyAddresses])`Faça um corte de cada valor no atributo proxyAddress de saudação.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Para cada valor com um @-sign, substitua o domínio Olá com @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Procure Olá endereço SIP e removê-lo de valores hello.

## <a name="next-steps"></a>Próximas etapas
* Leia mais sobre o modelo de configuração de saudação em [Noções básicas sobre o provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Veja declarativa como o provisionamento é usada fora da caixa na [Compreendendo a configuração padrão da saudação](active-directory-aadconnectsync-understanding-default-configuration.md).
* Veja como toomake um práticos alterados usando provisionamento declarativo em [como toomake toohello uma alteração de configuração padrão](active-directory-aadconnectsync-change-the-configuration.md).

**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

**Tópicos de referência**

* [Azure AD Connect Sync: referência de funções](active-directory-aadconnectsync-functions-reference.md)

