---
title: "mensagens de aaaX12 para a integração do enterprise B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Troca de mensagens X12 no formato EDI para integração de empresas B2B com aplicativos lógicos do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Troca de mensagens X12 para integração de empresas com aplicativos lógicos

Antes de trocar mensagens X12 para aplicativos lógicos do Azure, você deve criar um contrato X12 e armazenar esse contrato na sua conta de integração. Aqui estão as etapas de saudação para toocreate um X12 contrato.

> [!NOTE]
> Esta página aborda os recursos de saudação X12 para os aplicativos lógicos do Azure. Para obter mais informações, confira [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma [conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) que já esteja definida e associada à sua assinatura do Azure
* Pelo menos dois [parceiros](../logic-apps/logic-apps-enterprise-integration-partners.md) que são definidos em sua conta de integração e configurado com o identificador de saudação X12 em **identidades comerciais**    
* Necessário [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) para carregar tooyour [conta integration](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Depois que você [criar uma conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md), [adicionar parceiros](logic-apps-enterprise-integration-partners.md)e ter um [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) que você deseja toouse, você pode criar um X12 contrato seguindo estas etapas.

## <a name="create-an-x12-agreement"></a>Criar um contrato X12

1.  Entrar toohello [portal do Azure](http://portal.azure.com "portal do Azure"). No menu à esquerda do hello, selecione **mais serviços**. 

    > [!TIP]
    > Se você não vir **mais serviços**, você pode ter o menu de saudação tooexpand primeiro. Na parte superior de saudação do menu Olá recolhido, selecione **menu Mostrar**.

    ![No menu à esquerda, selecione "Mais serviços"](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  Na caixa de pesquisa hello, digite "integração" como filtro. Na lista de resultados de saudação, selecione **contas de integração**.  

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. Em Olá **contas de integração** folha que é aberta, conta de integração hello selecione onde você deseja que o contrato de saudação tooadd.
Caso não encontre nenhuma conta de integração, [crie uma primeiro](../logic-apps/logic-apps-enterprise-integration-accounts.md "O que é uma conta de integração?").

    ![Selecione a conta de integração onde toocreate Olá contrato](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Selecione **visão geral**, em seguida, selecione Olá **contratos** lado a lado. Se você não tiver um bloco de contratos, primeiro adicione o bloco de saudação. 

    ![Escolha o bloco de "Contratos"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Na folha de contratos de saudação é aberto, escolha **adicionar**.

    ![Escolha "Adicionar"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. Em **Adicionar**, insira um **Nome** para o seu contrato. Para o tipo de contrato hello, selecione **X12**. Selecione Olá **parceiro Host**, **identidade do Host**, **parceiro convidado**, e **convidado identidade** para o seu contrato. Para obter detalhes de propriedade, consulte a tabela de saudação nesta etapa.

    ![Fornecer detalhes de contrato](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Propriedade | Descrição |
    | --- | --- |
    | Nome |Nome do contrato de saudação |
    | Tipo de contrato | Deve ser X12 |
    | Parceiro de Host |Um contrato precisa dos parceiros host e convidado. parceiro de host Olá representa a organização de saudação que configura o contrato de saudação. |
    | Identidade do Host |Um identificador para o parceiro de host Olá |
    | Parceiro Convidado |Um contrato precisa dos parceiros host e convidado. parceiro de convidado Olá representa a organização de saudação que está fazendo a empresa com o parceiro de host de saudação. |
    | Identidade do Convidado |Um identificador para o parceiro convidado de saudação |
    | Configurações de Recebimento |Essas propriedades se aplicam a tooall mensagens recebidas por um contrato. |
    | Configurações de Envio |Essas propriedades se aplicam a tooall mensagens enviadas por um contrato. |  

  > [!NOTE]
  > Resolução de X12 contrato depende de correspondência de qualificador de remetente hello e identificador, qualificador de saudação do receptor e identificador definido no parceiro de saudação e mensagem de entrada. Se esses valores são alterados para seu parceiro, atualize contrato Olá muito.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurar como seu contrato lida com mensagens recebidas

Agora que você definiu propriedades de contrato hello, você pode configurar como este contrato identifica e manipula mensagens de entrada recebidas de seu parceiro por meio deste contrato.

1.  Em **Adicionar**, selecione **Configurações de Recebimento**.
Configure essas propriedades com base no seu contrato de parceiro de saudação que troca mensagens com você. Para obter descrições de propriedade, consulte as tabelas de saudação nesta seção.

    As **Configurações de recebimento** são organizadas nas seguintes seções: Identificadores, Confirmação, Esquemas, Envelopes, Números de controle, Validações e Configurações internas.

2. Depois de terminar, defina toosave-se de que suas configurações, escolhendo **Okey**.

Agora, o contrato é toohandle pronto entrada mensagens em conformidade tooyour configurações selecionadas.

### <a name="identifiers"></a>Identificadores

![Definir propriedades do identificador](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Propriedade | Descrição |
| --- | --- |
| ISA1 (Qualificador de Autorização) |Selecione o valor do qualificador de autorização de saudação da lista suspensa de saudação. |
| ISA2 |Opcional. Insira o valor de Informações de autorização. Se o valor de saudação inserido para ISA1 for diferente de 00, insira um mínimo de um caractere alfanumérico e um máximo de 10. |
| ISA3 (Qualificador de Segurança) |Selecione o valor do qualificador de segurança de saudação da lista suspensa de saudação. |
| ISA4 |Opcional. Insira o valor de informações de segurança de saudação. Se o valor de saudação inserido para ISA3 for diferente de 00, insira um mínimo de um caractere alfanumérico e um máximo de 10. |

### <a name="acknowledgment"></a>Confirmação

![Definir propriedades de confirmação](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Propriedade | Descrição |
| --- | --- |
| TA1 esperado |Retorna um emissor de intercâmbio toohello confirmação técnica |
| FA esperado |Retorna um emissor de intercâmbio toohello confirmação funcional. Em seguida, selecione se deseja as confirmações Olá 997 ou 999, com base na versão do esquema Olá |
| Incluir Loop AK2/IK2 |Habilita a geração de loops AK2 em confirmações funcionais para conjuntos de transação aceitos |

### <a name="schemas"></a>Esquemas

Escolha um esquema para cada tipo de transação (ST1) e o Aplicativo de remetente (GS2). Olá receber pipeline desmonta a mensagem de entrada hello correspondendo os valores de saudação de ST1 e GS2 na mensagem de entrada hello com hello valores definido aqui e o esquema de saudação da mensagem de entrada hello com esquema Olá definido aqui.

![Selecione um esquema](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Propriedade | Descrição |
| --- | --- |
| Versão |Selecione a versão de hello X12 |
| Tipo de Transação (ST01) |Selecione o tipo de transação Olá |
| Aplicativo do Remetente (GS02) |Selecione o aplicativo de remetente hello |
| Esquema |Selecione arquivo de esquema de saudação toouse desejado. Esquemas são adicionados tooyour conta de integração. |

> [!NOTE]
> Configurar Olá necessário [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) que é carregado tooyour [conta integration](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Envelopes

![Especifique o separador de saudação em um conjunto de transação: escolha identificador padrão ou separador de repetição](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Propriedade | Descrição |
| --- | --- |
| Uso de ISA11 |Especifica um conjunto de transações Olá separador toouse: <p>Selecione **identificador padrão** toouse um ponto (.) para notação decimal, em vez de notação decimal de saudação do documento de entrada hello em Olá EDI pipeline de recebimento. <p>Selecione **separador de repetição** toospecify separador de saudação para ocorrências repetidas de um elemento de dados simples ou uma estrutura de dados repetidos. Por exemplo, geralmente hello circunflexo (^) é usado como separador de repetição de saudação. Para esquemas HIPPA, você só pode usar a intercalação de saudação. |

### <a name="control-numbers"></a>Números de Controle

![Selecione como toohandle controlar duplicatas de número](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Propriedade | Descrição |
| --- | --- |
| Recusar duplicatas de Números de Controle de Intercâmbio |Bloqueia o intercâmbio de duplicatas. Verifica o número de controle de intercâmbio hello (ISA13) para o número de controle de intercâmbio de saudação recebida. Se uma correspondência for detectada, Olá receber pipeline não processará o intercâmbio de saudação. Você pode especificar o número de saudação de dias para executar a verificação de hello, fornecendo um valor para *verificar isa13 duplicado a cada (dias)*. |
| Recusar duplicatas de Números de controle de grupo |Bloqueia intercâmbios com números de controle de grupo de duplicatas. |
| Recusar duplicatas de Números de controle de Conjuntos de transações |Bloqueia intercâmbios com números de controle de conjunto de transações de duplicatas. |

### <a name="validations"></a>Validações

![Definir propriedades de validação das mensagens recebidas](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Quando você conclui cada linha de validação, outra é adicionada automaticamente. Se você não especificar todas as regras, validação usa a linha de "Padrão" de saudação.

| Propriedade | Descrição |
| --- | --- |
| Tipo de Mensagem |Selecione o tipo de mensagem EDI hello. |
| Validação de EDI |Execute a validação de EDI nos tipos de dados, conforme definido pelo esquema Olá EDI propriedades, restrições de comprimento, elementos de dados vazios e separadores à direita. |
| Validação Estendida |Se o tipo de dados Olá não for EDI, a validação será na exigência de elementos de dados de saudação e permitido a repetição, enumerações e dados de validação de comprimento de elemento (Mín/Máx). |
| Permitir Zeros à Esquerda/Direita |Retém zeros à esquerda ou à direita adicionais e caracteres de espaço. Não remova esses caracteres. |
| Cortar Zeros à Esquerda/Direita |Remove zeros à esquerda ou à direita e caracteres de espaço. |
| Política de Separador à Direita |Gera separadores à direita. <p>Selecione **não permitido** delimitadores à direita tooprohibit e separadores em Olá receberam intercâmbio. Se o intercâmbio de saudação tiver delimitadores e separadores à direita, intercâmbio de saudação é declarado não válido. <p>Selecione **opcional** tooaccept intercâmbios com ou sem delimitadores e separadores à direita. <p>Selecione **obrigatório** ao intercâmbio Olá deve ter delimitadores e separadores à direita. |

### <a name="internal-settings"></a>Configurações Internas

![Selecione Configurações internas](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Propriedade | Descrição |
| --- | --- |
| Converter o formato decimal implícito "Nn" tooa base 10 valor numérico |Converte um número EDI que é especificado com o formato de saudação "Nn" em um valor numérico de base 10 |
| Criar marcas XML vazias se forem permitidos separadores à direita |Selecione emissor de intercâmbio essa caixa de seleção toohave Olá incluem vazio marcas XML para separadores à direita. |
| Dividir Intercâmbio como conjuntos de transação – suspender conjuntos de transação com erro|Analisa cada transação definida em um intercâmbio dentro de um documento XML separado aplicando o conjunto de transação de toohello Olá envelope apropriado. Suspende somente as transações de saudação onde Olá falhará. |
| Dividir Intercâmbio como conjuntos de transação – suspender intercâmbio com erro|Analisa cada conjunto de transações em um intercâmbio dentro de um documento XML separado aplicando o envelope apropriado hello. Suspende o intercâmbio inteiro quando um ou mais conjuntos de transação no intercâmbio de saudação falharem na validação. | 
| Preservar Intercâmbio – suspender conjuntos transação com erro |Deixa o intercâmbio de saudação intacto, cria um documento XML para o intercâmbio em lote inteiro de saudação. Suspende somente conjuntos de transações Olá que falharem na validação, enquanto continua tooprocess todos os outros conjuntos de transação. |
| Preservar Intercâmbio – suspender intercâmbio com erro |Deixa o intercâmbio de saudação intacto, cria um documento XML para o intercâmbio em lote inteiro de saudação. Suspende o intercâmbio inteiro hello quando um ou mais conjuntos de transação no intercâmbio de saudação falharem na validação. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurar como seu contrato envia mensagens

Você pode configurar como este contrato identifica e manipula mensagens de saída que você enviar tooyour parceiro por meio deste contrato.

1.  Em **Adicionar**, selecione **Configurações de Envio**.
Configure essas propriedades com base no seu contrato com seu parceiro que troca mensagens com você. Para obter descrições de propriedade, consulte as tabelas de saudação nesta seção.

    **Configurações de envio** é organizado nas seguintes seções: Identificadores, Confirmação, Esquemas, Envelopes, Conjuntos de caracteres e separadores, Números de controle e Validação.

2. Depois de terminar, defina toosave-se de que suas configurações, escolhendo **Okey**.

Agora o contrato é toohandle pronto mensagens que estão de acordo com as configurações de tooyour selecionado de saída.

### <a name="identifiers"></a>Identificadores

![Definir propriedades do identificador](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Propriedade | Descrição |
| --- | --- |
| Qualificador de Autorização (ISA1) |Selecione o valor do qualificador de autorização de saudação da lista suspensa de saudação. |
| ISA2 |Insira o valor de Informações de autorização. Se esse valor é diferente de 00, insira no mínimo um caractere alfanumérico e no máximo 10. |
| Qualificador de segurança (ISA3) |Selecione o valor do qualificador de segurança de saudação da lista suspensa de saudação. |
| ISA4 |Insira o valor de informações de segurança de saudação. Se esse valor for diferente de 00, Olá valor (ISA4) caixa de texto, insira um mínimo de um valor alfanumérico e um máximo de 10. |

### <a name="acknowledgment"></a>Confirmação

![Definir propriedades de confirmação](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Propriedade | Descrição |
| --- | --- |
| TA1 esperado |Retorne um emissor de intercâmbio toohello confirmação técnica (TA1). Essa configuração especifica o parceiro host Olá que está enviando solicitações de mensagem de saudação uma confirmação do parceiro de convidado de saudação no contrato de saudação. Essas confirmações são esperadas pelo parceiro de host de saudação com base nas configurações de recebimento de saudação do contrato de saudação. |
| FA esperado |Retorne um emissor de intercâmbio toohello confirmação funcional (FA). Selecione se deseja que as confirmações de saudação 997 ou 999, com base nas versões de esquema de saudação com que você está trabalhando. Essas confirmações são esperadas pelo parceiro de host de saudação com base nas configurações de recebimento de saudação do contrato de saudação. |
| Versão de FA |Selecione a versão Olá FA |

### <a name="schemas"></a>Esquemas

![Selecione um esquema toouse](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Propriedade | Descrição |
| --- | --- |
| Versão |Selecione a versão de hello X12 |
| Tipo de Transação (ST01) |Selecione o tipo de transação Olá |
| Esquema |Selecione Olá esquema toouse. Esquema estão localizados na sua conta de integração. Se você selecionar o esquema pela primeira vez, ele configurará automaticamente o tipo de transação e a versão  |

> [!NOTE]
> Configurar Olá necessário [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) que é carregado tooyour [conta integration](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Envelopes

![Especifique o separador de saudação em um conjunto de transação: escolha identificador padrão ou separador de repetição](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Propriedade | Descrição |
| --- | --- |
| Uso de ISA11 |Especifica um conjunto de transações Olá separador toouse: <p>Selecione **identificador padrão** toouse um ponto (.) para notação decimal, em vez de notação decimal de saudação do documento de entrada hello em Olá EDI pipeline de recebimento. <p>Selecione **separador de repetição** toospecify separador de saudação para ocorrências repetidas de um elemento de dados simples ou uma estrutura de dados repetidos. Por exemplo, geralmente hello circunflexo (^) é usado como separador de repetição de saudação. Para esquemas HIPPA, você só pode usar a intercalação de saudação. |

### <a name="control-numbers"></a>Números de Controle

![Especifique as propriedades do número de controle](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Propriedade | Descrição |
| --- | --- |
| Número de Versão de Controle (ISA12) |Selecione a versão de saudação do saudação padrão X12 |
| Indicador de Uso (ISA15) |Selecione um contexto de um intercâmbio hello.  os valores Hello são informações de dados de produção, ou dados de teste |
| Esquema |Gera hello GS e ST segmentos para um intercâmbio X12 codificado que ele envia toohello Pipeline de envio |
| GS1 |Opcional, selecione um valor para o código funcional de saudação da lista suspensa de saudação |
| GS2 |Opcional, remetente do aplicativo |
| GS3 |Opcional, receptor do aplicativo |
| GS4 |Opcional, selecionar CCYYMMDD ou YYMMDD |
| GS5 |Opcional, selecionar HHMM, HHMMSS ou HHMMSSdd |
| GS7 |Opcional, selecione um valor para a agência responsável Olá da lista suspensa de saudação |
| GS8 |Opcional, versão do documento hello |
| Número de Controle de Intercâmbio (ISA13) |Necessário, insira um intervalo de valores para o número de controle de intercâmbio de saudação. Inserir um valor numérico entre 1 e 999999999 |
| Número de Controle de Grupo (GS06) |Necessário, insira um intervalo de números para número de controle de grupo hello. Inserir um valor numérico entre 1 e 999999999 |
| Número de Controle de Conjunto de Transações (ST02) |Necessário, insira um intervalo de números para Olá número de controle de conjunto de transação. Insira um valor numérico entre 1 e 999999999 |
| Prefixo |Opcional, designado para o intervalo de saudação de números de controle de conjunto de transação usados na confirmação. Insira um valor numérico para dois campos de saudação médios e um valor alfanumérico (se desejar) para campos de prefixo e sufixo hello. campos médios Olá são necessários e contêm Olá valores mínimo e máximo para o número de controle Olá |
| Suffix |Opcional, designado para o intervalo de saudação de números de controle de conjunto de transação usados em uma confirmação. Insira um valor numérico para dois campos de saudação médios e um valor alfanumérico (se desejar) para campos de prefixo e sufixo hello. campos médios Olá são necessários e contêm Olá valores mínimo e máximo para o número de controle Olá |

### <a name="character-sets-and-separators"></a>Conjuntos de Caracteres e Separadores

Diferente do conjunto de caracteres hello, você pode inserir um conjunto diferente de delimitadores para cada tipo de mensagem. Se não for especificado um conjunto de caracteres para um determinado esquema de mensagem, conjunto de caracteres saudação padrão é usado.

![Especifique os delimitadores para os tipos de mensagem](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Propriedade | Descrição |
| --- | --- |
| Toobe do conjunto de caracteres usado |Propriedades de saudação toovalidate, selecione Olá X12 conjunto de caracteres. Opções de saudação são básico, estendido e UTF8. |
| Esquema |Selecione um esquema da lista suspensa de saudação. Depois de concluir cada linha, uma nova linha é adicionada automaticamente. Para o esquema selecionado do hello, separadores de saudação selecione definido que você deseja toouse, com base em Olá descrições de separador a seguir. |
| Tipo de entrada |Selecione um tipo de entrada na lista suspensa de saudação. |
| Separador de componente |elementos de dados compostos de tooseparate, insira um único caractere. |
| Separador de elemento de dados |tooseparate elementos de dados simples em elementos de dados compostos, insira um único caractere. |
| Caractere de substituição |Insira um caractere de substituição usado para substituir todos os caracteres de separadores nos dados de carga Olá ao gerar a mensagem de saudação saída X12. |
| Terminador de segmento |fim de saudação tooindicate de um segmento EDI, insira um único caractere. |
| Suffix |Selecione o caractere de saudação que é usado com o identificador de segmento de saudação. Se você designa um sufixo, Olá elemento de dados de terminador de segmento pode ser vazio. Se o terminador de segmento de saudação for deixado vazio, será necessário designar um sufixo. |

> [!TIP]
> tooprovide valores de caractere especial, editar contrato hello como JSON e fornecem valor ASCII de saudação para caractere especial hello.

### <a name="validation"></a>Validação

![Definição de propriedades de validação para o envio de mensagens](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Quando você conclui cada linha de validação, outra é adicionada automaticamente. Se você não especificar todas as regras, validação usa a linha de "Padrão" de saudação.

| Propriedade | Descrição |
| --- | --- |
| Tipo de Mensagem |Selecione o tipo de mensagem EDI hello. |
| Validação de EDI |Execute a validação de EDI nos tipos de dados, conforme definido pelo esquema Olá EDI propriedades, restrições de comprimento, elementos de dados vazios e separadores à direita. |
| Validação Estendida |Se o tipo de dados Olá não for EDI, a validação será na exigência de elementos de dados de saudação e permitido a repetição, enumerações e dados de validação de comprimento de elemento (Mín/Máx). |
| Permitir Zeros à Esquerda/Direita |Retém zeros à esquerda ou à direita adicionais e caracteres de espaço. Não remova esses caracteres. |
| Cortar Zeros à Esquerda/Direita |Remove zeros à esquerda ou à direita adicionais. |
| Política de Separador à Direita |Gera separadores à direita. <p>Selecione **não permitido** delimitadores à direita tooprohibit e separadores em Olá enviados intercâmbio. Se o intercâmbio de saudação tiver delimitadores e separadores à direita, intercâmbio de saudação é declarado não válido. <p>Selecione **opcional** toosend intercâmbios com ou sem delimitadores e separadores à direita. <p>Selecione **obrigatório** se o intercâmbio de saudação enviados deve ter delimitadores e separadores à direita. |

## <a name="find-your-created-agreement"></a>Como localizar seu contrato criado

1.  Depois de terminar de definir todas as suas propriedades de contrato, em Olá **adicionar** folha, escolha **Okey** toofinish criando seu contrato e retorno tooyour folha de conta de integração.

    Agora seu contrato recém-adicionado é exibido na lista **Contratos**.

2.  Você também pode visualizar seus contratos na visão geral de conta de integração. Na folha sua conta de integração, escolha **visão geral**, em seguida, selecione Olá **contratos** lado a lado.

    ![Escolha "Contratos" bloco tooview todos os contratos](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/x12/). 

## <a name="learn-more"></a>Saiba mais
* [Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  

