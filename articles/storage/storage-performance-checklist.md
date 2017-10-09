---
title: "verificação de desempenho e escalabilidade do armazenamento de aaaAzure | Microsoft Docs"
description: "Uma lista de verificação de práticas comprovadas para uso com o Armazenamento do Azure no desenvolvimento de aplicativos de alto desempenho."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c0cd77da4a1abda42c018255ed93215b71f4fad8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Lista de verificação de desempenho e escalabilidade do armazenamento do Microsoft Azure
## <a name="overview"></a>Visão geral
Desde o lançamento de saudação do serviços de armazenamento do Microsoft Azure Olá, a Microsoft desenvolveu várias práticas comprovadas para usar esses serviços em um modo de alto desempenho, e este artigo serve tooconsolidate hello mais importante deles em uma lista de estilo de lista de verificação. Olá intenção deste artigo é toohelp os desenvolvedores de aplicativos, verifique se que eles estão usando práticas comprovadas com toohelp-los identificam outras práticas comprovadas, que eles devem considerar a adoção e o armazenamento do Azure. Este artigo não tenta toocover cada possível otimização de desempenho e escalabilidade — ele exclui os que são pequenos em seu impacto ou não é amplamente aplicável. extensão de toohello Olá o comportamento do aplicativo pode ser prevista durante o design, é útil tookeep em mente desde o início tooavoid designs que serão executado em problemas de desempenho.  

Todos os desenvolvedores de aplicativos usando o armazenamento do Azure devem levar Olá tempo tooread neste artigo e verifique que seus aplicativos seguem cada Olá listadas abaixo de práticas comprovadas.  

## <a name="checklist"></a>Lista de verificação
Este artigo organiza práticas comprovada de saudação em Olá grupos a seguir. As práticas comprovadas aplicam-se a:  

* Todos os serviços de armazenamento do Azure (blobs, tabelas, filas e arquivos)
* Blobs
* Tabelas
* Filas  

