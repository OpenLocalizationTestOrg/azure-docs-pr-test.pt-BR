---
title: "associação de grupo dinâmico com base em aaaAttribute no Active Directory do Azure | Microsoft Docs"
description: "Como toocreate avançados regras de associação de grupo dinâmico incluindo parâmetros e operadores de regra de expressão com suporte."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Criar regras baseadas em atributo para associação dinâmica de grupo no Azure Active Directory
No Azure Active Directory (AD do Azure), você pode criar regras avançadas tooenable complexa com base em atributo associações dinâmicas de grupos. Este artigo fornece detalhes sobre atributos hello e regras de associação dinâmica de toocreate de sintaxe para usuários ou dispositivos.

Quando os atributos de uma alteração de usuário ou dispositivo, o sistema Olá avaliará todas as regras de grupo dinâmico em um diretório toosee se alterar Olá dispararia qualquer grupo adiciona ou remove. Se um usuário ou dispositivo atender a uma regra em um grupo, ele será adicionado como membro desse grupo. Se eles não atendem mais regra hello, eles serão removidos.

> [!NOTE]
> - Você pode configurar uma regra de associação dinâmica em grupos de segurança ou em grupos do Office 365.
>
> - Este recurso requer uma licença Azure AD Premium P1 para cada grupo do usuário membro tooat adicionado pelo menos um dinâmico.
>
> - Você pode criar um grupo dinâmico para usuários ou dispositivos, mas não pode criar uma regra que contenha objetos de usuário e de dispositivo.

> - No momento da saudação não é possível toocreate um grupo de dispositivos com base em atributos do usuário de proprietário. Regras de associação de dispositivo podem apenas imediata atributos de referência de objetos no diretório de saudação do dispositivo.

