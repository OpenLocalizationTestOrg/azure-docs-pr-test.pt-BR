---
title: "aaaGetting iniciado - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "Esta é uma visão mais profunda realce Olá a ferramenta de modelagem de ameaças em ação."
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
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Guia de Introdução ao Olá, ferramenta de modelagem de ameaça

equipe de nuvem e ferramentas de segurança do Enterprise Olá lançado Olá visualização de ferramenta de modelagem de ameaça anteriormente este ano grátis  **[clique para baixar](https://aka.ms/tmtpreview)**. Olá alteração no mecanismo de entrega permite que toopush hello mais recentes aprimoramentos e correções de bugs toocustomers toda vez que abrirem ferramenta hello, facilitando toomaintain e uso.
Este artigo o conduz pelo processo de saudação do guia de Introdução com a abordagem de modelagem de ameaças do hello Microsoft SDL e mostra como os modelos de ameaça grande do toodevelop toouse Olá ferramenta como a base do seu processo de segurança.

Este artigo se baseia no conhecimento existente da abordagem de modelagem de ameaças SDL hello. Para uma rápida revisão, consulte muito**[aplicativos Web de modelagem de ameaça](https://msdn.microsoft.com/library/ms978516.aspx)**  e uma versão de arquivo morto  **[Olá descobrir falhas de segurança usando a abordagem STRIDE](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  Publicada do artigo do MSDN em 2006.

Resumir tooquickly, Olá abordagem envolve a criação de um diagrama, identificando as ameaças, mitigá-los e validar cada mitigação. Veja um diagrama que destaca esse processo:

![Processo do SDL](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Processo de modelagem de ameaças de saudação inicial

Quando você inicia a ferramenta de modelagem de ameaça de saudação, você observará algumas coisas, como mostrado na imagem de saudação:

![Página inicial em branco](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Seção de modelo de ameaça

| Componente                                   | Detalhes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Botão Comentários, Sugestões e Problemas** | Leva você Olá  **[Fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  para tudo SDL. Ele fornece uma tooread oportunidade por meio de que outros usuários estão fazendo, juntamente com recomendações e soluções alternativas. Se você ainda não é possível localizar o que você está procurando, envie por email tmtextsupport@microsoft.com para nosso toohelp da equipe de suporte é                                                                                                                            |
| **Criar um modelo**                          | Abre uma tela em branco para você toodraw seu diagrama. Verifique tooselect certeza de qual modelo deseja toouse para seu modelo                                                                                                                                                                                                                                                                                                                                                                       |
| **Padrão para novos modelos**                 | Você deve selecionar qual toouse modelo antes de criar um modelo. Nosso modelo principal é hello Azure ameaça modelo, que contém estênceis específicas do Azure, as ameaças e atenuações. Para modelos genéricos, selecione Olá SDL TM da Base de conhecimento do menu suspenso de saudação. Deseja toocreate seu próprio modelo ou enviar um novo para todos os usuários? Confira nosso  **[repositório de modelos](https://github.com/Microsoft/threat-modeling-templates)**  GitHub Page toolearn mais                              |
| **Abrir um modelo**                            | <p>Abre modelos de ameaça salvos anteriormente. recurso de modelos recentemente aberto Olá for grande, se você precisar tooopen seus arquivos mais recentes. Quando você focaliza seleção hello, você encontrará 2 maneiras tooopen modelos:</p><p><ul><li>Abrir deste Computador – modo clássico de abrir um arquivo usando o armazenamento local</li><li>Abrir do OneDrive – equipes podem usar as pastas no OneDrive toosave e compartilhar seus modelos de ameaças em uma colaboração e aumentar a produtividade único local toohelp</li></ul></p> |
| **Guia de Introdução**                   | Olá abre  **[ferramenta de modelagem de ameaças do Microsoft](./azure-security-threat-modeling-tool.md)**  página principal                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Seção do modelo

| Componente               | Detalhes                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Criar Novo Modelo** | Abre um modelo em branco para você toobuild em. A menos que você tenha extenso conhecimento na criação de modelos do zero, é recomendável toobuild das já existentes |
| **Abrir Modelo**       | Abre existente modelos para você toomake alterações muito                                                                                                             |

equipe de ferramenta de modelagem de ameaça Olá trabalha constantemente experiência e a funcionalidade da ferramenta de tooimprove. Algumas pequenas alterações podem ocorrer durante saudação do ano hello, mas todas as alterações principais requerem regravações no guia de saudação. Consulte tooit geralmente tooensure obter anúncios mais recentes hello.

## <a name="building-a-model"></a>Criando um modelo

Nesta seção, vamos seguir:

- Cristina (uma desenvolvedora)
- Ricardo (um gerente de programas) e
- Ashish (um testador)

Eles estão passando pelo processo de saudação do desenvolvimento de seu primeiro modelo de ameaça.

> Ricardo: Olá Cristina, trabalhar em um diagrama de modelo de ameaça hello e quisesse toomake-se de que temos detalhes de saudação à direita. Você pode me ajudar a examiná-lo?
> Cristina: Com certeza. Vamos conferir isso.
> Ricardo abre a ferramenta hello e compartilhe sua tela com Cristina.

![Modelo Básico de Ameaça](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: Certo, parece claro, mas você pode me explicar?
> Ricardo: Claro! Aqui está a divisão de saudação:
> - Nosso usuário humano é representado como uma entidade externa — um quadrado
> - Eles estão enviando o servidor de Web tooour comandos — círculo Olá
> - servidor Web de saudação é consultar um banco de dados (duas linhas paralelas)

O que Ricardo acabou de mostrar a Cristina é um DFD, isto é, **[Diagrama de Fluxo de Dados](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Olá, ferramenta de modelagem de ameaça permite que os limites de confiança toospecify usuários, indicados por linhas pontilhadas de saudação vermelho, tooshow onde diferentes entidades estão no controle. Por exemplo, os administradores de TI requerem um sistema de Active Directory para fins de autenticação, de forma saudação do Active Directory está fora de seu controle.

> Cristina: Parece toome à direita. E ameaças Olá?
> Ricardo: Deixe-me mostrar.

## <a name="analyzing-threats"></a>Analisando ameaças

Quando ele clica no modo de exibição de análise de saudação da seleção de menu Olá ícone (arquivo com lupa), ele é obtido tooa lista de ameaças gerado hello ferramenta de modelagem de ameaça encontrada com base no modelo de padrão de saudação, que usa a abordagem do SDL Olá chamada  **[ STRIDE (falsificação, violação, divulgação de informações, negação de serviço e elevação de privilégio)](https://en.wikipedia.org/wiki/STRIDE_(security))**. ideia Olá é que o software é fornecido em um conjunto previsível de ameaças, que pode ser encontrado usando essas 6 categorias.

Essa abordagem é como a proteção da sua casa, garantindo a cada porta e a janela tem um mecanismo de bloqueio em vigor antes de adicionar um sistema de alarme ou caça a registros após ladrão hello.

![Ameaças básicas](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo começa, selecionando primeiro o item na lista de Olá Olá. Veja o que acontece:

Primeiro, interação de saudação entre dois estênceis de saudação é aprimorada

![Interação](./media/azure-security-threat-modeling-tool/interaction.png)

Segundo informações adicionais sobre a ameaça de saudação aparecem na janela de propriedades de ameaça de saudação

![Informações da Interação](./media/azure-security-threat-modeling-tool/interactioninfo.png)

ameaça Olá gerado ajuda a entender as falhas potenciais de design. categorização de STRIDE Olá lhe dá uma ideia em vetores de ataque potencial, durante a saudação descrição adicional informa que exatamente o que tem incorreto, juntamente com toomitigate de maneiras possíveis-lo. Ele pode usar anotações de toowrite campos editáveis nos detalhes de justificação hello ou alterar as classificações de prioridade dependendo da barra de erros da sua organização.

Modelos do Azure tem usuários de toohelp detalhes adicionais entender não apenas o que está errado, mas também como toofix-lo adicionando hiperlinks, exemplos e descrições de documentação de tooAzure específica.

Descrição de saudação tornou a perceber a importância de saudação de adição de usuários de tooprevent do mecanismo de autenticação de serem falsificados, revelar Olá primeiro ameaça toobe trabalhado. Alguns minutos para discussão de saudação com Cristina, compreendia importância Olá da implementação de controle de acesso e funções. Ricardo preenchido alguns toomake anotações rápidas se que eles foram implementados.

Como Ricardo entrou em ameaças Olá em divulgação de informações, percebeu que o plano de controle de acesso Olá necessárias algumas contas somente leitura para auditoria e geração de relatórios. Ele se perguntou se isso deve ser uma ameaça de novo, mas Olá atenuações foram Olá iguais, portanto ele anotou ameaça Olá adequadamente.
Ele também pensar um pouco mais divulgação de informações e percebeu que as fitas de backup Olá fosse tooneed criptografia, um trabalho para a equipe de operações de saudação.

Ameaças design toohello não aplicável devido tooexisting atenuações ou segurança garante que pode ser alterada muito "Não aplicável" da saudação Status suspenso. Há três outras opções: não iniciado a seleção padrão, precisa de investigação – usados toofollow de itens e Mitigated – depois que ele é totalmente trabalhado.

## <a name="reports--sharing"></a>Relatórios e compartilhamento

Uma vez Ricardo percorre a lista de saudação com Cristina e adiciona observações importantes, atenuações/justificativas, prioridade e status muda, seleciona relatórios -> Criar relatório completo -> Salvar o relatório, que imprime uma boa de relatório para que ele toogo por meio de com trabalho de segurança adequadas colegas tooensure Olá é implementado.

![Informações da Interação](./media/azure-security-threat-modeling-tool/report.png)

Se Ricardo quer tooshare arquivo de saudação em vez disso, ele pode fazer isso facilmente salvando na conta do OneDrive da sua organização. Depois que ele faz isso, ele pode copiar link para documento hello e compartilhá-lo com seus colegas. 

## <a name="threat-modeling-meetings"></a>Reuniões sobre a modelagem de ameaça

Envios Ricardo seu colega de toohis do modelo de ameaça usando OneDrive, Ashish, testador Olá foi underwhelmed. Parece que Ricardo e Cristina deixaram escapar alguns pontos importantes, que poderiam ser facilmente comprometidos. Sua ceticismo é modelos de toothreat um complemento.

Neste cenário, após Ashish assumiu modelo de ameaça Olá, ele chamou para duas reuniões para modelagem de ameaça: toosynchronize uma reunião no processo de saudação e passo a passo diagramas hello e, em seguida, uma segunda reunião para análise de ameaça e aprovação.

Na primeira reunião de hello, Ashish levou 10 minutos descrevendo todos por meio do processo de modelagem de ameaças SDL hello. Ele, em seguida, retirado do diagrama de modelo de ameaça hello e iniciado explicar em detalhes. Em cinco minutos, foi identificada a ausência de um componente importante.

Alguns minutos mais tarde, Ashish e Ricardo iniciaram uma longa discussão sobre como o servidor de Web hello foi criado. Não era a maneira ideal Olá para tooproceed uma reunião, mas todos concordaram que descobrir discrepância Olá no início iria toosave tempo no futuro hello.

Olá segunda reunião, equipe Olá percorrido ameaças hello, discutidos tooaddress algumas maneiras-las e assinado off no modelo de ameaça hello. Eles marcado documento Olá para controle de origem e continuaram o desenvolvimento.

## <a name="thinking-about-assets"></a>Pensando sobre os ativos

Alguns leitores com a modelagem de ameaça podem notar que não falamos sobre ativos. Descobrimos que muitos engenheiros de software entendem melhor do que eles entendam o conceito de saudação de ativos e ativos de que um invasor pode estar interessado em seu software.

Se você vai toothreat uma casa de modelo, você pode iniciar, considere suas fotos de família, insubstituíveis ou obras de arte. Talvez comece pensando em possíveis invasores e um sistema de segurança atual hello. Ou você pode iniciar considerando Olá características físicas, como o pool de saudação ou entrada principal hello. Eles são análogo toothinking sobre ativos, invasores ou design de software. Qualquer uma dessas três abordagens funciona.

Olá toothreat a abordagem modelagem apresentados aqui é muito mais simples do que a Microsoft fez no hello anterior. Descobrimos que abordagem de design de software Olá funciona bem para muitas equipes. Esperamos que inclua a sua.

## <a name="next-steps"></a>Próximas etapas

Envie suas perguntas, comentários e preocupações tootmtextsupport@microsoft.com. **[Baixar](https://aka.ms/tmtpreview)**  Olá a ferramenta de modelagem de ameaça tooget iniciado.
