---
title: "otimização de download de arquivo aaaLarge via Olá rede de fornecimento de conteúdo do Azure"
description: "Otimização de downloads de arquivos grandes explicada em detalhes"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Otimização de download de arquivo grande por meio de saudação rede de fornecimento de conteúdo do Azure

Tamanhos de arquivos de conteúdo pela Internet da saudação continuam toogrow devido a funcionalidade de tooenhanced, elementos gráficos aprimorado e conteúdo de mídia avançada. Esse crescimento é causado por vários fatores: penetração de banda larga, dispositivos de armazenamento maiores de baixo custo, aumento generalizado de vídeos de alta definição, dispositivos conectados à Internet (IoT), etc. Um mecanismo de entrega rápida e eficiente para arquivos grandes é crítico tooensure uma experiência de consumidor e divertido e suave.

A distribuição de arquivos grandes apresenta vários desafios. Primeiro, toodownload de tempo médio de saudação um arquivo grande pode ser significativa porque os aplicativos não podem baixar todos os dados em sequência. Em alguns casos, os aplicativos podem baixar a última parte Olá de um arquivo antes da primeira parte do hello. Quando for solicitada uma pequena quantidade de um arquivo ou um usuário faz uma pausa de um download, download Olá pode falhar. download de saudação também pode ser atrasada até após Olá rede de fornecimento de conteúdo (CDN) recupera todo o arquivo de saudação do servidor de origem de saudação. 

Em segundo lugar, a latência entre o computador do usuário e o arquivo hello Olá determina velocidade Olá no qual eles podem exibir o conteúdo. Além disso, problemas de capacidade e congestionamento de rede também afetam a taxa de transferência. Maiores distâncias entre servidores e usuários criam mais oportunidades para toooccur de perda de pacotes, que reduz a qualidade. redução de saudação na qualidade causado por taxa de transferência limitada e perda de pacote maior pode aumentar o tempo de espera de saudação para um toofinish de download do arquivo. 

Em terceiro lugar, muitos arquivos grandes não são entregues em sua totalidade. Os usuários podem cancelar um download no meio ou assista somente Olá primeiros minutos de um vídeo MP4 de longo. Portanto, as empresas de entrega de software e mídia deseja toodeliver apenas parte de saudação de um arquivo que é solicitado. Distribuição eficiente de saudação solicitado partes reduz o tráfego de saída de saudação do servidor de origem de saudação. Distribuição eficiente também reduz a memória hello e pressão de e/s no servidor de origem de saudação. 

saudação de rede de entrega de conteúdo do Azure do Akamai agora oferece um recurso que fornece arquivos grandes com eficiência toousers globo Olá em escala. recurso de Olá reduz as latências porque ele reduz a carga de saudação em servidores de origem hello. Este recurso está disponível com a camada de preços padrão Akamai hello.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Configurar uma entrega de toooptimize de ponto de extremidade CDN de arquivos grandes

Você pode configurar o fornecimento de toooptimize de ponto de extremidade CDN para arquivos grandes via Olá portal do Azure. Você também pode usar nossas APIs REST ou qualquer um dos Olá cliente SDKs toodo isso. Olá, etapas a seguir mostram processo Olá via Olá portal do Azure.

