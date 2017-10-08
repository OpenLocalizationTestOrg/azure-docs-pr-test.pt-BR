---
title: "Sincronização do Azure AD Connect: Compreendendo a arquitetura de saudação | Microsoft Docs"
description: "Este tópico descreve a arquitetura de saudação de sincronização do Azure AD Connect e explica Olá termos usados."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Sincronização do Azure AD Connect: Compreendendo a arquitetura de saudação
Este tópico aborda a arquitetura básica Olá para sincronização do Azure AD Connect. Em muitos aspectos, é semelhante predecessores tooits MIIS 2003, 2007 ILM e FIM 2010. Sincronização do Azure AD Connect é a evolução de saudação dessas tecnologias. Se você estiver familiarizado com qualquer uma dessas tecnologias anteriores, o conteúdo de saudação deste tópico será familiar tooyou também. Se você for novo toosynchronization, este tópico é para você. No entanto não é detalhes requisito tooknow Olá desse toobe tópico bem-sucedida fazer personalizações tooAzure AD Connect sincronização (mecanismo de sincronização chamado neste tópico).

## <a name="architecture"></a>Arquitetura
o mecanismo de sincronização Olá cria uma exibição integrada de objetos que são armazenados em várias fontes de dados conectadas e gerencia informações de identidade em fontes de dados. Este modo de exibição integrado é determinado pelas informações de identidade Olá recuperadas de fontes de dados conectadas e um conjunto de regras que determinam como tooprocess essas informações.

### <a name="connected-data-sources-and-connectors"></a>Fontes de Dados Conectadas e Conectores
o mecanismo de sincronização Olá processa informações de identidade de repositórios de dados diferentes, como Active Directory ou um banco de dados do SQL Server. Cada repositório de dados que organiza os dados em um formato de banco de dados e que fornece métodos de acesso a dados padrão é um candidato potencial de fonte de dados para o mecanismo de sincronização de saudação. repositórios de dados de saudação que são sincronizados pelo mecanismo de sincronização são chamados **fontes de dados conectadas** ou **conectado diretórios** (CD).

encapsula o mecanismo de sincronização de saudação interação com uma fonte de dados conectada dentro de um módulo chamado um **conector**. Cada tipo de fonte de dados conectada tem um Conector específico. Olá conector converte uma operação necessária em formato Olá Olá dados conectada fonte compreende.

Conectores de fazer chamadas de API tooexchange informações de identidade (leitura e gravação) com uma fonte de dados conectada. Também é possível tooadd um conector personalizado usando a estrutura de conectividade extensível hello. Olá ilustração a seguir mostra como um conector se conecta a um mecanismo de sincronização de toohello de fonte dados conectada.