## <a name="toocreate-an-advanced-rule"></a>toocreate uma regra avançada
1. Entrar toohello [Centro de administração do AD do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global ou um administrador de conta de usuário.
2. Selecione **Usuários e grupos**.
3. Selecione **Todos os grupos**.

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. Em **Todos os grupos**, selecione **Novo grupo**.

   ![Adicione o novo grupo](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. Em Olá **grupo** folha, insira um nome e uma descrição para o novo grupo de saudação. Selecione um **tipo de associação** do **dinâmica do usuário** ou **dispositivo dinâmico**, dependendo se você deseja toocreate uma regra para usuários ou dispositivos e, em seguida, selecione **Consulta dinâmica adicionar**. Para atributos de saudação usados para regras de dispositivo, consulte [usando regras de toocreate de atributos para objetos de dispositivo](#using-attributes-to-create-rules-for-device-objects).

   ![Adicionar regra de associação dinâmica](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. Em Olá **regras de associação dinâmica** folha, digite sua regra em Olá **regra avançada de associação dinâmica de adicionar** caixa, pressione Enter e, em seguida, selecione **criar** na parte inferior de saudação do folha de saudação.
7. Selecione **criar** em Olá **grupo** grupo de saudação toocreate folha.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Construindo o corpo de saudação de uma regra avançada
Olá regra avançada que você pode criar para a associação dinâmica Olá de grupos é essencialmente uma expressão binária que consiste em três partes e resulta em um resultado true ou false. saudação de três partes é:

* Parâmetro da esquerda
* Operador binário
* Constante à direita

Uma regra avançada completa parece semelhante toothis: (leftParameter binaryOperator "RightConstant"), onde a saudação de abertura e fechamento parênteses é opcional para toda a expressão binária hello, aspas duplas são opcionais, necessário para a direita da saudação somente constante quando é cadeia de caracteres e sintaxe Olá para o parâmetro esquerdo Olá é User. Uma regra avançada pode consistir em mais de uma expressão binária separada pelos Olá- e, - ou e - operadores lógicos não.

Olá seguem exemplos de uma regra avançada construído corretamente:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Para lista completa de saudação de parâmetros com suporte e operadores de regra de expressão, consulte as seções a seguir. Para atributos de saudação usados para regras de dispositivo, consulte [usando regras de toocreate de atributos para objetos de dispositivo](#using-attributes-to-create-rules-for-device-objects).

tamanho total de saudação do corpo de saudação de sua regra avançada não pode exceder 2048 caracteres.

> [!NOTE]
> Operações de cadeia de caracteres e regex não diferenciam maiúsculas de minúsculas. Você também pode executar verificações de Null, usando $null como uma constante, por exemplo, user.department - eq $null.
> As cadeias de caracteres que contém aspas " devem ser ignoradas usando caracteres ', por exemplo, user.department -eq \`"Sales".

## <a name="supported-expression-rule-operators"></a>Operadores de regra de expressão com suporte
Olá tabela a seguir lista todos os operadores de regra de expressão Olá com suporte e seu toobe sintaxe usada no corpo da saudação do hello regra avançada:

| operador | Sintaxe |
| --- | --- |
| Não é igual a |-ne |
| É igual a |-eq |
| Não começa com |-notStartsWith |
| Começa com |-startsWith |
| Não contém |-notContains |
| Contém: |-contains |
| Não corresponde |-notMatch |
| Corresponde |-match |
| Nesse | -in |
| Não está em | -notIn |

## <a name="operator-precedence"></a>Precedência do operador

Todos os operadores são listados por precedência de toohigher inferior. Operadores na mesma linha têm a mesma precedência:
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Todos os operadores podem ser usados com ou sem o prefixo de hífen hello. Parênteses são necessários somente quando a precedência não atender às suas necessidades.
Por exemplo:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
é equivalente a:
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a>Usando Olá - em - notIn operadores e

Se você deseja toocompare Olá valor de um atributo de usuário em um número de valores diferentes que você pode usar hello - em - notIn operadores ou. Aqui está um exemplo usando Olá - no operador:
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Observe o uso de saudação do hello "[" e "]" no início de saudação e no final da lista de saudação de valores. Essa condição for avaliada tooTrue do valor de saudação do User. Department igual a um dos valores de saudação na lista de saudação.


## <a name="query-error-remediation"></a>Correção do erro de consulta
Olá, tabela a seguir lista os possíveis erros e como toocorrect-los, se ocorrerem

| Erro de análise de consulta | Erros de uso | Uso corrigido |
| --- | --- | --- |
| Erro: O atributo não tem suportado. |(user.invalidProperty -eq "Valor") |(user.department -eq "value") A propriedade <br/>Propriedade deve corresponder a uma das Olá [suporte para a lista de propriedades](#supported-properties). |
| Erro: Operador não é tem suportada no atributo. |(user.accountEnabled -contains true) |(user.accountEnabled -eq true) A propriedade <br/>é do tipo booliano. Use operadores Olá com suporte (-eq ou - ne) no tipo booliano da saudação acima da lista. |
| Erro: Erro de compilação de consulta. |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>Operador lógico deve corresponder a uma das propriedades Olá suportada listadas acima. (User-corresponder ". *@domain.ext") ou (User-corresponder "@domain.ext$") erro na expressão regular. |
| Erro: Expressão binária não está no formato correto. |user.department – eq ("Vendas") user.department - eq ("Vendas") user.department-eq ("Vendas") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>A consulta tem vários erros. Parênteses não no lugar certo. |
| Erro: Ocorreu um erro desconhecido durante a configuração de membros dinâmicos. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>A consulta tem vários erros. Parênteses não no lugar certo. |

## <a name="supported-properties"></a>Propriedades com suporte
Olá seguem todas as propriedades de usuário de saudação que você pode usar sua regra avançada:

### <a name="properties-of-type-boolean"></a>Propriedades de tipo booliano
Operadores permitidos

* -eq
* -ne

| Propriedades | Valores permitidos | Uso |
| --- | --- | --- |
| accountEnabled |verdadeiro, falso |user.accountEnabled -eq true |
| dirSyncEnabled |verdadeiro, falso |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>Propriedades do tipo cadeia de caracteres
Operadores permitidos

* -eq
* -ne
* -notStartsWith
* -startsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| Propriedades | Valores permitidos | Uso |
| --- | --- | --- |
| city |Qualquer valor de cadeia de caracteres ou $null |(user.city -eq "valor") |
| country |Qualquer valor de cadeia de caracteres ou $null |(user.country -eq "valor") |
| companyName | Qualquer valor de cadeia de caracteres ou $null | (user.companyName -eq "value") |
| department |Qualquer valor de cadeia de caracteres ou $null |(user.department -eq "value") A propriedade  |
| displayName |Um valor de cadeia de caracteres. |(user. DisplayName -eq "valor") |
| facsimileTelephoneNumber |Qualquer valor de cadeia de caracteres ou $null |user.facsimileTelephoneNumber -eq ("valor") |
| givenName |Qualquer valor de cadeia de caracteres ou $null |user.givenName -eq ("valor") |
| jobTitle |Qualquer valor de cadeia de caracteres ou $null |(user.jobTitle - eq "valor") |
| mail |Qualquer valor de cadeia de caracteres ou $null (endereço SMTP do usuário Olá) |(user.mail - eq "valor") |
| mailNickName |Qualquer valor de cadeia de caracteres (alias de email do usuário Olá) |(user.mailNickName - eq "valor") |
| Serviço Móvel |Qualquer valor de cadeia de caracteres ou $null |(user.mobile -eq "valor") |
| ID do objeto |GUID do objeto de usuário Olá |(user.objectId - eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | Identificador de segurança (SID) local para os usuários que foram sincronizados do toohello nuvem no local. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Qualquer valor de cadeia de caracteres ou $null |(user.physicalDeliveryOfficeName -eq "valor") |
| postalCode |Qualquer valor de cadeia de caracteres ou $null |(user.postalCode - eq "valor") |
| preferredLanguage |ISO 639-1 code |(user.preferredLanguage - eq "en-US") |
| sipProxyAddress |Qualquer valor de cadeia de caracteres ou $null |(user.sipProxyAddress -eq "valor") |
| state |Qualquer valor de cadeia de caracteres ou $null |(user.state -eq "valor") |
| streetAddress |Qualquer valor de cadeia de caracteres ou $null |(user.streetAddress -eq "valor") |
| sobrenome |Qualquer valor de cadeia de caracteres ou $null |(user.surname -eq "valor") |
| telephoneNumber |Qualquer valor de cadeia de caracteres ou $null |(user.telephoneNumber -eq "valor") |
| usageLocation |Código do país indicados dois |(user.usageLocation -eq "EUA") |
| userPrincipalName |Um valor de cadeia de caracteres. |(user.userPrincipalName -eq "alias@domain") |
| userType |member guest $null |(ser.userType -eq "Membro") |

### <a name="properties-of-type-string-collection"></a>Propriedades de coleção de cadeias de caracteres de tipo
Operadores permitidos

* -contains
* -notContains

| Propriedades | Valores permitidos | Uso |
| --- | --- | --- |
| otherMails |Um valor de cadeia de caracteres. |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP:alias@domainsmtp:alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Propriedades de vários valores
Operadores permitidos

* -qualquer (satisfeito quando pelo menos um item na coleção de saudação corresponde a condição de saudação)
* -todas (atendidas quando todos os itens na coleção de saudação correspondem à condição de saudação)

| Propriedades | Valores | Uso |
| --- | --- | --- |
| assignedPlans |Cada objeto na coleção de saudação expõe Olá propriedades de cadeia de caracteres a seguir: capabilityStatus, serviço, servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

Propriedades de vários valores são coleções de objetos de saudação mesmo tipo. Você pode usar - todo e qualquer-tooapply operadores tooone uma condição ou todos Olá itens na coleção de hello, respectivamente. Por exemplo:

assignedPlans é uma propriedade de valores múltiplos que lista todos os planos de serviço toohello usuário atribuídos. Olá abaixo expressão irá selecionar os usuários que têm Olá Exchange Online (plano 2) plano de serviço que também está no estado habilitado:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(identificador de Guid de saudação identifica o plano do serviço Exchange Online (plano 2) hello.)

> [!NOTE]
> Isso é útil se você quiser tooidentify todos os usuários para quem um Office 365 (ou outro serviço Online da Microsoft) recurso foi habilitado, para tootarget de exemplo com um determinado conjunto de políticas.

Olá expressão a seguir seleciona todos os usuários com qualquer plano de serviço que está associado a saudação serviço Intune (identificado pelo nome do serviço "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Uso de valores nulos

toospecify um valor nulo em uma regra, você pode usar "null" ou $null. Exemplo:
```
   user.mail –ne null
```
é equivalente a
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Atributos de extensão e atributos personalizados
Os atributos de extensão e os atributos personalizados têm suporte das regras de associação dinâmica.

Atributos de extensão são sincronizados do servidor local de janela AD e execute o formato de saudação do "ExtensionAttributeX", onde X é igual a 1-15.
Um exemplo de uma regra que usa um atributo de extensão:
```
(user.extensionAttribute15 -eq "Marketing")
```
Atributos personalizados são sincronizados a partir de locais AD do Windows Server ou conectado SaaS aplicativo e Olá Olá formato de "user.extension_[GUID]\__ [Attribute]", onde [GUID] é o identificador exclusivo Olá no AAD para o aplicativo hello que atributo Olá criado no AAD e [Attribute] é o nome de saudação do atributo hello como ele foi criado.
Um exemplo de uma regra que usa um atributo personalizado:
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Olá nome de atributo personalizado pode ser encontrado no diretório Olá consultando um usuário do atributo usando o Gerenciador de gráficos e a pesquisa de nome de atributo hello.

## <a name="direct-reports-rule"></a>Regra de "subordinados diretos"
Você pode criar um grupo contendo todos os subordinados diretos de um gerente. Quando altera subordinados diretos do gerente de saudação em Olá futuras, Olá a associação de grupo será ajustada automaticamente.

> [!NOTE]
> 1. Para Olá regra toowork, verifique se Olá **gerente** está definida corretamente nos usuários em seu locatário. Você pode verificar o valor atual de saudação para um usuário em seus **guia perfil**.
> 2. Essa regra só dá suporte a subordinados **diretos**. No momento não é possível toocreate um grupo para uma hierarquia aninhada, por exemplo, um grupo que inclui os subordinados diretos e seus relatórios.

**grupo de saudação tooconfigure**

1. Siga as etapas 1 a 5 da seção [regra avançada de saudação toocreate](#to-create-the-advanced-rule)e selecione um **tipo de associação** de **dinâmica do usuário**.
2. Em Olá **regras de associação dinâmica** folha, digite regra Olá com hello sintaxe a seguir:

    *Subordinados diretos para "{obectID_of_manager}"*

    Um exemplo de uma regra válida:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Depois de salvar a regra hello, todos os usuários com hello especificado valor de ID de gerente será adicionado toohello grupo.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>Usando regras de toocreate de atributos para objetos de dispositivo
Você também pode criar uma regra que seleciona objetos de dispositivo para associação em um grupo. Olá seguintes atributos de dispositivo pode ser usado.

 Atributo do dispositivo  | Valores | Exemplo
 ----- | ----- | ----------------
 accountEnabled | verdadeiro, falso | (device.accountEnabled -eq true)
 displayName | Um valor de cadeia de caracteres. |(device.displayName -eq "Rob Iphone”)
 deviceOSType | Um valor de cadeia de caracteres. | (device.deviceOSType -eq "IOS")
 deviceOSVersion | Um valor de cadeia de caracteres. | (device.OSVersion -eq "9.1")
 deviceCategory | o nome de uma categoria de dispositivo válida | (device.deviceCategory -eq "BYOD")
 deviceManufacturer | Um valor de cadeia de caracteres. | (device.deviceManufacturer -eq "Samsung")
 deviceModel | Um valor de cadeia de caracteres. | (device.deviceModel -eq "iPad Air")
 deviceOwnership | Pessoal, empresa | (device.deviceOwnership -eq "Company")
 domainName | Um valor de cadeia de caracteres. | (device.domainName -eq "contoso.com")
 enrollmentProfileName | Nome do perfil de registro do dispositivo da Apple | (device.enrollmentProfileName -eq "DEP iPhones")
 isRooted | verdadeiro, falso | (device.isRooted -eq true)
 managementType | MDM (para dispositivos móveis)<br>PC (para computadores gerenciados por agente de computador do Intune Olá) | (device.managementType -eq "MDM")
 organizationalUnit | qualquer valor de cadeia de caracteres correspondente Olá nome de unidade organizacional hello, definida por um Active Directory no local | (device.organizationalUnit -eq "US PCs")
 deviceId | uma ID de dispositivo do Azure AD válida | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 ID do objeto | uma ID de objeto do Azure AD válida |  (device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")




## <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre grupos no Azure Active Directory.

* [Consultar grupos existentes](active-directory-groups-view-azure-portal.md)
* [Criar um novo grupo e adicionando membros](active-directory-groups-create-azure-portal.md)
* [Gerenciar configurações de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerenciar associações de um grupo](active-directory-groups-membership-azure-portal.md)
* [Gerenciar regras dinâmicas para usuários em um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