1. tooadd um novo ponto de extremidade, em Olá **perfil CDN** página, selecione **ponto de extremidade**.

    ![Novo ponto de extremidade](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. Em Olá **otimizado para** lista suspensa, selecione **download de arquivo grande**.

    ![Otimização de arquivos grandes selecionada](./media/cdn-large-file-optimization/02_Creating.png)


Depois de criar o ponto de extremidade CDN hello, ela se aplica a otimizações de arquivo grande Olá para todos os arquivos que correspondem a certos critérios. Olá seção a seguir descreve esse processo.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Otimizar para entrega de arquivos grandes com hello Azure rede de fornecimento de conteúdo do Akamai

recurso de tipo de otimização de arquivo grande Olá ativa otimizações e configurações toodeliver grandes arquivos de rede mais rápido e mais responsively. Fornecimento de web gerais com Akamai armazena em cache os arquivos abaixo de 1,8 GB e pode túnel (não o cache) too150 GB de arquivos. Otimização de grandes arquivos armazena em cache os arquivos de backup too150 GB.

A otimização de arquivos grandes é eficaz quando determinadas condições são atendidas. As condições incluem o funcionamento do servidor de origem hello e tamanhos de saudação e tipos de arquivos de saudação que são solicitados. Antes de entrarmos em detalhes sobre essas questões, você deve entender como funciona a otimização de saudação. 

### <a name="object-chunking"></a>Agrupamento de objeto 

Olá rede de entrega de conteúdo do Azure do Akamai usa uma técnica chamada de agrupamento do objeto. Quando um arquivo grande é solicitado, Olá CDN recupera partes menores de arquivo hello origem hello. Depois que o servidor de borda/POP de CDN Olá recebe uma solicitação de arquivo completo ou o intervalo de bytes, ele verifica se o tipo de arquivo hello tem suporte para a otimização. Ele também verifica se o tipo de arquivo hello atende aos requisitos de tamanho de arquivo hello. Se o tamanho do arquivo hello for maior que 10 MB, o servidor de borda CDN Olá solicitações arquivo hello origem Olá em partes de 2 MB. 

Depois parte Olá chega ao Olá borda da CDN, ele tem armazenada em cache e imediatamente servido toohello usuário. Olá CDN e realiza a pré-busca dos Olá próxima parte em paralelo. Este pré-busca garante que o conteúdo de saudação permaneça uma parte à frente do usuário hello, o que reduz a latência. Esse processo continua até Olá todo arquivo é baixado (se solicitado), todos os intervalos de bytes estão disponíveis (se solicitado), ou o cliente Olá encerra a conexão de saudação. 

Para obter mais informações sobre a solicitação de intervalo de bytes hello, consulte [7233 RFC](https://tools.ietf.org/html/rfc7233).

Olá CDN armazena em cache todas as partes que são recebidas. todo o arquivo Hello não tem toobe armazenados em cache no cache CDN hello. As solicitações subsequentes de intervalos de bytes ou arquivo hello são atendidas do hello cache CDN. Se nem todas as partes de saudação são armazenados em cache no hello CDN, pré-busca é usada toorequest partes da origem de saudação. Essa otimização se baseia na capacidade de Olá Olá origem toosupport intervalo de bytes de solicitações de servidor. _Se o servidor de origem Olá não dá suporte a solicitações de intervalo de bytes, essa otimização não é eficaz._ 

### <a name="caching"></a>Cache
A otimização de arquivos grandes usa tempos de expiração de cache padrão diferentes da distribuição na Web geral. Ele faz distinção entre cache positivo e negativo cache com base em códigos de resposta HTTP. Se o servidor de origem Olá Especifica um tempo de expiração por meio de um controle de cache ou expira o cabeçalho de resposta de saudação, Olá CDN honra esse valor. Quando não especifica a origem de saudação e arquivo hello coincide com as condições de tipo e tamanho de saudação para este tipo de otimização, Olá CDN usa valores padrão de saudação para otimização de arquivos grandes. Caso contrário, Olá CDN usa padrões para a entrega da web geral.


|    | Web geral | Otimização de arquivos grandes 
--- | --- | --- 
Cache: Positivo <br> HTTP 200, 203, 300, <br> 301, 302 e 410 | 7 dias |1 dia  
Cache: Negativo <br> HTTP 204, 305, 404, <br> e 405 | Nenhum | 1 segundo 

### <a name="deal-with-origin-failure"></a>Lidar com falhas de origem

tempo de limite de leitura de origem de saudação aumenta de dois segundos para minutos de tootwo de entrega geral web hello grande otimização para tipo de arquivo. Esse aumento contas para tooavoid de tamanhos de arquivo maior do hello uma conexão de tempo limite prematuro.

Quando uma conexão for interrompida, Olá CDN repete várias vezes antes de enviar um erro "504 - tempo limite do Gateway" toohello ao cliente. 

### <a name="conditions-for-large-file-optimization"></a>Condições para a otimização de arquivo grande

Olá, a tabela a seguir lista o conjunto de saudação de critérios toobe satisfeito para otimização de grandes arquivos:

Condição | Valores 
--- | --- 
Tipos de arquivo com suporte | 3g2, 3gp, asf, avi, bz2, dmg, exe, f4v, flv, <br> gz, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> mpeg, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Tamanho mínimo do arquivo | 10 MB 
Tamanho máximo do arquivo | 150 GB 
Características do servidor de origem | Deve dar suporte a solicitações de intervalo de bytes 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Otimizar para entrega de arquivos grandes com hello Azure rede de fornecimento de conteúdo da Verizon

saudação de rede de entrega de conteúdo do Azure da Verizon oferece grandes arquivos sem um limite de tamanho do arquivo. Recursos adicionais são ativados pelo fornecimento de toomake padrão de arquivos grandes mais rapidamente.

### <a name="complete-cache-fill"></a>Concluir o preenchimento do cache

recurso de preenchimento de cache concluída Olá padrão permite Olá CDN toopull um arquivo no cache de saudação quando uma solicitação inicial é abandonada ou perdida. 

O preenchimento de cache completo é mais útil para ativos grandes. Normalmente, os usuários não baixá-las do toofinish de início. Eles usam o download progressivo. comportamento padrão de saudação força tooinitiate de servidor de borda Olá uma busca em segundo plano do ativo de saudação do servidor de origem de saudação. Posteriormente, o ativo de hello está no cache local do servidor de borda hello. Após completa do objeto Olá no cache de Olá, servidor de borda Olá atende a solicitações de intervalo de bytes toohello CDN para o objeto armazenado em cache hello.

comportamento padrão de saudação pode ser desabilitado por meio do mecanismo de regras de saudação em Olá camada Verizon Premium.

### <a name="peer-cache-fill-hot-filing"></a>Transmissão automática do preenchimento de cache par

recurso de arquivamento hot preenchimento do cache de par de padrão Olá usa um algoritmo de proprietário sofisticado. Ele usa o cache de servidores com base na largura de banda de borda adicional e agregação solicitações métricas toofulfill cliente para objetos grandes, populares. Esse recurso evita que uma situação em que o grande número de solicitações adicionais é enviado servidor de origem tooa do usuário. 

### <a name="conditions-for-large-file-optimization"></a>Condições para a otimização de arquivo grande

recursos de otimização Olá Verizon são ativados por padrão. Não há nenhum limite no tamanho máximo do arquivo. 

## <a name="additional-considerations"></a>Considerações adicionais

Considere Olá seguintes aspectos adicionais para este tipo de otimização.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Rede de Distribuição de Conteúdo do Azure da Akamai

- Olá agrupamento processo gera o servidor de origem toohello solicitações adicionais. No entanto, hello geral volume de dados distribuídos da origem de saudação é muito menor. Agrupamento resulta em melhor cache características no hello CDN.

- Pressão de e/s e memória são reduzidos na origem Olá porque partes menores de arquivo hello são entregues.

- Blocos em cache no hello CDN, não há nenhuma solicitação adicional toohello origem até que o conteúdo de saudação expira ou é removido do cache de saudação.

- Os usuários podem fazer intervalo solicitações toohello CDN e sejam tratados como qualquer arquivo normal. Otimização se aplica somente se ele é um tipo de arquivo válido e o intervalo de bytes Olá entre 10 MB e 150 GB. Se o tamanho de arquivo médio Olá solicitado é menor do que 10 MB, você poderá toouse fornecimento de web gerais em vez disso.

### <a name="azure-content-delivery-network-from-verizon"></a>Rede de Distribuição de Conteúdo do Azure da Verizon

tipo de otimização de entrega Olá web geral pode entregar arquivos grandes.
