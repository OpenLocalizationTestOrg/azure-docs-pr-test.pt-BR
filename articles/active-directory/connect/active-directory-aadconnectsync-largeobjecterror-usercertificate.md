---
title: "Sincronização do Azure AD Connect: Tratamento de erros LargeObject causados pelo atributo userCertificate | Microsoft Docs"
description: "Este tópico fornece as etapas de correção de saudação LargeObject erros causados pelo atributo userCertificate."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Sincronização do Azure AD Connect: Tratamento de erros LargeObject causados pelo atributo userCertificate

O AD do Azure impõe um limite máximo de **15** certificado valores hello **userCertificate** atributo. Se a conexão do AD do Azure exporta um objeto com mais de 15 valores tooAzure AD, o AD do Azure retorna um **LargeObject** erro com a mensagem:

>*"hello provisionado é muito grande. Corte o número de saudação de valores de atributo nesse objeto. Olá operação será repetida em Olá próximo ciclo de sincronização..."*

Olá LargeObject erro pode ser causado por outros atributos do AD. tooconfirm que realmente é causada por atributo de userCertificate hello, você precisa tooverify objeto Olá no AD local ou em Olá [Gerenciador de sincronização do serviço de pesquisa de metaverso](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

lista de saudação tooobtain de objetos em seu locatário com LargeObject erros, use um dos Olá métodos a seguir:

 * Se o seu locatário está habilitado para o Azure AD Connect Health para sincronização, você pode consultar toohello [relatório de erros de sincronização](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) fornecido.
 
 * Olá notificação por e-mail para erros de sincronização de diretório que é enviada no final de saudação de cada ciclo de sincronização tem a lista de saudação de objetos com LargeObject erros. 
 * Olá [guia de operações do Gerenciador de serviço de sincronização](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) exibe a lista de saudação de objetos com LargeObject erros se você clicar em operação de tooAzure AD hello mais recente exportação.
 
## <a name="mitigation-options"></a>Opções de mitigação
Até que o erro de LargeObject Olá for resolvido, outros toohello de alterações de atributo mesmo objeto não pode ser exportada tooAzure AD. Erro de saudação tooresolve, você pode considerar Olá as opções a seguir:

 * Atualização do Azure AD Connect toobuild 1.1.524.0 ou posterior. No Azure AD Connect compilar 1.1.524.0, regras de sincronização de fora da caixa de saudação foram atualizados toonot exportação atributos userCertificate e userSMIMECertificate se atributos Olá tem mais de 15 valores. Para obter detalhes sobre como tooupgrade do Azure AD Connect, consulte tooarticle [do Azure AD Connect: atualização do toohello versão anterior mais recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Implementar um **regra de sincronização de saída** no Azure AD Connect que exporta um **valor em vez de valores reais Olá para objetos com mais de 15 certificado nulo**. Essa opção é adequada se você não exige qualquer Olá certificado valores toobe exportado tooAzure AD para objetos com valores mais de 15. Para obter detalhes sobre como tooimplement esta sincronização de regra, consulte a seção toonext [exportação de toolimit de regra de sincronização de implementação do atributo userCertificate](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Reduzir Olá número de valores de certificado no hello local objeto do AD (15 ou menos) removendo valores que não estão mais em uso pela sua organização. Isso é adequado se inchaço do atributo Olá é causado por certificados expirados ou não é utilizados. Você pode usar o hello [aqui disponível do script PowerShell](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) toohelp localizar, fazer backup e excluir certificados expirados em suas instalações AD. Antes de excluir certificados Olá, é recomendável que você verifique com os administradores de infraestrutura de chave pública de saudação em sua organização.

 * Configurar o Azure AD Connect tooexclude Olá userCertificate atributo que está sendo exportado tooAzure AD. Em geral, não recomendamos essa opção como Olá atributo pode ser usado por cenários específicos do Microsoft Online Services tooenable. Especificamente:
    * atributo de userCertificate de saudação no objeto de usuário de saudação é usado por clientes do Outlook e o Exchange Online para assinatura e criptografia. toolearn mais sobre esse recurso, consulte tooarticle [S/MIME para assinatura e criptografia](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * atributo de userCertificate Olá no objeto de computador Olá é usado por dispositivos que ingressaram no domínio tooconnect tooAzure AD do AD do Azure tooallow Windows 10 no local. toolearn mais sobre esse recurso, consulte tooarticle [conectar dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Implementação de exportação de toolimit de regra de sincronização do atributo userCertificate
Erro de LargeObject de saudação tooresolve causado pelo atributo de userCertificate Olá, você pode implementar uma regra de sincronização de saída no Azure AD Connect que exporta um **valor em vez de valores reais Olá para objetos com valores de certificado mais de 15Nulo**. Esta seção descreve a regra de sincronização de Olá Olá etapas tooimplement necessária para **usuário** objetos. Olá etapas podem ser adaptadas para **contato** e **computador** objetos.

> [!IMPORTANT]
> Exportação de valor nulo remove valores previamente exportado com êxito tooAzure AD de certificado.

etapas de saudação podem ser resumidas como:

1. Desabilitar o agendador de sincronização e verificar se não há nenhuma sincronização em andamento.
3. Localize a regra de sincronização de saída existente Olá userCertificate atributo.
4. Crie regra de sincronização de saída Olá necessária.
5. Verifique se a nova regra de sincronização Olá em um objeto existente com o erro LargeObject.
6. Aplica Olá nova regra tooremaining objetos sincronizados com o erro LargeObject.
7. Verifique se nenhuma alteração inesperada esperando tooAzure toobe exportado AD.
8. Exporte Olá alterações tooAzure AD.
9. Habilitar o agendador de sincronização novamente.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Etapa 1. Desabilitar o agendador de sincronização e verificar se não há nenhuma sincronização em andamento
Certifique-se de que nenhuma sincronização ocorre enquanto você estiver no meio de saudação da implementação de uma nova sincronização tooavoid de regra não intencional altera sendo exportados tooAzure AD. Agendador de sincronização interna do hello toodisable:
1. Inicie sessão do PowerShell no servidor do Azure AD Connect hello.

2. Desabilite a sincronização agendada executando o cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Olá etapas anteriores são apenas toonewer aplicável versões (1.1.xxx.x) do Azure AD Connect com o agendador interno hello. Se você estiver usando versões anteriores (1.0.xxx.x) do Azure AD Connect que usa o Agendador de tarefas do Windows ou você estiver usando seu próprio sincronização periódica de tootrigger Agendador personalizado (não comum), você precisa toodisable-los adequadamente.

3. Iniciar Olá **Synchronization Service Manager** pelo vai tooSTART → serviço de sincronização.

4. Vá toohello **operações** guia e confirmar que não há nenhuma operação cujo status seja *"em"andamento.*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Etapa 2. Localizar a regra de sincronização de saída existente Olá para atributo userCertificate
Deve haver uma regra de sincronização existente que está habilitada e configurado tooexport userCertificate atributos para objetos de usuário tooAzure AD. Localize esse toofind de regra de sincronização out seu **precedência** e **filtro de escopo** configuração:

1. Iniciar Olá **Editor de regras de sincronização** pelo vai tooSTART → Editor de regras de sincronização.

2. Configure os filtros de pesquisa Olá com hello valores a seguir:

    | Atributo | Valor |
    | --- | --- |
    | Direção |**Saída** |
    | Tipo de Objeto de MV |**Pessoa** |
    | Conector |*nome de seu conector do Azure AD* |
    | Tipo de Objeto de Conector |**user** |
    | Atributos de MV |**userCertificate** |

3. Se você estiver usando o atributo de OOB (out-of-box) sincronização regras tooAzure AD conector tooexport userCertficiate para objetos de usuário, você deverá voltar Olá *"Out tooAAD – usuário ExchangeOnline"* regra.
4. Anote Olá **precedência** valor desta regra de sincronização.
5. Selecione a regra de sincronização hello e clique em **editar**.
6. Em Olá *"Editar reservado confirmação regra"* caixa de diálogo pop-up, clique em **não**. (Não se preocupe, não vamos toomake qualquer regra de sincronização de toothis de alteração).
7. Na tela de edição de saudação, selecione Olá **filtro de escopo** guia.
8. Anote a configuração do filtro de escopo de saudação. Se você estiver usando a regra de sincronização OOB hello, exatamente haverá **um grupo de filtro escopo que contém duas cláusulas**, incluindo:

    | Atributo | Operador | Valor |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Usuário |
    | cloudMastered | NOTEQUAL | True  |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Etapa 3. Criar regra de sincronização de saída Olá necessária
Olá nova regra de sincronização deve ter Olá mesmo **filtro de escopo** e **maior precedência** de Olá regra de sincronização existente. Isso garante que Olá nova regra de sincronização se aplica a toohello mesmo conjunto de objetos como regra de sincronização existente hello e substituições Olá sincronização regra existente para o atributo de userCertificate hello. regra de sincronização de saudação toocreate:
1. No Editor de regras de sincronização de saudação, clique em Olá **adicionar nova regra** botão.
2. Em Olá **guia Descrição**, fornecer Olá a seguinte configuração:

    | Atributo | Valor | Detalhes |
    | --- | --- | --- |
    | Nome | *Fornecer um nome* | Por exemplo, *"Out tooAAD – personalizado substituir para userCertificate"* |
    | Descrição | *Fornecer uma descrição* | Por exemplo, *“Se o atributo userCertificate tiver mais de 15 valores, exportar NULL”.* |
    | Sistema Conectado | *Selecione Olá conector AD do Azure* |
    | Tipo de Objeto do Sistema Conectado | **user** | |
    | Tipo de Objeto de Metaverso | **person** | |
    | Tipo de link | **Join** | |
    | Precedência | *Escolher um número entre 1 a 99* | Hello número escolhido não deve ser usado por qualquer regra de sincronização existente e tem um valor mais baixo (e, portanto, a precedência mais alta) de Olá regra de sincronização existente. |

3. Vá toohello **filtro de escopo** guia e implementar hello está usando o mesmo escopo Olá existente sincronização regra de filtro.
4. Olá ignorar **regras de junção** guia.
5. Vá toohello **transformações** guia tooadd uma nova transformação usando configuração a seguir:

    | Atributo | Valor |
    | --- | --- |
    | Tipo de Fluxo |**Expressão** |
    | Atributo de Destino |**userCertificate** |
    | Atributo de Origem |*Olá Use expressão a seguir*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Clique em Olá **adicionar** regra de sincronização do botão toocreate hello.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Etapa 4. Verifique se a nova regra de sincronização Olá em um objeto existente com o erro LargeObject
Isso é tooverify que Olá sincronização regra criada está funcionando corretamente em um objeto existente do AD com o erro LargeObject antes de aplicá-lo tooother objetos:
1. Vá toohello **operações** guia Olá Synchronization Service Manager.
2. Selecione a operação mais recente de tooAzure AD exportação hello e clique em um dos objetos de saudação com LargeObject erros.
3.  Na tela de pop-up de propriedades de objeto de espaço do conector hello, clique em Olá **visualização** botão.
4. Na tela pop-up de visualização de saudação, selecione **completo sincronização** e clique em **visualização confirmar**.
5. Fechar a tela de visualização hello e tela de propriedades de objeto de espaço do conector hello.
6. Vá toohello **conectores** guia Olá Synchronization Service Manager.
7. Clique duas vezes em Olá **AD do Azure** conector e selecione **executar...**
8. No pop-up de executar conector hello, selecione **exportar** etapa e clique em **Okey**.
9. Aguarde a exportação tooAzure AD toocomplete e confirmar que não há nenhum erro LargeObject mais nesse objeto específico.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Etapa 5. Aplicar Olá nova regra tooremaining objetos sincronizados com o erro LargeObject
Após a adição de regra de sincronização Olá, é necessário toorun uma etapa de sincronização completa no hello conector AD:
1. Vá toohello **conectores** guia Olá Synchronization Service Manager.
2. Clique duas vezes em Olá **AD** conector e selecione **executar...**
3. No pop-up de executar conector hello, selecione **sincronização completa** etapa e clique em **Okey**.
4. Aguarde Olá toocomplete de etapa de sincronização completa.
5. Repita Olá acima etapas para Olá restantes conectores AD se você tiver mais de um AD conectores. Normalmente, vários conectores serão necessários se você tiver vários diretórios locais.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Etapa 6. Verifique se nenhuma alteração inesperada esperando tooAzure toobe exportado AD
1. Vá toohello **conectores** guia Olá Synchronization Service Manager.
2. Clique duas vezes em Olá **AD do Azure** conector e selecione **espaço do conector de pesquisa**.
3. No pop-up de espaço do conector de pesquisa hello:
    1. Definir o escopo muito**exportar pendente**.
    2. Marque todas as 3 caixas de seleção, incluindo **Adicionar**, **Modificar** e **Excluir**.
    3. Clique em **pesquisa** botão tooreturn todos os objetos com alterações que aguardam tooAzure toobe exportado AD.
    4. Verifique se não há alterações inesperadas. alterações de saudação tooexamine para um determinado objeto, clique duas vezes no objeto de saudação.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Etapa 7. Exportar Olá alterações tooAzure AD
tooexport Olá alterações tooAzure AD:
1. Vá toohello **conectores** guia Olá Synchronization Service Manager.
2. Clique duas vezes em Olá **AD do Azure** conector e selecione **executar...**
4. No pop-up de executar conector hello, selecione **exportar** etapa e clique em **Okey**.
5. Aguarde a exportação tooAzure AD toocomplete e confirmar que não há mais erros de LargeObject.

### <a name="step-8-re-enable-sync-scheduler"></a>Etapa 8. Habilitar o agendador de sincronização novamente
Agora que Olá problema for resolvido, reabilitar o Agendador de sincronização interna hello:
1. Inicie uma sessão do PowerShell.
2. Habilite a sincronização agendada novamente executando o cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Olá etapas anteriores são apenas toonewer aplicável versões (1.1.xxx.x) do Azure AD Connect com o agendador interno hello. Se você estiver usando versões anteriores (1.0.xxx.x) do Azure AD Connect que usa o Agendador de tarefas do Windows ou você estiver usando seu próprio sincronização periódica de tootrigger Agendador personalizado (não comum), você precisa toodisable-los adequadamente.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

