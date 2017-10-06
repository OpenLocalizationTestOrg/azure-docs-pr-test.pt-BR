---
title: "aaaConnect tooDynamics 365 (online) de aplicativos do Azure lógica | Microsoft Docs"
description: "Criar lógica de fluxos de trabalho do aplicativo gerenciar entidades de Dynamics 365 (online) por meio de saudação API fornecida pelo conector Olá Dynamics 365"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Conecte-se tooDynamics 365 dos fluxos de trabalho de aplicativo de lógica

Com lógica de aplicativos, você pode se conectar tooDynamics 365 (online) e criar fluxos de negócios útil criar registros, atualizar itens ou retornam uma lista de registros. Com o conector de saudação do Dynamics 365, você pode:

* Crie o fluxo de negócios com base em dados Olá obtido Dynamics 365 (online).
* Use as ações que uma resposta de obtenção e saída de hello tornar disponível para outras ações. Por exemplo, quando um item é atualizado no Dynamics 365 (online), você pode enviar um e-mail usando o Office 365.

Este tópico mostra como toocreate um lógica de aplicativo que cria uma tarefa no Dynamics 365 sempre que um novo cliente potencial é criado no Dynamics 365.

## <a name="prerequisites"></a>Pré-requisitos
* Uma conta do Azure.
* Uma conta do Dynamics 365 (online).

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Criar uma tarefa sempre que um novo cliente em potencial é criado no Dynamics 365

