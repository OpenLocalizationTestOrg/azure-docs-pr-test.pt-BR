---
title: aaaIntro tooMicrosoft do Azure | Microsoft Docs
description: "Novo tooMicrosoft do Azure? Obter uma visão geral da saudação serviços ofertas com exemplos de como eles são úteis."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Apresentando o Microsoft Azure
Microsoft Azure é uma plataforma de aplicativos da Microsoft para a nuvem pública hello.  Olá objetivo deste artigo é toogive é uma base para entender os conceitos básicos de saudação do Azure, mesmo se você não sabe nada sobre a computação em nuvem.

**Como tooread neste artigo**

Azure está crescendo todo o tempo de saudação, portanto, é fácil tooget sobrecarregado.  Iniciar com serviços básicos hello, que são listados primeiro neste artigo e, em seguida, vá tooadditional serviços. Isso não significa que você não pode usar apenas os serviços adicionais do hello por si só, mas serviços básicos Olá compõem o núcleo de saudação de um aplicativo em execução no Azure.

**Fornecer feedback**

Seu feedback é importante. Este artigo deve oferecer a você uma visão geral eficaz do Azure. Se não estiver, conte-na seção de comentários Olá final Olá Olá página. Fornecem alguns detalhes sobre o que você esperava toosee e como tooimprove Olá artigo.  

