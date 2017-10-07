---
title: "Sincronização do Azure AD Connect: alterando a configuração padrão de saudação | Microsoft Docs"
description: "Fornece as práticas recomendadas para alterar a configuração padrão de saudação de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Sincronização do Azure AD Connect: práticas recomendadas para alterar a configuração padrão de saudação
Olá finalidade deste tópico é toodescribe com e sem suporte a alterações tooAzure AD Connect sincronização.

configuração de saudação criada pelo Azure AD Connect funciona "como está" para a maioria dos ambientes que sincronizam o Active Directory no local com o Azure AD. No entanto, em alguns casos, é necessário tooapply toosatisfy de configuração de tooa algumas alterações um determinado necessário ou requisito.

## <a name="changes-toohello-service-account"></a>Conta de serviço toohello alterações
Sincronização do Azure AD Connect está em execução em uma conta de serviço criado pelo Assistente de instalação de saudação. Essa conta de serviço contém Olá criptografia chaves toohello banco de dados usado pela sincronização. Ele é criado com uma senha longa de 127 caracteres e senha de saudação é definida toonot expirar.

* É **sem suporte** toochange ou redefinição de senha Olá Olá da conta de serviço. Isso destrói as chaves de criptografia de saudação e serviço Olá não é capaz de tooaccess Olá dados e não é capaz de toostart.

## <a name="changes-toohello-scheduler"></a>Agendador de toohello de alterações
Começando com as versões de saudação do build 1.1 (fevereiro de 2016), você pode configurar Olá [Agendador](active-directory-aadconnectsync-feature-scheduler.md) toohave uma sincronização diferente ciclo padrão Olá 30 minutos.

## <a name="changes-toosynchronization-rules"></a>Regras de tooSynchronization de alterações
Assistente de instalação de saudação fornece uma configuração que deve toowork para cenários mais comuns de saudação. Caso você precise de configuração de toohello toomake alterações, você deve seguir estas regras toostill têm uma configuração com suporte.

* Você pode [alterar fluxos de atributo](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) se fluxos de atributos diretos saudação padrão não são adequados para sua organização.
* Se você quiser muito[fluxo não um atributo](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) e remover valores de qualquer atributo existente no AD do Azure, e em seguida, você precisa toocreate uma regra para este cenário.
* [Desabilite uma Regra de sincronização indesejada](#disable-an-unwanted-sync-rule) em vez de excluí-la. Uma regra excluída é recriada durante uma atualização.
* muito[alterar uma regra de caixa de saída](#change-an-out-of-box-rule), você deve fazer uma cópia da saudação original de regras e desabilitar a regra de fora da caixa de saudação. Olá Editor de regra de sincronização solicita e ajuda.
* Exporte suas regras de sincronização personalizadas usando o Editor de regras de sincronização de saudação. Olá editor fornece um script do PowerShell que você pode usar tooeasily recriá-los em um cenário de recuperação de desastres.

> [!WARNING]
> regras de sincronização de fora da caixa de saudação têm uma impressão digital. Se você fizer uma alteração de regras de toothese, impressão digital de saudação não correspondentes. Você pode ter problemas no futuro de hello quando você tentar tooapply uma nova versão do Azure AD Connect. Só faça a forma de saudação de alterações que é descrito neste artigo.

### <a name="disable-an-unwanted-sync-rule"></a>Desabilite uma Regra de sincronização indesejada
Não exclua uma regra de sincronização integrada. Ela será recriada durante a próxima atualização.

Em alguns casos, o Assistente de instalação Olá produziu uma configuração que não está funcionando para a sua topologia. Por exemplo, se houver uma topologia de floresta de conta-recurso, mas têm esquema estendido Olá na floresta de conta Olá com o esquema de saudação do Exchange, regras para o Exchange são criadas para floresta de conta hello e floresta de recursos de saudação. Nesse caso, você precisa toodisable Olá regra de sincronização para o Exchange.

![Regra de sincronização desabilitada](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

Imagem Olá acima, o Assistente de instalação Olá encontrou um esquema antigo do Exchange 2003 na floresta de conta hello. Essa extensão do esquema foi adicionado antes de floresta de recursos de saudação foi introduzida no ambiente da Fabrikam. tooensure nenhum atributo de implementação do Exchange antigo Olá é sincronizado, a regra de sincronização Olá deve ser desabilitada, conforme mostrado.

### <a name="change-an-out-of-box-rule"></a>alterar uma regra integrada
tempo somente Hello, que você deve alterar uma regra de caixa de saída é quando precisar de regra de associação toochange hello. Se você precisar toochange um fluxo de atributos, você deve criar uma regra de sincronização com precedência maior do que as regras do hello fora da caixa. Olá somente é necessário praticamente tooclone é Olá regra **na entrada do AD – ingresso de usuário**. Você pode substituir todas as outras regras com uma regra de prioridade mais alta.

Se você precisar de regra de fora da caixa de tooan toomake alterações, faça uma cópia da regra de out-of-box hello e desabilitar a regra original hello. Em seguida, criar regra clonado do hello alterações toohello. Olá Editor de regra de sincronização é ajudá-lo com essas etapas. Quando você abre uma regra integrada, vê essa caixa de diálogo:   
![Aviso de regra integrada](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Selecione **Sim** toocreate uma cópia da regra de saudação. regra clonado Hello, em seguida, é aberta.  
![Regra clonada](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

Nessa regra clonado, faça quaisquer alterações necessárias tooscope, junção e transformações.

## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
