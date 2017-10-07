---
title: "resiliência de atributo de sincronização e duplicata aaaIdentity | Microsoft Docs"
description: "Novo comportamento de como toohandle objetos com UPN ou ProxyAddress conflitos durante a sincronização de diretório usando o Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Sincronização de identidades e resiliência do atributo duplicado 
A Resiliência do Atributo Duplicado é um recurso do Azure Active Directory que eliminará o atrito causado por conflitos de **UserPrincipalName** e **ProxyAddress** ao executar uma das ferramentas de sincronização da Microsoft.

Esses dois atributos são geralmente necessário toobe exclusivo em todos os **usuário**, **grupo**, ou **contato** objetos em um determinado locatário do Active Directory do Azure.

> [!NOTE]
> Somente os Usuários podem ter UPNs.
> 
> 

Olá novo comportamento permite que esse recurso está em parte da nuvem de saudação do pipeline de sincronização de saudação, portanto é cliente independente e relevante para qualquer produto de sincronização do Microsoft incluindo o Azure AD Connect, DirSync e MIM + conector. termo genérico do Hello "cliente de sincronização" é usado em toorepresent este documento qualquer um desses produtos.

## <a name="current-behavior"></a>Comportamento atual
Se houver uma tentativa de tooprovision um novo objeto com um valor UPN ou ProxyAddress que viola a restrição de exclusividade, o Active Directory do Azure bloqueia esse objeto seja criado. Da mesma forma, se um objeto for atualizado com um UPN ou ProxyAddress não exclusivos, atualização Olá falhará. Olá provisionamento tentativa ou atualização é repetida pelo cliente de sincronização de saudação em cada ciclo de exportação e continua toofail até Olá conflito é resolvido. Um email de relatório de erro é gerado após cada tentativa e um erro será registrado pelo cliente de sincronização de saudação.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Comportamento com Resiliência do Atributo Duplicado
Em vez de completamente falhando tooprovision ou atualizar um objeto com um atributo duplicado, Active Directory do Azure "colocar em quarentena" hello duplicar o atributo que possam violar a restrição de exclusividade hello. Se esse atributo é necessário para provisionamento, como UserPrincipalName, o serviço de saudação atribui um valor de espaço reservado. formato de saudação desses valores temporários  
“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.  
Se o atributo de saudação não for necessário, como um **ProxyAddress**, Active Directory do Azure simplesmente colocar em quarentena o atributo de conflito de saudação e continua com a criação do objeto de saudação ou atualização.

Ao colocar em quarentena atributo hello, informações sobre conflitos de saudação são enviadas em Olá mesmo email de relatório de erro usado no comportamento antigo hello. No entanto, essas informações só aparece no relatório de erro Olá uma vez, quando ocorre a quarentena hello, ele não continue toobe registrado no futuro emails. Além disso, como exportação Olá para este objeto foi bem-sucedida, o cliente de sincronização Olá não registrará um erro e não Olá de repetição não crie / operação após a sincronização subsequente ciclos de atualização.

toosupport que esse comportamento de um novo atributo tenha sido adicionado toohello classes de objeto de usuário, grupo e entre em contato com:  
**DirSyncProvisioningErrors**

Este é um atributo com valores múltiplos que toostore usado Olá atributos conflitantes que possam violar a restrição de exclusividade Olá devem eles adicionados normalmente. Uma tarefa de temporizador em segundo plano foi habilitada no Active Directory do Azure que executa cada toolook hora conflitos de atributo duplicados que foram resolvidos e remove automaticamente os atributos de saudação em questão de quarentena.

### <a name="enabling-duplicate-attribute-resiliency"></a>Habilitando a Resiliência do Atributo Duplicado
Resiliência de atributo duplicada será o comportamento padrão da nova Olá entre todos os locatários do Active Directory do Azure. Ela estará em por padrão para todos os locatários que habilitou a sincronização para Olá a primeira vez em 22 de agosto de 2016 ou posterior. Locatários que habilitado sincronização anterior toothis data serão Olá recurso foi habilitado em lotes. Essa distribuição começa em setembro de 2016, e uma notificação por email será enviada contato de notificação técnica do locatário tooeach com data específica de saudação quando Olá recurso será habilitado.

