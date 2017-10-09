---
title: "aaaMicrosoft ferramenta de modelagem de ameaças - Azure | Microsoft Docs"
description: "Saiba mais sobre todos os recursos de saudação disponíveis no Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Visão geral do recurso Threat Modeling Tool

Estamos contentes em escolhido toouse Olá a ferramenta de modelagem de ameaças para suas necessidades de modelagem de ameaças! Se você ainda não tiver feito isso, visite  **[Getting Started with Olá, ferramenta de modelagem de ameaça](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn Noções básicas de saudação.

> Nossa ferramenta é atualizada com frequência, portanto, verifique este guia geralmente toosee nossos recursos e melhorias mais recentes.

Clicando no botão de "Criar um novo modelo de" hello abre uma página em branco inicial, a imagem toohello semelhante abaixo:

![Página inicial em branco](./media/azure-security-threat-modeling-tool/tmtstart.png)

Usar o modelo de ameaça Olá criado pela nossa equipe de saudação  **[Introdução](./azure-security-threat-modeling-tool-getting-started.md)**  exemplo, vamos check-out de todos os recursos de saudação disponíveis na ferramenta Olá hoje.

![Modelo Básico de Ameaça](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Navegação

Antes de mergulhar nos recursos internos Olá, vamos falar sobre os componentes principais do hello encontrados na ferramenta Olá

### <a name="menu-items"></a>Itens de menu

experiência de saudação deve ser semelhantes produtos da Microsoft tooother. Vamos começar por meio de itens de menu de nível superior de saudação:

![Itens de menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| Rótulo                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Arquivo** | <ul><li>Abrir, Salvar e Fechar Arquivos</li><li>Entrar/Sair das contas do OneDrive</li><li>Compartilhar Links (Exibir + Editar)</li><li>Exibir Informações do Arquivo</li><li>Aplicar o novo modelo tooExisting modelos</li></ul> |
| **Editar** | Desfazer/refazer ações, bem como copiar, colar e excluir |
| **Exibir** | <ul><li>Alternar entre as exibições **Análise** e **Design**</li><li>Abrir as janelas fechadas (por exemplo, estênceis, propriedades do elemento e mensagens)</li><li>Redefinir layout toodefault configurações</li></ul> |
| **Diagrama** | Adicionar/excluir diagramas e navegar pelas "guias" dos diagramas |
| **Relatórios** | Criar tooshare de relatórios HTML com outras pessoas |
| **Ajuda** | Use a ferramenta de saudação de toohelp de guias |

ícones de saudação são atalhos para os menus de nível superior de saudação:

| ícone                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Abrir** | Abre um novo arquivo |
| **Salvar** | Salva o arquivo atual |
| **Design** | Entra no modo de exibição de design, no qual é possível criar modelos |
| **Analise** | Mostra ameaças geradas e suas propriedades |
| **Adicionar Diagrama** | Adiciona um novo diagrama (guias de toonew semelhante no Excel) |
| **Excluir Diagrama** | Exclui o diagrama atual |
| **Copiar/Recortar/Colar** | Copia/recorta/cola elementos |
| **Desfazer/Refazer** | Desfaz/refaz ações |
| **Ampliar/Reduzir** | Aplica zoom dentro e fora do diagrama de saudação para uma melhor exibição |
| **Comentários** | Abre a saudação Fórum do MSDN |

### <a name="canvas"></a>Tela

espaço de saudação em que você arraste e solte elementos em. Arrastar e soltar é hello mais rápida e modelos de toobuild de maneira mais eficientes. Você pode também clique direito e selecione no menu hello, que adiciona versões genéricas de elementos de saudação que você está usando, conforme mostrado abaixo.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Descartando estêncil Olá na tela hello

![Envio para a tela](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Clicar em estêncil Olá

![Propriedades do Elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Estênceis

Onde você pode encontrar todos os estênceis toouse disponível com base no modelo de saudação selecionado. Se você não encontrar elementos à direita hello, tente usar outro modelo ou modificar um toofit suas necessidades. Geralmente, você deve ser capaz de toofind uma combinação de categorias como Olá aquelas abaixo:

| Nome do Estêncil                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Processo** | Aplicativos, Plug-ins de Navegador, Threads, Máquinas Virtuais |
| **Interagente Externo** | Provedores de Autenticação, Navegadores, Usuários, Aplicativos Web |
| **Armazenamento de Dados** | Cache, Armazenamento, Arquivos de Configuração, Banco de Dados, Registro |
| **Fluxo de Dados** | Binário, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Pipe Nomeado, RPC/DCOM, SMB, UDP |
| **Limite de Linha/Borda de Confiança** | Redes Corporativas, Internet, Computador, Área Restrita, Modo de Usuário/Kernel |

### <a name="notesmessages"></a>Observações/Mensagens

| Componente                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Mensagens** | Lógica de ferramenta interna que alerta os usuários sempre que houver um erro, como ausência de fluxos de dados entre elementos |
| **Observações** | Notas manuais arquivo toohello adicionadas pelas equipes de engenharia Olá design durante todo esse processo e processo de revisão |

### <a name="element-properties"></a>Propriedades do elemento

Eles variam de acordo com elementos de saudação selecionados. Com exceção dos Limites de Confiança, todos os outros elementos contêm 3 seleções gerais:

| Propriedade do Elemento                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Nome** | Útil para nomear seu toobe processos, lojas, interadores e fluxos facilmente reconhecido |
| **Fora do Escopo** | Se selecionado, o elemento de saudação é retirado de matriz de geração de ameaça hello (não recomendado) |
| **Motivo para Estar Fora do Escopo** | Os usuários toolet de campo de justificação sabem por que fora do escopo selecionado |

As propriedades são alteradas em cada categoria de elemento. Clique em cada elemento tooinspect Olá as opções disponíveis, ou abra Olá modelo toolearn mais. Vamos falar recursos hello.

## <a name="welcome-screen"></a>Tela de boas-vindas

tela de boas-vindas Olá é Olá primeiro que você vê quando você abrir o aplicativo hello.

### <a name="open-a-model"></a>Abrir um Modelo

Ao passar o mouse sobre o botão "Abrir um Modelo", duas opções ocultas serão exibidas: "Abrir deste Computador" e "Abrir do OneDrive". Olá primeiro abre a tela de abrir arquivo hello, enquanto Olá segundo leva você através de processo de entrada hello para OneDrive, permitindo que você toopick pastas e arquivos após uma autenticação bem-sucedida.

![Abrir Modelo](./media/azure-security-threat-modeling-tool/openmodel.png)

![Abrir do Computador ou do OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Comentários, sugestões e problemas

Esta opção levará você toohello os fóruns do MSDN para as ferramentas do SDL. É toocheck uma ótima maneira out que outras pessoas estão falando sobre ferramenta hello, incluindo novas ideias e soluções alternativas.

![Comentários](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Modo de exibição de Design

Sempre que você abrir ou cria um novo modelo, você será levado toohello modo de design.

### <a name="adding-elements"></a>Adicionando elementos

Há 2 modos tooadd elementos na grade de saudação:

- **Arrastar e soltar** – arraste Olá elemento desejado toohello grade, em seguida, usar Olá elemento propriedades tooprovide obter informações adicionais.
- **Clique com botão direito** – clique com botão direito em qualquer lugar na grade hello e selecione no menu suspenso de saudação. Uma representação genérica desse elemento será exibido na tela hello.

### <a name="connecting-elements"></a>Conectando elementos

Há 2 modos tooconnect elementos na ferramenta hello:

- **Arrastar e soltar** – arraste Olá grade de toohello de fluxo de dados desejado e conectar os dois elementos apropriados de toohello termina.
- **Clique em + Shift** – clique no primeiro elemento de saudação (enviar dados), pressione e mantenha a tecla Shift de hello, em seguida, elemento de segundo select hello (recebimento de dados). Clique com o botão direito do mouse e selecione "Conectar". Se você estiver usando um fluxo de dados de bi-direcional, ordem de saudação não é tão importante.

### <a name="properties"></a>Propriedades

Mostra todas as propriedades de saudação que podem ser modificadas em estênceis Olá colocadas no diagrama de saudação. Propriedades de saudação toosee, basta clicar no estêncil hello e informações hello serão preenchidas adequadamente. exemplo Hello abaixo mostra antes e depois um estêncil é arrastado para o diagrama de hello "Database":

#### <a name="before"></a>Antes

![Antes](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>após

![após](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>Mensagens

Se você criar um modelo de ameaça e esquecer fluxos de dados de tooconnect tooelements, a janela de mensagem de saudação notifica tooact. Você pode escolher tooignore-lo ou siga Olá problema de saudação toofix instruções. 

![Mensagens](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Observações

As guias de tooNotes de mensagens permite que você tooadd notas tooyour diagrama toocapture todas as sugestões

## <a name="analysis-view"></a>Modo de exibição de análise

Quando terminar de criar seu diagrama, alternar exibição tooanalysis indo toohello seleções de menu superior e escolha Olá Lupa próxima toohello paint paleta.

![Modo de Exibição de Análise](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Seleção de ameaça gerada

Ao clicar em uma ameaça, você pode aproveitar três funções exclusivas:

| Recurso                               | Informações      |
| --------------------------------------- | ------------ |
| **Indicador de Leitura** | <p>Ameaça está marcada como leitura, que pode ajudá-lo facilmente manter o controle de itens de saudação que você já seguiu</p><p>![Indicador de Lido/Não Lido](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Foco de Interação** | <p>Interação no diagrama Olá pertencentes a ameaça de toothat é realçada</p><p>![Foco de Interação](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Propriedades da Ameaça** | <p>Informações adicionais sobre a ameaça de saudação são populadas na janela de propriedades de ameaça Olá</p><p>![Propriedades da Ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Alteração de prioridade

Alterar o nível de prioridade de saudação de cada ameaça gerada também altera seu toomake cores-tooidentify fácil ameaças de prioridade alta, média e baixa.

![Alteração de Prioridade](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Campos editáveis das propriedades da ameaça

Conforme mostrado na imagem de saudação acima, os usuários podem alterar informações de saudação geradas pela ferramenta Olá um também adicionar campos de toocertain de informações, como a justificação. Esses campos são gerados pelo modelo hello, então se você precisar de mais informações para cada uma delas, você está toomake incentivados modificações.

![Propriedades da Ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Relatórios

Quando você terminar as mudanças de prioridades e atualizar status de saudação de cada gerado ameaça, você pode salvar o arquivo hello e/ou imprimir um relatório indo muito "relatório" e, em seguida, "Criar relatório completo." Você será solicitado o relatório de saudação tooname e depois que você fizer isso, você verá algo semelhante imagem toohello abaixo:

![Relatório](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Próximas etapas

toocontribute um modelo para a comunidade de hello, acesse tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  página. **[Baixar](https://aka.ms/tmtpreview)**  Olá ferramenta tooget iniciado hoje.
