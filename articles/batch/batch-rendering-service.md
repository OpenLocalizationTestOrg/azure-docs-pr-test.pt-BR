---
title: "aaaUse Olá processamento de lote do Azure serviço toorender na nuvem Olá | Microsoft Docs"
description: "Processa trabalhos em máquinas virtuais do Azure diretamente do Maya e com base em pagamento por uso."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Introdução ao Olá serviço de processamento em lotes

Olá serviço de processamento de lote do Azure oferece recursos de renderização de escala de nuvem em uma base de pagamento por uso. Olá serviço de processamento em lotes trata o agendamento de trabalho e enfileiramento, gerenciando falhas de tentativas e o dimensionamento automático para o trabalho de processamento. Olá serviço de processamento em lotes dá suporte ao Autodesk Maya, 3ds Max e Arnold, com suporte para outros aplicativos em breve. Olá lote plug-in para 2017 Maya torna fácil toostart um trabalho de processamento no Azure diretamente de sua área de trabalho. 

## <a name="supported-applications"></a>Aplicativos com suporte

Olá serviço de processamento em lotes atualmente suporta Olá aplicativos a seguir:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Pré-requisitos

serviço de processamento em lotes de saudação de toouse, você precisa:

- Uma [conta do Azure](https://azure.microsoft.com/free/). 
- **Uma conta do Lote do Azure.** Para obter orientação sobre como criar uma conta de lote no hello portal do Azure, consulte [criar uma conta de lote com hello portal do Azure](batch-account-create-portal.md).
- **Uma conta de Armazenamento do Azure.** usado para o trabalho de processamento de ativos de saudação são armazenados no armazenamento do Azure. Você poderá criar uma conta de armazenamento automaticamente ao configurar a sua conta do Lote. Você também pode usar uma conta de armazenamento existente. toolearn mais sobre contas de armazenamento, consulte [como toocreate, gerenciar ou excluir uma conta de armazenamento no portal do Azure de saudação](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

Olá toouse lote plug-in para Maya, você precisa:

- **Maya 2017**
- **Arnold para Maya**

Você também pode usar o hello [portal do Azure](https://portal.azure.com) toocreate pools de máquinas virtuais que são pré-configurados com Maya, 3ds Max e Arnold. Você pode usar Olá toomonitor portal trabalhos e diagnosticar tarefas com Falha ao baixar os logs de aplicativo e conectando-se remotamente tooindividual VMs usando RDP ou SSH.

## <a name="basic-batch-concepts"></a>Conceitos básicos do Lote

Antes de começar a usar o serviço de processamento em lotes Olá, é útil toobe familiarizado com alguns conceitos de lote, incluindo trabalhos, pools e nós de computação. toolearn mais sobre o lote do Azure em geral, consulte [executar cargas de trabalho intrinsecamente paralelas com lotes](batch-technical-overview.md).

### <a name="pools"></a>Pools

O Lote é um serviço de plataforma para executar o trabalho de computação intensa, como renderização, em um **pool** de **nós de computação**. Cada nó de computação em um pool é uma VM (máquina virtual do Azure) que executa Linux ou Windows. 

Para obter mais informações sobre pools de lote e nós de computação, consulte Olá [Pool](batch-api-basics.md#pool) e [do nó de computação](batch-api-basics.md#compute-node) seções em [soluções com o lote de computação paralela em grande escala desenvolver](batch-api-basics.md).

### <a name="jobs"></a>Trabalhos

Um lote **trabalho** é uma coleção de tarefas que são executados em Olá nós de computação em um pool. Quando você enviar um trabalho de processamento, o lote divide o trabalho de saudação em tarefas e distribui nós de computação de toohello Olá tarefas em Olá pool toorun.

Para obter mais informações sobre trabalhos em lotes, consulte Olá [trabalho](batch-api-basics.md#job) seção [soluções com o lote de computação paralela em grande escala desenvolver](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Olá Use plug-in para Maya toosubmit um trabalho de processamento de lote

Com hello lote plug-in para Maya, é possível enviar um toohello de trabalho de processamento em lotes serviço diretamente do Maya. Olá seções a seguir descreve como tooconfigure Olá trabalho da saudação plug-in e, em seguida, enviá-lo. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Saudação de carga lote plug-in Maya

Olá lote plug-in está disponível em [GitHub](https://github.com/Azure/azure-batch-maya/releases). Descompacte Olá tooa arquivo morto de sua escolha. Você pode carregar o plug-in de saudação diretamente do hello *azure_batch_maya* directory.

Olá tooload plug-in Maya:

1. Execute o Maya.
2. Abra **Janela** > **Configurações/Preferências** > **Gerenciador de Plug-in**.
3. Clique em **Procurar**.
4. Navegue selecione tooand *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>Autenticar contas de lote e armazenamento de acesso tooyour

Olá toouse plug-in, você precisa tooauthenticate usando o lote do Azure e as chaves da conta de armazenamento do Azure. tooretrieve suas chaves de conta:

1. Saudação de exibição plug-in Maya e selecione Olá **Config** guia.
2. Navegue toohello [portal do Azure](https://portal.azure.com).
3. Selecione **contas em lotes** no menu esquerdo hello. Se necessário, clique em **Mais Serviços** e filtre com _Lote_.
4. Localize a conta do lote Olá desejado na lista de saudação.
5. Selecione Olá **chaves** toodisplay de item de menu seu nome de conta, a URL da conta e chaves de acesso:
    - Cole a URL da conta em lotes Olá Olá **Service** campo Olá plug-in do lote.
    - Nome da conta Olá colar em Olá **conta em lotes** campo.
    - Chave da conta primária Olá colar em Olá **chave lote** campo.
7. Selecione as contas de armazenamento no menu esquerdo hello. Se necessário, clique em **Mais Serviços** e filtre com _Armazenamento_.
8. Localize a conta de armazenamento Olá desejado na lista de hello.
9. Selecione Olá **chaves de acesso** nome de conta de armazenamento de saudação de toodisplay de item de menu e chaves.
    - Nome da conta de armazenamento colar Olá em Olá **conta de armazenamento** campo Olá plug-in do lote.
    - Chave da conta primária Olá colar em Olá **chave de armazenamento** campo.
10. Clique em **autenticar** tooensure Olá plug-in pode acessar as duas contas.

Depois de autenticado com êxito, conjuntos de plug-in Olá Olá campo status muito**autenticado**: 

![Autenticar suas contas do Lote e do Armazenamento](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>Configurar um pool para um trabalho de renderização

Depois que você autentica suas contas do Lote e do Armazenamento, configure um pool para o trabalho de renderização. Olá plug-in salva suas seleções entre sessões. Depois que você configurou sua configuração preferencial, não será necessário toomodify-lo, a menos que ele é alterado.

Olá seções a seguir mostram opções disponíveis hello, disponíveis no hello **enviar** guia:

#### <a name="specify-a-new-or-existing-pool"></a>Especificar um pool novo ou existente

toospecify um pool no trabalho de processamento que toorun hello, selecione Olá **enviar** guia. Esta guia oferece opções para criar um pool ou selecionar um pool existente:

- Você pode **automática provisionar um pool para este trabalho** (Olá a opção padrão). Quando você escolhe essa opção, lote cria o pool de saudação exclusivamente para o trabalho atual hello e automaticamente exclui Olá pool quando Olá renderizar o trabalho for concluída. Essa opção é recomendada quando você tem um toocomplete de trabalho de processamento único.
- Você pode **reutilizar um pool persistente existente**. Se você tiver um pool existente que está ocioso, você pode especificar esse pool de trabalho de processamento de saudação em execução, selecionando-o na lista suspensa de saudação. Reutilizar um pool persistente existente economiza Olá tempo necessário tooprovision Olá pool.  
- Você pode **criar um novo pool persistente**. Esta opção cria um novo pool para executar o trabalho de saudação. Ele não exclui pool hello quando o trabalho de saudação for concluído, para que você possa reutilizá-la para trabalhos futuros. Selecione esta opção quando você tiver uma necessidade contínua toorun processar trabalhos. Os trabalhos subsequentes, você pode selecionar **reutilizar um pool existente de persistente** toouse Olá persistente pool que você criou para o primeiro trabalho de saudação.

![Especificar pool, imagem do sistema operacional, tamanho da VM e licença](./media/batch-rendering-service/submit.png)

Para obter mais informações sobre como cobranças se acumulam para máquinas virtuais do Azure, consulte Olá [perguntas frequentes sobre preços Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) e [perguntas frequentes sobre preços Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Especifique a saudação SO tooprovision de imagem

Você pode especificar o tipo de saudação SO imagem toouse tooprovision de nós de computação no pool de saudação do hello **Env** guia (ambiente). Lote atualmente suporta Olá as opções de imagem para a renderização de trabalhos a seguir:

|Sistema operacional  |Imagem  |
|---------|---------|
|Linux     |Versão prévia do Lote CentOS |
|Windows     |Versão prévia do Lote Windows |

#### <a name="choose-a-vm-size"></a>Escolher um tamanho de VM

Você pode especificar o tamanho da VM Olá em Olá **Env** guia. Para saber mais sobre tamanhos de VM disponíveis, confira [Tamanhos de VM Linux no Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) e [Tamanhos de VM Windows no Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Especificar imagem do sistema operacional da VM hello e tamanho na guia de Env Olá](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Especificar opções de licenciamento

Você pode especificar licenças Olá desejar toouse em Olá **Env** guia. As opções incluem:

- **Maya**, que é habilitado por padrão.
- **Arnold**, que estará habilitado se Arnold for detectado como mecanismo de renderização active Olá em Maya.

 Se você quiser toorender usando sua própria licença, você pode configurar o ponto de extremidade de licença adicionando a tabela de toohello de variáveis de ambiente apropriadas hello. Ser toodeselect-se de que as opções de licenciamento do saudação padrão se você fizer isso.

> [!IMPORTANT]
> Você será cobrado para uso de licenças Olá durante a execução de máquinas virtuais no pool de Olá, mesmo se Olá VMs no momento não estão sendo usados para renderização. tooavoid encargos adicionais, navegar toohello **Pools** guia e redimensione nós do hello pool too0 até que você esteja pronto toorun outro trabalho de processamento. 
>
>

#### <a name="manage-persistent-pools"></a>Gerenciar pools persistentes

Você pode gerenciar um pool existente persistente em Olá **Pools** guia. Selecionar um pool na lista de saudação exibe o estado atual de saudação do pool de saudação.

De saudação **Pools** guia, você também pode excluir pool hello e redimensionar número Olá de máquinas virtuais no pool de saudação. Você pode redimensionar um tooavoid de nós do pool too0 incorrer em custos entre as cargas de trabalho.

![Exibir, redimensionar e excluir pools](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>Configurar um trabalho de renderização para envio

Depois que você especificou parâmetros Olá para o pool de saudação que executará o trabalho de processamento de hello, configure o trabalho de saudação em si. 

#### <a name="specify-scene-parameters"></a>Especificar parâmetros de cena

Olá plug-in de lote detecta qual mecanismo de renderização que você está usando atualmente em Maya e exibe Olá apropriado renderizar configurações Olá **enviar** guia. Essas configurações incluem o quadro inicial de hello, quadro final, o prefixo de saída e etapa do quadro. Você pode substituir as configurações de renderização de arquivo hello cena especificando configurações diferentes no hello plug-in. As alterações feitas toohello configurações do plug-in não são configurações de renderização de arquivo de cena toohello back persistente, você pode fazer alterações em uma base de trabalho por trabalho sem a necessidade de arquivo do tooreupload Olá cena.

Olá plug-in avisa se Olá renderizar mecanismo que você selecionou na Maya não tem suporte.

Se você carregar uma nova cena enquanto Olá plug-in estiver aberto, clique em Olá **atualização** botão toomake se Olá configurações sejam atualizadas.

#### <a name="resolve-asset-paths"></a>Resolver caminhos de ativos

Ao carregar plug-in de hello, ele analisa o arquivo em cena Olá para todas as referências de arquivo externo. Essas referências são exibidas no hello **ativos** guia. Se um caminho de referência não pode ser resolvido, Olá plug-in tentativas toolocate arquivo de saudação em alguns locais de padrão, incluindo:

- local de saudação do arquivo de cena Olá 
- do projeto atual Olá _sourceimages_ diretório
- diretório de trabalho atual Hello. 

Se Olá ativo ainda não puder ser localizado, ele é listado com um ícone de aviso:

![Os ativos ausentes são exibidos com um ícone de aviso](./media/batch-rendering-service/missing_assets.png)

Se você souber o local de saudação de uma referência de arquivo não resolvidos, você pode clicar em Olá aviso ícone toobe solicitado tooadd um caminho de pesquisa. Olá plug-in, em seguida, usa esse tooresolve de tooattempt de caminho de pesquisa qualquer recurso ausente. Você pode adicionar quantos caminhos de pesquisa adicionais quiser.

Quando uma referência é resolvida, ela é listada com um ícone de luz verde:

![Ativos resolvidos mostram um ícone verde claro](./media/batch-rendering-service/found_assets.png)

Se sua cena exigir outros arquivos que Olá plug-in não detectou, você pode adicionar outros arquivos ou diretórios. Saudação de uso **adicionar arquivos** e **Adicionar diretório** botões. Se você carregar uma nova cena enquanto Olá plug-in estiver aberto, ser tooclick se **atualização** referências da cena do tooupdate hello.

#### <a name="upload-assets-tooan-asset-project"></a>Carregar projeto de ativo tooan ativos

Quando você enviar um trabalho de processamento, hello referenciado arquivos exibidos no hello **ativos** guia são automaticamente carregado tooAzure armazenamento como um projeto de ativo. Você também pode carregar arquivos de ativo Olá independentemente de um trabalho de processamento, usando Olá **carregar** botão Olá **ativos** nome do projeto na guia Olá ativo for especificado em Olá **projeto**campo e é nomeado após o projeto atual de Maya Olá por padrão. Quando forem carregados arquivos de ativo, a estrutura de arquivo local de saudação é preservada. 

Uma vez carregados, os ativos podem ser referenciados por qualquer quantidade de trabalhos de renderização. Todos os ativos carregados são trabalho tooany disponíveis que referencia o projeto de ativo hello, ou não estão incluídos na cena hello. projeto de ativo Olá toochange referenciado por seu trabalho próximo, alterar o nome de saudação em Olá **projeto** campo Olá **ativos** guia. Se houver arquivos de referência que você deseja tooexclude carregue, desmarque-los usando o botão Olá verde ao lado da lista de saudação.

#### <a name="submit-and-monitor-hello-render-job"></a>Envie e Olá monitor processar trabalho

Depois que você tiver configurado o trabalho de processamento de saudação em Olá plug-in, clique em Olá **enviar trabalho** botão Olá **enviar** guia toosubmit Olá trabalho tooBatch:

![Enviar trabalho de processamento de saudação](./media/batch-rendering-service/submit_job.png)

Você pode monitorar um trabalho que está em andamento da saudação **trabalhos** guia Olá plug-in. Selecione um trabalho de saudação lista toodisplay Olá estado atual do trabalho de saudação. Você também pode usar toocancel neste guia e excluir trabalhos, bem como toodownload Olá saídas e processamento de logs. 

saídas de toodownload modificar Olá **gera** diretório de destino desejado de saudação do campo tooset. Clique em toostart ícone de engrenagem Olá um processo em segundo plano que observa o trabalho hello e downloads saídas medida que progride: 

![Exibir status do trabalho e baixar saídas](./media/batch-rendering-service/jobs.png)

Você pode fechar Maya sem interromper o processo de download de saudação.

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o lote, consulte [executar cargas de trabalho intrinsecamente paralelas com lotes](batch-technical-overview.md).
