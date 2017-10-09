---
title: "grupo de tooa aaaAssign licenças no Active Directory do Azure | Microsoft Docs"
description: "Como tooassign licenças toousers por meio de licenciamento de grupo do Active Directory do Azure"
services: active-directory
keywords: Licenciamento do AD do Azure
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Atribuir licenças toousers pela associação de grupo no Active Directory do Azure

Este artigo o orienta por meio de atribuição de grupo de tooa de licenças de produto de usuários no Azure Active Directory (AD do Azure) e, em seguida, verificar se estão licenciados corretamente.

Neste exemplo, o locatário Olá contém um grupo de segurança chamado **departamento de RH**. Esse grupo inclui todos os membros do departamento de recursos humanos da saudação (cerca de 1.000 usuários). Você deseja tooassign Office 365 Enterprise E3 licenças toohello todo o departamento. Olá serviço Yammer Enterprise que está incluído no produto Olá deve ser desabilitada temporariamente até que o departamento de saudação está pronto toostart usá-lo. Você também deseja toodeploy mobilidade corporativa + segurança licenças toohello mesmo grupo de usuários.

> [!NOTE]
> Alguns serviços da Microsoft não estão disponíveis em todos os locais. Usuário tooa possa ser atribuídos uma licença, o administrador de Olá tem propriedade de local de uso toospecify Olá no usuário hello.

> Para atribuição de grupo de licença, todos os usuários sem um local de uso especificado herdará o local de saudação do diretório de saudação. Se você tiver usuários em vários locais, recomendamos que você sempre defina local de uso como parte de seu fluxo de criação de usuário no AD do Azure (por exemplo, por meio de configuração do AAD Connect) - que garantirá o resultado de saudação da atribuição de licença sempre está correto e os usuários não receberão serviços em locais que não são permitidos.

## <a name="step-1-assign-hello-required-licenses"></a>Etapa 1: Atribuir licenças Olá necessária