## <a name="hello-components-of-azure"></a>Olá componentes do Azure
Azure grupos de serviços em categorias em Olá Portal de gerenciamento e em vários recursos visuais como Olá [o que é o Infográfico do Azure](https://azure.microsoft.com/documentation/infographics/azure/) . Olá Portal de gerenciamento é usada toomanage mais (mas não todos) serviços no Azure.

Este artigo usará um **organização diferente** tootalk sobre os serviços com base em função semelhante e toocall serviços subseção importante que fazem parte de maiores.  

![Componentes do Azure](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Figura: o Azure fornece serviços de aplicativos acessíveis pela Internet, sendo executados em datacenters do Azure.*

## <a name="management-portal"></a>Portal de Gerenciamento
O Azure tem uma interface da web chamada hello [Portal de gerenciamento](http://manage.windowsazure.com) que permite que os administradores tooaccess e administrar os recursos de maioria, mas não tudo do Azure.  Normalmente, a Microsoft lança portal na versão beta do hello mais recente da interface do usuário antes de desativar mais antiga. Hello mais recente é chamado hello ["Portal de visualização do Azure"](https://portal.azure.com/).

Geralmente, há uma grande sobreposição quando ambos os portais estão ativos. Embora os serviços essenciais apareçam nos dois portais, nem todas as funcionalidades estão presentes em ambos. Serviços mais recentes poderão ser exibidos na Olá serviços mais recentes portal primeiro e mais antigos e funcionalidade só pode existir em hello mais antigos.  mensagem de saudação aqui é que se você não encontrar algo no portal mais antigo de hello, verificar hello mais recente e vice-versa.

## <a name="compute"></a>Computação
Uma das coisas mais básicas de saudação que uma plataforma de nuvem é executar aplicativos. Cada um dos modelos de computação do Azure Olá tem sua própria tooplay de função.

Você pode usar essas tecnologias separadamente ou combiná-las conforme necessário base certa Olá de toocreate para seu aplicativo. abordagem de saudação escolhida depende em quais problemas você está tentando toosolve.

### <a name="azure-virtual-machines"></a>Máquinas Virtuais do Azure
![Máquinas Virtuais do Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Figura: Máquinas virtuais do Azure dá controle total sobre as instâncias de máquina virtual na nuvem hello.*

Olá capacidade toocreate uma máquina virtual sob demanda, se a partir de uma imagem padrão ou um que você fornecer, pode ser muito útil. Essa abordagem, geralmente conhecida como Infraestrutura como Serviço (IaaS), é fornecida pelas Máquinas Virtuais do Azure. A Figura 2 mostra uma combinação de como uma máquina Virtual (VM) é executado e toocreate em um VHD.  

toocreate uma VM, você especificar quais VHD toouse e hello do tamanho da VM.  Você, em seguida, paga por tempo de saudação que Olá que VM está em execução. Você paga por minuto hello e apenas enquanto estiver em execução, embora não haja uma taxa mínima de armazenamento para manter Olá VHD disponível. O Azure oferece uma galeria de estoque VHDs (chamados de "imagens") que contêm um toostart de sistema operacional inicializável do. Estas incluem opções da Microsoft e de parceiros, como o Windows Server e Linux, SQL Server, Oracle e muitos outros. Você está livre toocreate VHDs e imagens e, em seguida, carregá-los por conta própria. Você pode até mesmo carregar VHDs que contém somente dados e acessá-los a partir de suas VMs em execução.

Independentemente de onde vêm Olá VHD, você pode armazenar persistentemente todas as alterações feitas enquanto uma VM está em execução. Olá próxima vez que você criar uma máquina virtual em que o VHD, coisas escolher onde parou. Olá VHDs que volta Olá máquinas virtuais são armazenados em blobs de armazenamento do Azure, falamos sobre mais tarde.  Isso significa que você obter redundância tooensure que suas VMs não desaparecem devido a falhas de disco e toohardware. É também possível toocopy Olá alterado VHD fora do Azure, em seguida, executá-lo localmente.

Seu aplicativo é executado em uma ou mais máquinas virtuais, dependendo de como você criou antes ou decide toocreate-lo desde o início agora.

Este toocloud abordagem bastante geral computação pode ser usado tooaddress muitos problemas diferentes.

**Cenários para máquina virtual**

1. **Desenvolvimento/teste** -você pode usar toocreate uma plataforma de desenvolvimento e teste de baixo custo que você pode desligar quando tiver terminado de usá-lo. Também é possível criar e executar aplicativos que usem qualquer linguagem e biblioteca de sua preferência. Esses aplicativos podem usar qualquer uma das opções de gerenciamento de dados de saudação que o Azure fornece, e você também pode escolher toouse do SQL Server ou outro DBMS em execução em uma ou mais máquinas virtuais.
2. **Mover aplicativos tooAzure (comparação de precisão e shift)** -"Comparação de precisão e shift" refere-se toomoving seu aplicativo muito como você usaria uma toomove empilhadeira um objeto grande.  Você "comparação de precisão" hello VHD do data center local e "shift"-tooAzure e executá-lo lá.  Você geralmente terá toodo algumas dependências de tooremove trabalho em outros sistemas. Se houver muitas você pode escolher, em vez dessa opção, a opção 3.  
3. **Estenda seu Datacenter** - Use as VMs do Azure como uma extensão do seu datacenter local, executando o SharePoint ou outros aplicativos. toosupport isso, é possível toocreate domínios do Windows na nuvem hello, executando o Active Directory em máquinas virtuais do Azure. Você pode usar rede Virtual do Azure (mencionado mais tarde) tootie sua rede local e sua rede no Azure juntos.

### <a name="web-apps"></a>Aplicativos Web
![Aplicativos Web do Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Figura: Aplicativos da Web do Azure executa um aplicativo de site na nuvem Olá sem a necessidade de servidor de web toomanage Olá subjacente.*

Um coisas hello mais comuns que as pessoas na nuvem Olá é executar sites e aplicativos web. Máquinas virtuais do Azure permite isso, mas ainda resta com responsabilidade de saudação da administração de uma ou mais máquinas virtuais e Olá sistemas operacionais de base. As funções web dos serviços de nuvem podem fazer isso, mas implantá-las e mantê-las ainda exige trabalho administrativo.  Se você quiser apenas um site em que outra pessoa cuida de trabalho administrativo de saudação para você?

Isso é exatamente o que fornecem os aplicativos Web. Esse modelo de computação oferece um ambiente da web gerenciado usando o portal de gerenciamento do Azure do hello, bem como APIs. Você pode mover um aplicativo existente do site para aplicativos Web inalterados, ou você pode criar um novo diretamente na nuvem de saudação. Quando um site estiver em execução, você pode adicionar ou remover instâncias dinamicamente, depender equilibrar solicitações de aplicativos Web do Azure tooload entre eles. Aplicativos do Azure oferece uma opção compartilhada, em que seu site é executado em uma máquina virtual com outros sites, e uma opção padrão que permite que um site toorun em sua própria máquina virtual. opção de saudação padrão também permite aumentar o tamanho de saudação (computação de energia) das instâncias se necessário.

Para desenvolvimento, os Aplicativos Web dão suporte para .NET, PHP, Node.js, Java e Python, juntamente com o Banco de Dados SQL e o MySQL (da ClearDB, uma parceira da Microsoft) para armazenamento relacional. Eles também fornecem suporte interno para vários aplicativos conhecidos, incluindo WordPress, Joomla e Drupal. meta de saudação é tooprovide um baixo custo, escalonável e plataforma amplamente úteis para a criação de sites e aplicativos web na nuvem pública hello.

**Cenários de Aplicativos Web**

Os aplicativos Web é pretendido toobe útil para empresas, os desenvolvedores e órgãos de design de web. Para empresas, é uma solução fácil de gerenciar, flexível, altamente segura e altamente disponível para a execução de sites da web de presença. Quando você precisar tooset um site, é melhor toostart com aplicativos Web do Azure e continuar serviços tooCloud depois que você precisa de um recurso que não está disponível. Consulte a seção "Computação" Olá para obter mais links que podem ajudar você toochoose entre as opções de Olá Olá final.

### <a name="cloud-services"></a>Serviços de Nuvem
![Serviço de Nuvem do Azure](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Figura: Serviços de nuvem do Azure fornece um local toorun altamente escalonável personalizado código em uma plataforma como um ambiente de serviço (PaaS)*

Suponha que você queira toobuild um aplicativo em nuvem que pode dar suporte a vários usuários simultâneos, não requer muito administração e nunca fica inoperante. Você pode ser um fornecedor de software estabelecida, por exemplo, isso decidiu tooembrace Software como serviço (SaaS) com a criação de uma versão de um de seus aplicativos na nuvem de saudação. Ou você pode ser um iniciante criando um aplicativo de consumidor com grandes expectativas de que ele cresça rapidamente. Se estiver desenvolvendo com o Azure, que modelo de execução você deve usar?

Os Aplicativos Web do Azure permitem criar esse tipo de aplicativo Web, mas há algumas restrições. Por exemplo, se você não tiver acesso administrativo, significa que não poderá instalar softwares arbitrários. Máquinas virtuais do Azure oferece muita flexibilidade, incluindo acesso administrativo e você certamente pode usá-lo toobuild um aplicativo muito escalonável, mas você terá toohandle muitos aspectos de confiabilidade e administração por conta própria. O que você gostaria que é uma opção que lhe Olá controle você precisa, mas também lida com a maior parte do trabalho Olá necessário para a confiabilidade e administração.

Isso é exatamente o que é fornecido pelos Serviços de Nuvem do Azure. Essa tecnologia é projetado expressamente toosupport escalonável, confiável e aplicativos de baixa-admin, e é um exemplo do que é comumente chamado plataforma como um serviço (PaaS). toouse, criar um aplicativo usando a tecnologia de saudação sua escolha, como c#, Java, PHP, Python, Node.js ou alguma outra coisa. Seu código é executado em máquinas virtuais (chamados tooas instâncias) executando uma versão do Windows Server.

Mas essas VMs são diferentes de saudação aqueles que você cria com as máquinas virtuais do Azure. Em primeiro lugar, o Azure em si as gerencia, realizando tarefas como instalar patches do sistema operacional e implantar automaticamente novas imagens com patches. Isso implica que seu aplicativo não deve manter o estado nas instâncias de função web ou de trabalho; em vez disso, ele deve ser mantido em uma das opções de gerenciamento de dados do Azure Olá descritas na próxima seção, Olá. O Azure também monitora essas VMs, reiniciando todas que falharem. Você pode definir uma nuvem serviços tooautomatically criar instâncias de mais ou menos em toodemand de resposta. Isso permite que você toohandle maior uso e escala para não pagar tanta quando houver menos uso.

Você tem dois toochoose de funções de quando você cria uma instância, baseadas no Windows Server. Olá principal diferença entre Olá duas é que uma instância de uma função web executa o IIS, mas não uma instância de uma função de trabalho. Ambos são gerenciadas no hello mesma forma, no entanto e do comuns para um toouse aplicativo ambos os. Por exemplo, uma instância de função web pode aceitar solicitações de usuários e passá-las tooa instância de função de trabalho para processamento. tooscale seu aplicativo para cima ou para baixo, você pode solicitar que o Azure criar mais instâncias de qualquer uma dessas funções ou desligar as instâncias existentes. E tooAzure semelhante máquinas virtuais, você será cobrado somente para o tempo de saudação se cada instância de função web ou de trabalho está em execução.

**Cenários para serviços de nuvem**

Serviços de nuvem são expandir grandes toosupport ideal quando você precisa de mais controle sobre a plataforma de saudação que a fornecida por aplicativos Web do Azure, mas não precisa de controle do sistema operacional subjacente hello.

#### <a name="choosing-a-compute-model"></a>Escolhendo um Modelo de Computação
página Olá [comparação de aplicativos Web do Azure, serviços de nuvem e máquinas virtuais](app-service-web/choose-web-site-cloud-service-vm.md) fornece informações mais detalhadas sobre como toochoose um modelo de computação.

## <a name="data-management"></a>Gerenciamento de Dados
Os aplicativos precisam de dados, e diferentes tipos de aplicativos precisam de diferentes tipos de dados. Por isso, o Azure fornece toostore de várias maneiras diferentes e gerenciar dados. O Azure oferece muitas opções de armazenamento, mas todas são projetadas para serem armazenamento muito durável.  Com qualquer uma dessas opções, sempre há 3 cópias de seus dados mantidas em sincronia em um datacenter do Azure - 6, se você permitir que o Azure toouse redundância geográfica tooback backup tooanother datacenter, pelo menos, 300 milhas de distância.     

### <a name="in-virtual-machines"></a>Nas Máquinas Virtuais
Olá capacidade toorun do SQL Server ou outro DBMS em uma VM criada com as máquinas virtuais do Azure já mencionado. Observe que essa opção não está limitado toorelational sistemas; Você também está livre toorun NoSQL tecnologias como MongoDB e Cassandra. Executar seu próprio sistema de banco de dados é simples-it replica o que estamos usado tooin nossos datacenters- mas também requer tratamento de administração de saudação do que DBMS.  Em outras opções, o Azure lida com mais ou toda a administração Olá para você.

Novamente, o estado de saudação do hello Máquina Virtual e qualquer disco de dados adicionais que você cria ou carrega são apoiadas pelo repositório de blob (que falamos sobre posteriormente).  

### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure
![Banco de dados SQL de armazenamento do Azure](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Figura: O banco de dados SQL do Azure fornece um serviço gerenciado de banco de dados relacional na nuvem hello.*

Para armazenamento relacional, o Azure fornece o recurso de saudação banco de dados SQL. Não deixe de nomenclatura Olá enganá-lo. Isso é diferente de um banco de dados SQL comum, fornecido pelo SQL Server e sendo executado sobre o Windows Server.  

Chamado anteriormente SQL Azure, banco de dados do SQL Azure fornece todos Olá os principais recursos de um RDBMS, inclusive transações atômicas, acesso a dados simultâneo por vários usuários com uma programação familiar, integridade de dados e consultas SQL ANSI modelo. Assim como o SQL Server, o Banco de Dados SQL pode ser acessado usando o Entity Framework, ADO.NET, JDBC, entre outras tecnologias conhecidas de acesso a dados. Ele também dá suporte a maioria das Olá linguagem T-SQL, junto com as ferramentas do SQL Server como o SQL Server Management Studio. Para qualquer pessoa familiarizada com o SQL Server (ou outro banco de dados relacional), usar o Banco de Dados SQL é fácil.

Mas o banco de dados SQL não é apenas um DBMS em Olá nuvem-it de um serviço de PaaS. Você ainda controlar seus dados e quem pode acessá-lo, mas o banco de dados SQL cuida de trabalho do assistente administrativo hello, como gerenciar a infraestrutura de hardware hello e manter automaticamente o software de banco de dados e sistema operacional de saudação backup toodate. O Banco de Dados SQL também fornece uma alta disponibilidade, backups automáticos, capacidade de restauração a um ponto no tempo e também pode fazer a replicação de cópias através de regiões geográficas.  

**Cenários para banco de dados SQL**

Se você estiver criando um aplicativo do Azure (usando qualquer um dos modelos de computação Olá) que precisa de armazenamento relacional, banco de dados SQL pode ser uma boa opção. Aplicativos em execução nuvem Olá externa também podem usar esse serviço, no entanto, portanto, há muitos outros cenários. Por exemplo, os dados armazenados no Banco de Dados SQL podem ser acessados em diferentes sistemas cliente, incluindo desktops, laptops, tablets e telefones. E como essa tecnologia fornece alta disponibilidade interna por meio da replicação, usar o Banco de Dados SQL pode ajudar a minimizar o tempo de inatividade.

### <a name="tables"></a>Tabelas
![Tabelas de armazenamento do Azure](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Figura: Tabelas do Azure fornece um simples NoSQL maneira toostore de dados.*

Esse recurso às vezes é chamado por nomes diferentes, já que é parte de um recurso mais amplo chamado “Armazenamento do Azure". Se você vir "tabelas", "Tabelas do Azure" ou "tabelas de armazenamento", é todos os Olá a mesma coisa.  

E não confundir pelo nome da saudação: esta tecnologia não fornece armazenamento relacional. Na verdade, é um exemplo de uma abordagem NoSQL chamada de armazenamento de chave/valor. As Tabelas do Azure permitem que um aplicativo armazene propriedades de vários tipos, como cadeia de caracteres, inteiros e datas. Assim, um aplicativo pode recuperar um grupo de propriedades fornecendo uma chave exclusiva para esse grupo. Enquanto as operações complexas que não há suporte para junções, tabelas oferecem dados de tootyped de acesso rápido. Eles também são muito escalonáveis, com um toohold capaz de tabela única quanto um terabyte de dados. E correspondência de sua simplicidade, as tabelas são toouse geralmente é mais barato que o armazenamento relacional do banco de dados SQL.

**Cenários para tabelas**

Suponha que você queira toocreate um aplicativo do Azure que precisa rapidamente acessar dados de tootyped, talvez ele muitas, mas não precisa de consultas SQL complexas de tooperform nesses dados. Por exemplo, imagine que você está criando um aplicativo do consumidor que precisa de informações de perfil de cliente toostore para cada usuário. Seu aplicativo irá toobe muito popular, portanto você precisa tooallow grandes quantidades de dados, mas não muito com esses dados, além de fazê-lo, em seguida, recuperá-los de maneiras simples. Isso é exatamente o tipo de saudação do cenário em tabelas do Azure faz sentido.

### <a name="blobs"></a>Blobs
![Blobs de armazenamento do Azure](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Figura: os Blobs do Azure fornecem dados binários não estruturados.*  

Blobs do Azure (novamente "Armazenamento de Blob" e apenas o "armazenamento de Blobs" são Olá mesmo) é projetado toostore dados binários não estruturados. Assim como as Tabelas, os Blobs fornecem armazenamento barato; além disso, um único blob pode ter tamanho de até 1 TB (um terabyte). Os aplicativos do Azure também podem usar unidades do Azure, que permitem aos blobs fornecer armazenamento persistente para um sistema de arquivos do Windows montado em uma instância do Azure. aplicativo Hello vê arquivos comuns do Windows, mas conteúdo hello, na verdade, é armazenado em um blob.

O Armazenamento de Blob é utilizado por muitos outros recursos do Azure (incluindo Máquinas Virtuais), de modo que pode, com certeza, dar conta também das cargas de trabalho usadas por você.

**Cenários para blobs**

Um aplicativo que armazena vídeos, arquivos massivos ou outras informações binárias pode usar blobs para armazenamento simples e barato. Os blobs são utilizados frequentemente em conjunção com outros serviços como a CDN (Rede de Distribuição de Conteúdo), sobre a qual falaremos posteriormente.  

### <a name="import--export"></a>Importar/Exportar
![Serviço Importar/Exportar do Azure](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Figura: Importação do Azure exportação fornece Olá capacidade tooship um tooor de disco rígido físico do Azure para exportação ou importação de dados em massa mais rápido e mais barato.*  

Às vezes, você deseja toomove muitos dados no Azure. Isso levaria muito tempo, talvez dias, além de usar muita largura de banda. Nesses casos, você pode usar a importação/exportação do Azure, que permite que você tooship criptografados pelo Bitlocker 3.5" discos rígidos SATA diretamente tooAzure centros de dados, em que o Microsoft transferirá Olá dados no armazenamento de blob para você.  Após o carregamento de hello, a Microsoft fornece Olá unidades back tooyou.  Você também pode solicitar que grandes quantidades de dados do armazenamento de Blob ser exportadas em unidades de disco rígido e enviadas tooyou back via email.

**Cenários para importação/exportação**

* **Migração de dados grandes** - sempre que você tiver grandes quantidades de dados (Terabytes) que você deseja tooupload tooAzure, Olá serviço de importação/exportação geralmente é muito mais rápido e talvez mais barato do que transferi-lo sobre Olá internet. Quando dados saudação estão blobs, você pode processá-lo em outros formulários, como o armazenamento de tabela ou um banco de dados do SQL.
* **Arquivado recuperação de dados** -você pode usar a importação/exportação toohave Microsoft transferem grandes quantidades de dados armazenados no armazenamento de BLOBs do Azure tooa dispositivo de armazenamento que você envia e, em seguida, ter esse dispositivo entregues tooa back local desejado. Já que isso levará algum tempo, essa não é uma boa opção para recuperação de desastres. Ela é uma opção melhor para dados arquivados, para os quais você não precisa de acesso rápido.

### <a name="file-service"></a>Serviço de arquivos
![Serviço de Arquivos do Azure](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Figura: Serviços de arquivo do Azure fornece SMB \\ \\servidor\compartilhamento. caminhos para aplicativos em execução na nuvem hello.*

No local, é comum toohave grandes quantidades de armazenamento de arquivo acessível por meio de protocolo usando o bloco de mensagens de servidor (SMB) Olá um \\ \\servidor\compartilhamento. formato. Azure agora tem um serviço que permite a você toouse esse protocolo em nuvem hello. Aplicativos em execução no Azure podem usá-lo tooshare arquivos entre máquinas virtuais usando o sistema de arquivos familiar APIs como ReadFile e WriteFile. Além disso, os arquivos de saudação também podem ser acessados em Olá simultaneamente por meio de uma interface REST, que permite que você tooaccess Olá compartilhamentos do local ao configurar uma rede virtual também. Arquivos do Azure baseia-se ao serviço de blob hello, portanto ela herda Olá mesmo disponibilidade, a durabilidade, escalabilidade e redundância geográfica embutido no armazenamento do Azure.

**Cenários para arquivos do Azure**

* **Migrando nuvem existente de toohello aplicativos** -o mais fácil toomigrate aplicativos toohello nuvem local que use o arquivo compartilha dados de tooshare entre partes do aplicativo hello. Cada VM conecta toohello compartilhamento de arquivos e, em seguida, ele pode ler e gravar arquivos exatamente como ele faria em relação a um arquivo local no compartilhamento.
* **Configurações de aplicativo compartilhadas** -um padrão comum para aplicativos distribuídos é toohave arquivos de configuração em um local centralizado onde eles podem ser acessados de diversas máquinas virtuais. Esses arquivos de configuração podem ser armazenados em um compartilhamento de Arquivo Azure e lido por todas as instâncias de aplicativo. configurações de saudação também podem ser gerenciadas por meio da interface REST hello, o que permite o acesso em todo o mundo toohello arquivos de configuração.
* **Compartilhamento de Diagnóstico** - você pode compartilhar e salvar arquivos de diagnóstico como logs, métricas e despejo de memória. Esses arquivos disponíveis por meio de saudação SMB e a interface REST permite que aplicativos toouse uma variedade de ferramentas de análise para processamento e análise de dados de diagnóstico de saudação.
* **Desenvolvimento/teste/Debug** - quando os desenvolvedores ou administradores estão trabalhando em máquinas virtuais na nuvem hello, muitas vezes eles precisam de um conjunto de ferramentas ou utilitários. Instalar e distribuir esses utilitários em cada máquina virtual leva muito tempo. Com os arquivos do Azure, um desenvolvedor ou administrador pode armazenar suas ferramentas favoritas em um compartilhamento de arquivo e conectar toothem em qualquer máquina virtual.

## <a name="networking"></a>Rede
Azure é executado atualmente em vários data centers espalhados Olá, mundo. Quando você executa um aplicativo ou armazena dados, você pode selecionar um ou mais desses toouse datacenters. Você também pode conectar os datacenters toothese de várias maneiras, usando os serviços de saudação abaixo.

### <a name="virtual-network"></a>Rede Virtual
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Figura: Redes virtuais fornece uma rede privada na nuvem Olá para que diferentes serviços podem se comunicar tooeach outra ou a recursos locais tooon se você configurar uma conexão entre locais VPN.*  

Uma maneira útil toouse uma nuvem pública é tootreat-lo como uma extensão de seu próprio data center.

Como é possível criar VMs sob demanda e depois removê-las (e parar de pagar) quando elas não forem mais necessárias, você pode ter o poder da computação somente quando desejá-la. E, como máquinas virtuais do Azure permite que você crie VMs que executam o SharePoint, Active Directory e outro software local familiar, essa abordagem pode trabalhar com aplicativos Olá que você já tiver.

toomake este muito útil, no entanto, os usuários deve tootreat capaz de toobe esses aplicativos como se estivessem sendo executados em seu próprio datacenter. Isso é exatamente o que a Rede Virtual do Azure permite. Usando um dispositivo de gateway VPN, um administrador pode configurar uma rede virtual privada (VPN) entre sua rede local e suas VMs que são implantados tooa a rede virtual no Azure. Como atribuir seu próprio IP v4 endereços toohello nuvem VMs, elas são exibidas toobe em sua rede. Usuários em sua organização podem acessar aplicativos Olá essas VMs contêm como se estivessem sendo executados localmente.

Para obter mais informações sobre planejamento e criação de uma rede virtual que funciona para você, consulte [Rede Virtual](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>Rota Expressa
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Figura: Rota expressa usa uma rede Virtual do Azure, mas as conexões de rotas por meio de linhas em vez de dedicadas mais rápido Olá Internet pública.*  

Se você precisa de mais largura de banda ou segurança do que a oferecida por uma conexão de Rede Virtual do Azure, considere o ExpressRoute. Em alguns casos, o ExpressRoute também pode economizar o seu dinheiro. Você ainda precisará de uma rede virtual no Azure, mas Olá link entre o Azure e seu site usa uma conexão dedicada que não passa pelo Olá Internet pública. Em ordem toouse esse serviço, você precisará toohave um contrato com um provedor de serviços de rede ou um provedor do exchange.

Configurando uma conexão de rota expressa requer mais tempo e planejamento, portanto, talvez você queira toostart com uma VPN site a site, em seguida, migrar tooan conexão de rota expressa.

Para obter mais informações sobre o ExpressRoute, consulte [Visão Geral Técnica do ExpressRoute](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Gerenciador de Tráfego
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Figura: Azure Traffic Manager permite que você tooroute tráfego global tooyour serviço com base nas regras inteligentes.*

Se seu aplicativo do Azure é executado em vários datacenters, você pode usar o Azure Traffic Manager tooroute solicitações de usuários inteligentemente em instâncias do aplicativo hello. Você também pode rotear o tráfego tooservices não em execução no Azure, desde que eles são acessíveis de Olá da internet.  

Um aplicativo do Azure com usuários em uma única parte de Olá, mundo pode ser executado em apenas um datacenter do Azure. Um aplicativo com usuários espalhados Olá, mundo, no entanto, é mais provável toorun em vários datacenters, talvez ainda todos eles. Neste segundo caso, você enfrentar um problema: como você inteligente direcionar instâncias de tooapplication usuários? A maioria do tempo de saudação, provavelmente desejará cada usuário tooaccess Olá datacenter mais próximo tooher, desde que ele provavelmente fornecerá seu tempo de resposta melhor hello. Mas e se essa instância do aplicativo hello está sobrecarregado ou indisponível? Nesse caso, seria possível toodirect adequado a solicitação automaticamente tooanother datacenter. O Gerenciador de Tráfego do Azure faz exatamente isso.

proprietário de saudação de um aplicativo define regras que especifique como solicitações de usuários devem ser direcionado toodatacenters e depende do Traffic Manager toocarry out essas regras. Por exemplo, os usuários normalmente podem ser direcionado toohello data center mais próximo do Azure, mas são enviados tooanother um quando o tempo de resposta de saudação do seu datacenter de padrão excede o tempo de resposta de saudação de outros datacenters. Para aplicativos globalmente distribuídos com muitos usuários, é útil com problemas de toohandle um serviço interno como estes.

O traffic manager usa pontos de extremidade do serviço de nomes de diretório (DNS) tooroute usuários tooservice, mas ainda mais tráfego não passa pelo Traffic Manager depois que essa conexão é estabelecida. Isso impede que o Gerenciador de Tráfego atue como um gargalo que tornará suas comunicações de serviço lentas.

## <a name="developer-services"></a>Serviços para Desenvolvedores
Azure oferece um número de ferramentas toohelp desenvolvedores e profissionais de TI criar e manter aplicativos em nuvem hello.  

### <a name="azure-sdk"></a>SDK do Azure
Em 2008, hello primeira versão de pré-lançamento do Azure tem suporte apenas a desenvolvimento .NET. Hoje, no entanto, você pode criar aplicativos do Azure em praticamente qualquer linguagem. Atualmente, a Microsoft fornece SDKs específicos a cada linguagem para .NET, Java, PHP, Node. js, Ruby e Python. Também há um SDK geral do Azure que fornece suporte básico para qualquer linguagem, como C++.  

Estes SDKs vão ajudá-lo a desenvolver, implantar e gerenciar aplicativos do Azure. Eles estão disponíveis em [www.microsoftazure.com](https://azure.microsoft.com/downloads/) ou no GitHub e podem ser usados com o Visual Studio e o Eclipse. O Azure também oferece ferramentas de linha de comando que os desenvolvedores podem usar com qualquer ambiente de desenvolvimento ou editor, incluindo ferramentas de implantação de aplicativos tooAzure de sistemas Linux e Macintosh.

Além de ajudar a desenvolver aplicativos Azure, estes SDKs também oferecem bibliotecas de cliente que ajudam você a criar software que use os serviços do Azure. Por exemplo, você pode criar um aplicativo que lê e grava os blobs do Azure ou criar uma ferramenta que implanta aplicativos do Azure por meio da interface de gerenciamento do Azure hello.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services é um nome de marketing que abrangem um número serviços que ajudam a aplicativos toodevelop hello Azure.

tooavoid confusão - ele não fornece uma versão hospedada ou baseado na Web do Visual Studio. Você ainda precisa de sua cópia do Visual Studio sendo executada localmente. Mas ela oferece muitas outras ferramentas, que podem ser muito úteis.

Ela inclui um sistema de controle do código-fonte hospedado chamado Team Foundation Service, que oferece um controle de versão e acompanhamento de itens de trabalho.  Você pode até mesmo utilizar o Git para controle de versão, se preferir. E você pode variar o sistema de controle de origem Olá que use por projeto. Você pode criar projetos de equipe particulares ilimitados acessível em qualquer lugar no Olá, mundo.  

O Visual Studio Team Services fornece um serviço de teste de carga. Você pode executar testes de carga criados no Visual Studio nas máquinas virtuais na nuvem hello. Especifique o número total de saudação de usuários que você deseja testar tooload com e do Visual Studio Team Services automaticamente determinar quantos agentes são necessários, criar máquinas virtuais de saudação necessários e executar seus testes de carga. Se você é um assinante do MSDN, você recebe milhares de minutos de usuário para teste de carga a cada mês.

O Visual Studio Team Services também dá suporte ao desenvolvimento rápido com recursos como compilações de integração contínua, quadros Kanban e salas de equipe virtual.

**Cenários do Visual Studio Team Services**

Visual Studio Team Services é uma boa opção para empresas que precisam de toocollaborate em todo o mundo e ainda não tiver infra-estrutura Olá no lugar toodo assim. Você pode concluir a configuração em minutos, escolher um sistema de controle do código-fonte e iniciar a gravação do código e a compilação no mesmo dia.  ferramentas do team Olá oferecem um local para a coordenação e colaboração e ferramentas adicionais de saudação fornecem análise Olá necessário tootest e ajustar seu aplicativo rapidamente.

Mas, as organizações que já têm um sistema local podem testar novos projetos no Visual Studio Team Services toosee se é mais eficiente.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Figura: o Application Insights monitora o desempenho e o uso de seu aplicativo ativo da Web ou de dispositivo.*

Ao publicar seu aplicativo, seja ele executado em dispositivos móveis, em desktops ou em navegadores da Web, o Application Insights informa o desempenho dele e o que os usuários estão fazendo com ele. Ela manterá uma contagem de falhas e resposta lenta, alerta se Olá figuras cruzam os limites inaceitáveis e ajudarão-lo a diagnostica problemas.

Quando você desenvolve um novo recurso, planeje toomeasure o sucesso dos usuários. Analisando padrões de uso, você entende o que funciona melhor para seus clientes e aprimora seu aplicativo em todos os ciclos de desenvolvimento.

Embora esteja hospedado no Azure, o Application Insights funciona para uma grande e crescente variedade de aplicativos, no Azure e fora dele. Ambos os aplicativos Web J2EE e ASP.NET são abordados, bem como aplicativos para iOS, para Android, para OSX e para o Windows. Telemetria são enviadas de um SDK criado com o aplicativo hello, toobe analisados e exibidos no hello serviço Application Insights no Azure.

Se você quiser mais especializadas de análise, exporte Olá telemetria fluxo tooa banco de dados, ou tooPower BI ou qualquer outra ferramenta.

**Cenários do Application Insights**

Você está desenvolvendo um aplicativo. Pode ser um aplicativo Web ou um aplicativo de dispositivo ou um aplicativo de dispositivo com um back-end da Web.

* Ajustar o desempenho de saudação do seu aplicativo depois que ele é publicado ou enquanto estiver no teste de carga.  Application Insights agrega a telemetria de todas as instâncias de saudação instalada e apresenta gráficos de tempos de resposta de solicitação e contagens de exceção, tempos de resposta de dependência e outros indicadores de desempenho. Isso ajudará você a ajustar o desempenho do aplicativo. Você pode inserir o código tooreport dados mais específicos, se necessário.
* Detecte e diagnostique problemas em seu aplicativo ativo. Você poderá receber alertas por email se os indicadores de desempenho cruzarem os limites aceitáveis. Você pode investigar sessões de usuário específico, por exemplo toosee Olá solicitação causou uma exceção.
* Acompanhar o êxito de saudação de tooassess de uso de cada novo recurso. Quando você cria uma nova história de usuário, plano toomeasure quanto é usado, e se os usuários atingirem suas metas de esperado. Application Insights fornece dados de uso básico como modos de exibição de página da web, e você pode inserir a experiência do usuário do código tootrack hello mais detalhadamente.

### <a name="automation"></a>Automação
Ninguém gosta de tempo de toowaste fazendo Olá manual mesmo processa mais de uma vez. Automação do Azure fornece uma maneira para toocreate, monitorar, gerenciar e implantar recursos em seu ambiente do Azure.  

A automação usa "runbooks", que usa os fluxos de trabalho do Windows PowerShell (VS. PowerShell apenas regular) sob as coberturas de saudação. Runbooks são destinados a toobe executado sem interação do usuário. Fluxos de trabalho do PowerShell permite que o estado de saudação de um toobe script salvo em pontos de verificação ao longo de saudação maneira. Em seguida, se ocorrer uma falha, você não tem toostart um script de início de saudação. Você pode reiniciá-lo no último ponto de verificação de saudação. Isso economiza muito trabalho tentar identificador de script hello toomake cada falha possíveis.

**Cenários para automação**

Automação do Azure é manual boa opção tooautomate hello, demoradas, propensas a erros e tarefas repetidas com frequência no Azure.

### <a name="api-management"></a>Gerenciamento de API
Criar e publicar Interfaces do programador de aplicativo (APIs) em Olá internet é um tooapplications de serviços de tooprovide de maneira comum. Se esses serviços são resellable (por exemplo, os dados de clima), uma organização pode permitir que terceiros tooaccess esses mesmos serviços para uma taxa. À medida que dimensiona toomore parceiros, você geralmente precisa toooptimize e controlar o acesso.  Alguns parceiros talvez seja necessário até mesmo dados saudação em um formato diferente.

Gerenciamento de API do Azure facilita para as organizações toopublish APIs toopartners, funcionários e desenvolvedores de terceiros com segurança e em escala. Ele fornece um ponto de extremidade de API diferente e age como um proxy toocall Olá ponto de extremidade real ao fornecimento de serviços, como o armazenamento em cache, transformação, limitação e controle de acesso, agregação de análise.

**Cenários para Gerenciamento de API**

Digamos que sua empresa tem um conjunto de dispositivos que todos os dados são necessários toocall tooa back serviço central tooget – por exemplo, uma empresa de envio com dispositivos em cada caminhão na estrada hello.  Certamente empresa Olá desejará tooset backup de um sistema tootrack é caminhões próprios para que possa prever e atualizar o tempo de entrega confiável. Ela poderá saber quantos caminhões tem e planejar tudo adequadamente.  Cada caminhão precisará de um dispositivo que chama tooa a localização central com o posicionamento e a velocidade de dados e talvez mais.

Um cliente de saudação do envio da empresa provavelmente também se beneficiam de posicionamento dados.  Prezado cliente pode usá-lo tooknow quanto os produtos têm tootravel, onde eles presa, quanto eles pagar ao longo de determinadas rotas (se combinado com o que eles paga tooship). Saudação de envio da empresa agrega os dados já, muitos clientes podem pagar por ele.  Mas, em seguida, Olá envio da empresa deve tooprovide uma maneira toogive clientes Olá dados. Depois que eles fornecem acesso toocustomers, eles podem não ter controle sobre quantas vezes hello dados são consultados. Eles terão tooprovide regras sobre quem pode acessar os dados. Todas essas regras teria toobe incorporado sua API externa. É aqui que o Gerenciamento da API pode ajudar.  

## <a name="identity-and-access"></a>Identidade e Acesso
Trabalhar com identidade faz parte da maioria dos aplicativos. Saber quem um usuário é permite que um aplicativo decida como deve interagir com ele. Azure fornece serviços toohelp acompanhar identidade, bem como integrá-lo com repositórios de identidade, você pode já estar usando.

### <a name="active-directory"></a>Active Directory
Como a maioria dos serviços de diretório, o Active Directory do Azure armazena informações sobre usuários e organizações Olá pertencerem a. Permite aos usuários fazer logon, em seguida, fornece-los com os tokens podem passar tooapplications tooprove sua identidade. Ele também permite a sincronização de informações do usuário, sendo executado em locais de sua rede local. Enquanto os mecanismos de saudação e formatos de dados usados pelo Active Directory do Azure não são idênticos aos usados no Windows Server Active Directory, funções hello realiza são bastante semelhantes.

É importante toounderstand que Active Directory do Azure é projetado principalmente para uso por aplicativos de nuvem. Ele pode ser usado pelos aplicativos executados no Azure, por exemplo, em outras plataformas na nuvem. Ele também é usado pelos próprios aplicativos em nuvem da Microsoft, como os do Office 365. No entanto, se você quiser tooextend seu datacenter em nuvem hello usando máquinas virtuais do Azure e rede Virtual do Azure, Active Directory do Azure não escolha certa hello. Em vez disso, você desejará toorun Windows Server Active Directory em máquinas virtuais.

aplicativos toolet acessam informações Olá que ele contém, Active Directory do Azure fornece uma API RESTful chamado Azure Active Directory Graph. Essa API permite que os aplicativos em execução em todos os objetos de diretório de acesso de plataforma e relações de saudação entre eles.  Por exemplo, um aplicativo autorizado pode usar este toolearn API sobre um usuário, grupos de saudação que ele pertence ao e outras informações. Aplicativos também podem ver as relações entre usuários seus social gráfico-permitindo que eles mais inteligente trabalhar com conexões de saudação entre pessoas.

Outro recurso do serviço, controle de acesso diretório ativo do Azure, torna mais fácil para informações de identidade de tooaccept um aplicativo do Facebook, Google, Windows Live ID e outros provedores de identidade populares. Em vez de exigir Olá aplicativo toounderstand Olá dados diversos formatos e protocolos usados por cada um desses provedores, controle de acesso se traduz todos eles em um único formato comum. Ele também permite que um aplicativo aceite logons de um ou mais domínios Active Directory. Por exemplo, um fornecedor que oferece um aplicativo SaaS pode usar usuários do controle de acesso do Azure Active Directory toogive em cada um dos seus aplicativos de toohello de logon único aos clientes.

Os serviços de diretório são um suporte importante de uma computação local. Ele não deve ser surpreendente que também são importantes na nuvem hello.

### <a name="multi-factor-authentication"></a>Autenticação Multifator
![Autenticação Multifator do Azure](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Figura: Multi-Factor Authentication fornece funcionalidade de saudação para seu aplicativo tooverify mais de uma forma de identificação*

A segurança é sempre importante. A Multi-Factor Authentication (MFA) ajuda a garantir que somente os próprios usuários acessem suas contas. A MFA (também conhecida como autenticação em dois fatores ou "2FA") exige que os usuários forneçam dois desses três métodos de verificação de identidade, para logons e transações realizados por clientes.

* Algo que você sabe (normalmente, uma senha)
* Algo que você tem (um dispositivo confiável que não pode ser facilmente clonado, como um telefone)
* Algo seu (biometria)

Portanto, quando um usuário faz logon, você pode precisar deles tooalso verificar sua identidade com um aplicativo móvel, uma chamada telefônica ou uma mensagem de texto em combinação com sua senha. Por padrão, o Active Directory do Azure suporta o uso de saudação de senhas como seu único método de autenticação para entradas do usuário. Você pode usar a MFA junto com o AD do Azure ou aplicativos personalizados e diretórios usando Olá SDK de MFA. Você também pode utilizá-lo em conjunto com aplicativos locais, por meio do uso do servidor Multi-Factor Authentication.

**Cenários para MFA**

A proteção para logon em contas confidenciais, como logons bancários e acesso a código-fonte, nos quais uma entrada não autorizada poderia ter um elevado custo financeiro ou de propriedade intelectual.   

## <a name="mobile"></a>Móvel
Se você estiver criando um aplicativo para um dispositivo móvel, Azure pode ajudar a armazenar dados na nuvem hello, autenticar usuários e enviar notificações por push sem a necessidade de toowrite uma grande quantidade de código personalizado.

Enquanto você certamente pode criar hello back-end para um aplicativo móvel usando máquinas virtuais, serviços de nuvem ou aplicativos Web, você pode gastar muito menos Olá de gravação de tempo subjacente de componentes de serviço usando os serviços do Azure.

### <a name="mobile-apps"></a>Aplicativos Móveis
![Aplicativos Móveis](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Figura: os Aplicativos Móveis oferecem funcionalidades normalmente exigidas por aplicativos que fazem interface com dispositivos móveis.*

Os Aplicativos Móveis do Azure fornecem muitas funções úteis que podem poupar tempo ao criar um back-end para um aplicativo Móvel. Ele permite toodo provisionamento e gerenciamento simples de dados armazenados em um banco de dados SQL. Com o código do servidor, você pode facilmente usar opções de armazenamento de dados como armazenamento de blob ou MongoDB. Os Aplicativos Móveis dão suporte a notificações, apesar de, em determinados casos, ser possível usar também os Hubs de Notificação conforme descrito a seguir.  serviço de saudação também tem uma API REST que seu aplicativo móvel pode chamar tooget trabalho. Aplicativos móveis também fornece a capacidade de saudação tooauthenticate usuários por meio do Active Directory e Microsoft, bem como outros provedores de identidade conhecida como Facebook, Twitter e Google.   

Você pode usar outros serviços do Azure como o barramento de serviço e funções de trabalho e se conectar a sistemas locais tooon. Você ainda pode consumir 3º complementos de terceiros do hello funcionalidade adicional de tooprovide de armazenamento do Azure (como SendGrid para email).

Bibliotecas do Native client para Windows Store, Windows Phone, HTML/JavaScript, iOS e Android tornam mais fácil toodevelop para aplicativos em todas as principais plataformas móveis. Uma API REST permite toouse dados de serviços móveis e a funcionalidade de autenticação com aplicativos em diferentes plataformas. Um único serviço móvel pode dar suporte a múltiplos aplicativos clientes, de modo que você possa oferecer uma experiência de usuário consistente em todos os dispositivos.

Porque o Azure oferece suporte à expansão massiva já, você pode tratar tráfego hello como seu aplicativo se torna mais popular.  Há suporte para monitoramento e registro em log toohelp solucionar problemas e gerenciar o desempenho.

### <a name="notification-hubs"></a>Hubs de Notificação
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Figura: os Hubs de Notificação oferecem funcionalidades normalmente exigidas por aplicativos que fazem interface com dispositivos móveis.*

Enquanto você pode escrever código toodo notificações em aplicativos móveis do Azure, os Hubs de notificação é otimizada toobroadcast milhões de notificações por push altamente personalizados em minutos.  Você não tem tooworry sobre detalhes como operadora móvel ou fabricante do dispositivo. Você pode visar indivíduos ou milhões de usuários com uma única chamada à API.

Hubs de notificação é projetado toowork com qualquer back-end. Você pode usar os aplicativos móveis do Azure, um back-end personalizado na nuvem de saudação em execução em qualquer provedor ou um back-end no local.

**Cenários de Hub de notificação** se você estiver escrevendo um jogo móvel onde players levaram ativa, talvez seja necessário toonotify player 2 pelo player 1 terminar sua vez. Se isso é tudo o que você precisa toodo, você pode usar apenas os aplicativos móveis. Mas se você tivesse 100.000 usuários executa o jogo e deseja toosend uma oferta gratuita confidenciais tooeveryone, Hubs de notificação é Olá melhor opção.

Você pode enviar notícias mais recentes, esportivos eventos e toomillions de notificações de lançamento de produto de usuários com baixa latência. Empresas podem notificar os funcionários sobre comunicações confidenciais novo do tempo, como vendas potenciais, para que os funcionários não possuem tooconstantly verificar email ou outros toostay aplicativos informado. Você também pode enviar senhas de uso único exigidas para Multi-Factor Authentication.

## <a name="back-up"></a>Backup
Cada empresa precisa toobackup e restaurar dados. Você pode usar o Azure toobackup e restaurar seu aplicativo na nuvem hello ou local. O Azure oferece toohelp diferentes opções dependendo do tipo de saudação do backup.

### <a name="site-recovery"></a>Site Recovery
Recuperação de Site do Azure (anteriormente conhecida como o Hyper-V Recovery Manager) pode ajudar a proteger aplicativos importantes por coordenar a recuperação e replicação de saudação entre sites. Recuperação de site fornece aplicativos de tooprotect de recurso com base no Hyper-v, VMWare ou SAN tooyour próprio site secundário, site do hoster tooa ou tooAzure e evitem despesas de saudação e a complexidade de criar e gerenciar seu próprio local secundário. Azure criptografa os dados e as comunicações e você tem opção Olá habilitar a criptografia de dados em repouso muito.

Ele monitora a integridade de saudação de seus serviços continuamente e ajuda a automatizar a recuperação ordenada Olá dos serviços no evento de saudação de uma interrupção do site no data center principal de saudação. Máquinas virtuais pode ser ativadas em um serviço de restauração toohelp forma orquestrada rapidamente, mesmo para cargas de trabalho complexas de várias camadas.

O Site Recovery utiliza tecnologias existentes como Réplica do Hyper-V, System Center e SQL Server Always On. Verifique [Visão geral do Azure Site Recovery](site-recovery/site-recovery-overview.md) para obter mais detalhes.

### <a name="azure-backup"></a>Serviço de Backup do Azure
![Serviço de Backup do Azure](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Figura: O Backup do Azure faça backup dos dados de servidores do Windows local para nuvem hello.*  

O Backup do Azure faça backup dos dados de servidores no local executando o Windows Server para a nuvem de saudação. Você pode gerenciar seus backups diretamente a partir de ferramentas de backup de saudação no Windows Server 2012, o Windows Server 2012 Essentials ou o System Center 2012 - Data Protection Manager. Alternativamente, você pode utilizar um agente de backup especializado.

Os dados ficam mais seguros porque os backups são criptografados antes da transmissão e armazenados criptografados no Azure, protegidos por um certificado carregado por você. Olá usará a saudação a mesma proteção de dados redundantes e altamente disponível encontrada no armazenamento do Azure.  Você pode realizar backup de arquivos e pastas regularmente ou imediatamente, realizando esses backups de modo completo ou incremental. Depois que o backup dos dados toohello nuvem, os usuários autorizados poderão recuperar facilmente o servidor de tooany de backups. Ele também oferece políticas de retenção de dados configurável, compactação de dados e dados transferidos limitação para que você possa gerenciar Olá custo toostore e transferência de dados.

**Cenários para backup do Azure**

Se você já utiliza o Windows Server ou System Center, o Serviço de Backup do Azure é uma solução natural para suporte do sistema de arquivos de seus servidores, máquinas virtuais e bancos de dados de SQL Server.  Essa solução funciona com arquivos criptografados, esparsos e comprimidos. Existem algumas limitações, portanto você deve [Verificar pré-requisitos do Azure Backup Olá](http://technet.microsoft.com/library/dn296608.aspx) primeiro.

## <a name="messaging-and-integration"></a>Mensagens e integração
Não importa o que ele está fazendo, o código precisa frequentemente toointeract com outro código.  Em algumas situações, tudo o que é necessário é uma mensagem básica enfileirada. Em outros casos, são necessárias interações mais complexas. O Azure fornece toosolve de maneiras diferentes de alguns desses problemas. Figura 5 ilustra as opções de saudação.

### <a name="queues"></a>Filas
![Retransmissão do Barramento de Serviço do Azure](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Figura: as filas permitem o acoplamento solto entre peças de um aplicativo e facilitam a colocação em escala.*  

O enfileiramento é uma ideia simples: um aplicativo coloca uma mensagem na fila e essa mensagem, por fim, é lida por outro aplicativo. Se seu aplicativo precisa apenas esse serviço simples, Olá melhor opção talvez seja a filas do Azure.

Devido a saudação de maneira hello que Azure aumentou ao longo do tempo, filas de armazenamento do Azure e filas do barramento de serviço fornecem serviços de enfileiramento de mensagens similares. Olá motivos seria toouse sobre Olá outros são abordados em papel razoavelmente técnico Olá [filas do Azure e filas do Service Bus - semelhanças e diferenças](http://msdn.microsoft.com/library/azure/hh767287.aspx).  Na maioria dos cenários, qualquer uma dessas opções funcionará.

**Cenários para fila**

Um uso comum das filas hoje é toolet uma instância de função da web se comunicam com uma instância de função de trabalho em Olá mesmo aplicativo de serviços de nuvem.

Por exemplo, suponha que você crie um aplicativo do Azure para compartilhamento de vídeo. aplicativo Hello consiste em código PHP em execução em uma função web que permite aos usuários carregam e assista a vídeos, junto com uma função de trabalho implementados em c# que converte carregado vídeo em vários formatos.

Quando uma instância de função web obtém um novo vídeo de um usuário, pode armazenar vídeo Olá em um blob, em seguida, enviar uma função de trabalho tooa de mensagem por meio de uma fila informando onde toofind esse novo vídeo. Uma função de trabalho instância-it não importa qual mensagem de saudação será um e leitura da fila de saudação e realizar traduções de vídeo Olá necessárias no plano de fundo de saudação.

Estruturar um aplicativo dessa maneira permite que o processamento assíncrono e ele também torna Olá tooscale mais fácil de aplicativo, desde que o número de saudação de instâncias de função web e instâncias de função de trabalho pode ser variado independentemente. Você também pode usar o tamanho da fila hello como gatilho tooscale Olá inúmeras funções de trabalho para cima e para baixo. Se está alto demais, você acrescenta mais funções. Quando ele obtém inferior, você pode reduzir o número de saudação da execução de funções toosave money.  

Você pode usar esse mesmo padrão entre vários componentes diferentes do seu aplicativo, mesmo que eles não utilizem funções de trabalho e da Web.  Ele permite tooscale partes de saudação em ambos os lados da fila de saudação acima e abaixo como demanda e requer tempo de processamento.

### <a name="service-bus"></a>Barramento de Serviço
Se eles executados na nuvem hello, no seu data center, em um dispositivo móvel, ou em outro local, os aplicativos precisam toointeract. meta de saudação do barramento de serviço do Azure é toolet aplicativos em execução de praticamente qualquer lugar trocam de dados.

Em adição toohello filas (um para um) descritas anteriormente, o barramento de serviço também fornece tooother métodos de comunicação.

#### <a name="service-bus-relay"></a>Retransmissão do Service Bus
![Retransmissão do Barramento de Serviço do Azure](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Figura: a Retransmissão do Barramento de Serviço permite a comunicação entre os aplicativos em diferentes lados de um firewall.*

Barramento de serviço permite a comunicação direta por meio de seu serviço de retransmissão, fornecendo um toointeract de maneira segura através de firewalls. Retransmissões de barramento de serviço permitem que aplicativos toocommunicate trocando mensagens por meio de um ponto de extremidade hospedado na nuvem hello, em vez de localmente.

**Cenários para retransmissão do Barramento de Serviço**

Os aplicativos que se comunicam por meio do Barramento de Serviço podem ser aplicativos ou softwares do Azure em execução em alguma outra plataforma na nuvem. Eles também podem ser aplicativos em execução fora da nuvem hello, no entanto. Por exemplo, pense em uma companhia aérea que implementa serviços de reserva em computadores dentro de seu próprio datacenter. aéreo Olá precisa tooexpose esses clientes toomany de serviços, incluindo quiosques de check-in em aeroportos, terminais de agente de reserva e telefones dos clientes talvez até mesmo. Ele pode usar barramento de serviço toodo isso criando acopladas interações entre Olá vários aplicativos.

#### <a name="service-bus-topics-and-subscriptions"></a>Tópicos e assinaturas do Barramento de Serviço
![Tópicos do Barramento de Serviço do Azure](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Figura: Tópicos de barramento de serviço permite que vários aplicativos toopost mensagens e outros aplicativos toosubscribe tooreceive que atendem a critérios específicos.*

O Barramento de Serviço oferece um mecanismo de publicação e assinatura chamado Tópicos e Assinaturas. Com a publicação, um aplicativo pode enviar tópico tooa de mensagens, enquanto outros aplicativos podem criar o tópico de toothis de assinaturas. Isso permite a comunicação de um-para-muitos entre um conjunto de aplicativos, permitindo que Olá mesma mensagem ser lido por vários destinatários.

**Cenários dos Tópicos e assinaturas do Barramento de Serviço**

Sempre que você estiver configurando onde há muitas mensagens que são importantes, mas vários sistemas downstream só precisam toolisten toodiffering subconjuntos dessas comunicações, o tópico do barramento de serviço e as assinaturas são uma boa opção.

### <a name="biztalk-services"></a>Serviços do BizTalk
![Serviços do BizTalk](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Figura: Os serviços do BizTalk fornece capacidade Olá tootransform formatos de mensagens XML na nuvem hello.*

Algumas vezes, você precisa conectar sistemas que comunicam-se utilizando diferentes formatos de mensagens. É comum para esquemas de banco de dados diferente de toohave de negócios e mensagens formatos, mesmo quando há um padrão comum de XML. Em vez de gravar um lote de código personalizado, você pode usar o BizTalk Server local toointegrate vários sistemas.  Serviços BizTalk do Azure fornece Olá mesmo tipo de serviço, mas na nuvem hello. Você paga apenas o que você use e não se preocupar sobre escala, como você teria tooon local.

**Cenários dos serviços BizTalk**

As interações entre empresas (B2B) normalmente requerem esse tipo de conversão.  Por exemplo, uma empresa criando aeronaves necessidades tooorder partes dele é fornecedores de várias partes. Essa empresa terá muitos fornecedores de peças.  Os pedidos devem ser automatizada toogo diretamente de sistemas de construtores de avião Olá em sistemas de fornecedores de saudação.  Nenhum dos negócios exigirem toochange seus sistemas de núcleo e formatos de mensagem e é pouco provável que esses formatos são Olá mesmo. Os serviços do BizTalk podem assumir mensagens e converter entre formatos de novo Olá das duas maneiras. O fornecedor de avião Olá pode Olá tootranslate de trabalho ou Olá vários fornecedores podem, dependendo de quem deseja mais controle e saudação do valor da conversão necessária.     

## <a name="compute-assistance"></a>Assistência de Computação
O Azure fornece assistência para serviços que não é necessário toorun todo o tempo de saudação.  

### <a name="scheduler"></a>Agendador
![Agendador do Azure](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Figura: O Agendador do Azure fornece uma maneira tooschedule trabalhos em um horário específico para uma duração específica.*

Às vezes, os aplicativos só precisa toorun em um determinado momento. No Azure, você pode economizar dinheiro com esse tipo de aplicativo em vez de permitir que um aplicativo apenas manter 24x7 aguardando dados tooprocess a execução. O Agendador do Azure permite que você tooschedule quando um aplicativo deve ser executado com base no intervalo de tempo ou em um calendário. Ele é confiável e verificará se um processo está em execução, mesmo se houver falhas de rede, computador e datacenter. Você usar Olá API REST do Agendador toomanage essas ações.

Quando ocorre um alarme agendado, o Agendador envia HTTP ou HTTPS mensagens tooa ponto de extremidade específico ou pode colocar uma mensagem em uma fila de armazenamento.  Portanto, você precisa toohave seu aplicativo tem um ponto de extremidade acessível ou que ele seja monitorar uma fila de armazenamento. Em seguida, depois que ele obtém a mensagem de saudação, ele pode realizar qualquer ação programada para.

**Cenários para agendador**

* Ações recorrentes de aplicativo: por exemplo, um serviço pode periodicamente obter dados do twitter e reunir dados de Olá em um feed regular.
* Manutenção diária: processamento de log ou remoção, realização de backups e outras tarefas agendamento intermitentes.
* Tarefas noturnas.
* Tarefas de aplicativos web como redução diária de logs, realização de backups e outras tarefas de manutenção. Um administrador pode escolher toobackup seu banco de dados à 1H00 todos os dias para Olá próximos 9 meses, por exemplo.

Olá API do Agendador permite toocreate, atualizar, excluir, exibir e gerenciar coleções de trabalhos e trabalhos agendados programaticamente.

## <a name="performance"></a>Desempenho
O desempenho é sempre importante para um aplicativo. Aplicativos tendem tooaccess Olá os mesmos dados repetidamente. Desempenho de uma maneira tooimprove é tookeep uma cópia desse aplicativo toohello mais dados, minimizar tempo de saudação necessário tooretrieve-lo. O Azure fornece diferentes serviços para realizar essa tarefa.

### <a name="azure-caching"></a>Cache do Azure
![Cache do Azure](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Figura: um aplicativo do Azure pode armazenar em cache dados na memória e até mesmo dividi-los em muitas funções de trabalho**

Acessar dados armazenados em algum dos serviços de gerenciamento de dados do Azure (Banco de dados SQL, Tabelas ou Blobs) é muito rápido. Porém, acessar dados armazenados na memória é ainda mais rápido. Por esse motivo, manter uma cópia dos dados acessados frequentemente na memória pode aumentar o desempenho do aplicativo. Você pode usar toodo de cache na memória do Azure isso.

Um aplicativo de serviços de nuvem pode armazenar dados no cache e recuperá-lo diretamente sem a necessidade de armazenamento persistente tooaccess. cache de saudação pode ser mantida em seu aplicativo de VMs ou ser fornecido pelas VMs dedicado exclusivamente toocaching. Em ambos os casos, cache Olá pode ser distribuído, com dados saudação contém disseminado entre várias VMs em um datacenter do Azure.

O Azure tem um número de tecnologias de cache diferentes que mudaram ao longo do tempo. Na ordem de saudação que foram introduzidos, há um compartilhado na função, gerenciado e o cache Redis. caching Olá compartilhado é uma tecnologia mais antiga e você não deve criar novas implementações com ele. Olá, Cache gerenciado tem Olá mesmos recursos de saudação na função de cache, mas como um serviço gerenciado fora do hello Portal de gerenciamento. Olá Redis Cache está em visualização. implementação de Redis Olá tem Olá maior número de recursos e é recomendada quando você escreve novo código de cache.

**Cenários para cache do Azure**

Um aplicativo que lê repetidamente um catálogo de produtos pode se beneficiar do uso desse tipo de armazenamento em cache, por exemplo, desde dados saudação ele precisa estará disponível mais rapidamente. tecnologia de saudação também oferece suporte a bloqueio, permitindo que ele seja usado com leitura/gravação, bem como dados somente leitura. E aplicativos ASP.NET podem usar dados de sessão Olá serviço toostore com apenas uma alteração de configuração.

### <a name="content-delivery-network"></a>Rede de Distribuição de Conteúdo
![CDN do Azure](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Figura: Cópias de um blob podem ser armazenados em cache em locais em todo o mundo de saudação.**

Suponha que você precisa de dados de blob toostore que serão acessados por usuários Olá mundo. Talvez seja um vídeo de hello mais recente World Cup correspondência, por exemplo, ou atualizações de driver ou um livro eletrônico popular. Armazenar uma cópia dos dados de saudação em vários datacenters do Azure ajudará, mas se houver vários usuários, provavelmente não é suficiente. Para um desempenho ainda melhor, você pode usar o hello CDN do Azure.

Olá CDN possui vários sites ao redor Olá, mundo, cada capaz de armazenar cópias de blobs do Azure. Olá primeira vez que um usuário em alguma parte da Olá, mundo acessa um determinado blob, Olá informações nele são copiadas de um datacenter do Azure para armazenamento CDN local em que Geografia. Depois disso, acessos de parte do Olá, mundo usará a cópia de blob Olá armazenado em cache na CDN do hello-eles não será necessário toogo todos os toohello de maneira hello mais próximo do datacenter do Azure. resultado de saudação é mais rápido acessar dados de toofrequently acessado por usuários em qualquer lugar em Olá, mundo.

**Cenários para CDN**

É comum toouse CDN com vídeo de toodeliver de serviços de mídia em todo o mundo. Vídeo geralmente significa arquivos grandes, que exigem muita largura de banda.  Falamos sobre os Serviços de Mídia em outra parte desta página.

## <a name="big-data-and-big-compute"></a>Big Data e Computação de Grande Porte
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Figura: HDInsight ajuda com processamento em massa Olá enormes quantidades de dados**

Há muitos anos, foi feita em massa de saudação da análise de dados em dados relacionais armazenados em um data warehouse criado com um DBMS relacional. Esse tipo de análise de negócios é importante e é para um toocome muito tempo. Mas e se são tão grandes que bancos de dados relacionais apenas não é possível utilizar dados Olá deseja tooanalyze? E suponha que os dados de saudação não relacionais? Eles podem ser logs de servidor em um datacenter, por exemplo, ou dados de eventos históricos de sensores, ou algo parecido. Em casos assim, você tem o que é conhecido como problema de big data. É necessária outra abordagem.

a tecnologia dominante Olá hoje para análise de dados grandes é Hadoop. Um Apache Abrir projeto de origem, essa tecnologia armazena dados usando o sistema de arquivos distribuído da Hadoop (HDFS) do hello permite aos desenvolvedores criar MapReduce trabalhos tooanalyze esses dados. HDFS difundirá os dados em vários servidores, em seguida, partes de execuções do trabalho de MapReduce Olá em cada um deles, permitindo que os dados de grande Olá ser processadas em paralelo.

HDInsight é o nome de saudação do serviço do Azure Olá Apache Hadoop. HDInsight permite HDFS armazenar dados no cluster hello e distribuí-lo em várias VMs. Ele também se espalha lógica de saudação de um trabalho de MapReduce entre as VMs. Assim como com Hadoop no local, os dados são lógica processados localmente saudação e dos dados Olá funciona em Olá mesma VM- e em paralelo para melhorar o desempenho. O HDInsight também pode armazenar dados no Azure Storage Vault (ASV), que usa os blobs.  Usar ASV permite toosave dinheiro porque você pode excluir o cluster HDInsight quando não estiver em uso, mas ainda manter seus dados na nuvem hello.

HDinsight oferece suporte a outros componentes do ecossistema de Hadoop hello, incluindo Hive e Pig. A Microsoft criou também os componentes que o tornam mais fácil toowork com dados produzidos por HDInsight usando ferramentas de BI tradicionais, como o adaptador de HiveODBC hello e Gerenciador de dados que funcionam com o Excel.

### <a name="high-performance-computing-big-compute"></a>HPC (Computação de Alto Desempenho) - Computação de Grande Porte
Um dos toouse de maneiras muito atraente Olá uma plataforma de nuvem é toorun computação de alto desempenho (HPC) e outros aplicativos "Computação intensa". Exemplos incluem especializado toouse engenharia de aplicativos criados Olá padrão da indústria Interface MPI (Message Passing), bem como os chamados aplicativos paralelos, esses modelos de riscos financeiros.

essência Olá da computação intensa está executando código em diversas máquinas em Olá simultaneamente. No Azure, isso significa que em muitas máquinas virtuais em execução simultaneamente, tudo trabalhando em paralelo toosolve algum problema. Isso requer algumas maneira tooresources e tooschedule aplicativos, ou seja, toodistribute seu trabalho entre essas instâncias. Pacote de HPC gratuito da Microsoft e outras soluções de cluster de computação podem executar bem no Azure, aproveitando as vantagens de serviços de computação e a infraestrutura do Azure tooadd capacidade sob demanda tooan local do cluster de computação ou executam aplicativos de computação intensa totalmente na Olá nuvem.

O Azure fornece um intervalo de VM tamanhos de instância com diferentes configurações de núcleos de CPU, memória, capacidade de disco e outros requisitos de saudação toomeet características de diferentes aplicativos. Olá introduzidos recentemente A8 e A9 trabalho de instâncias bem para muitos de computação intensivas cargas de trabalho e aplicativos MPI paralelos em particular, porque têm alta velocidade, CPUs de vários núcleos e grandes quantidades de memória. Em determinadas configurações de instâncias de saudação tirar proveito de uma rede de baixa latência e alta taxa de transferência de aplicativos em nuvem Olá que inclui a tecnologia de acesso (RDMA) de memória direta remota para máxima eficiência de aplicativos MPI paralelos.

O Azure também oferece a desenvolvedores de aplicativos de Computação de Grande Porte e a parceiros um conjunto completo de recursos de computação, serviços, opções de arquitetura e ferramentas de desenvolvimento. Azure oferece suporte à computação intensa fluxos de trabalho personalizados que envolvem fluxos de trabalho de dados especializados e núcleos de computação de trabalhos e tarefas que podem ser dimensionado toothousands de padrões de agendamento.

## <a name="media"></a>Mídia
![Serviços de Mídia do Azure](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Figura: Serviços de mídia é uma plataforma para aplicativos que fornecem o vídeo e outras tooclients de mídia em torno de Olá, mundo.**

A reprodução de vídeos constitui uma grande parte do tráfego de Internet hoje em dia, e essa porcentagem será ainda maior no futuro. Ainda fornecer vídeo Olá web não é simple. Há muitas variáveis, como Olá algoritmo de codificação e hello resolução de vídeo de tela de saudação do usuário. Vídeo também tende toohave picos de demanda como um aumento de sábado noite quando decidir de muitas pessoas gostariam toowatch um filme online.

Dada sua popularidade, é seguro apostar que muitos aplicativos novos que usam vídeo serão criados. Ainda todos eles precisará toosolve alguns da saudação mesmo problemas e fazer com que cada uma delas resolver esses problemas em seu próprio faz sentido. Uma abordagem melhor é toocreate uma plataforma que oferece soluções comuns para muitos toouse de aplicativos. E criar essa plataforma em nuvem Olá tem algumas vantagens claras. Pode ser amplamente disponível em uma base de pagamento, e também pode lidar com a variabilidade Olá na demanda geralmente voltadas para aplicativos de vídeo.

Os Serviços de Mídia do Azure resolvem esse problema. Eles fornecem um conjunto de componentes de nuvem que tornam mais fácil a vida das pessoas que criam e executam aplicativos usando vídeo e outras mídias.

Como mostra a Figura Olá, o Media Services fornece um conjunto de componentes para aplicativos que funcionam com vídeo e outras mídias. Por exemplo, ele inclui uma mídia de ingestão de vídeo componente tooupload em serviços de mídia (onde ele é armazenado em Blobs do Azure), um componente de codificação que dá suporte a vários formatos de vídeo e áudio, um componente de proteção de conteúdo que fornece gerenciamento de direitos digitais um componente para inserindo anúncios em um fluxo de vídeo, componentes de streaming e muito mais. Parceiros da Microsoft também podem fornecer componentes para a plataforma de saudação e ter o Microsoft distribuir esses componentes e cobrar em seu nome.

Os aplicativos que usam essa plataforma podem ser executados no Azure ou em outro lugar. Por exemplo, um aplicativo de área de trabalho para uma casa de vídeo de produção pode permitir que seus usuários carregar vídeo tooMedia serviços, em seguida, processá-la de várias maneiras. Como alternativa, um serviço de gerenciamento de conteúdo baseado em nuvem em execução no Azure pode contar com os serviços de mídia tooprocess e distribuir o vídeo. Sempre que ele é executado e o que ele faz, cada aplicativo escolhe quais componentes necessários toouse, acessá-los por meio das interfaces RESTful.

toodistribute o que ele produz, um aplicativo pode usar Olá CDN do Azure CDN outro, ou enviar apenas diretamente bits toousers. No entanto, vídeos criados usando os Serviços de Mídia podem ser consumidos por vários sistemas de clientes, incluindo Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash e Silverlight. meta de saudação é toomake-aplicativos de mídia modernos toocreate mais fácil.

**Referências**

Para obter uma exibição mais visual de como funciona o Media Services, baixar Olá [pôster de serviços de mídia do Azure][Azure Media Services Poster].

## <a name="commerce"></a>Comércio
aumento de saudação do Software como um serviço é transformar como podemos criar aplicativos. Ele também está transformando a forma como vendemos aplicativos. Como um aplicativo SaaS reside na nuvem hello, faz sentido que seus clientes potenciais devem procurar soluções on-line. E essa alteração se aplica a toodata, bem como tooapplications. Por que pessoas não devem pesquisar toohello nuvem para conjuntos de dados disponíveis no mercado? A Microsoft aborda ambas essas preocupações com hello [Azure Marketplace](https://azure.microsoft.com/marketplace/).

![Comércio do Azure](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Figura: o Azure Marketplace e a Azure Store permitem encontrar e comprar aplicativos Azure e conjuntos de dados comerciais e utilizá-los como parte de seus aplicativos do Azure.**

Hello diferença entre hello duas é que Marketplace está fora da saudação Portal de gerenciamento, mas Olá repositório pode ser acessado de dentro do portal de saudação. Clientes potenciais podem pesquisar toofind Azure aplicativos que atendem às suas necessidades. Os clientes também podem pesquisar conjuntos de dados comerciais, incluindo dados demográficos, dados financeiros, dados geográficos e muito mais. Quando encontrar algo que queiram, podem acessar do fornecedor de saudação diretamente por meio de saudação Marketplace ou locais de repositório de web ou em alguns casos de saudação Portal de gerenciamento. Aplicativos também podem usar o hello API de pesquisa do Bing através de saudação Marketplace, dando a eles acesso toohello resultados de pesquisas na web.

**Cenários para comércio**

SendGrid é um aplicativo hello armazenamento do Azure que permite que você toosend email. Ele oferece funções adicionais, como entrega e estatísticas confiáveis.  Você pode comprar este aplicativo e serviços relacionados em vez de tentar toobuild essa infra-estrutura por conta própria.  

## <a name="getting-started"></a>Introdução
Agora que você tem Olá visão, Olá próxima etapa é toowrite seu primeiro aplicativo do Azure. Escolha o idioma [obter Olá SDK adequado](/downloads/)e vá para ele. Nuvem de computação é o padrão de novos hello – comece agora mesmo.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
