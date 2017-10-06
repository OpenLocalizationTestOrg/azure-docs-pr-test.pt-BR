---
title: "aaaManage análise Azure Data Lake usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toomanage análise Data Lake contas, dados de fontes, usuários e trabalhos."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Gerenciar análise Azure Data Lake usando Olá portal do Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados de conta, os usuários e trabalhos usando Olá portal do Azure. tópicos de gerenciamento toosee sobre como usar outras ferramentas, clique na guia na parte superior de saudação da página de saudação.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Gerenciar contas do Data Lake Analytics

### <a name="create-an-account"></a>Criar uma conta

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Intelligence + análise** > **Data Lake Analytics**.
3. Selecione os valores para Olá itens a seguir: 
   1. **Nome**: nome de saudação do hello conta da análise Data Lake.
   2. **Assinatura**: Olá usada para a conta de saudação de assinatura do Azure.
   3. **Grupo de recursos**: grupo de recursos do Azure Olá qual conta de saudação toocreate. 
   4. **Local**: Olá datacenter do Azure para a conta de análise Data Lake hello. 
   5. **Repositório data Lake**: Olá toobe de armazenamento padrão usado para a conta de análise Data Lake hello. Olá a conta do repositório Azure Data Lake Hello e hello análise Data Lake conta deve estar no mesmo local.
4. Clique em **Criar**. 

### <a name="delete-a-data-lake-analytics-account"></a>Excluir uma conta do Data Lake Analytics

Antes de excluir uma conta do Data Lake Analytics, exclua sua conta padrão do Data Lake Store.

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Excluir**.
3. Nome de conta de saudação do tipo.
4. Clique em **Excluir**.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Gerenciar as fontes de dados

Análise data Lake dá suporte a saudação fontes de dados a seguir:

* Data Lake Store
* Armazenamento do Azure

Você pode usar fontes de dados do Gerenciador de dados toobrowse e executar operações de gerenciamento de arquivo básico. 

### <a name="add-a-data-source"></a>Adicionar uma fonte de dados

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Fontes de Dados**.
3. Clique em **Adicionar Fonte de Dados**.
    
   * tooadd uma conta do repositório Data Lake, você precisa de conta de saudação toohello acesso e do nome de conta tooquery capaz de toobe-lo.
   * tooadd armazenamento de BLOBs do Azure, você precisa conta de armazenamento hello e chave de conta de saudação. toofind toohello-los, vá a conta de armazenamento no portal de saudação.

## <a name="set-up-firewall-rules"></a>Configurar regras de firewall

Você pode usar análise Data Lake toofurther bloquear acesso tooyour conta da análise Data Lake no nível de rede hello. Você pode habilitar um firewall e definir um endereço IP ou um intervalo de endereços IP para seus clientes confiáveis. Depois de habilitar essas medidas, somente os clientes que têm endereços IP hello dentro do intervalo de saudação definido podem se conectar toohello repositório.

Se outros serviços do Azure, como Azure Data Factory ou VMs, conecte-se a conta de análise Data Lake toohello, verifique se **permitem que os serviços do Azure** está ativada **em**. 

### <a name="set-up-a-firewall-rule"></a>Configurar uma regra de firewall

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. No menu Olá Olá esquerda, clique em **Firewall**.

## <a name="add-a-new-user"></a>Adicione um novo usuário

Você pode usar o hello **Assistente para adicionar usuário** tooeasily provisionar novos usuários Data Lake.

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Em saudação à esquerda, em **Introdução**, clique em **Assistente para adicionar usuário**.
3. Selecione um usuário e, em seguida, clique em **Selecionar**.
4. Selecione uma função e, em seguida, clique em **Selecionar**. tooset backup de um novo toouse de desenvolvedor do Azure Data Lake, selecione Olá **Data Lake análise desenvolvedor** função.
5. Selecione as listas de controle de acesso hello (ACLs) para bancos de dados Olá U-SQL. Quando estiver satisfeito com suas escolhas, clique em **Selecionar**.
6. Selecione Olá ACLs para arquivos. Para armazenamento de saudação padrão, não altere Olá ACLs para a pasta raiz de hello "/" e para a pasta de /system hello. Clique em **Selecionar**.
7. Examine todas as alterações selecionadas e, em seguida, clique em **Executar**.
8. Quando o Assistente de saudação for concluído, clique em **feito**.