![Arco1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Os dados podem fluir em qualquer direção, mas não podem fluir em ambas as direções simultaneamente. Em outras palavras, um conector pode ser configurado tooallow tooflow de dados do mecanismo de toosync de fonte de dados conectada hello ou da fonte de dados conectada de toohello de mecanismo de sincronização, mas apenas uma dessas operações pode ocorrer a qualquer momento para um objeto e atributo. direção de saudação pode ser diferente para diferentes objetos e atributos diferentes.

tooconfigure um conector, você especificar tipos de objeto de saudação que você deseja toosynchronize. Especificar tipos de objeto Olá define o escopo de saudação de objetos que serão incluídos no processo de sincronização de saudação. Olá próxima etapa é tooselect Olá atributos toosynchronize, que é conhecido como uma lista de inclusão de atributo. Essas configurações podem ser alteradas a qualquer momento nas regras de negócio resposta toochanges tooyour. Quando você usa o Assistente de instalação do Azure AD Connect hello, essas configurações são configuradas para você.

fonte de dados conectada tooa de objetos tooexport, lista de inclusão de atributo Olá deve incluir pelo menos Olá mínimo atributos toocreate necessário, digite um objeto específico em uma fonte de dados conectada. Por exemplo, Olá **sAMAccountName** atributo deve ser incluído no hello tooexport de lista de inclusão de atributo de um usuário objeto tooActive diretório porque todos os objetos de usuário no Active Directory devem ter um **sAMAccountName**  atributo definido. Novamente, o Assistente de instalação de saudação faz essa configuração para você.

Se a fonte de dados conectada Olá usa componentes estruturais, como objetos tooorganize partições ou contêineres, você pode limitar as áreas de saudação na fonte de dados conectada Olá que são usadas para uma determinada solução.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Estrutura interna do namespace de mecanismo de sincronização Olá
namespace de mecanismo de sincronização inteiro Olá consiste em dois namespaces que armazenam informações de identidade hello. Olá dois namespaces são:

* espaço do conector Hello (CS)
* Olá metaverso (MV)

Olá **espaço conector** é uma área de preparação que contém representações de saudação designado objetos de um atributos de fonte e hello de dados conectada especificado na lista de inclusão de atributo de saudação. o mecanismo de sincronização Olá usa toodetermine de espaço do conector Olá o que mudou no hello conectado fonte e toostage entradas alterações de dados. o mecanismo de sincronização Olá também usa toostage de espaço do conector Olá alterações para a fonte de dados conectada toohello de exportação de saída. mecanismo de sincronização de saudação mantém um espaço do conector distintos como uma área de transferência para cada conector.

Usando uma área de preparação, o mecanismo de sincronização Olá permanece independente Olá conectado de fontes de dados e não é afetado por sua disponibilidade e a acessibilidade. Como resultado, você pode processar informações de identidade a qualquer momento usando dados saudação na área de preparação de saudação. o mecanismo de sincronização Olá pode solicitar somente Olá alterações feitas dentro da fonte de dados conectada Olá desde a saudação última sessão de comunicação encerrada ou push informações somente Olá alterações tooidentity que Olá a fonte de dados conectada ainda não recebeu, que reduz tráfego de rede Olá entre o mecanismo de sincronização hello e fonte de dados conectada hello.

Além disso, o mecanismo de sincronização armazena informações de status sobre todos os objetos que ele prepara no espaço do conector de saudação. Quando novos dados são recebidos, o mecanismo de sincronização sempre avalia se dados saudação já foi sincronizados.

Olá **metaverso** é uma área de armazenamento que contém informações de identidade Olá agregado de várias fontes de dados conectadas, fornecendo uma única exibição global e integrada de todos os objetos combinados. Objetos do metaverso são criados com base nas informações de identidade de saudação que são recuperadas de fontes de dados de saudação conectada e um conjunto de regras que permitem que o processo de sincronização de saudação toocustomize.

Olá ilustração a seguir mostra Olá conector espaço namespaces e Olá metaverso no mecanismo de sincronização de saudação.

![Arco2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Objetos de identidade do mecanismo de sincronização
objetos de saudação do mecanismo de sincronização de hello são representações de qualquer um dos objetos na fonte de dados conectada hello ou hello visão integrada que o mecanismo de sincronização tem desses objetos. Todos os objetos do mecanismo de sincronização devem ter um identificador global exclusivo (GUID). Os GUIDs fornecem a integridade dos dados e expressam relacionamentos entre objetos.

### <a name="connector-space-objects"></a>Objetos de espaço do conector
Quando o mecanismo de sincronização se comunica com uma fonte de dados conectada, ele lê as informações de identidade Olá na fonte de dados conectada hello e usa que toocreate informações uma representação de objeto de identidade Olá no espaço do conector de saudação. Você não pode criar ou excluir esses objetos individualmente. No entanto, você pode excluir manualmente todos os objetos em um espaço de conector.

Todos os objetos no espaço do conector Olá tem dois atributos:

* Um identificador global exclusivo (GUID)
* Um nome distinto (também conhecido como DN)

Se conectado Olá fonte de dados atribui um objeto de toohello atributo exclusivo, objetos no espaço do conector Olá também podem ter um atributo de âncora. o atributo de âncora Olá identifica exclusivamente um objeto de fonte de dados conectada hello. mecanismo de sincronização de saudação usa Olá Olá âncora toolocate correspondente representação do objeto na fonte de dados conectada hello. Mecanismo de sincronização pressupõe que ancoram Olá de um objeto nunca alterações em tempo de vida de saudação do objeto hello.

Muitos dos conectores Olá usam toogenerate um identificador exclusivo conhecidos uma âncora automaticamente para cada objeto quando ele é importado. Por exemplo, a saudação conector do Active Directory usa Olá **objectGUID** atributo de âncora. Para fontes de dados conectada que não fornecem um identificador exclusivo claramente definido, você pode especificar a geração de âncora como parte da configuração de conector hello.

Nesse caso, âncora Olá baseia-se de um ou mais atributos exclusivos de um objeto de tipo, nenhum dos quais alterações e que exclusivamente identifica o objeto de saudação no espaço do conector de saudação (por exemplo, um número de funcionário ou uma ID de usuário).

Um objeto de espaço do conector pode ser uma das seguintes hello:

* Um objeto de preparação
* Um espaço reservado

### <a name="staging-objects"></a>Objetos de preparação
Um objeto de preparo representa uma instância de saudação tipos de objeto da fonte de dados conectada Olá designada. Além disso toohello GUID e nome distinto hello, um objeto de preparo sempre tem um valor que indica o tipo de objeto hello.

Objetos de preparo que foram importados sempre têm um valor para o atributo de âncora hello. Objetos de preparo que foram provisionados recentemente pelo mecanismo de sincronização e que estão no processo de saudação do que está sendo criado na fonte de dados conectada Olá não tem um valor para o atributo de âncora hello.

Objetos de preparo também transportar valores atuais dos atributos de negócios e informações operacionais necessários pelo processo de sincronização sincronização mecanismo tooperform hello. Informações operacionais incluem sinalizadores que indicam o tipo de saudação de atualizações que são testados em Olá objeto preparação. Se um objeto de preparo recebeu novas informações de identidade da fonte de dados conectada Olá que ainda não foi processada, o objeto Olá será sinalizado como **importação pendente**. Se um objeto de preparo tem novas informações de identidade que ainda não foram exportados toohello fonte de dados conectada, ele é marcado como **pendentes exportação**.

Um objeto de preparação pode ser um objeto de importação ou de exportação. o mecanismo de sincronização Olá cria um objeto de importação usando as informações de objeto recebidas da fonte de dados conectada hello. Quando o mecanismo de sincronização recebe informações sobre a existência de saudação de um novo objeto que corresponde a um dos tipos de objeto Olá selecionados no hello conector, ele cria um objeto de importação no espaço do conector hello como uma representação de objeto Olá na fonte de dados conectada hello.

Olá ilustração a seguir mostra um objeto de importação que representa um objeto de fonte de dados conectada hello.

![Arco3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

o mecanismo de sincronização Olá cria um objeto de exportação usando as informações de objeto metaverso hello. Objetos de exportação são exportados toohello fonte de dados conectada durante a saudação próxima sessão de comunicação. Da perspectiva de saudação do mecanismo de sincronização hello, objetos de exportação ainda não existe na fonte de dados conectada hello. Portanto, o atributo de âncora Olá para um objeto de exportação não está disponível. Depois que ele recebe o objeto de saudação do mecanismo de sincronização, fonte de dados conectada Olá cria um valor exclusivo para o atributo de âncora de saudação do objeto hello.

Olá ilustração a seguir mostra como um objeto de exportação é criado usando as informações de identidade no metaverso hello.

![Arco4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

mecanismo de sincronização de saudação confirma a exportação de saudação do objeto de saudação por reimportação objeto Olá Olá conectado da fonte de dados. Objetos de exportação tornam-se importar objetos quando o mecanismo de sincronização recebe-los durante a importação de Avançar Olá dessa fonte de dados conectada.

### <a name="placeholders"></a>Espaços reservados
o mecanismo de sincronização Olá usa objetos de toostore um namespace simples. No entanto, algumas fontes de dados conectadas, como o Active Directory, usam um namespace hierárquico. informações de tootransform de um namespace hierárquico em um namespace simples, o mecanismo de sincronização usa a hierarquia de Olá de toopreserve de espaços reservados.

Cada espaço reservado representa um componente (por exemplo, uma unidade organizacional) de um nome de objeto hierárquica que não foi importado para o mecanismo de sincronização, mas é necessário tooconstruct Olá hierárquica nome. Eles preenchem lacunas criadas por referências no tooobjects de fonte de dados Olá conectado que não são objetos no espaço do conector de saudação de preparo.

o mecanismo de sincronização Olá também usa objetos toostore referenciado de espaços reservados que ainda não foram importados. Por exemplo, se a sincronização é atributo de gerente de saudação tooinclude configurado para Olá *Abbie Spencer* de objeto e o valor recebido hello é um objeto que não foi importado, como *CN = Lee Sperry, CN = Users, DC = fabrikam, DC = com*, informações do Gerenciador de saudação são armazenadas como espaços reservados no espaço do conector de saudação. Se o objeto do Gerenciador de saudação é importado mais tarde, o objeto de espaço reservado Olá é substituído pelo Olá objeto que representa o Gerenciador de saudação de preparo.

### <a name="metaverse-objects"></a>Objetos do metaverso
Um objeto do metaverso contém a exibição da saudação agregada tem esse mecanismo de sincronização de saudação objetos no espaço do conector de saudação de preparo. Mecanismo de sincronização cria objetos do metaverso usando informações de saudação importar objetos. Vários objetos de espaço do conector podem ser objeto de metaverso único tooa vinculado, mas um objeto de espaço do conector não pode ser vinculado toomore que um objeto do metaverso.

Os objetos de metaverso não podem ser criados ou excluídos manualmente. mecanismo de sincronização de saudação exclui automaticamente os objetos do metaverso que não têm um objeto de espaço do conector de tooany link no espaço do conector de saudação.

objetos de toomap dentro um dados conectada fonte tooa correspondente tipo de objeto no metaverso hello, o mecanismo de sincronização fornece um esquema extensível com um conjunto predefinido de tipos de objeto e atributos associados. Você pode criar novos tipos de objeto e de atributos para os objetos de metaverso. Atributos podem ter valor único ou vários valores e tipos de atributo de saudação podem ser referências, cadeias de caracteres, números e valores booleanos.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relacionamentos entre objetos de preparação e objetos de metaverso
No namespace do mecanismo de sincronização Olá, Olá fluxo de dados é habilitado pela relação de link de saudação entre objetos de preparo e objetos do metaverso. Um teste do objeto que é chamado de objeto do metaverso tooa vinculado um **objeto Unido** (ou **objeto conector**). Um objeto de preparo que não é um objeto do metaverso tooa vinculado é chamado um **retirado objeto** (ou **objeto separadora**). termos de saudação associado e retirado são preferencial toonot confunda com hello conectores responsáveis para importar e exportar dados de um diretório conectado.

Espaços reservados nunca são vinculados tooa objeto do metaverso

Um objeto associado consiste em um objeto de preparo e seu objeto de metaverso único tooa relação vinculada. Os objetos associados são toosynchronize usados valores de atributo entre um objeto de espaço do conector e um objeto do metaverso.

Quando um objeto de preparo se torna um objeto associado durante a sincronização, os atributos possam fluir entre Olá Olá metaverso objeto e preparo. O fluxo de atributos é bidirecional e é configurado usando regras de atributos de importação e de exportação.

Um objeto de espaço do conector único pode ser vinculado tooonly metaverso um objeto. No entanto, cada objeto do metaverso pode ser vinculado toomultiple conector espaço objetos em Olá mesmo ou em espaços de conector diferente, conforme mostrado na ilustração a seguir de saudação.

![Arco5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Olá vinculado a relação entre hello objeto preparação e um objeto do metaverso é persistente e pode ser removido apenas por regras que você especificar.

Um objeto separado é um objeto de preparo que não é um objeto do metaverso tooany vinculado. atributo Olá valores de um objeto desvinculado não são processados qualquer no metaverso hello. Olá atributo valores de objeto correspondente do hello na fonte de dados conectada Olá não são atualizados pelo mecanismo de sincronização.

Ao usar os objetos separados, você pode armazenar informações de identidade no mecanismo de sincronização e processá-las mais tarde. Manter um objeto temporário como um objeto separado no espaço do conector Olá tem muitas vantagens. Porque o sistema Olá já testou informações Olá necessárias sobre este objeto, não é necessário toocreate em seguida importe uma representação do objeto novamente durante a saudação da fonte de dados conectada hello. Dessa forma, o mecanismo de sincronização sempre tem um instantâneo completo da fonte de dados conectada hello, mesmo se não houver nenhuma fonte de dados conectada toohello conexão atual. Desvinculados objetos podem ser convertidos em objetos associados e vice-versa, dependendo de regras de saudação que você especificar.

Um objeto de importação é criado como um objeto separado. Um objeto de exportação deve ser um objeto unido. lógica de sistema Olá impõe essa regra e exclui cada objeto de exportação que não é um objeto associado.

## <a name="sync-engine-identity-management-process"></a>Processo de gerenciamento de identidades do mecanismo de sincronização
o processo de gerenciamento de identidade Olá controla como as informações de identidade são atualizadas entre fontes de dados conectadas diferentes. O gerenciamento de identidades ocorre em três processos:

* Importar
* Sincronização
* Exportação

Durante o processo de importação Olá, o mecanismo de sincronização avalia Olá entrada informações de identidade de uma fonte de dados conectada. Quando forem detectadas alterações, ele cria novos objetos de preparo ou objetos de preparo existentes no espaço do conector Olá para sincronização de atualizações.

Durante o processo de sincronização Olá, mecanismo de sincronização atualiza Olá metaverso tooreflect alterações que ocorreram no espaço do conector hello e atualiza Olá conector espaço tooreflect alterações que ocorreram no metaverso Olá.

Durante o processo de exportação hello, mecanismo de sincronização envia as alterações que são testados em objetos de preparo e que são sinalizadas como pendentes de exportação.

Olá ilustração a seguir mostra onde cada um dos processos de saudação ocorre como fluxos de informações de identidade de tooanother de fonte de dados conectada um.

![Arco6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Processo de importação
Durante o processo de importação hello, mecanismo de sincronização avalia as atualizações tooidentity informações. Mecanismo de sincronização compara as informações de identidade Olá recebidas da fonte de dados conectada Olá com informações de identidade Olá sobre um objeto de preparo e determina se a saudação objeto preparação requer atualizações. Se for necessário tooupdate Olá objeto com novos dados de preparo, Olá preparo objeto será sinalizada como importação pendente.

Por objetos no espaço do conector Olá antes da sincronização de preparo, o mecanismo de sincronização pode processar apenas informações de identidade Olá que foi alterado. Esse processo fornece Olá benefícios a seguir:

* **Sincronização eficiente**. quantidade de saudação de dados processados durante a sincronização é minimizada.
* **Ressincronização eficiente**. Você pode alterar como o mecanismo de sincronização processa informações de identidade sem fonte de dados do reconectar Olá sincronização mecanismo toohello.
* **Sincronização de toopreview oportunidade**. Você pode visualizar tooverify de sincronização que suas suposições sobre o processo de gerenciamento de identidade Olá estão corretas.

Para cada objeto especificado em Olá conector, o mecanismo de sincronização de saudação tenta primeiro toolocate uma representação de objeto Olá no espaço do conector Olá Olá conector. Mecanismo de sincronização examina todos os objetos de preparo no espaço do conector hello e tenta toofind um objeto de preparo correspondente que tem um atributo de âncora correspondente. Se nenhum objeto de preparo existente tiver uma correspondência ancorar atributo, sincronização mecanismo tentativas toofind um objeto de preparo correspondente com hello mesmo nome distinto.

Quando o mecanismo de sincronização localiza um objeto de preparo que faz a correspondência por nome distinto, mas não por âncora, hello comportamento especial seguinte ocorre:

* Se objeto Olá localizado no espaço do conector Olá não tem nenhuma âncora, mecanismo de sincronização remove o objeto do espaço do conector hello e marcas Olá objeto do metaverso é vinculado tooas **novamente na próxima execução da sincronização de provisionamento**. Em seguida, ele cria um novo objeto de importação hello.
* Se o objeto Olá localizado no espaço do conector Olá tem uma âncora, mecanismo de sincronização supõe que esse objeto foi renomeado ou excluído no diretório conectado hello. Atribui um nome diferenciado temporário e novos para o objeto de espaço do conector Olá para que ele pode preparar objeto de entrada hello. Olá objeto antigo torna-se **transitório**, aguardando Olá conector tooimport Olá renomeação ou exclusão tooresolve Olá situação.

Se o mecanismo de sincronização localiza um objeto de preparo que corresponde o objeto toohello especificado em Olá conector, ele determina que tipo de alterações tooapply. Por exemplo, mecanismo de sincronização pode renomear ou excluir o objeto Olá na fonte de dados conectada hello, ou ele só pode atualizar valores de atributo do objeto de saudação.

Os objetos de preparação com dados atualizados são marcados como importação pendente. Tipos diferentes de importações pendentes estão disponíveis. Dependendo do resultado de saudação do processo de importação de saudação, um objeto de preparo no espaço do conector Olá tem um dos seguintes tipos de importação pendente de saudação:

* **Nenhum**. Nenhum tooany alterações de atributos de saudação do hello objeto preparação estão disponíveis. O mecanismo de sincronização não sinaliza esse tipo como importação pendente.
* **Adicionar**. Olá, objeto de preparo é um novo objeto de importação no espaço do conector hello. Mecanismo de sincronização sinalizadores desse tipo como importação para processamento adicional no metaverso Olá pendente.
* **Atualizar**. Mecanismo de sincronização localiza um objeto de preparo correspondente no espaço do conector hello e sinaliza este tipo como importação pendente para que as atualizações toohello atributos podem ser processados no metaverso hello. As atualizações incluem a renomeação do objeto.
* **Excluir**. Mecanismo de sincronização localiza um objeto de preparo correspondente no espaço do conector hello e sinaliza este tipo como importação pendente para que hello Unido objeto pode ser excluído.
* **Excluir/Adicionar**. Mecanismo de sincronização de encontra um objeto de preparo correspondente no espaço do conector hello, mas os tipos de objeto Olá não correspondem. Nesse caso, uma modificação excluir-adicionar é preparada. A exclusão-adicionar modificação indica o mecanismo de sincronização de toohello uma ressincronização completa do objeto deve ocorrer porque diferentes conjuntos de regras se aplicam a objeto toothis quando altera o tipo de objeto hello.

Olá definindo status de importação de um objeto de preparo pendente, é possível tooreduce Olá significativamente a quantidade de dados processados durante a sincronização porque isso permite que Olá sistema tooprocess apenas os objetos que têm dados atualizados.

### <a name="synchronization-process"></a>Processo de sincronização
A sincronização consiste em dois processos relacionados:

* Sincronização de entrada, quando o conteúdo de saudação do metaverso Olá é atualizado usando dados saudação no espaço do conector de saudação.
* Sincronização de saída, quando o conteúdo de saudação do espaço do conector Olá é atualizado usando dados no metaverso hello.

Usando informações de saudação testadas no espaço do conector hello, hello processo de sincronização de entrada cria no hello metaverso Olá integrado modo de dados Olá armazenados em fontes de dados Olá conectado. Todos os objetos de preparo ou apenas aqueles com informações de importação pendente são agregados, dependendo de como as regras de saudação são configuradas.

atualizações de processo de sincronização de saída Olá exportar objetos quando alterar objetos do metaverso.

Sincronização de entrada cria a exibição de saudação integrada no metaverso Olá Olá de informações de identidade que são recebidos de fontes de dados Olá conectado. Mecanismo de sincronização pode processar informações de identidade a qualquer momento usando as informações de identidade mais recentes Olá que ele tenha de saudação fonte de dados conectada.

**Sincronização de entrada**

Sincronização de entrada inclui Olá processos a seguir:

* **Provisionar** (também chamado de **projeção** se for importante toodistinguish esse processo de provisionamento de sincronização de saída). o mecanismo de sincronização Olá cria um novo objeto de metaverso com base em um objeto de preparo e links-los. O provisionamento é uma operação que ocorre no nível do objeto.
* **Junção**. o mecanismo de sincronização Olá vincula um preparo tooan existente metaverso de objeto. Uma junção é uma operação que ocorre no nível do objeto.
* **Fluxo de atributos de importação**. Mecanismo de sincronização de atualizações de valores de atributo hello, chamados de fluxo de atributo do objeto Olá no metaverso hello. O fluxo de atributos de importação é uma operação que ocorre no nível do atributo que exige um vínculo entre um objeto de preparação e um objeto de metaverso.

Provisionar é Olá único processo que cria objetos no metaverso hello. O provisionamento afeta apenas os objetos de importação separados. Durante o provisionamento, o mecanismo de sincronização cria um objeto de metaverso correspondente toohello o tipo de objeto do objeto de importação hello e estabelece um vínculo entre os dois objetos, criando assim um objeto associado.

processo de junção Olá também estabelece um vínculo entre objetos de importação e um objeto do metaverso. diferença de saudação entre associação e provisionar é que o processo de associação Olá requer esse objeto de importação de saudação são vinculados tooan objeto metaverso existente, onde o processo de provisionamento de saudação cria um novo objeto do metaverso.

Mecanismo de sincronização tenta toojoin um objeto do metaverso importação objeto tooa usando critérios especificados na configuração de regra de sincronização de saudação.

Durante processos de junção e provisionar Olá, o mecanismo de sincronização vincula um objeto do metaverso tooa objeto desvinculados, tornando-os associado. Depois de concluir essas operações de nível de objeto, mecanismo de sincronização pode atualizar valores de atributo de saudação do objeto do metaverso associado hello. Esse processo é chamado de fluxo de atributos de importação.

Importar o fluxo de atributos ocorre em todos os objetos de importação que contêm dados novos e objeto do metaverso tooa vinculado.

**Sincronização de saída**

A sincronização de saída atualiza objetos de exportação quando um objeto de metaverso é alterado mas não é excluído. objetivo de saudação de sincronização de saída é tooevaluate se alterações toometaverse objetos exigem atualizações toostaging objetos nos espaços do conector de saudação. Em alguns casos, Olá alterações podem exigir que o preparo objetos em todos os espaços de conector ser atualizado. Os objetos de preparação alterados são sinalizados como exportação pendente, transformando-os em objetos de exportação. Esses objetos são enviados posteriormente toohello fonte de dados conectada durante o processo de exportação de saudação de exportação.

A sincronização de saída tem três processos:

* **Provisionamento**
* **Desprovisionamento**
* **Fluxo de atributos de exportação**

O provisionamento e o desprovisionamento são ambas operações que ocorrem no nível do objeto. O desprovisionamento depende do provisionamento porque somente o provisionamento pode iniciá-lo. Cancelando o provisionamento é disparado quando o provisionamento remove Olá link entre um objeto do metaverso e um objeto de exportação.

Provisionamento sempre é acionado quando as alterações são aplicadas tooobjects no metaverso hello. Quando as alterações são feitas a objetos toometaverse, mecanismo de sincronização pode executar qualquer uma das tarefas a seguir como parte do processo de provisionamento de saudação do hello:

* Crie objetos associados, onde um objeto do metaverso é vinculado tooa recém-criado exportação de objeto.
* Renomear um objeto unido.
* Separar os vínculos entre um objeto de metaverso e objetos de preparação, criando um objeto separado.

Se provisionamento requer o mecanismo de sincronização toocreate um novo objeto de conector, Olá preparo objeto toowhich Olá metaverso é vinculado é sempre um objeto de exportação, porque o objeto Olá ainda não existe na fonte de dados conectada hello.

Se provisionamento requer o mecanismo de sincronização toodisjoin um objeto associado, criar um objeto separado, cancelando o provisionamento é disparado. Olá desprovisionamento processo exclui o objeto de saudação.

Durante desprovisionamento, a exclusão de um objeto de exportação não exclua fisicamente objeto hello. Olá objeto esteja sinalizado como **excluído**, que significa que essa operação de exclusão Olá preparado no objeto de saudação.

Fluxo de atributo de exportação também ocorre durante o processo de sincronização de saída de hello, modo toohello semelhante que importar o fluxo de atributos ocorre durante a sincronização de entrada. O fluxo de atributos de exportação ocorre apenas entre os objetos de metaverso e os objetos de exportação unidos.

### <a name="export-process"></a>Processo de exportação
Durante o processo de exportação hello, mecanismo de sincronização examina todos os objetos de exportação serão sinalizados como pendentes de exportação no espaço do conector hello e, em seguida, envia as atualizações toohello de fonte de dados conectada.

mecanismo de sincronização de saudação pode determinar o êxito de saudação de exportação, mas ele suficientemente não pode determinar que o processo de gerenciamento de identidade Olá foi concluído. Objetos na fonte de dados conectada Olá sempre podem ser alterados por outros processos. Porque o mecanismo de sincronização não tem uma fonte de dados conectada toohello conexão persistente, não é suficiente suposições toomake sobre as propriedades de saudação de um objeto de fonte de dados conectada Olá com base apenas em uma notificação de exportação com êxito.

Por exemplo, um processo em Olá conectado fonte de dados podem alterar Olá atributos de objeto fazer valores originais tootheir (ou seja, fonte de dados conectada Olá pode substituir valores hello imediatamente após os dados de saudação é enviada por push fora pelo mecanismo de sincronização e com êxito aplicado na fonte de dados conectada Olá).

repositórios de mecanismo de sincronização de saudação exportar e importar informações de status sobre cada objeto de preparo. Se os valores dos atributos de saudação que são especificados na lista de inclusão de atributo Olá foram alterados desde a última exportação de Olá, Olá armazenamento de importação e Exportar status permite sincronização mecanismo tooreact adequadamente. Mecanismo de sincronização usa Olá importação processo tooconfirm valores de atributo que foram exportados toohello fonte de dados conectada. Importado de uma comparação entre hello e informações exportadas, conforme mostrado no hello ilustração, a seguir habilita toodetermine do mecanismo de sincronização se exportação Olá teve êxito ou se precisa toobe repetido.

![Arco7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Por exemplo, se o mecanismo de sincronização exporta atributo C, que tem um valor de 5, tooa conectado a fonte de dados, ele armazena C = 5 em sua memória de status de exportação. Cada exportação adicional neste objeto resulta em uma fonte de dados conectada tentativa tooexport C = 5 toohello novamente porque o mecanismo de sincronização supõe que esse valor não foi toohello persistentemente aplicado objeto (ou seja, a menos que um valor diferente foi importado recentemente de saudação conectado fonte de dados). memória de exportação de saudação é limpo quando C = 5 for recebida durante uma operação de importação no objeto de saudação.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

