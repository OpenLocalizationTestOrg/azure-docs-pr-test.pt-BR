---
title: "aaaAzure do Active Directory cenários adicionais de licenciamento baseado em grupo | Microsoft Docs"
description: "Mais cenários de licenciamento baseado em grupo do Azure Active Directory"
services: active-directory
keywords: Licenciamento do AD do Azure
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Cenários, as limitações e problemas conhecidos com o licenciamento de toomanage grupos no Active Directory do Azure

Use Olá toogain uma compreensão mais avançada de licenciamento do Azure Active Directory (AD do Azure) baseado em grupo de informações e exemplos a seguir.

## <a name="usage-location"></a>Local de uso

Alguns serviços da Microsoft não estão disponíveis em todos os locais. Usuário tooa possa ser atribuídos uma licença, o administrador de saudação tem Olá toospecify **local de uso** propriedade no usuário hello. Em [Olá portal do Azure](https://portal.azure.com), você pode especificar em **usuário** &gt; **perfil** &gt; **configurações**.

Para atribuição de grupo de licença, todos os usuários sem um local de uso especificado herdará o local de saudação do diretório de saudação. Se você tiver usuários em vários locais, verifique se tooreflect corretamente nos objetos do usuário antes de adicionar usuários toogroups com licenças.

> [!NOTE]
> A atribuição de licença de grupo nunca modificará um valor existente de localização de uso em um usuário. Recomendamos que você sempre defina local de uso como parte de seu fluxo de criação de usuário no AD do Azure (por exemplo, por meio de configuração do AAD Connect) - que garantirá o resultado de saudação da atribuição de licença sempre está correto e os usuários não recebem serviços em locais que não são permitido.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Usar o licenciamento baseado em grupo com grupos dinâmicos

Você pode usar o licenciamento baseado em grupo com qualquer grupo de segurança, o que significa que ele pode ser combinado a grupos dinâmicos do Azure AD. Grupos dinâmicos executados regras em tooautomatically de atributos de objeto de usuário adicionar e remover usuários dos grupos.

Por exemplo, você pode criar um grupo dinâmico do mesmo conjunto de produtos que você deseja tooassign toousers. Cada grupo é preenchido por uma regra de adição de usuários por seus atributos, e cada grupo é licenças Olá atribuído quando você quer tooreceive. Você pode atribuir Olá atributo local e sincronizá-lo com o Azure AD, ou você pode gerenciar o atributo Olá diretamente na nuvem de saudação.

Licenças são atribuídas toohello usuário logo após serem adicionados toohello grupo. Quando o atributo de saudação é alterado, usuário Olá deixa grupos Olá e licenças de saudação são removidas.

### <a name="example"></a>Exemplo

Considere o exemplo hello de uma solução de gerenciamento de identidade local que decide quais usuários terão acesso tooMicrosoft web services. Ele usa **extensionAttribute1** toostore representando licenças Olá Olá usuário deve ter de valor de uma cadeia de caracteres. O Azure AD Connect é sincronizado com o Azure AD.

Os usuários podem precisar de uma licença, mas não da outra ou talvez precisem de ambas. Aqui está um exemplo, no qual você está distribuindo o Office 365 Enterprise E5 e mobilidade corporativa + segurança (EMS) toousers em grupos de licenças:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: serviços de base

![Captura de tela de serviços de base do Office 365 Enterprise E5](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: usuários licenciados

![Captura de tela de usuários licenciados do Enterprise Mobility + Security](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

Neste exemplo, modificar um usuário e definir seu valor de toohello extensionAttribute1 de `EMS;E5_baseservices;` se você quiser Olá usuário toohave ambas as licenças. Você pode fazer essa modificação local. Depois de saudação alterar sincronizado com a nuvem hello, Olá é adicionado automaticamente grupos tooboth e licenças são atribuídas.

![Captura de tela mostrando como tooset Olá extensionAttribute1 do usuário](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Tenha cuidado ao modificar uma regra de associação de um grupo existente. Quando uma regra é alterada, associação de saudação do grupo hello serão reavaliada e os usuários que não correspondem Olá novo regra será removida (usuários que correspondam a nova regra de saudação ainda não serão afetados durante esse processo). Esses usuários terão suas licenças removidas durante processo de saudação que pode resultar na perda de serviço ou, em alguns casos, perda de dados.

> Se você tiver um grande grupo dinâmico que dependem para atribuição de licença, considere a possibilidade de validar alterações principais em um grupo menor de teste antes de aplicá-las grupo principal toohello.

## <a name="multiple-groups-and-multiple-licenses"></a>Vários grupos e várias licenças

Um usuário pode ser membro de vários grupos com licenças. Aqui estão algumas coisas tooconsider:

- Várias licenças para Olá mesmo produto pode sobrepor e geram todos habilitados serviços sendo aplicado toohello usuário. Olá, exemplo a seguir mostra dois grupos de licenciamento: *serviços base E3* contém Olá foundation services toodeploy primeiro tooall usuários. E *E3 estendidos serviços* contém serviços adicionais (Sway e planejador) toodeploy somente toosome os usuários. Neste exemplo, o usuário Olá foi adicionado tooboth grupos:

  ![Captura de tela de serviços habilitados](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Como resultado, Olá usuário tem 7 dos serviços de 12 Olá produto Olá habilitado, ao mesmo tempo usando apenas uma licença para este produto.

- Olá selecionando *E3* licença mostra mais detalhes, incluindo informações sobre quais grupos causou que toobe serviços habilitado para o usuário hello.

  ![Captura de tela de serviços habilitados por grupo](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>As licenças diretas coexistem com as licenças de grupo

Quando um usuário herda uma licença de um grupo, você não pode remover ou modificar essa atribuição de licença em Propriedades de saudação do usuário diretamente. As alterações devem ser feitas no grupo de saudação e, em seguida, propagadas tooall usuários.

É possível, no entanto, tooassign Olá mesmo licença de produto diretamente toohello usuário, na inclusão toohello herdada de licença. Você pode habilitar serviços adicionais do produto de saudação apenas para um usuário, sem afetar outros usuários.

Licenças atribuídas diretamente podem ser removidas e não afetam as licenças herdadas. Considere a possibilidade de usuário de saudação que herda de uma licença do Office 365 Enterprise E3 de um grupo.

1. Inicialmente, o usuário Olá herda licença Olá somente de Olá *serviços básicos E3* grupo, o que permite que os quatro planos de serviço, conforme mostrado:

  ![Captura de tela de serviços habilitados para grupo E3](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. Você pode selecionar **atribuir** toodirectly atribuir um usuário de toohello de licença E3. Nesse caso, você vai toodisable serviço todos os planos exceto Enterprise Yammer:

  ![Captura de tela de como tooassign uma licença de usuário de tooa diretamente](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Como resultado, o usuário Olá ainda usa apenas uma licença de produto do hello E3. Mas atribuição direta Olá permite Olá serviço Yammer Enterprise somente para esse usuário. Você pode ver quais serviços estão habilitados por membros do grupo Olá versus atribuição direta hello:

  ![Captura de tela de atribuição herdada versus direta](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Quando você usar a atribuição direta, Olá operações a seguir é permitida:

  - Yammer que Enterprise pode ser desativado no objeto de usuário Olá diretamente. Olá **ativar/desativar** alternância na ilustração Olá foi habilitada para esse serviço, como contrário toohello outros alternâncias de serviço. Porque o serviço hello está habilitado diretamente no usuário hello, ele pode ser modificado.
  - Serviços adicionais podem ser habilitados, assim como parte da saudação atribuído diretamente a licença.
  - Olá **remover** botão pode ser usado tooremove Olá direto licença usuário hello. Você pode ver que usuário Olá agora somente tem licença de grupo herdadas hello e permanecem habilitados, somente os serviços original de saudação:

    ![Captura de tela mostrando como tooremove direto atribuição](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>Gerenciar novos serviços adicionado tooproducts
Quando a Microsoft adiciona um novo produto tooa serviço, ele será habilitado por padrão em todos os toowhich grupos atribuídos a licença de produto hello. Os usuários em seu locatário que estão inscritos toonotifications sobre alterações do produto receberá emails antecipadamente, notificando sobre adições de serviço futuros hello.

Como administrador, você pode revisar todos os grupos afetados pela alteração hello e tome uma ação, como desabilitar o novo serviço de saudação em cada grupo. Por exemplo, se você criou grupos que direcionam apenas serviços específicos para implantação, reveja esses grupos e verifique se os serviços recém-adicionados estão desabilitados.

Este é um exemplo da aparência desse processo:

1. Originalmente, você atribuiu Olá *Office 365 Enterprise E5* grupos de tooseveral do produto. Um desses grupos, chamados *O365 E5 - Exchange somente* foi Olá somente projetado tooenable *Exchange Online (planejar 2)* serviço para seus membros.

2. Você recebeu uma notificação da Microsoft que Olá E5 produto será estendido com um novo serviço - *Microsoft Stream*. Quando o serviço de saudação fica disponível em seu locatário, você pode fazer a seguir hello:

3. Vá toohello [ **Active Directory do Azure > licenças > todos os produtos** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) folha e selecione *Office 365 Enterprise E5*, em seguida, selecione **grupos licenciado**  tooview uma lista de todos os grupos com o produto.

4. Clique no grupo de saudação desejado tooreview (nesse caso, *O365 E5 - Exchange somente*). Isso abrirá o hello **licenças** guia. Clicar na licença de E5 Olá abrirá uma folha listando todos os serviços habilitados.
> [!NOTE]
> Olá *Microsoft Stream* serviço foi automaticamente adicionado e habilitado neste grupo, na inclusão toohello *Exchange Online* serviço:

  ![Captura de tela de serviço novo adicionado tooa licença de grupo](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Toodisable Olá novo serviço nesse grupo, clique em Olá **ativar/desativar** alternar próximo serviço toohello e clique em Olá **salvar** botão de alteração de saudação tooconfirm. O AD do Azure agora processará todos os usuários na alteração de saudação do hello grupo tooapply; todos os novos usuários adicionados toohello grupo não terá Olá *Microsoft Stream* serviço habilitado.

  > [!NOTE]
  > Os usuários ainda podem ter serviço Olá habilitado por meio de alguns outros atribuição de licença (outro grupo que são membros ou uma atribuição de licença direto).

6. Se necessário, execute Olá atribuídas mesmas etapas para outros grupos com este produto.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Use toosee PowerShell que foi herdada e direcionar licenças
Se os usuários tiverem uma licença atribuída diretamente ou herdada de um grupo, você pode usar um toocheck de script do PowerShell.

1. Executar Olá `connect-msolservice` tooauthenticate de cmdlet e conecte-se tooyour locatário.

2. `Get-MsolAccountSku`pode ser usado toodiscover todas as licenças de produto provisionado no locatário hello.

  ![Captura de tela do cmdlet Get-Msolaccountsku de saudação](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Saudação de uso *AccountSkuId* valor licença Olá lhe interessam com [este script do PowerShell](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Isso produzirá uma lista de usuários que têm esta licença com informações de saudação sobre como licença Olá é atribuída.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Atividade de licenciamento baseado em grupo toomonitor os logs de auditoria de uso

Você pode usar [logs de auditoria do AD do Azure](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee todas as atividades relacionadas a toogroup licenciamento baseado, incluindo:
- quem alterou licenças em grupos
- Quando o sistema Olá iniciou o processamento de uma alteração de licença do grupo, e quando concluído
- as alterações de licença foram feitas tooa usuário como resultado de uma atribuição de grupo de licenças.

>[!NOTE]
> Logs de auditoria estão disponíveis na maioria dos blades em Olá seção do Active Directory do Azure do portal de saudação. Dependendo de onde você acessá-los, os filtros podem ser tooonly previamente aplicadas Mostrar atividade toohello relevantes contexto folha hello. Se você não estiver vendo resultados Olá esperado, examine [Olá opções de filtragem](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) ou acessar logs de auditoria Olá filtrada em [ **Active Directory do Azure > atividade > logs de auditoria** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Descobrir quem modificou uma licença de grupo

1. Saudação de conjunto **atividade** filtrar muito*conjunto grupo licença* e clique em **aplicar**.
2. resultados da saudação incluem todos os casos de licenças que estão sendo definidas ou modificadas em grupos.
>[!TIP]
> Você também pode digitar o nome de saudação do grupo de saudação em Olá *destino* filtrar tooscope Olá resultados.

3. Clique em um item Olá lista Exibir toosee Olá detalhes do que foi alterado. Em *propriedades modificadas* valores novos e antigos para atribuição de licença de saudação são listados.

Este é um exemplo de alterações recentes de licença de grupo, com detalhes:

![Captura de tela de alterações de licença de grupo](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Descobrir quando as alterações de grupo iniciaram e concluíram o processamento

Quando uma licença é alterado em um grupo, AD do Azure começará a aplicar alterações que Olá tooall os usuários.

1. toosee quando grupos iniciou o processamento, defina Olá **atividade** filtrar muito*começar a aplicar toousers de licença de grupo com base em*. Observe que ator Olá para operação de saudação é *AD do Microsoft Azure licenciamento baseado em grupo* -conta de um sistema que é usado tooexecute todas as alterações do grupo de licença.
>[!TIP]
> Clique em um item de saudação do hello lista toosee *propriedades modificadas* field - mostra as alterações de licença Olá foram escolhidas para processamento. Isso é útil se você fez várias alterações tooa grupo e não tiver certeza que foi processado.

2. Da mesma forma, toosee quando grupos de conclusão do processamento, use Olá filtro valor *concluir a aplicação toousers de licença de grupo com base em*.
>[!TIP]
> Nesse caso, Olá *propriedades modificadas* campo contém um resumo dos resultados de saudação - isso é útil tooquickly seleção se processamento resultou em erros. Resultado de exemplo:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. toosee Olá registro completo como um grupo foi processado, incluindo todas as alterações do usuário, defina Olá filtros a seguir:
  - **Iniciado Por (Ator)**: “Licenciamento Baseado em Grupo do Microsoft Azure AD”
  - **Intervalo de Datas** (opcional): intervalo personalizado para quando você sabe que um grupo específico iniciou e concluiu o processamento

Neste exemplo de saída mostra início de saudação do processamento, resultante de todas as alterações do usuário e saudação de conclusão do processamento de.

![Captura de tela de alterações de licença de grupo](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Clicar em itens relacionados muito*licença de usuário de alteração* mostrará detalhes de licença alterações aplicadas tooeach individuais de usuário.

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

Se você usar o licenciamento baseado em grupo, é uma boa ideia toofamiliarize por conta própria com hello lista de limitações e problemas conhecidos a seguir.

- No momento, o licenciamento baseado em grupo não dá suporte a grupos que contêm outros grupos (grupos aninhados). Se você aplicar um grupo aninhado de tooa de licença, somente membros de primeiro nível imediata do usuário de saudação do grupo de Olá tem licenças de saudação aplicadas.

- recurso de saudação só pode ser usado com grupos de segurança. Grupos do Office não têm suporte no momento e não será capaz de toouse-los no processo de atribuição de licença hello.

- Olá [portal de administração do Office 365](https://portal.office.com ) não oferece suporte para licenciamento baseado em grupo. Se um usuário herda uma licença de um grupo, esta licença aparece no portal de administração do Office de hello como uma licença de usuário normal. Se você tentar toomodify de licença ou tente licença de saudação tooremove, portal Olá retorna uma mensagem de erro. Licenças herdadas de grupos não podem ser modificadas diretamente em um usuário.

- Quando um usuário é removido de um grupo e perde licença hello, planos de serviço de saudação de licença (por exemplo, SharePoint Online) são definidos tooa **suspenso** estado. Olá planos de serviço não estão definidos tooa final, estado de desabilitado. Essa precaução pode evitar a remoção acidental de dados do usuário, caso um administrador cometa um erro no gerenciamento de associação a um grupo.

- Quando as licenças são atribuídas ou modificadas para um grupo grande (por exemplo, 100.000 usuários), isso pode afetar o desempenho. Especificamente, volume Olá alterações gerados por automação do Azure AD pode afetar negativamente o desempenho de saudação da sincronização de diretório entre o AD do Azure e sistemas locais.

- Automação de gerenciamento de licença não reage automaticamente tooall tipos de alterações no ambiente de saudação. Por exemplo, você pode executou fora de licenças, fazendo com que alguns usuários toobe em um estado de erro. toofree se a contagem de estações disponíveis hello, você pode remover alguns licenças atribuídas diretamente de outros usuários. No entanto, sistema Olá automaticamente reagir toothis alteração e corrija os usuários em que estado de erro.

  Como tipos de toothese uma solução alternativa de limitações, você pode ir toohello **grupo** folha no AD do Azure e clique em **reprocessar**. Este comando processa todos os usuários nesse grupo e resolve os estados de erro hello, se possível.

- Licenciamento baseado em grupo não registra erros quando uma licença não pôde ser atribuída a usuário tooa devido a configuração de endereço proxy duplicado tooa no Exchange Online; Esses usuários são ignorados durante a atribuição de licença. Para obter mais informações sobre como tooidentify e resolver esse problema, consulte [nesta seção](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre outros cenários de gerenciamento de licenças por meio de licenciamento baseado em grupo, consulte:

* [O que é o licenciamento baseado em grupo no Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Atribuir licenças tooa grupo no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificar e resolver problemas de licença para um grupo no Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Como indivíduo toomigrate licenciado usuários licenciamento no Azure Active Directory com base em toogroup](active-directory-licensing-group-migration-azure-portal.md)
