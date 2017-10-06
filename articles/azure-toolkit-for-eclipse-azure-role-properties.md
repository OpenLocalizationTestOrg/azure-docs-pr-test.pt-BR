---
title: "aaaAzure propriedades de função"
description: "Saiba como toouse hello o Kit de ferramentas do Azure para configurações de função do Azure tooconfigure Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Propriedades da função do Azure
Várias configurações para sua função do Azure podem ser definidas dentro Olá Kit de ferramentas do Azure para Eclipse.

## <a name="configuring-azure-role-properties"></a>Configuração das propriedades da função do Azure
Configurar as propriedades de função do Azure é feito por meio da caixa de diálogo de propriedades de saudação para sua função de trabalho. Menu de contexto Olá aberto para a função hello no painel Explorador de projeto do Eclipse e o selecione Olá **Azure** submenu. (Se você não vir a função hello em Olá Explorador de projeto do Eclipse, expanda seu projeto do Azure no Explorador de projeto).

![][ic789599]

Olá várias propriedades que podem ser definidas de saudação **propriedades** caixas de diálogo descritas neste tópico. Observe que muitas propriedades são preenchidas automaticamente quando você cria um novo projeto de implantação do Azure.

Olá, páginas de propriedades a seguir está disponível para funções do Azure.

* [Propriedades de máquina virtual](#virtual_machine_properties)
* [Propriedades de caching](#caching_properties)
* [Propriedades de certificados](#certificates_properties)
* [Propriedades de componentes](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Propriedades de pontos de extremidade](#endpoints_properties)
* [Propriedades de variáveis do ambiente](#environment_variables_properties)
* [Propriedades de balanceamento de carga/afinidade (também conhecidas como "sessões temporárias")](#session_affinity_properties)
* [Propriedades de armazenamento local](#local_storage_properties)
* [Propriedades de configuração do servidor](#server_configuration_properties)
* [Propriedades de descarregamento de SSL](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Propriedades de máquina virtual
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **propriedades**, e você tem o tamanho da máquina virtual Olá Olá capacidade toochange e também alterar número de saudação de instâncias, conforme mostrado no Olá a imagem a seguir.

![][ic719499]

> [!NOTE]
> Somente o Windows: quando você definir Olá número de instâncias tooa valor maior que 1 e também configurar um servidor de aplicativos, o Kit de ferramentas de saudação permitirá apenas 1 toorun de instância de função no emulador do Windows hello, independentemente dessa configuração. Isso é tooavoid conflitos de associação de porta entre instâncias de servidor diferente de saudação (por exemplo, todas tentando toobind tooport 8080) quando executadas no hello mesmo computador. A configuração de contagem de instância desejada é preservada, mas entra em vigor somente quando você implanta toohello nuvem.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Propriedades de caching
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **cache**. Na caixa de diálogo, você pode habilitar localizados compatíveis com o memcache os caches nomeados, permitindo que você toohelp velocidade seus aplicativos web.

![][ic719483]

Dentro de saudação **cache** página de propriedades, você pode especificar as configurações globais para Olá a seguir:

* se o cache colocalizado está habilitado.
* tamanho do cache Hello como uma porcentagem da memória.
* nome de conta de armazenamento Olá para salvar o estado do cache hello quando seu aplicativo é executado como um serviço de nuvem, ou nenhum se não quiser que o estado do cache Olá toosave. (nome de conta de armazenamento Olá não é usado quando você executar o aplicativo no emulador de computação hello.) Se você definir o nome de conta de armazenamento Olá muito**(automática)** (que é o padrão de saudação), sua configuração de cache usará automaticamente Olá a mesma conta de armazenamento como Olá um selecione em Olá **publicar tooAzure**caixa de diálogo.

> [!NOTE]
> Olá **(automática)** configuração terá efeito de saudação desejado somente se você publicar sua implantação usando Olá Kit de ferramentas Assistente de publicação. Se em vez disso, você pode publicar arquivo do hello. cspkg manualmente usando um mecanismo externo, como Olá [Portal de gerenciamento][Azure Management Portal], implantação de saudação não funcionará corretamente.
> 
> 

Olá, caixa de diálogo a seguir mostra as propriedades de Olá para um cache.

![][ic719501]

* **Nome:** cache colocalizado do nome de saudação do hello.
* **Número da porta:** Olá toouse de número de porta para o cache de saudação.
* **Política de expiração:** uma saudação valores a seguir que especifica quando uma chave no cache de saudação expira.
  * **Absoluto:** chave Olá expira quando o tempo de saudação especificado por **minutos toolive** for atingido.
  * **NeverExpires:** Olá chave não tem um tempo de expiração.
  * **SlidingWindow:** chave Olá expira se não tiver sido acessada por Olá tempo especificado por **minutos toolive**; cada vez que ela é acessada, Olá relógio de expiração é redefinido.
* **Minutos toolive:** o número máximo de minutos que uma chave memcached toolive, política de expiração de toohello da entidade.
* **Alta disponibilidade com backups replicados em diferentes instâncias de função:** se esta opção estiver habilitada, ajuda a fornecer alta disponibilidade utilizando backups replicados em diferentes instâncias de função. Observe que pelo menos duas instâncias de função devem estar em vigor para a implantação para esse recurso toowork.

tooadd um novo cache, clique em Olá **adicionar** botão Olá **cache** página de propriedades e um **configurar Cache nomeado** caixa de diálogo será aberta. Forneça valores para propriedades de saudação descritas acima.

toomodify um cache nomeado, selecione hello e clique Olá **editar** botão Olá **cache** página de propriedades. Uma caixa de diálogo será aberta permitindo que você toomodify Olá propriedades de cache. Pressione **Okey** toosave valores de cache de saudação.

toodelete um cache, selecione hello e clique Olá **remover** botão Olá **cache** página de propriedades e clique **Sim** tooconfirm exclusão de saudação.

Para obter mais informações sobre como toouse cache, consulte [como tooUse localizada cache][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Propriedades de certificados
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **certificados**.

![][ic710964]

Na caixa de diálogo, você pode adicionar ou remover certificados referenciados pelo seu projeto do Eclipse. Observe que os certificados de saudação listados aqui não são automaticamente armazenados em qualquer armazenamento de chaves Java e, portanto, não estão automaticamente disponíveis para nenhum uso de um aplicativo Java. Eles só são registrados com o Azure para que eles possam ser pré-carregados no hello Windows armazenar em máquinas virtuais de saudação executando a implantação de certificado e subsequentemente usada por outros softwares Windows. Olá no momento, somente o recurso do Kit de ferramentas de saudação que usa Olá certificados referenciados dessa maneira na Olá **certificados** caixa de diálogo [descarregamento de SSL][SSL Offloading], devido tooits a dependência de serviços de informações da Internet (IIS) e o roteamento ARR (Application Request), que exigem Olá toobe certificado apropriado disponibilizado dessa maneira.

Quando você implanta seu tooAzure projeto usando o Assistente de publicação Olá, serão solicitada toopoint em Olá troca de informações pessoais (PFX) arquivos toothese certificados, juntamente com suas senhas correspondentes em ordem tooautomatically carregá-los toohello Serviço do Azure, mas somente se eles não tiverem sido carregados existe anteriormente.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Propriedades de componentes
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **componentes**. Na caixa de diálogo, você tem Olá capacidade tooadd, modifica, ou remove componentes de saudação de sua função, bem como alterar Olá ordem na qual eles são processados.

![][ic719502]

recurso de componentes Olá permite tooadd dependências tooyour Azure projeto de implantação, como projetos de aplicativo Java, arquivos especiais e instruções de linha de comando executável que são necessários para sua implantação.

Para cada componente, você pode especificar:

* Olá toobe de etapa executada ao importar o componente de saudação em seu projeto de implantação do Azure quando ele é criado.
* Olá toobe de etapa executada ao implantar esse componente no hello nuvem do Azure.

> [!NOTE]
> Ao especificar arquivos de componentes ou linhas de comando, tenha em mente que sua implantação será publicada tooa máquina de virtual do Windows, para que suas etapas padrão sejam válidas para um sistema operacional Windows. 
> 
> 

Componentes têm Olá propriedades a seguir:

* **Importação:** método que indica como Olá componente será importado no projeto hello quando Olá projeto é compilado. Pode ser uma saudação valores a seguir:
  * **cópia:** Olá componente é copiado do caminho de local Olá especificado pelo Olá **de** propriedade em função de saudação **approot** directory.
  * **ORELHA:** componente Olá é um Java enterprise archive (EAR) importado de um projeto de aplicativo empresarial no caminho de local de saudação especificado pela Olá **de** propriedade. (Isso é detectado automaticamente pelo Kit de ferramentas de saudação com base na natureza de saudação do projeto Olá nesse local).
  * **JAR:** componente Olá é um JAR (Java archive) e é importado de um projeto Java no caminho de local de saudação especificado pela Olá **de** propriedade. (Isso é detectado automaticamente pelo Kit de ferramentas de saudação com base na natureza de saudação do projeto Olá nesse local).
  * **NONE:** nenhuma ação será tomada tooimport componente de saudação. Isso é aplicável quando o componente de saudação é considerado tooalready estar presente na função de saudação **approot** diretório, ou quando o componente de saudação é simplesmente uma instrução executável de linha de comando, como especificado no hello **como**propriedade quando hello **implantar** método **exec**.
  * **WAR:** componente Olá é um arquivo do aplicativo web Java (WAR) e é importada de um projeto Web dinâmico no caminho de local de saudação especificado pela Olá **de** propriedade. (Isso é detectado automaticamente pelo Kit de ferramentas de saudação com base na natureza de saudação do projeto Olá nesse local).
  * **ZIP:** componente Olá é um arquivo zip e importado pelo diretório de saudação compactação ou arquivo especificado por Olá **de** propriedade.
* **De:** caminho de origem na sua pasta de toohello do computador local ou o arquivo que representa a implantação do hello itens tooimport tooyour. É possível usar variáveis de ambiente do Windows nessa propriedade. Todos os componentes importáveis serão importados para a função hello **approot** diretório quando Olá projeto é compilado.
  
    Observe que você tenha Olá capacidade toodeploy um componente de um download durante a implantação de nuvem toohello (não emulador de computação de saudação). Confira as informações relacionadas abaixo sobre como adicionar um componente.    
* **Como:** nome do arquivo sob o qual Olá componente será importado em função de saudação **approot** diretório e, por fim, implantado em Olá nuvem do Azure. Deixe essa tookeep em branco da propriedade Olá Olá nome mesmo que ele está na máquina local hello. (Para componentes executáveis, ou seja, aqueles cujo **implantar** método está definido muito**exec**, isso pode ser uma instrução de linha de comando do Windows arbitrária.)
  
  > [!IMPORTANT]
  > Se você usar caracteres de espaço para esse valor, eles serão tratados de maneira diferente dependendo da saudação método de implantação. Se o método de implantação de saudação é **exec**, espaços serão interpretados como separadores de argumentos de linha de comando e não como parte do nome de arquivo hello. Para todos os outros métodos de implantação, os espaços serão interpretados como parte do nome de arquivo hello.
  > 
  > 
* **Implantar:** método que indica a ação de saudação aplicado toohello componente quando Olá implantação é iniciada. Pode ser uma saudação valores a seguir:
  
  * **cópia:** componente Olá é copiado toohello caminho de destino especificado pelo Olá **para** propriedade.
  * **Exec:** componente Olá é uma instrução executável de linha de comando do Windows executada no contexto de saudação do caminho de saudação especificado pelo Olá **para** propriedade em tempo de Olá Olá implantação é iniciada.
  * **NONE:** nenhuma ação é aplicada toohello componente quando Olá implantação é iniciada.
  * **ZIP:** componente Olá é descompactado toohello caminho de destino especificado pelo Olá **para** propriedade. Este método está disponível somente quando hello **importação** é de propriedade **zip**.
* **Para:** caminho de destino na máquina virtual de saudação onde Olá componente será implantado. Variáveis de ambiente do Windows podem ser usadas nessa propriedade e caminhos de arquivo são relativos muito**approot**.

tooadd um novo componente, clique em Olá **adicionar** botão Olá **componentes** página de propriedades e um **componente de função do Azure** caixa de diálogo será aberta. Forneça valores para propriedades de saudação descritas acima. 

a seguir Olá mostra um exemplo de como adicionar um novo componente WAR.

![][ic719503]

Ao implantar nuvem toohello (não emulador de computação Olá), se você quiser toodeploy Olá componente de um download, certifique-se que **na nuvem, em vez de incluir no pacote de saudação implantar de** é verificada. Se você quiser toodownload de sua conta de armazenamento do Azure, selecione a conta de armazenamento de saudação do hello **conta de armazenamento** lista suspensa (você pode clicar em Olá **contas** link toomodify o que está na lista de saudação), que preenche parcialmente Olá **URL** campo e, em seguida, preencha Olá restantes parte da URL de saudação. Se você não quiser toouse armazenamento do Azure, selecione **(nenhum)** de saudação **conta de armazenamento** suspensa lista e digite o componente de tooyour URL Olá no hello **URL** campo. Especifique uma saudação métodos a seguir:

* **cópia:** componente Olá para download é copiado toohello caminho de destino especificado pelo Olá **tooDirectory** caminho.
* **mesmo:** Olá mesmo método usado para **implantar a partir de download** para **implantação de pacote**.
* **ZIP:** componente Olá para download é descompactado toohello caminho de destino especificado pelo Olá **tooDirectory** caminho.

toomodify Olá de componente e clique em uma saudação do componente, selecione **editar** botão Olá **componentes** página de propriedades. Uma caixa de diálogo será aberta permitindo que você toomodify Olá propriedades do componente. Pressione **Okey** toosave valores de componente de saudação.

toodelete Olá de componente e clique em uma saudação do componente, selecione **remover** botão Olá **componentes** página de propriedades e clique **Sim** tooconfirm exclusão de saudação.

Componentes são processados na ordem Olá listada. Saudação de uso **mover para cima** e **mover para baixo** tooarrange ordem de saudação de botões.

> [!NOTE]
> recurso de configuração do servidor de saudação se baseia em componentes também. Esses componentes não podem ser removidos ou editados sem remover a configuração do servidor correspondente hello. Você será solicitado sobre isso durante a tentativa de toomake alterações toosuch componentes.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Propriedades de pontos de extremidade
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **pontos de extremidade**. Na caixa de diálogo, você Olá capacidade toocreate um ponto de extremidade, bem como edita ou remove um ponto de extremidade, como mostrado no Olá a imagem a seguir.

![][ic719505]

tooadd um ponto de extremidade, clique em Olá **adicionar** botão Olá **pontos de extremidade** página de propriedades e um **Adicionar ponto de extremidade** caixa de diálogo será aberta.

![][ic710897]

Insira um nome para o ponto de extremidade hello, selecione o tipo de saudação (ou **entrada**, **interno**, ou **InstanceInput**) e especifique a porta pública e privada do hello. Pressione **Okey** toosave Olá novos valores de ponto de extremidade.

Dependendo do tipo de saudação do ponto de extremidade, você pode usar intervalos de porta da seguinte maneira:

* Para um ponto de extremidade de entrada de instância, porta pública Olá pode ser um intervalo de portas (por exemplo **2000-2010**) e a porta privada Olá é um valor fixo.
* Para um ponto de extremidade interno, porta pública Olá não é usada e porta privada Olá pode ser um intervalo ou conjunto tooan asterisco tooindicate que é definida automaticamente pelo Azure ou deixado em branco.
* Para pontos de extremidade de entrada, porta pública Olá só pode ser um valor fixo e porta privada Olá pode ser um valor fixo ou conjunto tooan asterisco tooindicate que é definida automaticamente pelo Azure ou deixado em branco.

Se você quiser toouse um número de porta único em vez de um intervalo, deixe em branco caixa de texto de saudação do final de saudação do intervalo de saudação.

Para as portas que são tooautomatic de conjunto, se você precisar toodetermine qual porta é realmente usada em tempo de execução, seu aplicativo pode usar o hello API de tempo de execução do serviço do Azure, que está documentada na Olá [com.microsoft.windowsazure.serviceruntime pacote Resumo][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify um ponto de extremidade, selecione o ponto de extremidade hello e clique em Olá **editar** botão Olá **pontos de extremidade** página de propriedades. Uma caixa de diálogo será aberta permitindo portas públicas e privadas, tipo e nome de ponto de extremidade de saudação toomodify. Pressione **Okey** toosave Olá modificado valores de ponto de extremidade.

toodelete um ponto de extremidade, selecione o ponto de extremidade hello e clique em Olá **remover** botão Olá **pontos de extremidade** página de propriedades e clique **Sim** tooconfirm exclusão de saudação.

Em ordem tooproperly configurar alguns recursos de saudação (como descarregamento de cache, a afinidade de sessão ou SSL) habilitado por usuário Olá em uma função, Olá Kit de ferramentas pode configurar automaticamente os pontos de extremidade especiais que serão listados juntamente com os pontos de extremidade definidos pelo usuário. Olá Kit de ferramentas impede que o usuário de saudação editando ou excluindo esses pontos de extremidade gerados automaticamente como Olá associados recurso está habilitado.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Propriedades de variáveis do ambiente
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **variáveis de ambiente**. Na caixa de diálogo, você Olá capacidade toocreate uma variável de ambiente, bem como modifica ou remove uma variável de ambiente, como mostrado no Olá a imagem a seguir.

![][ic719506]

Variáveis de ambiente são o script de inicialização tooyour disponível quando a função hello inicia.

> [!NOTE]
> Ao especificar variáveis de ambiente, tenha em mente que sua implantação será publicada tooa máquina virtual Windows para que suas variáveis de ambiente sejam válidas para um sistema operacional Windows.
> 
> 

Como um exemplo de uma variável de ambiente estará disponível quando a função hello for iniciada, crie uma nova variável de ambiente clicando Olá **adicionar** botão. Olá, a seguir mostra uma variável de ambiente denominada **MyRoleVersion** que está sendo criado e atribuído um valor de saudação **1.0**.

![][ic659268]

Em seu código jsp, você pode exibir o valor de saudação usando Olá `System.getenv` método:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Quando o aplicativo é executado está é a saída:

![][ic552233]

toomodify uma variável de ambiente, selecione a variável de ambiente hello e clique em Olá **editar** botão Olá **variáveis de ambiente** página de propriedades. Uma caixa de diálogo será aberta permitindo que você toomodify Olá ambiente propriedades da variável. Pressione **Okey** toosave valores de variáveis do ambiente de saudação.

toodelete uma variável de ambiente, selecione a variável de ambiente hello e clique em Olá **remover** botão Olá **variáveis de ambiente** página de propriedades e clique **Sim**tooconfirm exclusão de saudação.

Em ordem tooproperly configurar alguns recursos de saudação (como configuração do servidor, a depuração remota ou Local de armazenamento) habilitado por usuário Olá em uma função, Olá Kit de ferramentas pode configurar automaticamente as variáveis de ambiente especiais que serão listados juntamente com variáveis de ambiente definidas pelo usuário. Olá Kit de ferramentas impede que o usuário de saudação editar ou excluir essas variáveis de ambiente gerada automaticamente como Olá associados recurso está habilitado.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Propriedades de balanceamento de carga/afinidade (também conhecidas como "sessões temporárias")
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **balanceamento de carga**. Na caixa de diálogo, você tem Olá capacidade tooenable ou desabilite a afinidade de sessão, conforme mostrado no Olá a imagem a seguir.

![][ic719492]

Para saber mais, veja [Afinidade de sessão][Session Affinity]. Além disso, observe o comportamento desse recurso no contexto de saudação do descarregamento de SSL, conforme descrito em [descarregamento de SSL][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Propriedades de armazenamento local
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **armazenamento Local**. Na caixa de diálogo, você tem Olá capacidade toocreate, modificar ou remove armazenamento local temporário para a máquina virtual Olá que está executando o aplicativo. Valores específicos podem ser definidos para o tamanho de saudação do armazenamento local de hello, bem como se o conteúdo de saudação é preservado quando a função hello é reciclada, conforme mostrado no Olá a imagem a seguir.

![][ic719508]

Você também pode especificar uma variável de ambiente que corresponde o armazenamento local toohello.

Por padrão, tudo o que você implanta no Azure é colocado (e descompactado) em Olá **approot** pasta Olá da instância de função. Embora a maioria das implantações simples caibam mesmo após descompactar, espaço de saudação alocado para hello **approot** diretório é limitado e não é bem definido (menos de 1 GB é uma regra prática razoável). Portanto, tooensure Azure aloca espaço em disco suficiente para implantações maiores que talvez não caibam na Olá **approot** pasta, você deve configurar um recurso de armazenamento local usando Olá **armazenamento Local** caixa de diálogo. Para uma maneira fácil toodo isso, consulte [Implantando grandes implantações][Deploying Large Deployments].

Você pode referenciar facilmente recursos de armazenamento de saudação de scripts de inicialização (por exemplo, o **startup.cmd**) usando a variável de ambiente Olá associada automaticamente pelo Kit de ferramentas Olá com recurso de hello, conforme mostrado na Olá  **Armazenamento local** caixa de diálogo. Essa variável de ambiente conterá o caminho completo de saudação do recurso de local de saudação configurado no tempo de saudação que seu script de inicialização é executado. 

toomodify um recurso de armazenamento local, selecione o recurso de armazenamento local hello e clique em Olá **editar** botão Olá **armazenamento Local** página de propriedades. Uma caixa de diálogo será aberta permitindo que você toomodify Olá recurso propriedades de armazenamento local. Pressione **Okey** toosave valores de recursos de armazenamento local de saudação.

toodelete um recurso de armazenamento local, selecione o recurso de armazenamento local hello e clique em Olá **remover** botão Olá **armazenamento Local** página de propriedades e clique **Sim** exclusão de saudação tooconfirm.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Propriedades de configuração do servidor
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **configuração do servidor**. Na caixa de diálogo, você deve ter um Olá capacidade tooadd, remover e modificar hello JDK e servidor de aplicativos Java usado pela sua implantação, bem como adicionar ou remover aplicativos de saudação (como arquivos WAR, JAR ou EAR) usados pela sua implantação.

### <a name="jdk-configuration"></a>Configuração de JDK
Essa caixa de diálogo permite que você toospecify Olá JDK pacote toouse para sua implantação. Se você estiver usando o Eclipse no Windows, você pode especificar Olá JDK pacote toouse localmente quando em execução no hello emulador do Azure e você tiver Olá opção toodeploy tooAzure essa instalação local. Em sistemas operacionais não Windows, a configuração do JDK de emulador Olá não é aplicável e não é possível implantar Olá localmente instalado JDK, pois ele não é compatível com o Windows. No entanto, independentemente do hello sistema operacional que você está usando, você pode optar entre Olá 3ª parte JDK pacotes toodeploy tooAzure ou apontar para seu próprio pacote JDK compatível com o Windows de um local alternativo de download.

a seguir Olá é um exemplo de como você pode especificar um JDK no Windows:

![][ic780647]

Se você estiver usando o Eclipse no Windows, você pode especificar um toouse JDK com hello computação emulador; toodo assim, certifique-se de **Olá Use JDK desse caminho de arquivo para testar localmente** check-in Olá **implantação de emulador** seção. Em seguida, especifique Olá caminho local tooyour JDK; Você pode procurar toodifferent JDK se hello aquele que você deseja toouse não será selecionado automaticamente. Você também tem Olá opção toodeploy tooyour seu JDK serviço de nuvem do Azure. toodo assim, marque Olá **implantar meu JDK local (carregamento automático toocloud armazenamento)** opção Olá **implantação de nuvem** seção.

Observação: Em sistemas operacionais não Windows, Olá **implantação de emulador** configurações e hello **implantar meu JDK local** opção não estão disponíveis. Olá exemplo a seguir ilustra especificando um JDK em um Mac ou outro sistema de operacional de não-Windows com suporte:

![][ic789643]

Independentemente do sistema operacional do hello estão em, você tem Olá após dois **implantação de nuvem** opções para a origem de saudação e o tipo do pacote JDK:

* **Implantar um pacote JDK de terceiros disponível no Azure** 
* **Implantar de um download personalizado** 

Se você estiver usando Olá **implantar um pacote 3º de JDK de terceiros disponível no Azure** opção:

1. Marque caixa de seleção Olá denominada **implantar um pacote 3º de JDK de terceiros disponível no Azure**.
2. Olá lista suspensa, selecione lista Olá 3ª parte pacote JDK disponível no Azure.
3. O **JDK** guia terá aparência semelhante seguinte toohello no Windows: ![][ic780648] e terá aparência semelhante seguinte toohello no Mac OS, ou outros suporte para sistemas operacionais não Windows:![][ic789643]
4. Clique em **Okey** toosave suas alterações.
5. Quando solicitada tooaccept hello contrato de licença do provedor de pacote para Olá 3ª parte JDK, revise os termos de licença hello. Se você aceitar os termos de saudação, clique em **Sim** tooclose Olá **aceitar o contrato de licença** caixa de diálogo.
    Observe que Olá subjacente lógica para os quais itens aparecem na lista suspensa Olá Olá **implantar um pacote 3º de JDK de terceiros disponível no Azure** opção pode ser personalizada. toocustomize Olá itens, Olá **JDK** caixa de diálogo, clique em Olá **personalizar** link. Isso fecha Olá **JDK** página de propriedades e abra Olá **componentsets.xml** arquivo no Eclipse, que você pode modificar conforme necessário. Documentação para **componentsets.xml** está incluído no hello **componentsets.xml** próprio arquivo.

Se você estiver usando Olá **implantar um JDK a partir de um download personalizado** opção:

1. Crie um ZIP do diretório de instalação do JDK, garantir que próprio nó de diretório Olá é filho de Olá Olá ZIP da estrutura de e não seu conteúdo. Tome nota do nome de saudação do diretório Olá, será necessário mais tarde e tenha em mente que este JDK instalação será implantado tooa máquina de virtual do Windows.
2. Carregar Olá ZIP em sua conta de armazenamento do Azure como um blob. Você pode fazer isso usando uma ferramenta disponível externamente para carregar blobs tooAzure armazenamento. É recomendável toouse um blob privado. Anote a URL de blob de saudação do conteúdo do ZIP hello.
3. Marque caixa de seleção Olá denominada **implantar um JDK a partir de um download personalizado**.
    Se você quiser toodownload de sua conta de armazenamento do Azure, selecione a conta de armazenamento de saudação do hello **conta de armazenamento** lista suspensa (você pode clicar em Olá **contas** link toomodify o que está na lista de saudação), que preenche parcialmente Olá **URL** campo e, em seguida, preencha Olá restantes parte da URL de saudação. Se você não quiser toouse armazenamento do Azure, selecione **(nenhum)** de saudação **conta de armazenamento** suspensa lista e digite Olá URL tooyour baixar o JDK no hello **URL** campo. Se usar o armazenamento do Azure, nomes de blob na URL de saudação devem estar em minúsculos.
4. Certifique-se de que Olá **JAVA_HOME** caixa de texto se refere a toohello nome de diretório correto. Por padrão, ela fará referência Olá o mesmo nome de diretório do JDK como valor Olá escolhido para uso local. Porém, se o diretório de saudação contido em Olá ZIP tem um nome diferente (por exemplo, data de conclusão toousing uma versão diferente), nome de diretório de saudação de atualização no hello **JAVA_HOME** caixa de texto da mesma forma, desde que essa configuração será usada na saudação de nuvem ( não no emulador de computação Olá).
5. Clique em **Okey** toosave suas alterações.

É isso. Agora, quando você cria para nuvem hello, você observará tamanho de pacote hello será muito menor, o processo de compilação Olá normalmente deve levar menos tempo e implantação hello quando você publica toohello nuvem também deve levar menos tempo. Observe que Olá **implantar meu JDK local (carregamento automático toocloud armazenamento)** ou **implantar um JDK a partir de um download personalizado** opções estão em vigor somente quando o aplicativo for implantado na nuvem hello. Eles não têm nenhum efeito na sua experiência de emulador de computação; a versão local Olá dos componentes de saudação ainda será usado quando você implantar o emulador de computação toohello. 

### <a name="server-configuration"></a>Configuração de Servidor
a seguir Olá é um exemplo de como você pode especificar um servidor de aplicativos.

![][ic796926]

Verifique se esse Olá **implantar um servidor deste tipo** caixa de seleção está selecionada e, em seguida, escolha o tipo de saudação do servidor de aplicativos que você deseja toouse.

Para especificar um toouse de servidor para implantação em nuvem, você pode tirar proveito da saudação as opções a seguir:

1. **Implantar um servidor de terceiros 3º disponível no Azure** -isso é aplicável principalmente em cenários de desenvolvimento/teste onde simplicidade e eficiência de implantação é uma prioridade e servidor de saudação não exige uma configuração personalizada. Ou, quando você deseja toouse um desses servidores como ponto de partida de saudação mas incluir etapas de personalização de servidor apropriado na lógica de inicialização da implantação.
2. **Implantar a partir de um download personalizado** -isso é aplicável principalmente em cenários de produção quando você tiver um servidor especialmente configurado e preparado que você deseja toouse na nuvem hello.
3. **Implantar a instalação de meu servidor local** : essa opção é aplicável principalmente se a instalação do servidor local já estiver configurada de forma personalizada para uso. Se você escolher essa opção, você também deve especificar caminho do seu servidor local no hello **caminho de servidor Local** abaixo da caixa de texto.

Se você estiver usando Olá **implantar um servidor de terceiros 3º disponível no Azure** opção:

1. Marque caixa de seleção Olá denominada **implantar um servidor de terceiros 3º disponível no Azure**.
2. Menu suspenso de saudação, selecione Olá desejado toouse de software de servidor com a implantação na nuvem de saudação. Observe que se você já especificou um tipo de servidor toouse anteriormente, será limitado toochoosing apenas um servidor de nuvem que está em Olá mesma família de tipo de servidor. Mas se você não escolheu um tipo de servidor, você pode escolher qualquer um dos servidores de saudação que estão disponíveis no momento no Azure e o tipo de servidor de saudação será selecionado automaticamente para você.
3. Clique em **Okey** toosave suas alterações.

Se usar o hello **implantar a partir de um download personalizado** opção:

1. Certifique-se de que você já selecionou um tipo de servidor de acordo com o toohello etapas anteriores. Isso informa Olá plug-in como servidor de saudação toodeploy de seu download personalizado, como ele deve ser de saudação mesma família de seu tipo de servidor selecionado.
2. Marque caixa de seleção Olá denominada **implantar a partir de um download personalizado**.
    Se você quiser toodownload de sua conta de armazenamento do Azure, selecione a conta de armazenamento de saudação do hello **conta de armazenamento** lista suspensa (você pode clicar em Olá **contas** link toomodify o que está na lista de saudação), que preenche parcialmente Olá **URL** campo e, em seguida, preencha Olá restantes parte do servidor de tooyour URL Olá baixar ZIP (ao usar o armazenamento do Azure, nomes de blob na URL de saudação deve estar em minúscula). Se você não quiser toouse armazenamento do Azure, selecione **(nenhum)** de saudação **conta de armazenamento** suspensa lista e digite o download de servidor Olá URL tooyour ZIP em Olá **URL** campo. Olá ZIP contém uma pasta filho que representa o diretório de instalação do servidor de aplicativo. Por exemplo, se você estiver usando um zip para o Apache Tomcat 7.0.35, dentro de saudação zip seria Olá filho pasta representando Olá diretório de instalação, como **apache-tomcat-7.0.35**. 
3. Especifique o valor de Olá Olá diretório base variável de ambiente. O padrão será toohello valor usado para o servidor de aplicativo local, se houver, mas você pode especificar um valor diferente se o servidor de aplicativos de nuvem for diferente do seu servidor de aplicativo local. No entanto, você precisa toomake-se de que o servidor de aplicativos de nuvem é de saudação mesma família de tipo de servidor de saudação selecionado anteriormente.
    Se você atualizar seu zip de servidor de aplicativo de nuvem em Olá futura, você pode alterar manualmente o configuração do diretório base hello ou toohave-lo novamente corresponder a configuração local (se você alterou muito o seu servidor de aplicativo local).
4. Clique em **Okey** toosave suas alterações.

Olá subjacente lógica para que os itens aparecem na Olá **servidor** guia da saudação **configuração do servidor** página de propriedade pode ser personalizada. Este é um recurso avançado que você pode precisar se suas necessidades ultrapassam os valores padrão de saudação ou se você quiser tooadd outros servidores. lógica de saudação toocustomize, em Olá **servidor** caixa de diálogo, clique em Olá **personalizar** link. Isso fechará Olá **configuração do servidor** página de propriedades e abra Olá **componentsets.xml** arquivo no Eclipse, que você pode modificar como modelo de configuração de servidor de saudação tooextend necessários. Documentação para **componentsets.xml** está incluído no hello **componentsets.xml** próprio arquivo.

Se você estiver usando Olá **implantar meu servidor local (carregamento automático toocloud armazenamento)** opção:

1. Marque caixa de seleção Olá denominada **implantar meu servidor local (carregamento automático toocloud armazenamento)**.
2. Usando Olá **conta de armazenamento** lista suspensa, selecione **(automática)**. Se você especificar **(automática)** aqui, Olá Eclipse toolkit usará Olá mesma conta de armazenamento para o servidor como Olá um você selecionar para a implantação na Olá **publicar tooAzure** caixa de diálogo.
3. Clique em **Okey** toosave suas alterações.

Selecione um caminho de instalação do servidor em seu computador na Olá **caminho de servidor Local** caixa de texto se qualquer Olá seguintes condições forem verdadeiras:

* Você deseja tootest sua implantação no emulador de saudação (aplica-se somente a tooWindows).
* Você deseja toodeploy sua nuvem de toohello servidor instalado localmente.
* Você deseja toouse um download personalizado do servidor de nuvem hello, nesse caso, certifique-se também de saudação **implantar meu servidor local (carregamento automático toocloud armazenamento)** está selecionada acima.

Se nenhum dos Olá anterior opções se aplicar a situação tooyour, configuração do servidor local Olá é opcional.

### <a name="applications-configuration"></a>Configuração de aplicativos
a seguir Olá é um exemplo de como você pode especificar um aplicativo.

![][ic719512]

Clique em **adicionar** tooadd outro aplicativo, ou **remover** tooremove um aplicativo. Para fins de eficiência, se você quiser toouse um download para a origem de saudação de um aplicativo durante a implantação de nuvem toohello, usar Olá [propriedades de componentes](#components_properties) toospecify um URL, conta de armazenamento, etc. 

Começando com hello versão de abril de 2014, os aplicativos carregados automaticamente na Olá mesma conta de armazenamento (em Olá **eclipsedeploy** contêiner) como Olá selecionada para sua implantação. lógica de inicialização de saudação da sua implantação contém uma etapa que baixa primeiro esses aplicativos dessa conta de armazenamento. Isso significa que você pode atualizar seus aplicativos em sua implantação sem a necessidade de toorebuild e reimplante o pacote inteiro do hello, carregando manualmente as versões mais recentes do aplicativo hello diretamente na conta de armazenamento (por exemplo hello portal do Azure usando) , substituir arquivos WAR de saudação originalmente carregados pelo Kit de ferramentas de saudação. Em seguida, basta inicie Olá a reciclagem de todas as instâncias de função usando o portal de gerenciamento do Azure novamente ou através de utilitários de linha de comando. (Disparar a reciclagem de função diretamente de dentro do Kit de ferramentas Olá não há atualmente suporte.)

### <a name="notes-about-server-configuration"></a>Observações sobre a configuração do servidor
As alterações feitas por meio de saudação **configuração do servidor** página de propriedades serão refletidas no hello `<component>` elementos do arquivo package.xml de saudação.

Quando você usa Olá **carregar automaticamente...**  ou **implantar a partir de download...**  opções para hello JDK ou servidor de aplicativos e você estiver criando para nuvem hello (não emulador de computação Olá) e são conectados toohello rede, você pode perceber construir mensagens como seguinte Olá Olá Console de saída, como Olá Ant Construtor de relatórios verifica a disponibilidade do download hello:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

Se você selecionou Olá **implantar a partir de download...**  opção Olá aviso a seguir pode ser exibido, mas Olá compilação irá continuar:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

Esse aviso é Olá única indicação Olá disponibilidade do download ainda não foi verificada. Portanto, se uma implantação falhar na nuvem Olá por algum motivo, verifique toosee se você recebeu esse aviso.

Se você quiser toodisable verificação de download de saudação (por exemplo, se você se sentir desnecessariamente lenta compilação Olá), defina hello `verifydownloads` atributo muito`false` em Olá `<windowsazurepackage>` elemento de package.xml: 

`<windowsazurepackage verifydownloads="false" ...>` 

Se você selecionou Olá **carregar automaticamente...**  opção, em seguida, na janela de console Olá você verá mensagens de compilação relatar o andamento de saudação do carregamento de saudação a cada 5 segundos, sempre que um carregamento é necessário.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>Propriedades de descarregamento de SSL
Abra o menu de contexto de saudação de função hello no painel Explorador de projeto do Eclipse, clique em **Azure**e, em seguida, clique em **descarregamento de SSL**. 

![][ic719481]

Na caixa de diálogo, você pode habilitar o SSL descarregamento, permitindo que você tooeasily Habilitar suporte a HTTPS Hypertext Transfer Protocol Secure () na sua implantação do Java no Azure, sem exigir que você tooconfigure SSL em seu servidor de aplicativos Java. Para obter mais informações, consulte [descarregamento de SSL] [ SSL Offloading] e [como tooUse descarregamento de SSL][How tooUse SSL Offloading].

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Propriedades do Projeto do Azure][Azure Project Properties]

[Lista de contas de armazenamento do Azure][Azure Storage Account List]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