| Concluído | Área | Categoria | Pergunta |
| --- | --- | --- | --- |
| &nbsp; | Todos os serviços |Metas de escalabilidade |[Seu aplicativo criado tooavoid está se aproximando metas de escalabilidade Olá?](#subheading1) |
| &nbsp; | Todos os serviços |Metas de escalabilidade |[É o tooenable convenção projetada nomenclatura melhor balanceamento de carga?](#subheading47) |
| &nbsp; | Todos os serviços |Rede |[Dispositivos do lado cliente tem suficientemente alta largura de banda e o desempenho de saudação tooachieve de baixa latência necessárias?](#subheading2) |
| &nbsp; | Todos os serviços |Rede |[Os dispositivos cliente têm um link de alta qualidade?](#subheading3) |
| &nbsp; | Todos os serviços |Rede |[Aplicativo de cliente hello está localizado "próximo" conta de armazenamento Olá?](#subheading4) |
| &nbsp; | Todos os serviços |Distribuição de conteúdo |[Você usa um CDN para distribuir conteúdo?](#subheading5) |
| &nbsp; | Todos os serviços |Acesso direto do cliente |[Você está usando a SAS e CORS acesso direto de tooallow toostorage em vez de proxy?](#subheading6) |
| &nbsp; | Todos os serviços |Cache |[Seu aplicativo armazena em cache os dados que são usados com frequência e que raramente mudam?](#subheading7) |
| &nbsp; | Todos os serviços |Cache |[Seu aplicativo compila atualizações, armazenando-as em cache no cliente e carregando-as em grandes conjuntos?](#subheading8) |
| &nbsp; | Todos os serviços |Configuração .NET |[Você configurou seu toouse um número suficiente de conexões simultâneas do cliente?](#subheading9) |
| &nbsp; | Todos os serviços |Configuração .NET |[Você configurou .NET toouse um número suficiente de threads?](#subheading10) |
| &nbsp; | Todos os serviços |Configuração .NET |[Você usa o .NET 4.5 ou posterior, versões com recurso aprimorado de coleta de lixo?](#subheading11) |
| &nbsp; | Todos os serviços |Paralelismo |[Você garante que o paralelismo é limitado adequadamente para que você não sobrecarregar a recursos de cliente ou destinos de escalabilidade de saudação?](#subheading12) |
| &nbsp; | Todos os serviços |Ferramentas |[Usando a versão mais recente de saudação da Microsoft é fornecidos ferramentas e bibliotecas de cliente?](#subheading13) |
| &nbsp; | Todos os serviços |Novas tentativas |[Você usa uma política de nova tentativa de retirada exponencial para diminuir os erros e a ocorrência de tempos limite?](#subheading14) |
| &nbsp; | Todos os serviços |Novas tentativas |[Seu aplicativo evita novas tentativas para erros que não admitem novas tentativas?](#subheading15) |
| &nbsp; | Blobs |Metas de escalabilidade |[Você tem um grande número de clientes que acessam um único objeto simultaneamente?](#subheading46) |
| &nbsp; | Blobs |Metas de escalabilidade |[Seu aplicativo permanecer dentro da meta de escalabilidade da largura de banda ou operações de saudação para um único blob?](#subheading16) |
| &nbsp; | Blobs |Cópia de blobs |[Seu método de cópia de blobs é eficiente?](#subheading17) |
| &nbsp; | Blobs |Cópia de blobs |[Você usa o AzCopy para copiar blobs em massa?](#subheading18) |
| &nbsp; | Blobs |Cópia de blobs |[Você está usando a importação/exportação do Azure tootransfer muito grandes volumes de dados?](#subheading19) |
| &nbsp; | Blobs |Uso de metadados |[Você armazena os metadados sobre blobs usados com frequência?](#subheading20) |
| &nbsp; | Blobs |Carregamento rápido |[Durante a tentativa de um blob de tooupload rapidamente, você está carregando blocos em paralelo?](#subheading21) |
| &nbsp; | Blobs |Carregamento rápido |[Durante a tentativa de tooupload muitos blobs rapidamente, você está carregando blobs em paralelo?](#subheading22) |
| &nbsp; | Blobs |Tipo de blob correto |[Você usa blobs de página ou de bloco quando necessário?](#subheading23) |
| &nbsp; | Tabelas |Metas de escalabilidade |[São você aproxima Olá metas de escalabilidade para entidades por segundo?](#subheading24) |
| &nbsp; | Tabelas |Configuração |[Você usa JSON para suas solicitações de tabela?](#subheading25) |
| &nbsp; | Tabelas |Configuração |[Você desativou o Nagle tooimprove desempenho de saudação de solicitações pequenos?](#subheading26) |
| &nbsp; | Tabelas |Tabelas e partições |[Você particionou seus dados corretamente?](#subheading27) |
| &nbsp; | Tabelas |Partições mais acessadas |[Você evita padrões do tipo "somente anexar" e "somente incluir"?](#subheading28) |
| &nbsp; | Tabelas |Partições mais acessadas |[Suas inserções/atualizações valem para diversas partições?](#subheading29) |
| &nbsp; | Tabelas |Escopo da consulta |[Você criou seu tooallow de esquema para o ponto de consultas toobe usado na maioria dos casos e toobe de consultas de tabela usado com moderação?](#subheading30) |
| &nbsp; | Tabelas |Densidade da consulta |[As suas consultas geralmente verificam e indicam quais linhas o aplicativo usará?](#subheading31) |
| &nbsp; | Tabelas |Limitação dos dados retornados |[Você está usando filtragem entidades retornando tooavoid que não são necessários?](#subheading32) |
| &nbsp; | Tabelas |Limitação dos dados retornados |[Você está usando tooavoid de projeção retornando propriedades que não são necessários?](#subheading33) |
| &nbsp; | Tabelas |Desnormalização |[Você tem desnormalizada seus dados, de modo que você evitar consultas ineficientes ou várias solicitações de leitura durante a tentativa de tooget dados?](#subheading34) |
| &nbsp; | Tabelas |Inserção/atualização/exclusão |[É você envio em lote solicitações que precisam de toobe transacional ou podem ser feitas em Olá mesmo tempo de ida e volta de tooreduce?](#subheading35) |
| &nbsp; | Tabelas |Inserção/atualização/exclusão |[Você está evitando recuperando toodetermine de apenas uma entidade se toocall inserir ou atualizar?](#subheading36) |
| &nbsp; | Tabelas |Inserção/atualização/exclusão |[Você já pensou em armazenar séries de dados que serão recuperados em conjunto frequentemente, em uma única entidade e como propriedades, em vez de serem recuperados como diversas entidades?](#subheading37) |
| &nbsp; | Tabelas |Inserção/atualização/exclusão |[Você já pensou em usar blobs no lugar das tabelas para as entidades que serão recuperadas em conjunto e que podem ser escritas em lotes (por exemplo, dados de séries temporais)?](#subheading38) |
| &nbsp; | Filas |Metas de escalabilidade |[São você aproxima Olá metas de escalabilidade para mensagens por segundo?](#subheading39) |
| &nbsp; | Filas |Configuração |[Você desativou o Nagle tooimprove desempenho de saudação de solicitações pequenos?](#subheading40) |
| &nbsp; | Filas |Tamanho da mensagem |[São mensagens tooimprove compact Olá desempenho da fila de Olá?](#subheading41) |
| &nbsp; | Filas |Recuperação em massa |[Você recupera diversas mensagens com uma única operação "Obter"?](#subheading42) |
| &nbsp; | Filas |Frequência de votação |[Você esteja sondando com frequência suficiente Olá tooreduce percebida latência do seu aplicativo?](#subheading43) |
| &nbsp; | Filas |Atualização de mensagem |[Você está usando UpdateMessage toostore progresso no processamento de mensagens, evitando ter tooreprocess Olá toda a mensagem se ocorrer um erro?](#subheading44) |
| &nbsp; | Filas |Arquitetura |[Você está usando filas toomake todo o seu aplicativo mais escalonável, mantendo cargas de trabalho de longa execução fora do caminho crítico hello e escala, em seguida, independentemente?](#subheading45) |

## <a name="allservices"></a>Todos os serviços
Esta seção lista as práticas comprovadas que usam toohello aplicável de qualquer um dos serviços de armazenamento do Azure hello (blobs, tabelas, filas ou arquivos).  

### <a name="subheading1"></a>Metas de escalabilidade
Cada um dos serviços de armazenamento do Azure Olá tem metas de escalabilidade de capacidade (GB), a taxa de transações e largura de banda. Se seu aplicativo se aproximar ou excede qualquer um dos destinos de escalabilidade Olá, ele pode encontrar as latências de transação aumentada ou limitação. Quando um serviço de armazenamento limita seu aplicativo, o serviço de saudação começa tooreturn "servidor 503 ocupado" ou "500 tempo limite da operação" códigos de erro para algumas transações de armazenamento. Esta seção aborda os dois toodealing abordagem geral de Olá com destinos de escalabilidade e metas de escalabilidade de largura de banda em particular. As seções posteriores que lidam com os serviços de armazenamento individual discutem metas de escalabilidade no contexto de saudação do serviço específico:  

* [Largura de banda do blob e solicitações por segundo](#subheading16)
* [Entidades de tabela por segundo](#subheading24)
* [Fila de mensagens por segundo](#subheading39)  

#### <a name="sub1bandwidth"></a>Meta de escalabilidade de largura de banda para todos os serviços
No momento da saudação de gravação, destinos de largura de banda de saudação em conta hello dos EUA para um armazenamento com redundância geográfica (GRS) são 10 gigabits por segundo (Gbps) de entrada (os dados enviados toohello conta de armazenamento) e 20 Gbps para saída (dados enviados da conta de armazenamento Olá). Para uma conta de armazenamento localmente redundante (LRS), os limites de saudação são superior – 20 Gbps para entrada e 30 Gbps para saída.  Os limites de largura de banda internacional podem ser menores e constam na nossa [página de metas de escalabilidade](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Para obter mais informações sobre as opções de redundância de armazenamento hello, consulte os links de saudação em [recursos úteis](#sub1useful) abaixo.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Quais toodo quando se aproximando de uma meta de escalabilidade
Se seu aplicativo estiver se aproximando alvos de escalabilidade de saudação para uma única conta de armazenamento, considere adotando uma saudação abordagens a seguir:  

* Reconsidere a carga de trabalho de saudação que faz com que seu aplicativo tooapproach ou exceder a meta de escalabilidade de saudação. Pode criá-lo diferentemente toouse menos largura de banda ou capacidade ou poucas transações?
* Se um aplicativo deve exceder um dos destinos de escalabilidade hello, você deve criar várias contas de armazenamento e partição os dados do aplicativo entre essas várias contas de armazenamento. Se você usar esse padrão, em seguida, ser toodesign-se de que seu aplicativo para que você pode adicionar mais contas de armazenamento no hello futura para balanceamento de carga. No momento da publicação, cada assinatura do Azure pode ter até too100 contas de armazenamento.  O único custo das contas de armazenamento é o uso dos dados armazenados, das transações feitas ou dos dados transferidos.
* Se seu aplicativo atinge destinos de largura de banda hello, considere a compactação de dados no hello cliente tooreduce Olá largura de banda necessária toosend Olá dados toohello serviço de armazenamento.  Apesar de economizar a largura de banda e melhorar o desempenho da rede, isso também pode ter impactos negativos.  Você deve avaliar o impacto no desempenho Olá deste devido a requisitos de processamento adicionais toohello para compactar e descompactar os dados no cliente de saudação. Além disso, armazenar dados compactados pode tornar mais difícil problemas de tootroubleshoot desde que ele pode ser mais difícil dados tooview armazenado usando ferramentas padrão.
* Se seu aplicativo atinge as metas de escalabilidade de hello, em seguida, certifique-se de que você está usando uma retirada exponencial para repetições (consulte [tentativas](#subheading14)).  É melhor toomake-se de que você nunca aborda as metas de escalabilidade de saudação (usando um Olá acima métodos), mas isso irá garantir que seu aplicativo não apenas manter repetir rapidamente, tornando Olá limitação pior.  

#### <a name="useful-resources"></a>Recursos úteis
Olá links a seguir fornece detalhes adicionais sobre metas de escalabilidade:

* Confira [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para saber mais sobre metas de escalabilidade.
* Consulte [replicação de armazenamento do Azure](storage-redundancy.md) e postagem de blog Olá [opções de redundância de armazenamento do Azure e armazenamento geograficamente redundante de acesso de leitura](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) para obter informações sobre opções de redundância de armazenamento.
* Para obter informações atualizadas sobre os preços dos serviços Azure, confira [Preços do Azure](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Convenção de nomenclatura de partição
Armazenamento do Azure usa um baseada em intervalo particionamento esquema tooscale e carga saldo Olá sistema. chave de partição Olá é usado toopartition dados em intervalos e esses intervalos são com balanceamento de carga em todo sistema hello. Isso significa que as convenções de nomenclatura como lexical ordenação (por exemplo, msftpayroll, msftperformance, msftemployees, etc.) ou usando os carimbos de hora (log20160101, log20160102, log20160102, etc.) serão prestam toohello partições sendo potencialmente co-localizados no Olá mesmo servidor de partição, até que uma operação de balanceamento de carga divide-los em intervalos menores. Por exemplo, todos os blobs dentro de um contêiner podem ser atendidos por um único servidor até hello carga esses blobs exigir mais rebalanceamento de intervalos de partição hello. Da mesma forma, um grupo de contas pouco carregados com seus nomes organizados em ordem léxica pode ser atendido por um único servidor até Olá carregar em uma ou todas essas contas exigem-los toobe dividido em vários servidores de partições. Cada operação de balanceamento de carga pode afeta a latência de saudação de chamadas de armazenamento durante a operação de saudação. toohandle de capacidade do sistema Olá que uma intermitência repentina de partição de tooa de tráfego é limitada por escalabilidade de saudação do servidor de uma única partição até que a operação de balanceamento de carga de saudação é ativada no e redistribui o intervalo de chave de partição de saudação.  

Você pode seguir algumas melhores práticas tooreduce Olá frequência essas operações.  

* Examine a convenção de nomenclatura Olá usada para contas, contêineres, blobs, tabelas e filas em conjunto. Considere prefixar os nomes de conta com um hash de três dígitos usando uma função de hash que melhor atenda às suas necessidades.  
* Se você organizar seus dados usando os carimbos de hora ou identificadores numéricos, você tem tooensure não estiver usando um padrões de tráfego somente de acréscimo (ou preceda somente). Esses padrões não são adequados para um intervalo de-com base particionamento sistema e podem lead tooall Olá tráfego vai tooa única partição e sistema de Olá limitação de efetivamente o balanceamento de carga. Por exemplo, se você tiver diariamente operações que usam um objeto de blob com um carimbo de hora, como AAAAMMDD, em seguida, todos os tráfego de saudação para operação diária é direcionado tooa único objeto que é fornecido por um único servidor de partições. Examine se limita a saudação por blob e por partição limites atender às suas necessidades e considere dividir essa operação em vários blobs, se necessário. Da mesma forma, se você armazenar dados de série temporal em suas tabelas, todo o tráfego Olá pode ser direcionado toohello última parte do espaço para nome de chave de saudação. Se você deve usar os carimbos de hora ou IDs numéricos, um prefixo de id Olá com um hash de 3 dígitos, ou no caso de saudação de carimbos de hora prefixo Olá parte dos segundos de tempo de saudação como ssyyyymmdd. Se as operações de listagem e de consulta forem executadas rotineiramente, escolha uma função de hash que limite o número de consultas. Em outros casos, um prefixo aleatório pode ser suficiente.  
* Para obter informações adicionais sobre Olá particionamento esquema usado no armazenamento do Azure, leia o white paper do SOSP Olá [aqui](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Rede
Enquanto Olá API chama a questão, geralmente as restrições de rede física saudação do aplicativo hello tem um impacto significativo no desempenho. a seguir Olá descreve algumas das limitações que os usuários podem encontrar.  

#### <a name="client-network-capability"></a>Funcionalidade da rede do cliente
##### <a name="subheading2"></a>Produtividade
Largura de banda, problema Olá costuma ser recursos de saudação do cliente hello. Por exemplo, durante uma única conta de armazenamento pode lidar com 10 Gbps ou mais de entrada (consulte [metas de escalabilidade de largura de banda](#sub1bandwidth)), velocidade da rede Olá em uma instância de função de trabalho "Pequeno" só é capaz de aproximadamente 100 Mbps. As instâncias maiores do Azure têm NICs com mais capacidade. Por isso, você pode usar uma instância maior ou mais VMs se precisar de limites de rede mais altos em um único computador. Se você estiver acessando um serviço de armazenamento de um aplicativo local em, hello mesma regra se aplica: entender os recursos de rede de saudação do dispositivo do cliente hello e toohello de conectividade de rede Olá local de armazenamento do Azure e o aprimorá-los conforme necessário ou Crie toowork seu aplicativo em seus recursos.  

##### <a name="subheading3"></a>Qualidade do vínculo
Como é necessário com qualquer uso de rede, as condições de rede que resultam em erros e na perda de pacote desaceleram a taxa de transferência.  Usar WireShark ou NetMon pode ajudar a identificar esse problema.  

##### <a name="useful-resources"></a>Recursos úteis
Para saber mais sobre os tamanhos de máquina virtual e sobre a largura de banda alocada, veja [Tamanhos de VM do Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Tamanhos de VM do Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Local
Em qualquer ambiente distribuído, colocar cliente Olá próximo servidor toohello fornece em um melhor desempenho de saudação. Para acessar o armazenamento do Azure com a menor latência de hello, Olá melhor local para o cliente é dentro Olá mesma região do Azure. Por exemplo, se você tem um site do Azure que usa o armazenamento do Azure, ambos devem estar na mesma região (por exemplo, no oeste dos EUA ou no sudeste asiático). Isso reduz a latência de saudação e Olá custo — no momento da saudação de gravação, uso de largura de banda em uma única região é gratuito.  

Se o cliente de aplicativos não são hospedados no Azure (como aplicativos de dispositivos móveis ou nos serviços de local da empresa), em seguida, novamente colocando conta de armazenamento de saudação em uma região próximo dispositivos toohello poderá acessá-lo, será geralmente reduzir a latência. Se seus clientes estiverem amplamente distribuídos (por exemplo, alguns na América do Norte e alguns na Europa), você deve considerar o uso de várias contas de armazenamento: uma localizada em uma região na América do Norte e outra em uma região na Europa. Isso ajudará a latência tooreduce para usuários em ambas as regiões. Essa abordagem é geralmente mais fácil tooimplement se hello armazenamentos de dados de aplicativo hello tooindividual específico de usuários e não requer replicando dados entre contas de armazenamento.  Para ampla distribuição de conteúdo, recomenda-se um CDN – consulte Olá próxima seção para obter mais detalhes.  

### <a name="subheading5"></a>Distribuição de conteúdo
Às vezes, uma saudação de tooserve aplicativo necessidades de usuários do mesmo conteúdo toomany (por exemplo, um produto de demonstração usado na saudação da home page de um site de vídeo), localizado no hello mesmo ou em várias regiões. Nesse cenário, você deve usar uma rede de entrega de conteúdo (CDN) como CDN do Azure e Olá CDN usaria o armazenamento do Azure como origem de saudação do dados saudação. Ao contrário de uma conta de armazenamento do Azure que existem em uma única região e que não pode entregar conteúdo com baixa latência tooother regiões, o CDN do Azure usa servidores em vários data centers ao redor Olá, mundo. Além disso, uma CDN geralmente tem limites de saída muito maiores do que as contas de armazenamento individuais.  

Para obter mais informações, confira [CDN do Azure](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Usando SAS e CORS
Quando você precisar de código tooauthorize como JavaScript no navegador da web de um usuário ou um dados de tooaccess do aplicativo de telefone celular no armazenamento do Azure, uma abordagem é toouse um aplicativo em função da web como um proxy: dispositivo do usuário Olá autentica com a função de web de saudação, que por sua vez autentica com o serviço de armazenamento de saudação. Dessa forma, você pode evitar a exposição das chaves de conta de armazenamento em dispositivos que não são seguros. No entanto, isso coloca uma grande sobrecarga em função da web de saudação porque todos os dados de saudação transferidos entre o dispositivo do usuário hello e hello serviço de armazenamento precisa passar por função de web hello. Você pode evitar usando uma função web como um proxy para o serviço de armazenamento hello usando assinaturas de acesso compartilhado (SAS), às vezes, em conjunto com cabeçalhos de compartilhamento de recursos entre origens (CORS). Usando a SAS, você pode permitir que solicitações de toomake de dispositivo do usuário diretamente tooa armazenamento de serviço por meio de um token de acesso limitado. Por exemplo, se um usuário quiser tooupload um aplicativo de tooyour foto, sua função web pode gerar e enviar o dispositivo do usuário toohello um token SAS que concede permissão toowrite tooa específico blob ou contêiner para Olá Avançar 30 minutos (após o qual hello token SAS expira).

Normalmente, um navegador não permitirá que o JavaScript em uma página hospedada por um site em um domínio tooperform específico as operações, como um domínio de tooanother "PUT". Por exemplo, se você hospedar uma função web em "contosomarketing.cloudapp.net" e deseja toouse cliente lado JavaScript tooupload uma conta de armazenamento do blob tooyour em "contosoproducts.blob.core.windows.net", Olá do navegador "política de mesma origem" será proíba isso operação. CORS é um recurso de navegador que permite Olá domínio (por esta conta de armazenamento Olá maiusculas) toocommunicate toohello navegador de destino que ele confia solicitações originadas no domínio de origem da saudação (por essa função de web hello maiusculas).  

As duas tecnologias podem ajudar você a evitar cargas e gargalos desnecessários no seu aplicativo Web.  

#### <a name="useful-resources"></a>Recursos úteis
Para obter mais informações sobre SAS, consulte [assinaturas de acesso compartilhado, parte 1: Olá Noções básicas sobre o modelo de SAS](storage-dotnet-shared-access-signature-part-1.md).  

Para obter mais informações sobre CORS, consulte [suporte de compartilhamento de recursos entre origens (CORS) para Olá serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Cache
#### <a name="subheading7"></a>Obtenção de dados
Em geral, obter os dados de um serviço uma única vez é melhor do que obtê-los duas vezes. Considere o exemplo hello de um aplicativo web do MVC em execução em uma função web que já tem recuperados a um blob de 50MB de saudação tooserve de serviço de armazenamento como usuário tooa conteúdo. aplicativo Hello pode, em seguida, recuperar esse mesmo blob toda vez que um usuário solicita a ele, ou ele pode armazenar em cache-localmente toodisk e reutilização Olá em cache versão para solicitações subsequentes de usuário. Além disso, sempre que um usuário solicita dados hello, Olá aplicativo poderia problema obter com um cabeçalho condicional para a hora de modificação, o que seria evitar blob inteiro Olá se ele não tenha sido modificado. Você pode aplicar esse mesmo tooworking de padrão com entidades de tabela.  

Em alguns casos, você pode decidir que seu aplicativo possa assumir o que blob Olá permanece válido por um curto período depois de recuperá-lo, e que durante esse período Olá aplicativo não precisa toocheck se Olá blob foi modificado.

Configuração, pesquisa e outros dados que são sempre usados pelo aplicativo hello são ótimos candidatos para armazenamento em cache.  

Para obter um exemplo de como tooget Olá de toodiscover de propriedades do blob Data da última modificação usando .NET, consulte [definir e recuperar propriedades e metadados](storage-properties-metadata.md). Para saber mais sobre downloads condicionais, consulte [Atualização condicional de uma cópia local de um blob](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Carregamento de dados em lotes
Em algumas situações nos aplicativos, é possível agregar dados localmente e carregá-los em lotes em vez de carregar cada dado imediatamente. Por exemplo, um aplicativo web pode manter um arquivo de log de atividades: Olá aplicativo poderia seja a carregar detalhes de cada atividade conforme ela ocorre como uma entidade de tabela (que exige várias operações de armazenamento) ou ele foi possível salvar a atividade detalhes tooa arquivo de log local e, em seguida, periodicamente, carregar todos os detalhes da atividade como um blob de tooa arquivo delimitado. Se cada entrada de log é de 1KB de tamanho, você pode carregar milhares em uma única transação de "Colocar Blob" (você pode carregar um blob de backup too64MB de tamanho em uma única transação). É claro que, se máquina local Olá falhas de carregamento toohello anterior, potencialmente perderá alguns dados de log: desenvolvedor do aplicativo hello deve projetar a possibilidade de saudação do dispositivo cliente ou falhas de carregamento.  Se precisarem de dados de atividade de saudação toobe baixado para períodos de tempo (não apenas única atividade), blobs são recomendados em tabelas.

### <a name="net-configuration"></a>Configuração .NET
Se usar hello do .NET Framework, esta seção lista várias configurações rápida que você pode usar toomake melhorias significativas no desempenho.  Se estiver usando outros idiomas, verifique toosee se aplicam conceitos semelhantes em seu idioma escolhido.  

#### <a name="subheading9"></a>Aumentar o limite de conexão padrão
No .NET, Olá código a seguir aumenta o limite de conexão do saudação padrão (que geralmente é 2 em um ambiente de cliente ou 10 em um ambiente de servidor) too100. Normalmente, você deve definir número de saudação do hello valor tooapproximately de threads usados por seu aplicativo.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Você deve definir o limite de conexão de saudação antes de abrir todas as conexões.  

Para outras linguagens de programação, consulte toodetermine de documentação do idioma como limitar a conexão de saudação tooset.  

Para obter mais informações, consulte Olá postagem de blog [serviços da Web: conexões simultâneas](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>Aumentar o mínimo dos Threads de ThreadPool, caso esteja usando código síncrono com tarefas assíncronas
Esse código aumentará Olá min threads do pool:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Para saber mais, veja [Método ThreadPool.SetMinThreads](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Aproveitar a coleta de lixo do .NET 4.5
Use o .NET 4.5 ou posterior para Olá cliente aplicativo tootake aproveitar as melhorias de desempenho na coleta de lixo do servidor.

Para obter mais informações, consulte o artigo Olá [uma visão geral das melhorias de desempenho no .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Paralelismo não associado
Enquanto o paralelismo pode ser ótimo para desempenho, ter cuidado usando várias partições de paralelismo não vinculado (sem limite no número de saudação de threads de e/ou solicitações paralelas) tooupload ou baixar dados usando várias tooaccess de trabalhadores (contêineres, filas, ou partições de tabela) em Olá a mesma conta de armazenamento ou tooaccess vários itens no hello mesma partição. Se paralelismo Olá é não vinculado, seu aplicativo pode exceder os recursos do dispositivo do cliente de saudação ou Olá metas de escalabilidade da conta de armazenamento resultando em latências mais longas e limitação.  

### <a name="subheading13"></a>Ferramentas e bibliotecas cliente para armazenamento
Sempre use ferramentas e bibliotecas de cliente hello mais recentes fornecido pela Microsoft. No momento da saudação de gravação, há bibliotecas de cliente disponíveis para .NET, Windows Phone, Windows Runtime, Java e C++, bem como bibliotecas de visualização para outros idiomas. Além disso, a Microsoft liberou cmdlets do PowerShell e os comandos da CLI do Azure para trabalhar com o Armazenamento do Azure. Microsoft ativamente desenvolve essas ferramentas com o desempenho em mente, mantém o toodate com versões mais recentes de serviço hello e garante a lidar com muitas Olá comprovada práticas recomendadas de desempenho internamente.  

### <a name="retries"></a>Novas tentativas
#### <a name="subheading14"></a>Limitação/Servidor ocupado
Em alguns casos, Olá serviço de armazenamento pode acelerar o seu aplicativo ou pode simplesmente ser tooserve não é possível Olá solicitação devido a condição transitória toosome e retornar uma mensagem de "503 servidor ocupado" ou "tempo limite de 500".  Isso pode acontecer se qualquer uma das metas de escalabilidade hello está se aproximando do seu aplicativo, ou se o sistema Olá é rebalanceamento tooallow seus dados particionados para maior taxa de transferência.  aplicativo de cliente Hello normalmente deverá repetir a operação de saudação que causa um erro: tentativa de saudação mesma solicitação mais tarde pode ter êxito. No entanto, se o serviço de armazenamento de saudação está otimizando seu aplicativo porque ele está excedendo metas de escalabilidade, ou mesmo se o serviço de saudação foi solicitação de saudação tooserve não é possível por algum outro motivo, tentativas agressivas geralmente faz pior do problema de saudação. Por esse motivo, você deve usar um (Olá cliente bibliotecas padrão toothis comportamento) de retirada exponencial. Por exemplo, o aplicativo pode fazer uma nova tentativa em 2 segundos, 4 segundos, 10 segundos e 30 segundos para então abandonar o processo. Esse comportamento resulta em seu aplicativo significativamente reduzindo sua carga no serviço de saudação em vez de agrava ainda mais os problemas.  

Observe que os erros de conectividade podem ser repetidos imediatamente, porque eles não são resultado de saudação de limitação e são esperado toobe transitório.  

#### <a name="subheading15"></a>Erros sem nova tentativa
bibliotecas de saudação do cliente estão cientes de que os erros são capazes de repetição e quais não são. No entanto, se você estiver escrevendo seu próprio código em relação ao armazenamento Olá API REST, lembre-se há alguns erros que você não deverá tentar novamente: por exemplo, o erro 400 (solicitação incorreta) resposta indica que esse aplicativo de cliente hello enviou uma solicitação que não pôde ser processada porque ele não estava no formato esperado. Reenviar desta solicitação resultará Olá mesma resposta sempre, portanto não faz sentido em tentar novamente a ele. Se você estiver escrevendo seu próprio código em relação ao armazenamento Olá API REST, lembre-se de média e hello tooretry de maneira correta de códigos de erro que hello (ou não) para cada um deles.  

#### <a name="useful-resources"></a>Recursos úteis
Para obter mais informações sobre códigos de erro de armazenamento, consulte [Status e códigos de erro](http://msdn.microsoft.com/library/azure/dd179382.aspx) no site do Microsoft Azure hello.  

## <a name="blobs"></a>Blobs
Em adição toohello comprovadas práticas recomendadas para [todos os serviços](#allservices) descrito anteriormente, a seguir Olá práticas comprovadas se aplicam especificamente o serviço de blob toohello.  

### <a name="blob-specific-scalability-targets"></a>Metas de escalabilidade específicas do blob
#### <a name="subheading46"></a>Vários clientes que acessam um único objeto simultaneamente
Se você tiver um grande número de clientes que acessam um único objeto ao mesmo tempo, você precisará tooconsider por metas de escalabilidade de conta de armazenamento e objeto. número exato de saudação de clientes que podem acessar um único objeto irá variar dependendo de fatores como o número de saudação de clientes que solicitam o objeto Olá simultaneamente, tamanho de saudação do objeto hello, rede condições etc.

Se o objeto Olá pode ser distribuído por meio de um CDN, como imagens ou vídeos atendidas a partir de um site, em seguida, você deve usar um CDN. Consulte [aqui](#subheading5).

Em outros cenários, como Simulações científicas onde dados saudação são confidenciais, você tem duas opções. Olá primeiro é toostagger access do sua carga de trabalho tal que Olá objeto é acessado por um período de tempo vs que está sendo acessado simultaneamente. Como alternativa, você pode copiar temporariamente as contas de armazenamento toomultiple objeto Olá aumentando Olá IOPS total por objeto e em contas de armazenamento. Em testes limitados descobrimos que aproximadamente 25 VMs simultaneamente podem baixar um blob de 100GB em paralelo (cada VM foi paralelizar download hello usando 32 encadeamentos). Se você tiver 100 clientes que precisam de objeto do tooaccess Olá, primeiro copie-tooa segunda conta de armazenamento e, em seguida, ter Olá primeiros 50 VMs acesso Olá primeiro blob e Olá segundo 50 VMs acesso Olá segundo blob. Os resultados variam de acordo com o comportamento dos seus aplicativos e, portanto, você deve fazer testes durante o design. 

#### <a name="subheading16"></a>Largura de banda e operações por blob
Você pode ler ou gravar tooa único blob em backup tooa no máximo 60 MB/segundo (Isso é aproximadamente 480 Mbps que excede os recursos de saudação de várias redes de lado do cliente (incluindo Olá NIC física no dispositivo de cliente Olá). Além disso, um único blob dá suporte para até too500 solicitações por segundo. Se você tiver vários clientes que precisam de tooread hello mesmo blob e você poderá exceder esses limites, considere o uso de uma CDN para distribuir blob hello.  

Para saber mais sobre a taxa de transferência alvo para os blobs, consulte [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Copiando e movendo blobs
#### <a name="subheading17"></a>Copiar blob
armazenamento Olá REST API versão 2012-02-12 introduzido blobs de toocopy capacidade útil Olá entre contas: um aplicativo cliente pode instruir toocopy de serviço de armazenamento de saudação um blob de outra origem (possivelmente em outra conta de armazenamento) e deixe Olá serviço executar cópia Olá assincronamente. Isso pode reduzir significativamente a largura de banda Olá necessária para o aplicativo hello quando você está migrando dados de outras contas de armazenamento porque você não precisa toodownload e carregar dados de saudação.  

Uma consideração, no entanto, é que, ao copiar entre contas de armazenamento, não há nenhuma garantia de vez em quando a cópia de saudação será concluída. Se seu aplicativo precisa toocomplete um blob rapidamente copiar sob seu controle, pode ser melhor blob de saudação toocopy por download tooa VM e, em seguida, carregá-los toohello de destino.  Para previsibilidade completa nessa situação, certifique-se de que a cópia de saudação é executada por uma VM em execução no hello mesma região do Azure, caso contrário, as condições de rede pode (e provavelmente será) afetam o desempenho de cópia.  Além disso, você pode monitorar progresso de saudação de uma cópia assíncrona programaticamente.  

Observe que copia em Olá a mesma conta de armazenamento em si geralmente são concluídas rapidamente.  

Para saber mais, consulte [Copiar Blob](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>Usar AzCopy
equipe de armazenamento do Azure Olá lançou uma ferramenta de linha de comando "AzCopy" que é destinado toohelp com bulk transferindo muitos blobs para, de e em contas de armazenamento.  Essa ferramenta foi otimizada para esse cenário e pode alcançar altas taxas de transferência.  Ela deve ser usada para baixar e carregar itens, bem como para copiar cenários, em massa. toolearn mais sobre ele e baixá-lo, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Serviço de importação/exportação do Azure
Para grandes volumes de dados (mais de 1TB), Olá armazenamento do Azure oferece Olá serviço de importação/exportação, que permite o upload e download do armazenamento de blob pelo envio de unidades de disco rígido.  Você pode colocar seus dados em um disco rígido e enviá-lo tooMicrosoft para carregar ou enviar um disco rígido em branco tooMicrosoft toodownload de dados.  Para obter mais informações, consulte [usar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](storage-import-export-service.md).  Isso pode ser muito mais eficiente que Upload/download esse volume de dados pela rede hello.  

### <a name="subheading20"></a>Uso de metadados
serviço de blob Olá dá suporte a solicitações head, que podem incluir metadados sobre o blob de saudação. Por exemplo, se seu aplicativo necessário dados EXIF Olá fora de uma foto, ele pode recuperar foto hello e extraí-lo. toosave largura de banda e melhorar o desempenho, seu aplicativo armazena os dados EXIF Olá nos metadados do blob hello quando o aplicativo hello carregado foto Olá: você pode recuperar dados EXIF Olá nos metadados usando apenas uma solicitação HEAD, economizando largura de banda significativa e tempo de processamento de saudação necessária tooextract Olá dados EXIF é de leitura de blob de saudação cada vez. Isso pode ser útil em cenários onde você precisa apenas Olá metadados e não Olá conteúdo completo de um blob.  Observe que apenas 8 KB de metadados podem ser armazenado por blob (serviço de saudação não aceitará uma solicitação toostore maior), para que se dados saudação não couberem em tamanho, você não pode ser capaz de toouse essa abordagem.  

Para obter um exemplo de como tooget metadados do blob usando .NET, consulte [definir e recuperar propriedades e metadados](storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Carregamento rápido
blobs tooupload rápidas, Olá primeira pergunta tooanswer é: são você carregar um blob ou muitas?  Use Olá abaixo orientação toodetermine Olá método correto toouse dependendo do cenário.  

#### <a name="subheading21"></a>Carregamento rápido de um blob grande
tooupload rapidamente de um único grande blob, o aplicativo cliente deve carregar seus blocos ou páginas em paralelo (sendo atento alvos de escalabilidade de saudação para blobs individuais e conta de armazenamento hello como um todo).  Observe que bibliotecas de fornecida pela Microsoft RTM do cliente de armazenamento oficiais hello (.NET, Java) têm Olá capacidade toodo isso.  Para cada uma das bibliotecas de hello, use Olá abaixo do nível de saudação tooset especificado do objeto ou propriedade de simultaneidade:  

* .NET: ParallelOperationThreadCount de conjunto em um toobe de objeto BlobRequestOptions usado.
* Java/Android: usar BlobRequestOptions.setConcurrentRequestCount()
* Node. js: Use parallelOperationThreadCount ou opções de solicitação hello ou no serviço de blob hello.
* C++: Método blob_request_options:: set_parallelism_factor usar hello.

#### <a name="subheading22"></a>Carregamento rápido de diversos blobs
tooupload muitos blobs rapidamente, carregar blobs em paralelo. Isso é mais rápido que carregar blobs único por vez com carregamentos de bloco paralelo porque ela espalha Olá carregamento por várias partições saudação do serviço de armazenamento. Cada blob dá suporte a uma taxa de transferência de 60 MB/segundo (aproximadamente, 480 Mbps). No momento da saudação de gravação, uma conta com base nos EUA LRS dá suporte para até too20 Gbps de entrada que é muito mais do que a taxa de transferência Olá suportada por um blob individual.  [AzCopy](#subheading18) executa os carregamentos em paralelo por padrão e é a opção recomendada nesse caso.  

### <a name="subheading23"></a>Escolhendo o tipo correto de saudação do blob
O armazenamento do Azure oferece suporte a dois tipos de blob: blobs de *página* e blobs de *blocos*. Para um cenário de uso específico, a escolha do tipo de blob afetará o desempenho de saudação e a escalabilidade de sua solução. Blobs de bloco são apropriados quando desejar grandes quantidades de tooupload de dados com eficiência: por exemplo, talvez seja necessário um aplicativo cliente fotos tooupload ou armazenamento de vídeo tooblob. Blobs de página são apropriados se o aplicativo hello precisar tooperform as gravações aleatórias em dados Olá: por exemplo, os VHDs do Azure são armazenados como blobs de página.  

Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tabelas
Em adição toohello comprovadas práticas recomendadas para [todos os serviços](#allservices) descrito anteriormente, a seguir Olá práticas comprovadas se aplicam especificamente o serviço de tabela toohello.  

### <a name="subheading24"></a>Metas de escalabilidade específicas da tabela
Limitações de largura de banda de toohello de adição de uma conta de armazenamento inteira, tabelas tem Olá após o limite de escalabilidade específico.  Observe que o sistema Olá carregará o saldo conforme aumenta o tráfego, mas se o tráfego tem intermitências repentinas, você não pode ser capaz de tooget esse volume de taxa de transferência imediatamente.  Se seu padrão tem intermitências, você deve esperar a limitação de toosee e/ou tempos limite durante Olá intermitência como serviço de armazenamento de saudação automaticamente balanceia a carga da sua tabela.  Aumentando lentamente geralmente tem resultados melhores porque ele oferece o saldo de tooload Olá sistema tempo adequadamente.  

#### <a name="entities-per-second-account"></a>Entidades por segundo (conta)
limite de escalabilidade Olá para acessar tabelas é too20, 000 (1KB cada) de entidades por segundo para uma conta.  Em geral, cada entidade inserida, atualizada, excluída ou verificada é computada nessa meta.  Assim, uma inserção em lote com 100 entidades é computada como 100 entidades.  Uma consulta que verifica 1000 entidades e retorna apenas 5 é computada como 1000 entidades.  

#### <a name="entities-per-second-partition"></a>Entidades por segundo (partição)
Em uma única partição, Olá meta de escalabilidade para acessar tabelas é 2.000 entidades (1KB cada) por segundo, usando Olá contagem mesmo conforme descrito na seção anterior hello.  

### <a name="configuration"></a>Configuração
Esta seção lista várias configurações rápida que você pode usar toomake melhorias de desempenho significativas no serviço de tabela hello:  

#### <a name="subheading25"></a>Usar JSON
A partir da versão do serviço de armazenamento 2013-08-15, o serviço de tabela Olá oferece suporte usando JSON em vez do formato do hello AtomPub baseado em XML para a transferência de dados da tabela. Isso pode reduzir o tamanho de carga em 75% e pode melhorar significativamente o desempenho de saudação do seu aplicativo.

Para obter mais informações, consulte Olá postagem [tabelas do Microsoft Azure: apresentando o JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) e [formato de carga para operações do serviço tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Desativação do Nagle
Algoritmo do Nagle é amplamente implementado em redes TCP/IP como um meio de desempenho de rede de tooimprove. No entanto, ele não é ideal em todas as circunstâncias (como em ambientes altamente interativos). Para o armazenamento do Azure, algoritmo do Nagle tem um impacto negativo no desempenho de saudação do serviços de tabela e fila de solicitações toohello e você deverá desabilitá-la se possível.  

Para obter mais informações, consulte nossa postagem de blog [algoritmo do Nagle não é amigável para solicitações de pequenas](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), que explica por que o algoritmo do Nagle mal interage com solicitações de tabela e fila e mostra como toodisable-lo no seu cliente aplicativo.  

### <a name="schema"></a>Esquema
Como você declara e consulta seus dados é Olá maiores único fator que afeta o desempenho de saudação do serviço de tabela de saudação. Embora cada aplicativo seja único, esta seção descreve algumas práticas gerais comprovadas relacionadas:  

* Ao design da tabela
* A consultas eficientes
* A atualizações de dados eficientes  

#### <a name="subheading27"></a>Tabelas e partições
As tabelas são divididas em partições. Cada entidade armazenada em uma partição compartilhamentos Olá a mesma chave de partição e tem um tooidentify de chave de linha exclusivo-la dentro dessa partição. As partições trazem benefícios, mas também criam limites de escalabilidade.  

* Benefícios: Você pode atualizar entidades na mesma partição em uma transação única, atômica, o lote que contém as operações de armazenamento separado de too100 (limite de tamanho total de 4MB) de saudação. Supondo que Olá o mesmo número de entidades toobe de recuperados, você também pode consultar dados em uma única partição com mais eficiência do que os dados que abrange partições (embora continue lendo para obter mais recomendações sobre consultar dados de tabela).
* Limite de escalabilidade: tooentities de acesso armazenada em uma única partição não pode ser com balanceamento de carga porque partições oferecem suporte a transações em lote atômicas. Por esse motivo, meta de escalabilidade de saudação para uma partição de tabela individual é menor do que o serviço de tabela hello como um todo.  

Devido a essas características de tabelas e partições, você deve adotar Olá princípios de design a seguir:  

* Dados que seu aplicativo cliente atualizado com frequência ou consultados Olá mesma unidade lógica de trabalho deve estar localizada em Olá mesma partição.  Isso pode ser porque seu aplicativo está agregando gravações, ou porque você deseja tootake proveito das operações em lote atômicas.  Além disso, é possível consultar os dados em uma única partição com mais eficiência do que fazer a consulta em diversas partições.
* Dados que seu aplicativo cliente não inserir/atualizar ou consultar em Olá mesma unidade lógica de trabalho (única consulta ou atualização em lotes) deve estar localizada em partições separam.  Uma observação importante é que não há nenhum toohello limitar o número de chaves de partição em uma única tabela, portanto ter milhões de chaves de partição não é um problema e não afetará o desempenho.  Por exemplo, se seu aplicativo for um site da Web popular com logon de usuário, usar Olá Id de usuário como chave de partição Olá poderia ser uma boa opção.  

#### <a name="hot-partitions"></a>Partições mais acessadas
Uma partição ativa é aquela que está recebendo uma porcentagem desproporcional de conta de tooan tráfego hello e não pode ser com balanceamento de carga porque é uma única partição.  Em geral, essas partições são criadas de duas formas:  

##### <a name="subheading28"></a>Padrões somente anexar e somente incluir
Olá "Somente acréscimo" padrão é um onde todos os (ou quase todos) de saudação tráfego tooa fornecido PK aumentam e diminui o acordo toohello hora atual.  Um exemplo é se o aplicativo usou Olá data atual como uma chave de partição para dados de log.  Isso resulta em todas as inserções de saudação vai toohello última partição na tabela e sistema Olá não pode balancear a carga porque todos Olá gravações estão indo toohello final da tabela.  Se volume Olá da partição de toothat de tráfego excede meta de escalabilidade de nível de partição de hello, ele resultará na limitação.  É melhor tooensure que toomultiple partições, o tráfego será enviado solicitações tooenable Olá de balanceamento de carga em sua tabela.  

##### <a name="subheading29"></a>Dados de tráfego intenso
Se os resultados de esquema de particionamento em uma única partição que tem apenas dados que é muito mais usados que as outras partições, você também poderá ver a limitação conforme meta de escalabilidade Olá para uma única partição se aproxima da partição.  É melhor toomake-se de que os resultados do esquema de partição em nenhum partição próximo metas de escalabilidade de saudação.  

#### <a name="querying"></a>Consultas
Esta seção descreve as práticas comprovadas para consultar o serviço de tabela de saudação.  

##### <a name="subheading30"></a>Escopo de consulta
Há várias maneiras toospecify Olá variedade de tooquery de entidades.  a seguir Olá é uma discussão de usos de saudação de cada.  

Em geral, evite verificações (consultas maiores do que uma única entidade), mas se você deve examinar, tente tooorganize seus dados para que as varreduras recuperam dados de saudação sem verificação ou retornar uma quantidade significativa de entidades que não é necessário.  

###### <a name="point-queries"></a>Consultas pontuais
A consulta recupera exatamente uma entidade. Ele faz isso especificando a chave de partição hello e chave de linha de saudação tooretrieve de entidade. Essas consultas são muito eficientes e você deve usá-las sempre que possível.  

###### <a name="partition-queries"></a>Consultas às partições
Esse tipo de consulta recupera um conjunto de dados que tem uma chave de partição em comum. Normalmente, a consulta de saudação especifica um intervalo de valores de chave de linha ou um intervalo de valores para algumas propriedades de entidade na chave de partição tooa adição. Elas são menos eficientes do que as consultas pontuais e devem ser usados com critério.  

###### <a name="table-queries"></a>Consultas às tabelas
Esse tipo de consulta recupera um conjunto de entidades que não tem uma chave de partição em comum. Essas consultas não são eficientes e você deve evitá-las sempre que possível.  

##### <a name="subheading31"></a>Densidade de consulta
Outro fator chave na eficiência da consulta é o número de saudação de entidades retornadas como toohello em comparação com o número de entidades toofind digitalizados hello retornada definido. Se o aplicativo executa uma consulta de tabela com um filtro para um valor de propriedade que apenas 1% dos compartilhamentos de dados hello, Olá consulta examinará 100 entidades para cada uma entidade que ele retorna. Hello metas de escalabilidade de tabela abordadas anteriormente todos se relacionam toohello número de entidades examinados e Olá não o número de entidades retornadas: uma densidade baixa de consulta pode facilmente fazer Olá toothrottle de serviço de tabela de seu aplicativo porque ele deve verificar tantas entidade de saudação de tooretrieve entidades que está procurando.  Consulte a seção de saudação abaixo em [desnormalização](#subheading34) para obter mais informações sobre como tooavoid isso.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Limitando Olá a quantidade de dados retornados
###### <a name="subheading32"></a>Filtragem
Quando você souber que uma consulta retornará entidades que não é necessário no aplicativo de cliente hello, considere o uso de um tamanho de saudação do filtro tooreduce de saudação retornada um conjunto de. Ao entidades Olá retornado não toohello cliente ainda são contadas Olá limites de escalabilidade, desempenho do seu aplicativo será melhorar devido ao tamanho de carga de rede Olá reduzido e Olá redução do número de entidades que seu aplicativo cliente deve processar .  Consulte acima Observação sobre [consulta densidade](#subheading31), porém – metas de escalabilidade Olá relacionam toohello número de entidades verificado, para uma consulta que filtra as muitas entidades ainda pode resultar na limitação, mesmo se algumas entidades são retornadas.  

###### <a name="subheading33"></a>Projeção
Se seu aplicativo cliente precisa apenas um conjunto limitado de propriedades de entidades de saudação em sua tabela, você pode usar o tamanho de saudação toolimit projeção de saudação retornada um conjunto de dados. Com filtragem, isso ajuda a carga de rede tooreduce e processamento de cliente.  

##### <a name="subheading34"></a>Desnormalização
Ao contrário de trabalhar com bancos de dados relacionais, hello práticas comprovadas para consultar os dados da tabela com eficiência levam toodenormalizing seus dados. Ou seja, duplicando Olá os mesmos dados em várias entidades (uma para cada chave, você pode usar dados de saudação toofind) toominimize número de saudação de entidades que uma consulta deve verificar toofind Olá dados Olá cliente necessidades, em vez de ter tooscan grandes números de entidades toofind dados de saudação seu aplicativo precisa.  Por exemplo, em um site de comércio eletrônico, talvez você queira toofind uma ordem tanto por ID de cliente de saudação (dar pedidos do cliente) e pela data da saudação (me dar ordens em uma data).  No armazenamento de tabela, é melhor entidade de saudação toostore (ou uma referência tooit) duas vezes, uma vez com o nome da tabela, PK e trabalho Localizando toofacilitate por ID do cliente, uma vez toofacilitate localizá-lo por data de saudação.  

#### <a name="insertupdatedelete"></a>Inserção/atualização/exclusão
Esta seção descreve as práticas comprovadas para modificar entidades armazenadas no serviço de tabela de saudação.  

##### <a name="subheading35"></a>Envio em lote
As transações em lotes são conhecidas como transações de grupo de entidade (ETG) no armazenamento do Azure; todas as operações de saudação dentro de um ETG devem estar em uma única partição em uma única tabela. Sempre que possível, use ETGs tooperform inserções, atualizações e exclusões em lotes. Isso reduz o número de saudação de viagens de ida e volta do seu servidor de toohello do aplicativo cliente, reduz Olá número de transações cobráveis (uma ETG contará como uma única transação para fins de cobrança e pode conter as operações de armazenamento too100) e habilita atômico atualizações (todas as operações de êxito ou todos falham dentro de um ETG). Os ambientes com altos níveis de latência, como os dispositivos móveis, veem muitos benefícios no uso das ETGs.  

##### <a name="subheading36"></a>Upsert
Use as operações de tabela **Upsert** sempre que possível. Há dois tipos de **Upsert** e os dois podem ser mais eficientes do que as operações tradicionais **Insert** e **Update**:  

* **InsertOrMerge**: Use essa opção quando quiser tooupload um subconjunto das propriedades da entidade hello, mas não tiver certeza se entidade Olá já existe. Se existir a entidade hello, essa chamada atualiza propriedades de saudação incluídas no hello **Upsert** operação e deixa todas as propriedades existentes, como eles são, se hello entidade não existe, ele insere Olá nova entidade. Isso é semelhante projeção toousing em uma consulta, em que você só precisa de propriedades de saudação tooupload que estão alterando.
* **InsertOrReplace**: Use essa opção quando desejar que tooupload uma entidade totalmente nova, mas você não tiver certeza se ele já existe. Você deve usar isso apenas quando você sabe que Olá carregado recentemente a entidade está totalmente correto porque ela substitui completamente a entidade antiga hello. Por exemplo, você deseja tooupdate entidade de saudação que armazena o local atual do usuário, independentemente de ou não aplicativo hello armazenou anteriormente dados de local para o usuário Olá; Olá nova entidade de local é concluída, e todas as informações de qualquer entidade anterior não é necessário.

##### <a name="subheading37"></a>Armazenamento de séries de dados em uma única entidade
Às vezes, um aplicativo armazena uma série de dados que frequentemente precisa tooretrieve todos de uma vez: por exemplo, um aplicativo pode acompanhar o uso de CPU ao longo do tempo em ordem tooplot um gráfico sem interrupção de dados de saudação do hello últimas 24 horas. Uma abordagem é a entidade de uma tabela de toohave por hora, com cada entidade que representa uma hora específica e armazenar o uso de CPU Olá para essa hora. tooplot esses dados, o aplicativo hello precisam de entidades de saudação tooretrieve mantendo dados Olá Olá 24 horas mais recentes.  

Como alternativa, seu aplicativo pode armazenar o uso de CPU de saudação para cada hora como uma propriedade separada de uma única entidade: tooupdate a cada hora, seu aplicativo pode usar um único **InsertOrMerge Upsert** pedir tooupdate valor de Olá Olá hora mais recente. dados de saudação tooplot, o aplicativo hello só precisa tooretrieve uma única entidade em vez de 24, tornando-se para uma consulta muito eficiente (consulte acima discussão sobre [escopo de consulta](#subheading30)).

##### <a name="subheading38"></a>Armazenando dados estruturados em blobs
Às vezes parece que os dados estruturados devem ser dispostos em tabelas, mas os intervalos das entidades sempre são recuperados em conjunto e podem ser inseridos em lote.  Um bom exemplo disso são os arquivos de log.  Nesse caso, você pode considerar diversos minutos de log como um lote, inseri-los e recuperar diversos minutos de uma só vez.  Nesse caso, para o desempenho, é melhor blobs toouse em vez de tabelas, desde que você pode reduzir significativamente Olá número de objetos gravados/retornados, bem como Olá normalmente o número de solicitações que precisam feitas.  

## <a name="queues"></a>Filas
Em adição toohello comprovadas práticas recomendadas para [todos os serviços](#allservices) descrito anteriormente, a seguir Olá práticas comprovadas se aplicam especificamente o serviço de fila de toohello.  

### <a name="subheading39"></a>Limites de escalabilidade
Uma única fila pode processar aproximadamente 2.000 mensagens (1 KB cada) por segundo (cada contagem AddMessage, GetMessage e DeleteMessage como uma mensagem aqui). Se isso for insuficiente para seu aplicativo, você deve usar várias filas e distribuir mensagens de saudação entre eles.  

Exiba as metas atuais de escalabilidade em [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md).  

### <a name="subheading40"></a>Desativação do Nagle
Consulte a seção de saudação na configuração de tabela que descreve o algoritmo de Nagle hello – algoritmo de Nagle de saudação é geralmente negativamente o desempenho de saudação de solicitações de fila e, em seguida, você deverá desabilitá-la.  

### <a name="subheading41"></a>Tamanho da mensagem
O desempenho e a escalabilidade da fila diminui quando o tamanho de mensagem aumenta. Você deve colocar somente Olá Olá receptor necessidades de informações em uma mensagem.  

### <a name="subheading42"></a>Recuperação de lote
Você pode recuperar as mensagens de too32 de uma fila em uma única operação. Isso pode reduzir o número de saudação de idas e voltas do aplicativo de cliente hello, que é especialmente útil em ambientes, como dispositivos móveis, com alta latência.  

### <a name="subheading43"></a>Intervalo de sondagem de fila
A maioria dos aplicativos a sondagem para mensagens de uma fila, que pode ser uma das fontes de saudação maior de transações para o aplicativo. Selecione o intervalo de sondagem criteriosamente: com muita frequência de sondagem pode fazer com que seu aplicativo tooapproach alvos de escalabilidade de saudação para fila de saudação. No entanto, em 200.000 transações para US $0,01 (em tempo de saudação de gravação), um único processador quando a cada segundo por um mês custaria menos de 15 centavos assim o custo de sondagem não é normalmente um fator que afeta sua opção de intervalo de sondagem.  

Para obter informações atualizadas sobre custos, confira [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
Você pode usar **UpdateMessage** tooincrease Olá invisibilidade tooupdate ou tempo limite de informações de estado de uma mensagem. Embora seja eficiente, lembre-se de que cada **UpdateMessage** operação conta para a meta de escalabilidade de saudação. No entanto, isso pode ser uma abordagem muito mais eficiente do que um fluxo de trabalho que passa um trabalho de uma fila toohello em seguida, como cada etapa de trabalho de saudação é concluída. Usando Olá **UpdateMessage** operação permite que a mensagem de toohello aplicativo toosave Olá trabalho estado e continue a trabalhar, em vez de mensagem de saudação do enfileiramento de mensagens novamente para a próxima etapa saudação do trabalho Olá toda vez que uma etapa for concluída.  

Para obter mais informações, consulte o artigo Olá [como: alterar o conteúdo de saudação de uma mensagem na fila](storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Arquitetura do aplicativo
Você deve usar filas toomake a arquitetura do aplicativo escalonável. lista a seguir de saudação algumas maneiras de usar filas toomake seu aplicativo mais escalonável:  

* Você pode usar listas de pendências de toocreate de filas de trabalho para processamento e suavizam as cargas de trabalho em seu aplicativo. Por exemplo, você pode enfileirar solicitações de trabalho intensivas de processador do tooperform de usuários como redimensionar imagens carregadas.
* Você pode usar partes de toodecouple filas de seu aplicativo para que você pode dimensionar independentemente. Por exemplo, um front-end da Web pode colocar os resultados de pesquisa dos usuários em uma fila para análise posterior e armazenamento. Você pode adicionar que mais tooprocess de instâncias de função de trabalho Olá dados da fila conforme necessário.  

## <a name="conclusion"></a>Conclusão
Neste artigo, alguns hello mais comuns, discutido comprovadas práticas recomendadas para otimizar o desempenho ao usar o armazenamento do Azure. Podemos incentivar cada tooassess de desenvolvedor do aplicativo seu aplicativo em relação a cada Olá acima práticas e considerar agindo em Olá recomendações tooget excelente desempenho para os aplicativos que usam o armazenamento do Azure.