1.  [Entrar tooAzure](https://portal.azure.com).

2.  Na caixa de pesquisa do Azure hello, digite `Logic apps`, e pressione ENTER.

      ![Localizar aplicativos lógicos](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  Em **Aplicativos lógicos**, clique em **Adicionar**.

      ![Adicionar LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  aplicativo lógico do hello toocreate, Olá completa **nome**, **assinatura**, **grupo de recursos**, e **local** campos e, em seguida, clique em  **Criar**.

5.  Selecione Olá novo aplicativo de lógica. Quando você receber Olá **implantação bem-sucedida** notificação, clique em **atualizar**.

6.  Em **Ferramentas de Desenvolvimento**, clique em **Designer de Aplicativo Lógico**. Na lista de modelos de saudação, clique em **aplicativo lógica em branco**.

7.  Na caixa de pesquisa hello, digite `Dynamics 365`. No hello Dynamics 365 dispara lista, selecione **Dynamics 365 – quando um registro é criado**.

8.  Se você for solicitado toosign em tooDynamics 365, faça isso agora.

9.  Nos detalhes de gatilho hello, digite Olá informações a seguir:

  * **Nome da organização**. Selecione Olá Dynamics 365 instância que você deseja Olá lógica aplicativo toolisten para.

  * **Nome da entidade**. Selecione a entidade de saudação que você deseja toolisten para. Esse evento atua como um aplicativo de lógica do gatilho toostart hello. 
  Neste passo a passo, **Clientes em potencial** está selecionado.

  * **Com que frequência você deseja toocheck para itens?** Esses valores são definidos como geralmente Olá lógica aplicativo verifica para gatilho de toohello relacionados de atualizações. configuração de padrão de saudação é toocheck para atualizações a cada três minutos.

    * **Frequência**. Selecione segundos, minutos, horas ou dias.

    * **Intervalo**. Insira o número de saudação de segundos, minutos, horas ou dias que você deseja toopass antes da próxima verificação de saudação.

      ![Detalhes do Gatilho de Aplicativo Lógico](./media/connectors-create-api-crmonline/trigger-details.png)

10. Clique na caixa **Nova etapa** e depois clique em **Adicionar uma ação**.

11. Na caixa de pesquisa hello, digite `Dynamics 365`. Na lista de ações de saudação, selecione **Dynamics 365 – criar um novo registro**.

12. Digite hello informações a seguir:

    * **Nome da organização**. Selecione a instância de saudação do Dynamics 365 onde você deseja que o registro de Olá Olá fluxo toocreate. 
    Observe que essa instância não tem toobe Olá mesmo instância onde o evento de saudação é disparado do.

    * **Nome da entidade**. Selecione a entidade de saudação que você deseja toocreate um registro quando Olá evento for disparado. 
    Neste passo a passo, **Tarefas** está selecionado.

13. Clique em Olá **assunto** caixa que aparece. Olá dinâmico conteúdo lista que aparece, você pode selecionar qualquer um desses campos:

    * **Sobrenome**. Selecionar este campo insere Olá sobrenome Olá lead campo assunto Olá tarefa Olá, quando Olá tarefa registro é criado.
    * **Tópico**. Selecionar este campo inserções Olá tópico campo cliente potencial de saudação no campo de assunto Olá para tarefa Olá, quando Olá tarefa registro é criado. 
    Clique em **tópico** tooadd que toohello **assunto** caixa.

      ![Criar novos detalhes do registro do Aplicativo Lógico](./media/connectors-create-api-crmonline/create-record-details.png)

14. Na barra de ferramentas de Designer de lógica do aplicativo hello, clique em **salvar**.

    ![Barra de ferramentas do Designer do Aplicativo Lógico Salvar](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. Olá toostart lógica de aplicativo, clique em **executar**.

    ![Barra de ferramentas do Designer do Aplicativo Lógico Salvar](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Agora, crie um registro de cliente em potencial no Dynamics 365 para Vendas e veja seu fluxo em ação!

## <a name="set-advanced-options-for-a-logic-app-step"></a>Definir opções avançadas para uma etapa de aplicativo lógico

toospecify como toofilter dados em uma etapa de aplicativo lógica, clique em **Mostrar opções avançadas** essa etapa, em seguida, adicionar um filtro ou a ordem pela consulta.

Por exemplo, você pode usar um filtro consulta tooget somente as contas ativas e Ordenar por nome de conta de saudação. tooperform tarefas, insira a consulta de filtro OData Olá `statuscode eq 1`e selecione **nome da conta** na lista de conteúdo dinâmico Olá. Mais informações: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) e [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Opções avançadas de aplicativo lógico](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Práticas recomendadas ao usar o opções avançadas

Quando você adiciona um campo de valor de tooa, você deve corresponder o tipo de campo de saudação se você digitar um valor ou selecione um valor na lista de conteúdo dinâmico Olá.

Tipo de campo  |Como toouse  |Onde toofind  |Nome  |Tipo de dados  
---------|---------|---------|---------|---------
Campos de texto|Campos de texto exigem uma única linha de texto ou conteúdo dinâmico que seja um campo de tipo de texto. Exemplos incluem campos de categoria e subcategoria hello.|Configurações > personalizações > Personalizar Olá System > entidades > tarefa > campos |categoria |Linha única de texto        
Campos de número inteiro | Alguns campos exigem conteúdo inteiro ou dinâmico que seja um campo de tipo inteiro. Exemplos incluem Porcentagem concluída e Duração. |Configurações > personalizações > Personalizar Olá System > entidades > tarefa > campos |percentcomplete |Número inteiro         
Campos de data | Alguns campos exigem a data inserida no formato dd/mm/aaaa ou conteúdo dinâmico que seja um campo do tipo data. Exemplos incluem Criado em, Data de início, Início real, Último tempo de espera, Término real e Data de vencimento. | Configurações > personalizações > Personalizar Olá System > entidades > tarefa > campos |createdon |Data e hora
Campos que exigem um registro de ID e tipo de pesquisa |Alguns campos que fazem referência a outro registro de entidade requerem Olá ID do registro e o tipo de pesquisa de saudação. |Configurações > personalizações > Personalizar Olá System > entidades > conta > campos  | accountid  | Chave primária

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Mais exemplos de campos que exigem uma ID de registro e tipo de pesquisa
Expandindo a tabela anterior Olá, aqui estão mais exemplos de campos que não funcionam com os valores selecionados da lista de conteúdo dinâmico Olá. Em vez disso, esses campos exigem ambos os uma pesquisa e a ID de tipo de registro inserido nos campos de saudação em PowerApps.  
* Proprietário e Tipo de proprietário. campo de proprietário Olá deve ser uma ID válida. registro de usuário ou da equipe Olá tipo proprietário deve ser **systemusers** ou **equipes**.
* Cliente e Tipo de cliente. campo de saudação do cliente deve ser uma conta válida ou entre em contato com a ID de registro. Olá tipo proprietário deve ser **contas** ou **contatos**.
* Referente e Referente ao tipo. Olá sobre o campo deve ser uma ID de registro válida, como uma conta ou entre em contato com a ID de registro. Hello em relação ao tipo deve ser tipo de pesquisa Olá para registro Olá, como **contas** ou **contatos**.

Olá seguinte exemplo de ação de criação de tarefa adiciona um registro de conta que corresponde a ID do registro toohello adicioná-lo toohello sobre o campo de tarefa hello.

![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid-type-account.png)

Este exemplo também atribui Olá tarefa tooa usuário específico com base na ID de registro. do usuário hello

![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind um registro da ID, consulte Olá seção a seguir: *localizar a ID de registro de saudação*

## <a name="find-hello-record-id"></a>Localizar a ID de registro de saudação

1. Abra um registro, como um registro de conta.

2. Na barra de ferramentas do hello ações, clique em **Pop-Out** ![pop-up registro](./media/connectors-create-api-crmonline/popout-record.png).
Como alternativa, na barra de ferramentas de ações de hello, toocopy Olá a URL completa em seu programa de email padrão, clique em **EMAIL um LINK**.

   ID do registro Olá é exibida entre Olá % 7b e %7 d codificação de caracteres da URL de saudação.

   ![Fluxo recordId e conta tipo](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Solucionar problemas
tootroubleshoot uma etapa com falha em um aplicativo de lógica, exibir detalhes de status saudação do evento hello.

1. Em **Aplicativos Lógicos**, clique no seu aplicativo lógico e, em seguida, em **Visão geral**. 

   Olá área Resumo é mostrado e fornece o status de saudação executar para o aplicativo de lógica de saudação. 

   ![Status de execução do aplicativo lógico](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview obter mais informações sobre todas as execuções com falha, clique em Olá Falha ao evento. tooexpand uma etapa com falha, clique nesta etapa.

   ![Expandir etapa com falha](./media/connectors-create-api-crmonline/tshoot2.png)

   detalhes da etapa Olá aparecem e podem ajudar a solucionar Olá causa da falha de saudação.

   ![Detalhes da etapa com falha](./media/connectors-create-api-crmonline/tshoot3.png)

Para obter mais informações sobre como solucionar problemas de aplicativos lógicos, consulte [Diagnosticando falhas do aplicativo lógico](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/crm/). 

## <a name="next-steps"></a>Próximas etapas
Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).