1. Entrar toohello [ **portal do Azure** ](https://portal.azure.com) com uma conta de administrador. licenças de toomanage, conta Olá deve ser um administrador de conta de usuário ou função de administrador global.

2. Selecione **mais serviços** Olá painel de navegação esquerdo e, em seguida, selecione **Active Directory do Azure**. Você pode adicionar esse tooFavorites folha ou fixá-lo toohello painel do portal.

3. Em Olá **Active Directory do Azure** folha, selecione **licenças**. Isso abrirá uma folha de onde você pode ver e gerenciar todos os produtos licenciados por locatário hello.

4. Em **todos os produtos**, selecione o Office 365 Enterprise E3 e mobilidade corporativa + segurança selecionando nomes de produto hello. atribuição de saudação toostart, selecione **atribuir** na parte superior de saudação da folha de saudação.

   ![Todos os produtos, atribuir licença](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. Em Olá **atribuir licenças** folha, clique em **usuários e grupos** tooopen Olá **usuários e grupos** folha. Pesquisa de nome de grupo Olá *departamento de RH*, selecione o grupo hello e, em seguida, ser tooconfirm se clicando **selecione** na parte inferior da saudação da folha de saudação.

   ![Selecione um grupo](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. Em Olá **atribuir licenças** folha, clique em **opções de atribuição (opcionais)**, que exibe todos os planos de serviço incluídos no hello dois produtos são selecionados anteriormente. Localizar **Yammer Enterprise** e ativá-la **Off** toodisable do serviço de licença do produto hello. Confirmar clicando **Okey** na parte inferior de saudação do **opções atribuição**.

   ![Opções de atribuição](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. atribuição de saudação toocomplete, em Olá **atribuir licenças** folha, clique em **atribuir** na parte inferior da saudação da folha de saudação.

8. É exibida uma notificação no canto superior direito de saudação que mostra o status de saudação e o resultado do processo de saudação. Se o grupo de toohello Olá atribuição não pôde ser concluído (por exemplo, devido a licenças já existentes no grupo de saudação), clique em detalhes de tooview Olá notificação de falha de saudação.

Agora, especificamos um modelo de licença para o grupo de saudação do departamento de RH. Um processo em segundo plano no AD do Azure foi iniciada tooprocess todos os membros desse grupo existentes. Esta operação inicial pode levar algum tempo, dependendo do tamanho atual de saudação do grupo de saudação. Na próxima etapa de Olá, vamos descrevem como tooverify esse processo Olá foi concluído e determinar se atenção adicional é necessário tooresolve problemas.

> [!NOTE]
> Você pode iniciar Olá mesma atribuição de um local alternativo: **usuários e grupos** no AD do Azure. Vá muito**Active Directory do Azure** > **usuários e grupos** > **todos os grupos de**. Localize o grupo de saudação, selecioná-la e ir toohello **licenças** Olá guia **atribuir** botão na parte superior da folha de saudação abre a folha de atribuição de licença de saudação.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Etapa 2: Verificar se a atribuição de saudação inicial foi concluída

1. Vá muito**Active Directory do Azure** > **usuários e grupos** > **todos os grupos de**. Em seguida, localize Olá **departamento de RH** licenças atribuídas ao grupo.

2. Em Olá **departamento de RH** folha de grupo, selecione **licenças**. Isso permite confirmar rapidamente se licenças tiverem sido atribuídas totalmente toousers e se houver erros que você precisa toolook em. Olá informações a seguir está disponível:

   - Lista de licenças de produtos que estão atualmente atribuídos toohello grupo. Selecione uma entrada tooshow Olá serviços específicos que foram habilitados e toomake é alterado.

   - Status da saudação mais recente licença alterações feitas toohello grupo (se alterações Olá estão sendo processadas ou se a conclusão do processamento de todos os membros de usuário).

   - Informações sobre os usuários que estão em um estado de erro porque não podem ser atribuídas a licenças toothem.

   ![Opções de atribuição](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Confira informações mais detalhadas sobre a licença de processamento em **Azure Active Directory** > **Usuários e grupos** > *Nome do grupo* > **Logs de auditoria**. Observe Olá atividades a seguir:

   - Atividade: **começar a aplicar toousers de licença de grupo com base em**. Isso é registrado quando o sistema Olá pega Olá alterações de atribuição de licença no grupo de saudação e inicia aplicá-la tooall membros de usuário. Ele contém informações sobre Olá alteração foi feita.

   - Atividade: **concluir a aplicação toousers de licença de grupo com base em**. Isso é registrado quando o sistema Olá termina de processar todos os usuários no grupo de saudação. Ele contém um resumo de quantos usuários foram processados com êxito e quantos usuários não puderam ter licenças de grupo atribuídas.

   [Leia esta seção](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn mais informações sobre como os logs de auditoria podem ser tooanalyze usado alterações feitas pelo licenciamento baseado em grupo.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Etapa 3: verificar problemas de licença e resolvê-los

1. Vá muito**Active Directory do Azure** > **usuários e grupos** > **todos os grupos de**e localize Olá **departamento de RH**licenças atribuídas ao grupo.
2. Em Olá **departamento de RH** folha de grupo, selecione **licenças**. notificação de saudação na parte superior da folha de saudação mostra que há 10 usuários que não foi possível atribuir licenças para. Clicar nela abre uma lista de todos os usuários com um estado de erro para esse grupo.
3. Olá **falha atribuições** coluna indica que ambas as licenças de produto não foi possível atribuir usuários toohello. Olá **principais o motivo da falha** coluna contém causa falha Olá Olá. Nesse caso, **Planos de serviço conflitante**.

   ![Atribuições com falha](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Selecione uma saudação do usuário tooopen **licenças** folha. Esta folha mostra todas as licenças atribuídas atualmente toohello usuário. Neste exemplo, o usuário de saudação tem licença de saudação do Office 365 Enterprise E1 que foi herdada de saudação **os usuários do quiosque** grupo. Isso está em conflito com licença Olá E3 Olá tooapply sistema tentativa de saudação **departamento de RH** grupo. Como resultado, nenhuma das licenças de saudação do grupo recebeu toohello usuário.

   ![Exibir as licenças para um usuário](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve este conflito, remover usuário Olá Olá **os usuários do quiosque** grupo. Depois que o AD do Azure processa alterações Olá, Olá **departamento de RH** licenças são atribuídas corretamente.

   ![Licença atribuída corretamente](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o recurso de saudação definida para o gerenciamento de licenças por meio de grupos, consulte Olá artigos a seguir:

* [O que é o licenciamento baseado em grupo no Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identificar e resolver problemas de licença para um grupo no Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Como indivíduo toomigrate licenciado usuários licenciamento no Azure Active Directory com base em toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Cenários adicionais de licenciamento baseado em grupo do Azure Active Directory](active-directory-licensing-group-advanced.md)