> [!NOTE]
> Depois que a opção Resiliência do Atributo Duplicado for habilitada, ela não poderá ser desabilitada.

toocheck se Olá recurso estiver habilitado para seu locatário, você pode fazer isso baixando a versão mais recente de saudação do módulo do Azure Active Directory PowerShell hello e executando:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> Você não pode usar o recurso de resiliência de atributo duplicada do conjunto MsolDirSyncFeature cmdlet tooproactively ativar Olá antes que ele está ativado para seu locatário. recurso de saudação do toobe tootest capaz, você precisará toocreate um novo locatário do Active Directory do Azure.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Identificação de objetos com DirSyncProvisioningErrors
Existem atualmente dois métodos tooidentify objetos que têm esses erros devido a conflitos de propriedade tooduplicate, Active Directory do Azure PowerShell e hello Portal de administração do Office 365. Não há planos tooextend tooadditional portal com base em relatórios no hello futuras.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Para Olá cmdlets do PowerShell neste tópico, a seguir Olá é verdadeira:

* Todos os cmdlets a seguir de saudação diferenciam maiusculas de minúsculas.
* Olá **– ErrorCategory PropertyConflict** devem ser incluídos. Atualmente, não existem outros tipos de **ErrorCategory**, mas isso pode ser estendido em Olá futuras.

Primeiro, comece executando **Connect-MsolService** e inserindo as credenciais para um administrador de locatário.

Em seguida, use Olá erros de tooview cmdlets e os operadores a seguir de maneiras diferentes:

