---
title: "Azure AD Connect: solucionando erros durante a sincronização | Microsoft Docs"
description: "Explica como tootroubleshoot erros encontrados durante a sincronização com o Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Solucionando erros durante a sincronização
Poderão ocorrer erros quando os dados de identidade são sincronizados do Windows Server Active Directory (AD DS) tooAzure do Active Directory (AD do Azure). Este artigo fornece uma visão geral dos diferentes tipos de erros de sincronização, alguns cenários possíveis de saudação que fazer com que esses erros e possíveis maneiras toofix hello. Este artigo inclui tipos de erro comuns hello e não pode abranger todos os possíveis erros de saudação.

 Este artigo pressupõe leitor Olá esteja familiarizado com hello subjacente [design conceitos do AD do Azure e o Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Com a versão mais recente de saudação do Azure AD Connect \(agosto de 2016 ou posterior\), um relatório de erros de sincronização está disponível no hello [Portal do Azure](https://aka.ms/aadconnecthealth) como parte do Azure AD Connect Health para sincronização.

Começando em 1º de setembro de 2016 [do Azure Active Directory duplicar atributo resiliência](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) recurso será habilitado por padrão para todos os Olá *novo* locatários do Azure Active Directory. Este recurso será automaticamente habilitado para os locatários existentes nos meses futuros hello.

Conexão do AD do Azure executa 3 tipos de operações de diretórios Olá mantém em sincronia: Import, sincronização e exportação. Erros podem ocorrer em todas as operações de saudação. Este artigo se concentra principalmente em caso de erros durante a exportação tooAzure AD.

## <a name="errors-during-export-tooazure-ad"></a>Erros durante a exportação tooAzure AD
A seção seguinte descreve os diferentes tipos de sincronização de erros que podem ocorrer durante a saudação tooAzure AD da operação de exportação usando Olá conector AD do Azure. Esse conector pode ser identificado pelo formato de nome de saudação sendo "contoso. *onmicrosoft.com*".
Erros durante a exportação tooAzure AD indicam que a operação Olá \(adicionar, atualizar e excluir etc.\) tentativa de conexão do AD do Azure \(mecanismo de sincronização\) no Azure Active Directory falhou.

![Visão geral de Erros de Exportação](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Erros de Incompatibilidade de Dados
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Descrição
* Quando do Azure AD Connect \(mecanismo de sincronização\) instrui objetos de tooadd ou atualização do Active Directory do Azure, o AD do Azure correspondências Olá objeto de entrada usando Olá **sourceAnchor** atributo toohello  **immutableId** atributo de objetos no AD do Azure. Essa correspondência é chamada de **Correspondência Rígida**.
* Ao AD do Azure **não localizar** qualquer objeto que corresponde a saudação **immutableId** atributo com hello **sourceAnchor** atributo do objeto de entrada hello, antes de provisionar um novo objeto, ele volta toouse Olá ProxyAddresses e UserPrincipalName atributos toofind uma correspondência. Essa correspondência é chamada de **Correspondência Flexível**. Olá correspondência flexível é projetado toomatch objetos já está presente no AD do Azure (que são originados no AD do Azure) com hello novos objetos que está sendo adicionado/atualizado durante a sincronização que representam Olá mesma entidade (usuários e grupos) no local.
* **InvalidSoftMatch** erro ocorre quando hello rígida correspondência não localizar qualquer objeto correspondente **AND** correspondência flexível localiza um objeto correspondente, mas esse objeto tem um valor diferente de *immutableId* de Olá do objeto de entrada *SourceAnchor*, sugerir que Olá correspondência de objeto foi sincronizado com outro objeto do Active Directory local.

Em outras palavras, em ordem para Olá correspondência flexível toowork, Olá objeto toobe correspondido soft com não deve ter qualquer valor de saudação *immutableId*. Se qualquer objeto com *immutableId* conjunto com um valor está falhando Olá rígido correspondência mas satisfatória Olá soft-critérios, operação Olá resultaria em um erro de sincronização InvalidSoftMatch.

Atributos do Active Directory do Azure esquema permite que dois ou mais objetos toohave Olá mesmo valor de saudação a seguir. \(Esta não é uma lista completa.\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ObjectId

> [!NOTE]
> [Azure AD atributo duplicado atributo resiliência](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) recurso também está sendo revertido como o comportamento padrão de saudação do Active Directory do Azure.  Isso reduzirá o número de saudação de erros de sincronização visto pelo Azure AD Connect (bem como outros clientes de sincronização), tornando o AD do Azure mais resiliente forma Olá trata duplicados ProxyAddresses e UserPrincipalName atributos presentes no AD local ambientes. Esse recurso não corrigir erros de eliminação de duplicação de saudação. Para dados de saudação ainda precisam toobe fixa. Mas ele permite provisionamento de novos objetos que estão bloqueados caso contrário, que está sendo provisionado devido a valores de tooduplicated no AD do Azure. Isso também reduzirá o número de saudação de erros de sincronização retornada toohello cliente de sincronização.
> Se esse recurso estiver habilitado para seu locatário, você não verá erros de sincronização de InvalidSoftMatch Olá vistos durante o provisionamento de novos objetos.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Cenários de Exemplo para InvalidSoftMatch
1. Dois ou mais objetos com hello mesmo valor de atributo ProxyAddresses existe no local do Active Directory. Somente um deles está sendo provisionado no Azure AD.
2. Dois ou mais objetos com hello mesmo valor de userPrincipalName existe no local do Active Directory. Somente um deles está sendo provisionado no Azure AD.
3. Um objeto foi adicionado no Olá no Active Directory local com hello mesmo valor do atributo ProxyAddresses que um objeto existente no Active Directory do Azure. objeto Olá adicionado no local não está obtendo provisionado no Azure Active Directory.
4. Um objeto foi adicionado no local do Active Directory com hello mesmo valor do atributo userPrincipalName que uma conta no Active Directory do Azure. objeto Olá não obtendo provisionado no Active Directory do Azure.
5. Uma conta sincronizada foi movida de tooForest de uma floresta b. do Azure AD Connect (mecanismo de sincronização) estava usando Olá toocompute de atributo ObjectGUID SourceAnchor. Após a movimentação de floresta hello, valor Olá Olá SourceAnchor é diferente. novo objeto Hello (da floresta B) está falhando toosync com o objeto existente Olá no AD do Azure.
6. Um objeto sincronizado forem excluído acidentalmente no Active Directory local e um novo objeto foi criado no Active Directory para Olá mesma entidade (por exemplo, o usuário) sem excluir a conta de saudação no Active Directory do Azure. nova conta de saudação falha toosync com o objeto do AD do Azure existente de saudação.
7. O Azure AD Connect foi desinstalado e reinstalado. Durante a instalação da nova hello, um atributo diferente foi escolhido como Olá SourceAnchor. Todos os objetos de saudação que anteriormente tinham sincronizadas interrompido sincronizando com o erro InvalidSoftMatch.

#### <a name="example-case"></a>Caso de exemplo:
1. **Bob Smith** é um usuário sincronizado no Azure Active Directory do Active Directory local de *contoso.com*
2. O **UserPrincipalName** de Bob Smith está definido como **bobs@contoso.com**.
3. **"abcdefghijklmnopqrstuv = ="** é hello **SourceAnchor** calculado pelo AD do Azure Connect usando Bob Smith **objectGUID** do local do Active Directory, que é hello **immutableId** de Bob Smith no Active Directory do Azure.
4. Bob também tem os seguintes valores para Olá **proxyAddresses** atributo:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Um novo usuário, **Bob Taylor**, é adicionado toohello no Active Directory local.
6. O **UserPrincipalName** de Bob Taylor é definido como **bobt@contoso.com**.
7. **"abcdefghijkl0123456789 = =" "** é hello **sourceAnchor** calculado pelo AD do Azure Connect usando de Bob Taylor **objectGUID** do local do Active Directory. Objeto de Bob Taylor não sincronizou ainda tooAzure do Active Directory.
8. Bob Taylor tem Olá seguintes valores para o atributo proxyAddresses de saudação
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Durante a sincronização, o Azure AD Connect reconhecerá adição Olá Bob Taylor no local do Active Directory e peça do Azure AD toomake Olá a mesma alteração.
10. O Azure AD executará primeiro a correspondência rígida. Ou seja, ele irá procurar se houver qualquer objeto com hello immutableId igual muito "abcdefghijkl0123456789 = =". Correspondência de disco rígida falhará, pois nenhum outro objeto no Azure AD terá essa immutableId.
11. AD do Azure, em seguida, tente toosoft-match Bob Taylor. Ou seja, ele irá procurar se houver qualquer objeto com toohello igual proxyAddresses três valores, inclusivesmtp:bob@contoso.com
12. O AD do Azure encontrará objeto Bob Smith toomatch Olá soft-critérios. Mas esse objeto tem valor de saudação do immutableId = "abcdefghijklmnopqrstuv = =". Isso indica que esse objeto foi sincronizado de outro objeto do Active Directory local. Assim, o Azure AD não pode realizar uma correspondência flexível desses objetos e resulta em um erro de sincronização **InvalidSoftMatch**.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Como toofix InvalidSoftMatch erro
o motivo mais comum para Olá InvalidSoftMatch erro Hello é dois objetos com diferente SourceAnchor \(immutableId\) têm o mesmo valor para Olá ProxyAddresses e/ou o UserPrincipalName atributos, que são usados durante a saudação de saudação processo de correspondência de software no AD do Azure. Em ordem toofix Olá correspondência flexível inválido

1. Identificar proxyAddresses Olá duplicado, userPrincipalName ou outro valor de atributo que está causando o erro de saudação. Também identificar quais dois \(ou mais\) os objetos envolvidos no conflito de saudação. Olá relatório gerado pelo [Azure AD Connect Health para sincronização](https://aka.ms/aadchsyncerrors) podem ajudá-lo a identificar Olá dois objetos.
2. Identificar qual objeto deve continuar toohave valor de saudação duplicada e objeto que não deveria.
3. Remova valor duplicada de saudação do objeto de saudação que não deve ter esse valor. Observe que você deve alterar Olá no diretório Olá onde o objeto Olá foi originado em. Em alguns casos, talvez seja necessário toodelete um dos objetos de saudação em conflito.
4. Se você fez Olá alterar Olá no AD local, permitem Olá de sincronização do Azure AD Connect alterar.

Observe que o relatório de erros de sincronização no Azure AD Connect Health para sincronização é atualizado a cada 30 minutos e incluem erros de saudação da última tentativa de sincronização hello.

> [!NOTE]
> Imutável, por definição, não deve alterar no tempo de vida de saudação do objeto hello. Se a conexão do AD do Azure não foi configurado com alguns dos cenários de saudação em mente de saudação acima da lista, você pode acabar em uma situação onde do Azure AD Connect calcula um valor diferente de saudação SourceAnchor para objeto Olá AD representa Olá mesma entidade (usuário mesmo / grupo/contato etc) que tem um objeto do AD do Azure existente que você deseja usar toocontinue.
>
>

#### <a name="related-articles"></a>Artigos relacionados
* [Atributos duplicados ou inválidos impedem a sincronização de diretórios no Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Descrição
Quando o AD do Azure tenta toosoft correspondência dois objetos, é possível que dois objetos de diferentes "tipo de objeto" (como usuário, grupo, contato etc.) tem Olá mesmo valores para atributos de saudação usada correspondência flexível de saudação tooperform. Como a eliminação de duplicação desses atributos não é permitida no AD do Azure, Olá pode resultar em erro de sincronização "ObjectTypeMismatch".

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Cenários de exemplo para o erro ObjectTypeMismatch
* Um grupo de segurança habilitado para email é criado no Office 365. Administrador adiciona um novo usuário ou contato no AD local (que tooAzure AD ainda não sincronizou) com hello mesmo valor para o atributo ProxyAddresses de saudação do hello Office 365 grupos.

#### <a name="example-case"></a>Caso de exemplo
1. Administrador cria um novo grupo de segurança habilitado para email no Office 365 para o departamento de impostos hello e fornece um endereço de email como tax@contoso.com. Isso atribuirá o atributo ProxyAddresses de saudação para esse grupo com valor de saudação do**smtp:tax@contoso.com**
2. Um novo usuário une Contoso.com e uma conta é criada para o usuário de saudação no local com hello proxyAddress como**smtp:tax@contoso.com**
3. Quando o Azure AD Connect será sincronizado a nova conta de usuário hello, ele receberá o erro de "ObjectTypeMismatch" hello.

#### <a name="how-toofix-objecttypemismatch-error"></a>Como toofix ObjectTypeMismatch erro
motivo mais comum de saudação para erro de ObjectTypeMismatch Olá é dois objetos de tipo diferente (usuário, grupo, contato etc.) têm Olá mesmo valor para o atributo ProxyAddresses de saudação. Em ordem toofix Olá ObjectTypeMismatch:

1. Identificar Olá duplicado proxyAddresses (ou outro atributo) que causando erro de saudação do valor. Também identificar quais dois \(ou mais\) os objetos envolvidos no conflito de saudação. Olá relatório gerado pelo [Azure AD Connect Health para sincronização](https://aka.ms/aadchsyncerrors) podem ajudá-lo a identificar Olá dois objetos.
2. Identificar qual objeto deve continuar toohave valor de saudação duplicada e objeto que não deveria.
3. Remova valor duplicada de saudação do objeto de saudação que não deve ter esse valor. Observe que você deve alterar Olá no diretório Olá onde o objeto Olá foi originado em. Em alguns casos, talvez seja necessário toodelete um dos objetos de saudação em conflito.
4. Se você fez Olá alterar Olá no AD local, permitem Olá de sincronização do Azure AD Connect alterar. Relatório de erros de sincronização no Azure AD Connect Health para sincronização é atualizado a cada 30 minutos e incluem erros de saudação da última tentativa de sincronização hello.

## <a name="duplicate-attributes"></a>Atributos Duplicados
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Descrição
Atributos do Active Directory do Azure esquema permite que dois ou mais objetos toohave Olá mesmo valor de saudação a seguir. Que é a que cada objeto no AD do Azure é forçado toohave um valor exclusivo desses atributos em uma determinada instância.

* ProxyAddresses
* UserPrincipalName

Se a conexão do AD do Azure tenta tooadd um novo objeto ou atualizar um objeto existente com um valor para Olá acima atributos que já está atribuído a tooanother objeto no Active Directory do Azure, a operação de saudação resulta em erro de sincronização "AttributeValueMustBeUnique" hello.

#### <a name="possible-scenarios"></a>Cenários Possíveis:
1. Valor duplicado é o objeto já sincronizados tooan atribuído, que está em conflito com outro objeto sincronizado.

#### <a name="example-case"></a>Caso de exemplo:
1. **Bob Smith** é um usuário sincronizado no Azure Active Directory do Active Directory local de contoso.com
2. O **UserPrincipalName** local de Bob Smith está definido como **bobs@contoso.com**.
3. Bob também tem os seguintes valores para Olá **proxyAddresses** atributo:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Um novo usuário, **Bob Taylor**, é adicionado toohello no Active Directory local.
5. O **UserPrincipalName** de Bob Taylor é definido como **bobt@contoso.com**.
6. **Bob Taylor** tem Olá Olá valores a seguir **ProxyAddresses** atributo i. smtp:bobt@contoso.com ii. smtp:bob.taylor@contoso.com
7. O objeto de Bob Taylor foi sincronizado com êxito ao Azure AD.
8. Admin decidido de tooupdate Bob Taylor **ProxyAddresses** atributo com o seguinte valor de hello: posso. **smtp:bob@contoso.com**
9. AD do Azure tentará objeto de tooupdate Bob Taylor no AD do Azure com hello acima, mas que haverá falha na operação como se ProxyAddresses valor já está atribuído tooBob Smith, resultando em um erro de "AttributeValueMustBeUnique".

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Como toofix AttributeValueMustBeUnique erro
o motivo mais comum para Olá AttributeValueMustBeUnique erro Hello é dois objetos com diferente SourceAnchor \(immutableId\) ter Olá mesmo valor de saudação ProxyAddresses e/ou atributos UserPrincipalName. Em ordem toofix AttributeValueMustBeUnique erro

1. Identificar proxyAddresses Olá duplicado, userPrincipalName ou outro valor de atributo que está causando o erro de saudação. Também identificar quais dois \(ou mais\) os objetos envolvidos no conflito de saudação. Olá relatório gerado pelo [Azure AD Connect Health para sincronização](https://aka.ms/aadchsyncerrors) podem ajudá-lo a identificar Olá dois objetos.
2. Identificar qual objeto deve continuar toohave valor de saudação duplicada e objeto que não deveria.
3. Remova valor duplicada de saudação do objeto de saudação que não deve ter esse valor. Observe que você deve alterar Olá no diretório Olá onde o objeto Olá foi originado em. Em alguns casos, talvez seja necessário toodelete um dos objetos de saudação em conflito.
4. Se você fez Olá alterar Olá no AD local, permitem que Olá de sincronização do Azure AD Connect altere para Olá erro tooget fixada.

#### <a name="related-articles"></a>Artigos relacionados
-[Atributos duplicados ou inválidos impedem a sincronização de diretórios no Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Falha na Validação de Dados
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Descrição
Active Directory do Azure impõe várias restrições em Olá próprios dados antes de permitir que toobe dados gravado no diretório de saudação. Isso é tooensure que os usuários finais obtêm experiências de possíveis melhor Olá durante o uso de aplicativos de saudação que dependem de dados.

#### <a name="scenarios"></a>Cenários
a. Olá valor do atributo UserPrincipalName tem caracteres inválida ou não suportada.
b. atributo UserPrincipalName de saudação não segue o formato necessário hello.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Como toofix IdentityDataValidationFailed erro
a. Certifique-se de que o atributo userPrincipalName Olá tem suporte para caracteres e o formato necessário.

#### <a name="related-articles"></a>Artigos relacionados
* [Preparar tooprovision usuários por meio de sincronização de diretório tooOffice 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Descrição
Esse é um caso específico que resulta em uma **"FederatedDomainChangeError"** erro de sincronização quando sufixo Olá UserPrincipalName do usuário é alterado de um domínio federado tooanother de domínio federado.

#### <a name="scenarios"></a>Cenários
Para um usuário sincronizado, sufixo de UserPrincipalName Olá foi alterado de um domínio federado tooanother federado domínio local. Por exemplo, *UserPrincipalName = bob@contoso.com*  foi alterada muito*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Exemplo
1. Bob Smith, uma conta para Contoso.com, é adicionado como um novo usuário no Active Directory com hello UserPrincipalNamebob@contoso.com
2. Bob move a divisão de tooa diferente de Contoso.com chamada Fabrikam.com e sua UserPrincipalName é alteradotoobob@fabrikam.com
3. Tanto contoso.com quanto fabrikam.com são domínios federados com o Azure Active Directory.
4. O userPrincipalName de Bob não é atualizado e resulta em um erro de sincronização "FederatedDomainChangeError".

#### <a name="how-toofix"></a>Como toofix
Se o sufixo de UserPrincipalName do usuário foi atualizado de bob @**contoso.com** toobob @**fabrikam.com**, em que ambos **contoso.com** e **fabrikam.com** são **federado domínios**, em seguida, siga o erro de sincronização essas etapas toofix Olá

1. Atualização UserPrincipalName do usuário Olá no AD do Azure de bob@contoso.com toobob@contoso.onmicrosoft.com. Você pode usar o hello a seguir de comando do PowerShell com hello módulo PowerShell do AD do Azure:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Permita Olá próxima sincronização ciclo tooattempt sincronização. A sincronização de hora será bem-sucedido e atualizará Olá UserPrincipalName de Bob toobob@fabrikam.com conforme o esperado.

#### <a name="related-articles"></a>Artigos relacionados
* [As alterações não são sincronizadas pela ferramenta de sincronização do Active Directory do Azure de Olá depois de alterar Olá UPN de uma conta de usuário toouse um domínio federado diferente](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Descrição
Quando um atributo excede Olá permitido o limite de tamanho, o limite de comprimento ou o limite de contagem definido pelo esquema do Active Directory do Azure, a operação de sincronização de saudação resulta em Olá **LargeObject** ou **ExceededAllowedLength** erro de sincronização. Esse erro costuma ocorrer para Olá seguintes atributos

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Cenários possíveis
1. Atributo de userCertificate de Bob está armazenando tooBob de muitos certificados atribuídos. Eles podem incluir certificados mais antigos e expirados. limite rígido Olá é 15 certificados. Para obter mais informações sobre como toohandle LargeObject erros com userCertificate atributo, por favor, consulte tooarticle [LargeObject de tratamento de erros causados pelo atributo userCertificate](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Atributo de userSMIMECertificate de Bob está armazenando tooBob de muitos certificados atribuídos. Eles podem incluir certificados mais antigos e expirados. limite rígido Olá é 15 certificados.
3. ThumbnailPhoto de Bob definida no Active Directory é muito grande toobe sincronizado no AD do Azure.
4. Durante o preenchimento automático de atributo ProxyAddresses de saudação no Active Directory, um objeto tem muitas ProxyAddresses atribuídos.

### <a name="how-toofix"></a>Como toofix
1. Verifique esse atributo Olá causando erro hello está dentro Olá permitido limitação.

## <a name="related-links"></a>Links relacionados
* [Localizar objetos do Active Directory no Centro Administrativo do Active Directory](https://technet.microsoft.com/library/dd560661.aspx)
* [Como tooquery do Active Directory do Azure para um objeto usando o Azure Active Directory PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx)