## <a name="manage-role-based-access-control"></a>Gerenciar o controle de acesso baseado em função

Como outros serviços do Azure, você pode usar toocontrol de controle de acesso baseado em função (RBAC) como os usuários interagem com o serviço de saudação.

funções RBAC padrão Olá têm Olá recursos a seguir:
* **Proprietário**: pode enviar trabalhos, monitorar trabalhos, cancelar trabalhos de qualquer usuário e configurar a conta de saudação.
* **Colaborador**: pode enviar trabalhos, monitorar trabalhos, cancelar trabalhos de qualquer usuário e configurar a conta de saudação.
* **Leitor**: pode monitorar trabalhos.

Use Olá desenvolvedor de análise do Data Lake tooenable U-SQL desenvolvedores toouse Olá análise Data Lake serviço de função. Você pode usar a função de desenvolvedor de análise do Data Lake Olá para:
* Enviar trabalhos.
* Monitorar o progresso de status e hello de trabalho dos trabalhos enviados por qualquer usuário.
* Consulte Olá U-SQL scripts de trabalhos enviados por qualquer usuário.
* Cancelar apenas seus próprios trabalhos.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Adicionar usuários ou grupos de segurança tooa conta da análise Data Lake

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Controle de acesso (IAM)** > **Adicionar**.
3. Selecione uma função.
4. Adicione um usuário.
5. Clique em **OK**.

