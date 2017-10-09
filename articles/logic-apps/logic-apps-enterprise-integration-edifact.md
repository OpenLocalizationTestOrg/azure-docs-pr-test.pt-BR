---
title: "mensagens de aaaEDIFACT para a integração do enterprise B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Troca de mensagens EDIFACT no formato EDI para integração de empresas B2B com aplicativos lógicos do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Troca de mensagens EDIFACT para integração de empresas com aplicativos lógicos

Antes de trocar mensagens EDIFACT para aplicativos lógicos do Azure, você deve criar um contrato EDIFACT e armazenar esse contrato em sua conta de integração. Aqui estão as etapas de saudação para toocreate um contrato EDIFACT.

> [!NOTE]
> Esta página aborda os recursos EDIFACT de saudação para os aplicativos lógicos do Azure. Para obter mais informações, consulte [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma [conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) que já esteja definida e associada à sua assinatura do Azure  
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos em sua conta de integração

> [!NOTE]
> Quando você cria um contrato, o conteúdo de saudação em mensagens de saudação que receber ou enviar tooand do parceiro Olá deve corresponder ao tipo de contrato de saudação.

Depois de [criar uma conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) e [adicionar os parceiros](logic-apps-enterprise-integration-partners.md), você poderá criar um contrato EDIFACT executando as seguintes etapas:

## <a name="create-an-edifact-agreement"></a>Criar um contrato EDIFACT 

1.  Entrar toohello [portal do Azure](http://portal.azure.com "portal do Azure"). No menu à esquerda do hello, selecione **mais serviços**.

    > [!TIP]
    > Se você não vir **mais serviços**, você pode ter o menu de saudação tooexpand primeiro. Na parte superior de saudação do menu Olá recolhido, selecione **menu Mostrar**.

    ![No menu à esquerda, selecione "Mais serviços"](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. Na caixa de pesquisa hello, digite "integração" para o filtro. Na lista de resultados de saudação, selecione **contas de integração**.

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. Em Olá **contas de integração** folha que é aberta, conta de integração hello selecione onde você deseja que o contrato de saudação toocreate.
Caso não encontre nenhuma conta de integração, [crie uma primeiro](../logic-apps/logic-apps-enterprise-integration-accounts.md "O que é uma conta de integração?").  

    ![Selecione a conta de integração onde toocreate Olá contrato](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Escolha Olá **contratos** lado a lado. Se você não tiver um bloco de contratos, primeiro adicione o bloco de saudação.   

    ![Escolha o bloco de "Contratos"](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. Na folha de contratos de saudação é aberto, escolha **adicionar**.

    ![Escolha "Adicionar"](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. Em **Adicionar**, insira um **Nome** para o seu contrato. No **Tipo de contrato**, selecione **EDIFACT**. Selecione Olá **parceiro Host**, **identidade do Host**, **parceiro convidado**, e **convidado identidade** para o seu contrato.

    ![Fornecer detalhes de contrato](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Propriedade | Descrição |
    | --- | --- |
    | Nome |Nome do contrato de saudação |
    | Tipo de contrato | Deve ser EDIFACT |
    | Parceiro de Host |Um contrato precisa dos parceiros host e convidado. parceiro de host Olá representa a organização de saudação que configura o contrato de saudação. |
    | Identidade do Host |Um identificador para o parceiro de host Olá |
    | Parceiro Convidado |Um contrato precisa dos parceiros host e convidado. parceiro de convidado Olá representa a organização de saudação que está fazendo a empresa com o parceiro de host de saudação. |
    | Identidade do Convidado |Um identificador para o parceiro convidado de saudação |
    | Configurações de Recebimento |Essas propriedades se aplicam a tooall mensagens recebidas por um contrato. |
    | Configurações de Envio |Essas propriedades se aplicam a tooall mensagens enviadas por um contrato. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurar como seu contrato lida com mensagens recebidas

Agora que você definiu propriedades de contrato hello, você pode configurar como este contrato identifica e manipula mensagens de entrada recebidas de seu parceiro por meio deste contrato.

1.  Em **Adicionar**, selecione **Configurações de Recebimento**.
Configure essas propriedades com base no seu contrato de parceiro de saudação que troca mensagens com você. Para obter descrições de propriedade, consulte as tabelas de saudação nesta seção.

    As **configurações de recebimento** são organizadas nas seguintes seções: Identificadores, Confirmação, Esquemas, Envelopes, Números de controle, Validação e Configurações internas.

    ![Configure "Configurações de recebimento"](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Depois de terminar, defina toosave-se de que suas configurações, escolhendo **Okey**.

Agora, o contrato é toohandle pronto entrada mensagens em conformidade tooyour configurações selecionadas.

### <a name="identifiers"></a>Identificadores

| Propriedade | Descrição |
| --- | --- |
| UNB 6.1 (Senha de Referência do Destinatário) |Insira um valor alfanumérico entre 1 e 14 caracteres. |
| UNB 6.2 (Qualificador de Referência do Destinatário) |Insira um valor alfanumérico com no mínimo um caractere e no máximo dois caracteres. |

### <a name="acknowledgments"></a>Agradecimentos

| Propriedade | Descrição |
| --- | --- |
| Recebimento de Mensagem (CONTRL) |Selecione essa caixa de seleção tooreturn um emissor de intercâmbio toohello de confirmação técnica (CONTRL). confirmação de saudação é enviada toohello emissor de intercâmbio com base em hello configurações de envio para o contrato de saudação. |
| Confirmação (CONTRL) |Selecione tooreturn essa caixa de seleção que uma confirmação da saudação de remetente de intercâmbio de toohello do reconhecimento de funcional (CONTRL) é enviada toohello emissor de intercâmbio com base em hello configurações de envio para o contrato de saudação. |

### <a name="schemas"></a>Esquemas

| Propriedade | Descrição |
| --- | --- |
| UNH2.1 (TIPO) |Selecione um tipo de conjunto de transação. |
| UNH2.2 (VERSÃO) |Insira o número de versão de mensagem de saudação. (No mínimo um caractere; no máximo três caracteres). |
| UNH2.3 (LIBERAÇÃO) |Insira o número de versão de mensagem de saudação. (No mínimo um caractere; no máximo três caracteres). |
| UNH2.5 (CÓDIGO ATRIBUÍDO ASSOCIADO) |Insira o código de saudação atribuído. (No máximo seis caracteres. Deve ser alfanuméricos). |
| UNG 2.1 (ID DE REMETENTE DO APLICATIVO) |Insira um valor alfanumérico com no mínimo um caractere e no máximo 35 caracteres. |
| UNG 2.2 (QUALIFICADOR DE CÓDIGO DO APLICATIVO REMETENTE) |Insira um valor alfanumérico, com no máximo quatro caracteres. |
| Esquema |Selecione Olá carregado anteriormente esquema desejado toouse de sua conta de integração associado. |

### <a name="control-numbers"></a>Números de Controle
| Propriedade | Descrição |
| --- | --- |
| Recusar duplicatas de Números de Controle de Intercâmbio |intercâmbios de duplicata tooblock, selecione essa propriedade. Se selecionada, a saudação EDIFACT decodificar ação verifica que o número de controle de intercâmbio hello (UNB5) para intercâmbio de saudação recebido não coincide com um número de controle de intercâmbio processada anteriormente. Se uma correspondência for detectada, o intercâmbio de saudação não foi processado. |
| Verificar UNB5 duplicado a cada (dias) |Se você escolheu toodisallow números de controle de intercâmbio duplicados, você pode especificar o número de saudação de dias ao check-tooperform hello, fornecendo um valor apropriado Olá para essa configuração. |
| Recusar duplicatas de Números de controle de grupo |tooblock intercâmbios com números de controle de grupo duplicados (UNG5), selecione essa propriedade. |
| Recusar duplicatas de Números de controle de Conjuntos de transações |tooblock intercâmbios com transação duplicada conjunto de números de controle (UNH1), selecione essa propriedade. |
| Número de controle da confirmação EDIFACT |conjunto de transação de saudação de toodesignate números de referência para uso em uma confirmação, digite um valor de prefixo hello, um intervalo de números de referência e um sufixo. |

### <a name="validations"></a>Validações

Quando você conclui cada linha de validação, outra é adicionada automaticamente. Se você não especificar todas as regras, validação usa a linha de "Padrão" de saudação.

| Propriedade | Descrição |
| --- | --- |
| Tipo de Mensagem |Selecione o tipo de mensagem EDI hello. |
| Validação de EDI |Execute a validação de EDI nos tipos de dados, conforme definido pelo esquema Olá EDI propriedades, restrições de comprimento, elementos de dados vazios e separadores à direita. |
| Validação Estendida |Se o tipo de dados Olá não for EDI, a validação será na exigência de elementos de dados de saudação e permitido a repetição, enumerações e dados de validação de comprimento de elemento (Mín/Máx). |
| Permitir Zeros à Esquerda/Direita |Retém zeros à esquerda ou à direita adicionais e caracteres de espaço. Não remova esses caracteres. |
| Cortar Zeros à Esquerda/Direita |Remove zeros à esquerda ou à direita e caracteres de espaço. |
| Política de Separador à Direita |Gera separadores à direita. <p>Selecione **não permitido** delimitadores à direita tooprohibit e separadores em Olá receberam intercâmbio. Se o intercâmbio de saudação tiver delimitadores e separadores à direita, intercâmbio de saudação é declarado não válido. <p>Selecione **opcional** tooaccept intercâmbios com ou sem delimitadores e separadores à direita. <p>Selecione **obrigatório** ao intercâmbio Olá recebida deve ter delimitadores e separadores à direita. |

### <a name="internal-settings"></a>Configurações Internas

| Propriedade | Descrição |
| --- | --- |
| Criar marcas XML vazias se forem permitidos separadores à direita |Selecione emissor de intercâmbio essa caixa de seleção toohave Olá incluem vazio marcas XML para separadores à direita. |
| Dividir Intercâmbio como conjuntos de transação – suspender conjuntos de transação com erro|Analisa cada transação definida em um intercâmbio dentro de um documento XML separado aplicando o conjunto de transação de toohello Olá envelope apropriado. Suspenda somente conjuntos de transações Olá com falha na validação. |
| Dividir Intercâmbio como conjuntos de transação – suspender intercâmbio com erro|Analisa cada conjunto de transações em um intercâmbio dentro de um documento XML separado aplicando o envelope apropriado hello. Suspenda intercâmbio inteiro hello quando um ou mais conjuntos de transação no intercâmbio de saudação falharem na validação. | 
| Preservar Intercâmbio – suspender conjuntos transação com erro |Deixa o intercâmbio de saudação intacto, cria um documento XML para o intercâmbio em lote inteiro de saudação. Somente conjuntos de transações Olá com falha na validação de suspender, enquanto continua tooprocess define todas as outras transações. |
| Preservar Intercâmbio – suspender intercâmbio com erro |Deixa o intercâmbio de saudação intacto, cria um documento XML para o intercâmbio em lote inteiro de saudação. Suspenda intercâmbio inteiro hello quando um ou mais conjuntos de transação no intercâmbio de saudação falharem na validação. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurar como seu contrato envia mensagens

Você pode configurar como este contrato identifica e manipula mensagens de saída que você enviar tooyour parceiros por meio deste contrato.

1.  Em **Adicionar**, selecione **Configurações de Envio**.
Configure essas propriedades com base no seu contrato com seu parceiro que troca mensagens com você. Para obter descrições de propriedade, consulte as tabelas de saudação nesta seção.

    **Configurações de envio** é organizado nas seguintes seções: Identificadores, Confirmação, Esquemas, Envelopes, Conjuntos de caracteres e separadores, Números de controle e Validações.

    ![Configurar "Configurações de Envio"](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Depois de terminar, defina toosave-se de que suas configurações, escolhendo **Okey**.

Agora o contrato é toohandle pronto mensagens que estão de acordo com as configurações de tooyour selecionado de saída.

### <a name="identifiers"></a>Identificadores

| Propriedade | Descrição |
| --- | --- |
| UNB1.2 (Versão de sintaxe) |Selecione um valor entre **1** e **4**. |
| UNB 2.3 (Endereço de Roteamento do Remetente Inverso) |Insira um valor alfanumérico com no mínimo um caractere e no máximo 14 caracteres. |
| UNB3.3 (Endereço de Roteamento do Destinatário Inverso) |Insira um valor alfanumérico com no mínimo um caractere e no máximo 14 caracteres. |
| UNB 6.1 (Senha de Referência do Destinatário) |Insira um valor alfanumérico com no mínimo um e no máximo 14 caracteres. |
| UNB 6.2 (Qualificador de Referência do Destinatário) |Insira um valor alfanumérico com no mínimo um caractere e no máximo dois caracteres. |
| UNB7 (ID de Referência do Aplicativo) |Insira um valor alfanumérico com no mínimo um caractere e no máximo 14 caracteres |

### <a name="acknowledgment"></a>Confirmação
| Propriedade | Descrição |
| --- | --- |
| Recebimento de Mensagem (CONTRL) |Selecione essa caixa de seleção se o parceiro de saudação hospedado espera tooreceive uma confirmação técnica (CONTRL). Essa configuração especifica o parceiro Olá hospedado, que está enviando a mensagem de saudação, solicita uma confirmação do parceiro convidado de saudação. |
| Confirmação (CONTRL) |Selecione essa caixa de seleção se o parceiro de saudação hospedado espera tooreceive uma confirmação funcional (CONTRL). Essa configuração especifica o parceiro Olá hospedado, que está enviando a mensagem de saudação, solicita uma confirmação do parceiro convidado de saudação. |
| Gerar loop SG1/SG4 para conjuntos de transação aceitos |Se você escolher toorequest uma confirmação funcional, selecione a caixa de seleção tooforce geração de loops SG1/SG4 em confirmações CONTRL funcionais para conjuntos de transação aceitos. |

### <a name="schemas"></a>Esquemas
| Propriedade | Descrição |
| --- | --- |
| UNH2.1 (TIPO) |Selecione um tipo de conjunto de transação. |
| UNH2.2 (VERSÃO) |Insira o número de versão de mensagem de saudação. |
| UNH2.3 (LIBERAÇÃO) |Insira o número de versão de mensagem de saudação. |
| Esquema |Selecione Olá esquema toouse. Esquema estão localizados na sua conta de integração. tooaccess os esquemas, primeiro vincular seu aplicativo de conta tooyour lógica da integração. |

### <a name="envelopes"></a>Envelopes
| Propriedade | Descrição |
| --- | --- |
| UNB8 (Código de Prioridade de Processamento) |Insira um valor alfabético que não tenha mais de um caractere de comprimento. |
| UNB10 (Contrato de Comunicação) |Insira um valor alfanumérico com no mínimo um caractere e no máximo 40 caracteres. |
| UNB11 (Indicador de Teste) |Selecione tooindicate essa caixa de seleção que Olá intercâmbio gerado é dados de teste |
| Aplicar o Segmento UNA (Aviso de Cadeia de Caracteres de Serviço) |Selecione toogenerate essa caixa de seleção um segmento UNA para toobe de intercâmbio de saudação enviada. |
| Aplicar os segmentos UNG (Cabeçalho de Grupo de Função) |Selecione este toocreate de caixa de seleção Agrupar segmentos no cabeçalho de grupo funcional Olá Olá mensagens enviadas toohello convidado parceiro. Olá valores a seguir são usadas toocreate Olá UNG segmentos: <p>Para **UNG1**, insira um valor alfanumérico com no mínimo um e no máximo seis caracteres. <p>Para **UNG2.1**, insira um valor alfanumérico com no mínimo um e no máximo 35 caracteres. <p>Para **UNG2.2**, insira um valor alfanumérico, com no máximo quatro caracteres. <p>Para **UNG3.1**, insira um valor alfanumérico com no mínimo um e no máximo 35 caracteres. <p>Para **UNG3.2**, insira um valor alfanumérico, com no máximo quatro caracteres. <p>Para **UNG6**, insira um valor alfanumérico com no mínimo um e no máximo três caracteres. <p>Para **UNG7.1**, insira um valor alfanumérico com no mínimo um e no máximo três caracteres. <p>Para **UNG7.2**, insira um valor alfanumérico com no mínimo um e no máximo três caracteres. <p>Para **UNG7.3**, insira um valor alfanumérico com no mínimo um e no máximo seis caracteres. <p>Para **UNG8**, insira um valor alfanumérico com no mínimo um e no máximo 14 caracteres. |

### <a name="character-sets-and-separators"></a>Conjuntos de Caracteres e Separadores

Diferente do conjunto de caracteres hello, você pode inserir um conjunto diferente de delimitadores toobe usado para cada tipo de mensagem. Se um conjunto de caracteres não for especificado para um determinado esquema de mensagem, conjunto de caracteres saudação padrão é usado.

| Propriedade | Descrição |
| --- | --- |
| UNB1.1 (Identificador do Sistema) |Selecione Olá caracteres EDIFACT definido toobe aplicado Olá intercâmbio de saída. |
| Esquema |Selecione um esquema da lista suspensa de saudação. Depois de concluir cada linha, uma nova linha é adicionada automaticamente. Para o esquema selecionado do hello, separadores de saudação selecione definido que você deseja toouse, com base em Olá descrições de separador a seguir. |
| Tipo de entrada |Selecione um tipo de entrada na lista suspensa de saudação. |
| Separador de componente |elementos de dados compostos de tooseparate, insira um único caractere. |
| Separador de elemento de dados |tooseparate elementos de dados simples em elementos de dados compostos, insira um único caractere. |
| Terminador de segmento |fim de saudação tooindicate de um segmento EDI, insira um único caractere. |
| Suffix |Selecione o caractere de saudação que é usado com o identificador de segmento de saudação. Se você designa um sufixo, Olá elemento de dados de terminador de segmento pode ser vazio. Se o terminador de segmento de saudação for deixado vazio, será necessário designar um sufixo. |

### <a name="control-numbers"></a>Números de Controle
| Propriedade | Descrição |
| --- | --- |
| UNB5 (Número de Controle de Intercâmbio) |Insira um prefixo, um intervalo de valores para o número de controle de intercâmbio de saudação e um sufixo. Esses valores são usado toogenerate um intercâmbio de saída. prefixo hello e sufixo são opcionais, enquanto o número de controle de saudação é necessário. número de controle de saudação é incrementado para cada nova mensagem; saudação de prefixo e sufixo permanecem Olá mesmo. |
| UNG5 (Número de Controle de Grupo) |Insira um prefixo, um intervalo de valores para o número de controle de intercâmbio de saudação e um sufixo. Esses valores são usados toogenerate número de controle de grupo de saudação. prefixo hello e sufixo são opcionais, enquanto o número de controle de saudação é necessário. número de controle de saudação é incrementado para cada nova mensagem até que o valor máximo de saudação é atingido. saudação de prefixo e sufixo permanecem Olá mesmo. |
| UNH1 (Número de Referência do Cabeçalho da Mensagem) |Insira um prefixo, um intervalo de valores para o número de controle de intercâmbio de saudação e um sufixo. Esses valores são usados toogenerate número de referência de cabeçalho da mensagem hello. prefixo hello e sufixo são opcionais, enquanto o número de referência de saudação é necessário. número de referência de saudação é incrementado para cada nova mensagem; saudação de prefixo e sufixo permanecem Olá mesmo. |

### <a name="validations"></a>Validações

Quando você conclui cada linha de validação, outra é adicionada automaticamente. Se você não especificar todas as regras, validação usa a linha de "Padrão" de saudação.

| Propriedade | Descrição |
| --- | --- |
| Tipo de Mensagem |Selecione o tipo de mensagem EDI hello. |
| Validação de EDI |Execute a validação de EDI nos tipos de dados conforme definidos pelas propriedades EDI de saudação do esquema hello, restrições de comprimento, elementos de dados vazios e separadores à direita. |
| Validação Estendida |Se o tipo de dados Olá não for EDI, a validação será na exigência de elementos de dados de saudação e permitido a repetição, enumerações e dados de validação de comprimento de elemento (Mín/Máx). |
| Permitir Zeros à Esquerda/Direita |Retém zeros à esquerda ou à direita adicionais e caracteres de espaço. Não remova esses caracteres. |
| Cortar Zeros à Esquerda/Direita |Remove zeros à esquerda ou à direita adicionais. |
| Política de Separador à Direita |Gera separadores à direita. <p>Selecione **não permitido** delimitadores à direita tooprohibit e separadores em Olá enviados intercâmbio. Se o intercâmbio de saudação tiver delimitadores e separadores à direita, intercâmbio de saudação é declarado não válido. <p>Selecione **opcional** toosend intercâmbios com ou sem delimitadores e separadores à direita. <p>Selecione **obrigatório** se o intercâmbio de saudação enviados deve ter delimitadores e separadores à direita. |

## <a name="find-your-created-agreement"></a>Como localizar seu contrato criado

1.  Depois de terminar de definir todas as suas propriedades de contrato, em Olá **adicionar** folha, escolha **Okey** toofinish criando seu contrato e retorno tooyour folha de conta de integração.

    Agora seu contrato recém-adicionado é exibido na lista **Contratos**.

2.  Você também pode visualizar seus contratos na visão geral de conta de integração. Na folha sua conta de integração, escolha **visão geral**, em seguida, selecione Olá **contratos** lado a lado. 

    ![Escolha "Contratos" bloco tooview todos os contratos](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Exibir o arquivo do Swagger
detalhes de Swagger tooview Olá para o conector EDIFACT hello, consulte [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>Saiba mais
* [Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  

