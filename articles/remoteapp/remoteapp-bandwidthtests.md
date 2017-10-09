---
title: "aaaAzure RemoteApp - o uso da largura de banda de rede com alguns cenários comuns de teste | Microsoft Docs"
description: "Saiba mais sobre cenários de uso comuns que podem ajudá-lo a entender suas necessidades de largura de banda de rede para o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp - testando o uso da largura de banda de sua rede com alguns cenários comuns
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Conforme abordado em [uso de largura de banda de rede de estimativa do Azure RemoteApp](remoteapp-bandwidth.md), Olá toofigure de maneira melhor o impacto de saudação da rede do Azure RemoteApp tooyour está toorun alguns testes de uso. Execute esses testes para uma conjunto de tempo período e medidas Olá largura de banda necessária para cada cenário. Se você tem a capacidade de saudação, você também pode medir Olá rede pacote perda e rede tremulação toounderstand Olá rede padrões que serão criados no seu ambiente específico.

Ao avaliar o uso de largura de banda hello, lembre-se de que o uso varia entre usuários diferentes em sua empresa. Por exemplo, usuários que gravam e leem textos geralmente consomem menos largura de banda do que usuários que trabalham com vídeos. Para obter melhores resultados, estude a suas necessidades de usuário e crie uma mistura de saudação os seguintes cenários que melhor representa usuários Olá da sua empresa. Lembre-se muito[fatores de saudação de revisão que afetam o uso de largura de banda e o usuário tiver](remoteapp-bandwidthexperience.md) -que ajuda a identificar os testes de saudação ideal.

Leia primeiro sobre testes de hello, escolher a combinação e, em seguida, executá-los. Você pode usar a tabela Olá abaixo toohelp controlar o desempenho.

> [!NOTE]
> Se você não pode fazer seus próprios testes de rede ou você não tem Olá tempo toodo assim, Confira nosso [largura de banda de rede básica estimativas/recomendações](remoteapp-bandwidthguidelines.md). No entanto, seu nível de uso pode variar. Sendo assim, se *puder* executar seus próprios testes, faça isso.
> 
> 

## <a name="hello-usage-tests"></a>Olá testes de uso
Cada um destes testes é executado por períodos de tempo diferentes e testa funções/recursos diferentes que consomem largura de banda de rede. Lembre-se a combinação de saudação toochoose de teste que melhor corresponde os usuários individuais da empresa.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>PowerPoint executivo/completo - executado por 900 a 1000 segundos
Um usuário apresenta entre 45 e 50 slides de alta fidelidade usando o Microsoft Office PowerPoint no modo de tela inteira. os slides Olá devem conter imagens, as transições (com animações) e planos de fundo com gradiente de cores que são comuns para a sua empresa. usuário Olá deve passar pelo menos 20 segundos em cada slide.

Este cenário cria tráfego intermitente, quando um slide faz a transição toohello próximo slide na apresentação de saudação.

### <a name="simple-powerpoint---run-for-620-seconds"></a>PowerPoint simples - execute por cerca de 620 segundos
Um usuário apresenta um arquivo de PowerPoint simples com aproximadamente 30 slides usando o Microsoft Office PowerPoint no modo de tela inteira. slides Olá consomem mais texto de cenário de PowerPoint executivo/complexos hello e tem mais simples de planos de fundo e imagens (diagramas pretos). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - execute por cerca de 250 segundos
Um usuário navega Olá web usando o Internet Explorer. usuário Olá procura e rola uma mistura de texto, imagens naturais e alguns diagramas de esquema. Olá páginas da web armazenadas na unidade de disco local saudação do servidor de Host de sessão de área de trabalho remota (Host de sessão de área de trabalho remota) hello como um. Arquivo MHT. usuário de saudação rolar com Page Up, Page Down, para cima e para baixo de chaves, intervalos diferentes para cada chave/tipo de rolagem:

    - Seta para baixo – 250 pressionamentos de tecla a cada 500 ms
    - Page Up – 36 pressionamentos de tecla a cada 1.000 ms
    - Seta para baixo – 75 pressionamentos de tecla a cada 100 ms
    - Page Down – 20 pressionamentos de tecla a cada 500 ms
    - Seta para cima – 120 pressionamentos de tecla a cada 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>Documento em PDF - simples - execute por cerca de 610 segundos
Um usuário lê e pesquisa em um documento em PDF de várias maneiras usando o Adobe Acrobat Reader. documento de saudação deve consistir de várias fontes de texto, tabelas e gráficos simples. documento de saudação tem 35-40 páginas. usuário Olá rola para trás em duas diferentes taxas e encaminha em quatro tamanhos diferentes de zoom (ajustar toopage, ajustar toowidth, 100% e outro de sua escolha). Olá zoom garante que o texto de saudação (fonte) renderiza em tamanhos diferentes. A rolagem é usando Olá Page Up, Page Down, para cima e para baixo de chaves, com diferentes intervalos para cada rolagem.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>Documento em PDF - misto - execute por cerca de 320 segundos
Um usuário lê e pesquisa em um documento em PDF de várias maneiras usando o Adobe Acrobat Reader. Olá documento consiste em várias fontes de texto, tabelas, gráficos simples e imagens de alta qualidade (incluindo fotografias). usuário Olá rola para trás em duas diferentes taxas e encaminha em quatro tamanhos diferentes de zoom (ajustar toopage, ajustar toowidth, 100% e outro de sua escolha). Olá zoom garante que o texto de saudação (fonte) renderiza em tamanhos diferentes. A rolagem é usando Olá Page Up, Page Down, para cima e para baixo de chaves, com diferentes intervalos para cada rolagem.