>[!NOTE]
>Se um usuário ou um grupo de segurança precisa toosubmit trabalhos, eles também precisam de permissão na conta do repositório de saudação. Para obter mais informações, consulte [Proteger os dados armazenados no Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>Gerenciar trabalhos

### <a name="submit-a-job"></a>Enviar um trabalho

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.

2. Clique em **Novo Trabalho**. Para cada trabalho, configure:

    1. **Nome do trabalho**: nome de saudação do trabalho de saudação.
    2. **Prioridade**: números menores têm prioridade mais alta. Se dois trabalhos são enfileirados, Olá com valor de prioridade inferior é executado primeiro.
    3. **Paralelismo**: número máximo de saudação de computação processa tooreserve para este trabalho.

3. Clique em **Enviar Trabalho**.

### <a name="monitor-jobs"></a>Monitorar trabalhos

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Exibir Todos os Trabalhos**. É mostrada uma lista de todos os trabalhos de ativo e concluído recentemente de saudação na conta de saudação.
3. Opcionalmente, clique em **filtro** toohelp localizar trabalhos Olá por **intervalo de tempo**, **nome do trabalho**, e **autor** valores. 

### <a name="monitoring-pipeline-jobs"></a>Monitorando trabalhos de pipeline
Trabalhos que fazem parte de um pipeline funcionam juntos, geralmente em sequência, tooaccomplish um cenário específico. Por exemplo, você pode ter um pipeline que limpa, extrai, transforma, agrega o uso de Customer Insights. Trabalhos do pipeline são identificados usando a propriedade de "Pipeline" hello quando Olá trabalho foi enviado. Trabalhos agendados usando o ADF V2 terão, automaticamente, essa propriedade populada. 

tooview uma lista de trabalhos de U-SQL que fazem parte de pipelines: 

1. No hello portal do Azure, vá tooyour contas de análise Data Lake.
2. Clique em **Insights de trabalho**. Olá que guia de "Todos os trabalhos" padrão, mostrando uma lista de execução, na fila e foi encerrado trabalhos.
3. Clique em Olá **Pipeline trabalhos** guia. Uma lista de trabalhos do pipeline será mostrada juntamente com estatísticas agregadas para cada pipeline.

### <a name="monitoring-recurring-jobs"></a>Monitorando trabalhos recorrentes
Um trabalho recorrente é aquele que tem Olá mesma lógica de negócios mas usa dados de entrada diferentes toda vez que ele é executado. Idealmente, trabalhos recorrentes devem sempre ter êxito e têm relativamente estável de tempo de execução; monitoramento desses comportamentos ajuda a garantir o trabalho hello está íntegro. Trabalhos recorrentes são identificados usando a propriedade de "Recurrence" hello. Trabalhos agendados usando o ADF V2 terão, automaticamente, essa propriedade populada.

tooview uma lista de trabalhos de U-SQL que são recorrentes: 

1. No hello portal do Azure, vá tooyour contas de análise Data Lake.
2. Clique em **Insights de trabalho**. Olá que guia de "Todos os trabalhos" padrão, mostrando uma lista de execução, na fila e foi encerrado trabalhos.
3. Clique em Olá **trabalhos recorrentes** guia. Uma lista de trabalhos recorrentes será mostrada juntamente com estatísticas agregadas para cada trabalho recorrente.

## <a name="manage-policies"></a>Gerenciar políticas

### <a name="account-level-policies"></a>Políticas no nível da conta

Essas políticas se aplicam a tooall trabalhos em uma conta da análise Data Lake.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Número máximo de AUs em uma conta do Data Lake Analytics
Uma política controla o número total de saudação de unidades de análise (Austrália) pode usar sua conta da análise Data Lake. Por padrão, o valor de saudação é definido too250. Por exemplo, se esse valor é definido too250 Austrália, você pode ter um trabalho em execução com 250 tooit de AUs atribuídos ou 10 trabalhos em execução com 25 Austrália cada. Trabalhos adicionais que são enviados são enfileirados até que trabalhos em execução Olá tenham terminados. Quando terminarem de trabalhos em execução, Austrália é liberadas para Olá na fila de trabalhos toorun.

número de saudação toochange de AUs para sua conta da análise Data Lake:

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Propriedades**.
3. Em **Austrália máximo**, mover o controle deslizante de saudação tooselect um valor ou insira o valor de saudação na caixa de texto de saudação. 
4. Clique em **Salvar**.

> [!NOTE]
> Se você precisa de mais do que Olá padrão (250) Austrália, no portal de saudação, clique em **ajuda + suporte** toosubmit uma solicitação de suporte. número de saudação de AUs disponíveis em sua conta da análise Data Lake pode ser aumentado.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Número máximo de trabalhos que podem ser executados simultaneamente
Uma política que controla quantos trabalhos podem ser executados em Olá simultaneamente. Por padrão, esse valor é definido too20. Se sua análise Data Lake Austrália disponíveis novos trabalhos são agendado toorun imediatamente até que número total de saudação de trabalhos em execução atinja o valor de saudação dessa política. Quando você atingir o número máximo de saudação de trabalhos que podem ser executadas simultaneamente, os trabalhos subsequentes são enfileirados em ordem de prioridade até que conclua a um ou mais trabalhos em execução (dependendo da disponibilidade Austrália).

número de saudação toochange de trabalhos que podem ser executadas simultaneamente:

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Propriedades**.
3. Em **máximo número de executando trabalhos**, mover o controle deslizante de saudação tooselect um valor ou insira o valor de saudação na caixa de texto de saudação. 
4. Clique em **Salvar**.

> [!NOTE]
> Se você precisar toorun mais de hello (20) o número de trabalhos, no portal de saudação padrão clique **ajuda + suporte** toosubmit uma solicitação de suporte. número de saudação de trabalhos que podem ser executadas simultaneamente em sua conta da análise Data Lake pode ser aumentado.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>Quanto tempo tookeep metadados de trabalho e recursos 
Quando os usuários executam trabalhos de U-SQL, Olá serviço de análise Data Lake retém todos os arquivos relacionados. Arquivos relacionados incluem script hello U-SQL, arquivos DLL Olá referenciados no script hello U-SQL, recursos compilados e estatísticas. arquivos de saudação estão na pasta de /system/ de saudação da conta de armazenamento do Azure Data Lake saudação padrão. Esta política controla por quanto tempo esses recursos são armazenados antes de serem excluídos automaticamente (o padrão de saudação é de 30 dias). Você pode usar esses arquivos para depuração e ajuste de desempenho de trabalhos que você vai executar novamente no futuro de saudação.

toochange quanto tookeep metadados de trabalho e recursos:

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Propriedades**.
3. Em **tooRetain dias consultas de trabalho**, mover o controle deslizante de saudação tooselect um valor ou insira o valor de saudação na caixa de texto de saudação.  
4. Clique em **Salvar**.

### <a name="job-level-policies"></a>Políticas no nível do trabalho
Com as políticas de nível de trabalho, você pode controlar Olá máximo Austrália e Olá prioridade máxima que podem ser definida por usuários individuais (ou membros de grupos de segurança específicos) em trabalhos que são enviados. Esse permite controlar Olá custos de usuários. Ele também permite que você pode ter efeito de saudação do controle que os trabalhos agendados em alta prioridade trabalhos de produção que são executados em Olá a mesma conta da análise Data Lake.

Análise data Lake tem duas políticas que podem ser definidas no nível de trabalho hello:

* **Limite de Austrália por trabalho**: os usuários podem enviar apenas trabalhos com número de toothis de Austrália. Por padrão, esse limite é Olá mesmo que o limite máximo de Austrália Olá para conta de saudação.
* **Prioridade**: os usuários somente podem enviar trabalhos que têm um valor de prioridade toothis menores ou iguais. Observe que um número maior significa uma prioridade mais baixa. Por padrão, isso é definido too1, que é a prioridade possível hello.

Há uma política padrão definida em cada conta. política padrão de saudação aplica tooall usuários da conta de saudação. Você pode definir políticas adicionais para usuários e grupos específicos. 

> [!NOTE]
> As políticas no nível da conta e no nível do trabalho aplicam-se ao mesmo tempo.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Adicionar uma política para um usuário ou grupo específico

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Propriedades**.
3. Em **limites de envio de trabalho**, clique em Olá **adicionar política** botão. Em seguida, selecione ou insira Olá configurações a seguir:
    1. **Nome da política de computação**: insira um nome de política, tooremind você finalidade de saudação da política de saudação.
    2. **Selecione o usuário ou grupo**: Selecionar usuário hello ou grupo essa política se aplica.
    3. **Definir Olá trabalho Austrália limite**: limite de saudação Austrália definido que se aplica a toohello selecionado usuário ou grupo.
    4. **Definir Olá prioridade limite**: Definir limite de prioridade de saudação que se aplica a toohello selecionado usuário ou grupo.

4. Clique em **OK**.

5. Olá nova diretiva é listada no hello **padrão** política de tabela, em **limites de envio de trabalho**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Excluir ou editar uma política existente

1. No hello portal do Azure, vá tooyour conta de análise Data Lake.
2. Clique em **Propriedades**.
3. Em **limites de envio de trabalho**, localizar Olá política deseja tooedit.
4.  Olá toosee **excluir** e **editar** opções, na coluna mais à direita de saudação da tabela de saudação, clique em **...** .

### <a name="additional-resources-for-job-policies"></a>Recursos adicionais para políticas de trabalho
* [Postagem no blog de visão geral de política](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Postagem no blog de políticas no nível da conta](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Postagem no blog de políticas no nível do trabalho](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Próximas etapas

* [Visão geral do Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Introdução ao análise Data Lake usando Olá portal do Azure](data-lake-analytics-get-started-portal.md)
* [Gerenciar o Azure Data Lake Analytics usando o Azure PowerShell](data-lake-analytics-manage-use-powershell.md)

