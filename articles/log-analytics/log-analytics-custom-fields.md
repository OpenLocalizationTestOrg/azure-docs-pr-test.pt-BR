---
title: "campos de aaaCustom na análise de Log | Microsoft Docs"
description: "Olá recurso de campos personalizados da análise de Log permite que você toocreate seus próprios campos pesquisáveis de dados OMS que adicionar toohello propriedades de um registro coletado.  Este artigo descreve o processo de saudação toocreate um campo personalizado e fornece uma explicação detalhada com um evento de amostra."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Campos personalizados no Log Analytics
Olá **campos personalizados** recurso de análise de Log permite tooextend os registros existentes no repositório do OMS Olá adicionando seus próprios campos pesquisáveis.  Campos personalizados são populados automaticamente de dados extraídos de outras propriedades no hello mesmo registro.

![Visão geral dos campos personalizados](media/log-analytics-custom-fields/overview.png)

Por exemplo, o registro de exemplo hello abaixo tem dados úteis ocultos na descrição do evento hello.  A extração desses dados em propriedades separadas os torna disponíveis para ações como a classificação e a filtragem.

![Botão Pesquisar Log](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> Olá Preview, você é too100 limitado de campos personalizados em seu espaço de trabalho.  Esse limite será expandido quando essa funcionalidade atingir a disponibilidade geral.
> 
> 

## <a name="creating-a-custom-field"></a>Criando um campo personalizado
Quando você cria um campo personalizado, análise de Log deve compreender quais toopopulate de toouse dados seu valor.  Ele usa uma tecnologia da Microsoft Research, chamada flashextract, tooquickly identificar os dados.  Em vez de exigir tooprovide de instruções explícitas, análise de Log aprende sobre dados saudação deseja tooextract de exemplos que você fornecer.

Olá seções a seguir fornece procedimento Olá para criar um campo personalizado.  Olá final deste artigo é um passo a passo de uma extração de exemplo.

> [!NOTE]
> campo personalizado Olá é populado como registros correspondente Olá especificados critérios são adicionados toohello repositório de dados do OMS, portanto, ele só aparecerá em registros coletados após a criação do campo personalizado de saudação.  campo personalizado Olá não será adicionado toorecords que já estão no repositório de dados hello quando ele é criado.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Etapa 1 – identificar registros que terão o campo personalizado Olá
Olá primeira etapa é tooidentify registros de saudação que obterão o campo personalizado hello.  Iniciar com uma [pesquisa de log padrão](log-analytics-log-searches.md) e selecione um registro tooact como modelo de saudação que orientará a análise de Log do.  Quando você especificar que você vai tooextract dados em um campo personalizado, Olá **Assistente de extração de campo** é aberto em que você valida e refina os critérios de saudação.

1. Vá muito**pesquisa de Log** e usar um [consultar os registros de saudação tooretrieve](log-analytics-log-searches.md) que terão o campo personalizado hello.
2. Selecione um registro que a análise de Log usará tooact como um modelo para extração de campo personalizado de saudação de toopopulate de dados.  Você identificará os dados de saudação que você deseja tooextract deste registro e análise de Log usará informações toodetermine Olá lógica toopopulate Olá campo personalizado para todos os registros semelhantes.
3. Clique em Olá botão toohello esquerda de qualquer propriedade de texto de saudação registro e selecione **extrair campos de**.
4. Olá **Assistente de extração de campo é aberto**, e registro de saudação selecionado é exibido no hello **exemplo principal** coluna.  campo personalizado Olá será definido para os registros com hello mesmos valores nas propriedades de saudação que são selecionadas.  
5. Se a seleção de saudação não é exatamente o que você deseja, selecione critérios de saudação toonarrow campos adicionais.  Em ordem toochange Olá valores de campo para os critérios de hello, cancele e selecione outro registro corresponde aos critérios de saudação desejado.

### <a name="step-2---perform-initial-extract"></a>Etapa 2: Executar a extração inicial.
Depois de identificar registros Olá que terão o campo personalizado hello, você identificar dados Olá que você deseja tooextract.  Análise de log usará esse padrões semelhantes de tooidentify informações registros semelhantes.  Na etapa Olá depois disso você toovalidate capaz de resultados hello e fornecer mais detalhes para a análise de Log toouse em sua análise.

1. Realce o texto de saudação no registro de exemplo hello que você deseja que o campo personalizado de saudação toopopulate.  Em seguida, ser apresentados a você um tooprovide da caixa de diálogo um nome para Olá campo e tooperform Olá extração inicial.  Olá caracteres  **\_CF** serão acrescentados automaticamente.
2. Clique em **extrair** tooperform uma análise dos registros coletados.  
3. Olá **resumo** e **resultados da pesquisa** seções exibem os resultados de saudação de extração de saudação para que você possa inspecionar sua precisão.  **Resumo** exibe Olá critérios usados tooidentify registros e uma contagem para cada um dos valores de dados Olá identificados.  **Resultados da pesquisa** fornece uma lista detalhada dos registros Olá critérios de correspondência.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Etapa 3 – verificar a precisão da extração de saudação e criar campo personalizado
Após ter realizado a extração inicial hello, análise de Log exibirá seus resultados com base nos dados que já foram coletados.  Se Olá resultados parecem ser precisos, em seguida, você pode criar campo personalizado Olá sem trabalho adicional.  Caso contrário, você pode refinar os resultados de saudação para que a análise de Log possa melhorar sua lógica.

1. Se quaisquer valores na extração de saudação inicial não estiverem corretas, clique em Olá **editar** próximo registro de imprecisas tooan ícone e selecione **modificar esse Realce** na seleção de saudação do toomodify de ordem.
2. a entrada Hello está copiado toohello **exemplos adicionais** seção abaixo Olá **exemplo principal**.  Você pode ajustar o realce de saudação aqui toohelp análise de Log entender Olá seleção que deveria ter feito.
3. Clique em **extrair** toouse registra esse novo tooevaluate de informações todos Olá existente.  resultados de saudação podem ser modificados para registros que não sejam Olá uma recém-modificado baseada nessa nova inteligência.
4. Continue tooadd correções até que todos os registros no hello extrair corretamente identificam Olá dados toopopulate Olá novo campo personalizado.
5. Clique em **salvar extração** quando estiver satisfeito com os resultados de saudação.  campo personalizado Olá agora está definido, mas ele não será adicionado tooany registros ainda.
6. Espera para novos registros de correspondência Olá especificado critérios toobe coletados e depois execute novamente a pesquisa de log de saudação. Novos registros devem ter o campo personalizado hello.
7. Use saudação de campo personalizado como qualquer outra propriedade de registro.  Você pode usá-lo tooaggregate e agrupar dados e usá-lo tooproduce novas ideias.

## <a name="viewing-custom-fields"></a>Exibindo campos personalizados
Você pode exibir uma lista de todos os campos personalizados em seu grupo de gerenciamento do hello **configurações** lado a lado do painel do OMS hello.  Selecione **Dados** e **Campos personalizados** para obter uma lista de todos os campos personalizados no espaço de trabalho.  

![Campos Personalizados](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Removendo um campo personalizado
Há dois tooremove de maneiras de um campo personalizado.  Olá é primeiro hello **remover** opção para cada campo ao exibir a lista completa de saudação conforme descrito acima.  Olá, outro método é tooretrieve que um toohello de botão de saudação do registro e clique em à esquerda do campo hello.  menu de saudação terá um campo personalizado da opção tooremove hello.

## <a name="sample-walkthrough"></a>Passo a passo de exemplo
Olá seção a seguir apresenta um exemplo completo de como criar um campo personalizado.  Este exemplo extrai o nome do serviço Olá eventos do Windows que indicam um alteração de estado do serviço.  Isso depende de eventos criados pelo Gerenciador de controle de serviço no log do sistema Olá em computadores Windows.  Se você quiser toofollow neste exemplo, você deve ser [coletar eventos de informações de log do sistema Olá](log-analytics-data-sources-windows-events.md).

Podemos inserir Olá tooreturn de consulta a seguir todos os eventos do Gerenciador de controle do serviço que têm uma ID de evento de 7036, que é o evento Olá que indica que um serviço iniciando ou parando.

![Consultar](media/log-analytics-custom-fields/query.png)

Em seguida, selecionamos qualquer registro com a ID de Evento de 7036.

![Registro de origem](media/log-analytics-custom-fields/source-record.png)

Queremos que o nome do serviço Olá que aparece no hello **RenderedDescription** propriedades e selecione Olá botão Avançar toothis.

![Extrair campos](media/log-analytics-custom-fields/extract-fields.png)

Olá **Assistente de extração de campo** é aberto e Olá **EventLog** e **EventID** campos são selecionados na Olá **exemplo principal** coluna.  Isso indica que o campo personalizado Olá será definido para eventos de log do sistema Olá com uma ID de evento de 7036.  Isso é suficiente para que não seja necessário tooselect todos os outros campos.

![Main Example](media/log-analytics-custom-fields/main-example.png)

Podemos destacar o nome de saudação do serviço Olá Olá **RenderedDescription** propriedade e use **Service** tooidentify nome do serviço de saudação.  campo personalizado Olá será chamado **Service_CF**.

![Título do campo](media/log-analytics-custom-fields/field-title.png)

Podemos ver que o nome hello serviço é identificado corretamente para alguns registros, mas não para outras pessoas.   Olá **resultados da pesquisa** mostram que essa parte do nome Olá Olá **adaptador de desempenho WMI** não foi selecionada.  Olá **resumo** mostra que quatro registra com **DPRMA** serviço incluíram incorretamente uma palavra extra e dois registros identificados **instalador de módulos** em vez de **Instalador de módulos do Windows**.  

![Resultados da Pesquisa](media/log-analytics-custom-fields/search-results-01.png)

Vamos começar com hello **adaptador de desempenho WMI** registro.  Clicamos em seu ícone de edição e em **Modify this highlight**(Modificar esse realce).  

![Modificar o realce](media/log-analytics-custom-fields/modify-highlight.png)

Aumentaremos palavra de Olá Olá realce tooinclude **WMI** e execute novamente a extração de saudação.  

![Exemplo adicional](media/log-analytics-custom-fields/additional-example-01.png)

Podemos ver que Olá entradas para **adaptador de desempenho WMI** foram corrigidas, e a análise de Log também usou esse registros de saudação informações toocorrect para **instalador de módulos do Windows**.  Podemos ver na Olá **resumo** seção embora que **DPMRA** ainda não está sendo identificado corretamente.

![Resultados da Pesquisa](media/log-analytics-custom-fields/search-results-02.png)

Podemos rolar tooa registro com hello serviço DPMRA e usar Olá mesmo processo toocorrect registrar.

![Exemplo adicional](media/log-analytics-custom-fields/additional-example-02.png)

 Quando executamos a extração hello, podemos ver que todos os nossos resultados agora são precisos.

![Resultados da Pesquisa](media/log-analytics-custom-fields/search-results-03.png)

Podemos ver que **Service_CF** é criado, mas ainda não foi adicionado tooany registros.

![Contagem inicial](media/log-analytics-custom-fields/initial-count.png)

Depois de algum tempo para novos eventos são coletados, podemos ver que que Olá **Service_CF** campo agora está sendo adicionado toorecords que corresponde aos nossos critérios.

![Resultados finais](media/log-analytics-custom-fields/final-results.png)

Estamos agora pode usar o campo personalizado de saudação como qualquer outra propriedade de registro.  tooillustrate isso, podemos criar uma consulta que agrupa pelo novo de saudação **Service_CF** tooinspect campo quais serviços estão hello mais ativo.

![Agrupar por consulta](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) toobuild consultas usando campos personalizados para os critérios.
* Monitorar [arquivos de log personalizados](log-analytics-data-sources-custom-logs.md) que você analisa usando campos personalizados.