1. [Ver tudo](#see-all)
2. [Por Tipo de Propriedade](#by-property-type)
3. [Por Valor Conflitante](#by-conflicting-value)
4. [Usando uma Pesquisa da Cadeia de Caracteres](#using-a-string-search)
5. [Classificado](#sorted)
6. [Em uma Quantidade Limitada ou Todos](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Ver tudo
Uma vez conectado, toosee geral lista de erros no locatário de saudação de provisionamento do atributo de execução:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Isso produz um resultado semelhante Olá seguinte:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "MsolDirSyncProvisioningError Get")  

#### <a name="by-property-type"></a>Por Tipo de Propriedade
erros de toosee por tipo de propriedade, adicione Olá **- PropertyName** sinalizador com hello **UserPrincipalName** ou **ProxyAddresses** argumento:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

Ou

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Por Valor Conflitante
erros de toosee relacionados a propriedade específica tooa adicionar Olá **- PropertyValue** sinalizador (**- PropertyName** devem também ser usados ao adicionar este sinalizador):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>Usando uma Pesquisa da Cadeia de Caracteres
toodo uma pesquisa de cadeia de caracteres amplo usar Olá **- SequênciaDePesquisa** sinalizador. Isso pode ser usado independentemente de todos os Olá acima sinalizadores, com exceção de saudação do **- ErrorCategory PropertyConflict**, que sempre é necessário:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>Em uma Quantidade Limitada ou Todos
1. **MaxResults <Int>**  pode ser usado toolimit Olá consulta tooa número específico de valores.
2. **Todos os** pode ser usado tooensure todos os resultados são recuperados no caso de Olá que existe um grande número de erros.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Portal de administração do Office 365
Você pode exibir os erros de sincronização de diretórios no Centro de administração do Office 365 hello. Olá relatório no portal só exibe Olá Office 365 **usuário** objetos que têm esses erros. Ele não mostra informações sobre conflitos entre **Groups** e **Contacts**.

![Usuários ativos](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Usuários ativos")

Para obter instruções sobre como os erros de sincronização de diretório tooview em Olá Office 365 admin center, consulte [identificar erros de sincronização de diretórios no Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Relatório de erros de sincronização de identidades
Quando um objeto com um conflito de atributo duplicado é tratado com esse novo comportamento em que uma notificação está incluída no padrão de saudação relatório de erros de sincronização de identidade de email que é enviado toohello contato técnico notificação locatário hello. No entanto, há uma alteração importante nesse comportamento. Em Olá anterior, informações sobre um conflito de atributo duplicada seriam incluídas em cada relatório de erro subsequentes até Olá conflito foi resolvido. Com esse novo comportamento, notificação de erro Olá para um determinado conflito só aparecem uma vez - ao tempo de Olá atributo conflitantes Olá foi colocado em quarentena.

Aqui está um exemplo de notificação por email que Olá parece com um conflito de ProxyAddress:  
    ![Usuários ativos](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Usuários ativos")  

## <a name="resolving-conflicts"></a>Resolução de conflitos
Táticas de estratégia e resolução para esses erros de solução de problemas não deve diferir de maneira Olá atributo duplicado erros foram manipulados em Olá anterior. Olá única diferença é que Olá timer tarefa varreduras por meio de locatário de saudação em Olá no lado do serviço tooautomatically Adicionar atributo de Olá no objeto apropriado de toohello de pergunta quando Olá conflito seja resolvido.

Hello artigo a seguir descreve as várias estratégias de solução de problemas: [atributos inválidos ou duplicados impedem a sincronização de diretórios no Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Problemas conhecidos
Nenhum desses problemas conhecidos causa degradação do serviço nem a perda de dados. Vários deles são estéticos, outras pessoas fazem com que o padrão "*pré-resiliência*" atributo duplicado erros toobe lançado em vez de colocar em quarentena o atributo de conflito hello e outro faz com que determinados erros toorequire manual extra correção-up.

**Comportamento básico:**

1. Objetos com configurações de atributo específico continuam tooreceive exportação erros como atributos de toohello contrário duplicado sendo colocados em quarentena.  
   Por exemplo:
   
    a. Um novo usuário é criado no AD com o UPN **Joe@contoso.com** e o ProxyAddress **smtp:Joe@contoso.com**
   
    b. Olá propriedades do objeto estão em conflito com um grupo existente, onde é ProxyAddress  **SMTP:Joe@contoso.com** .
   
    c. Ao exportar, um **ProxyAddress conflito** erro será lançado em vez de ter atributos de conflito de saudação em quarentena. operação de saudação é repetida após cada ciclo de sincronização subsequente como teria sido antes da habilitação do recurso de resiliência de saudação.
2. Se dois grupos são criados no local com hello mesmo endereço SMTP, tooprovision uma falha na tentativa de saudação primeiro com um padrão duplicado **ProxyAddress** erro. No entanto, valor duplicado hello está corretamente em quarentena após Olá próximo ciclo de sincronização.

**Relatório do Portal do Office**:

1. mensagem de erro detalhada Olá para dois objetos em um conjunto de conflito UPN é Olá mesmo. Isso indica que ambos tiveram seus UPNS alterados/colocados em quarentena, quando, na verdade, apenas um deles teve os dados alterados.
2. mensagem de erro detalhada Olá um conflito de UPN mostra Olá o displayName incorreto para um usuário que teve seu UPN alterado/em quarentena. Por exemplo:
   
    a. O **Usuário A** é sincronizado primeiro com **UPN = User@contoso.com**.
   
    b. **O usuário B** é tentada toobe sincronizado próximo com **UPN = User@contoso.com** .
   
    c. **Usuário B** UPN é alterado muito **User1234@contoso.onmicrosoft.com**  e  **User@contoso.com**  é adicionado muito**DirSyncProvisioningErrors**.
   
    d. a mensagem de erro Olá **usuário B** deve indicar que **usuário** já tem  **User@contoso.com**  como um UPN, mas ele mostra **usuário B** próprio displayName.

**Relatório de erros de sincronização de identidades**:

link de saudação para *etapas sobre como tooresolve esse problema* está incorreto:  
    ![Usuários ativos](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Usuários ativos")  

Ela deve apontar muito[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Consulte também
* [Sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
* [Identificar erros de sincronização de diretório no Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