### <a name="flash-video-playback---run-for-180-seconds"></a>Reprodução de vídeo Flash - execute por cerca de 180 segundos
Um usuário exibe um vídeo codificado com Adobe Flash inserido em uma página da Web. página da web de saudação é armazenada no disco rígido local de saudação do servidor de Host de sessão de área de trabalho remota hello. Olá vídeo é reproduzido no Internet Explorer por um player incorporado do plug-in.

Este cenário emula usuários exibindo páginas da Web com conteúdo avançado e contendo multimídia. A maioria dos dados Olá deve bo por meio de VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Digitação remota do Word - execute por cerca de 1.800 segundos
Um usuário digita um documento em uma sessão de RDP. Pressionamentos de teclas são enviados do lado do cliente Olá documento de tooa de sessão Olá RDP no Microsoft Word em execução na sessão remota hello. Olá digitando taxa é um caractere de cada 250 ms (total 7050 caracteres). 

Esse é um dos cenários mais comuns de saudação para trabalhadores do conhecimento. Este cenário testa a capacidade de resposta de saudação de um usuário digitando em um processador de trabalho moderno. Esse cenário é tooeven confidenciais pequenas alterações no uso de largura de banda.

## <a name="tracking-hello-test-results"></a>Resultados de teste de saudação do controle
Você pode usar o hello os seguintes cenários de saudação tooevaluate tabela em seu ambiente. dados de saudação fornecidos abaixo são apenas para ilustração - pode ser muito diferente daqueles que você observar. 

Para simplificar, vamos supor que todos os cenários são testados usando a resolução da tela hello mesmo 1920 x 1080 pixels e transportes TCP em uma rede com latência (atraso) abaixo 200 ms e rede variação na marca de saudação 120 ms + de aproximadamente 1%.

Sobre tabela hello:

* **Média de experiência** contém Olá largura de banda em que a produtividade do usuário não é afetada significativamente, mas não excluir eventuais problemas de áudio ou vídeos. sistema Olá é capaz de toorecover rapidamente aproveitando lógica dinâmico Olá. Olá rede largura de banda estimativas tentativa tooguarantee Olá qualidade Olá da experiência do usuário.
  * **Problemas notáveis (ponto de interrupção)** contém Olá largura de banda onde os usuários podem notar problemas significativos na sua experiência e sua produtividade é afetada por períodos de tempo mensurável. Neste ponto algoritmos RDP Olá enfrentam e não podem garantir a experiência de qualidade do usuário Olá devido a largura de banda de rede insuficiente.
  * **Recomendado** contém a largura de banda de rede Olá recomendada para experiência boa ou excelente. Ele é normalmente uma etapa de maior valor Olá Olá correspondente **médio experiência** coluna.
  * **Notas** incluem observações e comentários.

| Teste | Experiência média | Problemas perceptíveis (ponto de interrupção) | Largura de banda de rede recomendada | Notas |
| --- | --- | --- | --- | --- |
| PPT executivo/complexo |10 MB/s |1 MB/s |> 10 MB/s, preferencialmente 100 MB/s |A 1 MB/s, muitas animações são perdidas |
| PPT simples |5 MB/s |256 KB/s |10 MB/s |A 256 KB/s slides Olá carregar com atraso perceptível |
| Internet Explorer |10 MB/s |1 MB/s |> 10 MB/s, preferencialmente 100 MB/s |A 1 MB/s, vídeos da Web ficam confusos e instáveis, a rolagem rápida apresenta problemas |
| PDF simples |1 MB/s |256 KB/s |5 MB/s |A 256 KB/s que leva um tempo página de saudação tooload |
| PDF misto |1 MB/s |256 KB/s |5 MB/s |A 256 KB/s página Olá leva uma quantidade considerável de tooload de tempo |
| Reprodução de vídeo Flash |10 MB/s |1 MB/s |> 10 MB/s, preferencialmente 100 MB/s |A 1 MB/s Olá vídeo é granulado e alguns quadros são ignorados |
| Digitação remota do Word |256 KB/s |128 KB/s |1 MB/s |A 256 KB/s usuário pode observar o tempo de saudação entre pressionamentos de tecla |

largura de banda de rede Olá de tooevaluate por usuário, crie uma mistura de saudação acima cenários e proporção correspondente de saudação de largura de banda necessária. Separar o número mais alto de Olá necessário para seus cenários. Como os usuários quase nunca usam apenas o sistema hello, considere algumas reserva para os usuários que trabalham simultaneamente na mesma rede de hello.

## <a name="learn-more"></a>Saiba mais
* [Estimar o uso de largura de banda de rede do Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp - como a largura de banda de rede e a qualidade da experiência funcionam juntas?](remoteapp-bandwidthexperience.md)
* [Largura de banda de rede do Azure RemoteApp - diretrizes gerais (se não puder testar a sua)](remoteapp-bandwidthguidelines.md)

